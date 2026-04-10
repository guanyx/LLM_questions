# Hermes Agent对象拆解：第 11 张Cron Scheduler文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "Hermes 为什么不只是“等你发消息”？".

**Design Concept:**
Use a scheduled-runtime activation metaphor: the image should show that Hermes is not only reactive to chat input. A cron scheduler can wake the runtime at specific times, load a job, create a fresh agent session, inject the right context and skills, run the task, and deliver the result outward. The visual emphasis should be on autonomous activation and service-like continuity.

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "Hermes 为什么不只是“等你发消息”？"
- Subtitle below: "当 Agent 学会定时工作，它就开始像服务，而不只是像聊天对象"
- Small supporting sentence: "Cron 跑的不是裸 shell，而是完整的 Agent 任务：到点唤醒、拉起会话、注入技能、执行再投递"
- Typography should feel like a runtime operations poster, not a generic task-scheduler UI

**Central Section (Hero Diagram - 55%):**
Create a top-to-bottom scheduled-execution flow diagram with a strong service-runtime feeling:

- At the very top place one large clock icon / scheduler dial labeled "Cron Scheduler"
  - make it feel mechanical and system-level, not decorative
  - add tiny tick labels around it:
    - 09:00
    - 18:00
    - 每日
    - 每周
  - annotation: "按规则触发，不等用户来消息"

- Under the clock, build one vertical execution pipeline with 6 major stages:
  1. scheduler tick
     - icon cue: pulse signal leaving the clock
     - annotation: "时间命中调度规则"
  2. load job
     - icon cue: job card / task manifest
     - annotation: "读取任务定义、目标渠道、触发条件"
  3. fresh agent session
     - icon cue: clean session box
     - annotation: "拉起新的 Agent 会话，不直接复用旧对话表面"
  4. inject skills
     - icon cue: skill cards flowing into session
     - annotation: "按任务需要注入技能、上下文和提示"
  5. run prompt
     - icon cue: runtime execution core
     - annotation: "完整 Agent 任务开始运行"
  6. deliver result
     - icon cue: output packet splitting outward
     - annotation: "把结果投递到目标位置"

- Make the 6 stages look like a controlled runtime pipeline, not a plain list
- Use one thick downward main arrow from top to bottom to emphasize that the job is fully executed end-to-end

- On the right side place one small box connected to "load job":
  - label: "Job Definition"
  - inside add tiny labels:
    - prompt
    - 频率
    - 目标渠道
    - 技能需求
  - purpose: show that cron jobs are structured agent tasks, not mere timers

- On the left side place one small box connected to "fresh agent session":
  - label: "新会话上下文"
  - annotation: "与普通聊天会话类似，但由调度器主动拉起"

- At the bottom, fan out the "deliver result" stage into three destination outputs:
  1. 发回原平台
  2. 发到指定渠道
  3. 写本地输出
  - make this branching explicit and visually clean

- Add one green design-strength callout:
  - label: "设计亮点"
  - annotation: "Cron 运行的是完整 Agent 任务，因此可以带 prompt、技能、上下文和投递目标"

- Add one orange design-tradeoff callout:
  - label: "设计代价"
  - annotation: "一旦进入定时调度，Hermes 就更像持续运行服务，失败重试、重复投递、调度漂移都会变成系统级问题"

- Add one bold judgment note near the center:
  - "这不是定时器，而是定时唤醒 Agent Runtime"

**Bottom Section (Interpretation Strip - 25%):**

- Create a horizontal 3-step interpretation strip:
  1. 到点触发
  2. 拉起完整 Agent 任务
  3. 像服务一样持续工作
- Under each step add one compact explanation:
  - 到点触发："不是等用户输入"
  - 拉起完整 Agent 任务："load job → fresh session → inject skills → run"
  - 像服务一样持续工作："结果可以自动投递到不同目的地"
- Add one conclusion sentence centered at bottom:
  "Cron Scheduler 让 Hermes 从会话助手走向持续运行系统，关键变化不是“定时”，而是“主动拉起完整运行时”"
- Add footer label:
  "Hermes Agent 对象拆解 / 11"

**What Must Be Clear in the Diagram:**

- Cron is not just a shell timer
- A scheduled task becomes a full Agent run with session, skills, prompt, and delivery
- The scheduler actively wakes the runtime instead of waiting for human chat input
- Delivery destinations are part of the design, not an afterthought
- The image must visually communicate this judgment:
  "这不是定时器，而是定时唤醒 Agent Runtime"

**Suitable Diagram Types to Combine:**

- Vertical scheduled-execution flow diagram
- Clock-trigger control node
- Structured job-definition side card
- Session/skills injection side callouts
- Multi-destination delivery fan-out
- Bottom interpretation timeline

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Pure white background
- Strong top-to-bottom operations flow
- Dense but readable runtime annotations
- Should feel like service orchestration infrastructure, not a calendar app page
- Composition ratio:
  - 50% detailed schematic illustration
  - 25% text labels and technical callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, scheduler body, stage frames, and labels
- Bright blue (#3498DB) for main flow arrows and activation pulses
- Green (#16A085) for successful execution and delivery branching
- Orange (#E67E22) for tradeoff callouts and operational risk emphasis
- Light gray for guide lines, helper boxes, and supporting structure
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep technical terms in English where appropriate: Cron Scheduler, scheduler tick, load job, fresh agent session, inject skills, run prompt, deliver result, Job Definition
- Title should be bold and visually strong
- Flow labels should be compact but mobile-readable

**Overall Feel:**

- Operational and service-like
- Clearly shows that Hermes can initiate work on its own schedule
- Makes scheduled automation feel like a runtime feature, not a side utility
- Easy to understand at a glance, but rich enough for technical readers
- Suitable for Xiaohongshu-style technical carousel

Style: Detailed technical hand-drawn infographic, scheduled Agent runtime activation flow, cron-driven autonomous execution and delivery system, pure white background
