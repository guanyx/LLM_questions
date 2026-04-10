# Hermes Agent对象拆解：第 4 张Prompt组装层文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "Hermes 是怎么把“自己”组装出来的？".

**Design Concept:**
Use a concrete prompt-building journey metaphor instead of a broad assembly-line concept diagram: the image should follow one task from “准备开工”开始，展示 Hermes 如何收集上下文材料、先做扫描、再拼成系统提示词快照，最后把它送进当前任务。 The visual emphasis should be on one clearly readable组装过程，而不是只看见一堆输入材料。

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "Hermes 是怎么把“自己”组装出来的？"
- Subtitle below: "Hermes 每次开工前，都会先把“我是谁、我记得什么、当前项目是什么”拼成一张工作底稿"
- Small supporting sentence: "系统提示词不是一段固定文案，而是一条由人格、记忆、用户偏好、项目上下文、技能索引、工具说明组成的装配线"
- Typography should feel like an engineering teardown poster, not a conceptual AI poster

**Central Section (Hero Diagram - 55%):**
Create a left-to-right concrete prompt-building journey diagram with one start point and one final output:

- Build one thick main path across the center:
  - 当前任务准备开工
  - 收集上下文材料
  - 上下文扫描
  - 组装系统提示词
  - 冻结快照
  - 进入当前任务工作底稿

- Stage 1 - 当前任务准备开工
  - on the far left place one small task card
  - tiny example:
    - "开始处理代码库问题"
  - annotation: "Hermes 开工前，不是直接把模型叫起来，而是先准备工作底稿"

- Stage 2 - 收集上下文材料
  - place one medium-large collection box
  - split it into 7 compact material slots:
    - SOUL
    - MEMORY
    - USER
    - AGENTS
    - 项目上下文
    - Skills Index
    - Tool Instructions
  - use material-slot visuals instead of scattered cards
  - this should feel like one装料步骤，而不是七个并列主角

- Stage 3 - 上下文扫描
  - place one clear checkpoint box after the collection box
  - label:
    - 上下文扫描
    - 注入风险检查
  - add mini note:
    - "过滤明显 prompt injection 风险"

- Stage 4 - 系统提示词组装
  - place one larger assembly box
  - inside show 4 compact steps:
    - 收敛材料
    - 排序结构
    - 生成前缀
    - 形成系统提示词
  - this is the main process stage, not a decorative工作台

- Stage 5 - 冻结快照
  - place one smaller but visually crisp box after组装
  - label:
    - snapshot
    - 稳定
    - 可缓存
  - annotation: "优先稳定，不在会话中途频繁漂移"

- Stage 6 - 当前任务工作底稿
  - place one final output sheet on the far right
  - label: "当前任务工作底稿"
  - add one smaller subtitle:
    - Stable System Prompt
  - this should feel like真实投入使用的工作前缀，而不是抽象产物

- Add one small lower-side note box:
  - label: "cache / snapshot"
  - annotation: "技能系统提示词可复用，避免每轮全量重组"

- Add one green design-strength callout:
  - label: "设计亮点"
  - annotation: "系统提示词不是固定文案，而是从人格、记忆、用户、项目、技能、工具共同组装出来的稳定工作底稿"

- Add one orange design-tradeoff callout:
  - label: "设计代价"
  - annotation: "来源越多，行为越强，但也越难追溯“这一轮到底受谁影响”"

- Add one bold judgment note below the main path:
  - "这不是 prompt 文案，而是一条工作底稿生成旅程"

**Bottom Section (Interpretation Strip - 25%):**

- Create a horizontal 3-step interpretation strip:
  1. 不是固定文案
  2. 是上下文装配
  3. 输出稳定工作底稿
- Under each step add one compact explanation:
  - 不是固定文案："不是一段死 prompt"
  - 是上下文装配："人格 / 记忆 / 用户 / 项目 / 技能 / 工具共同拼装"
  - 输出稳定工作底稿："稳定优先，支持缓存，不随时漂移"
- Add one conclusion sentence centered at bottom:
  "Prompt 组装层的本质不是即时拼接，而是先把复杂上下文装成一张可工作的底稿"
- Add footer label:
  "Hermes Agent 对象拆解 / 04"

**What Must Be Clear in the Diagram:**

- Hermes is not starting from one static system prompt
- The prompt is assembled from multiple structured context files and runtime sources
- There is a scan/filter step before the final prompt is formed
- The final output is a stable working prompt snapshot, not a constantly mutating stream
- The viewer should see one concrete start-to-finish prompt-building journey
- The image must visually communicate this judgment:
  "这不是 prompt 文案，而是一条工作底稿生成旅程"

**Suitable Diagram Types to Combine:**

- Concrete prompt-building journey
- Material collection box
- Inspection/filter checkpoint
- Snapshot freeze box
- Final working-draft output sheet
- Stability/cache callouts
- Bottom interpretation timeline

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Pure white background
- Strong left-to-right assembly flow
- Rich technical labels, but the structure should stay readable at a glance
- Closer to a systems workflow board than an abstract LLM diagram
- Composition ratio:
  - 50% detailed schematic illustration
  - 25% text labels and technical callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, labels, frames, and final prompt sheet border
- Bright blue (#3498DB) for assembly arrows and workflow direction
- Green (#16A085) for stable output, cache, and reusable context cues
- Orange (#E67E22) for scan/filter and design tradeoff callouts
- Light gray for helper guides, paper textures, and secondary annotations
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep technical terms in English where appropriate: Prompt, Stable System Prompt, Skills Index, Tool Instructions, cache, snapshot
- Title should be bold and prominent
- Secondary callouts should be compact but readable on mobile

**Overall Feel:**

- Concrete and explanatory
- Calm but information-dense
- Immediately conveys how Hermes “把工作底稿先准备好” before work begins
- Not decorative; clearly operational and source-driven
- Suitable for Xiaohongshu-style technical carousel

Style: Detailed technical hand-drawn infographic, concrete prompt-building journey, structured context-to-stable-working-draft workflow, pure white background
