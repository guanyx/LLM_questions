# 微调的硬件准备：图 1 Prompt

Create a highly detailed vertical technical infographic in refined hand-drawn editorial sketch style on pure white background. The theme is "评估微调硬件时，先看训练方式，再看模型大小与上下文，最后看吞吐目标". The infographic should preserve the information density of a practical decision framework, while also feeling elegant, intentional, and visually memorable.

**Design Concept:**
Use a clean vertical editorial infographic with a strong central progression spine. The whole composition should feel like a hardware planning board for LLM fine-tuning: precise, structured, premium, and immediately actionable.

The reader should scan from top to bottom and complete one continuous reasoning path:

- Step 1: decide what kind of fine-tuning you are doing
- Step 2: understand why model size is only the floor, while context length can become the ceiling
- Step 3: realize that training duration is really a throughput question

Do not use a decorative metaphor that overwhelms the content. Instead, give each module its own restrained visual identity:

- Module 1 feels like a training-mode control panel
- Module 2 feels like a memory-pressure blueprint
- Module 3 feels like a throughput planning dashboard

The whole image should feel like a compact but premium hardware estimation framework for real-world fine-tuning work.

**Layout Structure:**

**Top Section (Title Area - 10%):**

- Main title in bold, large font: "微调硬件怎么估？训练方式，模型大小，上下文和吞吐"
- Add a subtle top header system:
  - left corner micro label: "Fine-Tuning Hardware Planning"
  - right corner micro label: "Step 1-3"
- Typography should feel like a magazine cover mixed with a technical whitepaper
- Large breathing room around title, but no wasted space

**Body Structure (Main Content - 85%):**
Create three vertically stacked information modules connected by a slim central guide line or directional spine. Each module should feel visually distinct, but still part of one coherent system.

- Use asymmetric layout rhythm: title block on one side, content block on the other, alternating lightly for sophistication
- Use divider bands, arrow cues, and panel framing to create progression
- Keep information dense, but introduce visual breathing through grouping and hierarchy

## Module 1 - 第一步：先判断你做的是哪种微调

- Module title: "第一步：先判断你做的是哪种微调"
- Intro annotation: "训练方式一变，硬件量级就会变。"
- Visual idea: this section should feel like a training-mode control panel or strategy selector
- Show four complete fine-tuning modes as refined cards in a 2-column × 2-row matrix:
  - LoRA / DoRA / Adapter 类微调
    - 只训练少量新增参数
    - 对显存最友好，通常是默认起点
  - QLoRA / 量化后再做适配器微调
    - 在 LoRA 的基础上继续压低显存
    - 适合单卡试验和成本敏感场景
    - 代价是吞吐更低，稳定性要更谨慎评估
  - 全参数微调
    - 真正把整个模型都训起来
    - 对显存、通信、稳定性要求都更高
    - 只有必要性很强时才考虑
  - 偏好优化 / DPO / RLHF 后续阶段
    - 如果建立在 SFT 模型之上
    - 硬件需求通常继承前面的训练方式
    - 流程更复杂，工程开销继续上升
- Add one highlighted takeaway strip:
  - "先决定训练方式，再决定硬件"
- Visual instruction:
  - Each card should have a small distinct control-panel icon or module badge
  - Use subtle level cues to imply different hardware weights, but do not turn it into a chart
  - The section should read as "hardware planning starts with training mode"

## Module 2 - 第二步：基座模型大小决定地板，上下文长度决定天花板

- Module title: "第二步：基座模型大小决定“地板”，上下文长度决定“天花板”"
- Intro annotation: "模型大小决定最低门槛，但真正把你从“能跑”推到“跑不动”的，往往是上下文长度。"
- Visual idea: this section should feel like a memory-pressure blueprint with layered capacity zones
- Show two core memory concepts as technical callout blocks:
  - 显存（VRAM）
    - GPU 的高速工作区
    - 不够就会直接失败，或被迫压小 batch 和长度
  - 激活内存
    - 前向传播时临时保存的中间结果
    - 序列越长、batch 越大、层数越多，越容易爆
- Add a compact scenario illustration for a 7B model:
  - 短输入、短输出、LoRA、小 batch → 一张消费级高显存卡就可能跑起来
  - 长上下文或更高吞吐 → 需求会迅速上跳
- Show the four core planning variables as a grouped checklist or technical panel:
  - 模型参数规模
  - 上下文长度
  - 有效 batch size
  - 训练方式
- Add one emphasis note:
  - "这 4 个量缺一个，预算都可能不准。"
- Visual instruction:
  - Use layered boxes, capacity bars, or blueprint-style zones to suggest floor vs ceiling
  - Make “激活内存” visibly feel like the underestimated pressure source
  - The section should communicate: model size matters, but long context can rewrite the budget

## Module 3 - 第三步：训练时长其实是在问你要多高的吞吐

- Module title: "第三步：训练时长其实是在问“你要多高的吞吐”"
- Intro annotation: "很多人说“我想估硬件”，其实是在问：我希望多久训完。"
- Visual idea: this section should feel like a throughput planning dashboard or scheduling panel
- Show the three hardware choices as a progression row or routing band:
  - 单卡慢慢跑
  - 多卡并行
  - 直接上高带宽、高显存的数据中心卡
- Show the two core throughput factors in a formula-like visual block:
  - 总共要处理多少 token
  - 你每秒能吞多少 token
- Add the interpretation note:
  - 第一项跟数据规模和 epoch 有关
  - 第二项跟硬件、精度、并行方式、序列长度都有关系
- Add a practical caution panel:
  - 数据量不大，不一定意味着硬件要求低
  - 如果你要求一天内出结果
  - 或者你要频繁调参、反复重训
  - 你需要的不是“勉强能跑”，而是“有足够吞吐”
- Add one conclusion line:
  - "很多团队买的不是最低可运行硬件，而是能跟上业务节奏的硬件。"
- Visual instruction:
  - Use directional arrows, schedule lanes, or throughput gauges
  - Make “多久训完” become the emotional focal point of this module
  - The section should visually communicate: hardware planning is really time-to-result planning

**Key Visual Elements:**

- A slim central progression spine running vertically through the whole infographic
- Large editorial section numbers: 01 / 02 / 03
- Clear horizontal separators between modules
- Training-mode selector cards in module 1
- Memory blueprint / floor-vs-ceiling layout in module 2
- Throughput dashboard / scheduling panel in module 3
- Small arrow cues or transition markers connecting the three steps
- Tiny technical annotations, corner labels, and framing lines to create a premium information-design feel
- Minimal decorative noise, maximum structured beauty

**Typography:**

- All labels and annotations in simplified Chinese
- Technical terms can remain in English only where natural: LoRA, QLoRA, DoRA, Adapter, DPO, RLHF, SFT, VRAM, token, batch
- Chinese text slightly enlarged for readability
- Strong hierarchy between title, module title, callout blocks, and emphasis notes
- Use typography contrast intentionally:
  - bold condensed style for big titles and section numbers
  - regular clean sans-serif for annotations
  - compact mono or semi-mono feeling for technical labels and small data-like blocks
- Text should be dense but still clean, premium, and scannable

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
- Burnt orange (#E67E22) for emphasis strips, bottleneck warnings, and decision points
- Sage green (#7D9D8C) or muted green-gray for memory and throughput accents
- Light gray for secondary lines, panel backgrounds, and helper guides
- Pure white background

**Overall Feel:**

- Direct and practical
- Beautiful but disciplined
- Feels like a real hardware planning framework someone can apply immediately
- Emphasize retention of original information, not visual simplification
- The design should feel "smart", "expensive", and "trustworthy"
- The viewer should finish the image with one clear takeaway: hardware planning is not just about model size; it starts with training mode, is constrained by memory behavior, and is ultimately shaped by throughput goals

Style: Highly structured vertical technical infographic, refined hand-drawn editorial sketch on white background, premium information design, strong information retention, three stacked modules, social-media-friendly knowledge graphic
