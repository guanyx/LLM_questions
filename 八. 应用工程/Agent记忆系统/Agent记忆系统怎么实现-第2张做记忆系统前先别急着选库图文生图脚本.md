# Agent记忆系统怎么实现：第 2 张“做记忆系统前，先别急着选库”图文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "做记忆系统前，先别急着选库". The image should make it immediately clear that before choosing any storage stack, the real job is to define what the memory system is supposed to improve: cross-session continuity, long-horizon task stability, experience reuse, or cost control. This should feel like a goal-definition board, not a database comparison chart.

**Design Concept:**

Use a "goal-definition decision board" metaphor. Because the target canvas is 3:4 portrait ratio, do NOT treat this page like a cover poster with one central object and surrounding satellites. Instead, structure the page according to the actual content logic of slide 2: first raise the decision question, then expand the 4 real engineering goals, and finally show how they are validated and where people go wrong. The image should feel like the reader is looking at a planning dossier that forces goal definition before any architecture or storage choice.

**Layout Structure:**

**Top Section (Title Area - 18%):**

- Main title in bold, large font: "做记忆系统前，先别急着选库"
- Subtitle below: "先回答你到底想解决连续性、长任务、经验沉淀，还是成本问题"
- Small supporting sentence:
  "没有验收目标的记忆系统，最后往往只会变成一堆昂贵的历史数据"
- Typography should feel like a technical editorial page, not a storage vendor poster

**Central Section (Hero Diagram - 68%):**

Create a portrait-oriented goal-definition board with a strong top-to-bottom information structure.

- Overall composition:
  - upper area = one problem-definition header board
  - middle area = one balanced 2x2 goal matrix
  - lower area = one compact validation strip plus one anti-pattern warning strip
  - do NOT use a central hub-and-spoke layout
  - the page should read like:
    - 先问问题
    - 再看四类目标
    - 最后看验收与误区

- Problem-definition header board:
  - place one wide structured board right below the title area
  - label it:
    - Memory Goals
    - 先定义目标，再谈架构
  - inside the board, show 3 compact guiding questions laid out horizontally or vertically:
    - 你要提升什么？
    - 你怎么验收？
    - 你愿意付出什么成本？
  - add one small side note:
    - "选型是结果，不是起点"
  - this board should feel like the setup for the 2x2 matrix below, not like the page's hero object

- Goal Panel 1 - 跨会话连续性
  - place this in the upper-left cell of the 2x2 goal matrix
  - title:
    - continuity
    - 跨会话连续性
  - compact explanation:
    - "用户不想重复背景"
  - add 3 tiny metric tags:
    - preference consistency
    - context carry-over
    - fewer repeated instructions
  - add one mini visual cue:
    - two separated sessions linked by a stable memory bridge

- Goal Panel 2 - 长任务稳定性
  - place this in the upper-right cell of the 2x2 goal matrix
  - title:
    - long-horizon stability
    - 长任务稳定性
  - compact explanation:
    - "任务拉长后不能掉线"
  - add 3 tiny metric tags:
    - long task success rate
    - state continuity
    - fewer recovery failures
  - add one mini visual cue:
    - a multi-step task board that stays connected across many steps

- Goal Panel 3 - 经验沉淀能力
  - place this in the lower-left cell of the 2x2 goal matrix
  - title:
    - experience reuse
    - 经验沉淀能力
  - compact explanation:
    - "同类问题第二次要更快做对"
  - add 3 tiny metric tags:
    - repeated error rate
    - reuse of validated steps
    - skill accumulation
  - add one mini visual cue:
    - one failed attempt evolving into a reusable playbook card

- Goal Panel 4 - 成本可控
  - place this in the lower-right cell of the 2x2 goal matrix
  - title:
    - cost control
    - 成本可控
  - compact explanation:
    - "召回和重排不能把系统拖死"
  - add 3 tiny metric tags:
    - prompt cost
    - latency
    - retrieval overhead
  - add one mini visual cue:
    - a cost gauge kept below a danger zone while memory quality stays usable

- Goal matrix structure:
  - all four panels should have matched visual weight and similar internal density
  - use a clean grid or dossier-card layout so the page feels like a structured classification, not a conceptual poster
  - each panel can carry one tiny shorthand tag near the title:
    - continuity -> "记得住"
    - long-horizon stability -> "不断片"
    - experience reuse -> "下次更会做"
    - cost control -> "跑得起"
  - if connector lines are used, keep them light and only use them from the top header board down into the matrix as setup lines, not as hub-and-spoke lines

- Connection semantics (important):
  - this page is mainly about classification and decision framing, not process flow
  - do NOT draw strong directional arrows between the four goal panels
  - do NOT connect the four goal panels to each other, because they are parallel goal types, not sequential stages
  - the top problem-definition board may connect downward into the 2x2 goal matrix with light setup lines or bracket-like guide lines only
  - those lines mean:
    - "these four goals are candidate target types"
    - not "the system flows from one panel into another"
  - if the validation strip is visually linked to the 2x2 matrix, use shared alignment, braces, or very light guide lines
  - do NOT use arrows from each goal panel directly into the validation strip, otherwise the page starts reading like a workflow
  - the anti-pattern strip should be visually separated as a caution zone
  - do NOT draw arrows from the anti-pattern strip into the goal matrix, because that falsely implies it is an input or an alternative branch
  - line meaning on this page should be very strict:
    - light guide line = classification / framing relation
    - divider or bracket = grouping relation
    - strong arrow = avoid unless absolutely necessary

- Validation strip:
  - place one compact horizontal strip directly below the 2x2 matrix
  - label:
    - 验收指标
  - include 4 tiny score labels:
    - consistency
    - task success
    - reuse gain
    - cost / latency
  - this strip should feel like the engineering consequence of the 4 goals above
  - visually it should read as:
    - 目标不同
    - 验收指标也不同
  - if any connector is used here, it should express "validation perspective under the whole matrix", not one-to-one causal mapping

- Anti-pattern warning zone:
  - place one compact orange caution strip near the bottom of the hero area
  - title:
    - 常见误区
  - inside it place 3 short anti-pattern tags:
    - 只堆历史
    - 只做向量库
    - 只加上下文长度
  - add one blunt note:
    - "看起来很强，实际上无法验收"
  - this strip should visually contrast with the four valid goal panels above
  - it should feel like the wrong instinct that appears when people skip the goal-definition step
  - this zone should be separated by color block, spacing, or frame treatment rather than by directional arrows

- Structural emphasis:
  - this page should not feel like "four random benefits around a title"
  - it should feel like a structured decision board where architecture comes later
  - the central message must be:
    - first define what kind of memory problem you are solving
    - then choose the architecture and storage accordingly
  - use gentle board dividers and light setup lines, but avoid turning the page into either a flowchart or a cover-style radial layout

**Bottom Section (Interpretation Area - 14%):**

- Keep the bottom area compact
- Add one short conclusion sentence centered at the bottom:
  "记忆系统不是为了显得高级，而是为了让某类能力变得可验收、可优化、可权衡"
- Add a small footer label:
  "Agent记忆系统怎么实现 / 02"

**What Must Be Clear in the Diagram:**

- The page is about goal definition, not storage selection
- All four goals should feel concrete and engineering-relevant
- The reader should immediately understand that "memory system" has multiple possible jobs
- The real mistake is jumping from "I need memory" directly to "which database should I use"
- The anti-pattern zone should make the wrong instinct visible
- The visual logic should be:
  - question first
  - goal classification second
  - validation and anti-patterns last
- The connector logic must stay accurate:
  - no fake process arrows
  - no implied causality between parallel goal types
  - no misleading arrows from anti-patterns into the valid goal system

**Visual Elements That Should Appear:**

- One top problem-definition board
- Four balanced goal panels in a 2x2 matrix
- Metric tags under each goal
- One validation strip
- One anti-pattern warning strip
- Footer label

**Visual Elements That Must NOT Appear:**

- Vendor logos
- Database product matrix
- Giant vector database cylinder
- Full end-to-end runtime pipeline
- Brain illustration
- Futuristic hologram storage dashboard
- One huge central hero object dominating the page

**Suitable Diagram Types to Combine:**

- Technical planning board
- 2x2 goal matrix
- Problem-definition header board
- Validation strip
- Anti-pattern warning strip

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Professional engineering documentation style
- White background with editorial clarity
- Portrait-first composition optimized for 3:4 canvas
- Dense but balanced information hierarchy
- Strong top-to-bottom structure with a balanced middle matrix
- 50% diagram illustration, 20% labels and callouts, 30% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, titles, central frames, and main labels
- Bright blue (#3498DB) for connections, guide lines, and structure emphasis
- Green (#16A085) for healthy engineering goals and metrics that imply successful optimization
- Orange (#E67E22) for the anti-pattern warning zone and "无法验收" emphasis
- Light gray for helper grids, score labels, and secondary notes
- Pure white background

**Typography:**

- All major annotations in simplified Chinese
- Keep only these technical terms in English where appropriate: Memory Goals, continuity, long-horizon stability, experience reuse, cost control, consistency, latency
- Title font should be bold and larger than standard social infographic text
- Secondary labels should be compact but clearly readable on mobile

**Overall Feel:**

- Clean and sharp
- More like a technical planning dossier than a product slide
- Clearly communicates that architecture selection must follow goal definition
- Makes the page feel pragmatic, not abstract
- Immediately tells the reader: "你不是先缺数据库，你是先缺目标定义"
- Suitable for Xiaohongshu-style technical carousel second slide

Style: Detailed technical hand-drawn planning infographic, problem-definition header board, 2x2 engineering goal matrix, validation strip, anti-pattern warning strip, portrait-oriented 3:4 layout, pure white background
