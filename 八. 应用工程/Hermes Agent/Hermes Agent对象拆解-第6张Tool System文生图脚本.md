# Hermes Agent对象拆解：第 6 张Tool System文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "Hermes 是怎么从“会说”变成“会做”的？".

**Design Concept:**
Use a concrete tool-call journey metaphor instead of a static capability bus: the image should follow one tool invocation from “模型想做事” all the way to “工具真的执行并把结果回填回来”. The key message is that Hermes tools are not random add-ons. They pass through a governed call chain with registration, filtering, dispatch, and standardized result return.

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "Hermes 是怎么从“会说”变成“会做”的？"
- Subtitle below: "工具系统决定 Agent 能不能落地执行，而不只是生成一段看起来很聪明的话"
- Small supporting sentence: "Hermes 的工具不是零散外挂，而是统一注册表里的能力，由同一条执行总线收口、过滤、分发"
- Typography should feel like a technical architecture poster, not a product feature sheet

**Central Section (Hero Diagram - 55%):**
Create a left-to-right concrete tool-call journey diagram with one main example and one capability map:

- Build one thick horizontal main path across the center:
  - AIAgent 生成 tool call
  - Tool Registry 查定义
  - check_fn / toolset 过滤
  - dispatch 到具体工具
  - 工具执行
  - 结果标准化
  - 回填给 AIAgent

- Stage 1 - AIAgent / Model Output
  - place one example call card on the far left
  - show a tiny example intent:
    - "请帮我搜索官网并读取文件"
  - annotation: "模型产生 tool call 意图"

- Stage 2 - Tool Registry
  - place one dominant registry box
  - inside show 4 compact labels:
    - schema 收集
    - handler 映射
    - toolset 管理
    - dispatch 准备
  - this should feel like a registry desk or control柜，不是大总线

- Stage 3 - 可用性过滤
  - place one thin checkpoint box after Tool Registry
  - label:
    - check_fn
    - availability
    - toolset
  - annotation: "先决定哪些工具现在可以被暴露和执行"

- Stage 4 - 具体工具执行
  - place 4 larger example tool tiles as the main execution destinations:
    - Web
    - File
    - Terminal
    - Memory
  - one of them can be highlighted as the main example execution branch
  - annotation for each:
    - Web："联网查询 / 页面获取"
    - File："读写文件 / 代码修改"
    - Terminal："命令执行 / 环境交互"
    - Memory："写记忆 / 读记忆"

- Under the 4 main tiles, place 5 smaller auxiliary capability tabs:
  - Browser
  - Todo
  - Delegate
  - Cronjob
  - MCP
  - these should read as “同类能力家族”，而不是主视觉中心

- Stage 5 - 统一结果包装
  - place one result-normalization box after the selected execution tile(s)
  - annotation:
    - 标准结果
    - 错误包装
    - 回填消息

- Stage 6 - 返回 AIAgent
  - place one return arrow and one compact output box on the far right
  - annotation: "把执行结果重新送回主循环"

- Add two category labels beneath the execution area:
  - 改外部世界
    - connect to Web / Terminal / File / Browser / MCP
  - 改 Agent 自己
    - connect to Memory / Todo / Delegate / Cronjob

- Add one green design-strength callout near Tool Registry:
  - label: "设计亮点"
  - annotation: "工具不是零散外挂，而是统一注册、过滤、分发、回填的一套调用链"

- Add one orange design-tradeoff callout near the execution area:
  - label: "设计代价"
  - annotation: "统一治理更稳定，但工具越多，Tool System 越像能力管理层，而不只是调用层"

- Add one caution note:
  - label: "模块导入即注册"
  - annotation: "运行时方便，但对读代码的人不够显式"

- Add one bold judgment note below the main path:
  - "Tool System 不是工具列表，而是一条工具调用旅程"

**Bottom Section (Interpretation Strip - 25%):**

- Create a horizontal 3-step interpretation strip:
  1. 工具不是外挂
  2. 工具被统一治理
  3. Agent 因此真的能执行
- Under each step add one compact explanation:
  - 工具不是外挂："不是零散函数集合"
  - 工具被统一治理："schema / filter / dispatch / result 都由总线收口"
  - Agent 因此真的能执行："从生成动作意图变成真实世界操作"
- Add one conclusion sentence centered at bottom:
  "Tool System 的本质不是工具列表，而是一条把能力注册、过滤、分发、回填串起来的执行总线"
- Add footer label:
  "Hermes Agent 对象拆解 / 06"

**What Must Be Clear in the Diagram:**

- Tool System is not a gallery of tools
- Tool Registry is the control center of capability governance
- One tool call should visibly travel through register → filter → dispatch → execute → return
- Some tools change the outside world, while some change the Agent itself
- The image must visually communicate this judgment:
  "Tool System 不是工具列表，而是一条工具调用旅程"

**Suitable Diagram Types to Combine:**

- Concrete tool-call journey flow
- Registry control box
- Availability/filter checkpoint
- Execution destination tiles
- Result return flow arrows
- Capability category zoning
- Bottom interpretation timeline

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Pure white background
- Strong left-to-right reading path
- Dense but readable annotations
- Should feel like system infrastructure, not like an app icon board
- Composition ratio:
  - 50% detailed schematic illustration
  - 25% text labels and technical callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, registry bus, and labels
- Bright blue (#3498DB) for main capability flow arrows
- Green (#16A085) for memory / internal-state-changing tools
- Orange (#E67E22) for tradeoff callouts and governance emphasis
- Light gray for helper structures and category zones
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep technical terms in English where appropriate: Tool Registry, schema, check_fn, toolset, availability, dispatch, Web, Terminal, File, Browser, Memory, Todo, Delegate, Cronjob, MCP
- Title should be bold and prominent
- Card annotations should remain compact but mobile-readable

**Overall Feel:**

- Operational and system-like
- Clear sense of “tool invocation lifecycle”
- More concrete and narrative than a static registry map
- Easy to grasp at a glance, but rich enough to reward close reading
- Suitable for Xiaohongshu-style technical carousel

Style: Detailed technical hand-drawn infographic, concrete tool-call journey, governed registry-to-dispatch-to-result workflow, pure white background
