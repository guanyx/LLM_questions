# Agent记忆系统怎么实现：第 4 张“大多数记忆系统，先坏在写入链路”图文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "大多数记忆系统，先坏在写入链路". The image should make it immediately clear what an engineer should do in practice when new information arrives: what should be written immediately, what should go into an episodic candidate pool, and what should never become long-term memory. This page must feel like an operational write-policy board, not a generic architecture concept page.

**Design Concept:**

Use a "write-policy operating board" metaphor. Because the target canvas is 3:4 portrait ratio, do NOT make this page just another abstract pipeline. Instead, build a portrait-oriented decision board that directly answers three operational questions:

- 什么该立刻写？
- 什么先放候选池？
- 什么根本不要写？

The image should feel like a practical decision manual that a builder can use while implementing memory writes. The key message is: memory systems fail early when they lack a strict write policy.

**Layout Structure:**

**Top Section (Title Area - 18%):**

- Main title in bold, large font: "大多数记忆系统，先坏在写入链路"
- Subtitle below: "问题往往不是取不出来，而是一开始就写错了东西"
- Small supporting sentence:
  "真正的实操难点不是“能不能记”，而是“哪些东西该立刻写、延后写，还是根本不该写”"
- Typography should feel like a technical runtime control board, not a generic product slide

**Central Section (Hero Diagram - 68%):**

Create a portrait-oriented write-policy board with one strong top-to-bottom decision structure.

- Overall composition:
  - upper area = incoming information strip
  - center = one dominant write-policy decision board
  - lower-middle = three practical outcome zones
  - lower side = one execution timing strip
  - side = one orange "千万别这么写" warning area
  - the page should read like:
    - 先看新信息属于什么类型
    - 再做写入判定
    - 再决定进入哪种处理路径
    - 最后明确写入时机

- Incoming information strip:
  - place 5 compact incoming-information cards across the upper area
  - suggested cards:
    - 用户偏好表达
    - 工具执行结果
    - 文件改动结果
    - 报错与根因
    - 长对话中间结论
  - these cards should feel heterogeneous and ambiguous: some are worth writing, some are not
  - add one small label above the strip:
    - incoming information
    - 新信息进入系统
  - mini annotation:
    - "不是每条新信息都该进入长期记忆"

- Source-of-truth note:
  - place one small note near the upper area:
    - source of truth
    - "原始日志可以保留作回放依据，但这不等于它已经成为长期记忆"
  - this note should be visually secondary, because this page is about write policy, not raw log storage

- Central write-policy decision board:
  - place one large central object labeled:
    - write policy
    - 这条信息该怎么处理？
  - inside the board, show 3 compact practical questions:
    - 跨会话还成立吗？
    - 下次还会复用吗？
    - 写进去会不会污染长期记忆？
  - add one small second-row prompt group:
    - 立即写？
    - 放候选池？
    - 不写长期记忆？
  - this board must visually feel like the hero object of the page
  - add one mini annotation:
    - "不是见啥都记，而是见啥先分类"

- Practical outcome zone A - 立即写入
  - place this as one of the major lower-middle result cards
  - title:
    - 立即写
    - sync write
  - split internally into 2 sub-targets:
    - 写入 Semantic Memory
    - 写入 Procedural Memory
  - Semantic examples:
    - 明确用户偏好
    - 稳定项目约束
    - 环境事实变更
  - Procedural examples:
    - 已验证修复流程
    - 可复用工具套路
    - 高成本踩坑后的稳定做法
  - add one mini rule:
    - "高价值、稳定、未来会复用"

- Practical outcome zone B - 进入候选池
  - place this as the second major lower-middle result card
  - title:
    - 先放候选池
    - episodic candidate pool
  - examples:
    - 中间尝试
    - 工具轨迹
    - 失败过程
    - 长对话摘要
  - add one mini rule:
    - "先保留，后面再固化"
  - small note:
    - "适合后台 consolidation，不适合立刻升格成长期记忆"

- Practical outcome zone C - 不写长期记忆
  - place this as the third major result card
  - title:
    - 不写长期记忆
    - keep out
  - examples:
    - 一次性情绪表达
    - 临时 TODO 状态
    - 未验证猜测
    - 低价值噪音
  - add one mini rule:
    - "可以留在会话或日志里，但不要污染长期层"

- Outcome-zone design requirement:
  - these three outcome zones should feel like practical operator choices
  - they should not look like abstract memory categories
  - the viewer should be able to answer:
    - "面对一条新信息，我应该把它送去哪一格？"

- Execution timing strip:
  - place one compact strip below the three outcome zones
  - split it into two timing labels:
    - 立刻落盘
    - 后台固化
  - map the three outcome zones to timing:
    - 立即写入 -> 通常对应立刻落盘
    - 进入候选池 -> 通常对应后台固化
    - 不写长期记忆 -> 不进入长期持久化
  - this strip should make the operational timing explicit without turning the page into another pipeline layer

- Orange anti-pattern zone:
  - place one orange caution block on one side of the lower area
  - title:
    - 千万别这么写
  - include 3 concrete anti-pattern cards:
    - "这次先简单写" 被记成永久偏好
    - 一次失败尝试被写成通用流程
    - 一长段工具日志被直接塞进长期记忆
  - add one blunt note:
    - "记错比忘记更危险，脏记忆比没记忆更难救"
  - this block must read like practical failure cases, not generic principles

- Structural emphasis:
  - the central write-policy board must be the hero object of the page
  - the three lower outcome zones should feel like operator decisions, not taxonomy boxes
  - the execution timing strip should feel like implementation guidance
  - the anti-pattern area should warn through concrete examples, not slogans

- Connection semantics (important):
  - this page is a practical decision board, so the only strong causal path should be:
    - incoming information -> write policy decision board -> three outcome zones
  - that main path should use strong arrows
  - the three outcome zones are parallel choices, not sequential stages
  - do NOT connect:
    - 立即写入 -> 进入候选池
    - 候选池 -> 不写长期记忆
    - Semantic -> Procedural
  - the execution timing strip should be linked downward from the three outcome zones as an implementation mapping layer
  - those links mean:
    - "这个选择通常对应什么写入时机"
    - not "所有路径最终都会进入同一个持久化过程"
  - the anti-pattern block should stay off the main path
  - connect the anti-pattern zone only with dashed caution markers or local warning callouts
  - line meaning on this page should be strict:
    - strong arrow = decision flow
    - branch arrow = operator choice split
    - thin downward link = timing mapping
    - dashed warning line = anti-pattern / risk reminder
    - grouped box = same operational category

**Bottom Section (Interpretation Area - 14%):**

- Keep the bottom area compact
- Add one short conclusion sentence centered at the bottom:
  "写入链路决定记忆质量，后面的检索只是放大前面的选择"
- Add a small footer label:
  "Agent记忆系统怎么实现 / 04"

**What Must Be Clear in the Diagram:**

- Not all incoming information deserves long-term storage
- The first implementation question is "which write bucket should this go to?"
- Immediate write, candidate-pool write, and no-write are different operational choices
- Persistence timing is separate from memory category
- The anti-patterns are caused by wrong write decisions, not by weak retrieval
- Connector logic must stay accurate:
  - main path arrows are decision flow
  - outcome zones are branching choices, not sequencing
  - timing links are mappings, not causal chains

**Visual Elements That Should Appear:**

- Incoming information cards
- One dominant write-policy decision board
- Three practical outcome zones
- One execution timing strip
- One anti-pattern warning block
- One small source-of-truth note
- Precise directional arrows
- Footer label

**Visual Elements That Must NOT Appear:**

- One giant storage bucket receiving everything directly
- Arrows that make the three outcome zones look sequential
- A retrieval-heavy layout
- Brain illustration
- End-to-end full agent architecture
- A radial wheel of event types
- A single undifferentiated "save memory" box

**Suitable Diagram Types to Combine:**

- Technical write-policy board
- Central decision board
- Three-way operator choice schematic
- Timing-mapping strip
- Anti-pattern warning block

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Professional engineering documentation style
- White background with editorial clarity
- Portrait-first composition optimized for 3:4 canvas
- Strong decision reading flow from top to lower-middle
- Dense but controlled information hierarchy
- 54% diagram illustration, 18% labels and callouts, 28% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, titles, main frames, and destination cards
- Bright blue (#3498DB) for the main decision flow, gate arrows, and operator-choice structure
- Green (#16A085) for correct write decisions and high-value keep/write zones
- Orange (#E67E22) for the anti-pattern block, memory pollution risk, and caution accents
- Light gray for helper dividers, secondary notes, and non-primary scaffolding
- Pure white background

**Typography:**

- All major annotations in simplified Chinese
- Keep only these technical terms in English where appropriate: source of truth, sync write, async consolidation, Semantic Memory, Procedural Memory
- Title font should be bold and larger than standard social infographic text
- Secondary labels should be compact but clearly readable on mobile

**Overall Feel:**

- Clean and operational
- More like an implementation cheat sheet than a concept poster
- Makes the write-decision problem obvious at a glance
- Clearly communicates what to write now, what to defer, and what to keep out
- Visually strict enough that wrong arrow semantics are hard to introduce
- Suitable for Xiaohongshu-style technical carousel fourth slide

Style: Detailed technical hand-drawn write-policy infographic, portrait-oriented decision board, three-way operator choice layout, execution timing strip, practical anti-pattern warning block, pure white background
