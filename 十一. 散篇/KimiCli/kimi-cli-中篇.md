# Kimi CLI 技术全览（中篇）：Soul step 循环与工具边界

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

- 它创建 `Wire`，并把它写进 ContextVar（`get_wire_or_none()`），因此 Soul 内部只要调用 `wire_send(...)` 就能把事件发到 UI。
- 它同时跑 `ui_loop_fn(wire)` 和 `soul.run(user_input)`，并用 `cancel_event` 触发优雅取消。

具体的“大脑循环”：

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

- **工具装配与依赖注入**：`load_agent(...)` 会构建 `tool_deps`（Runtime/Session/Approval/DenwaRenji/Environment...），然后按工具类 `__init__` 的参数注入依赖。
- **工具调用上下文**：`KimiToolset.handle(...)` 会把当前 tool call 写进 ContextVar（`current_tool_call`），工具内部可拿到 `tool_call_id` 等信息，做到审批与展示精确关联。
- **路径安全检查**：以 `ReadFile` 为例，读取工作目录外的路径必须提供绝对路径，并通过 canonical 后判定是否在允许目录内。
- **YOLO 模式**：`--yolo/--auto-approve` 会让 Approval 自动通过；同时 `--print` 会隐式开启 yolo，避免脚本管道阻塞等待交互确认。
