# Hermes Agent对象拆解：第 1 张封面图文生图脚本

Create a highly detailed technical cover infographic for social media in hand-drawn sketch style on pure white background. The theme is "Hermes Agent 对象拆解：一个学习型 Agent Runtime 由什么构成？".

**Design Concept:**
Use a layered runtime-architecture metaphor instead of a radial layout: modules should be placed according to their role in the processing stack, with clear upstream/downstream relationships and one visible main execution path running through the whole system. The image should immediately communicate that Hermes is not a pile of isolated features, but a coordinated Agent Runtime composed of entry, orchestration, context assembly, model routing, tool execution, memory, delivery, scheduling, security, and extension layers.

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "Hermes Agent 对象拆解"
- Subtitle below: "一个学习型 Agent Runtime 由什么构成？"
- Small lead sentence under subtitle: "不是另一个聊天助手，而是一台把会话、记忆、技能、执行、安全、调度接起来的系统机器"
- Typography should have strong hierarchy, centered composition, clean engineering-poster feel

**Central Section (Hero System Diagram - 60%):**
Create a dense layered architecture overview diagram with the following structure:

- Build the picture as a vertical processing stack with a strong top-to-bottom main path
- Use 6 horizontal architecture bands, each band labeled and visually separated by thin blueprint divider lines

- Band 1 - 任务入口层
  - place 5 small entry nodes across the top:
    - CLI
    - Gateway
    - ACP
    - API
    - Batch
  - all five converge into one intake box labeled "统一任务入口"
  - mini annotation: "不同入口进入同一个 Agent 会话"

- Band 2 - 主控编排层
  - place one dominant box in the center: "Agent Loop"
  - inside the box, show the mini loop:
    - 接收输入
    - 组装上下文
    - 模型判断
    - 调工具
    - 回填结果
    - 收敛输出
  - to the left of Agent Loop, place "Memory & Session"
    - mini annotation: "会话状态 / 长短期记忆 / 回写"
  - to the right of Agent Loop, place "Security & Isolation"
    - mini annotation: "审批 / 权限边界 / 风险控制"
  - show arrows:
    - Memory & Session → Agent Loop
    - Agent Loop → Memory & Session
    - Security & Isolation → Tool System
    - Security & Isolation → Execution Backends

- Band 3 - 上下文组装层
  - place one wide assembly strip under Agent Loop labeled "Prompt 组装层"
  - feed into it with several small material cards:
    - SOUL
    - MEMORY
    - USER
    - AGENTS
    - 项目上下文
    - Skills 索引
    - Tool 描述
  - arrow from Prompt 组装层 upward into Agent Loop
  - mini annotation: "把人格、记忆、用户偏好、项目信息装配成工作底稿"

- Band 4 - 模型与能力决策层
  - place "Provider 路由层" under Prompt 组装层
  - beside it place "Skills System"
  - show relation:
    - Agent Loop → Provider 路由层
    - Agent Loop → Skills System
    - Skills System → Prompt 组装层
  - mini annotation for Provider: "模型选择 / 路由 / 成本与能力匹配"
  - mini annotation for Skills: "专项能力注入 / 任务增强"

- Band 5 - 工具执行层
  - place two strongly connected boxes:
    - Tool System
    - Execution Backends
  - show main arrow:
    - Provider 路由层 / Agent Loop → Tool System → Execution Backends
  - add a return arrow:
    - Execution Backends → Agent Loop
  - mini annotation for Tool System: "工具描述 / 参数结构 / 调用接口"
  - mini annotation for Execution Backends: "命令执行 / 沙箱 / 外部环境"

- Band 6 - 外围连接与持续运行层
  - place three supporting boxes near the bottom/right side:
    - Gateway & Delivery
    - Cron Scheduler
    - Plugin / MCP / External Memory
  - show relation arrows:
    - Gateway & Delivery ↔ 入口层
    - Cron Scheduler → 统一任务入口
    - Plugin / MCP / External Memory ↔ Tool System
    - Plugin / MCP / External Memory ↔ Memory & Session
  - mini annotation: "对外连接、定时触发、扩展协议"

- Add one thick highlighted main path running through the entire stack:
  - 任务进入 → Agent Loop → Prompt 组装 → Provider 路由 → Tool System → Execution Backends → 结果回填 → 输出交付
- Add two secondary feedback paths in thinner lines:
  - 记忆回写路径
  - 安全审批路径
- Use technical leader lines to connect callouts to key boxes
- Make the overall composition feel like a runtime architecture teardown with explicit dependencies rather than isolated feature bubbles

**Bottom Section (Reading Guide - 20%):**

- Add a horizontal guide strip showing that this is the opening image of a series
- Show a compact progression line with 4 grouped phases:
  1. 入口与主循环
  2. 上下文与模型路由
  3. 工具、执行、记忆、技能
  4. 网关、调度、安全、扩展
- Under the progression line, add one guiding sentence:
  "下面 12 张，逐个掰开看"
- Add a small footer label:
  "Hermes Agent 对象拆解 / 01"

**Key Visual Metaphor:**

- Hermes Agent should feel like a multi-layer runtime pipeline rather than a single center point
- Different modules should visibly occupy different processing layers and control boundaries
- The whole image should convey "不是功能清单，而是有主链路、有支撑层、有反馈回路的运行时机器"
- Visual impression should be closer to a technical architecture blueprint than a marketing poster

**Suitable Diagram Types to Combine:**

- Layered system architecture diagram
- Main-path execution flow schematic
- Supporting dependency arrows
- Module cards with subsystem icons
- Feedback loop arrows
- Architecture band labels
- Reading-path timeline strip at bottom

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Professional engineering documentation style
- Clean blueprint-like layout on pure white background
- Dense but readable information hierarchy
- Strong structural symmetry with slight sketch irregularity
- Small labels and rich callouts integrated tightly into the drawing
- 55% diagram illustration, 15% text labels, 30% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for main outlines, text, and architecture frames
- Bright blue (#3498DB) for runtime arrows, loop emphasis, and central orchestration flow
- Green (#16A085) for memory, skills, and growth-related modules
- Orange (#E67E22) for security, approval, and risk-control highlights
- Light gray for secondary guides and construction lines
- Pure white background

**Typography:**

- All major annotations in simplified Chinese
- Keep these technical terms in English where appropriate: Agent, Runtime, Prompt, Provider, Tool System, Memory, Session, Skills, Gateway, Cron, Plugin, MCP
- Title font should be bold and larger than normal social cover text
- All annotations should be about 10% larger than baseline for readability on mobile

**Overall Feel:**

- Clean and modern
- Systematic and explanatory
- Professional but visually striking
- Immediately communicates "Hermes 是运行时，不是聊天壳"
- Optimized for Xiaohongshu/social cover readability at a glance

Style: Detailed technical hand-drawn cover infographic, layered runtime architecture blueprint, explicit module relationships and processing hierarchy, dense annotations, pure white background
