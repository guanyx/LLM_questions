🚀 GraphRAG 十大硬核工程铁律 (2025 版)

1. 别被“重构”吓死：微软原生 GraphRAG 的社区摘要（Community Summaries）虽然强，但必须全量重构。如果你的业务要求 T+0 实时性，请直接放弃原生架构，拥抱 LightRAG 或 FalkorDB 的增量索引方案。
2. 小模型大用途：千万别用 GPT-4o 跑全量实体抽取，成本会让你破产。请微调 7B 甚至 3B 的专用小模型（如 Qwen2.5-IE），在抽取任务上效果媲美大模型，成本仅为 1/50。
3. 对齐是生命线：“马云”和“Jack Ma”不对齐，图谱就是废的。除了 Embedding 相似度，必须引入 LLM 二次清洗 或 社区检测 来合并实体，这是图谱质量的分水岭。
4. Schema 决定上限：不要一直跑 Schema-Free（自由抽取），那会导致关系类型爆炸。先自由跑少量数据发现规律，再固化 Schema 跑全量，这是平衡泛化与精准的最佳实践。
5. 剪枝即正义：检索时绝对不要把 2-Hop 邻居一股脑塞给 LLM。必须上 语义剪枝（Semantic Pruning），计算 Query 与边属性的相似度，只保留“顺路”的边，否则 Token 必爆。
6. 结构化 Prompt：把子图喂给 LLM 时，别用自然语言（“A 是 B 的父亲”），用 YAML 或 Markdown 列表。Token 密度更高，且 GPT-4 对这种结构化数据的推理能力显著更强。
7. 混合检索是标配：GraphRAG 不是 Vector RAG 的替代品，是互补品。Vector 负责模糊语义召回，Graph 负责精准逻辑推理。请务必使用 RRF 或 Router 进行双路融合。
8. 数据血缘（Lineage）：建图时必须把 Source Doc ID 和 Chunk ID 刻在每一条边上。否则删文档时，你根本不知道该删哪些边，增量更新直接变成灾难。
9. 图片别入库：千万别把图片 Base64 存进图数据库！对象存储（S3）存原图 + 向量库存 Embedding + 图数据库存元数据，这才是多模态图谱的标准姿势。
10. ColPali 降维打击：处理 PDF 图表时，忘掉 OCR 吧。2025 年请使用 ColPali，它直接对页面截图进行多向量索引（Visual-RAG），效果吊打“OCR 转文字”流派。

#GraphRAG #AI #知识图谱 #RAG #工程实践 #架构设计
