# Harness Engineering 是什么：第 8 张“成本、延迟与恢复机制”文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "真正能上线的 Harness，一定同时考虑成本、速度和失败恢复". The image should make it immediately clear that a production-grade harness is not just about getting the best answer. It must also control runtime cost, bound latency, and recover from failure. This should feel like a "runtime run sheet / execution work order / task incident sheet" diagram, not a route metaphor or abstract control board.

**Design Concept:**

Use a "任务执行工单 / runtime incident sheet" metaphor:

- left side = one concrete task ticket
- center = this run's execution steps
- lower center = retry / fallback / handoff actions triggered by one failed step
- right side = final delivery status card
- bottom = run-level cost and latency summary

The key visual judgment is:

**成熟的 Harness 不是从不失败，而是失败时仍然可控、可恢复、可承受。**

The image should make viewers feel that system quality is defined not only by intelligence ceiling, but by the ability to keep cost bounded, latency acceptable, and failure recoverable. The reading order must be obvious at first glance:

- left = this task是什么
- middle = 这次运行经过了哪些步骤
- below = 失败后系统做了什么
- right = 最终以什么状态交付
- bottom = 这次运行的成本和耗时是不是可接受

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "真正能上线的 Harness，一定同时考虑成本、速度和失败恢复"
- Subtitle below: "强模型只是上限，模型路由、缓存和恢复边界决定下限"
- Small supporting sentence:
  "真实系统不可能每一步都用最贵模型，也不可能假装自己永远不会失败。真正能上线的系统，必须把成本、延迟和恢复路径一起设计进去"
- Typography should feel like a technical runbook or execution sheet, not a generic architecture poster

**Central Section (Hero Diagram - 58%):**

Create one dominant "runtime run sheet" composition with five explicit areas:

- Left task-ticket zone:
  - place one large task card on the left side labeled:
    - 任务工单
  - inside the task card show one concrete example:
    - "修复测试失败并提交结论"
  - include 4 compact requirement rows:
    - 要读项目文件
    - 要运行测试
    - 要检查失败原因
    - 要输出可交付结论
  - add one small note at the bottom of the ticket:
    - "这不是单轮回答，而是一条会消耗资源、可能失败、必须交付的运行任务"

- Center execution sheet zone:
  - place one horizontal row of 5 execution step cards across the middle
  - each step card should look like a concrete run record, not an abstract module
  - use these 5 step cards:
    - Step 1 - 理解任务
    - Step 2 - 选择模型
    - Step 3 - 调工具执行
    - Step 4 - 中间校验
    - Step 5 - 输出结论
  - inside each step card add 2 compact runtime tags:
    - 模型强度
    - 耗时 / 成本
  - example annotations:
    - 理解任务: 小模型 / 低成本
    - 选择模型: routing decision / 数十毫秒
    - 调工具执行: terminal + file / 成本低但耗时高
    - 中间校验: 强模型 / 成本升高
    - 输出结论: 结果封装 / 交付状态
  - this middle row should make it clear that different steps have different runtime profiles

- Lower incident-handling zone:
  - under the middle row, directly below one failed step card, create one incident handling panel
  - highlight the failed step in orange, for example on "调工具执行" or "中间校验"
  - show three concrete response boxes branching from that failed step:
    - bounded retry
    - fallback path
    - human takeover
  - each response box should have one short Chinese explanation:
    - bounded retry: 允许补救，但只试有限次
    - fallback path: 换更稳的路线，不再硬顶原方案
    - human takeover: 超出自动恢复边界，就交给人
  - one branch should visibly feed back into the next step
  - one branch should terminate at a safe stop state
  - this zone should look like an incident playbook attached to one specific failed step

- Right delivery-status zone:
  - place one structured delivery card on the right side
  - title:
    - 交付状态
  - include 4 outcome rows:
    - cost controlled
    - latency bounded
    - recovery available
    - result delivered
  - also include one compact status summary:
    - 成功交付 / 降级交付 / 人工接管
  - this card should feel like the end-state of this run, not an abstract slogan

- Bottom run-metrics zone:
  - create one bottom strip labeled:
    - 本次运行摘要
  - include 5 compact metric cards:
    - total cost
    - total latency
    - retry count
    - cache reuse
    - fallback used
  - each metric card should have one small Chinese cue:
    - total cost: 总成本是否可接受
    - total latency: 总耗时是否还可用
    - retry count: 有没有失控重试
    - cache reuse: 有没有避免重复计算
    - fallback used: 有没有走降级路线

- Engineering contrast:
  - add one orange callout near the failed-step incident zone:
    - "坏系统的常见问题：每一步都上最强模型，失败就盲目重试，最后又慢又贵还不稳定"
  - add one teal callout near the delivery-status card:
    - "成熟系统的目标：stable / affordable / fast enough"

**Bottom Interpretation Layer (integrated if space is tight):**

If there is enough space, add a very compact interpretation sequence below the run-metrics strip:

1. "任务进入"
2. "逐步运行"
3. "某步失败"
4. "按策略处理"
5. "受控交付"

- Add one final conclusion sentence:
  "Harness 最像系统工程的地方，不是让模型更会想，而是让系统在现实约束里依然跑得下去"
- Add footer label:
  "Harness Engineering / 08"

**What Must Be Clear in the Diagram:**

- The image is about a real run record, not pure model capability
- Different steps must visibly have different resource intensities
- Failure must appear as one concrete failed step with attached handling options
- Recovery must be shown as a practical incident response, not random improvisation
- The viewer should immediately understand:
  - strongest model everywhere is not the goal
  - bounded retry is not blind retry
  - a production system needs cost, latency, and recovery constraints together

**Suitable Diagram Types to Combine:**

- Runtime task ticket
- Execution step cards
- Incident handling branch panel
- Delivery status card
- Bottom run-metrics strip
- Compact interpretation sequence

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Professional engineering documentation style
- White background with strong work-order organization
- Dense annotations but explicit run logic
- More like a runtime execution sheet than a route-planning board
- Composition ratio:
  - 50% detailed schematic illustration
  - 25% labels and operations callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, titles, and work-sheet frames
- Bright blue (#3498DB) for execution arrows, step connectors, and run annotations
- Teal (#16A085) for stable delivery, successful recovery, and acceptable run state
- Orange (#E67E22) for failed steps, retry danger, and expensive/slow warnings
- Light gray for helper guides, secondary boxes, and passive system panels
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep only these technical terms in English where appropriate: model routing, caching, bounded retry, fallback path, cost controlled, latency bounded, recovery available
- Title should be bold and large
- Secondary labels should be compact but readable on mobile

**Overall Feel:**

- Clear and highly readable at a glance
- Technical and operational rather than abstract
- Makes the difference between "能跑一次" and "能上线运行" visually unforgettable
- Immediately communicates that the final layer of harness engineering is not pure intelligence, but one run can stay within cost, latency, and recovery boundaries
- Suitable for Xiaohongshu-style knowledge carousel final slide

Style: Detailed technical hand-drawn infographic, runtime execution work order with task ticket, step-by-step run cards, incident handling panel, delivery status card, and run summary strip, pure white background
