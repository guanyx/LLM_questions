# OpenClaw 实战部署手册：打造你的持久化 AI 队友

> **核心摘要**：这份手册不仅仅是 OpenClaw 的功能介绍，更是一份手把手的实战指南。我们将基于 OpenClaw 框架，构建一个具备**长期记忆**、**自主决策**能力、且能**自我维护**的 AI Agent。这不再是一个简单的聊天机器人，而是一个能真正像团队成员一样工作的数字员工。

---

## 1. 为什么选择 OpenClaw？

OpenClaw (曾用名 Clawdbot/Moltbot) 是 2026 年初爆火的开源 AI Agent 框架。传统的 Chatbot（如 ChatGPT 网页版）存在致命缺陷：**窗口关闭即失忆**。
OpenClaw 的核心理念是 **"Files as Brain"（文件即大脑）**。它不依赖复杂的向量数据库或黑盒存储，而是将 Agent 的认知、记忆、状态全部持久化为本地 Markdown 文件。

- **透明可控**：你可以直接用文本编辑器修改 Agent 的“记忆”或“性格”。
- **持久化**：重启后，Agent 会先读取“工作日志”，无缝恢复进度。
- **自动化**：通过 Heartbeat 和 Cron 机制，它能在你睡觉时继续工作。

## 2. 快速启动 (Quick Start)

### 环境准备

- Node.js (v22+)
- pnpm (推荐) 或 npm
- MiniMax API Key (推荐 MiniMax，OpenClaw 官方原生支持，编程能力强悍)

### 安装与初始化

```bash
# 1. 全局安装 OpenClaw
npm install -g openclaw

# 2. 创建工作区 (这是 Agent 的"家")
mkdir ~/my-agent-workspace && cd ~/my-agent-workspace

# 3. 运行向导 (Wizard)
openclaw onboard --install-daemon

# 4. 验证环境健康度
openclaw doctor
# 按照提示输入 API Key (推荐选择 MiniMax-M2.1，OpenClaw 官方原生支持)
```

## 3. 构建大脑：核心文件配置详解

在 `~/my-agent-workspace` 目录下，我们需要创建以下核心文件。Agent 启动时会“阅读”这些文件来重塑自我。

### 3.1 身份与准则 (`AGENTS.md`)

这是 Agent 的最高宪法。定义它的职责边界和操作规范。

```markdown
# AGENTS.md - 核心操作手册

## 启动协议 (First Run)

1. 检查 `memory/active-tasks.md`。
2. 如果有未完成任务，直接继续，不要询问“我该做什么”。
3. 检查 `HEARTBEAT.md` 确认是否有定期维护任务。

## 安全边界 (Safety)

- **绝对禁止**：上传私钥、密码或 .env 文件到外部服务器。
- **高危操作**：执行 `rm -rf` 或修改系统配置前，必须请求人类确认。
- **文件操作**：优先使用追加写入，避免覆盖重要数据。

## 自主原则

- 你拥有读取、写入和执行工作区内代码的权限。
- 遇到错误时，先尝试通过日志自行修复，尝试 3 次失败后再报错。
```

### 3.2 灵魂注入 (`SOUL.md`)

这决定了 Agent 像个真人还是个复读机。

```markdown
# SOUL.md - 人格设定

## 工作风格

- **实干家**：不要说“好的，我来试试”，直接给出代码或结果。
- **拒绝客套**：不要以“作为一个 AI 模型...”开头。
- **诚实**：不知道就说不知道，不要编造库或函数。
- **主动性**：发现代码里的坏味道（Bad Smell），顺手修掉或记录在 Todo 里。
```

### 3.3 环境认知 (`TOOLS.md`)

让 Agent 熟悉它的工作环境，就像新员工入职指南。

```markdown
# TOOLS.md - 本地环境指南

## 项目结构

- 源码目录: `~/projects/myapp/src`
- 文档目录: `~/projects/myapp/docs`

## 常用命令

- 启动服务: `pnpm dev` (端口 3000)
- 运行测试: `pnpm test:unit`
- 数据库迁移: `pnpm prisma migrate dev`

## 凭证管理

- 推荐将 API Key 写入 `~/.openclaw/.env` 文件（OpenClaw 会自动加载），而非系统全局配置。
- 所有 API Key (如 `MINIMAX_API_KEY`) 均已注入环境变量，**严禁**在代码中硬编码 Key。
```

## 4. 记忆系统：如何让 Agent "过目不忘"

OpenClaw 的记忆系统分为三层，对应不同的时效性。

### 4.1 短期工作记忆 (`memory/active-tasks.md`)

**作用**：崩溃恢复 (Crash Recovery)。类似于操作系统的“进程表”。

```markdown
# Active Tasks (启动必读)

## In Progress (进行中)

- [ ] **Feature: OAuth2 登录**
  - [x] 创建路由结构
  - [ ] 实现 JWT 校验 (目前卡在签名验证失败)

## Blocked (阻塞)

- 等待 GitHub API 权限申请通过
```

_实战技巧_：Agent 每次执行大任务前，强制它先更新这个文件。这样即使进程挂了，重启后它也能知道“JWT 校验失败了”，而不是从头开始。

### 4.2 长期流水账 (`memory/YYYY-MM-DD.md`)

**作用**：审计与回溯。

- 自动记录当天的关键操作、执行的命令、修改的文件。
- 建议配置 Cron 任务，每天凌晨将当天的日志归档。

### 4.3 肌肉记忆 (`memory/lessons.md`)

**作用**：错误规避。

```markdown
# Lessons Learned (经验教训)

## Code

- 在 Next.js 14 中，Server Actions 必须标记 'use server'。
- 永远不要在循环中调用 `await database.connect()`。

## Process

- 修改 `package.json` 后必须运行 `pnpm install`，否则 CI 会挂。
```

_实战技巧_：当 Agent 犯错并被你纠正后，要求它将这个错误总结为一条规则写入此文件。

## 5. 赋予生命：自动化与心跳

让 Agent 从“被动响应”变为“主动工作”。

### 心跳机制 (Heartbeats)

OpenClaw 会定期（如每 10 分钟）唤醒 Agent 读取 `HEARTBEAT.md`。

```markdown
# HEARTBEAT.md - 定期自查清单

## 每 1 小时

- 检查 `active-tasks.md` 是否有超过 2 小时未更新的任务？如果是，标记为 Stale 并分析原因。
- 运行 `git status`，如果有未提交的代码且测试通过，自动 commit。

## 每 4 小时

- 执行自我审查 (`memory/self-review.md`)：我是否陷入了死循环？我的上下文窗口是否过大？
```

### Cron 自动化

利用系统的 Cron 或 OpenClaw 内置调度器：

- `0 9 * * *` **早报**：检查 GitHub Issues，总结今天需要处理的高优先级任务。
- `0 23 * * *` **晚报**：总结今日工作，更新 `active-tasks.md`，归档日志。

## 6. 技能扩展 (Skill Engineering)

技能 (Skill) 是 Agent 的“手”。定义良好的 Skill 是成功的关键。

### 最佳实践：路由与负样本

不要只告诉 Agent 怎么用，要告诉它**什么时候不用**。

**示例：代码重构技能 (`skills/refactor.md`)**

```markdown
## When to Use (何时使用)

- 用户明确要求重构某个模块。
- 代码复杂度过高（圈复杂度 > 10）。

## When NOT to Use (何时不用)

- 简单的变量重命名（直接用 IDE 工具）。
- 涉及架构变更的重构（先写 RFC 文档）。
- 代码没有任何测试覆盖（先补测试）。
```

### 内置模板

将复杂的输出格式预定义在 Skill 中，节省 Token 并保证格式统一。

```markdown
## PR Description Template

### Summary

[一句话描述变更]

### Changes

- [ ] 文件 A: 修改了逻辑 X

### Verification

- [ ] 单元测试通过
- [ ] 本地运行验证截图
```

## 7. 安全与避坑指南

### ⚠️ 关键陷阱

1.  **无限递归**：Agent 可能会陷入“报错 -> 尝试修复 -> 报错 -> 尝试修复”的死循环。
    - _解法_：在 `AGENTS.md` 中设定“尝试 3 次失败后停止并呼叫人类”。
2.  **上下文爆炸**：长期运行后 `memory.md` 会变得巨大。
    - _解法_：设置 Heartbeat 任务，当文件超过 500 行时，触发“总结并归档”动作，只保留摘要。
3.  **幻觉命令**：Agent 可能会臆造不存在的 CLI 参数。
    - _解法_：在 `TOOLS.md` 中明确列出可用命令及常用参数。

### 🔒 安全底线

- **运行诊断**：定期运行 `openclaw doctor` 检查是否有不安全的 DM (Direct Message) 策略。
- **沙箱运行**：如果可能，让 Agent 运行在 Docker 容器中。
- **凭证隔离**：**绝对不要**把 API Key 写在 `TOOLS.md` 或 `AGENTS.md` 里。Agent 只能通过环境变量读取。
- **网络白名单**：限制 Agent 只能访问必要的域名（如 github.com, npmjs.org），防止数据外泄。

---

_实战建议：从最简单的配置开始，先让 Agent 学会“写日记”和“记住任务”，然后再尝试让它写代码。文件系统是它的大脑，保持文件的整洁结构就是保持 Agent 的思维清晰。_
