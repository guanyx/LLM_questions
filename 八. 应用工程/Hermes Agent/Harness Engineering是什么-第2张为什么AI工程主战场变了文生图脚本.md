# Harness Engineering 是什么：第 2 张“为什么 AI 工程主战场变了”文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "模型越来越强，为什么工程反而更重要了". The image should make it immediately clear that AI engineering has shifted from a "single-turn answer paradigm" to a "system-completion paradigm". This should be a balanced comparison board, not a sparse-left / crowded-right pipeline poster.

**Design Concept:**

Use a "双面任务板 / paradigm shift dossier" metaphor. The left side should not be empty; it should be a fully explained "单轮回答范式" board with its own assumptions, structure, and evaluation criteria. The right side should be a fully explained "系统完成范式" board, but instead of listing every Harness module separately, compress the modern reality into a few grouped stages so the composition stays balanced. The center should be a narrow pivot lane showing why the shift happened: tasks got longer, side effects appeared, and system reliability started to matter more than answer elegance.

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "模型越来越强，为什么工程反而更重要了"
- Subtitle below: "瓶颈已经从“会不会回答”，变成“能不能完成任务”"
- Small supporting sentence:
  "AI 工程的新难点，不再只是让模型说得像样，而是让系统把一条真实任务稳定跑完"
- Typography should feel like a technical editorial spread, not a marketing slide

**Central Section (Hero Diagram - 58%):**

Create a balanced left-to-right comparison board with three vertical regions:

- left dossier panel = 旧世界 / 单轮回答范式
- center pivot lane = 范式切换原因
- right dossier panel = 新世界 / 系统完成范式

Both dossier panels should have similar visual weight and similar internal density.

- Left zone - 旧世界 / model output world:
  - build this as a complete technical board with 4 stacked sub-areas, not just a tiny 3-node pipeline
  - Sub-area 1 - 输入区:
    - one small chat/request card:
      - "这个报错是什么意思？"
    - label:
      - 单轮问题
      - no external state
  - Sub-area 2 - 核心结构:
    - a compact straight pipeline:
      - question
      - model
      - answer
    - show only one forward arrow, no loops
    - add one tiny side annotation:
      - "核心是生成回答"
  - Sub-area 3 - 默认假设:
    - place 4 small assumption tags in a 2x2 grid:
      - 无工具调用
      - 无长期状态
      - 无副作用
      - 无交付责任
  - Sub-area 4 - 评判标准:
    - place one small scorecard panel:
      - 回答像不像
      - 语言顺不顺
      - 解释清不清
      - 速度快不快
    - main note:
      - "主要关注：回答质量"
  - add one bottom judgment note:
    - "这更像一次输出，不像一次完整工作"

- Center transition zone:
  - keep this region narrow but information-rich
  - add one vertical pivot arrow or turning gate:
    - from answer quality
    - to task completion
  - around the pivot, place 4 compact shift cards:
    - 任务链变长
    - 外部工具接入
    - 状态开始累积
    - 副作用必须控制
  - add one small note near the center:
    - "问题没有变少，系统责任变重了"
  - this center lane should feel like a turning hinge between two eras

- Right zone - 新世界 / system completion world:
  - also build this as a complete technical board with 4 stacked sub-areas, mirroring the left panel's density
  - use one concrete task card at the top:
    - "修复测试失败并提交结论"
  - Sub-area 1 - 输入区:
    - request card with tiny attached requirements:
      - 要找文件
      - 要调工具
      - 要检查结果
      - 要安全交付
  - Sub-area 2 - 核心结构:
    - do NOT draw seven tiny cards in a row
    - instead compress the new world into 4 grouped stages:
      - 任务理解
      - 外部操作
      - 中间校验
      - 结果交付
    - inside each grouped stage, place tiny internal cues:
      - 任务理解: context / constraints
      - 外部操作: tools / workflow
      - 中间校验: memory / check
      - 结果交付: delivery / status
    - connect the 4 grouped stages with strong arrows and one small feedback loop from 中间校验 back to 外部操作
  - Sub-area 3 - 系统责任:
    - place 4 responsibility tags in a 2x2 grid:
      - 要控边界
      - 要留状态
      - 要能回看
      - 要能恢复
  - Sub-area 4 - 评判标准:
    - place one structured delivery scorecard:
      - 跑没跑完
      - 是否可复现
      - 是否越界
      - 是否可交付
    - main note:
      - "主要关注：系统完成度"
  - final output card should look like a delivery packet, not a plain answer bubble:
    - 任务完成
    - 改动结果
    - 风险说明
    - 下一步状态

- Harness emphasis layer:
  - above or around the right dossier panel, add one outer bracket or engineering frame labeled:
    - "Harness"
  - this bracket should visually show that the new-world panel is held together by the surrounding engineering system
  - small tags on the bracket:
    - control
    - routing
    - boundary
    - observability
    - recovery

- Contrast emphasis:
  - the left side should feel complete but narrower in responsibility
  - the right side should feel equally balanced in layout, but broader in system responsibility
  - the viewer must immediately feel:
    - left = 用模型回答
    - right = 用系统完成

**Bottom Section (Interpretation Strip - 22%):**

Create a horizontal interpretation strip with 3 stages:

1. "旧瓶颈"
   - tiny explanation: "模型会不会答"
2. "范式切换"
   - tiny explanation: "从输出走向完成"
3. "新主战场"
   - tiny explanation: "系统能不能跑完任务"

- Connect the three stages with arrows
- Add one bottom conclusion sentence:
  "Harness Engineering 之所以重要，是因为今天要竞争的，已经不是回答本身，而是系统完成度"
- Add footer label:
  "Harness Engineering / 02"

**What Must Be Clear in the Diagram:**

- Left side is intentionally simpler than right side
- But it must not be visually empty
- The contrast is not "old model weak vs new model strong"
- The real contrast is:
  - old focus = answer quality
  - new focus = task completion quality
- The right side must clearly show that modern AI work includes grouped engineering responsibility layers
- Harness must appear as the thing that makes the right-side chain stable and runnable

**Suitable Diagram Types to Combine:**

- Before/after comparison infographic
- Two balanced paradigm dossier panels
- Paradigm-shift pivot lane
- Single-turn answer board
- Grouped system-completion board
- Outer harness bracket / control frame
- Bottom interpretation timeline

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Professional engineering documentation style
- White background with editorial comparison clarity
- Strong left-to-right reading flow
- Dense but easy-to-scan information hierarchy
- Composition ratio:
  - 50% detailed diagram illustration
  - 20% labels and callouts
  - 30% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, titles, and main frames
- Bright blue (#3498DB) for arrows, system chain flow, and the paradigm-shift pivot
- Teal (#16A085) for stable delivery, completed system behavior, and Harness bracket highlights
- Orange (#E67E22) for friction, complexity growth, and shift emphasis near the center transition
- Light gray for construction lines and secondary annotations
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep only these technical terms in English where appropriate: model, answer, request, context, tools, workflow, memory, check, delivery, Harness
- Title should be bold and larger than standard Xiaohongshu cover text
- Secondary labels should be small but clearly readable on mobile

**Overall Feel:**

- Clean and intellectually sharp
- Visually makes a big conceptual shift obvious at a glance
- More like a technical editorial comparison board than a product poster
- Immediately communicates that "AI 工程的难点已经从回答升级成系统完成任务"
- Balanced enough that both panels carry information, instead of one side being empty and the other side overloaded
- Suitable for Xiaohongshu-style knowledge carousel second slide

Style: Detailed technical hand-drawn comparison infographic, balanced dual dossier panels, single-turn answer paradigm vs system-completion paradigm, paradigm-shift pivot lane, Harness as outer engineering frame, pure white background
