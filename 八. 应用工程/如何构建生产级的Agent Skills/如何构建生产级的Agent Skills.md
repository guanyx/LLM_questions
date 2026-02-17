# 深度分享：如何构建生产级 (Production-Grade) Agent Skills

> **副标题**：从“调戏 AI”到“工程化编排”——跨越 Claude Skills 的七大鸿沟

## 一、 开场：重新定义 Skill

大多数人认为 Skill 只是“保存下来的 Prompt”，这是最大的误区。
在工程视角下，Skill 是**微服务 (Microservice)**。

- 它有明确的输入/输出接口 (`SKILL.md` Frontmatter)。
- 它有确定性的业务逻辑 (Scripts)。
- 它有权限控制边界 (`allowed-tools`)。
- 它有独立的运行时上下文 (`context: fork`)。

**核心观点**：写 Skill 不是在写文章，而是在**写代码**。

---

## 二、 跨越七大鸿沟：Bad vs Good vs Perfect

### 0. 类型鸿沟 (Reference vs Task)

> **问题**：同一个 Skill 既当知识库又当执行流，最终会出现误触发与不可控的副作用。

- ❌ **Bad Skill (混合型)**
  - _结构_：把“规范/知识”与“有副作用的动作（发消息、部署、写文件）”塞在同一个 Skill。
  - _结果_：Claude 可能在你只想“咨询怎么做”的时候就进入“真的开始做”，而且触发时机不可预测。
- ✅ **Good Skill (分工型)**
  - _做法_：把 Skill 分成两类，并用不同的触发策略对待：
    - **Reference Skill**：提供约束、规范、风格、领域知识；允许自动触发。
    - **Task Skill**：执行明确流程（通常有副作用）；默认只允许人工显式触发。
- 🚀 **Perfect Skill (可治理型)**
  - _Policy_：对 Task Skill 一律启用“手动锁”，并明确写进 frontmatter：
    ```yaml
    ---
    name: deploy
    description: Deploy the application to production safely with checks and rollback notes.
    disable-model-invocation: true
    ---
    ```
  - _效果_：把“咨询”与“执行”分开，团队也更容易做权限与审计。

### 1. 确定性鸿沟 (Determinism Gap)

> **问题**：LLM 算不准日期、记不住格式、容易幻觉。

- ❌ **Bad Skill (自然语言流)**
  - _Prompt_: "请查看 git log，找到最近一周的提交，把 chore 去掉，按时间倒序排列..."
  - _结果_：当 Log 有 500 条时，Context 溢出，漏掉关键提交，时间排序错乱。
- ✅ **Good Skill (工具流)**
  - _Prompt_: "运行 `scripts/get_log.py`，它会返回清洗后的 JSON。直接使用该数据。"
  - _结果_：Python 处理数据 100% 准确，LLM 只负责润色文字。
- 🚀 **Perfect Skill (自愈流)**
  - _Logic_: 脚本不仅提取数据，还内置 `validate_json_schema()`。如果脚本报错，Skill 捕获 stderr 并自动重试不同参数。
  - _Code_:
    ```python
    # scripts/get_log.py
    if len(sys.argv) < 2:
        print("Error: Missing date range", file=sys.stderr)
        sys.exit(1) # Claude 会看到这个 exit code 并尝试修正调用
    ```

### 2. 架构鸿沟 (Architecture Gap)

> **问题**：单线程会话容易被中间步骤污染 (Context Pollution)。

- ❌ **Bad Skill (单体模式)**
  - _结构_：一个 Skill 负责“调研 -> 撰写 -> 翻译 -> 格式化”。
  - _结果_：调研时的网页噪声（广告、无关文本）遗留在上下文中，导致最后的“翻译”步骤出现幻觉。
- ✅ **Good Skill (分层模式)**
  - _结构_：拆分为 `research-skill` 和 `writer-skill`，用户手动分步调用。
- 🚀 **Perfect Skill (Fork & Spawn)**
  - _Feature_: 利用 Claude Code 2.1 的 `context: fork`。
  - _SKILL.md_:
    ```yaml
    ---
    name: deep-research
    context: fork # <--- 关键：启动独立子进程
    agent: Explore # <--- 使用专门的 Explore Agent (Haiku模型, 便宜且快)
    ---
    ```
  - _效果_：主会话非常干净，Skill 在隔离上下文内完成探索/调研，只把最终摘要带回；中间的大量噪音不会污染主上下文。

### 3. 安全鸿沟 (Security Gap)

> **问题**：默认权限过大，存在 Prompt Injection 风险。

- ❌ **Bad Skill (Root 权限)**
  - _默认_：继承主会话权限（读写任意文件、执行任意 Bash）。
  - _风险_：恶意指令可能诱导 Skill 执行 `rm -rf /` 或 `cat ~/.ssh/id_rsa`。
- ✅ **Good Skill (自然语言防御)**
  - _Prompt_: "请不要删除文件，不要读取敏感信息。" (防御力 ≈ 0)
- 🚀 **Perfect Skill (最小特权 + Hooks)**
  - _Configuration_:
    ```yaml
    ---
    allowed-tools:
      - Read(src/*) # 只能读 src 目录
      - Bash(npm test) # 只能运行测试，不能运行其他命令
    hooks:
      PreToolUse: # 2.1 新特性：工具调用前的拦截器
        - matcher: "Bash"
          command: "scripts/audit_cmd.sh" # 强制审计
    ---
    ```
  - _补充_：仅限制工具还不够，生产级 Skill 还要做“指令/数据隔离”：
    - 外部内容（网页、日志、工单、PR 描述）一律当作**数据**而不是**指令**处理。
    - 先提取结构化字段（例如标题/链接/编号/关键信息）再进入主流程，避免整段原文进入上下文。
    - 明确禁止把外部原文直接拷贝进最终产物（除非白名单字段）。

### 4. 性能鸿沟 (Context Engineering Gap)

> **问题**：Skill 加载即占用大量 Token，导致“变贵变傻”。

- ❌ **Bad Skill (Eager Loading)**
  - 把 5000 字的 `API_DOC.md` 直接写在 `SKILL.md` 里。
  - _结果_：每次对话起步价 $0.05，且模型注意力被稀释。
- ✅ **Good Skill (Reference Files)**
  - 把文档拆出去，但在 Prompt 里让 Claude 也就是 "Read it at the beginning"。
- 🚀 **Perfect Skill (Lazy Loading / RAG)**
  - _Prompt_: "当且仅当遇到 `Error 404` 时，读取 `docs/404_guide.md`。"
  - _技巧_：利用 `argument-hint` 和 `description` 做路由，只在必要时刻加载必要上下文。

### 5. 契约鸿沟 (Contract Gap)

> **问题**：Skill 没有明确的输入/输出契约，导致“每次看起来差不多，但没有一次完全可复用”。

- ❌ **Bad Skill (作文式)**
  - _指令_：只说“生成一份发布说明/复盘/周报”，没有输入定义与输出边界。
  - _结果_：格式漂移、字段缺失、很难做二次自动化（比如发到飞书、入库、生成差异对比）。
- ✅ **Good Skill (接口式)**
  - _做法_：像写 API 一样写 Skill：
    - **Inputs**：参数、默认值、边界条件（repo 路径、日期范围、环境）。
    - **Outputs**：固定结构（模板/字段），并写清楚“不得输出什么”。
    - **Argument hint**：在 frontmatter 给调用者明确参数提示。
      ```yaml
      ---
      name: release-notes
      description: Generate release notes from git history using our template.
      argument-hint: "<repo-path> <since> <until>"
      ---
      ```
- 🚀 **Perfect Skill (可测试契约)**
  - _做法_：把输出结构设计成机器可校验的契约：
    - Markdown：严格按 `TEMPLATE.md` 的标题与段落顺序，字段填充占位符统一。
    - JSON：定义 schema（字段、枚举、长度限制），让 validator 可直接报错定位。
  - _结果_：Skill 的输出可以进入流水线（lint、diff、发布、归档）而不是停留在“看上去不错”。

### 6. 验收鸿沟 (Validation Gap)

> **问题**：没有验收，就不叫生产级；只能靠人眼检查，就无法规模化。

- ❌ **Bad Skill (生成即结束)**
  - _结果_：偶发错误永远存在，只能靠“运气 + 人肉返工”兜底。
- ✅ **Good Skill (有验收标准)**
  - _做法_：在 `SKILL.md` 明确“验收清单”，例如必须包含哪些章节、每条变更必须带来源。
- 🚀 **Perfect Skill (机器门禁)**
  - _做法_：把验收做成脚本并强制执行：
    - `scripts/validate_output.py`：检查模板结构、字段完整性、长度限制、敏感信息扫描。
    - 不通过则自动修复/重试；仍不通过则明确失败原因并停止输出。
  - _结果_：输出质量可以被 CI 约束，稳定性来自门禁而不是模型“发挥”。

### 7. 治理鸿沟 (Observability & Delivery Gap)

> **问题**：团队要规模化使用 Skill，必然进入“可观测、可回溯、可复现、可交付”的治理问题。

- ❌ **Bad Skill (个人手艺)**
  - _结果_：只能在某个人电脑上跑；出了问题没人能复盘；换机器/换项目就失效。
- ✅ **Good Skill (可交付)**
  - _做法_：项目内统一放 `.claude/skills/`，进入代码评审与版本管理；把大文件拆成支持文件（模板、术语表、示例、脚本）。
- 🚀 **Perfect Skill (可治理)**
  - _做法_：
    - **可观测**：用 hooks 记录关键工具调用（读了哪些路径、跑了哪些命令、产物写到了哪里），并在 Stop 阶段输出“执行摘要”。
    - **可复现**：脚本依赖要可复现（锁版本/固定镜像/明确安装策略），避免运行时漂移。
    - **可覆盖**：明确团队层级（企业/个人/项目/插件）同名 Skill 的优先级与命名策略，避免“看起来装了但实际没生效”。
  - _结果_：Skill 从“个人工作流”升级为“团队基础设施”。

---

## 三、 总结：从入门到精通的路线图

| 阶段                | 关键词      | 特征                                    | 适用场景                                |
| :------------------ | :---------- | :-------------------------------------- | :-------------------------------------- |
| **L1: Hobbyist**    | Prompt      | 只有 `SKILL.md`，纯自然语言             | 个人日常、简单问答                      |
| **L2: Pro**         | Script      | 引入 `scripts/`，逻辑代码化             | 团队内的数据处理、简单的自动化          |
| **L3: Engineering** | Context     | 使用 `allowed-tools` 限制权限，文件拆分 | 企业级 CI/CD 集成、代码审查             |
| **L4: Autonomous**  | Fork & Hook | 使用 `context: fork` 和生命周期 Hooks   | **复杂的无人值守任务** (如自动修复 Bug) |

## 四、 给团队的 Actionable Advice

1.  **Code Review 你的 Skill**：像 Review 代码一样 Review `SKILL.md`，检查是否有模糊的自然语言指令。
2.  **先定类型再定触发**：Reference Skill 可自动触发；Task Skill 一律 `disable-model-invocation: true`。
3.  **默认开启 Fork**：对“探索/调研/阅读大量材料”的技能，优先 `context: fork` 来隔离上下文污染。
4.  **脚本优先**：能用 Python/Shell 解决的逻辑，绝不写在 Prompt 里；让 LLM 负责编排与表达。
5.  **把输出当作契约**：写清 Inputs/Outputs，并用模板或 schema 固化结构，避免格式漂移。
6.  **把验收做成门禁**：输出后强制跑 validator；不过就修复/重试，仍不过则明确失败并停止。
7.  **建立可治理的 Skill 仓库**：统一放在项目 `.claude/skills/` 并纳入版本控制；用 hooks 做审计与摘要，保证可回溯。
