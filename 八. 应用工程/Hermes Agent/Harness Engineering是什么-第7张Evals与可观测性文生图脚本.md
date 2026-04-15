# Harness Engineering 是什么：第 7 张“Evals 与可观测性”文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "没有评测的 Agent，几乎等于不可维护". The image should make it immediately clear that an Agent is not one output, but a chain of steps that must be observed, replayed, attributed, and evaluated. This should feel like a "flight recorder / replay console / failure attribution desk" diagram, not another generic process flow.

**Design Concept:**

Use a "飞行记录台 / replay console" metaphor:

- top = task trajectory
- middle = replay and observation windows
- right side = failure attribution board
- bottom = metrics and eval strip

The key visual judgment is:

**Harness 最容易被低估的一层，是让系统失败时仍然能被看见、被定位、被复现。**

The image should make viewers feel that without evals and observability, an Agent is almost impossible to maintain. It is not enough to know the final answer was wrong. You need to know which step went wrong, why it went wrong, and whether the failure can be reproduced. The reading order must be obvious at first glance:

- top = what happened
- middle = what each step looked like
- right = where the fault belongs
- bottom = what the system metrics say

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "没有评测的 Agent，几乎等于不可维护"
- Subtitle below: "你必须知道它错在哪一步，而不只是知道它“这次没做好”"
- Small supporting sentence:
  "Agent 不是一次输出，而是一串过程。只看最终结果，你只知道它失败了；看见轨迹，你才能知道它为什么失败"
- Typography should feel like a technical incident-analysis board, not a business dashboard poster

**Central Section (Hero Diagram - 58%):**

Create one dominant "task replay console" composition with four explicit areas:

- Top zone - 任务轨迹带:
  - place one horizontal task trajectory strip across the upper middle of the image
  - split it into 5 step nodes:
    - input
    - context assembly
    - tool call
    - model decision
    - output
  - connect them with a clean main path arrow
  - highlight one step in orange as the problematic step
  - add one small label above the strip:
    - "Task Trace"
  - this top strip should feel like the master flight path of one task run

- Middle zone - 回放与观测窗口:
  - directly under the task trajectory, place 4 or 5 compact replay windows aligned with the top nodes
  - each replay window should show a different observation surface:
    - input window: 请求内容 / 约束 / 用户目标
    - context window: 注入了哪些上下文 / 哪些被压缩
    - tool log window: 调了什么工具 / 参数 / 返回结果
    - decision window: 模型选择了哪条路径 / 为什么继续
    - output window: 最终产出 / 收敛状态
  - these windows should feel like small forensic panels, not simple labels
  - add one small note near the middle:
    - "只看终点不够，必须能把中间过程逐步回放出来"

- Right-side zone - 失败归因板:
  - create one separate vertical analysis board on the right side
  - title:
    - "Failure Attribution"
  - split it into 4 diagnosis rows:
    - planning error
    - context error
    - tool error
    - recovery error
  - each row should have one short Chinese explanation:
    - planning error: 任务拆分和路径判断出了问题
    - context error: 喂错了上下文，或丢了关键条件
    - tool error: 外部调用失败，或返回未被正确处理
    - recovery error: 明明已经失败，却没有被正确拉回
  - one row should be visually highlighted to show the diagnosed source of failure
  - add one side note:
    - "失败不是一个模糊状态，而是可以被归因的过程问题"

- Bottom zone - 指标与评测条:
  - create a compact bottom instrumentation strip
  - include 6 metric modules:
    - trace
    - replay
    - tool logs
    - latency
    - cost
    - step-level eval
  - each metric module should have a tiny Chinese cue:
    - trace: 任务完整轨迹
    - replay: 能否重放当时路径
    - tool logs: 外部调用细节
    - latency: 每步耗时
    - cost: 每步成本
    - step-level eval: 每步是否达标
  - this bottom strip should feel like instrumentation, not decoration

- Core contrast emphasis:
  - add one orange callout near the top or left side:
    - "只看最终结果：你只能知道它错了"
  - add one teal callout near the replay windows or attribution board:
    - "看见过程：你才能知道它为什么错、错在哪一步、能不能复现"

**Bottom Interpretation Layer (integrated into lower strip if space is tight):**

If there is enough space, add a very compact interpretation sequence under the metric strip:

1. "记录过程"
2. "逐步回放"
3. "定位错误"
4. "做 step-level eval"

- Add one final conclusion sentence:
  "Evals 与可观测性不是上线后的装饰，而是 Harness 让系统可调、可复现、可维护的核心层"
- Add footer label:
  "Harness Engineering / 07"

**What Must Be Clear in the Diagram:**

- The image is about process visibility, not final-output beauty
- The task is shown as a trajectory, not a single answer bubble
- Replay windows must visibly correspond to steps on the trajectory
- Failure attribution must be a separate analytical object, not just a warning box
- The viewer should immediately understand:
  - result-only view is insufficient
  - process visibility is required
  - step-level evaluation is part of the system, not an afterthought

**Suitable Diagram Types to Combine:**

- Flight-recorder style task trajectory
- Replay console windows
- Failure attribution board
- Bottom instrumentation strip
- Compact interpretation sequence

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Professional engineering documentation style
- White background with strong panel organization
- Dense annotations but explicit investigative structure
- More like an incident replay console than a monitoring dashboard
- Composition ratio:
  - 50% detailed schematic illustration
  - 25% labels and analysis callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, titles, and analysis frames
- Bright blue (#3498DB) for trace lines, replay connectors, and system structure
- Teal (#16A085) for observability gains, successful traceability, and evaluable steps
- Orange (#E67E22) for failure highlights, problematic steps, and diagnostic emphasis
- Light gray for helper panels, inactive windows, and supporting guides
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep only these technical terms in English where appropriate: Task Trace, replay, Failure Attribution, planning error, context error, tool error, recovery error, trace, tool logs, latency, cost, step-level eval
- Title should be bold and large
- Secondary labels should be compact but readable on mobile

**Overall Feel:**

- Clear and highly readable at a glance
- Technical and analytical rather than abstract
- Makes the difference between "只看结果" and "看见过程" visually unforgettable
- Immediately communicates that evals and observability are the maintenance layer of a serious agent system
- Suitable for Xiaohongshu-style knowledge carousel seventh slide

Style: Detailed technical hand-drawn infographic, task replay console with flight-recorder trajectory, replay windows, failure attribution board, and instrumentation strip, pure white background
