# Kimi CLI 技术全览（下篇）：Session、扩展与总结

## 5. 工作区与记忆：Session、Context 与 Metadata

### 宏观比喻：档案室 + 录像带

Kimi CLI 的“记忆”不是只存在内存里：它把对话历史（context）和行为事件（wire）都落盘，并维护一个全局的索引（metadata），用于在同一工作目录里恢复到“上一次聊到哪”。

用“档案室 + 录像带”的比喻来看，这一层的角色分工是：

- **索引卡（metadata）决定档案柜位置**：每个 work_dir 都会被登记到全局 JSON 里，真正的 sessions 目录用 work_dir 的 md5 做分桶，避免路径过长或冲突。
- **档案袋（context.jsonl）记录事实与里程碑**：除了消息本身，还会把 token 用量与 checkpoint 这种“里程碑标记”写进去，便于恢复与回退。
- **录像带（wire.jsonl）记录过程**：不仅保存最终回答，还能保存“中间发生了什么”；甚至会从 TurnBegin 里截取用户输入生成会话标题。
- **回滚像“封存旧档再复印一份”**：revert/clear 会先把旧 context 文件做旋转重命名，然后重建新文件并恢复到指定 checkpoint 前的内容。

### 深度解密：文件结构与恢复策略

- **metadata（全局索引）**：`~/.kimi/kimi.json` 记录每个 work_dir 的 `last_session_id`，并用 work_dir 的 md5 决定 sessions 存储目录。
- **session（会话目录）**：每个 session 目录里至少包含：
  - `context.jsonl`：Message 历史 + `_usage`（token_count）+ `_checkpoint`（checkpoint id）。
  - `wire.jsonl`：Wire 事件流；Session 标题会从 `TurnBegin.user_input` 中截取生成。
- **回滚与旋转**：`revert_to` 与 `clear` 都会先把旧 context 文件做“旋转重命名”，再重建新文件并恢复到目标 checkpoint 前。

---

## 6. 扩展与集成：Skills、MCP 与 ACP

### 宏观比喻：说明书、外包团队与 IDE 接口

如果把 Kimi CLI 当成一个“可装配的助理团队”，扩展系统就像三种不同来源的能力补给：

- **Skills 是说明书书架**：启动时先把技能目录扫描一遍，只把“目录与简介”塞进系统提示词；真正要执行某个技能时，再去读对应的 `SKILL.md`，把完整说明变成一次新的 user 输入。
- **MCP 是外包团队**：通过配置连上 MCP server，把远端提供的工具动态转换成可调用的 Tool，挂到同一套 toolset 里，让 Soul 以同一种方式调用“本地工具”和“外部工具”。
- **ACP 是 IDE 的前台与代理人**：当在 IDE 里运行时，ACP server 负责创建/加载 session 并创建 `KimiCLI`；如果客户端支持相关能力，还能用“替换工具”的方式把 filesystem/terminal 等能力代理到客户端侧，让执行发生在更合适的位置。

### 深度解密：三类扩展如何落到同一条主链路

- **Skills**：
  - 启动时发现技能 roots 并索引成 `runtime.skills`，再把技能清单格式化成 `KIMI_SKILLS` 注入系统提示词。
  - Soul 会把技能注册成 `/skill:xxx`；flow 技能额外生成 `/flow:xxx`。
- **MCP**：
  - toolset 会按配置连接 MCP server，把外部工具转换成可调用的 Tool 并注入 toolset。
- **ACP**：
  - ACP server 会为每个工作目录创建 session，并创建 `KimiCLI` 实例；如果客户端支持相关能力，还会用“替换工具”的方式把 filesystem/terminal 等能力代理到客户端侧。

---

## 总结：一条消息如何在 Kimi CLI 内部旅行

1. 你在终端输入 `kimi`（或 IDE 通过 ACP 建立 session）。
2. CLI 完成选项校验、加载配置、选择/创建 session，并创建 `KimiCLI` 实例。
3. `Runtime.create` 发现技能、探测环境、准备 Approval/DenwaRenji 等运行时组件。
4. `load_agent` 读取 agent spec，拼装 system prompt 与 toolset（本地工具 + MCP 工具）。
5. `run_soul` 建立 Wire，把 Soul 与 UI 通过事件流连接起来。
6. Soul 进入 step 循环：调用 `kosong.step` 产出流式内容与工具调用，工具执行结果回写上下文，必要时触发 compaction 或回滚。
7. 最终，UI（Shell/Print/Wire/ACP）消费 Wire 消息，把“最终回答”与“过程细节”以合适形态呈现给你。
