# 处理线上故障时 work 和 persona 协同工作的文生图提示词

Create a highly detailed technical infographic in hand-drawn sketch style on pure white background. The theme is "How work.md and persona.md collaborate during incident response".

Use a single clear narrative: a completed collaboration architecture is opened layer by layer, showing how `persona.md` and `work.md` cooperate during incident response. The image should explain the internal collaboration structure, not the source material or distillation process.

**Main design concept:**
Use a "three-stage collaboration architecture" metaphor:

- Center = a large collaboration blueprint as the hero visual
- Left or top = `persona.md` as entry strategy and interaction control
- Center or middle = `work.md` as execution and troubleshooting engine
- Right or bottom = final response rendering controlled again by `persona.md`

The visual emphasis should be on handoff, sequencing, and recombination during a real incident. Do not re-explain the internal structure of `work.md` or `persona.md`; those are covered in other diagrams.

**Layout structure:**

Vertical or centered infographic with 4 major sections, connected by strong directional arrows.
Image-to-text ratio should be approximately 60% diagrams / 20% text / 20% whitespace.
Keep enough blank white space between modules so the image has breathing room.

**Title area (top, 15-20%):**

- Main title in medium-large bold font:
  "线上故障来了，work.md 和 persona.md 怎么一起工作"
- Subtitle below in smaller font:
  "人格定入口，能力做执行，再回到人格包输出"
- Small side annotation:
  "重点：只解释协同结构，不展开前置来源"

【一：协同运行时序 - 一次任务如何在三段之间流动】

- Center hero visual should be a large collaboration blueprint card
- The blueprint should be divided into three major stages:
  · 阶段一：Persona 定义入口
  · 阶段二：Work 执行排障
  · 阶段三：Persona 包装输出
- Add a small annotation:
  · "这不是两份文档并列展示"
  · "这是一次任务在运行时的三段式编排"
- Suggested diagram elements:
  · large architecture blueprint
  · three connected stage blocks
  · stage dividers
  · main directional arrows
- Arrow label:
  · "同一个任务，按顺序经过三段处理"

【二：阶段之间传递什么 - 协同不是并排，而是接力】

- Show three handoff cards between the stages:
  · 输入任务：告警 / 问题 / 初始上下文
  · 中间结果：排查路径 / 诊断判断 / 处置建议
  · 最终响应：像这个人说出来的结论
- For each stage, show only what it receives and what it passes forward:
  · Persona 入口：接收任务 → 产出提问方向和进入姿态
  · Work 执行：接收上下文 → 产出诊断判断和建议动作
  · Persona 输出：接收判断结果 → 产出风格化回应
- Add a side note:
  · "重点不是谁更重要"
  · "重点是上一段产出的结果，决定下一段能做什么"
- Suggested diagram elements:
  · handoff cards between stages
  · input/output arrows on each stage block
  · small payload labels on arrows
  · relay-baton metaphor or packet handoff boxes
- Arrow label:
  · "每一段都在消费上一段的结果"

【三：协同如何改变故障处理过程 - 不是多一步，而是换了组织方式】

- Show a compact incident-response action chain in the center:
  · 先问变更 / 影响面
  · 再看监控 / 发布记录
  · 缩小异常范围
  · 定位链路和依赖
  · 形成处置建议
- Add mapping arrows from the collaboration stages to these actions:
  · Persona 入口 → 先问变更 / 影响面
  · Work 执行 → 看监控 / 查发布 / 定位链路 / 形成建议
  · Persona 输出 → 把判断说得像这个人
- Add compact structured note cards:
  · "先问最近是否发版"
  · "异常集中在支付回调链路"
  · "建议先回滚并观察"
- Add a small annotation:
  · "协同并不增加步骤数量"
  · "它改变的是步骤的组织方式和表达方式"
- Suggested diagram elements:
  · action chain
  · mapping arrows
  · mini monitoring panel
  · deploy timeline
  · output suggestion cards
- Arrow label:
  · "协同结构最终都要落成真实动作"

【四：最终效果只看一件事 - 同样的判断，为什么更像真人协作】

- Right side should show final response rendering as the result of collaboration
- Use a split comparison visual:
  · Left small card: 纯 Work 输出
  · Right larger card: Work + Persona 输出
- Pure Work output card can be concise and neutral:
  · "先看监控，再查最近发布，异常主要集中在支付回调链路，建议先回滚并观察"
- Work + Persona output card should feel like a real colleague speaking:
  · "先别乱猜，最近是不是刚发过版？影响面先拉齐。现在看起来异常集中在支付回调链路，下游超时把错误率带上来了。先回滚，别硬顶。"
- Add arrows from different stages to different parts of the response:
  · Persona 入口 → 开场怎么问
  · Work 执行 → 中间判断和建议
  · Persona 输出 → 最终语气和表达方式
- Add a small annotation block:
  · "work 决定内容正确"
  · "persona 决定表达像本人"
- Show a final stamped output badge:
  · "像这个人处理出来的故障响应"
- Suggested diagram elements:
  · side-by-side response cards
  · stage-to-response mapping lines
  · style transformation arrow
  · final delivery panel
- Arrow label:
  · "人格包输出，能力保正确"

**Supporting mini-diagrams to reduce text density:**

- Central collaboration blueprint with 3 major stages
- Stage handoff cards showing payload transfer
- Compact incident action chain
- Mini monitoring + deploy timeline cards
- Before/after response comparison cards

These diagrams should do most of the explanatory work, so the annotations stay concise.

**Key annotations to keep in Chinese:**

- "人格定入口"
- "能力做执行"
- "人格包输出"
- "先问变更"
- "先看监控"
- "定位链路"
- "形成建议"
- "三段式编排"
- "接力式协同"

**Visual style:**

- Technical hand-drawn sketch aesthetic
- Engineering blueprint feel, but centered on collaboration architecture rather than detailed source flow
- Clear three-stage composition: entry strategy, execution engine, response rendering
- Use leader lines, arrows, and subtle dotted guides to connect concepts
- Diagrams should be more important than text
- Avoid huge blocks of prose

**Color palette:**

- Navy blue (#2C3E50) for main structure and labels
- Teal (#16A085) for collaboration arrows and layer highlights
- Soft orange (#E67E22) for incident alerts and critical attention points
- Light gray for secondary boxes and scaffolding
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Title bold and slightly larger
- Module titles medium weight
- Small dense annotation text, but not overcrowded
- Technical terms allowed in English: Persona, Work, incident, deploy, rollback

**Overall feel:**

- Professional, clear, and engineering-oriented
- Easy to understand at a glance
- Strong sense of process and role division
- More like a production-grade agent runtime collaboration diagram than a scenario poster
- Preserve whitespace so the final image feels breathable and not cramped

Style: Technical hand-drawn workflow infographic, runtime-collaboration diagram, incident-response-centered, white-background engineering sketch
