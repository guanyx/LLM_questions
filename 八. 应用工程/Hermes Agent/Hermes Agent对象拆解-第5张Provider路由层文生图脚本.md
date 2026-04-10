# Hermes Agent对象拆解：第 5 张Provider路由层文生图脚本

Create a highly detailed technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "Hermes 怎么决定这次该用哪个模型？".

**Design Concept:**
Use a concrete model-selection journey metaphor instead of a static routing matrix: the image should follow one request as it leaves Hermes Runtime, passes through provider parsing and API-mode selection, chooses one model path based on capability/cost, and then returns a result. The image should communicate that models are replaceable, APIs are heterogeneous, and the routing layer is what keeps the upper runtime stable.

**Layout Structure:**

**Top Section (Title Area - 20%):**

- Main title in bold, large font: "Hermes 怎么决定这次该用哪个模型？"
- Subtitle below: "模型是会换的，路由层才是稳定的"
- Small supporting sentence: "Hermes 不把自己绑死在一个模型 API 上，而是把 provider、凭证、API 形态和成本选择都吸收到运行时中间层"
- Typography should feel like a technical system blueprint, not a product comparison poster

**Central Section (Hero Diagram - 55%):**
Create a left-to-right concrete model-selection journey with one main chosen path and several alternative provider paths:

- Build one thick main path across the center:
  - Hermes Runtime 发起请求
  - Provider Router 解析 provider
  - 选择 API mode
  - 判断能力 / 成本
  - 走向一个具体模型端点
  - 返回结果

- Stage 1 - Hermes Runtime
  - on the far left place one stable runtime box
  - inside show 3 compact internal labels:
    - 任务需求
    - 能力判断
    - 调用请求
  - add a tiny example:
    - "这次要代码能力，还是普通对话能力？"
  - note:
    - "核心稳定，不直接绑定单一模型接口"

- Stage 2 - Provider Router
  - place one routing process box after Hermes Runtime
  - inside split into 4 smaller cells:
    - provider 解析
    - credentials 管理
    - API mode 选择
    - cost / capability 匹配
  - this should read as one具体选择过程，而不是抽象总控矩阵

- Stage 3 - 选择条件
  - place one thin decision strip above or below the router
  - labels:
    - 任务复杂度
    - 模型能力
    - 成本约束
  - connect this strip into the router as decision input

- Stage 4 - 候选模型路径
  - on the right side place 5 candidate endpoint tiles, but do not give them equal visual weight
  - highlight one main chosen path, keep the others as alternative branches:
    - OpenAI-compatible Chat
    - Responses / Codex
    - Anthropic Messages
    - OpenRouter / 聚合 provider
    - Custom Endpoint

- For the chosen path, show a thick arrow with tiny edge labels:
  - API mode
  - credentials
  - fallback
  - make this the visible “本次真正走的路”

- For the unchosen paths, use lighter dashed branches to show they are alternatives, not simultaneous main routes

- Add one green fast-path line as a side branch:
  - label: "cheap route"
  - annotation: "简单请求优先走更便宜路径"
  - make it feel like a special-case shortcut, not another full architecture lane

- Add one result-return box after the chosen endpoint:
  - label: "结果返回 Hermes Runtime"
  - annotation: "上层逻辑不需要理解底层 provider 差异"

- Add one green design-strength callout:
  - label: "设计亮点"
  - annotation: "provider、凭证、API 形态和成本判断都被 runtime 中间层吸收，上层任务逻辑因此保持稳定"

- Add one orange design-tradeoff callout:
  - label: "设计代价"
  - annotation: "provider 解析、凭证池、API 形态判断分散在多层运行时里，排查链路更绕"

- Add one bold judgment note below the main path:
  - "路由层真正做的不是“换模型”，而是“帮一次请求走对路”"

**Bottom Section (Interpretation Strip - 25%):**

- Create a horizontal 3-step interpretation strip:
  1. 模型可替换
  2. 路由层吸收差异
  3. 上层运行时保持稳定
- Under each step add one compact explanation:
  - 模型可替换："provider 和接口不是写死的"
  - 路由层吸收差异："chat / responses / messages 都在这里被统一"
  - 上层运行时保持稳定："任务逻辑不跟着模型 API 一起重写"
- Add one conclusion sentence centered at bottom:
  "Provider 路由层真正的价值，不是帮 Hermes 换模型，而是帮 Hermes 隔离模型差异"
- Add footer label:
  "Hermes Agent 对象拆解 / 05"

**What Must Be Clear in the Diagram:**

- Hermes runtime itself is not the provider-specific layer
- The Provider Router is the translation and decision layer
- Different API shapes coexist behind the routing layer
- One concrete request should visibly choose one path, while other provider paths remain alternatives
- Cheap route / cost-aware routing is part of the design
- The image must visually communicate this judgment:
  "路由层的价值不是换模型，而是帮一次请求走对路"

**Suitable Diagram Types to Combine:**

- Concrete model-selection journey
- Routing process box
- Candidate provider path branches
- Chosen-path emphasis
- Cost-aware fast path callout
- Protocol label overlays on edges
- Bottom interpretation timeline

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Pure white background
- Strong left-to-right story flow
- Rich but compact engineering annotations
- Should feel like protocol routing infrastructure, not like a model leaderboard poster
- Composition ratio:
  - 50% detailed schematic illustration
  - 25% text labels and technical callouts
  - 25% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for outlines, labels, frames, and router body
- Bright blue (#3498DB) for main routing lines
- Green (#16A085) for cheap route and successful optimized routing
- Orange (#E67E22) for complexity/tradeoff callouts and fallback emphasis
- Light gray for protocol helpers and secondary construction lines
- Pure white background

**Typography:**

- All annotations in simplified Chinese
- Keep technical terms in English where appropriate: Provider Router, API mode, credentials, fallback, cheap route, OpenAI-compatible Chat, Responses, Codex, Anthropic Messages, Custom Endpoint
- Title should be bold and prominent
- Edge labels should be compact but still mobile-readable

**Overall Feel:**

- Stable on the left, chosen path in the middle, alternatives on the right
- Technical and operational rather than abstract
- Immediately readable as a request-routing journey
- Strong sense of system mediation and protocol normalization
- Suitable for Xiaohongshu-style technical carousel

Style: Detailed technical hand-drawn infographic, concrete provider-selection journey, one chosen model path among multiple normalized endpoints, pure white background
