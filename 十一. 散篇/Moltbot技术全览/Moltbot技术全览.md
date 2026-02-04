# Moltbot 技术全览：从宏观到内核

Moltbot 不仅仅是一个简单的“聊天机器人脚本”，更像是一个**运行在你电脑上的微型“AI 操作系统”**。

如果不写代码，我们可以用一个**“全能私人秘书办公室”**的比喻来理解它的内部运作机制。但为了让你真正看懂它的“骨架”，我们会在每个模块的比喻之后，直接拆解它的**底层代码实现**。

---

## 1. 核心指挥塔：Gateway (网关)

### 🏢 宏观比喻：永不睡觉的总调度台

Moltbot 的心脏是一个叫做 **Gateway** 的服务。

- **它的工作**：想象一个永远在线的调度员。它不直接处理业务，而是负责“接电话”和“派活”。当你启动 Moltbot 时，实际上是启动了这个服务器。它同时维护着你的微信、Telegram、Discord 等所有渠道的连接，以及后台运行的 AI 智能体。
- **为什么重要**：因为有它，你的 AI 助理才能同时在手机（通过聊天软件）和电脑（通过命令行）上随时待命，而且状态是同步的。

### ⚙️ 深度解密：WebSocket 与协议帧

在代码层面，Gateway 的核心是一个基于 **WebSocket** 的长连接服务器。

- **通信协议 (`src/gateway/protocol`)**：
  Moltbot 为了统一管理，定义了一套严格的 **JSON 通信协议**（使用 TypeBox 定义 Schema）。它不透传聊天软件的原始数据，而是将所有交互抽象为三种核心“帧”（Frames）：

  1.  `RequestFrame (req)`: 客户端发起的请求（如“发送消息”、“列出文件”）。
      - 代码细节：`validateRequestFrame` 使用 AJV 验证 JSON Schema，确保请求格式合法。
  2.  `ResponseFrame (res)`: 服务器对请求的响应。
  3.  `EventFrame (event)`: 服务器主动推送的状态变更（如“Agent 正在思考”、“新消息到达”）。
      - 例子：当 Agent 开始生成回复时，会广播 `agent.thought` 事件，让所有客户端（Telegram, Web UI）同时显示“Thinking...”状态。

- **握手与安全 (`src/gateway/server/ws-connection.ts`)**：
  为了防止外人控制你的电脑，Gateway 启动时会生成一个**握手挑战（Handshake Challenge）**。
  - **连接过程**：
    1.  客户端连接 WebSocket。
    2.  服务器发送 `connect.challenge` 包含一个 `nonce`（随机数）。
    3.  客户端必须用预共享的 Token 或 Tailscale 身份签名这个 `nonce` 并回传。
    4.  服务器验证签名，只有验证通过才建立会话。这确保了只有你的设备能下达指令。

---

## 2. 万能翻译官：Channels (渠道层)

### 🗣️ 宏观比喻：多语言翻译官

你可能好奇它是怎么同时支持 WhatsApp、Telegram、Signal 这么多软件的。

- **它的工作**：源码里有一层专门的“翻译官”。无论你从哪里发消息，无论是 WhatsApp 的语音，还是 Discord 的图片，这层翻译官都会把它们统一转换成一种 Moltbot 内部通用的**标准消息格式**。
- **巧妙之处**：对 AI 大脑来说，它根本不知道（也不在乎）你用的是什么软件，它只看到“主人发来了一段话/一张图”。

### ⚙️ 深度解密：标准化消息总线与插件

- **归一化处理**：
  所有外部渠道（Telegram Bot API, Discord Gateway 等）的消息在进入系统前，都会被 `normalizeMessage` 函数清洗。

  - **输入**：`TelegramUpdate` / `DiscordMessage`
  - **输出**：`AgentMessage` (Moltbot 内部标准结构)
    这使得核心的 Agent 逻辑与具体的聊天平台**完全解耦**。

- **插件化扩展 (`src/channels/plugins`)**：
  Moltbot 不仅内置了常见渠道，还提供了一个**插件系统**。
  - **动态加载**：启动时扫描 `src/channels/plugins` 目录。
  - **接口规范**：每个插件只需实现标准接口（`onMessage`, `sendMessage`），即可被系统识别。这意味着你可以通过编写插件来支持自研的内部聊天软件，甚至让 Agent 对接邮件服务器，而无需修改核心代码。

---

## 3. 住在本地的大脑：Pi Agent (嵌入式智能体)

### 🧠 宏观比喻：思考-行动的循环

这是最核心的部分。Moltbot 并没有简单地把你的话转发给 ChatGPT，它运行着一个叫做 **Pi Agent** 的智能体循环。

- **思考模式**：它不是“问一答一”的傻瓜模式，而是**“思考 -> 行动 -> 观察”**的循环模式。
  1.  **收到任务**：“帮我把这个文件夹里的图片都压缩一下。”
  2.  **思考**：它会想“我需要先看看文件夹里有什么（列出文件），然后用压缩工具处理（调用工具）。”
  3.  **行动**：它真的会在你的电脑上执行命令。
- **多智能体协作**：它不仅可以单打独斗，还可以拥有“下属”（Sub-agents），将复杂任务分拆给专门的子智能体去完成。

### ⚙️ 深度解密：有限状态机与容错

Agent 的运行逻辑位于 `src/agents/pi-embedded-runner`，它本质上是一个**具备容错能力的有限状态机**。

- **运行尝试 (Attempt Mechanism)**：
  代码逻辑封装在 `runEmbeddedAttempt` 函数中。每次 Agent 被唤醒，都是一次“Attempt”。
  - **状态流转**：`Idle -> Running -> Thinking -> ToolExecution -> FinalResponse`。
- **智能容错 (Context Window Guard)**：
  在运行前，`evaluateContextWindowGuard` 会计算当前对话历史的 Token 数。

  - **动态模型切换**：如果发现当前上下文超出了配置模型（如 GPT-4）的限制，它会自动触发 **Failover（故障转移）**，无缝切换到上下文窗口更大的模型（比如 Claude 3 Opus 或 Gemini 1.5 Pro）。这确保了对话不会因为“脑容量不足”而报错中断。

- **多智能体 (`src/agents/agent-scope.ts`)**：
  配置解析逻辑中包含 `subagents` 字段。Agent 可以通过 `spawn_subagent` 工具启动子任务。主 Agent 此时会挂起等待，直到子 Agent 完成任务并返回结果。

---

## 4. 技能手册与工具：Skills & Tools

### 📚 宏观比喻：实时查阅说明书

这是我觉得 Moltbot 最像真人的地方。

- **以前的 Bot**：功能通常是写死在代码里的函数。
- **Moltbot 的方式**：它的技能就像是放在书架上的**说明书（Markdown 文件）**。
  - 当你想让它干一件新事（比如“帮我管理 GitHub Issue”），你不需要给它重新编程。
  - 你只需要给它一本“说明书”（SKILL.md）。
  - AI 会**实时阅读**这本说明书，学习怎么使用相关的工具，然后立马照做。

### ⚙️ 深度解密：动态绑定与虚拟内存

- **动态工具绑定 (`src/agents/pi-tools.ts`)**：
  Moltbot 的工具不是静态编译的，而是**运行时动态生成**的。

  - **Shell 工具 (`src/agents/bash-tools.ts`)**：`exec` 工具允许执行 Shell 命令。但为了安全，它通过 `safeBins`（白名单）和 `approval`（人工审批）机制进行限制。

- **网页自动化 (`src/browser` & `src/gateway/server-methods/browser.ts`)**：
  这是一个极其强大的隐藏功能。Moltbot 内置了基于 **Playwright** 的浏览器控制能力。

  - **Browser Node**：Gateway 可以将浏览器操作请求路由到具备浏览器环境的节点（Node）。
  - **能力**：它不仅能获取网页 HTML，还能像人一样**点击按钮、填写表单、截图**，甚至处理动态加载的 SPA 页面。这赋予了 Agent “看”和“操作”互联网的能力，而不仅仅是作为爬虫抓取文本。

- **技能注入机制 (`src/agents/skills.ts`)**：
  这实现了一种类似**“虚拟内存”**的机制：
  1.  **扫描**：Agent 启动时，`resolveSkillsPromptForRun` 扫描工作区内的 `SKILL.md` 文件。
  2.  **索引**：它只提取技能的**描述（Description）**放入 System Prompt，不占用宝贵的 Context Window。
  3.  **加载**：只有当 AI 决定使用某个技能时，才会通过工具读取该技能的完整内容（命令参数、使用示例）。这让 AI 拥有了理论上无限的技能库。

---

## 5. 真实的工作台：Workspace & Memory (工作区与记忆)

### 🛠️ 宏观比喻：坐在你电脑前的员工

与其他云端 AI 不同，Moltbot 是**Local-First（本地优先）**的。

- 它直接在你的硬盘上有一个“工作目录”。
- 它不仅能“读”文件，还能“写”文件、运行脚本。它就像一个坐在你电脑前的远程员工，拥有操作你文件系统的真实权限。
- **混合记忆**：它不仅记得刚才聊了什么，还能通过“即时搜索”回忆起很久以前的对话或文档内容。

### ⚙️ 深度解密：沙箱与 RAG 引擎

- **沙箱机制 (`src/agents/sandbox.ts`)**：
  为了防止“员工”删库跑路，Moltbot 引入了严格的路径限制和权限控制。

  - **Docker 隔离**：支持在 Docker 容器中运行 Agent，完全隔离文件系统和网络。
  - **路径白名单**：即使在宿主机运行，文件读写也只能访问配置中指定的 `workspace` 目录。高风险命令（如 `rm`）可设置强制人工审批。

- **混合记忆引擎 (`src/agents/memory-search.ts`)**：
  Moltbot 不仅有简单的聊天记录，还内置了一个先进的 **RAG (Retrieval-Augmented Generation)** 系统。
  - **向量数据库**：使用 **SQLite + Vector Extension** 存储记忆，轻量且无需额外部署数据库服务。
  - **混合搜索 (Hybrid Search)**：结合了**向量搜索**（语义相似度）和**全文检索**（关键词匹配）。
    - _代码逻辑_：`query.hybrid` 配置决定了向量权重和文本权重的比例，确保既能找到“意思相近”的，也能找到“字面匹配”的。
  - **自动同步**：它会监听文件变化，自动更新索引，确保记忆永远是最新的。支持多种后端（OpenAI, Gemini, Local）来生成 Embedding。

---

## 总结：一次完整的生命周期 ✉️

把以上所有模块串起来，就是一条消息的奇幻漂流：

1.  **用户**在 Telegram 发送：“帮我检查服务器状态。”
2.  **Gateway** 接收消息，**Channels** 将其标准化为 `AgentMessage`。
3.  **Agent Runtime** 被唤醒，创建一个新的 `Attempt`。
4.  **Context Guard** 检查 Token 充足，加载 **Workspace** 配置。
5.  **Agent** 思考，在 **Skills** 列表中发现了“服务器管理技能”。
6.  **Agent** 动态加载该技能的 `SKILL.md`，并决定调用 `exec` 工具运行 `status` 命令。
7.  **Sandbox** 确认命令安全，允许执行。
8.  **Agent** 拿到结果，生成自然语言回复。
9.  **Gateway** 通过 **Channels** 把回复转译回 Telegram 格式发给你。

这就是 Moltbot 的魔法：**它把云端的大模型能力，真正“落地”到了你的本地文件系统和工具链中。**
