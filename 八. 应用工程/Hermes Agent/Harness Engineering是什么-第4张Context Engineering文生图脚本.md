# Harness Engineering 是什么：第 4 张“Context Engineering”文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "最贵的不是模型调用，而是错误的上下文". The image should make it immediately clear that many so-called model failures are actually context failures. This should feel like a left-to-right "dirty context pool -> context shaping layer -> clean working context" rectification diagram, not a vague abstract concept poster.

**Design Concept:**

Use a "上下文整流 / context shaping" metaphor:

- left side = noisy, bloated, mixed context pool
- middle section = filtering, retrieval, compression, and isolation layer
- right side = clean, short, task-relevant working context entering the model

The key visual judgment is:

**今天很多 Agent 体验差，不是因为模型太笨，而是因为喂给它的上下文太脏。**

The image should make viewers feel that context is not something you simply dump into a model. It must be selected, compressed, isolated, and shaped before it becomes usable. The reading direction must be obvious at first glance: left = raw context, middle = shaping system, right = clean context.

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "最贵的不是模型调用，而是错误的上下文"
- Subtitle below: "很多看起来像“模型不行”的问题，本质上是上下文工程没做好"
- Small supporting sentence:
  "真实任务里，难的不是把更多内容塞给模型，而是把最关键、最干净、最当前的那部分工作底稿筛出来"
- Typography should feel like a technical editorial blueprint, not a prompt-tips poster

**Central Section (Hero Diagram - 58%):**

Create one dominant horizontal context-rectification composition with three clear regions:

- Left region - 原始上下文池:
  - build a large, visually messy source area
  - represent multiple kinds of raw context materials as overlapping cards, strips, and fragments:
    - 聊天历史
    - 长文档
    - 检索结果
    - 工具输出
    - 日志片段
    - 项目文件
    - 用户偏好
    - 旧任务状态
  - these materials should feel mixed together, not yet structured
  - add tiny warning tags scattered across the left region:
    - 重复
    - 过时
    - 无关
    - 太长
    - 噪声
  - use a small top-left label:
    - "Raw Context Pool"
  - visually this area should look crowded, heavy, and slightly chaotic

- Middle region - Context Shaping 层:
  - this is the key engineering layer of the image
  - build this as a vertical processing strip or a stack of shaping modules
  - include 4 shaping modules in order:
    - preselection
    - retrieval
    - compression
    - isolation
  - each module should have compact Chinese explanations:
    - preselection: 先筛出这一步真正相关的内容
    - retrieval: 先找证据，再决定注入什么
    - compression: 把长历史压成可工作的短上下文
    - isolation: 不同角色、不同任务不要混用
  - add one small note near the shaping stack:
    - "不是把更多塞进去，而是把无关的挡在外面"
  - use arrows to show raw context fragments entering this layer and only some selected fragments passing through
  - some noisy fragments should be visibly rejected, cut off, or reduced at this layer

- Right region - 干净工作上下文:
  - create a clean, structured context board that will feed the model
  - this should look visibly shorter, cleaner, and more intentional than the left side
  - structure it into 4 compact blocks:
    - 当前任务目标
    - 关键约束条件
    - 必要背景资料
    - 最近有效状态
  - above or beside it, add one label:
    - "Working Context"
  - show one short arrow from this clean board into a small model-entry box
  - the model-entry box should be simple, not the main focus
  - add one green result note:
    - 更稳
    - 更快
    - 更省 token
    - 更少跑偏

- Cost and failure contrast:
  - near the left region add one orange callout:
    - "全塞进去的代价：token 膨胀、注意力发散、目标漂移"
  - near the right region add one teal callout:
    - "筛出来的价值：短、准、当前、可执行"

- Reading logic:
  - the entire hero section should read as:
    - 混乱来源 -> 工程整流 -> 工作底稿
  - do not make the model itself too visually dominant
  - this page is about context shaping, not about model brilliance

**Bottom Section (Interpretation Strip - 22%):**

Create a bottom horizontal interpretation strip with 4 compact stages:

1. "原始上下文"
   - tiny explanation: "历史、文档、日志、工具结果混在一起"
2. "上下文整流"
   - tiny explanation: "筛选、检索、压缩、隔离"
3. "工作底稿"
   - tiny explanation: "当前任务真正需要的那一小部分"
4. "稳定输入"
   - tiny explanation: "更快、更准、更省"

- Connect the four stages with arrows
- Add one bottom conclusion sentence:
  "Context Engineering 的核心，不是喂更多，而是先决定什么不该喂进去"
- Add footer label:
  "Harness Engineering / 04"

**What Must Be Clear in the Diagram:**

- Left side must feel bloated and noisy
- Middle section must look like an active engineering processing layer
- Right side must feel shorter, cleaner, and task-specific
- The image must not imply that long history is automatically beneficial
- The viewer should immediately understand:
  - raw context is not working context
  - context shaping is an engineering step
  - model quality depends heavily on what reaches it

**Suitable Diagram Types to Combine:**

- Left-to-right rectification diagram
- Raw context pool board
- Context shaping processing stack
- Clean working-context board
- Rejected fragment paths
- Bottom interpretation strip

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Professional engineering documentation style
- White background with very clear left-to-right reading order
- Dense annotations but obvious visual hierarchy
- More like a runtime input-conditioning anatomy page than a generic AI explainer
- Composition ratio:
  - 55% detailed schematic illustration
  - 20% labels and technical callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, titles, and structure frames
- Bright blue (#3498DB) for shaping arrows, selection paths, and engineering transitions
- Teal (#16A085) for clean context blocks and stable-input benefits
- Orange (#E67E22) for noise, context bloat, and drift warnings
- Light gray for helper grids, faded historical material, and secondary notes
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep only these technical terms in English where appropriate: Raw Context Pool, Working Context, preselection, retrieval, compression, isolation, token
- Title should be bold and large
- Secondary labels should be compact but readable on mobile

**Overall Feel:**

- Clear and highly readable at a glance
- Technical but not abstract
- Makes the difference between "context dump" and "working context" visually unforgettable
- Immediately communicates that Context Engineering is a shaping layer, not a prompt trick
- Suitable for Xiaohongshu-style knowledge carousel fourth slide

Style: Detailed technical hand-drawn infographic, left-to-right context rectification architecture, noisy raw context pool filtered through shaping modules into clean working context, pure white background
