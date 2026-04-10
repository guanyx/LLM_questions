# Hermes Agent对象拆解：第 8 张Memory 与 Session文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "Hermes 怎么记住你，又不把上下文撑爆？".

**Design Concept:**
Use a concrete memory write-and-recall journey metaphor instead of a broad layered architecture diagram: the image should show one conversation gradually产生信息，其中一部分被写成长期记忆，一部分进入会话仓库，之后在新任务里按需被搜索召回，同时上下文压缩控制长度。 The visual emphasis should be on one complete记忆旅程，而不是只展示静态层次。

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "Hermes 怎么记住你，又不把上下文撑爆？"
- Subtitle below: "真正的记忆系统，不是全记住，而是在正确的时候想起正确的事"
- Small supporting sentence: "Hermes 把长期记忆、会话检索、上下文压缩拆成不同层，而不是把所有历史都硬塞进 prompt"
- Typography should feel like a technical systems poster, not a sentimental memory metaphor poster

**Central Section (Hero Diagram - 55%):**
Create a left-to-right concrete memory journey diagram with one “写入” and one “召回”:

- Build one main horizontal story across the middle:
  - 当前会话产生信息
  - 分流写入不同记忆位置
  - 新任务发起
  - 按需搜索召回
  - 上下文压缩后进入当前窗口

- Stage 1 - 当前会话
  - place one conversation strip on the far left
  - show 3 tiny example message fragments:
    - "用户偏好是中文回答"
    - "项目用 pnpm"
    - "刚讨论过部署问题"
  - annotation: "会话里产生的信息不全都要直接塞进下一轮 prompt"

- Stage 2 - 写入分流
  - place one decision/split box after 当前会话
  - split into two downward / sideward write paths:
    - 写入 Persistent Memory
    - 写入 Session Search
  - make it visually clear that不同类型的信息进入不同记忆层

- Stage 3A - Persistent Memory
  - place one compact curated memory box
  - label: "Persistent Memory"
  - include 3 cards:
    - 环境事实
    - 用户偏好
    - 项目约定
  - add tiny file cues:
    - MEMORY.md
    - USER.md
  - annotation: "小而精、稳定、长期存在"

- Stage 3B - Session Search
  - place one larger searchable archive box
  - label: "Session Search"
  - visual cue: SQLite cylinder + search lens
  - internal labels:
    - 历史对话仓库
    - FTS5 搜索
    - 过去讨论召回
  - annotation: "大而全，需要时再找回来"

- Stage 4 - 新任务进入
  - on the right side place one new task card
  - tiny example:
    - "再次处理类似部署问题"
  - this task should connect upward into a search/retrieval box

- Stage 5 - 按需召回
  - place one retrieval box between 新任务 and Session Search / Persistent Memory
  - label:
    - 稳定注入
    - 条件召回
  - connect Persistent Memory → retrieval box with a stable arrow
  - connect Session Search → retrieval box with a search arrow
  - add note:
    - "不是全量加载，而是按需取用"

- Stage 6 - Context Compression
  - after the retrieval box place one compression-control box
  - show one long conversation ribbon entering, then mid-section folding, while the latest messages remain visible
  - internal labels:
    - 压缩中段
    - 保留最近消息
    - 控制上下文长度
  - annotation: "不是删光历史，而是折叠中段，保住近端工作面"

- Stage 7 - 当前上下文窗口
  - place one final box on the far right labeled "当前上下文窗口"
  - show that only the selected and compressed subset enters here

- Add one green design-strength callout:
  - label: "设计亮点"
  - annotation: "长期记忆、会话检索、上下文压缩分层协作，既能记住关键事实，又不把 prompt 撑爆"

- Add one orange design-tradeoff callout:
  - label: "设计代价"
  - annotation: "记忆分散在文件、数据库、压缩摘要、外部 provider 之间，统一心智模型并不简单"

- Add one smaller caution note:
  - label: "FTS5 很实用，但不是完整语义记忆"
  - annotation: "压缩摘要也天然会丢细节"

- Add one bold judgment note below the main path:
  - "记忆不是全存全取，而是先分流写入，再按需召回"

**Bottom Section (Interpretation Strip - 25%):**

- Create a horizontal 3-step interpretation strip:
  1. 不是全量塞进 prompt
  2. 是分层记忆系统
  3. 在需要时想起正确的事
- Under each step add one compact explanation:
  - 不是全量塞进 prompt："否则上下文很快爆掉"
  - 是分层记忆系统："Persistent Memory / Session Search / Compression"
  - 在需要时想起正确的事："稳定注入、按需召回、长度控制三套机制协同"
- Add one conclusion sentence centered at bottom:
  "Hermes 的记忆系统强在工程实用：分层、可控、可检索，而不是幻想一个无穷大的万能记忆体"
- Add footer label:
  "Hermes Agent 对象拆解 / 08"

**What Must Be Clear in the Diagram:**

- Memory is not one single storage block
- One conversation should visibly split into persistent memory and searchable session history
- Compression is part of memory architecture, not just a cleanup step
- The current context window only receives the right subset at the right time
- The image must visually communicate this judgment:
  "Hermes 的记忆不是全存全取，而是先分流写入，再按需召回"

**Suitable Diagram Types to Combine:**

- Concrete memory write-and-recall journey
- Split-write decision box
- Search-and-recall schematic
- Compression-control box
- Current-context window box
- Strength/tradeoff callouts
- Bottom interpretation timeline

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Pure white background
- Strong left-to-right story flow with readable information hierarchy
- Dense callouts, but visually calm and systematic
- Should feel like a concrete memory-control workflow, not like a database ad
- Composition ratio:
  - 50% detailed schematic illustration
  - 25% text labels and technical callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, labels, and architectural frames
- Bright blue (#3498DB) for recall and routing arrows
- Green (#16A085) for persistent memory and stable facts
- Orange (#E67E22) for compression pressure and design tradeoffs
- Light gray for helper lines, storage textures, and secondary annotations
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep technical terms in English where appropriate: Persistent Memory, Session Search, Context Compression, SQLite, FTS5, MEMORY.md, USER.md
- Title should be bold and visually strong
- Layer labels should be crisp and mobile-readable

**Overall Feel:**

- Concrete and practical
- Makes memory feel like a controllable write-and-recall workflow, not a vague ability
- Emphasizes selective recall and context discipline
- Easy to understand at a glance, with enough detail for technical readers
- Suitable for Xiaohongshu-style technical carousel

Style: Detailed technical hand-drawn infographic, concrete memory write-and-recall journey, persistent-memory plus session-search plus compression workflow, pure white background
