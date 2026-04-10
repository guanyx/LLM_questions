Create a highly detailed infographic with explanatory diagrams, accurate visual semantics, and Chinese labels where text appears inside the image:

**Title (top):**
"Prefix cache 和 冷 KV 下放"

**Subtitle (Optional):**
"Prefix cache 是少做重复计算，冷 KV 下放是先把东西放下。这两招，不是在解决同一个问题。"

**Main Content - Detailed sections:**
*Create one section for EACH optimization path in the source text. Keep one continuous mini-case across the full page: the same DeepSeek-R1-Distill-Llama-70B handles the same long strip labeled “128K token 上下文”, and the same long document plus repeated user follow-up questions appear across all sections so the viewer can track how Prefix cache and cold-KV offloading cut different parts of the cost.*
*For each section, keep only 1 mandatory text block plus 2 non-redundant visual dimensions. Prefer larger labels and fewer micro-callouts over maximum detail density.*

**Section 1: Prefix cache 省的是重复 prefill**
- **Mandatory Text Block**: "它省的不是整段长上下文本身，而是别把同一段前缀一遍遍重算。"
- Show one multi-turn timeline titled "同一份长材料反复追问": first panel "第 1 轮" shows a long prefix strip labeled "120,000 token 旧前缀" plus a short tail labeled "11,072 token 新内容", and a big arrow to a cache cabinet labeled "前缀 KV 已算好"; second panel "下一轮" reuses the same prefix cabinet in gray-blue with a bold stamp "直接复用", while only the short new tail is highlighted in orange and sent into compute.
- Include technical/details: add one compact savings board titled "这笔重复账怎么省", showing two paths side by side: "整段重算：4.05 × 10^16 FLOPs" versus "只算新增：5.16 × 10^15 FLOPs", ending in one large green badge "约省 7.8×"; place one short note below "不是把模型压小了，是把旧前缀直接接着用".

**Section 2: Prefix cache 真正在工程里要做什么**
- **Mandatory Text Block**: "难点不是“有缓存”，难点是让它真命中、该失效时就失效。"
- Show ... step by step: draw one engineering chain titled "Prefix cache 实际怎么跑", with four large nodes "第 1 次正常 prefill" → "把前缀 KV 建出来" → "下一轮先看前缀是不是一模一样" → "一样就跳过旧前缀，只算新增"; attach one side branch in red labeled "中间改 1 个 token → 后面 cache 失效".
- Error/Consequence Mode: add one checklist board titled "这条路的坑", with four large checklist cards only: "只对前缀不变有效", "首轮显存一点也不会变小", "cache 生命周期更难管", "prompt 拼接不稳，命中率就会掉"; add one small side note "多租户不是所有 cache 都能共用".

**Section 3: 冷 KV 下放先解决“放不下”**
- **Mandatory Text Block**: "这条路先解决“放不下”，不是先解决“跑得便宜”。"
- Detailed diagram of one tiered storage system titled "KV 分层放", with top layer labeled "HBM：热 KV", middle layer labeled "CPU 内存：温 KV", bottom layer labeled "NVMe / 更慢层：冷 KV"; show the same long history strip aging over time and flowing downward from top to bottom, while one highlighted current decode token on the right keeps requesting old history.
- Comparative Visual: add one simple tradeoff scale titled "它换来了什么", with the left side labeled "先放下" and one large tag "HBM 压力更小", and the right side labeled "会变慢" with three large tags "延迟更高", "带宽更差", "调度更复杂"; make the right side visually heavier in orange-red.

**Section 4: decode 时为什么还会卡住**
- **Mandatory Text Block**: "理论上放下了，不等于跑起来就顺。热点猜错了，每一步都可能卡在等数据。"
- Show ... step by step: add one request path titled "decode 时到底在干嘛", with four large nodes in sequence "先猜这一步最可能会读哪些 KV" → "尽量提前搬回更快层" → "GPU 开始算当前 token" → "边算边等剩下的数据回来"; place one red consequence badge at the end "猜错了，就会一直等".
- Include technical/details: add one engineering checklist titled "真正难的是这三件事", with three large cards only: "怎么判断哪些 KV 是热的", "怎么别让搬运把收益吃掉", "怎么让计算和回传重叠"; attach one bottom conclusion bar "这条路主要解容量，不直接解单位成本".

**Optional top/bottom overview:**
Add one compact top overview strip titled "两种办法，在砍两种账", with two large arrows from the same "128K token 上下文" strip: one arrow to "Prefix cache → 少做重复 prefill", another arrow to "冷 KV 下放 → 先把它放下"; under them place three target badges only: "显存", "prefill", "decode".

Annotations: "120,000 token 旧前缀", "11,072 token 新内容", "前缀 KV 已算好", "直接复用", "整段重算", "只算新增", "HBM：热 KV", "CPU 内存：温 KV", "NVMe：冷 KV", "先判断热点", "提前搬回", "边算边等", "容量问题", "不是同一个问题"

**Style specifications:**
- Explanatory infographic, not decorative illustration
- Choose the right visual form based on meaning
- Clean layout, clear hierarchy, dense but readable
- Readability first: fewer but larger labels when the content is numerically dense
- Functional colors with restrained palette
- Arrows, labels, legends, zoom-ins, guides, and callouts where useful
- Keep text embedded inside the visual explanation
- Make objects, relationships, transitions, comparisons, and evidence visible
