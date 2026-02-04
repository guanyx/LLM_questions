# Kimi CLI 技术全览：从宏观到内核

- 拆分阅读：
  - [上篇：CLI 入口、装配与 Wire](kimi-cli-上篇.md)
  - [中篇：Soul step 循环与工具边界](kimi-cli-中篇.md)
  - [下篇：Session、扩展与总结](kimi-cli-下篇.md)

Kimi CLI 不只是“能在终端里聊天”的程序，更像是一套把 AI Agent 工程化后的本地运行时：能装配会话与模型、能执行工具、能把每一步行为变成可观察的事件流，并且能把状态落盘以便恢复与回放。

如果不用代码解释，它可以被类比成一个“坐在你电脑前的智能助理团队”：有人负责接待（CLI/UI），有人负责决策与调度（Soul），有人负责联络外部专家（MCP），有人负责真正去操作文件与命令（Tools/Kaos），还有一套实时的“直播字幕与日志系统”（Wire）把全过程投影出来。

---

## 1. 核心指挥台：CLI 入口与装配

### 宏观比喻：一键开机的“装机师”

你敲下 `kimi`，并不是立刻把文本发给模型这么简单。Kimi CLI 更像是在做一次“装机 + 开机自检 + 上电交接”：先把“这一趟运行需要的全部零件”装好、校验好，然后才把控制权交给 Soul 去执行。

如果把一次运行想象成你叫来一个助理团队开始干活，那么 CLI 入口扮演的是“装机师/值班经理”：

- **先做门禁与互斥校验**：哪些 UI 能同时开、哪些参数不能混用、哪些模式会强制收敛输出（例如 quiet 变成 print 并只留最终一句）。
- **再做会话定位**：是切到指定会话、续上一次会话，还是新开一个会话档案夹。
- **把运行时打包成一个口袋（Runtime）**：把工作目录信息、`AGENTS.md`、技能清单、环境探测、审批开关、DenwaRenji 等组件统一装进去，后面所有工具都从这个“口袋”拿依赖。
- **把 Agent 装配成可执行体**：读 agent spec，生成 system prompt，把工具集（含 MCP 工具）装上，并恢复 context 历史。

### 深度解密：参数校验、Session 选择与实例创建

入口在 [cli/\_\_init\_\_.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/cli/__init__.py) 的 `typer` callback：

1. **互斥选项校验**：`--print/--acp/--wire` 互斥，`--continue` 与 `--session` 互斥；`--quiet` 会被翻译成“print + 只输出最终答案”等组合。
2. **会话选择**：
   - `--session`：找不到就创建同 ID 会话。
   - `--continue`：根据 metadata 找到该 work_dir 的 last session。
   - 默认：创建新 session。
3. **实例创建**：最终落到 `KimiCLI.create(...)`（见 [app.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/app.py)），完成三件关键事：
   - `Runtime.create(...)`：探测环境、读取 `AGENTS.md`、发现技能、创建 Approval/DenwaRenji 等运行时组件（见 [agent.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/agent.py)）。
   - `load_agent(...)`：按 agent spec 装配 system prompt 与 toolset，并把工具依赖通过“按类型注入”的方式喂进工具构造函数（同样在 [agent.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/agent.py)）。
   - `Context.restore()`：从 `context.jsonl` 恢复历史与 token 计数（见 [context.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/context.py)）。

---

## 2. 直播字幕系统：Wire 消息总线

### 宏观比喻：导演喊话 + 实况字幕

很多终端 AI 工具的 UI 是“表演结束才告诉你结果”。Kimi CLI 更像是把整个执行过程做成“直播”：Soul 一边指挥，一边把每一个动作都口述给字幕组，字幕组再把它同步投到不同屏幕上（Shell/Print/Wire/ACP）。

这条“字幕流”不只是模型的输出文本，还包含：

- **逐步进度**：Turn/Step 的开始与结束，让你知道现在在第几步。
- **工具动作**：每个 tool call 的请求与结果，让“电脑上发生了什么”变得可追踪。
- **审批互动**：当遇到敏感动作时，把审批请求也作为“直播的一部分”交给 UI 去展示并回传结果。
- **原始逐字稿 + 剪辑版**：同一条消息既能以“原始流”完整播出，也能以“尽量合并后的流”播出（例如把连续的文本增量合并成更易读的一段）。
- **可回放录像**：字幕流还能选择写进 `wire.jsonl`，用于调试与复盘。

### 深度解密：SPMC 通道、消息合并与落盘回放

Wire 的实现核心在 [wire/\_\_init\_\_.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/wire/__init__.py)：

- **通信模型**：一个 Soul 端发送，多 UI 端订阅（SPMC）。
- **两路队列**：原始消息流与“尽量合并”的消息流（例如把连续的文本增量合并），UI 可以按需订阅。
- **可选落盘**：传入 `WireFile` 时，Wire 会把“合并后的完整消息”写入 `wire.jsonl`，用于调试与会话回放（Session 的标题也会从 wire 记录里派生，见 [session.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/session.py)）。

这一层把 Soul 和 UI 解耦：Shell/Print/Wire/ACP 都只是 Wire 的不同消费者。

---

## 3. 住在本地的大脑：Soul 的 step 循环

### 宏观比喻：有节奏的“思考-行动-复盘”

Kimi CLI 的核心不是“问一句答一句”，而是一个可以被观察、被打断、还能自我修复的 step 循环：每一步都像助理团队的一次“开会 → 派工 → 交付 → 复盘”，并把过程同步到 Wire 供 UI 展示。

把 Soul 当成“项目经理”，它在每个 turn 里会做这些和深度解密一一对应的事情：

- **开工前先检查证件**：每个 turn 先刷新 OAuth，避免你刚停顿一下就 token 过期导致整个任务中断。
- **给行动链上限**：用 max step 限制避免“越想越多”陷入无限循环。
- **给大脑留安全边距**：在接近上下文上限时先做压缩（compaction），而不是等模型报错才补救。
- **允许短暂失败但不轻易放弃**：对网络/超时/429/5xx 做统一重试，保证一次 step 不是“一次就死”。
- **把审批做成流水线**：工具请求审批时，Soul 只负责把请求送进 Wire、等待 UI 回传，再把结果回填给 Approval 队列。
- **支持“回到过去改方案”**：当工具通过 DenwaRenji 触发回滚，Soul 会把 context 回退到指定 checkpoint，再插入“来自未来的提示”让模型走另一条路。

### 深度解密：连接 Wire、可中断执行与容错

Soul 与 Wire 的连接点在 [soul/\_\_init\_\_.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/__init__.py) 的 `run_soul(...)`：

- 它创建 `Wire`，并把它写进 ContextVar（`get_wire_or_none()`），因此 Soul 内部只要调用 `wire_send(...)` 就能把事件发到 UI。
- 它同时跑 `ui_loop_fn(wire)` 和 `soul.run(user_input)`，并用 `cancel_event` 触发优雅取消。

具体的“大脑循环”在 [kimisoul.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/kimisoul.py)：

1. **每个 turn 先刷新 OAuth**：`ensure_fresh` 避免“用户停顿一下 token 过期”。
2. **Step 上限**：`max_steps_per_turn` 防止无限行动链。
3. **上下文护栏**：`reserved_context_size` 留安全边距；当 `token_count + reserved >= max_context_size` 时触发 compaction（并发送 `CompactionBegin/End` 事件）。
4. **调用模型一步**：每一步都调用一次 `kosong.step(...)`，并把 `on_message_part/on_tool_result` 直接绑定到 `wire_send`，因此流式输出天然变成 Wire 事件。
5. **统一重试策略**：step 与 compaction 都用 tenacity 做指数退避重试；对连接/超时/空响应/429/5xx 视为可重试。
6. **工具审批管道**：Soul 把 Approval 队列里的请求翻译成 `ApprovalRequest` Wire 消息，等待 UI 回答后再回填（这意味着“审批也是事件流的一部分”）。
7. **回到过去（D-Mail）**：工具可通过 DenwaRenji 发送一条“寄回某个 checkpoint”的消息。Soul 检测到 D-Mail 后会 `revert_to(checkpoint)`，再把那条“来自未来的系统消息”插入上下文，让模型改走另一条路线。

---

## 4. 真实的执行力：Tools、Kaos 与审批边界

### 宏观比喻：能干活，但必须有权限

Agent 真正的危险与价值都在“能对文件系统和命令做副作用”。Kimi CLI 的做法是把副作用关进一个清晰的“工具箱边界”：会干活，但每次干活都带工单号、能被 UI 看见、必要时还得走审批。

如果把工具看成“员工手里的电钻和扳手”，那么这一层的约束像是：

- **工具怎么拿到公司资源**：工具不自己到处 import 全局单例，而是由装配阶段把 Runtime/Session/Approval/Environment 等按类型注入，形成清晰依赖边界。
- **每次操作都有工单编号**：toolset 在处理 tool call 时把当前调用写进 ContextVar，工具内部可以拿到 `tool_call_id`，让审批、展示、回放都能精确对齐到同一次调用。
- **路径与权限像门禁**：文件读取要做 canonical，并对“工作目录外的相对路径”直接拒绝，要求显式绝对路径来表达意图。
- **YOLO 是特殊通道**：当你显式（或 print 模式隐式）开启 auto-approve，相当于把审批闸门常开，避免管道脚本卡住。

### 深度解密：工具注入、工具上下文与路径校验

- **工具装配与依赖注入**：`load_agent(...)` 会构建 `tool_deps`（Runtime/Session/Approval/DenwaRenji/Environment...），然后按工具类 `__init__` 的参数注入依赖（见 [agent.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/agent.py) 与 [toolset.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/toolset.py)）。
- **工具调用上下文**：`KimiToolset.handle(...)` 会把当前 tool call 写进 ContextVar（`current_tool_call`），工具内部可拿到 `tool_call_id` 等信息，做到审批与展示精确关联（见 [toolset.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/toolset.py)）。
- **路径安全检查**：以 `ReadFile` 为例，读取工作目录外的路径必须提供绝对路径，并通过 canonical 后判定是否在允许目录内（见 [read.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/tools/file/read.py)）。
- **YOLO 模式**：`--yolo/--auto-approve` 会让 Approval 自动通过；同时 `--print` 会隐式开启 yolo，避免脚本管道阻塞等待交互确认（入口逻辑在 [cli/\_\_init\_\_.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/cli/__init__.py)）。

---

## 5. 工作区与记忆：Session、Context 与 Metadata

### 宏观比喻：档案室 + 录像带

Kimi CLI 的“记忆”不是只存在内存里：它把对话历史（context）和行为事件（wire）都落盘，并维护一个全局的索引（metadata），用于在同一工作目录里恢复到“上一次聊到哪”。

用“档案室 + 录像带”的比喻来看，这一层的角色分工是：

- **索引卡（metadata）决定档案柜位置**：每个 work_dir 都会被登记到全局 JSON 里，真正的 sessions 目录用 work_dir 的 md5 做分桶，避免路径过长或冲突。
- **档案袋（context.jsonl）记录事实与里程碑**：除了消息本身，还会把 token 用量与 checkpoint 这种“里程碑标记”写进去，便于恢复与回退。
- **录像带（wire.jsonl）记录过程**：不仅保存最终回答，还能保存“中间发生了什么”；甚至会从 TurnBegin 里截取用户输入生成会话标题。
- **回滚像“封存旧档再复印一份”**：revert/clear 会先把旧 context 文件做旋转重命名，然后重建新文件并恢复到指定 checkpoint 前的内容。

### 深度解密：文件结构与恢复策略

- **metadata（全局索引）**：`~/.kimi/kimi.json` 记录每个 work_dir 的 `last_session_id`，并用 work_dir 的 md5 决定 sessions 存储目录（见 [metadata.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/metadata.py)）。
- **session（会话目录）**：每个 session 目录里至少包含：
  - `context.jsonl`：Message 历史 + `_usage`（token_count）+ `_checkpoint`（checkpoint id）（见 [context.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/context.py)）。
  - `wire.jsonl`：Wire 事件流；Session 标题会从 `TurnBegin.user_input` 中截取生成（见 [session.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/session.py)）。
- **回滚与旋转**：`revert_to` 与 `clear` 都会先把旧 context 文件做“旋转重命名”，再重建新文件并恢复到目标 checkpoint 前（见 [context.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/context.py)）。

---

## 6. 扩展与集成：Skills、MCP 与 ACP

### 宏观比喻：说明书、外包团队与 IDE 接口

如果把 Kimi CLI 当成一个“可装配的助理团队”，扩展系统就像三种不同来源的能力补给：

- **Skills 是说明书书架**：启动时先把技能目录扫描一遍，只把“目录与简介”塞进系统提示词；真正要执行某个技能时，再去读对应的 `SKILL.md`，把完整说明变成一次新的 user 输入。
- **MCP 是外包团队**：通过配置连上 MCP server，把远端提供的工具动态转换成可调用的 Tool，挂到同一套 toolset 里，让 Soul 以同一种方式调用“本地工具”和“外部工具”。
- **ACP 是 IDE 的前台与代理人**：当在 IDE 里运行时，ACP server 负责创建/加载 session 并创建 `KimiCLI`；如果客户端支持相关能力，还能用“替换工具”的方式把 filesystem/terminal 等能力代理到客户端侧，让执行发生在更合适的位置。

### 深度解密：三类扩展如何落到同一条主链路

- **Skills**：
  - 启动时发现技能 roots 并索引成 `runtime.skills`，再把技能清单格式化成 `KIMI_SKILLS` 注入系统提示词（见 [agent.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/agent.py)）。
  - Soul 会把技能注册成 `/skill:xxx`；flow 技能额外生成 `/flow:xxx`（见 [kimisoul.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/kimisoul.py)）。
- **MCP**：
  - toolset 会按配置连接 MCP server，把外部工具转换成可调用的 Tool 并注入 toolset（见 [toolset.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/soul/toolset.py)）。
- **ACP**：
  - ACP server 会为每个工作目录创建 session，并创建 `KimiCLI` 实例；如果客户端支持相关能力，还会用“替换工具”的方式把 filesystem/terminal 等能力代理到客户端侧（见 [acp/server.py](file:///Users/watermoon/WebstormProjects/articles/kimi_cli_temp/src/kimi_cli/acp/server.py)）。

---

## 总结：一条消息如何在 Kimi CLI 内部旅行

1. 你在终端输入 `kimi`（或 IDE 通过 ACP 建立 session）。
2. CLI 完成选项校验、加载配置、选择/创建 session，并创建 `KimiCLI` 实例。
3. `Runtime.create` 发现技能、探测环境、准备 Approval/DenwaRenji 等运行时组件。
4. `load_agent` 读取 agent spec，拼装 system prompt 与 toolset（本地工具 + MCP 工具）。
5. `run_soul` 建立 Wire，把 Soul 与 UI 通过事件流连接起来。
6. Soul 进入 step 循环：调用 `kosong.step` 产出流式内容与工具调用，工具执行结果回写上下文，必要时触发 compaction 或回滚。
7. 最终，UI（Shell/Print/Wire/ACP）消费 Wire 消息，把“最终回答”与“过程细节”以合适形态呈现给你。
