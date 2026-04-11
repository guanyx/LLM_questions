# Hermes Agent 对象拆解：Provider 路由层设计详解

很多人一看到 Provider 路由层，第一反应都是：这不就是选模型吗。

这话只对了一半。

真正难的地方，不是这次走 OpenAI 还是 Anthropic。真正难的地方是，底下的模型世界一直在变，上面的 Agent 逻辑还得稳。

provider 会变。

认证会变。

接口会变。

模型名字会变。

报错的样子也会变。

如果这些变化一路漏到 Agent Loop、Tool System、Gateway、Cron 和 ACP 里，系统很快就会散。今天补一个分支，明天补一个判断。最后谁都说不清一条请求到底为什么这么走。

Hermes 没把这些判断塞进主流程里。它单独做了一层 Provider 路由。专门接这个脏活。

它先认人。

再定这次怎么连。

再定该说哪种 API 语言。

出错了再决定先在哪一层止损。

所以这层东西，表面像路由。往里看，其实更像缓冲带。它把乱七八糟的模型世界挡在外面，让上层还能按一个比较稳的方式工作。

## 一、Provider 路由层到底在管什么

很多系统一开始就把 provider 当一个字符串用。配置里写什么，代码里就传什么。

这就是后面变乱的起点。

Hermes 比较稳的一点，是它没把 provider 当字符串，而是拆成了几种不同的对象。

第一种是 provider identity。

说白了，就是先把“你说的到底是谁”这件事讲清楚。别名、历史名、口语名，先都归一。相关逻辑能在 [auth.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/auth.py#L786-L855) 和 [providers.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/providers.py#L156-L260) 里看到。

这一步看着像小事，其实很要命。因为同一个 provider 只要在系统里出现几种写法，后面的缓存、计费、监控、重试、fallback 都会慢慢歪掉。

第二种是 ProviderDef。

这东西管的是“这个 provider 平时长什么样”。Hermes 没把这份信息散在各处，而是放到 [providers.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/providers.py#L1-L155) 里统一收口。它会把 models.dev 元数据、Hermes 自己的 overlay、还有用户配置合在一起。

你可以把它想成地图。

底图先给你一张大范围地图。

overlay 再补本地规则。

用户配置最后改你自己的导航点。

这样上层拿到的是一份完整定义，不是一堆零碎字段。

第三种是 runtime provider。

这一步才开始碰真问题：这次请求到底该拿哪个 base_url、哪把 api_key、什么 auth_type、哪个 credential pool、哪种 api_mode。核心逻辑在 [runtime_provider.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L581-L803)。

这一步很关键。

因为真正发请求的，从来不是一个 provider 名字。真正发请求的，是一整套运行时绑定结果。

第四种是 recovery policy。

也就是出错以后怎么办。

Hermes 没把它做成一个“备用模型开关”。它拆成了三层：先在同一个 provider 里自救，再跨 provider fallback，下一轮再试着把主线路拉回来。相关逻辑在 [credential_pool.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/agent/credential_pool.py#L352-L846)、[run_agent.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/run_agent.py#L4138-L4189) 和 [run_agent.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/run_agent.py#L4829-L5015)。

看到这里，基本就能明白一件事：

Provider 路由层不是在“按配置选模型”。

它是在管一整套运行时对象。

举个更真一点的例子。

假设你在 CLI 里发了一句：“帮我改这个 Python 项目的测试。”

你在配置里写的是 openai。

你机器里又留着一组 OpenRouter 环境变量。

你还额外配了一个公司内部网关地址。

如果系统里只有一个 provider 字符串，这时候基本已经乱了。到底该认成谁。该连官方。该连聚合器。还是该走公司网关。根本说不清。

但如果先拆成 identity、ProviderDef、runtime provider 这几层，事情就会顺很多。

identity 先把“你想用谁”认出来。

ProviderDef 再把“这家平时长什么样”补出来。

runtime provider 最后把“这次到底走哪条 URL、带哪把 key、说哪种 API 语言”定下来。

这时候，上层 Agent 只管继续做任务。它不用跟着一起猜。

## 二、为什么不能写成一个大函数

很多项目早期都会这么写。

进来一个 provider。

判断一下 model。

拼一个 client。

请求失败了就切备用。

一开始很快。后面很容易炸。

因为这里面混了好几类问题。

第一类是身份问题。

用户说的 provider，不一定就是系统真正要认的 provider。openai 可能指官方，也可能指某个聚合入口。glm、z.ai、智谱这些名字，也可能最后要归到同一家 provider 家族。本地 endpoint 更是这样，看着像 provider，实际上更像运行时入口。

第二类是运行时问题。

你逻辑上说“这次走某家”，不等于这次请求真的知道该连哪里。base_url 是哪个。key 用哪把。该挂哪个 credential pool。这些都得临场解析。

Hermes 在 [runtime_provider.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L208-L224) 里把优先级排得很清楚：显式请求优先，其次是 config.yaml，再往下才是环境变量，最后才是 auto。

这个顺序很像小事，其实不是。

它在说一件很实在的事：长期事实要比临时覆盖更重要。你上次 shell 里 export 过什么，不该悄悄改掉今天的默认运行结果。

第三类是协议问题。

很多人总想把所有 provider 包成一种协议。看着省事，后面最容易漏水。

Hermes 没这么干。它明确承认底下至少有几种主要 API 形态，比如 chat_completions、codex_responses、anthropic_messages。相关逻辑在 [providers.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/providers.py#L244-L250)、[runtime_provider.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L138-L205) 和 [runtime_provider.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L756-L803)。

这一步不是在追求花样多。

它是在认现实。

现实就是，不同 provider、不同 endpoint、甚至同一家 provider 的不同模型，可能就得说不同的话。

第四类是恢复问题。

请求失败了，到底该原地重试、换 key、换 provider，还是先保住这轮、下轮再回主线路？这不是一句“报错就 fallback”能讲清楚的。

这就是为什么不能靠一个大函数硬扛。

因为一个大函数会把命名、协议、安全、恢复全搅在一起。短期少几个文件，长期多一堆耦合。

还是拿一个常见场景来说。

你让 Agent 帮你改仓库里的 Bug。

这次请求进来，用户写的是 claude。

系统先把它认成 anthropic 语义。

然后发现这次实际连的，不是官方 Anthropic，而是一个挂了 /anthropic 路径的第三方入口。

再往下，运行时又发现这条线路该用的不是默认 key，而是这个 endpoint 自己绑的那组凭证。

最后请求失败了，还得先判断这是凭证问题、限流问题，还是 provider 整体有问题。

你看，这里面每一步都不是一回事。

硬塞进一个函数里，代码当然也能跑。

但你以后几乎没法改。

## 三、Hermes 这层为什么这样设计

我觉得 Hermes 这层最值得看的，不是它写了多少分支，而是它抓得很准。

它抓住了三个矛盾。

第一个矛盾，是上层要稳，底下却一直在变。

Agent Loop 想要的是固定入口、稳定语义、可预测报错。provider 世界给你的却是另一套节奏：名字不统一，接口不统一，认证不统一，错误也不统一。

所以中间一定要有一层，把这些差异先吞掉。

第二个矛盾，是你想统一，但你不能装作大家都一样。

这点很重要。

很多系统的问题，不是抽象太少，而是抽象太假。它们嘴上说统一接口，实际是在假装所有 provider 都能塞进同一种壳里。短期写起来确实快，后面工具调用、消息结构、上下文窗口、SDK 行为，一个个都会露出来。

Hermes 的做法更老实。上层统一入口，底下保留事实。

这就对了。

第三个矛盾，是系统想继续跑，但又不能把错误藏起来。

这也是很多人最容易做歪的地方。为了“高可用”，什么错都 fallback。结果表面看起来没挂，真实问题却一直埋着。

Hermes 没有一上来就跨 provider 跳。它先看错误是什么。像 [run_agent.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/run_agent.py#L4138-L4189) 里这样：

- 401 更像凭证过期，先 refresh
- 429 可能只是短时限流，先别急着切线
- 402 更像额度没了，那就直接轮转下一把 key

这不是“更聪明”。

这是更克制。

先在最便宜的一层止损。救不回来，再往上切。

这个思路很重要。因为好的路由层会用 fallback，但不会滥用 fallback。

这里也可以放一个很有代入感的场景。

假设你在半夜跑一个修复任务。Agent 已经读了仓库，也准备动手改文件了。这时候模型请求突然报 429。

如果系统一看到 429 就立刻切到另一个 provider，表面像聪明，实际可能很亏。

因为这次 429 也许只是当前 key 被打热了，等一下就能恢复。你这时候直接跨 provider，可能会把另一条线路也打热，还顺手把上下文窗口、提示缓存、工具调用行为全换掉。

Hermes 没急着这么做。

它先在便宜的一层动手。

先看能不能继续用当前 provider。

先看是不是只要换 key。

先看是不是短时限流。

只有这些都救不回来，它才往上切。

这时候 fallback 才像止损，不像乱跳。

## 四、Hermes 最关键的几个设计动作

如果把整层继续往下压，我觉得 Hermes 真正关键的动作有四个。

第一个动作，是先统一身份。

先认人，再谈路由。

入口名字不稳，后面都会跟着晃。

第二个动作，是把选择权放到运行时。

不是你在配置里写了一个 provider，系统就机械地照着跑。Hermes 会在运行时继续把 base_url、key、api_mode 这些东西补齐。它不是在执行文本，它是在组装这次请求。

第三个动作，是把协议模式单独拎出来。

这点很容易被低估。很多时候，请求不是发错 provider，而是说错话。尤其是你同时接 OpenAI 风格、Anthropic 风格、聚合器风格和 custom endpoint 的时候，这个问题会很快冒出来。

Hermes 允许 URL、endpoint、模型特征一起参与 api_mode 判定。这个做法比“只看 provider 名称”稳得多。

第四个动作，是把恢复拆层。

不是“主线挂了就去备线”这么简单。

Hermes 会先在 provider 内部转 key。再按顺序试 fallback chain。等这一轮撑过去了，下一轮再把主线路拉回来。后两段逻辑可以在 [run_agent.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/run_agent.py#L4829-L4949) 和 [run_agent.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/run_agent.py#L4953-L5015) 里看到。

这一步很像生产系统。

因为很多故障就是暂时的。你这一轮为了保活切到 backup，不代表以后都该留在 backup。

还有一个动作，我觉得也得单独拎出来。

就是 key 和 endpoint 的绑定。

Hermes 在 [provider-runtime.md](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/website/docs/developer-guide/provider-runtime.md#L85-L106) 和 [runtime_provider.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L390-L446) 里把这件事讲得很清楚。走不同 base_url，就该拿不同语义的 key。

这事不能糊弄。

请求发错地方，最多是功能问题。key 发错地方，就是安全问题。

这个地方最好也用一个真场景去想。

比如你同时接了三条线。

一条是官方 OpenAI。

一条是 OpenRouter。

一条是公司内部挂的 OpenAI-compatible 网关。

这三条线都长得有点像。请求格式也可能差不多。最危险的时候，不是你发不出去，而是你把 OpenRouter 的 key 带到了公司网关，或者把内部 key 带到了外部域名。

这种错，测试环境里经常不显眼。

真到生产里，问题一下就变味了。

所以 key 和 endpoint 绑定，不能当成小优化。它本身就是设计主干的一部分。

## 五、这套设计换来了什么

先说最直接的。

上层终于不用懂 provider 世界那堆细枝末节了。

Agent Loop 不需要知道 Anthropic 为什么走 Messages。也不需要知道为什么 OpenAI 某些模型更适合 Responses。它更不需要知道 custom endpoint 到底该算哪一类 provider。

第二个收益，是新 provider 更好接。

你不用每来一家新 provider，就把 CLI、Gateway、Cron、ACP 全改一遍。只要这家 provider 能在身份层、定义层、运行时层、协议层被说清楚，大部分新增工作就能收在路由层里。

第三个收益，是恢复动作更细。

凭证失效、限流、provider 级故障，不再混成一种“失败”。这样你就能先做便宜恢复，再做昂贵恢复，而不是一上来就把整条线路切掉。

第四个收益，是安全边界更清楚。

哪个 endpoint 配哪类 key，哪个 custom provider 绑哪个 credential pool，都会更好管。系统一旦同时接官方 provider、聚合器、内部网关和本地模型，这一点会非常重要。

第五个收益，是成本路由更容易复用。

Hermes 在 [smart_model_routing.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/agent/smart_model_routing.py#L62-L194) 里做了回合级 cheap model route。重点不只是省钱。重点是，这种分流能力不再散在产品入口里，而是变成一层统一 runtime 能力。

最近一两年，这种做法越来越常见。

简单请求先走便宜模型。

复杂请求回主模型。

Hermes 这层设计正好接得住这种变化。

这个收益放到真实场景里也很容易懂。

比如早上九点，团队里几十个人同时在用 Agent。

有人只是问一句：“帮我看下这个报错像不像依赖没装全。”

也有人在让 Agent 拆一个老项目、跑测试、改代码、补说明。

如果这两类请求都硬塞给同一个贵模型，账单会涨得很快。

但如果简单问题先走便宜模型，复杂任务再回主模型，体验通常不会差太多，成本却会好看很多。

这就是为什么成本路由最好放在运行时层，而不是写在某个产品入口的小规则里。

## 六、这套设计也会带来什么代价

这层不是白来的。

它把系统级的混乱收住了，但也把局部复杂度抬高了。

第一个代价，是新人更难追链路。

身份归一化一层。

runtime 解析一层。

credential pool 一层。

fallback chain 一层。

主线路恢复又一层。

刚接手的人很容易问一句：不就是发个请求吗，怎么绕这么多圈。

第二个代价，是状态更分散。

ProviderDef 在一处。

runtime provider 在一处。

当前 key 状态在一处。

fallback 状态又在一处。

只要边界没收紧，文档和实现就会慢慢出现小错位。比如 fallback 的文档和测试，在 [fallback-providers.md](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/website/docs/user-guide/features/fallback-providers.md#L69-L90) 和 [test_provider_fallback.py](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/tests/run_agent/test_provider_fallback.py#L105-L125) 里就能看出这种时差。

第三个代价，是你必须补可观测性。

路由越智能，就越要能回答一句话：为什么这次这样走。

为什么选这个 provider。

为什么用这个 base_url。

为什么判成这个 api_mode。

为什么没走主线路。

为什么 fallback 停在这里。

答不上来，排查就会很痛。

第四个代价，是测试更难写。

因为你测的已经不是一个小函数，而是一条运行时装配线。它跨身份、跨协议、跨凭证、跨恢复策略。测试如果只看最后成功没成功，很容易漏掉中间状态。

这个代价也很真实。

比如你写了一个测试，只断言“请求最后成功返回了”。

那这个测试很可能完全没告诉你，中间是不是用错了 provider、是不是走错了 api_mode、是不是本来该换 key 却直接切了 provider。

表面看它过了。

实际上最关键的路由动作，你一个都没测到。

## 七、如果你自己设计这一层，我会多加几条约束

第一条，不要把 provider 当字符串一路传。

字符串只适合当入口。真正执行请求的，应该始终是 runtime provider。

第二条，不要把“统一接口”听成“统一协议”。

统一的是上层抽象，不是底下事实。只要系统真的接了多家 provider，这件事就躲不开。

第三条，不要滥用 fallback。

哪些错能切。

先切 key 还是先切 provider。

切几次。

什么时候把主线路拉回来。

这些都要明着设计。别把 fallback 用成遮羞布。

第四条，把 custom endpoint 当正式公民。

别把它当调试后门。

这两年越来越多团队会把内部网关、自建代理、本地模型服务和第三方聚合入口放到同一套 Agent 基础设施里。custom provider 早就不是边角料了。

第五条，尽早补 decision trace。

每次请求为什么这么走，最好都能追出来。不然路由层越强，排查越像猜。

第六条，别让这层管太多别的事。

它不该替业务决定 prompt 策略。

不该替工具系统决定工具选择。

也不该承担“把所有错误都兜住”的职责。

它最重要的工作，还是把运行时接稳。

## 八、最后怎么看 Hermes 这一层

我觉得 Hermes 这层最值钱的地方，不是 provider 多，也不是 fallback 多。

而是它把一个很容易散掉的问题，硬收成了一套运行时设计。

它先定义对象。

再划边界。

再拆层级。

最后才谈切换。

这条顺序很重要。

因为很多系统正好反过来：先上 fallback，先上兼容层，先上补丁。最后对象没定义清楚，边界也没划清楚，整个系统就一直靠经验在顶。

Hermes 至少没走这条路。

一句话讲完：

好的 Provider 路由层，不是替系统找更多模型。

它是替系统把模型世界的波动、异构和故障，压成一个上层还能稳稳依赖的运行时。
