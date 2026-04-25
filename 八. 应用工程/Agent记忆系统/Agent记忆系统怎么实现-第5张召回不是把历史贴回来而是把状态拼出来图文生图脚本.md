# Agent记忆系统怎么实现：第 5 张“召回不是把历史贴回来，而是把状态拼出来”图文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "召回不是把历史贴回来，而是把状态拼出来". The image should make it immediately clear what an engineer should do when a new task arrives: first judge whether memory is even needed, then decide which memory layer to query, then filter and rerank candidate recall, and finally assemble only a small actionable state packet for the current context window. This page must feel like an operational recall-policy board, not a generic retrieval concept page.

**Design Concept:**

Use a "recall-decision operating board" metaphor. Because the target canvas is 3:4 portrait ratio, do NOT make this page a long retrieval pipeline with every step stretched across one row. Instead, build a portrait-oriented decision board where the task card sits at the top, the key judgment point sits in the center, the candidate recall pools sit in the middle-lower area, and the final context pack sits near the bottom as the refined output. The key message is: good recall is selective assembly, not bulk retrieval.

**Layout Structure:**

**Top Section (Title Area - 18%):**

- Main title in bold, large font: "召回不是把历史贴回来，而是把状态拼出来"
- Subtitle below: "判断搜不搜、搜哪层、怎么重排，比把内容召回来更重要"
- Small supporting sentence:
  "召回真正要解决的，不是“找回更多历史”，而是“只让当前任务拿到最需要的那一小部分状态”"
- Typography should feel like a technical decision board, not a search-engine marketing slide

**Central Section (Hero Diagram - 68%):**

Create a portrait-oriented recall-policy board with one strong top-to-bottom decision structure.

- Overall composition:
  - upper area = incoming task cards
  - center = one dominant recall-judgment board
  - middle-lower = candidate recall pools
  - lower-middle = rerank and filtering layer
  - bottom = final context pack
  - side = one orange anti-pattern warning area
  - the page should read like:
    - 先看任务
    - 再判要不要调记忆
    - 再判该搜哪层
    - 再把候选项过滤
    - 最后拼成当前可行动状态

- Incoming task area:
  - place 3 compact task cards across the upper area
  - suggested cards:
    - "继续那个部署问题"
    - "按我平时风格写"
    - "像上次那样排查"
  - these task cards should visually show that different tasks trigger different memory needs
  - add one small label above them:
    - incoming task
    - 当前任务来了
  - mini annotation:
    - "不是每轮都该搜历史"

- Central recall-judgment board:
  - place one large central object labeled:
    - recall policy
    - 这轮到底该召回什么？
  - inside the board, show 3 practical questions:
    - 要不要搜历史？
    - 该搜哪一层？
    - 需要多少就够了？
  - add one small second-row prompt group:
    - need episodic?
    - need semantic?
    - need procedural?
  - this board must be the hero object of the page
  - add one mini annotation:
    - "先判断，再召回"

- Candidate recall pools:
  - below the central board, split into 3 practical candidate pools
  - pool A:
    - Episodic candidates
    - 历史事件候选
  - pool B:
    - Semantic candidates
    - 稳定事实候选
  - pool C:
    - Procedural candidates
    - 流程技能候选
  - each pool should have compact examples:
    - Episodic:
      - 上次部署失败原因
      - 某次工具调用轨迹
      - 某次问题最终结论
    - Semantic:
      - 用户偏好直截了当
      - 项目使用 pnpm
      - 回答必须中文
    - Procedural:
      - 排障顺序
      - 工具调用套路
      - 已验证工作流
  - these candidate pools should feel like possible sources, not guaranteed final inputs

- Filtering and rerank layer:
  - place one structured layer below the candidate pools
  - title:
    - rerank / filtering
    - 不是召回来就能用
  - show 4 compact criteria cards:
    - relevance
    - freshness
    - credibility
    - environment match
  - add one practical annotation:
    - "最像的不一定最该进当前上下文"
  - this layer should visually feel like a compression-and-selection checkpoint

- Final context pack:
  - place one compact but visually important output board near the bottom-center
  - title:
    - context pack
    - 当前可行动状态
  - show 4 tiny structured slots inside:
    - 2-3 条关键事件
    - 稳定事实
    - 1 条已验证流程
    - 下一步状态摘要
  - add one mini annotation:
    - "召回的终点不是原文，而是当前任务能直接用的状态"
  - this box should feel distilled, small, and clean compared with the noisy candidate pools above

- Orange anti-pattern zone:
  - place one orange caution block on one side of the lower area
  - title:
    - 千万别这么召回
  - include 3 concrete anti-pattern cards:
    - 全量 history 直接塞进 prompt
    - 只按向量相似度 Top-K
    - 原文整段贴入，不做状态整理
  - add one blunt note:
    - "召回越多不一定越好，噪音常常比缺信息更先毁掉结果"
  - this block should feel like practical failure cases, not generic principles

- Small cost and noise note:
  - add one small side note near the rerank layer:
    - cost / noise tradeoff
    - "每多召回一段历史，都在增加成本、延迟和注意力污染风险"
  - this note should reinforce that selective recall is an engineering constraint, not just a style preference

- Structural emphasis:
  - the recall-policy board must be the hero object of the page
  - the candidate pools should feel broad and messy compared with the final compact context pack
  - the rerank/filtering layer should visibly act like a narrowing funnel
  - the anti-pattern zone should be operational and concrete

- Connection semantics (important):
  - this page is a practical recall-decision board, so the main path is causal and directional
  - the main path should be:
    - incoming task -> recall policy -> candidate pools -> rerank/filtering -> context pack
  - that main path should use strong arrows
  - the split from recall policy into Episodic / Semantic / Procedural candidate pools is a branching choice
  - those branches mean:
    - "this task may need one or more of these layers"
    - not "all three must always be recalled"
  - do NOT connect Episodic -> Semantic -> Procedural with arrows
  - do NOT imply that the candidate pools are sequential stages
  - the rerank/filtering layer should collect from the candidate pools downward into a smaller final pack
  - those collecting lines mean:
    - "many candidates shrink into a smaller usable set"
  - the anti-pattern block must stay off the main path
  - connect the anti-pattern zone only with dashed warning markers or local caution callouts
  - line meaning on this page should be strict:
    - strong arrow = recall decision flow
    - branch arrow = layer-selection choice
    - converging line = candidate narrowing
    - dashed warning line = anti-pattern / risk reminder
    - grouped box = same operational category

**Bottom Section (Interpretation Area - 14%):**

- Keep the bottom area compact
- Add one short conclusion sentence centered at the bottom:
  "召回的终点不是文档，而是让模型立刻能用的状态"
- Add a small footer label:
  "Agent记忆系统怎么实现 / 05"

**What Must Be Clear in the Diagram:**

- Not every task should trigger memory recall
- The first recall question is "which layer is needed", not "how much can I stuff back"
- Candidate recall is broad, but final context pack must be narrow
- Rerank/filtering is where noisy recall becomes usable state
- The anti-patterns are caused by bad recall policy, not by missing bigger context windows
- Connector logic must stay accurate:
  - main path arrows are decision flow
  - candidate pools are branching choices, not sequence
  - converging lines mean narrowing, not averaging

**Visual Elements That Should Appear:**

- Incoming task cards
- One dominant recall-policy board
- Three candidate recall pools
- One rerank/filtering layer
- One final context-pack board
- One anti-pattern warning block
- One cost/noise note
- Precise directional arrows
- Footer label

**Visual Elements That Must NOT Appear:**

- One giant retrieval box doing everything
- Arrows that make the three candidate pools look sequential
- A giant search bar UI as the main visual metaphor
- Full agent runtime architecture
- Brain illustration
- Vector database hero object
- A final context pack bigger than the candidate pools

**Suitable Diagram Types to Combine:**

- Technical recall-policy board
- Branch selection schematic
- Candidate-pool layout
- Rerank narrowing layer
- Compact context-pack output board
- Anti-pattern warning block

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Professional engineering documentation style
- White background with editorial clarity
- Portrait-first composition optimized for 3:4 canvas
- Strong decision reading flow from top to bottom
- Dense but controlled information hierarchy
- 54% diagram illustration, 18% labels and callouts, 28% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, titles, main frames, and candidate-pool cards
- Bright blue (#3498DB) for the main recall path, branching structure, and filtering convergence
- Green (#16A085) for the final context pack and correct selective-recall outcomes
- Orange (#E67E22) for the anti-pattern block, noise overload risk, and caution accents
- Light gray for helper dividers, secondary notes, and non-primary scaffolding
- Pure white background

**Typography:**

- All major annotations in simplified Chinese
- Keep only these technical terms in English where appropriate: recall policy, Episodic, Semantic, Procedural, rerank, filtering, context pack
- Title font should be bold and larger than standard social infographic text
- Secondary labels should be compact but clearly readable on mobile

**Overall Feel:**

- Clean and operational
- More like an implementation cheat sheet than a concept poster
- Makes the recall-decision problem obvious at a glance
- Clearly communicates what to query, what to filter, and what to finally hand back to the model
- Visually strict enough that wrong arrow semantics are hard to introduce
- Suitable for Xiaohongshu-style technical carousel fifth slide

Style: Detailed technical hand-drawn recall-policy infographic, portrait-oriented decision board, candidate recall pools, rerank narrowing layer, compact context-pack output board, anti-pattern warning block, pure white background
