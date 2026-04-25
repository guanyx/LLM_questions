# Agent记忆系统怎么实现：第 6 张“记忆不是单库问题，而是存储分工问题”图文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "记忆不是单库问题，而是存储分工问题". The image should make it immediately clear that a production-grade memory system should not be imagined as one all-powerful database. Instead, different storage types are responsible for different objects, query styles, and engineering roles. This page must feel like a storage-responsibility board, not a runtime pipeline.

**Design Concept:**

Use a "storage responsibility split board" metaphor. Because the target canvas is 3:4 portrait ratio, do NOT turn this page into a central pipeline where all storage systems are linked in a sequence. Instead, build a portrait-oriented classification board: one upper framing statement, a balanced field of storage cards in the middle, and one lower warning strip showing the common mistake of treating vector DB as the whole memory system. The key message is: the right question is not "which database should I use?" but "which memory object belongs to which storage role?"

**Layout Structure:**

**Top Section (Title Area - 18%):**

- Main title in bold, large font: "记忆不是单库问题，而是存储分工问题"
- Subtitle below: "文件系统、关系库、向量索引、图存储、技能库，各自负责不同对象"
- Small supporting sentence:
  "没有一种存储能优雅承接所有记忆，真正成熟的设计是按对象和查询方式拆分职责"
- Typography should feel like a technical system-ownership page, not a vendor comparison poster

**Central Section (Hero Diagram - 68%):**

Create a portrait-oriented storage-responsibility board with one framing header and a balanced set of storage cards.

- Overall composition:
  - upper area = one framing board with the key judgment
  - middle area = five storage cards arranged in a balanced portrait layout
  - lower area = one warning strip plus one small object-to-storage mapping reminder
  - do NOT force a sequential left-to-right architecture flow
  - the page should read like:
    - 先看记忆对象
    - 再看查询方式
    - 最后决定存储职责

- Framing board:
  - place one medium-width framing board below the title
  - label:
    - Storage Split
    - 先分对象，再分库
  - inside it show 3 compact framing prompts:
    - 存的是什么对象？
    - 以后怎么查它？
    - 它最怕什么误用？
  - add one small side note:
    - "选库是职责映射，不是信仰表态"
  - this board should set the logic for the storage cards below, not dominate the page

- Storage card field:
  - place 5 storage cards in a portrait-friendly balanced layout
  - recommended arrangement:
    - top row: filesystem, relational DB
    - middle row: vector index, graph store
    - bottom center: skills library
  - alternative acceptable layout:
    - 2 + 2 + 1 dossier-card arrangement
  - all five cards should have similar visual weight

- Card 1 - filesystem
  - title:
    - filesystem
    - 文件系统
  - 3 fixed sub-lines:
    - 适合存什么：notes / snapshots / readable memory files
    - 优势：透明、可审计、适合工作区协同
    - 不适合做什么：复杂过滤、大规模语义召回
  - add one mini visual cue:
    - note files / snapshot cards / workspace docs

- Card 2 - relational DB
  - title:
    - relational DB
    - 关系型数据库
  - 3 fixed sub-lines:
    - 适合存什么：events / metadata / version / confidence
    - 优势：过滤强、事务强、适合做系统主账本
    - 不适合做什么：单独承担模糊语义召回
  - add one mini visual cue:
    - rows, schemas, timestamp fields, structured event log

- Card 3 - vector index
  - title:
    - vector index
    - 向量索引
  - 3 fixed sub-lines:
    - 适合存什么：semantic recall / approximate match / long-text retrieval
    - 优势：模糊语义召回强
    - 不适合做什么：时序判断、冲突更新、完整记忆治理
  - add one mini visual cue:
    - similarity cloud / semantic neighbors / retrieval ranking dots

- Card 4 - graph store
  - title:
    - graph store
    - 图存储
  - 3 fixed sub-lines:
    - 适合存什么：relations / evolving facts / constraints
    - 优势：关系可解释、适合复杂实体约束
    - 不适合做什么：所有场景一上来就全图化
  - add one mini visual cue:
    - nodes, edges, temporal relationship paths

- Card 5 - skills library
  - title:
    - skills library
    - 技能库
  - 3 fixed sub-lines:
    - 适合存什么：reusable procedures / validated playbooks
    - 优势：把经验变成可复用流程
    - 不适合做什么：保存原始事件或用户偏好
  - add one mini visual cue:
    - skill cards / procedural docs / reusable playbooks

- Object-to-storage mapping reminder:
  - place one small mapping strip near the lower-middle area
  - label:
    - 对象先行
  - show 5 quick pairings:
    - 工作笔记 -> filesystem
    - 结构化事件 -> relational DB
    - 语义召回 -> vector index
    - 实体关系 -> graph store
    - 可复用流程 -> skills library
  - this strip should make the page feel implementation-oriented rather than just descriptive

- Warning strip:
  - place one orange warning strip near the bottom
  - title:
    - 最常见误区
  - include one large blunt statement:
    - vector DB != full memory system
  - add 2 compact supporting warnings:
    - "把所有记忆都丢给向量库，最后只会得到召回层，不会得到完整治理层"
    - "存储强项不同，乱混职责会让系统越来越难维护"
  - this strip should be visually sharp and unmistakable

- Structural emphasis:
  - all five storage cards should be treated as peer responsibility units, not as stages in a chain
  - this page should feel like a classification and ownership map
  - the lower mapping strip should turn the page from "知识介绍" into "落地分工建议"
  - the warning strip should be visible but not dominate the storage field

- Connection semantics (important):
  - this page is about responsibility split, not runtime sequence
  - do NOT connect filesystem -> relational DB -> vector index -> graph store -> skills library with arrows
  - do NOT imply that one storage layer automatically feeds the next as a fixed pipeline
  - the five storage cards are parallel storage roles, not ordered processing stages
  - if connector lines are used, they should be light and express:
    - grouping
    - comparison
    - object-to-storage mapping
  - the framing board may connect lightly downward into the storage card field as a setup relation
  - the object-to-storage mapping strip may connect upward to relevant cards with light guide lines or brackets
  - those lines mean:
    - "this object type is best matched with this storage role"
    - not "this data flows through every storage card"
  - the warning strip should stay visually separated
  - do NOT draw arrows from the warning strip into the storage cards
  - line meaning on this page should be strict:
    - light guide line = mapping / classification relation
    - bracket or frame = grouping relation
    - strong arrow = avoid unless absolutely necessary

**Bottom Section (Interpretation Area - 14%):**

- Keep the bottom area compact
- Add one short conclusion sentence centered at the bottom:
  "好的记忆架构不是单点最强，而是每种存储只做自己最擅长的事"
- Add a small footer label:
  "Agent记忆系统怎么实现 / 06"

**What Must Be Clear in the Diagram:**

- There is no single storage that elegantly handles all memory roles
- Storage choice must follow object type and query style
- Vector index is only one role inside a larger memory system
- The page is about division of responsibility, not dataflow order
- Connector logic must stay accurate:
  - no fake sequential arrows across the five storages
  - no implied full-stack database tower
  - only mapping and grouping relations where necessary

**Visual Elements That Should Appear:**

- One framing board
- Five balanced storage cards
- One object-to-storage mapping strip
- One warning strip
- Light guide lines or brackets only where needed
- Footer label

**Visual Elements That Must NOT Appear:**

- One central giant database hero object
- Storage cards connected as a full pipeline
- Vendor logo comparison
- Full runtime architecture flow
- Brain illustration
- One layered tower that implies "higher" vs "lower" database superiority
- Arrows that suggest every memory object moves through all five storages

**Suitable Diagram Types to Combine:**

- Technical responsibility board
- 2+2+1 storage card layout
- Mapping strip
- Warning strip
- Comparison-oriented guide lines

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Professional engineering documentation style
- White background with editorial clarity
- Portrait-first composition optimized for 3:4 canvas
- Balanced classification layout, not process flow
- Dense but controlled information hierarchy
- 52% diagram illustration, 18% labels and callouts, 30% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, titles, storage frames, and main labels
- Bright blue (#3498DB) for mapping lines, grouping emphasis, and classification structure
- Green (#16A085) for well-matched storage-role pairings and healthy division-of-responsibility cues
- Orange (#E67E22) for the warning strip and misuse emphasis
- Light gray for helper dividers, card scaffolding, and secondary notes
- Pure white background

**Typography:**

- All major annotations in simplified Chinese
- Keep only these technical terms in English where appropriate: filesystem, relational DB, vector index, graph store, skills library, Storage Split
- Title font should be bold and larger than standard social infographic text
- Secondary labels should be compact but clearly readable on mobile

**Overall Feel:**

- Clean and explanatory
- More like a storage-ownership dossier than a concept poster
- Makes storage division of labor obvious at a glance
- Clearly communicates that asking "which database?" is the wrong first question
- Visually strict enough that connection mistakes are hard to introduce
- Suitable for Xiaohongshu-style technical carousel sixth slide

Style: Detailed technical hand-drawn storage-responsibility infographic, portrait-oriented balanced storage-card board, object-to-storage mapping strip, warning strip, pure white background
