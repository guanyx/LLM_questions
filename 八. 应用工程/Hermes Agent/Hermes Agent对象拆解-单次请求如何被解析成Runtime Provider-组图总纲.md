# 《Hermes 是怎么把一次请求解析成 Runtime Provider 的》组图总纲

## 一、这次为什么值得重做

上一版“为什么 2026 的 Agent 必须有 Provider Router”更像观点型文章，适合当开题，不适合撑一整组高信息量信息图。问题不在题目错，而在它的主要内容是判断，不是对象。

这次重做要把重心彻底拉回**一条真实请求的解析链路**。

因为真正适合做图的，不是“Provider Router 很重要”这类宏观判断，而是下面这些可以被画出来、拆开来、逐层推进的东西：

- 一条请求进入系统以后，前面到底摆着哪些候选线路
- 系统先按什么顺序读取输入
- `Provider Identity`、`ProviderDef`、`Runtime Provider` 到底是不是一回事
- endpoint、key、`api_mode` 是怎么一起绑定出来的
- 出错以后为什么不是立刻跨 provider 切线

也就是说，这一组图不再围绕“观点”展开，而是围绕**对象 + 判断链 + 运行时结果**展开。

---

## 二、组图主线

整组图要讲清楚的不是“Provider Router 有多重要”，而是：

**Hermes 如何把一句自然语言请求，逐步解析成一份可以真正发出去、带对 key、说对协议、并且带着恢复路径的 Runtime Provider。**

如果压缩成一句适合放在总封面或导语里的话，可以用：

**Provider 层真正产出的不是模型名字，而是一份运行时决定。**

---

## 三、为什么这次的组图会更有信息量

因为这次每一张图都能承载一个明确对象或明确判断，而不是反复换说法。

这组图里的信息密度主要来自四类内容：

- **真实输入条件**：不是抽象 provider，而是 `config.yaml`、`base_url`、环境变量、fallback 同时存在
- **对象拆分**：`Provider Identity`、`ProviderDef`、`Runtime Provider`、`Recovery Policy`
- **判断链**：优先级、绑定、协议判定、恢复顺序
- **最终结果**：逻辑身份和物理目标分离，恢复策略分层

所以这一版更像“运行时档案”，不是“架构口号板”。

---

## 四、建议张数

建议做成 **7 张图**，比上一版更紧，也更实：

- 第 1 张：封面 / 总问题
- 第 2 张：一条请求面前到底摆着几条候选线路
- 第 3 张：系统先按什么顺序读取输入
- 第 4 张：为什么要拆成 Identity、Def、Runtime 三层
- 第 5 张：这条请求最后是怎么绑定出 Runtime Provider 的
- 第 6 张：请求发出去以后，错误是怎么分层恢复的
- 第 7 张：这一条请求背后的架构判断

如果后面觉得还想再压缩，也可以收成 5 张，但当前建议先按 7 张设计，因为这 7 张刚好覆盖完整解析链。

---

## 五、统一视觉语言

### 1）整体风格

- 视觉气质：Object Anatomy / Runtime Dossier / 协议对象拆解
- 基调：白底、技术杂志感、结构清楚、标注密集
- 关键词：resolution、identity、binding、runtime、recovery、fallback
- 禁止：工业机器、齿轮、控制柜、流水线机械剖面

### 2）术语约束

- 描述性文字尽量中文
- 术语保留英文：
  - Provider Identity
  - ProviderDef
  - Runtime Provider
  - Recovery Policy
  - endpoint
  - api_key
  - api_mode
  - fallback
- `ProviderDef` 必须始终表现为**静态定义**
- `Runtime Provider` 必须始终表现为**最终运行时结果**

### 3）配色

- 深蓝：主对象板、标题、结构边界
- 亮蓝：主判断链、解析路径、依赖线
- 绿色：稳定运行时结果、恢复成功、主线路恢复
- 橙色：错误、歧义、串线风险、跨 provider 切换
- 灰色：辅助说明、背景网格、次级标注

### 4）叙事规则

- 每张图只讲一个主要判断
- 每张图里必须有“输入 → 判断 → 结果”
- 不做重复导读，不做空泛总结条
- 金句只保留一句，而且必须对应本张的核心判断

---

## 六、逐张总纲

### 第 1 张：封面 / 总问题

**标题建议：**

Hermes 是怎么把一次请求解析成 Runtime Provider 的

**副标题建议：**

Provider 层真正产出的不是模型名，而是一份运行时决定

**这一张承载的信息：**

- 这组图不是讲“怎么选模型”
- 而是讲一句请求如何被压成 Runtime Provider
- 中心对象不是厂商，不是模型，而是运行时解析边界

**适合直接上图的一句话：**

一条请求进来以后，Hermes 最终产出的不是 provider 字符串，而是一份真正可执行的 Runtime Provider。

**画面结构建议：**

- 中间放一个大对象板：`Runtime Provider`
- 左侧是混乱输入区：
  - request
  - config.yaml
  - base_url
  - env vars
  - fallback
- 左侧每个输入块只保留极短标签，不展开完整判断链
- 中央对象板内部只提示 4 个结果字段：
  - endpoint
  - api_key
  - api_mode
  - recovery path
- 用一条从左到右的主压缩箭头连接：
  - mixed inputs → Runtime Provider
- 在中央对象板旁边补一条很短的次级提示：
  - resolve
  - identify
  - bind
- 不要把完整 `resolve → identify → define → bind → recover` 流程全部铺在封面上
- 右侧只放“稳定输出”性质的小标签，不再展开成第二块完整结果面板

**这一张的作用：**

- 立住“运行时结果”这个对象
- 让读者知道后面每一张都在解释这份结果是怎么来的
- 封面只负责立题，不提前透支后面各页的信息量

---

### 第 2 张：这条请求面前到底摆着几条候选线路

**标题建议：**

同一句请求，前面其实摆着不止一条路

**副标题建议：**

Provider 冲突不是抽象问题，而是多个候选线路同时存在

**这一张承载的信息：**

- 请求本身很普通，但环境其实很复杂
- 当前场景里至少同时存在：
  - `provider: custom`
  - `base_url = https://api.openai.com/v1`
  - OpenRouter 环境变量
  - 公司内部兼容网关
  - fallback provider
- 其中“OpenAI-compatible”不是独立候选线路，而是几条线路共享的协议表象
- 这说明 Provider 问题不是“选一家”，而是“在多条线里收口”

**适合直接上图的一句话：**

真正复杂的不是请求本身，而是请求背后同时存在的多条候选线路。

**画面结构建议：**

- 顶部放用户请求：
  - “帮我修一下这个 Python 项目的测试”
- 中间展开 4 张候选线路卡：
  - custom + saved base_url
  - OpenRouter env
  - internal gateway
  - fallback provider
- 在 `custom + saved base_url` 和 `internal gateway` 旁边挂同一种小协议标签：
  - OpenAI-compatible
- 把 “OpenAI-compatible” 画成协议徽标，而不是独立候选卡
- 每张卡旁边标它带来的歧义：
  - 认谁
  - 连哪里
  - 带哪把 key
  - 说哪种协议

**这一张的作用：**

- 把“为什么不能把 Provider 当字符串”讲得非常具体

---

### 第 3 张：系统先按什么顺序读取输入

**标题建议：**

第一步不是连模型，而是先确定解析优先级

**副标题建议：**

显式参数、持久配置、环境变量、auto，谁先进入解析链

**这一张承载的信息：**

- 对应 [resolve_requested_provider](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L208-L224)
- Hermes 先决定优先采用哪一层输入：
  - 显式参数
  - `config.yaml`
  - env vars
  - `auto`
- 这一步解决的是控制权和优先级问题，不是连接问题
- 在这个例子里，`config.yaml` 先进入优先路径，所以 OpenRouter env 和内部网关暂时退出主链

**适合直接上图的一句话：**

Provider 解析的第一步，不是选厂商，而是先确定这轮请求优先读取哪一层输入。

**画面结构建议：**

- 做成一张优先级阶梯板
- 最上层显式参数高亮
- 第二层 `config.yaml` 高亮
- 第三层 env vars 灰化
- 第四层 `auto` 更浅
- 右侧放本轮结果：
  - 当前采用：`provider = custom`
  - 当前采用：saved `base_url`

**这一张的作用：**

- 把“优先级”这个抽象概念转成可视化判断链

---

### 第 4 张：为什么要拆成 Identity、Def、Runtime 三层

**标题建议：**

`custom`、`ProviderDef`、`Runtime Provider` 不是一回事

**副标题建议：**

逻辑身份、静态定义、运行时结果必须拆开

**这一张承载的信息：**

- `Provider Identity`：系统内部先认哪条逻辑路径
- `ProviderDef`：这家 provider 的静态轮廓是什么
- `Runtime Provider`：这轮请求最终绑定出来的运行时结果
- 如果三者混写，就会出现：
  - 逻辑身份混乱
  - endpoint 语义错位
  - key 语义串线
  - 协议判断散落

**适合直接上图的一句话：**

Hermes 不是把 provider 当成一个名字在传，而是把它拆成三层不同对象来处理。

**画面结构建议：**

- 做成三联对象剖面板：
  - `Provider Identity`
  - `ProviderDef`
  - `Runtime Provider`
- 每块都要有“它回答什么问题”的说明
- `ProviderDef` 用静态档案卡风格
- `Runtime Provider` 用最终落地结果板风格

**这一张的作用：**

- 这是整组图最核心的一张对象拆解图
- 它决定后面所有判断有没有清楚的对象边界

---

### 第 5 张：这条请求最后是怎么绑定出 Runtime Provider 的

**标题建议：**

这条请求最后为什么会落到 OpenAI

**副标题建议：**

逻辑身份是 `custom`，物理目标却是 OpenAI endpoint

**这一张承载的信息：**

- 对应 [resolve_runtime_provider](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L581-L803)
- 以及 [_resolve_openrouter_runtime](file:///Users/watermoon/WebstormProjects/articles/hermes-agent/hermes_cli/runtime_provider.py#L352-L446)
- 本轮判断链是：
  - 没有显式 `base_url`
  - 发现配置里有持久化 `base_url`
  - 该地址属于 `provider = custom`
  - 因此把这条地址提升为真实目标
- 最终结果：
  - `Provider Identity = custom`
  - endpoint = `https://api.openai.com/v1`
  - key 选择走 OpenAI 语义
  - `api_mode = codex_responses`

**适合直接上图的一句话：**

Runtime Provider 的关键，不是“选了 OpenAI”，而是把逻辑身份、物理目标、凭证语义和协议模式同时绑定出来。

**画面结构建议：**

- 左侧放输入条件
- 中间放判断链节点
- 右侧放最终结果板
- 结果板必须把四个字段写清楚：
  - identity
  - endpoint
  - api_key semantics
  - `api_mode`

**这一张的作用：**

- 它会是整组图里信息密度最高的一张
- 也是最容易让读者产生“原来如此”的一张

---

### 第 6 张：请求发出去以后，错误是怎么分层恢复的

**标题建议：**

Hermes 为什么不会一报错就跨 provider 切线

**副标题建议：**

先本层恢复，再决定是否 fallback

**这一张承载的信息：**

- Runtime Provider 不只是“能不能发出去”
- 它还要包含恢复路径
- Hermes 在**当前这一轮**里的顺序是：
  - `401`：先 refresh
  - `402`：先轮转 key
  - `429`：先重试，再换 key
  - 只有本层救不回来，才跨 provider fallback
- fallback 以后仍然重新走同一套解析与运行时绑定逻辑
- 如果本轮因为保活切到了 fallback，后续还会尝试回到 primary；这不是同一层即时恢复，而是后续恢复动作

**适合直接上图的一句话：**

Hermes 的恢复顺序不是“先换 provider”，而是“先判断当前 provider 内部还能不能恢复”。

**画面结构建议：**

- 左侧做“本轮恢复顺序”梯子：
  - 第一层：retry
  - 第二层：refresh / rotate key
  - 第三层：cross-provider fallback
- 右侧单独做一张“后续恢复主线路”侧板：
  - return to primary
- 两部分之间用不同颜色或不同边框明确区分：
  - 左边是 turn-scoped recovery
  - 右边是 post-fallback restore
- 底部再补一个说明卡：
  - 主线路和故障线路共享同一套运行时边界

**这一张的作用：**

- 把 `Recovery Policy` 从抽象概念变成可读的错误处理顺序
- 同时避免把“本轮止损”和“后续回主线”画成同一层动作

---

### 第 7 张：这一条请求背后的架构判断

**标题建议：**

这一条请求，为什么能代表 2026 年的 Agent 架构

**副标题建议：**

Provider 层已经不是“模型切换器”，而是运行时边界

**这一张承载的信息：**

- 这一整条链路说明：
  - Provider 层不只是选模型
  - 它产出的是 Runtime Provider
  - 上层依赖的是这份运行时结果，而不是 provider 品牌本身
- 这条链路进一步说明：
  - endpoint、key、协议、恢复路径必须被同一层统一吸收
  - 上层拿到的应该是稳定运行时结果，而不是分散的 provider 细节

**适合直接上图的一句话：**

上层之所以还能只关心任务推进，前提是中间已经有一层把 provider 世界的复杂度收口了。

**画面结构建议：**

- 上半部分用一条压缩后的请求链：
  - request → source resolution → identity → def → runtime → recovery
- 下半部分用一张判断板：
  - 上层拿到的是什么
  - 中间层吸收了什么
  - 为什么这已经不是“选模型”
- 不再额外加入行业趋势卡片或“大模型时代”口号区

**这一张的作用：**

- 不是空泛拔高
- 而是把前 6 张的对象链压缩回一个架构判断

---

## 七、这一组图的优势

和上一版相比，这一版更强的地方在于：

- **对象更实**：每张图都有明确对象，不是抽象判断
- **链路更连续**：读者能顺着一条请求一路走到底
- **结果更具体**：最后能看到 identity / endpoint / key / `api_mode` 的同时落地
- **恢复更真实**：不是只讲“能发”，还讲“出错后怎么恢复”
- **宏观判断收束得更自然**：高度来自链路本身，不靠外加观点

---

## 八、后续拆分建议

如果这版总纲确认成立，下一步最值得优先展开的，不是全部 7 张一起写，而是先写这 3 张：

- 第 1 张封面
- 第 4 张对象拆解
- 第 5 张运行时绑定结果

因为这三张最能检验这次方向是不是对的：

- 封面负责立住“Runtime Provider”这个对象
- 第 4 张负责把 Identity / Def / Runtime 三层讲清
- 第 5 张负责把整条判断链真正落地

如果这三张成立，后面的恢复页和总结页就会自然很多。
