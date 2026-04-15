# Harness Engineering 是什么：第 3 张“工具接入与权限边界”文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "Agent 一旦开始做事，第一层问题就是工具和权限". The image should make it immediately clear that the first real engineering layer of an Agent is not model intelligence, but the controlled interface between the Agent core and the external world. This should feel like a "left-to-right gated access architecture" diagram, not a circular feature map.

**Design Concept:**

Use a "三段式过闸结构" metaphor:

- left side = external world tools
- middle section = permission and approval gates
- right side = Agent core

The key visual judgment is:

**工具决定它能碰到什么，权限决定它能不能碰，Harness 决定它会不会越界。**

The picture should make viewers feel that tools are not directly wired into the Agent. There is a deliberate gated boundary section between them. This middle control section is the first true Harness layer. The viewer should know where to start reading immediately: left = tools, middle = control gates, right = Agent.

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "Agent 一旦开始做事，第一层问题就是工具和权限"
- Subtitle below: "没有工具，它只会说；没有边界，它就会乱做"
- Small supporting sentence:
  "真正危险的从来不是‘能不能接工具’，而是‘允许它做什么、在哪些条件下做、出了问题谁来拦住它’"
- Typography should feel like a technical editorial blueprint, not a security marketing poster

**Central Section (Hero Diagram - 58%):**

Create one dominant horizontal gated-access composition with three clear regions:

- Left region - 外部工具区:
  - place 5 or 6 tool cards in a clear vertical or staggered grid on the left side, not in a ring
  - recommended tool cards:
    - filesystem
    - terminal
    - browser
    - database
    - internal API
    - message / webhook
  - each tool card should have one tiny cue:
    - filesystem: 项目文件 / 配置 / 文档
    - terminal: 命令执行 / 构建 / 测试
    - browser: 页面读取 / 搜索 / 表单
    - database: 查询 / 更新 / 连接
    - internal API: 企业系统 / 服务接口
    - message / webhook: 外部通知 / 自动触发
  - add a small left-zone label:
    - "外部世界入口"
  - the tools should feel reachable, concrete, and slightly heterogeneous

- Middle region - 权限边界闸门:
  - this is the most important part of the image
  - place a vertical gated control strip or segmented checkpoint wall between tools and Agent
  - label this whole middle section:
    - 权限边界层
    - permission boundary
  - split the middle section into 4 checkpoint modules stacked vertically:
    - allowlist
    - permissions
    - approval
    - guardrails
  - each checkpoint module should have tiny internal Chinese annotations:
    - allowlist: 允许哪些工具出现
    - permissions: 允许哪些资源被访问
    - approval: 哪些动作必须人工确认
    - guardrails: 哪些危险路径要被中断
  - use colored status markers on the gates:
    - green = allowed
    - orange = blocked
    - yellow = approval required
  - this middle section should visually look like decision-making infrastructure, not decoration
  - add one small note near the control strip:
    - "Harness 的第一层，不是扩能力，而是先收边界"

- Right region - Agent 核心:
  - place one clearly framed runtime box on the right labeled:
    - Agent Core
  - inside the core, add 4 compact internal labels:
    - 理解任务
    - 生成动作意图
    - 请求外部操作
    - 接收结果回填
  - visually this core should feel active but bounded
  - add one small side note:
    - "不是直接碰工具，而是先申请动作"

- Access control paths:
  - draw multiple horizontal access paths running left <-> middle <-> right
  - no direct Agent-to-tool access should exist; all paths must visibly cross the middle gate section
  - show 4 or 5 example paths with different statuses:
    - filesystem -> allowed
    - terminal -> approval required
    - browser -> allowed
    - database -> blocked or limited
    - internal API -> scoped access
  - annotate example paths with small labels:
    - read-only
    - sandboxed
    - human approval
    - denied
  - some lines should stop at the gate to show blocked access
  - one or two lines should pass through in green to show controlled permission

- Boundary contrast:
  - make the middle gate visually feel like a semi-transparent engineering checkpoint wall, not a cage
  - it should be obvious that the gate is doing decision work
  - the viewer should be able to read the whole image in one sweep from left to right

- Risk illustration:
  - add one small orange risk callout near one blocked path:
    - "没有边界，Agent 可能把‘会做’误变成‘乱做’"
  - add one green system-strength callout near one approved path:
    - "真正成熟的系统，不是放开所有工具，而是清楚定义哪条路能走"

**Bottom Section (Interpretation Strip - 22%):**

Create a bottom horizontal interpretation strip with 4 compact stages:

1. "接入工具"
   - tiny explanation: "接触外部世界"
2. "建立边界"
   - tiny explanation: "不是默认开放"
3. "控制动作"
   - tiny explanation: "按权限和审批放行"
4. "安全执行"
   - tiny explanation: "既能做事，也不越界"

- Connect the four stages with arrows
- Add one bottom conclusion sentence:
  "Harness 的第一层价值，不是给 Agent 更多手，而是先告诉它哪些门能进、哪些动作不能做"
- Add footer label:
  "Harness Engineering / 03"

**What Must Be Clear in the Diagram:**

- Tools are external, not inside the Agent
- Permission boundary is a distinct middle engineering layer
- Every external action must cross that gated middle section
- The image must not imply that all tools are equally open
- The viewer should immediately understand:
  - tools expand reach
  - permissions define scope
  - harness prevents overreach
- Reading order must be obvious at first glance: left -> middle -> right

**Suitable Diagram Types to Combine:**

- Left-to-right gated architecture diagram
- Tool grid / tool board on the left
- Permission checkpoint wall in the middle
- Agent runtime box on the right
- Access-path status annotations
- Bottom interpretation strip

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Professional engineering documentation style
- White background with clear left-to-right boundary hierarchy
- Dense annotations but obvious reading order
- Not a cybersecurity warning poster, more like a runtime control anatomy page
- Composition ratio:
  - 55% detailed schematic illustration
  - 20% labels and technical callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, titles, and core/system frames
- Bright blue (#3498DB) for access paths, tool connection lines, and structural arrows
- Teal (#16A085) for safe/allowed routes and stable control signals
- Orange (#E67E22) for blocked paths, risk warnings, and overreach danger
- Yellow (#F4B942) for approval-required transitions
- Light gray for helper lines and secondary annotations
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep only these technical terms in English where appropriate: Agent Core, filesystem, terminal, browser, database, internal API, allowlist, permissions, approval, guardrails, sandboxed, read-only
- Title should be bold and large
- Secondary labels should be compact but readable on mobile

**Overall Feel:**

- Clear and controlled
- More structural than flashy
- Immediately understandable at a glance
- Makes the "tools -> permission gates -> agent" relationship visually unforgettable
- Suitable for Xiaohongshu-style knowledge carousel third slide

Style: Detailed technical hand-drawn infographic, left-to-right gated access architecture, external tools crossing permission checkpoints before reaching Agent core, pure white background
