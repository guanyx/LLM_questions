# Large Language Model Reasoning Failures

# 大型语言模型推理失败

**原论文标题**: Large Language Model Reasoning Failures
**作者**: Peiyang Song, Pengrui Han, Noah Goodman
**发布时间**: 2026 年 2 月
**arXiv 链接**: [2602.06176](https://arxiv.org/abs/2602.06176)
**GitHub 仓库**: [Awesome-LLM-Reasoning-Failures](https://github.com/Peiyang-Song/Awesome-LLM-Reasoning-Failures)

---

## 摘要 (Abstract)

大型语言模型（LLMs）展现出了卓越的推理能力，在广泛的任务中取得了令人印象深刻的成果。尽管取得了这些进步，但**重大的推理失败（Reasoning Failures）**仍然存在，甚至发生在看似简单的场景中。

为了系统地理解和解决这些不足，本文提出了首个专门针对 LLM 推理失败的综合综述。我们引入了一个新颖的分类框架，将推理分为：

1.  **具身推理 (Embodied Reasoning)**
2.  **非具身推理 (Non-embodied Reasoning)**：进一步细分为
    - **非正式（直觉）推理 (Informal/Intuitive Reasoning)**
    - **正式（逻辑）推理 (Formal/Logical Reasoning)**

与此同时，我们将推理失败沿互补轴分类为三种类型：

1.  **基础性失败 (Fundamental Failures)**：LLM 架构固有的、广泛影响下游任务的失败。
2.  **特定应用局限性 (Application-specific Limitations)**：在特定领域中表现出的局限性。
3.  **鲁棒性问题 (Robustness Issues)**：以在微小变化下表现不一致为特征的问题。

对于每种推理失败，我们提供了清晰的定义，分析了现有研究，探讨了根本原因，并提出了缓解策略。通过统一分散的研究工作，我们的综述为 LLM 推理中的系统性弱点提供了结构化的视角，提供了宝贵的见解，并指导未来的研究朝着构建更强大、更可靠和更鲁棒的推理能力方向发展。

---

## 1. 引言 (Introduction)

“如果是我们从中吸取教训，失败就是成功。” —— 马尔科姆·福布斯

随着强大的架构、高效的算法和海量数据的兴起，大型语言模型（LLMs）在各个领域都取得了显著的成功。在这些成就中，作为 LLM 涌现能力的**推理（Reasoning）**引起了特别的关注。

尽管 LLM 在推理方面创下了令人印象深刻的记录，但在尝试这些任务时，LLM 是否真的利用了类似人类的推理过程仍然存在争议。本综述并不旨在解决这一激烈的争论，而是关注 LLM 推理研究中长期被忽视的一个重要领域——**LLM 推理失败**。

尽管现有的一些工作已经前瞻性地意识到了这一点的重要性，并逐案调查了 LLM 的推理失败，但该主题仍然是碎片化的，且作为一个统一的研究领域尚未得到充分探索。为了填补这一空白，我们提出了首个致力于统一 LLM 推理失败研究的综合综述。

---

## 2. 推理失败分类框架 (Taxonomy of Reasoning Failures)

本文提出了一个统一的分类框架，沿两个正交轴区分推理失败：

1.  **推理类型 (Type of Reasoning)**
2.  **失败性质 (Nature of Failure)**

### 2.1 推理类型 (Reasoning Types)

- **具身推理 (Embodied Reasoning)**：

  - 涉及空间感知、物理启示（affordances）或接地气（grounded）的运动/动作规划的任务中的崩溃。
  - 原因通常是缺乏物理交互信号的仅文本/视觉预训练。

- **非具身推理 (Non-embodied Reasoning)**：
  - **非正式（直觉）推理 (Informal/Intuitive)**：
    - 常识、社会推理或启发式推理中的失败。
    - 例如：不一致的道德判断、心智理论（Theory of Mind）错误、认知偏差重现。
  - **正式（逻辑）推理 (Formal/Logical)**：
    - 符号推理、思维链（CoT）组合和已验证的多步推理中的缺陷。
    - 例如：逻辑谬误、算术错误、变量绑定丢失。

### 2.2 失败性质 (Nature of Failure)

- **基础性失败 (Fundamental Failures)**：

  - LLM 架构或训练范式固有的失败。
  - 例如：自注意力分散导致的工作记忆崩溃、逆转诅咒（Reversal Curse）、认知偏差（源于训练数据中的语言模式或 Transformer 的因果掩码导致的顺序偏差）。

- **特定应用/领域局限性 (Domain-/Application-Specific Limitations)**：

  - 系统性但与领域绑定的限制。
  - 表现：在数学应用题、代码生成、逻辑基准测试或社会推断中，由于依赖浅层启发式方法而失败。

- **鲁棒性失败 (Robustness Failures)**：
  - 对语义上无关的提示变化敏感。
  - 例如：选项顺序打乱、插入干扰项、领域重述导致性能不一致。

---

## 3. 关键发现与分析 (Key Findings & Analysis)

### 3.1 组合性、系统性和析取推理缺陷

LLM 即使经过广泛的指令微调和 RLHF，在组合性和析取推理（Disjunctive Reasoning）方面仍然存在系统性弱点：

- **浅层析取推理**：在定性关系推理基准测试中，模型擅长单路径（链式）推理，但在多路径（析取/交集）任务中失败。
- **抽象和因果推理缺陷**：LLM 缺乏因果世界模型，无法归纳出超出直接观察模式的“因果路径”。
- **自洽性崩溃 (Self-Consistency Breakdown)**：LLM 违反了假设一致性（在语义等效的提示变换下预测相同的答案）和组合一致性。

### 3.2 多语言推理病理 (Multilingual Reasoning Pathologies)

多语言 LLM 显示出推理路径保真度和准确性的系统性崩溃，主要由语言先验和内部表示限制驱动：

- **跨语言崩溃 (Cross-Lingual Collapse)**：在低资源或非英语语言中进行 CoT 微调时，模型在内部推理路径中会恢复到其主导的预训练语言（通常是英语）。

---

## 4. 缓解策略与未来方向 (Mitigation Strategies)

为了解决这些推理失败，研究界正在探索多种缓解策略：

1.  **神经符号混合 (Neuro-symbolic Hybrids)**：结合神经网络的灵活性和符号系统的逻辑严密性。
2.  **思维链提示 (Chain-of-Thought Prompting)**：虽然提供了一些改进，但在真正的抽象和复杂推理中仍有局限性。
3.  **显式约束模块 (Explicit Constraint Modules)**：用于增强可靠性和安全部署。
4.  **动态课程与鲁棒性导向训练**。
5.  **早期检测诊断 (Early Detection Diagnostics)**。

未来的研究应超越简单的提示工程，深入探究根本原因，并致力于构建不仅在推理任务中表现更好，而且能“更好地失败”（优雅、透明、可恢复）的系统。
