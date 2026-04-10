Create a highly detailed infographic with explanatory diagrams, accurate visual semantics, and Chinese labels where text appears inside the image:

**Title (top):**
"冷 KV 下放和 FlashAttention，分别在省什么？"

**Subtitle (Optional):**
"前者主要解决“能不能放下”，后者主要解决“数据怎么更省地流过 GPU”，它们都不是直接把理论大账变没。"

**Main Content - Detailed sections:**
*Create one section for EACH optimization path in the source text. Keep one continuous mini-case across the full page: the same DeepSeek-R1-Distill-Llama-70B handles the same long strip labeled “128K token 上下文”, and the same decode loop keeps requesting old KV history so the viewer can compare how cold-KV offloading and FlashAttention attack different bottlenecks.*
*For each section, keep only 1 mandatory text block plus 2 non-redundant visual dimensions. Prefer larger labels and fewer micro-callouts over maximum detail density.*

**Section 1: 冷 KV 下放到更慢层级**
- **Mandatory Text Block**: "这条路主要解决的是“能不能放下”，不是“能不能便宜地跑”。"
- Detailed diagram of one tiered storage system titled "KV 分层存放": top layer is a small fast cabinet labeled "HBM：热 KV", middle layer is a larger cabinet labeled "CPU 内存：温 KV", bottom layer is the largest slower cabinet labeled "NVMe / 更慢层级：冷 KV"; show the same long history strip aging over time and flowing downward from top to bottom, while one highlighted current decode token on the right keeps requesting old history.
- Show ... step by step: add one explicit request path titled "decode 时发生了什么", with four large nodes in sequence "先判断这一步最可能访问哪些 KV" → "尽量提前搬回更快层" → "GPU 开始算当前 token" → "算的时候继续等剩余数据回来"; place one red consequence badge at the end "猜错了，就会一直等数据".

**Section 2: 冷 KV 下放的代价**
- **Mandatory Text Block**: "它没有把成本变没，只是把成本从 GPU 显存容量，换成了更高延迟、更差带宽和更复杂调度。"
- Comparative Visual: show one left-right tradeoff scale titled "这条路到底换了什么", with the left side labeled "放得下" and icons "HBM 压力更小", and the right side labeled "跑得慢" with icons "回传等待", "搬运开销", "调度复杂"; make the right side visually heavier in orange-red.
- Include technical/details: add one compact engineering checklist titled "真正难的是这些", with three big checklist cards only: "如何判断哪些 KV 是热的", "如何避免搬运本身把收益吃掉", "如何让 GPU 计算和数据回传重叠"; add one bottom conclusion bar "这条路解决的是容量问题，不直接解决单位成本问题".

**Section 3: FlashAttention 省的是实现税**
- **Mandatory Text Block**: "FlashAttention 主要优化的是数据怎么流过 GPU，不是把 full attention 的理论主项从 n² 改掉。"
- Comparative Visual: draw one left-right pipeline comparison. On the left, show "传统 attention" as a bulky pipeline with four large boxes "写入大 score 矩阵" → "读出做 softmax" → "写回结果" → "再读出乘 V", with repeated arrows to a large HBM box. On the right, show "FlashAttention" as tiled compute blocks labeled "Q/K/V 小 tile" operating inside a chip-local area labeled "片上 SRAM", with a short arrow note "尽量不把完整中间矩阵落回 HBM".
- Include technical/details: add one result board titled "它到底改了什么", with three large cards only: "HBM 读写更少", "临时显存更小", "真实实现常数项更低"; below them place one short note "改的是数据流，不是理论复杂度".

**Section 4: 两种手段不是一回事**
- **Mandatory Text Block**: "冷 KV 下放在解决容量边界，FlashAttention 在解决实现效率，它们打的不是同一个瓶颈。"
- Comparative Visual: draw one 2×2 matrix titled "两种手段分别在打哪里", with horizontal axis labeled "容量压力 ←→ 数据流效率" and vertical axis labeled "系统级 ←→ kernel级"; place "冷 KV 下放" in the "容量压力 + 系统级" quadrant and "FlashAttention" in the "数据流效率 + kernel级" quadrant, with short notes under each.
- Error/Consequence Mode: add one bottom warning strip titled "别把账算错", with two red callouts only: "冷 KV 下放不等于免费长上下文" and "FlashAttention 不等于把 O(n²) 变没了".

**Optional top/bottom overview:**
Add one compact top overview strip titled "两条路，各省一笔不同的账", with two big arrows: "冷 KV 下放 → 先解决放不下" and "FlashAttention → 先减少实现浪费", both pointing to the same long strip labeled "128K token 上下文".

Annotations: "HBM：热 KV", "CPU 内存：温 KV", "NVMe：冷 KV", "先判断热点", "提前搬运", "等数据回来", "传统 attention", "FlashAttention", "Q/K/V 小 tile", "片上 SRAM", "HBM 读写更少", "容量问题", "实现税", "不是同一个瓶颈"

**Style specifications:**
- Explanatory infographic, not decorative illustration
- Choose the right visual form based on meaning
- Clean layout, clear hierarchy, dense but readable
- Readability first: fewer but larger labels when the content is numerically dense
- Functional colors with restrained palette
- Arrows, labels, legends, zoom-ins, guides, and callouts where useful
- Keep text embedded inside the visual explanation
- Make objects, relationships, transitions, comparisons, and evidence visible
