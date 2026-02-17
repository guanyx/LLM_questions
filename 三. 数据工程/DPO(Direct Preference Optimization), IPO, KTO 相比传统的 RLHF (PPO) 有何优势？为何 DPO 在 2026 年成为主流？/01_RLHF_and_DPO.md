# DPO, IPO, KTO 相比传统的 RLHF (PPO) 有何优势？为何 DPO 在 2026 年成为主流？ (Part 1)

> **摘要**：2026 年，大模型对齐（Alignment）领域完成了一场彻底的范式转移。DPO 及其变体（IPO, KTO, SimPO）通过数学上的等价性推导，成功移除了 RLHF 流程中昂贵且不稳定的 Reward Model，将强化学习问题转化为更稳定的监督学习问题。本文将从第一性原理出发，剖析这一技术演进背后的工程逻辑与数学本质。

---

## 1. 核心问题：RLHF (PPO) 的工程瓶颈

在 2023 年，基于 PPO (Proximal Policy Optimization) 的 RLHF 是训练 ChatGPT 等顶级模型的唯一路径。然而，从系统工程的角度来看，PPO 存在三个显著的痛点，限制了其在工业界的规模化应用：

1.  **显存开销极大**：PPO 训练过程中需要同时加载四个模型：

    - **Policy Model (Actor)**：正在被优化的主角模型。它的目标是生成能获得高奖励的回答。
    - **Reference Model (Ref)**：Policy Model 的一个冻结副本（SFT 阶段的模型）。它作为一个“锚点”，用来计算 KL 散度，防止 Policy Model 在优化过程中过度跑偏，产生乱码或失去语言能力。
    - **Reward Model (Critic)**：模拟人类偏好的打分器。它输入“问题+回答”，输出一个标量分数。这个模型通常和 Policy Model 一样大。
    - **Value Model**：用于预测当前状态的长期预期收益（Value Function）。它辅助计算 Advantage（优势函数），以降低梯度估计的方差，保证训练的稳定性。

      这四个模型通常大小相当，意味着如果我们要微调一个 70B 的 Llama-3，在 PPO 阶段我们需要在显存中同时塞入 4 个 70B 级别的模型（或其梯度/优化器状态），这对硬件资源构成了天文数字般的要求。

2.  **训练稳定性差**：PPO 对超参数（如学习率、Clip 范围、GAE 参数）极度敏感。Reward Model 的打分往往存在噪声，而强化学习算法容易利用这些噪声（Reward Hacking），导致模型输出乱码或重复内容以骗取高分。

3.  **流程复杂**：需要先训练 SFT 模型，再训练 Reward Model，最后进行 PPO。流程长，维护成本高。

---

## 2. 第一性原理：从“间接优化”到“直接优化” (DPO)

DPO (Direct Preference Optimization) 的核心洞察在于重新审视了“对齐”的数学本质，开启了“无 Reward Model”时代。

### 核心痛点：中间商赚差价 (RLHF/PPO)

传统的 RLHF 包含一个中间环节：**Reward Model (奖励模型)**。
这本质上是一个**代理（Proxy）**机制。Reward Model 是人类意图的代理，但这个代理并不完美，且引入了额外的计算成本。

### 机制创新：直接映射 (Direct Mapping)

DPO 的作者 Rafailov 等人通过数学推导发现：**Optimal Policy (最优策略) $\pi^*$ 和 Reward Function (奖励函数) $r$ 之间存在一一映射关系（同构）。**

- **机制**：
  它不再去拟合一个分数值，而是**直接最大化“好回答”与“坏回答”的相对概率差**。
  - 计算当前 Policy Model 生成“好回答” $y_w$ 的概率相对于 Reference Model 的提升程度。
  - 计算当前 Policy Model 生成“坏回答” $y_l$ 的概率相对于 Reference Model 的提升程度。
  - **DPO 的目标就是让前者尽可能地大于后者。**

### 实际价值

1.  **显存减半**：只需加载 Policy Model 和 Reference Model，相比 PPO 的四模型架构，显存占用直接砍半。
2.  **训练稳定**：整个过程类似于监督学习（Supervised Learning），没有强化学习中那种高方差的梯度估计，训练曲线平滑，不易发散。

### 局限性：概率过拟合 (Probability Overfitting)

DPO 倾向于无限拉大“好回答”和“坏回答”之间的概率差。为了让 Loss 最小，模型会拼命提高好回答的概率，压低坏回答的概率。这会导致 KL 散度过高，模型为了迎合偏好数据，牺牲了语言生成的自然度和多样性。
