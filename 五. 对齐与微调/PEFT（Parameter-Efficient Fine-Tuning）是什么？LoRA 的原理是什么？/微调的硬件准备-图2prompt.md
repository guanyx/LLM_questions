# 微调的硬件准备：图 2 Prompt

Create a highly detailed vertical technical infographic in refined hand-drawn editorial sketch style on pure white background. The theme is "微调硬件怎么快速判断？先定基线，再看增压，再判断值不值得升级". The infographic should preserve the information density of a practical hardware decision framework, while also feeling elegant, intentional, and visually memorable.

**Design Concept:**
Use a clean vertical editorial infographic with a strong central progression spine. The whole composition should feel like a hardware decision card for LLM fine-tuning: structured, premium, practical, and immediately usable.

The reader should scan from top to bottom and complete one continuous planning path:

- Step 1: use training method × model size to determine a baseline tier
- Step 2: use context length and batch to decide whether to move up one or two tiers
- Step 3: use throughput target and data scale to decide whether the upgrade is worth it

Do not use a decorative metaphor that overwhelms the content. Instead, give each module its own restrained visual identity:

- Module 1 feels like a baseline-tier card wall
- Module 2 feels like a pressure booster panel
- Module 3 feels like an upgrade-worth-it decision board

The whole image should feel like a compact but premium hardware planning framework for real-world fine-tuning work.

**Layout Structure:**

**Top Section (Title Area - 10%):**

- Main title in bold, large font: "微调硬件怎么快速判断？先定基线，再看增压，再判断值不值得升级"
- Add a subtle top header system:
  - left corner micro label: "Fine-Tuning Hardware Planning"
- Typography should feel like a magazine cover mixed with a technical whitepaper
- Large breathing room around title, but no wasted space

**Body Structure (Main Content - 85%):**
Create four vertically stacked information modules connected by a slim central guide line or directional spine. Each module should feel visually distinct, but still part of one coherent system.

- Use asymmetric layout rhythm: title block on one side, content block on the other, alternating lightly for sophistication
- Use divider bands, arrow cues, and panel framing to create progression
- Keep information dense, but introduce visual breathing through grouping and hierarchy

## Module 1 - 先定基线档：训练方式 × 模型大小

- Module title: "先定基线档：训练方式 × 模型大小"
- Intro annotation: "先不要急着想卡数，先把项目归到一个基础档位。"
- Visual idea: this section should feel like a baseline-tier card wall or hardware tier board
- Show four baseline tiers as refined cards:
  - A 档：轻量试验
    - 常见组合：QLoRA + 7B～8B
    - 直觉：先追求“跑起来”
    - 常落在：16GB～24GB 起步，24GB 更从容
  - B 档：常规微调
    - 常见组合：LoRA + 7B～14B，或 QLoRA + 13B～14B
    - 直觉：已经不是能不能跑，而是跑得别太难受
    - 常落在：24GB～48GB，部分场景希望到 48GB
  - C 档：高压训练
    - 常见组合：LoRA + 30B～32B，或较小模型但想做更激进的全参数微调
    - 直觉：高显存开始变成前提
    - 常落在：80GB 档，或者多卡配合
  - D 档：企业级 / 研究级
    - 常见组合：70B+，或中大模型的全参数微调
    - 直觉：瓶颈已经不只是显存
    - 常落在：多张高显存卡，甚至完整集群
- Add one takeaway strip:
  - "先问自己：这个项目的基线档位是 A / B / C / D 哪一档？"
- Visual instruction:
  - Make the four cards feel like a tier system, not a score table
  - Use progressively heavier visual weight from A → D
  - The section should communicate: baseline first, details later

## Module 2 - 再看增压项：上下文长度 + batch

- Module title: "再看增压项：上下文长度 + batch"
- Intro annotation: "基线档位只是起点，真正会把你从“能跑”推到“跑不动”的，往往是上下文长度和有效 batch。"
- Visual idea: this section should feel like a pressure booster panel or activation-pressure blueprint
- Show three pressure states:
  - 不加压
    - 短上下文
    - 小 batch
    - 可以按基线档位先估
  - 上调一档
    - 上下文明显变长
    - 或 batch 想做得更像样
    - 显存和激活内存压力都会明显上来
  - 上调两档
    - 长上下文 + 还想保留较高吞吐
    - 或模型本来就不小，还要更大的有效 batch
    - 很容易从“单卡勉强跑”跳到“高显存卡 / 多卡”
- Add one warning strip:
  - "模型大小决定地板，上下文和 batch 决定会不会突然撞天花板。"
- Visual instruction:
  - Use layered pressure bars, arrows, or booster stages
  - Make this section feel like a modifier on top of the baseline tier
  - The viewer should immediately understand: long context can move the whole plan up

## Module 3 - 最后判断：值不值得升级

- Module title: "最后判断：值不值得升级"
- Intro annotation: "前两步解决能不能装下，第三步解决值不值得为了更快出结果而升级硬件。"
- Visual idea: this section should feel like an upgrade decision board or cost-benefit panel
- Split this section into two decision columns:
  - 吞吐目标
    - 能跑就行
    - 当天要出结果
    - 高频调参 / 多轮重训
  - 数据规模
    - 小：不一定逼你升级显存，但时间成本可能仍然高
    - 中：会明显影响总训练时长和 checkpoint 数量
    - 大：训练时长、迭代成本、存储和恢复训练压力都会上来
- Add the key interpretation:
  - 数据规模不一定直接决定“单步能不能放进显存”
  - 但会决定“慢训练是不是已经不可接受”
- Add one final memory strip:
  - "吞吐目标和数据规模，决定升级值不值。"
- Visual instruction:
  - Use decision lanes, yes/no upgrade cues, or cost-benefit arrows
  - Make “值不值得升”成为这一块的焦点，而不是单纯罗列概念
  - The section should read like a business decision, not a hardware checklist

**Key Visual Elements:**

- Clear horizontal separators between modules
- Baseline-tier wall in module 1
- Pressure booster panel in module 2
- Upgrade-worth-it decision board in module 3
- Small arrow cues or transition markers connecting the four steps
- Tiny technical annotations, corner labels, and framing lines to create a premium information-design feel
- Minimal decorative noise, maximum structured beauty

**Typography:**

- All labels and annotations in simplified Chinese
- Technical terms can remain in English only where natural: QLoRA, LoRA, batch, checkpoint
- Chinese text slightly enlarged for readability
- Strong hierarchy between title, module title, tier labels, and emphasis notes
- Use typography contrast intentionally:
  - bold condensed style for big titles and section numbers
  - regular clean sans-serif for annotations
  - compact mono or semi-mono feeling for tiers, labels, and hardware-like data blocks
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
- Burnt orange (#E67E22) for emphasis strips, threshold warnings, and decision points
- Sage green (#7D9D8C) or muted green-gray for VRAM and system-resource accents
- Light gray for secondary lines, panel backgrounds, and helper guides
- Pure white background

**Overall Feel:**

- Direct and practical
- Beautiful but disciplined
- Feels like a real hardware decision framework someone can apply immediately
- Emphasize retention of original information, not visual simplification
- The design should feel "smart", "expensive", and "trustworthy"
- The viewer should finish the image with one clear takeaway: use a tiered decision card rather than isolated concepts — baseline first, pressure second, upgrade value third, system check last

Style: Highly structured vertical technical infographic, refined hand-drawn editorial sketch on white background, premium information design, strong information retention, four stacked modules, social-media-friendly knowledge graphic
