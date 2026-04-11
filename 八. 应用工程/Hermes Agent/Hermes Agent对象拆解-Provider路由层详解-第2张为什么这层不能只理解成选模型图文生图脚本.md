# Hermes Agent对象拆解：Provider路由层详解第2张四类运行时对象图文生图脚本

Create a dense technical infographic for social media in hand-drawn sketch style on pure white background. The theme is "Provider 不是一个字符串，而是四类运行时对象".

**Design Concept:**
Do not repeat the cover judgment. Move straight into structure. This page should look like an object decomposition sheet for the routing layer. The point is simple: Hermes 没把 provider 当成一个名字一路传。它把这件事拆成几种不同的运行时对象。图里要把这四类对象讲实，不要讲虚。让读者一眼看到：名字只是入口，真正发请求的是后面那套绑定结果。

**Layout Structure:**

**Top Section (Title Area - 18%):**

- Main title in bold, large font: "Provider 不是一个字符串"
- Subtitle below: "Hermes 把它拆成 4 类运行时对象"
- Small lead sentence under subtitle: "入口可以写 openai。真正发请求的，不会只是 openai 这 6 个字母。"
- Typography should feel like a technical breakdown page, direct and dense

**Central Section (Object Decomposition Diagram - 64%):**
Create a left-to-right object decomposition pipeline with four large object blocks:

- Start with one narrow input block on the far left:
  - label: "入口字符串 / 用户输入"
  - examples:
    - openai
    - claude
    - OpenRouter
    - custom
  - add a small note:
    - "这里只是入口，不是最终运行时对象"

- Then build 4 dominant object blocks across the center:

- Block 1 - Provider Identity
  - title: "1. Provider Identity"
  - purpose label:
    - "先认人"
  - show inside this block:
    - alias
    - historical name
    - family mapping
    - canonical provider name
  - add small example pairs:
    - claude → anthropic 语义
    - glm / z.ai / 智谱 → 同一 provider family
  - side annotation:
    - "名字不先归一，缓存、计费、监控、重试都会歪"

- Block 2 - ProviderDef
  - title: "2. ProviderDef"
  - purpose label:
    - "再看这家平时长什么样"
  - draw this block as a stacked map-like structure with 3 layers:
    - base metadata
    - overlay
    - user config
  - add small technical labels on the layers:
    - model catalog
    - endpoint defaults
    - local rule patch
    - user override
  - side annotation:
    - "这不是一次请求。它更像 provider 的静态定义。"

- Block 3 - Runtime Provider
  - title: "3. Runtime Provider"
  - purpose label:
    - "这次到底怎么连"
  - make this the heaviest block in the page
  - show inside this block:
    - base_url
    - api_key
    - auth_type
    - credential pool
    - API mode
    - chosen endpoint
  - add one compact bundle label:
    - "request-time binding"
  - add side note:
    - "真正发请求的是它，不是 provider 名字"

- Block 4 - Recovery Policy
  - title: "4. Recovery Policy"
  - purpose label:
    - "出错以后怎么救"
  - show a small layered ladder inside:
    - provider 内自救
    - rotate key
    - provider fallback
    - return to primary
  - add tiny error tags next to the ladder:
    - 401
    - 429
    - 402
  - side annotation:
    - "不是一个备用开关，是一套分层恢复策略"

- Connect the 4 blocks with one thick main path:
  - 输入名字
  - 归一身份
  - 读取定义
  - 生成 runtime binding
  - 挂上 recovery policy

- Add one compact lower strip under the 4 blocks:
  - label: "上层真正拿到的东西"
  - show one final boxed result:
    - "可执行的 runtime provider object"
  - connect this final result to:
    - Agent Loop
    - Tool System
    - Gateway
  - add one note:
    - "上层接的不是零碎字段，而是一个能直接工作的对象"

- Add two strong judgment callouts:
  - "Provider 字符串只适合当入口"
  - "运行时对象才适合真的发请求"

**Bottom Section (Reading Strip - 18%):**
Show a compact 4-step strip:

1. "Identity" - 先把名字讲清楚
2. "Def" - 再把静态定义讲清楚
3. "Runtime" - 再把这次请求绑实
4. "Recovery" - 最后把故障处理挂上

- Under the strip add one centered sentence:
  - "Provider 路由层不是在传字符串，它在组装对象。"
- Add small footer label:
  - "Hermes Agent 对象拆解 / Provider Routing / 02"

**Key Visual Elements:**

- One thin input string block on the far left
- Four dominant runtime object blocks in the center
- ProviderDef rendered as layered static definition
- Runtime Provider rendered as bound request object
- Recovery Policy rendered as a fault ladder
- One final executable object handed to upper runtime modules

**Visual Style:**

- Hand-drawn technical sketch aesthetic
- Object-decomposition sheet, not concept poster
- White background with strong hierarchy and dense labels
- Use leader lines, stacked cards, binding bundles, and fault ladders
- Visual flow should be input string → four object layers → executable runtime object
- 60% diagram illustration, 18% text labels, 22% whitespace

**Color Palette:**

- Deep navy (#2C3E50) for frames, text, and object boundaries
- Bright blue (#3498DB) for main path, binding arrows, and runtime handoff
- Green (#16A085) for final executable runtime object and stable upper-runtime handoff
- Orange (#E67E22) for recovery ladder and error tags
- Light gray for internal helper labels and construction lines
- Pure white background

**Typography:**

- All major annotations in simplified Chinese
- Keep these technical terms in English where appropriate: Provider Identity, ProviderDef, Runtime Provider, Recovery Policy, base_url, api_key, auth_type, credential pool, API mode
- Title should be bold and direct
- Labels should read like runtime notes, not slogans
- Small technical text should stay dense but clear

**Overall Feel:**

- Hard and structural
- More like a runtime teardown page
- Not introductory anymore
- Should make the reader feel the abstraction boundary suddenly变具体
- Suitable for Xiaohongshu-style technical carousel page 2

Style: Dense technical hand-drawn object-decomposition infographic, four runtime object blocks, strong left-to-right assembly flow, compact engineering annotations, pure white background
