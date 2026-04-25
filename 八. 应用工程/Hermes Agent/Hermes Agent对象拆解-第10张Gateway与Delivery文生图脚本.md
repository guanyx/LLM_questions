# Hermes Agent对象拆解：第 10 张Gateway 与 Delivery文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "Hermes 为什么能生活在 Telegram、Slack、Discord 里？".

**Design Concept:**
Use a concrete message-journey metaphor instead of an abstract bus diagram: the image should follow one real message as it enters from a chat platform, passes through authorization and session routing, reaches the same AIAgent core, and then gets delivered back out. The visual emphasis should be on one visible request lifecycle, while other platforms appear as parallel entry surfaces on the side.

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "Hermes 为什么能生活在 Telegram、Slack、Discord 里？"
- Subtitle below: "Gateway 不是“多开几个聊天窗口”，而是让同一个 Agent 穿过不同平台继续工作"
- Small supporting sentence: "多平台支持的难点，不是接几个 Bot，而是把不同平台统一成同一套 Agent 行为"
- Typography should feel like a systems poster, not a social-media integration ad

**Central Section (Hero Diagram - 55%):**
Create a concrete left-to-right message journey diagram with one main example flow and several side platforms:

- Build one thick main path across the middle of the image:
  - Telegram 用户消息
  - authorize
  - route 到正确 session
  - 进入 AIAgent
  - 生成结果
  - deliver 回 Telegram

- Stage 1 - 平台输入面
  - on the far left place one enlarged example platform card: Telegram
  - inside show a concrete incoming message bubble:
    - "帮我看下服务器日志"
  - make this the main example entry
  - beneath or beside it, place 5 smaller parallel platform tabs:
    - Slack
    - Discord
    - WhatsApp
    - Signal
    - Email
  - these smaller tabs should clearly look like“同类入口”，不是主视觉中心

- Stage 2 - Gateway Runner
  - place one medium-large process box labeled "Gateway Runner"
  - inside split it into 3 vertical subcells:
    - authorize
    - route
    - deliver
  - add one tiny note under the box:
    - "平台差异、会话映射、消息回传都在这里吸收"

- Stage 3 - Session Context
  - place one side box slightly below Gateway Runner labeled "Session Context"
  - annotation:
    - 会话 ID
    - 平台来源
    - 用户绑定
    - 历史状态
  - connect it to the "route" subcell
  - make it very clear that gateway 不只是转发消息，而是在维护会话语义

- Stage 4 - AIAgent
  - on the right place one stable runtime box labeled "AIAgent"
  - annotation: "同一个 Agent 核心，不随平台变化"
  - add tiny internal labels:
    - 读上下文
    - 处理任务
    - 生成输出

- Stage 5 - Delivery 返回
  - continue the main arrow from AIAgent back toward the left-lower side
  - deliver output back to the example Telegram card
  - show a returned message bubble:
    - "已分析日志，发现异常在 ..."
  - then add thinner secondary branches from Delivery to the other smaller platform tabs
  - this should communicate: 同一个 gateway 既能回原平台，也能把行为扩展到其它表面

- Add one green design-strength callout near the center:
  - label: "设计亮点"
  - annotation: "平台差异、会话路由、结果投递都被网关层吸收，同一个 Agent 因此能跨表面延续"

- Add one orange design-tradeoff callout near the smaller platform tabs:
  - label: "设计代价"
  - annotation: "媒体处理、鉴权方式、平台会话模型都不统一，多平台支持会放大边角复杂度"

- Add one bold judgment note under the main path:
  - "Gateway 不是多开窗口，而是把多平台统一成同一条会话入口"

- Important visual hierarchy:
  - one main example flow must be very concrete and完整
  - the other platforms only serve as parallel evidence
  - the viewer should instantly know where the message starts, where it is routed, and where it returns

**Bottom Section (Interpretation Strip - 25%):**

- Create a horizontal 3-step interpretation strip:
  1. 多平台输入
  2. 网关统一语义
  3. 同一个 Agent 持续工作
- Under each step add one compact explanation:
  - 多平台输入："Telegram / Slack / Discord / WhatsApp / Signal / Email"
  - 网关统一语义："authorize / route / deliver 都在这里完成"
  - 同一个 Agent 持续工作："不是每个平台都养一套独立脑子"
- Add one conclusion sentence centered at bottom:
  "Gateway 的价值不在接入数量，而在把多平台统一成同一条消息总线"
- Add footer label:
  "Hermes Agent 对象拆解 / 10"

**What Must Be Clear in the Diagram:**

- Gateway is not just a collection of platform connectors
- The main example message should visibly pass through authorization, routing, and delivery
- Session routing and delivery are first-class responsibilities
- Outputs return through the gateway, not through direct platform-specific logic in the core
- The image must visually communicate this judgment:
  "Gateway 不是多开窗口，而是多平台统一会话入口"

**Suitable Diagram Types to Combine:**

- Concrete message journey flow
- One enlarged example platform card
- Gateway process box with subcells
- Session-state side box
- Delivery return path
- Parallel platform tabs
- Bottom interpretation timeline

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Pure white background
- Strong left-to-right story flow
- Clear message flow from concrete user message → gateway → agent → returned message
- Dense annotations, but easy to parse at a glance
- Should feel like communication infrastructure, not a messaging app promotion page
- Composition ratio:
  - 50% detailed schematic illustration
  - 25% text labels and technical callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, frames, and labels
- Bright blue (#3498DB) for main routing lines and normalized message flow
- Green (#16A085) for stable session continuity and successful delivery cues
- Orange (#E67E22) for complexity/tradeoff callouts and authorization emphasis
- Light gray for helper structures, adapter strips, and background guidance
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep technical terms in English where appropriate: Gateway Runner, AIAgent, Delivery, Session Context, authorize, route, deliver, Telegram, Slack, Discord, WhatsApp, Signal, Email
- Title should be bold and visually strong
- Platform labels should be compact but mobile-readable

**Overall Feel:**

- Concrete and narrative
- Strong sense of one message traveling through a unified gateway lifecycle
- Makes multi-platform support feel like a runtime capability, not a cosmetic integration
- Easy to scan and immediately understandable
- Suitable for Xiaohongshu-style technical carousel

Style: Detailed technical hand-drawn infographic, concrete gateway message journey, multi-platform unified session routing and delivery architecture, pure white background
