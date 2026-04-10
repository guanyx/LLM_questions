# 砍 KV cache：模型厂商先动哪几刀？

```text
Create a highly detailed infographic with explanatory diagrams, accurate visual semantics, and Chinese labels where text appears inside the image:

**Title (top):**
"砍 KV cache：模型厂商先动哪几刀？"

**Subtitle (Optional):**
"1M 上下文先撞墙的，往往不是算力，而是显存。"

**Main Content - Detailed sections:**
*Create one section for EACH optimization move in the source text. Keep one continuous mini-case across the full page: the same decoder-only Transformer handles the same long context strip labeled “1M token 历史上下文”, and the same KV cache block is repeatedly modified through head sharing, precision compression, and tiered storage migration.*

**Section 1: 第一刀：减少 KV heads（GQA / MQA，同样适用 decode 阶段）**
- **Mandatory Text Block**: "query heads 还可以很多，但 K 和 V 不需要一份一份都存。"
- Detailed diagram of a before-vs-after attention architecture: left side labeled "改动前" shows many query heads each paired with their own KV heads; right side labeled "改动后" shows many query heads converging into fewer shared KV heads, with Chinese labels for "query heads", "KV heads", "共享 K", "共享 V", "GQA / MQA".
- Show the same "1M token 历史上下文" strip feeding both sides, so the viewer sees that the context length is unchanged while only the KV storage pattern changes.
- Comparative Visual: add one clear ratio board in the middle with "32 个 KV heads → 8 个 KV heads → KV cache 体积约降到 1/4", and use proportional blocks whose width visibly shrinks to one quarter.
- Show ... step by step: "多个 query 头读取同一组 KV" → "需要存的 K/V 份数减少" → "每 token 的 KV cache 下降" → "decode 阶段读取量同步下降", with labeled arrows and Chinese step numbers.
- Include technical/details: add a small decode inset showing one new token 生成时读取更少的 KV head slots, with a note "不只是显存降，decode 也少读一截".
- Context/Background: place a side note panel titled "这一刀改的是哪一层", explaining that the optimization touches the internal attention representation rather than cutting context length itself.

**Section 2: 第二刀：把 KV 从高精度压低（同样适用 decode 阶段）**
- **Mandatory Text Block**: "bit 越低，显存越省，但精度、副作用、工程复杂度也会上来。"
- Detailed diagram of the same KV cache block now shown as a precision ladder, with three stacked rungs labeled "fp16 / bf16：2 字节", "fp8：1 字节", "4 bit：0.5 字节"; each rung should connect to the same cache object to show that the object is unchanged but its storage density changes.
- Comparative Visual: place three memory bars side by side with large Chinese labels "128 GB", "64 GB", "32 GB", and add arrows "直接减半" and "再减半" between adjacent bars.
- Show the calculation linkage explicitly: "每个元素字节数下降" → "每个 token 的 KV cache 下降" → "1M token 总显存下降", with thin guide lines connecting precision labels to total memory result bars.
- Include technical/details: add a small magnified tile view of the same KV cell under three precisions, labeled "高精度", "中精度", "更低精度", to visually explain that the saved space comes from fewer bits per value rather than fewer tokens.
- Error/Consequence Mode: place an orange caution box titled "压缩不是白送的", listing three Chinese impact tags: "精度风险", "误差累积", "工程实现更复杂".
- Context/Background: add one note beside the decode arrow saying "decode 阶段读取的还是这些 KV，只是每份更小".

**Section 3: 第三刀：冷 KV 下沉到更低层存储**
- **Mandatory Text Block**: "这刀主要省的是 HBM 容量，不是白捡。"
- Detailed diagram of a tiered memory stack drawn vertically: top layer "GPU HBM：最贵、最快", middle layer "CPU 内存：更大、更慢", bottom layer "更低层存储：更便宜、更慢"; show the same KV cache split into two color-coded groups "热 KV" and "冷 KV".
- Show ... step by step: "最近常用的热 KV 留在 GPU" → "较旧较冷的 KV 往外放" → "需要时再回传" → "HBM 常驻压力下降", with directional arrows crossing layers and Chinese step numbers.
- Comparative Visual: add a left-right storage occupancy comparison labeled "全部留在 GPU" vs "热冷分层后", where the GPU HBM block visibly shrinks after cold KV is moved out.
- Include technical/details: place a narrow latency-and-bandwidth tradeoff strip beside the memory layers with labels "更高延迟", "更差带宽", "更复杂调度", and show these costs increasing as data moves downward.
- Error/Consequence Mode: add a warning callout near the arrows between GPU and CPU saying "省下 HBM，不代表访问免费", with three Chinese labels "跨层搬运", "等待增加", "系统复杂度上升".
- Context/Background: keep the same "1M token 历史上下文" strip at the top of the section, and mark earlier tokens as "冷", newer tokens as "热", so the viewer sees why older历史状态更适合被下沉。

**Optional top/bottom overview:**
At the very top, add one compact global overview titled "同一个 1M 上下文，三种砍法", with three downward branches labeled "少存几份 KV", "每份 KV 更小", "把冷 KV 挪出去". At the very bottom, place one strong summary sentence "砍 KV cache，本质上是在想办法让 1M 历史状态少占点最贵的显存", followed by a bold transition question "KV cache 省下来以后，full attention 的计算量还怎么砍？", with a dotted continuation arrow to the next page.

Annotations: "1M token 历史上下文", "32 个 KV heads → 8 个 KV heads", "KV cache 体积约降到 1/4", "2 字节 → 1 字节 → 0.5 字节", "128 GB", "64 GB", "32 GB", "热 KV 留在 GPU", "冷 KV 往外放", "这刀主要省的是 HBM 容量，不是白捡"

**Style specifications:**
- Explanatory infographic, not decorative illustration
- Choose the right visual form based on meaning: head-sharing comparison, precision ladder, tiered storage migration
- Single-page vertical engineering layout on pure white background
- Hand-drawn technical sketch aesthetic with clear leader lines, arrows, brackets, legends, and local zoom-ins
- Clean hierarchy, dense but readable composition, functional colors only
- Keep all visible labels, notes, warnings, summaries, and axis-like guides in Chinese
- Keep English only for necessary technical terms already in the source, such as GQA, MQA, fp16, bf16, fp8, 4 bit, GPU HBM, decode
- Use navy blue for main structure, teal for formulas and flow arrows, orange for reductions and warnings, light gray for guides and background frames
- Make objects, comparisons, transitions, storage locations, and trade-offs visually explicit
```
