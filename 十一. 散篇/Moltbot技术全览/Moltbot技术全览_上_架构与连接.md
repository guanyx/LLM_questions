# Moltbot 技术全览 (上)：架构与连接

## 引言：你的微型 AI 操作系统

Moltbot 不仅仅是一个简单的“聊天机器人脚本”，更像是一个**运行在你电脑上的微型“AI 操作系统”**。

如果不写代码，我们可以用一个**“全能私人秘书办公室”**的比喻来理解它的内部运作机制。但为了让你真正看懂它的“骨架”，我们会在每个模块的比喻之后，直接拆解它的**底层代码实现**。

本文是系列文章的第一篇，我们将深入 Moltbot 的“身体”与“感官”，看看它是如何运行的，以及如何与外部世界连接。

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

**下篇预告**：
Moltbot 不仅有“身体”和“耳朵”，它更有一个强大的“大脑”。在下一篇文章《Moltbot 技术全览 (中)：大脑与工具》中，我们将深入其 Agent 运行循环，探索它是如何思考、决策并使用工具来完成复杂任务的。
