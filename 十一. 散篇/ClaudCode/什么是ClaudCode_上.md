# 揭秘 Claude Code（上）：核心原理与安全机制

如果说传统的 AI 助手是“问答机器人”，那么 Claude Code 就是一个**“拥有手脚且懂行规的资深程序员”**。它直接驻扎在你的终端，通过一套精密设计的插件化架构，实现了从代码理解到自动执行的全链路闭环。

---

## **1. 技术总览：模块化的“智能体工厂”**

Claude Code 的核心设计哲学是 **“解耦”** 与 **“赋能”**。整个项目并没有将逻辑堆砌在一起，而是通过 **Plugin（插件）** 机制构建了一个生态。

### **核心三要素**

- **Commands（指令）**：用户直接触发的动作（如 `/review`, `/commit`）。
- **Agents（智能体）**：具备特定角色的“数字员工”（如 `code-explorer` 负责探索，`code-architect` 负责设计）。
- **Skills（技能）**：智能体执行任务时的知识库和操作规范（如 `agent-development` 指导如何创建新智能体）。

### **为什么是插件化？**

这种架构允许开发者像安装 npm 包一样安装“AI 能力”。比如安装 `feature-dev` 插件，你就瞬间拥有了一整套“需求分析 -> 架构设计 -> 代码实现”的研发流水线。这不仅仅是一个工具，更是一套如何将 LLM 融入严肃软件工程的最佳实践架构。

---

## **2. 深度解密（Part 1）：智能与安全内核**

### **🧠 任务调度：Prompt as Code (提示词即代码)**

Claude Code 的智能体并不是由 Python 或 TypeScript 写成的复杂类，而是**“结构化的 Markdown 文件”**。在 [code-explorer.md](file:///Users/watermoon/WebstormProjects/articles/claude_code_temp/plugins/feature-dev/agents/code-explorer.md) 中，我们可以看到一个智能体的“源码”实际上就是它的 System Prompt：

- **YAML 定义元数据**：

  ```yaml
  name: code-explorer
  tools: [Glob, Grep, LS, Read, NotebookRead] # 明确授权的工具集
  model: sonnet # 指定模型（如 Claude 3.5 Sonnet）
  ```

- **结构化思维链**：
  Prompt 被设计成严格的步骤：`1. Feature Discovery` -> `2. Code Flow Tracing` -> `3. Architecture Analysis`。这强制 LLM 遵循人类专家的分析路径，而不是随机发散。
- **触发机制（更贴近真实）**：源码里存在把 `<example>...</example>` 直接写进 `description` 的做法，用于提高“自动触发”可靠性；例如 `conversation-analyzer` 的 `description` 内嵌了多个 Example。这更像是“用结构化触发示例做召回增强”，而不是只靠一句泛化的语义匹配。

### **🛡️ 安全红线：Event-Driven Hooks (事件驱动钩子)**

它是如何拦截危险操作的？[Hookify](file:///Users/watermoon/WebstormProjects/articles/claude_code_temp/plugins/hookify) 插件展示了底层的拦截流：

1. **事件监听 (`hooks.json`)**：
   系统定义了关键生命周期事件，如 `PreToolUse`（工具使用前）、`UserPromptSubmit`（用户提交时）。

   ```json
   {
     "hooks": {
       "PreToolUse": [
         {
           "hooks": [
             {
               "type": "command",
               "command": "python3 ${CLAUDE_PLUGIN_ROOT}/hooks/pretooluse.py"
             }
           ]
         }
       ]
     }
   }
   ```

2. **入口脚本 (`pretooluse.py`)**：
   `pretooluse.py` 作为拦截的入口，并不直接写死规则，而是充当调度器：
   - **加载配置**：它会读取环境变量 `CLAUDE_PLUGIN_ROOT` 来定位插件根目录。
   - **判断上下文**：从 `stdin` 读取 JSON 输入，通过 `tool_name` 字段判断当前操作是 `Bash`（命令执行）还是 `Edit/Write`（文件修改）。
   - **动态路由**：如果检测到 `Bash` 操作，加载 `event='bash'` 的规则；如果是文件操作，加载 `event='file'` 的规则。
3. **规则引擎 (`rule_engine.py`)**：
   引擎实例化 `RuleEngine` 类，调用 `evaluate_rules` 方法。
   - **正则审计**：使用 `lru_cache` 缓存编译后的正则表达式（`compile_regex`），对命令或内容进行匹配。
   - **决策输出（补上关键协议细节）**：
     - 对 `Stop` 这类“是否允许结束会话”的事件：使用 `{"decision": "approve|block", "reason": "...", "systemMessage": "..."}`（Hookify 的 `RuleEngine` 对 Stop 分支就是这么返回的）。
     - 对 `PreToolUse/PostToolUse` 这类“是否允许工具执行”的事件：核心不是 `decision:block`，而是 `hookSpecificOutput.permissionDecision = deny|ask|allow`。Hookify 在命中 block 规则时会返回 `permissionDecision: "deny"`。
     - 另外还有一个很容易漏掉的实现要点：很多 hook 示例是通过 **退出码** 来触发“阻断并把信息反馈给 Claude”，例如示例脚本里用 `exit 2` 阻止危险 Bash/Write。

> 补充：Hooks 不只做“安全拦截”，也能做“上下文注入 / 行为改写”。例如：
>
> - `SessionStart` 可以往 `additionalContext` 注入指令，把会话变成“解释型输出模式”。
> - `Stop` hook 甚至能把“阻止退出的 reason”当成下一轮输入，实现循环式自治。

