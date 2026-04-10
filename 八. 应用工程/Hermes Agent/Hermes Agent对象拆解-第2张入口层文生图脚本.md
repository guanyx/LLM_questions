# Hermes Agent对象拆解：第 2 张入口层文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "Hermes 从哪里接收任务？".

**Design Concept:**
Use a concrete task-entry journey metaphor instead of a static convergence diagram: the image should follow one task as it enters from different surfaces, passes through the same intake steps, and lands in one shared AIAgent runtime. The image should make it immediately clear that Hermes does not have five independent brains. It has different doors, but one receiving process behind them.

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "Hermes 从哪里接收任务？"
- Subtitle below: "不同入口，只是不同的门；进门以后，走进的是同一个 Agent"
- Small supporting sentence: "CLI、消息平台、编辑器、API、批处理，最后都汇入同一个 AIAgent 核心"
- Typography should feel like a technical teardown cover rather than a marketing poster

**Central Section (Hero Diagram - 55%):**
Create a top-to-bottom “任务进入同一个 Agent”的旅程图 with one main example path and four parallel entry tabs:

- At the top place 5 entry surfaces in one horizontal row, with one main example highlighted and the others shown as parallel entrances:
  1. CLI
     - icon cue: terminal window
     - show one tiny example command:
       - "hermes 帮我分析这个报错"
     - annotation: "本地交互入口"
  2. Gateway
     - icon cue: stacked chat bubbles
     - mini sketch detail: Telegram / Slack / Discord badges
     - annotation: "多平台消息入口"
  3. ACP
     - icon cue: editor pane + cursor
     - mini sketch detail: code selection frame
     - annotation: "编辑器协作入口"
  4. API
     - icon cue: HTTP request card
     - mini sketch detail: POST /tasks
     - annotation: "程序调用入口"
  5. Batch Runner
     - icon cue: queued task stack
     - mini sketch detail: jobs 01 / 02 / 03
     - annotation: "批量任务入口"

- Under the entry row place one thin intake strip labeled "入口适配层"
  - split the strip into 3 small cells:
    - 请求适配
    - 会话创建
    - 上下文绑定
  - make this strip visibly thin, so it reads as bridge logic rather than the real brain

- Under the intake strip place one dominant runtime box labeled "AIAgent"
  - inside show 4 compact internal labels:
    - 接收任务
    - 绑定上下文
    - 调用主循环
    - 返回结果
  - add one small note below:
    - "同一个 Agent 核心"

- Under AIAgent place one output strip labeled "结果返回层"
  - split into 3 small cells:
    - 状态回传
    - 输出封装
    - 返回原表面

- Use one thick vertical main path for the highlighted CLI example:
  - CLI → 入口适配层 → AIAgent → 结果返回层 → CLI
  - this should give the viewer a concrete start and end

- Use four thinner parallel vertical lines for Gateway / ACP / API / Batch Runner
  - they should visually prove that all surfaces走的是同一套 intake 过程

- Add one side note box on the right:
  - label: "共享的不是界面，而是运行时"
  - tiny labels inside:
    - 会话
    - 工具
    - 记忆

- Add one green design-strength callout:
  - label: "设计亮点"
  - annotation: "新增入口更多是在补协议适配和会话桥接，而不是重写一套 Agent"

- Add one orange design-tradeoff callout:
  - label: "设计代价"
  - annotation: "核心统一，但外围接入层会变厚，不同平台仍然要维护协议胶水和状态回传"

- Add one bold judgment note near the lower center:
  - "表面不同，核心不分叉"

**Bottom Section (Interpretation Strip - 25%):**

- Create a horizontal 3-step interpretation strip:
  1. 多入口
  2. 统一汇聚
  3. 同核执行
- Under each step place one tiny explanation:
  - 多入口："终端 / 平台 / 编辑器 / API / 批处理"
  - 统一汇聚："协议适配，不重写 Agent"
  - 同核执行："共享主循环、工具、记忆、压缩"
- Add one conclusion sentence centered at bottom:
  "Hermes 的入口设计强在统一大脑，代价是外围接线更复杂"
- Add footer label:
  "Hermes Agent 对象拆解 / 02"

**What Must Be Clear in the Diagram:**

- The five entry surfaces are not equal internal modules
- The intake strip is interface-adaptation logic, not the real brain
- The real center of gravity is one shared AIAgent runtime
- The viewer should see one concrete request path from entry to return
- The image must visually communicate this architectural judgment:
  "五种表面 → 同一个运行时核心"

**Suitable Diagram Types to Combine:**

- Concrete task-entry journey diagram
- Thin intake-strip schematic
- Shared runtime core diagram
- Parallel vertical entry/exit paths
- Bottom interpretation timeline

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- White background, engineering-document clarity
- Strong top-to-bottom reading path
- Rich technical callouts, but keep the structure easy to scan
- Avoid looking like a generic product architecture slide
- Composition ratio:
  - 50% detailed schematic illustration
  - 25% text labels and technical callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, titles, and runtime frame
- Bright blue (#3498DB) for convergence arrows and routing lines
- Teal (#16A085) for session/context binding highlights
- Orange (#E67E22) for adapter-layer friction or complexity callouts
- Light gray for helper lines and secondary boxes
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep technical terms in English where appropriate: CLI, Gateway, ACP, API, Batch Runner, AIAgent, Agent
- Title should be bold and large
- Secondary labels should be small but readable on mobile

**Overall Feel:**

- Clean and structural
- Instantly understandable at a glance
- Technically grounded rather than decorative
- Emphasize concrete request journey, not feature enumeration
- Suitable for Xiaohongshu-style knowledge cover carousel

Style: Detailed technical hand-drawn infographic, concrete multi-entry task journey, shared intake-to-runtime-to-return architecture, pure white background
