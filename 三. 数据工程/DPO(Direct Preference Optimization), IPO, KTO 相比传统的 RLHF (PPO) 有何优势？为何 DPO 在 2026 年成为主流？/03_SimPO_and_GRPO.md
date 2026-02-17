# 2026 对齐技术演进 (Part 3)：SimPO 的极致效率与 GRPO 的推理革命

## 5. SimPO (Simple Preference Optimization): 极致的显存效率

SimPO 是为资源受限场景（如边缘计算、消费级显卡微调）量身定制的方案，它彻底移除了 RLHF 流程中最后的“赘肉”——Reference Model，实现了真正的单模型训练。

### 核心痛点：Reference Model 的“隐形税” (The Hidden Cost of Reference Models)

在 DPO/IPO/KTO 中，虽然我们去掉了 Reward Model，但公式里依然保留了 $\pi_{ref}$ (Reference Model)。

- **显存双倍负担**：为了计算 KL 散度（防止模型跑偏），训练时必须始终加载一个冻结的 Reference Model。这意味着如果你要微调一个 Llama-3-70B，你需要双倍的显存（或者复杂的 Offloading 策略）。
- **计算效率低**：每次前向传播都需要跑两个模型，浪费了大量的算力在“计算参考值”上。

### 机制创新：自带标尺与长度归一化 (Self-Contained Reward & Length Norm)

SimPO (Simple Preference Optimization) 的核心洞察是：**能不能把 KL 散度约束直接融入到 Reward 的定义里？**

- **移除 Reference Model**：
  SimPO 发现，Reference Model 的主要作用是作为一个 Baseline。SimPO 直接抛弃了它，转而使用**平均对数概率 (Average Log Probability)** 作为 Reward 的代理。
- **长度归一化 (Length Normalization)**：
  直接使用 Log Probability 有个大坑：**长度偏见 (Length Bias)**。如果不做处理，模型往往会倾向于生成极短的回答（因为概率连乘越少数值越大）或者为了得分而生成冗长的废话。
  SimPO 将生成概率除以序列长度，计算**平均 Log Prob**。这不仅消除了长度偏见，还奖励了那些**“言简意赅”**的高质量回答。

- **目标边际 (Target Margin)**：
  SimPO 在优化目标中引入了一个硬性的 Margin ($\gamma$)：
  “好回答的平均得分，必须比坏回答高出 $\gamma$ 分。”
  这迫使模型在 Logits 层面直接拉开差距，起到了替代 KL 散度约束的作用。

### 实际价值

1.  **真正的单模型训练**：这是 SimPO 的杀手级特性。它不需要加载 Reference Model，显存占用直接减半。
2.  **消费级显卡友好**：使得在 3090/4090 等 24GB 显存的卡上微调更大参数的模型成为可能，是个人开发者和边缘计算场景的首选。
3.  **训练速度提升**：由于去除了对 Reference Model 的依赖，训练速度提升了约 20%~40%（省去了 Reference 的前向传播）。
4.  **更加简洁 (Conciseness)**：由于长度归一化的存在，SimPO 训练出的模型倾向于输出更简洁、直接的答案，在 AlpacaEval 2 等榜单上表现优异。

## 6. GRPO (Group Relative Policy Optimization): 复杂推理的新霸主

如果说 DPO 是擅长聊天的“文科生”，那 GRPO 就是擅长逻辑推演的“理科生”。它是 DeepSeek-R1 能够通过强化学习涌现出“Aha Moment”（顿悟时刻）的核心武器。

### 核心痛点：DPO 的探索短板与 PPO 的显存重负

- **DPO 的局限 (No Exploration)**：DPO 是离线算法，它只能学习给定的数据，无法探索新的解题路径。对于数学和代码问题，往往存在多种解法，模型需要通过“尝试-错误-修正”来通过测试。
- **PPO 的代价 (The Critic Burden)**：为了引入探索能力，传统的 PPO 引入了一个 **Critic Model (价值模型)** 来评估每一步的好坏。这意味着显存里需要同时容纳 4 个模型（Policy, Reference, Reward, Critic），显存消耗巨大且训练极不稳定。

### 机制创新：去 Critic 化的群体博弈 (Group Relative Advantage)

GRPO 巧妙地结合了 RL 的探索能力和 DPO 的简洁性。它移除了昂贵的 Critic Model，转而利用**群体统计特征**来充当 Baseline。

- **组团采样 (Group Sampling)**：
  对于每一个问题，GRPO 不只生成一个答案，而是让模型一口气生成一组答案（比如 $G=64$ 个）。这相当于让模型进行一次“头脑风暴”，探索不同的思维链路 (Chain of Thought)。

- **相对优势 (Group Relative Advantage)**：
  如何评价这 64 个答案的好坏？GRPO 不需要一个训练好的 Critic 来打分，而是直接计算**组内相对排名**。

  - 首先，用客观规则（如数学答案正确性、代码通过率）或 Reward Model 给这 64 个答案打分。
  - 然后，计算这组分数的平均值和标准差。
  - **优势函数 (Advantage)** = (当前得分 - 组内平均分) / 组内标准差。

  这句潜台词是：“我不需要知道绝对分值是多少，我只需要知道你是否比你的‘兄弟姐妹’们表现得更好。”

- **PPO 式的裁剪更新**：
  有了优势函数后，GRPO 采用类似 PPO 的裁剪（Clip）机制来更新策略，确保每次更新步子不会迈得太大，保证了训练的稳定性。

### 实际价值

1.  **推理能力的涌现**：GRPO 允许模型在训练中通过大量的采样尝试，自我发现更优的推理路径。DeepSeek-R1 正是靠它“悟”出了自我验证和长思维链的能力。
2.  **PPO 的终结者**：在保留 RL 探索能力的同时，GRPO 砍掉了 Critic Model，显存占用与 DPO 持平（仅需 Policy + Reference），使得大规模强化学习变得经济可行。
3.  **Outcome Reward 的最佳拍档**：在数学/代码领域，结果真值（Answer Correctness）很容易获得，GRPO 能极其高效地利用这些客观信号进行自我进化，而无需依赖难以训练的过程奖励模型（Process Reward Model）。
