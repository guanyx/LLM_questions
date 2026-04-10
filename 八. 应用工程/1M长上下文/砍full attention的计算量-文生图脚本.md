# 砍 full attention 的计算量：模型厂商怎么把平方爆炸压下去？

Create a highly detailed technical infographic in hand-drawn sketch style on pure white background. The theme is "砍 full attention 的计算量：模型厂商怎么把平方爆炸压下去？"

Visual structure should explain how model providers reduce full-attention compute for ultra-long-context inference, in ONE single infographic, arranged vertically from top to bottom with dense formulas, complexity comparisons, before-vs-after diagrams, and engineering callouts.

## Top Section - Title + Problem

- Main title at top center: "砍 full attention 的计算量：模型厂商怎么把平方爆炸压下去？"
- Subtitle below: "1M 上下文最可怕的第二笔账，是 prefill 的 n² 计算量"

## Section 1 - 第一刀：缩短活跃上下文（同样适用 decode 阶段）

- Section title: "1. 第一刀：把活跃上下文从 1M 压到 100k（同样适用 decode 阶段）"
- Opening note:
  - 这一刀的核心，不是优化 kernel
  - 而是先别让模型真的背着 1M 活跃上下文去算
  - 它首先是在砍 full attention 的 n² 计算量
  - 但同样也会线性降低 decode 每一步要扫的历史长度
- Show before-vs-after sequence length cards:
  - 活跃上下文：1,000,000
  - 活跃上下文：100,000
- Show one compact impact note:
  - 活跃上下文缩短以后，full attention 的主计算量会按平方往下掉
- Show four method cards as the visual focus:
  - 卡片一：检索
    - 先把材料切块和建索引
    - 提问时只召回最相关的那一小部分
  - 卡片二：摘要
    - 原文不一直放在前台
    - 先压成章节摘要、阶段摘要、状态摘要
  - 卡片三：分层记忆
    - 最近的内容留原文
    - 更老的内容只留结论、约束、状态
  - 卡片四：动态精读
    - 每一轮都围着当前问题重新组上下文
    - 谁相关谁上前台，谁不相关谁退后台
- Add closing explanation:
  - 这四种做法表面不同
  - 本质上都在做同一件事：把真正进入 full attention 的活跃上下文压短

## Section 2 - 第二刀：滑动窗口 / 块稀疏注意力

- Section title: "2. 第二刀：把 n² 改成 n × w"
- Show structural comparison:
  - 左侧：dense full attention，所有 token 两两相看
  - 右侧：滑动窗口 + 少量全局 token，只看局部邻域
- Show complexity comparison:
  - 原始：O(n²)
  - 现在：O(n × w)
- Show one concrete substitution:
  - n = 1,000,000
  - w = 16,000
  - 相对 full attention ≈ 降到原来的 1/62.5
- Add engineering note:
  - 这不是完全免费
  - 它是在“少看一点历史”和“把计算压下来”之间做交换

## Section 3 - 第三刀：prefix cache

- Section title: "3. 第三刀：别把同一段前缀反复重算"
- Show repeated-query visual:
  - 同一份超长材料
  - 多轮连续追问
  - 如果前缀不变，没必要每轮重做整段 prefill
- Show mechanism note:
  - prefix cache 不会改变单次 full attention 的公式
  - 它省的是重复 prefill
- Add direct takeaway:
  - 对“同一份长材料反复问”特别值钱
  - 不做这一步，就是每轮都在重复烧最贵那段算力

## Bottom Section - Summary

- Place one strong summary sentence:
  - "砍 full attention 的计算量，本质上是在想办法别让 n² 真的按 1M 全量爆开"
- Add one transition question at the very bottom:
  - "其中 GQA / MQA、KV 量化、缩短活跃上下文，这三类做法在 decode 阶段也会继续发挥作用"

## Overall Layout and Style

- One single infographic page
- Pure white background
- Hand-drawn technical sketch aesthetic
- Use formulas, complexity ladders, sequence-length comparison cards, sparse-attention diagrams, repeated-query flow diagrams, and callout arrows
- All labels and annotations in Chinese
- Keep English only for technical terms such as dense full attention, FLOPs, prefix cache, sliding window, sparse attention
- Professional engineering documentation style with leader lines and clear hierarchy
- Very information-dense, small but readable text
- Color palette:
  - Navy blue for main structure
  - Teal for formulas and arrows
  - Orange for highlighted reductions
  - Light gray for secondary guides

Style: Technical hand-drawn sketch infographic, information-dense engineering blueprint, single-page optimization breakdown, clean white background, strong visual hierarchy
