# 揭秘 Claude Code（下）：工程实践与生态架构

## **2. 深度解密（Part 2）：指令与工程架构**

### **🔌 指令系统：Markdown 解释器**

当你输入 `/review` 时，系统实际上是在执行 `.claude/commands/review.md`。

- **指令即文档**：Command 文件本质上是**“写给 Claude 看的说明书”**。例如在 `review-pr.md` 中，它详细定义了 `Review Workflow` 的 7 个步骤，从 `Identify Changed Files` 到 `Launch Review Agents`。
- **动态参数**：支持像 `$ARGUMENTS` 这样的占位符，将用户输入的参数动态注入到 Prompt 中。
- **工具授权（更关键的细节）**：`allowed-tools` 并不仅仅是“允许哪些工具”，更像一套权限 DSL，可以写成 `Bash(git commit:*)` 这类“只允许某些命令形态”的约束。
- **命令内联执行**：命令里可以用 `!` 反引号在运行时执行 shell 并把输出注入上下文。
- **位置参数**：除了 `$ARGUMENTS` 这种整体参数，也支持 `$1/$2` 位置参数；并且参数语法在演进。

### **🛠️ 流程工业化：Manifest 驱动的插件架构**

每个插件的核心是一个 `plugin.json` 清单文件，它定义了插件的“能力边界”：

- **自包含**：一个插件包里包含了它所需的所有 Commands, Agents, Skills 和 Hooks。
- **清单远不止“name/version/description”**：manifest 还定义组件路径（commands/agents/skills）、hooks 配置位置、mcpServers 配置等，并且有严格的路径规则（必须 `./` 开头、不能 `../`、统一正斜杠等）。仓库里有完整规范。
- **分发形态：Marketplace 源**：把多个插件打包成一个可安装的“市场源”。这比“像 npm 包一样安装”更贴近 Claude Code 的真实插件分发方式。

---

## **3. 总结：软件工程的“AI 落地样本”**

Claude Code 的源码揭示了当前 AI Agent 开发的最高水准：

- **它不写死逻辑**，而是用 Markdown 定义思维（Prompt as Code）。
- **它不裸奔运行**，而是用 Python 钩子构筑防线（Security Hooks）。
- **它不单打独斗**，而是用 Manifest 组装生态（Plugin Architecture）。

这不仅仅是一个工具，更是一套如何将 LLM 融入严肃软件工程的最佳实践架构。
