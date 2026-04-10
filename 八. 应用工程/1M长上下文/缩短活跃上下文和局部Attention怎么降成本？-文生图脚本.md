Create a highly detailed infographic with explanatory diagrams, accurate visual semantics, and Chinese labels where text appears inside the image:

**Title (top):**
"缩短上下文 和 局部 Attention"

**Subtitle (Optional):**
"一条路是先少送点进去，另一条路是送进来了也别让它们全连。"

**Main Content - Detailed sections:**
*Create one section for EACH optimization path in the source text. Keep one continuous mini-case across the full page: the same DeepSeek-R1-Distill-Llama-70B handles the same long strip labeled “128K token 上下文”, and the same long document is shown before and after optimization so the viewer can directly compare how each method cuts a different part of the bill.*
*For each section, keep only 1 mandatory text block plus 2 non-redundant visual dimensions. Prefer larger labels and fewer micro-callouts over maximum detail density.*

**Section 1: 缩短活跃上下文**
- **Mandatory Text Block**: "这条路不改公式，先把真正送进去算的那一段变短。"
- Show one top-down pipeline titled "先筛，再算": start from one huge wall of text labeled "128K 原始材料", cut it into many visible chunks, then split into three branches with large Chinese labels "先检索", "先压摘要", "分层记忆"; finally merge them into a much shorter strip labeled "真正送进 attention 的部分". Keep the three branches visually distinct: retrieval keeps only a few highlighted source chunks, summarization compresses long text blocks into short abstract cards, layered memory shows three tiers labeled "近的留原文", "远一点留摘要", "更远只留目录".
- Include technical/details: add one compact comparison board titled "上下文一缩，账就往下掉", with two vertical columns "压到 64K" and "压到 32K", and only three metric rows: "fp16 KV cache：42.95 GB → 21.47 GB / 10.74 GB", "prefill：4.05 × 10^16 → 1.46 × 10^16 / 5.89 × 10^15 FLOPs", "decode / token：4.80 × 10^11 → 3.09 × 10^11 / 2.23 × 10^11 FLOPs"; attach one orange corner note "prefill 掉得最快，因为 full attention 主项是 n²".

**Section 2: 这条路是怎么真的把 n 变小的**
- **Mandatory Text Block**: "它不是在 attention 里面省，而是在 attention 开始前，先把大部分不相关内容挡掉。"
- Show ... step by step: draw one left-to-right action chain titled "系统一般怎么做", with four large nodes "长文档切块" → "每块先做 embedding" → "用户提问时先召回" → "只把得分最高的几段拼进 prompt"; under the main chain, add two alternate mini-paths: "旧历史先压成摘要再拼" and "最近原文 + 更早摘要 + 更远目录".
- Error/Consequence Mode: add one tradeoff board titled "代价也很直接", with four large warning cards only: "召回链路更复杂", "召回错了，后面再强也没用", "摘要会丢原句细节", "跨很远的精确对齐更难做".

**Section 3: 局部 attention / 块稀疏**
- **Mandatory Text Block**: "token 还是都进来了，但不是每个 token 都要看完全部历史。"
- Comparative Visual: show one side-by-side attention matrix comparison. On the left, draw one full square matrix labeled "全局 attention" with a fully filled grid and one badge "128K × 128K". On the right, divide the panel into two clearly separated examples: a diagonal band labeled "滑动窗口" and a sparse block matrix labeled "块稀疏"; from one highlighted current token position, draw arrows only to nearby windows, chapter-title blocks, and summary blocks, labeled "附近块", "标题块", "摘要块".
- Include technical/details: add one result board titled "把 n² 这块削薄以后", showing "复杂度更像 n × w", then substitute "n = 131,072, w = 16,000", and end with three large metric cards only: "总 prefill：4.05 × 10^16 → 2.07 × 10^16", "decode / token：4.80 × 10^11 → 1.79 × 10^11", "理想 fp16 热 KV：42.95 GB → 5.24 GB"; attach one orange tag "attention core 大约省 8.19×，但总账不会跟着等比例掉".

**Section 4: 它和“缩短上下文”不是一回事**
- **Mandatory Text Block**: "前一条是先少送点进去，这一条是都送进去了，但别让它们彼此全连。"
- Comparative Visual: draw one clean two-column comparison titled "这两条路差在哪", with the left column "缩短活跃上下文" and the right column "局部 / 稀疏 attention". Under the left column show one icon flow "先删 / 先压 / 先筛 → n 变小"; under the right column show one icon flow "token 全进来 → 连接关系变稀". Put one big center divider label "一个改输入量，一个改连接方式".
- Error/Consequence Mode: add one bottom warning strip titled "这条路也有代价", with four large callouts only: "超窗口逐 token 匹配会变弱", "得设计全局 token 去补远距离信息", "窗口大小和稀疏规则都要调", "远距离逐字细节任务会更敏感".

**Style specifications:**
- Explanatory infographic, not decorative illustration
- Choose the right visual form based on meaning
- Clean layout, clear hierarchy, dense but readable
- Readability first: fewer but larger labels when the content is numerically dense
- Functional colors with restrained palette
- Arrows, labels, legends, zoom-ins, guides, and callouts where useful
- Keep text embedded inside the visual explanation
- Make objects, relationships, transitions, comparisons, and evidence visible
