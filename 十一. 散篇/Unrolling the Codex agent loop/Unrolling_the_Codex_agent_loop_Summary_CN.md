# 深入解析 Codex Agent 循环 (Unrolling the Codex agent loop)

**来源**: [OpenAI - Unrolling the Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/)

Codex CLI 是 OpenAI 推出的跨平台本地软件 Agent，旨在安全高效地在用户机器上进行高质量的软件修改。本文深入探讨了 Codex CLI 的核心逻辑——**Agent 循环 (Agent Loop)**，即 Agent 如何协调用户、模型和工具之间的交互。

## Agent 循环的核心机制

所有 AI Agent 的核心都是“Agent 循环”。其基本流程如下：

1.  **用户输入**：Agent 接收用户指令，准备 Prompt。
2.  **模型推理 (Inference)**：将 Prompt 发送给模型，模型生成响应。
3.  **响应处理**：
    - 如果模型生成了最终回复，流程结束，控制权交还用户。
    - 如果模型请求**工具调用 (Tool Call)**（例如“运行 `ls` 命令”），Agent 会执行该工具。
4.  **循环迭代**：工具的执行结果会被追加到原 Prompt 中，再次查询模型。这个过程会一直重复，直到模型不再请求工具调用，而是输出一条**助手消息 (Assistant Message)**。

从用户输入到 Agent 最终回复的过程被称为一个**对话轮次 (Turn)**。随着对话的进行，历史消息（包括工具调用和结果）会不断积累，Prompt 的长度也随之增加。

## 模型推理与 Responses API

Codex CLI 通过 HTTP 请求 **Responses API** 来运行模型推理。这个 API 端点是高度可配置的：

- **ChatGPT 登录**：使用 `https://chatgpt.com/backend-api/codex/responses`。
- **API Key 认证**：使用 OpenAI 托管模型 `https://api.openai.com/v1/responses`。
- **本地/OSS 模型**：支持通过 Ollama 或 LM Studio 运行本地模型（如 `http://localhost:11434/v1/responses`）。
- **云服务商**：支持 Azure 等云服务商托管的 Responses API。

## 构建初始 Prompt

Prompt 并非由用户直接指定，而是由 Responses API 根据用户提供的输入类型结构化生成的。一个 Prompt 包含多个带有角色的列表项，**角色的优先级从高到低依次为**：`system`, `developer`, `user`, `assistant`。

Codex 构建 Prompt 的主要参数包括：

1.  **`instructions` (指令)**：

    - 来自 `~/.codex/config.toml` 中的 `model_instructions_file`。
    - 或者使用模型关联的默认基础指令。

2.  **`tools` (工具)**：

    - Codex CLI 内置工具（如 `shell`, `update_plan`）。
    - Responses API 提供的工具（如 `web_search`）。
    - 用户通过 MCP (Model Context Protocol) 服务器提供的工具（如获取天气）。

3.  **`input` (输入)**：
    Codex 会在用户消息前插入一系列上下文信息：
    - **沙箱说明 (`role=developer`)**：描述文件权限和网络访问限制。**注意：沙箱限制仅适用于 Codex 提供的 `shell` 工具**，通过 MCP 引入的其他工具需自行负责其安全边界。
    - **开发者指令**：来自用户的配置文件。
    - **用户指令 (`role=user`)**：聚合自 `AGENTS.md`、`AGENTS.override.md` 以及配置的 Skills。
    - **环境上下文 (`role=user`)**：包含当前工作目录 (CWD) 和使用的 Shell 类型（如 zsh）。

## 执行流与工具调用

Codex 使用 **Server-Sent Events (SSE)** 来接收模型的流式响应。

- **流式输出**：`response.output_text.delta` 用于在 UI 上实时显示文本。
- **推理过程 (Reasoning)**：模型可能会先输出推理步骤（`response.reasoning_summary_text`），这些内容在后续轮次中会以 `type=reasoning` 的形式（通常包含 `encrypted_content`）回传给模型，以保持思维链的连续性。
- **工具执行**：当收到 `response.output_item.done` (类型为 `function_call`) 时，Codex 会执行相应工具。
- **结果回填**：工具执行的输出（`function_call_output`）会被追加到 Prompt 中，用于下一次模型查询。

重要的是，新的 Prompt 包含旧 Prompt 作为**精确前缀 (Exact Prefix)**，这为利用 Prompt 缓存奠定了基础。

## 性能优化与设计考量

随着对话变长，发送给 API 的 JSON 数据量呈二次方增长（Quadratic）。为了解决性能问题，Codex 在设计上做出了以下权衡：

### 1. 无状态与零数据保留 (ZDR)

Codex **故意不使用** `previous_response_id` 参数来引用历史对话。

- **无状态 (Stateless)**：这使得每个请求都是独立的，简化了服务端逻辑。
- **支持 ZDR**：对于开启了“零数据保留”的企业客户，服务端不存储数据。虽然数据不落地，但通过客户端回传加密的 `encrypted_content`，模型依然可以利用之前的推理信息（服务端仅持有解密密钥）。

### 2. Prompt 缓存 (Prompt Caching)

由于请求体巨大，缓存是降低延迟和成本的关键。

- **缓存机制**：只要 Prompt 的前缀匹配，就可以重用之前的计算结果，使得采样成本从二次方降低到线性。
- **避免缓存未命中 (Cache Miss)**：
  - 静态内容（指令、工具定义）放在 Prompt 开头。
  - 动态内容（用户特定信息）放在末尾。
  - **MCP 工具陷阱**：文章特别提到一个早期 Bug，即 MCP 工具列表顺序不一致曾导致频繁的缓存未命中，这提醒开发者需保证工具枚举的确定性。
  - **配置变更处理**：如果中途更改了沙箱配置或工作目录，Codex 不会修改之前的消息，而是**追加**新的 `developer` 或 `user` 消息来反映变更，从而保持前缀一致性。

## 上下文窗口管理：压缩 (Compaction)

为了防止 Prompt 长度超出模型的上下文窗口限制，Codex 采用了**压缩 (Compaction)** 策略。

- 当 Token 数量超过阈值（`auto_compact_limit`）时，Codex 会自动调用 `/responses/compact` 端点。
- 该端点返回一个压缩后的对象列表，包含一个特殊的 `type=compaction` 项（带有加密的潜在状态内容）。
- 这个压缩后的列表将替换原本冗长的历史记录，作为新的 `input` 继续对话，既释放了空间，又保留了模型对对话历史的理解。

## 总结

Codex Agent 循环展示了如何通过精细的 Prompt 构建、流式交互、缓存优化和上下文管理，构建一个高效、可靠的本地 AI 编程助手。未来的文章还将深入探讨其 CLI 架构、工具使用实现以及沙箱模型。
