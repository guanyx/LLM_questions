# 微调的数据准备：图 1 Prompt

Create a highly detailed vertical technical infographic in refined hand-drawn editorial sketch style on pure white background. The theme is "接到微调任务后，先判断目标，再判断实现手段，再定义数据形状". The infographic should preserve the original information density, but it should also feel intentionally designed, elegant, and visually memorable rather than merely listing text blocks.

**Design Concept:**
Use a clean vertical editorial infographic with a strong central visual spine. The whole composition should feel like a professional strategist's decision board: structured, layered, and beautiful. Keep the information complete, but present it through deliberate visual choreography, hierarchy, and rhythm.

The reader should scan from top to bottom and experience one continuous reasoning path:

- Step 1: classify the training target
- Step 2: judge whether fine-tuning is the right method
- Step 3: determine the data shape for each target type

Do not use a literal decorative metaphor that overwhelms the content. Instead, introduce subtle visual metaphors inside each module:

- Module 1 feels like a taxonomy wall / classification gallery
- Module 2 feels like a strategy switchboard / routing panel
- Module 3 feels like a data blueprint / specification sheet

The whole image should feel like a compact but premium planning framework for real-world fine-tuning work.

**Layout Structure:**

**Top Section (Title Area - 10%):**

- Main title in bold, large font: "老板让你微调一个模型，第一时间怎么规划？"
- Add a subtle top header system:
  - left corner micro label: "Fine-Tuning Planning Framework"
  - right corner micro label: "Step 1-3"
- Typography should feel like a magazine cover mixed with a technical whitepaper
- Large breathing room around title, but no wasted space

**Body Structure (Main Content - 85%):**
Create three vertically stacked information modules connected by a slim central guide line or directional spine. Each module should feel visually distinct, but still part of one coherent system.

- Use oversized section numbers 01 / 02 / 03 as anchor elements
- Use asymmetric layout rhythm: title block on one side, content block on the other, alternating lightly for sophistication
- Use divider bands, arrow cues, and panel framing to create progression
- Keep information dense, but introduce visual breathing through grouping and hierarchy

## Module 1 - 第一步：先把目标翻译成训练目标

- Module title: "第一步：先把目标翻译成训练目标"
- Intro annotation: "老板说的通常是业务语言，不是训练语言。你要先把它翻译成下面几类之一："
- Visual idea: this section should feel like a taxonomy board or curated card wall
- Show six complete target categories as elegant structured cards in a 3-column × 2-row matrix:
  - 风格对齐：更像某种口吻、品牌语气、客服语气
  - 格式约束：稳定输出 JSON、表格、固定字段
  - 任务学习：分类、抽取、改写、摘要、排序
  - 复杂生成：SQL、代码、长文生成、多轮决策
  - 知识增强：更懂公司知识、行业知识、产品知识
  - 偏好对齐：更稳、更短、更礼貌、更少废话
- Add one emphasis note below:
  - "这一步最关键，因为不同类别直接决定数据长什么样。"
- Visual instruction:
  - Keep all six categories fully visible
  - Each card should have a distinct micro-icon and a slightly different accent marker, but remain stylistically unified
  - Prefer refined classification cards, not plain bullet blocks
  - Use subtle shadows, thin technical borders, corner tags, and tiny annotation marks
  - The section should read as "first classify the problem space"

## Module 2 - 第二步：先判断“是不是该微调”

- Module title: "第二步：先判断“是不是该微调”"
- Intro annotation: "很多需求看起来像微调，实际上不一定。你可以直接用这个判断表："
- Visual idea: this section should feel like a routing console or strategy switchboard
- Show a clear decision table or paired routing list:
  - 学风格、学格式、学固定任务 → 优先考虑微调
  - 补最新知识、企业知识、频繁变化知识 → 优先考虑 RAG / 检索，不要先想着 SFT
  - 让输出更符合偏好 → 先做 SFT，必要时再做偏好优化
  - 复杂工具调用、多步决策 → 可以微调，但要预期需要更高质量数据和更细评测
- Add a highlighted central question box:
  - "这个需求，是想让模型“会一种行为”，还是想让模型“记住一批知识”？"
- Add a short conclusion line:
  - "前者通常适合微调，后者很多时候更适合检索或继续预训练。"
- Visual instruction:
  - Use left-right paired lanes or stacked routing rows with directional arrows
  - Highlight the central question as the emotional and visual focal point of this module
  - Make "行为" and "知识" visually contrast through color or badge treatment
  - The reader should feel a clear moment of decision here, not just more text

## Module 3 - 第三步：立刻确定数据最小单元

- Module title: "第三步：立刻确定“数据最小单元”"
- Intro annotation: "一旦知道目标类型，你就能很快知道数据该长什么样。"
- Visual idea: this section should feel like a polished data specification sheet or blueprint
- Show a high-density three-column mapping table:
  - Column A: 目标类型
  - Column B: 数据形式
  - Column C: 重点
- Populate the table with all original content:
  - 风格对齐 → 用户输入 -> 理想回答 → 语气、长度、结构一致
  - 格式约束 → 输入 -> 标准格式输出 → 字段完整、边界输入、异常输入
  - 分类 / 抽取 / 改写 / 摘要 → 原始输入 -> 唯一标准答案 → 标注一致性，减少多解
  - SQL / 代码 / 复杂生成 → 需求描述 + 上下文 -> 高质量目标输出 → 覆盖 schema、边界条件、失败样本
  - 知识问答 → 问题 + 必要上下文 -> 标准回答 → 别把“裸知识背诵”当主要路径，优先考虑带检索上下文
  - 偏好优化 → 同一输入 -> 好回答 / 差回答 → 偏好标准要一致
- Add one emphasis note below:
  - "真正决定后续效率的，不是先收多少条，而是先把“每条样本长什么样”定义清楚。"
- Visual instruction:
  - Prioritize completeness and mapping clarity
  - Use a table-like layout with thin technical divider lines
  - Add subtle row-grouping highlights so the table feels designed, not spreadsheet-like
  - Keep the row alignment clean and readable
  - This section should visually communicate: "now we are translating strategy into training data specs"

**Key Visual Elements:**

- A slim central progression spine running vertically through the whole infographic
- Large editorial section numbers: 01 / 02 / 03
- Clear horizontal separators between modules
- Classification gallery cards in module 1
- Strategy routing panel in module 2
- Dense but elegant specification table in module 3
- Small arrow cues or transition markers connecting the three steps
- Tiny technical annotations, corner labels, and framing lines to create a premium information-design feel
- Minimal decorative noise, maximum structured beauty

**Typography:**

- All labels and annotations in simplified Chinese
- Technical terms can remain in English only where natural: JSON, SQL, RAG, SFT
- Chinese text slightly enlarged for readability
- Strong hierarchy between title, module title, table items, and emphasis notes
- Use typography contrast intentionally:
  - bold condensed style for big titles and section numbers
  - regular clean sans-serif for annotations
  - compact mono or semi-mono feeling for table rows and technical labels
- Text should be dense but still clean, luxurious, and scannable

**Visual Style:**

- Hand-drawn technical infographic aesthetic with editorial sophistication
- White background
- Professional knowledge-card style, not cartoon style
- Strong editorial composition, like a hybrid of engineering cheat sheet and premium magazine infographic
- Information-dense, highly structured, clearly segmented
- Thin blueprint lines, sketch arrows, lightly imperfect hand-drawn outlines, elegant spacing rhythm
- Social-media optimized for Xiaohongshu educational content

**Color Palette:**

- Navy blue (#2C3E50) for main text, structure, and major borders
- Teal (#16A085) for arrows, progression spine, and strategic highlights
- Burnt orange (#E67E22) for emphasis boxes and decision moments
- Sage green (#7D9D8C) or muted green-gray for data-specification accents
- Light gray for secondary lines, panel backgrounds, and helper guides
- Pure white background

**Overall Feel:**

- Direct and practical
- Beautiful but disciplined
- Feels like a real decision framework someone can apply immediately
- Emphasize retention of original information, not visual simplification
- The design should feel "smart", "expensive", and "trustworthy"
- The viewer should finish the image with one clear takeaway: first classify the goal, then choose the method, then define the data unit

Style: Highly structured vertical technical infographic, refined hand-drawn editorial sketch on white background, premium information design, strong information retention, three stacked modules, social-media-friendly knowledge graphic
