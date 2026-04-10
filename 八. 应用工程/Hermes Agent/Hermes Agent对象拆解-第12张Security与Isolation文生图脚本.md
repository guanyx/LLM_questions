# Hermes Agent对象拆解：第 12 张Security 与 Isolation文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "为什么 Agent 安全不是“内容审核”那么简单？".

**Design Concept:**
Use a sequential security-gate metaphor instead of concentric rings: the image should show that Agent safety is not one filter at the end of the pipeline, but a left-to-right chain of checkpoints. Hermes applies different security gates across identity, authorization, tool execution, context scanning, and runtime isolation. The visual emphasis should be on ordered decision points and where each risk gets blocked.

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "为什么 Agent 安全不是“内容审核”那么简单？"
- Subtitle below: "对 Agent 来说，真正的风险不是输出一句错话，而是拿着工具去执行一件错事"
- Small supporting sentence: "Hermes 的安全不是一层过滤器，而是一串分布在不同环节的运行时安全门"
- Typography should feel like a runtime security blueprint, not a generic cybersecurity poster

**Central Section (Hero Diagram - 55%):**
Create a left-to-right staged security architecture diagram with explicit stop points:

- Build one strong horizontal execution path from left to right:
  - 外部输入 → 权限校验 → 行为审批 → 运行时隔离 → Agent Execution Core
- Make each checkpoint visually distinct and readable in order, so the viewer can tell where the process starts and where it ends

- Stage 1 - 外部输入区
  - place 4 incoming threat/input cards on the far left:
    - Prompt Injection
    - Dangerous Command
    - Unauthorized DM
    - Cross-session contamination
  - these should look like incoming requests or attack vectors, not inner modules

- Stage 2 - 谁能进来
  - place one gate box labeled "身份与入口控制"
  - include 2 gate labels:
    - 用户授权
    - Unauthorized DM 拦截
  - annotation: "不是任何人、任何入口都能无条件触发 Agent"

- Stage 3 - 内容进入前
  - place one scanning box labeled "上下文文件注入扫描"
  - annotation: "在内容进入系统前先筛一遍"
  - show Prompt Injection risk being weakened or blocked here

- Stage 4 - 什么能执行
  - place one decision/approval box labeled "行为与工具控制"
  - include 3 checks:
    - 危险命令审批
    - 输入参数净化
    - 技能安全审计
  - annotation: "先判断能不能做，再判断怎么做"

- Stage 5 - 执行时能碰到什么
  - place one environment boundary box labeled "运行时隔离"
  - include 3 protections:
    - 容器隔离
    - 跨会话隔离
    - task_id / 环境边界
  - annotation: "就算执行，也不能无限制碰到所有东西"

- Stage 6 - Agent Execution Core
  - place one compact final runtime box on the far right
  - inside show 3 tiny labels:
    - 工具执行
    - 结果回写
    - 状态更新
  - this box should feel protected by the previous checkpoints, not exposed

- Use colored stop/block markers on the main line to show where each threat is intercepted:
  - Unauthorized DM mainly blocked at Stage 2
  - Prompt Injection mainly blocked at Stage 3
  - Dangerous Command mainly blocked at Stage 4
  - Cross-session contamination mainly blocked at Stage 5

- Add one small lower-side runtime note:
  - label: "安全不是单点模块"
  - annotation: "approval.py / terminal_tool.py / prompt_builder.py / skills_guard.py 分布协同"

- Add one green design-strength callout:
  - label: "设计亮点"
  - annotation: "上下文进入前扫注入，命令执行前做审批，技能加载前做审计，再叠加环境和会话隔离"

- Add one orange design-tradeoff callout:
  - label: "设计代价"
  - annotation: "覆盖更全，但安全逻辑分散，理解更难；安全门越多，交互摩擦和误报也会上升"

- Add one bold architectural judgment note near the bottom-center:
  - "安全不是一堵墙，而是一串门"

**Bottom Section (Interpretation Strip - 25%):**

- Create a horizontal 3-step interpretation strip:
  1. 先决定谁能进
  2. 再决定什么能做
  3. 最后限制执行边界
- Under each step add one compact explanation:
  - 先决定谁能进："用户授权 / 非法入口拦截"
  - 再决定什么能做："危险命令审批 / 参数净化 / 技能审计"
  - 最后限制执行边界："容器隔离 / 跨会话隔离 / 环境边界"
- Add one conclusion sentence centered at bottom:
  "Hermes 把安全看成运行时结构问题：不只审输出，更要控制谁能触发、什么能执行、执行时能碰到什么"
- Add footer label:
  "Hermes Agent 对象拆解 / 12"

**What Must Be Clear in the Diagram:**

- Security is not one final moderation step
- Different attack types are stopped at different checkpoints
- Entry control, execution approval, and runtime isolation are separate concerns
- The protection model is designed for real-world tool use, not only text generation
- The image must visually communicate this judgment:
  "安全不是一堵墙，而是一串门"

**Suitable Diagram Types to Combine:**

- Left-to-right security-gate flow
- Threat-input cards
- Stop-point markers on the main path
- Security checkpoint boxes
- Distributed security note callouts
- Protected runtime core
- Bottom interpretation timeline

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Pure white background
- Strong left-to-right structure with clear start/end direction
- Dense security callouts, but easy to understand at a glance
- Should feel like runtime threat modeling, not like a generic antivirus infographic
- Composition ratio:
  - 50% detailed schematic illustration
  - 25% text labels and technical callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for rings, labels, frames, and runtime core
- Bright blue (#3498DB) for legitimate control flows and safe boundaries
- Green (#16A085) for approved/safe paths and strong protection cues
- Orange (#E67E22) for threats, risk arrows, and tradeoff callouts
- Light gray for secondary guides and helper lines
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep technical terms in English where appropriate: Agent Execution Core, Prompt Injection, Dangerous Command, Unauthorized DM, Cross-session contamination, task_id
- Title should be bold and visually strong
- Threat labels should remain compact but readable on mobile

**Overall Feel:**

- Serious and structural
- Makes Agent security feel like a systems problem, not a content policy problem
- Visually strong and easy to scan
- Conveys both protection depth and operational tradeoffs
- Suitable for Xiaohongshu-style technical carousel

Style: Detailed technical hand-drawn infographic, layered runtime security and isolation architecture, concentric defense rings with threat-path modeling, pure white background
Style: Detailed technical hand-drawn infographic, staged runtime security-gate architecture, left-to-right threat interception flow, pure white background
