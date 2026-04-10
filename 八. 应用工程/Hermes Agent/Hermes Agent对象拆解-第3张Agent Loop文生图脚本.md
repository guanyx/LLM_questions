# Hermes Agent对象拆解：第 3 张Agent Loop文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "Hermes 真正的大脑：Agent Loop".

**Design Concept:**
Use a staged runtime-control metaphor instead of a circular loop: the image should show that Hermes does not stop at one model call. Instead, it pushes a task through a clearly ordered sequence of steps, then conditionally jumps back to an earlier stage when more work is needed. The visual focus should be on readable control flow, not on chat UI or abstract rings.

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "Hermes 真正的大脑：Agent Loop"
- Subtitle below: "聊天模型只负责生成；Agent Loop 负责把任务真的跑完"
- Small supporting sentence: "Hermes 的核心不是一次回答，而是一轮轮判断、执行、回填、再判断"
- Typography should feel like a systems teardown poster, not a consumer product banner

**Central Section (Hero Diagram - 55%):**
Create a left-to-right staged control-flow diagram with one clear main path and one visible return jump:

- Build the main execution path as a horizontal 7-stage pipeline across the middle of the image
- Make each stage a clearly separated box so the viewer always knows where to start and where to end:
  1. 用户输入
     - icon cue: message bubble or task card
     - annotation: "新请求 / 中断重定向 / 继续执行"
  2. 构造上下文
     - icon cue: stacked prompt sheets
     - annotation: "系统提示词 / 会话历史 / 技能 / 工具"
  3. 模型判断
     - icon cue: model core box
     - annotation: "生成下一步动作"
  4. 是否调工具
     - icon cue: decision diamond
     - annotation: "回答 or 调用工具"
  5. 工具执行
     - icon cue: wrench + terminal + browser mini icons
     - annotation: "命令 / 文件 / Web / 记忆"
  6. 回填结果
     - icon cue: result packet
     - annotation: "工具结果写回上下文"
  7. 再次判断 / 最终输出
     - icon cue: split-output decision box
     - annotation: "继续循环 or 收敛结束"

- Make the "是否调工具" and "再次判断 / 最终输出" stages visually different from ordinary process boxes
  - use decision-diamond or decision-split shapes
  - these must read as the control points of the whole flow

- Place one compact controller box above the middle stages labeled "AIAgent Runtime"
  - connect it downward to 构造上下文 / 模型判断 / 工具执行 / 再次判断
  - inside show 4 tiny labels:
    - 迭代控制
    - 工具编排
    - 状态维护
    - 收敛判断
  - this box should feel like the stage controller, not the center of a circle

- Add one clear return arrow from "回填结果" back to "构造上下文"
  - label this arrow: "继续循环"
  - make it a clean upper or lower jump-back path, not a full ring
  - the viewer should see: 主路径向前推进，但必要时会跳回前面重跑

- Add one thinner alternate direct path:
  - 模型判断 → 最终输出
  - label: "无需工具时直接收敛"

- Add three side callout modules with leader lines:
  - 可中断
    - annotation: "任务执行中可被用户打断或改道"
  - 可重试
    - annotation: "失败后可继续尝试，不必整轮重来"
  - 有预算上限
    - annotation: "最大迭代数 / 防止无限循环"

- Add two secondary hidden-mechanism boxes below the main path:
  - 上下文压缩
    - connect to 回填结果 → 构造上下文 的跳回路径
    - annotation: "上下文过长时压缩中段历史"
  - 会话持久化
    - connect near 最终输出
    - annotation: "结束时写回状态，避免进度丢失"

- Add one orange runtime-warning strip near the lower right:
  - 最大迭代数触发
  - 工具失败重试
  - 上下文过长触发压缩
  - make it feel like runtime constraints, not another stage

**Bottom Section (Interpretation Strip - 25%):**

- Create a horizontal 3-step interpretation strip:
  1. 不是单轮调用
  2. 是回合式执行
  3. 直到任务收敛
- Under each step add one compact explanation:
  - 不是单轮调用："不是问一句答一句"
  - 是回合式执行："判断 → 调工具 → 回填 → 再判断"
  - 直到任务收敛："受预算、压缩、重试机制约束"
- Add one conclusion sentence centered at bottom:
  "Hermes 把真正难的部分放在主循环：控制任务如何继续，而不是只控制模型说什么"
- Add footer label:
  "Hermes Agent 对象拆解 / 03"

**What Must Be Clear in the Diagram:**

- Agent Loop is the real brain of Hermes
- A model call is only one stage inside the loop, not the whole system
- Tools are not outside the loop; they are one decision branch inside the loop
- Compression, retry, interruption, and iteration budget are runtime control features
- The image must visually communicate this judgment:
  "Hermes 的核心不是生成答案，而是让任务在循环里收敛"

**Suitable Diagram Types to Combine:**

- Staged control-flow diagram
- Decision-diamond control flow
- Runtime controller box above the flow
- Jump-back return arrow
- Runtime constraint callouts
- Bottom interpretation timeline

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Pure white background
- Clear left-to-right control flow with dense engineering annotations
- Strong control-system feeling, closer to a runtime flowchart than a product illustration
- Composition ratio:
  - 50% detailed schematic illustration
  - 25% text labels and technical callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, stage boxes, and text
- Bright blue (#3498DB) for main loop arrows and control flow
- Green (#16A085) for successful return paths and convergence cues
- Orange (#E67E22) for retry, iteration cap, and warning branches
- Light gray for helper guides and subtle structure lines
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep technical terms in English where appropriate: Agent Loop, AIAgent Runtime
- Title should be bold and visually dominant
- Callout text should be compact but readable on mobile

**Overall Feel:**

- Strong runtime-control feeling
- Intellectually dense but visually clear
- Not a chat product diagram, but a task-execution brain diagram
- Easy to understand even at a glance
- Suitable for Xiaohongshu-style technical carousel

Style: Detailed technical hand-drawn infographic, closed-loop Agent runtime control diagram, task-convergence flowchart, pure white background
Style: Detailed technical hand-drawn infographic, staged Agent runtime control flow, readable jump-back iteration path, task-convergence flowchart, pure white background
