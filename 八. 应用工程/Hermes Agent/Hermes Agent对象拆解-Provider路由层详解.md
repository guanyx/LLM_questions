# Hermes 是怎么把一次请求解析成 Runtime Provider 的

很多人第一次看 Hermes 的 Provider 层，会以为它在做一件很简单的事：选模型。

但如果沿着一次真实请求的解析链路往下看，结论就会变得很明确：它真正做的不是“从几家厂商里挑一个”，而是把一组互相竞争的配置、协议、凭证和故障路径，收敛成一份上层可以直接依赖的运行时结果。

这份结果，Hermes 里叫 **Runtime Provider**。

理解这件事很重要，因为 2026 年的 Agent 已经不再活在“单模型、单 endpoint、单协议”的世界里。上层 Agent Loop 之所以还能像在和一个稳定系统打交道，前提是中间已经有一层把这些复杂度吸收掉了。Hermes 的 Provider 层，承担的正是这部分工作。

## 一、先从一句真实请求开始

假设你在 CLI 里输入一句话：

“帮我修一下这个 Python 项目的测试。”

这时环境里同时存在几条候选线路：

- `config.yaml` 里保存的是 `provider: custom`
- 同一份配置里还保存了 `base_url = https://api.openai.com/v1`
- 机器上同时还有一组 OpenRouter 的环境变量
- 你还配置过一个公司内部网关，它也兼容 OpenAI 风格协议
- 系统另外还准备了一条 fallback provider

这里最常见的误解，是把“这轮该走谁”理解成一个 provider 字符串问题。

但真正的问题并不在这里。

真正的问题是：**这轮请求到底由谁决定、最后落到哪个 endpoint、该带哪把 key、说哪种 API 语言，失败以后又先在哪一层恢复。**

Hermes 的 Provider 层，就是专门把这些问题集中处理的地方。

## 二、第一步不是建 client，而是先判断谁有资格决定这次请求

一条请求进来以后，Hermes 不会立刻创建模型 client。

它先要解决一个更基础的问题：**这轮请求的控制权到底在谁手里。**

对应逻辑在 [resolve_requested_provider](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L208-L224)。

这一步的顺序很明确：

- 显式参数优先
- 然后看 `config.yaml`
- 再往下才是环境变量
- 最后才轮到 `auto`

这个顺序看起来像小事，但它决定的是系统优先尊重哪一层输入。

如果把环境变量放在持久配置前面，系统就会进入一种很危险的状态：用户上次临时 export 过什么，今天就可能覆盖真正保存下来的默认选择。

回到这个例子里，因为这次没有显式传 `--provider`，也没有临时传 `--base-url`，Hermes 会先看 `config.yaml`，发现里面已经明确写着两件事：

- `provider = custom`
- `base_url = https://api.openai.com/v1`

到这一步，OpenRouter 的环境变量和公司内部网关都还不能参与本轮解析。不是它们不可用，而是它们**此刻不在优先路径上**。

第一层收口，就是先把“这一轮优先采用哪一层配置”定下来。

## 三、第二步不是认品牌，而是先认内部身份

接下来 Hermes 会先把这次请求归一成系统内部承认的身份。

这里对应的是 **Provider Identity**。

在这个例子里，Hermes 先认出来的不是 `openai`，而是 `custom`。相关逻辑在 [resolve_provider](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/auth.py#L841-L844)。

系统内部首先要知道“这轮请求属于哪条逻辑路径”，而不是一开始就根据 URL 的外观，直接把它并到某个更大的厂商标签下。

如果这一步处理得不够严格，后面很容易出现一种混乱：

- 表面上是 `custom`
- 运行时又想按 `openrouter` 的逻辑取 key
- 协议判断又想按 `openai` 的风格走

最后整条线路就会进入“外表相似，因此共用同一套处理逻辑”的状态。

Hermes 不这么做。它先把逻辑身份固定下来，然后后续解析都围绕这个身份继续展开。

换句话说，先确认请求所属的逻辑线路，再继续做后续绑定。

## 四、第三步去查静态档案，但这时还没得到最终结果

身份统一以后，Hermes 会去拿这家 provider 的静态定义，也就是 **ProviderDef**。

相关结构在 [ProviderDef](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/providers.py#L136-L149) 和 [get_provider](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/providers.py#L271-L334)。

这里最容易误解的一点是：`ProviderDef` 不是运行时结果。

它更像一张静态档案，回答的是：

- 这家 provider 平时长什么样
- 默认协议轮廓是什么
- 认证方式通常是什么
- 大概会从哪些地方拿配置

但它不直接回答“这次请求最后到底发到哪里”。

这也是为什么 Hermes 要把 **Provider Identity**、**ProviderDef** 和 **Runtime Provider** 拆开。

如果把这三件事混成一层，代码表面上会显得更短，实际上会把静态知识和动态绑定搅在一起。系统刚开始还能运行，但等 provider、协议和 fallback 路径都增多以后，整个调用链就会越来越难分析。

## 五、真正决定结果的是第四步：组装 Runtime Provider

真正决定结果的动作发生在 [resolve_runtime_provider](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L581-L803)。

到了这里，Hermes 才把前面几层信息真正合成一份可执行结果。

这份结果至少要回答四个问题：

- 最终 `base_url` 是什么
- 这轮请求该带哪把 `api_key`
- 该走哪种 `api_mode`
- 如果失败，后面挂着哪条恢复路径

回到这个例子里，Hermes 会继续把 `provider = custom` 和保存下来的 `base_url` 一起带进运行时解析。真正有决定性的，不再是“它像不像 OpenAI”，而是“这轮请求最后绑定到哪个 endpoint”。核心逻辑在 [_resolve_openrouter_runtime](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L352-L446)。

判断链大致是这样的：

- 先看这轮有没有显式传临时 `base_url`
- 没有，再看配置里有没有持久化保存的 `base_url`
- 有，而且它属于 `provider = custom`
- 那就直接把这条地址提升为本轮请求的真实目标

而这条地址恰好是 `https://api.openai.com/v1`。

所以这一步完成以后，系统得到的就不再是模糊判断，而是一个明确结论：

- 逻辑身份仍然是 `custom`
- 运行时目标却是 OpenAI 官方 endpoint

**Runtime Provider** 的关键价值，就在于它把“我是谁”和“我最终连到哪里”分开了。

很多系统的问题恰恰出在这里：逻辑身份、物理 endpoint、凭证语义和协议模式全部被合并成一个概念，最后只要新增一种兼容路径，就得整条链一起改。

## 六、为什么 Runtime Provider 里最敏感的不是模型名，而是 endpoint、key 和 api_mode

到这一步，很多人还会把注意力放在“模型选没选对”上。

但从工程角度看，更敏感的是另外三件事：

- 发到哪里
- 带哪把 key
- 说哪种 API 语言

### 1. endpoint

同样都叫 OpenAI-compatible，背后可能是官方 endpoint、OpenRouter、中转网关，甚至公司内部代理。

这些线路外表相似，运行时语义却未必相同。

### 2. key

只要 endpoint 和 key 绑定错位，问题就不再只是“功能不工作”，而是很容易直接变成安全问题。

在这个例子里，因为真正落到的不是 `openrouter.ai`，Hermes 在选 key 时会优先走 OpenAI 这一侧的凭证语义，而不是随手把 `OPENROUTER_API_KEY` 塞进去。相关逻辑也在 [_resolve_openrouter_runtime](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L390-L446)。

### 3. api_mode

Hermes 明确承认 provider 世界里不是只有一种统一 API。它内部至少区分：

- `chat_completions`
- `codex_responses`
- `anthropic_messages`

相关逻辑在 [providers.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/providers.py#L244-L250)、[determine_api_mode](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/providers.py#L391-L411) 和 [runtime_provider.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L756-L803)。

在这个例子里，因为最终 URL 指向的是 `api.openai.com`，Hermes 会继续把这一轮判成 `codex_responses`。URL 检测逻辑在 [_detect_api_mode_for_url](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L36-L45)。

所以真正落出来的结果，不是“这轮用 OpenAI”这么一句话，而是一整组运行时事实：

- `Provider Identity` 是 `custom`
- 真实目标是 OpenAI 官方 endpoint
- key 选择走 OpenAI 语义
- `api_mode` 是 `codex_responses`

回到整条链路来看，Hermes 的 Provider 层并不是模型选择器，而是一条运行时装配线。

## 七、请求发出以后，Hermes 也不会立刻切换 provider

到这里，请求终于可以发出去了。

但 Runtime Provider 这件事还没有结束。因为一条真正可用的运行时结果，不只是“能打出去”，还得回答“出错以后先怎么办”。

假设这次请求先撞上了 `429`。

很多系统第一反应是跨 provider fallback，看起来像高可用设计，实际上却容易过早切线。Hermes 的顺序更克制。它会先在当前 provider 内部做成本最低的恢复。逻辑在 [_recover_with_credential_pool](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/run_agent.py#L4138-L4189)。

大致顺序是：

- `401` 更像凭证失效，先尝试 refresh
- `402` 更像余额或额度耗尽，优先轮转下一把 key
- `429` 先重试，连续限流再换 key

如果只是某把 key 达到限流阈值，或者某个 token 过期了，根本没必要把整条请求语义一起迁走。先在当前 provider 内止损，成本最低，也最不容易掩盖真实问题。

只有当本层真救不回来，Hermes 才会进入跨 provider fallback。入口在 [_try_activate_fallback](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/run_agent.py#L4829-L4949)。

更关键的是，到了 fallback 阶段，它也不是“直接换个模型名字继续运行”，而是重新走同一套 provider 解析与运行时绑定逻辑。

这意味着 Hermes 的主线路和故障线路，背后仍然是同一条运行时边界。

## 八、这一条请求为什么能代表更大的架构判断

如果把上面整条链路压缩成一句话，Hermes 做的事情是：

用户发来一句“帮我修一下这个 Python 项目的测试”，系统先判断这次请求优先采用显式参数、持久配置还是环境变量，再把请求归一成内部身份，接着查静态定义，最后把 endpoint、key、`api_mode` 和恢复路径一起组装成一份 Runtime Provider，出错后优先在本层恢复，只有本层解决不了才跨 provider 切线。

这条链路表面上像实现细节，但背后对应着一个更大的架构判断：

**2026 年的 Agent 已经不可能继续把 provider 当成下拉框。**

因为现在的上层会越来越像下面这样工作：

- 普通步骤走便宜模型
- 关键判断升级到更强模型
- 某些流程交给特定 provider
- 某些失败先在本 provider 内自救

上层可以继续保持“我只是在推进任务”的视角，但前提是中间已经有一层把 provider 世界里不断分化的 endpoint、key、协议和故障吸收掉了。

Hermes 的 Provider 层真正重要的地方，不是它接了多少模型，而是它把这些问题收口成了一份可执行的 Runtime Provider。

## 九、最后一句话

如果只记一句话，这篇文章想讲清楚的是：

**Hermes 不是把一次请求解析成“该用哪家模型”，而是把它解析成“一份能真正发出去、能正确带 key、能说对协议、出错后还有恢复路径的 Runtime Provider”。**

这也是为什么今天再看 Provider Router，它已经不只是一个方便切模型的中间层，而更像 Agent 世界里的运行时边界。
