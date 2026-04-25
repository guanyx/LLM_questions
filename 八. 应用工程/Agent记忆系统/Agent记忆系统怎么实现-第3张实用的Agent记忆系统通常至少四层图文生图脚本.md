# Agent记忆系统怎么实现：第 3 张“实用的 Agent 记忆系统，通常至少四层”图文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "实用的 Agent 记忆系统，通常至少四层". The image should make it immediately clear that Working Set, Episodic Memory, Semantic Memory, and Procedural Memory are not academic labels for completeness, but engineering layers with different distance to the current task, different retrieval behavior, and different lifecycle. This page should feel like a runtime layer anatomy board, not a process pipeline.

**Design Concept:**

Use a "memory layer anatomy / distance-to-context board" metaphor. Because the target canvas is 3:4 portrait ratio, do NOT draw the four layers as a long horizontal chain or as a four-step workflow. Instead, build a portrait-oriented stratified board: current context near the top, the four memory layers stacked from near to far beneath it, and one side legend explaining lifecycle and retrieval mode. The central message should be that memory architecture is about runtime role separation, not about naming more boxes.

**Layout Structure:**

**Top Section (Title Area - 18%):**

- Main title in bold, large font: "实用的 Agent 记忆系统，通常至少四层"
- Subtitle below: "不是为了概念完整，而是因为不同信息根本不该放在同一层"
- Small supporting sentence:
  "记忆失败往往不是没存，而是把不同生命周期的信息塞进了同一个地方"
- Typography should feel like a technical editorial anatomy page, not a concept poster

**Central Section (Hero Diagram - 68%):**

Create a portrait-oriented runtime layer board with strong top-to-bottom organization.

- Overall composition:
  - top = current task / current context reference area
  - middle = one dominant 4-layer anatomy stack
  - side = lifecycle and retrieval legend
  - lower area = one warning comparison showing what happens when all layers are mixed together
  - the page should read like:
    - 当前任务离哪层最近
    - 每层分别存什么
    - 每层怎么参与运行
    - 如果不分层会发生什么

- Current task reference area:
  - place one compact header object above the layer stack
  - label:
    - 当前任务
    - current context window
  - inside it show 4 tiny tags:
    - 最近消息
    - 当前目标
    - 当前状态
    - 下一步动作
  - mini annotation:
    - "模型真正直接工作的，是眼前这块工作面"
  - this box should visually anchor the whole page and clarify what "near" means

- Main 4-layer anatomy stack:
  - place one dominant vertical layer structure in the center
  - use 4 large stacked bands or cards from top to bottom:
    - Working Set
    - Episodic Memory
    - Semantic Memory
    - Procedural Memory
  - add one small vertical side label on the left:
    - 近
    - 到
    - 远
  - add one small vertical side label on the right:
    - 运行时距离

- Layer 1 - Working Set
  - this should be the top layer, closest to the current context box
  - Chinese descriptor:
    - 当前工作面
  - 3 compact sub-slots inside the band:
    - 存什么：最近消息 / 当前目标 / 临时状态
    - 什么时候用：每一轮都在用
    - 不该存什么：长期档案 / 大量历史 / 过期中间结果
  - visual cue:
    - active notes, highlighted cards, live workspace feeling
  - one tiny lifecycle tag:
    - 短期

- Layer 2 - Episodic Memory
  - second band below Working Set
  - Chinese descriptor:
    - 历史事件与回放
  - 3 compact sub-slots inside the band:
    - 存什么：工具调用 / 失败案例 / 历史结论
    - 什么时候用：需要回看前情时
    - 不该存什么：稳定偏好 / 抽象规则
  - visual cue:
    - searchable event trails, timestamped records, case history cards
  - one tiny lifecycle tag:
    - 中期

- Layer 3 - Semantic Memory
  - third band below Episodic Memory
  - Chinese descriptor:
    - 稳定事实与偏好
  - 3 compact sub-slots inside the band:
    - 存什么：用户偏好 / 项目约束 / 稳定事实
    - 什么时候用：需要稳定约束时
    - 不该存什么：临时状态 / 一次性尝试
  - visual cue:
    - compact curated fact cards, stable keys, preference sheet
  - one tiny lifecycle tag:
    - 长期

- Layer 4 - Procedural Memory
  - bottom band
  - Chinese descriptor:
    - 技能与可复用流程
  - 3 compact sub-slots inside the band:
    - 存什么：技能 / 流程 / 最佳实践
    - 什么时候用：类似任务再次出现时
    - 不该存什么：未经验证的即兴做法
  - visual cue:
    - reusable playbooks, skill cards, validated routines
  - one tiny lifecycle tag:
    - 可复用

- Side legend - lifecycle and retrieval mode:
  - place one compact side panel on the right side of the layer stack
  - split it into two mini columns:
    - 生命周期
    - 参与方式
  - align each row to one layer:
    - Working Set -> 短期 / 直接工作
    - Episodic -> 中期 / 按需回看
    - Semantic -> 长期 / 稳定注入
    - Procedural -> 可复用 / 类似任务触发
  - this side panel should make the engineering distinction explicit without cluttering the main stack

- Warning comparison zone:
  - place one compact orange comparison block near the lower area
  - title:
    - 不分层会怎样
  - show one "混在一起的上下文团块" visual:
    - 最近消息
    - 历史日志
    - 用户偏好
    - 技能流程
    - 全部挤成一锅
  - add one blunt note:
    - "把所有信息塞进同一层，最后得到的不是记忆系统，而是一锅越来越脏的上下文"
  - this area should feel like a concrete anti-pattern, not an abstract warning

- Structural emphasis:
  - the middle 4-layer stack should be the unquestioned hero object of the page
  - the current context box at the top exists to define distance, not to become another full panel
  - the page should clearly express runtime separation, not process steps
  - prioritize layer readability over decorative symmetry

- Connection semantics (important):
  - this page is mainly about layered role separation, not about execution sequence
  - do NOT connect the four memory layers with strong downward arrows as if they were a four-step pipeline
  - vertical stacking means:
    - distance to current task
    - difference in lifecycle
    - difference in runtime role
    - not chronological flow
  - the only strong direct connection may exist between Working Set and the current context box, because that layer is the closest active work surface
  - Episodic, Semantic, and Procedural Memory may have light upward influence lines toward the current context area
  - those light lines mean:
    - "按需参与当前任务"
    - not "先经过 Episodic 再经过 Semantic 再经过 Procedural"
  - do NOT connect Episodic -> Semantic -> Procedural with arrows, because that falsely implies one layer transforms into the next in a fixed path
  - use dividers, proximity, and aligned legends to express hierarchy
  - use light recall markers or small upward cues to express possible retrieval
  - line meaning on this page should be strict:
    - stacked adjacency = runtime distance
    - divider line = layer boundary
    - light upward cue = possible recall / influence
    - strong arrow = only for direct active working relation

**Bottom Section (Interpretation Area - 14%):**

- Keep the bottom area compact
- Add one short conclusion sentence centered at the bottom:
  "记忆分层的意义，不是学术命名，而是让不同信息进入正确的生命周期"
- Add a small footer label:
  "Agent记忆系统怎么实现 / 03"

**What Must Be Clear in the Diagram:**

- This page is about layered runtime roles, not process flow
- The viewer must understand that the four layers are separated by function and lifecycle
- "Near to current context" is a key organizing principle
- Working Set is not just another storage bucket; it is the active working surface
- The warning zone must make visible why non-layered memory becomes dirty and unusable
- Connector logic must stay accurate:
  - no fake pipeline arrows between the four layers
  - no implied transformation chain from one layer into another
  - only direct or light influence relations where they really make sense

**Visual Elements That Should Appear:**

- One current task / current context reference box
- One dominant 4-layer vertical anatomy stack
- One side legend for lifecycle and participation mode
- One warning comparison block
- Minimal but precise guide lines
- Footer label

**Visual Elements That Must NOT Appear:**

- Long horizontal four-step flowchart
- One giant bidirectional arrow linking all layers
- Brain illustration
- Knowledge tree metaphor
- Giant database cylinder
- Radial memory wheel
- Arrows that imply Working Set flows into Episodic into Semantic into Procedural

**Suitable Diagram Types to Combine:**

- Technical anatomy board
- Vertical layer stack
- Runtime-distance legend
- Lifecycle classification panel
- Warning comparison block

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Professional engineering documentation style
- White background with editorial clarity
- Portrait-first composition optimized for 3:4 canvas
- Strong top-to-bottom visual logic
- Dense but clean information hierarchy
- 52% layered diagram, 18% labels and callouts, 30% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, titles, frames, and layer boundaries
- Bright blue (#3498DB) for direct working relations and light recall cues
- Green (#16A085) for stable and reusable memory layers, especially Semantic and Procedural
- Orange (#E67E22) for the warning comparison block and "混在一起" anti-pattern emphasis
- Light gray for helper grids, dividers, and side legend scaffolding
- Pure white background

**Typography:**

- All major annotations in simplified Chinese
- Keep only these technical terms in English where appropriate: Working Set, Episodic Memory, Semantic Memory, Procedural Memory, current context
- Title font should be bold and larger than standard social infographic text
- Secondary labels should be compact but clearly readable on mobile

**Overall Feel:**

- Clean and explanatory
- More like a runtime anatomy dossier than a concept poster
- Makes the four-layer architecture easy to remember at a glance
- Clearly communicates that the real question is "which information belongs to which layer"
- Visually stable and accurate enough that connection mistakes are hard to make
- Suitable for Xiaohongshu-style technical carousel third slide

Style: Detailed technical hand-drawn runtime anatomy infographic, portrait-oriented 4-layer memory stack, current-context reference box, lifecycle side legend, warning comparison block, pure white background
