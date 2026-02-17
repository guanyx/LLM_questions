# Karpathy's microGPT 源码深度解析

Andrej Karpathy 发布的 `microgpt.py` 是一个极简的、零依赖的 GPT 实现。它在约 200 行纯 Python 代码中实现了从自动微分（Autograd）到 Transformer 模型架构，再到训练和推理的全过程。

这份代码展示了 Large Language Model (LLM) 最底层的数学原理，剥离了 PyTorch/TensorFlow 等框架的复杂性。它最大的特点是：**极其缓慢，但极其清晰**。

以下是对源码的逐行、逐块详细解读。

---

## 1. 基础设置与数据加载 (Lines 1-28)

这部分负责环境准备、数据下载和简单的 Tokenizer 实现。

```python
import os, math, random
random.seed(42) # 固定随机种子，保证结果可复现

# ...下载数据的代码...
docs = [l.strip() for l in open('input.txt').read().strip().split('\n') if l.strip()]
random.shuffle(docs)
```

- **零依赖**：只使用了 Python 标准库 (`math`, `random`, `os`, `urllib`)。这意味着你需要自己手写每一个数学运算（如矩阵乘法、指数、对数）。
- **数据**：默认下载 `names.txt`（一个包含 32k 个名字的数据集），用于训练模型生成类似的名字。
- **Tokenizer**：
  ```python
  uchars = sorted(set(''.join(docs))) # 构建字符集
  BOS = len(uchars) # 定义特殊的 "Beginning of Sequence" token
  vocab_size = len(uchars) + 1
  ```
  这里使用的是最简单的**字符级 Tokenizer**。
  - **Vocabulary**: 所有出现过的唯一字符 + 1 个特殊 Token。
  - **BOS (Beginning of Sequence)**: 用于标记一个名字的开始和结束。模型看到 BOS 就知道要开始生成新名字；生成 BOS 就意味着名字结束。

---

## 2. Autograd 引擎：`Value` 类 (Lines 30-73)

这是整个项目的核心基石。Karpathy 手写了一个标量级别的自动微分引擎（类似他的另一个项目 `micrograd`）。

### 核心概念：计算图 (Computation Graph)

深度学习框架的核心是构建一个“计算图”。当你计算 $a + b = c$ 时，框架不仅仅计算数值，还记住了 $c$ 是由 $a$ 和 $b$ 通过加法生成的。这样在反向传播时，它可以通过链式法则计算梯度。

```python
class Value:
    __slots__ = ('data', 'grad', '_children', '_local_grads')

    def __init__(self, data, children=(), local_grads=()):
        self.data = data        # 前向传播计算出的数值
        self.grad = 0           # 反向传播计算出的梯度（损失函数对该值的导数 dL/dValue）
        self._children = children # 计算图中的子节点（前驱节点，即生成该值的输入）
        self._local_grads = local_grads # 局部梯度（当前操作的导数）
```

### 运算符重载与链式法则

通过重载 Python 的运算符（`__add__`, `__mul__` 等），每次运算都会生成一个新的 `Value` 对象，并记录它是如何计算而来的。

- **加法 (`__add__`)**: $z = x + y$

  - 前向: `z.data = x.data + y.data`
  - 反向 (局部梯度): $\frac{\partial z}{\partial x} = 1, \frac{\partial z}{\partial y} = 1$
  - 代码体现: `local_grads=(1, 1)`

- **乘法 (`__mul__`)**: $z = x \cdot y$

  - 前向: `z.data = x.data * y.data`
  - 反向 (局部梯度): $\frac{\partial z}{\partial x} = y, \frac{\partial z}{\partial y} = x$
  - 代码体现: `local_grads=(other.data, self.data)`

- **其他运算**:
  - `exp`: $e^x$ 的导数是 $e^x$ (即它自己)。
  - `log`: $\ln(x)$ 的导数是 $1/x$。
  - `relu`: $max(0, x)$ 的导数在 $x>0$ 时为 1，否则为 0。

### 反向传播 (`backward`)

这是最神奇的部分。调用 `loss.backward()` 会自动计算所有参数的梯度。

```python
    def backward(self):
        # 1. 拓扑排序 (Topological Sort)
        # 确保在计算节点 v 的梯度前，依赖 v 的所有后续节点（父节点）都已计算完毕。
        topo = []
        visited = set()
        def build_topo(v):
            if v not in visited:
                visited.add(v)
                for child in v._children:
                    build_topo(child)
                topo.append(v)
        build_topo(self)

        # 2. 反向遍历并应用链式法则
        self.grad = 1 # 损失函数对自身的梯度为 1 (dL/dL = 1)
        for v in reversed(topo):
            for child, local_grad in zip(v._children, v._local_grads):
                # 链式法则: dL/dChild += (dL/dV) * (dV/dChild)
                child.grad += local_grad * v.grad
```

- **梯度累加 (`+=`)**: 一个节点可能被多个后续节点使用（例如一个权重矩阵被多次乘法使用），所以它的梯度是所有路径传回梯度的**和**。

---

## 3. 模型参数初始化 (Lines 75-90)

定义了 GPT 的超参数和所有可学习的权重。

```python
n_embd = 16     # 嵌入维度 (非常小，GPT-2 是 768)
n_head = 4      # 注意力头数
n_layer = 1     # Transformer 层数
block_size = 16 # 上下文窗口长度
```

### 参数字典 `state_dict`

所有的权重都被初始化为 `Value` 对象，这意味着它们都参与自动微分。

- `wte`: **Token Embeddings** (词嵌入)。形状 `[vocab_size, n_embd]`。将字符 ID 映射为向量。
- `wpe`: **Position Embeddings** (位置嵌入)。形状 `[block_size, n_embd]`。GPT 是位置敏感的，第 1 个字和第 2 个字的向量不同。
- `layer{i}.attn_...`: **Attention 投影矩阵**。
  - `wq`, `wk`, `wv`: 将输入 $x$ 投影到 Query, Key, Value 空间。
  - `wo`: Attention 输出后的线性投影。
- `layer{i}.mlp_...`: **前馈网络 (MLP) 权重**。
  - `fc1`: 升维到 $4 \times n\_embd$。
  - `fc2`: 降维回 $n\_embd$。
- `lm_head`: **语言模型头**。将最终的向量映射回词表大小的 logits，用于预测下一个字。

---

## 4. 辅助函数 (Lines 94-106)

- **`linear(x, w)`**: 全连接层。

  - 输入 $x$ 是一个向量（列表），权重 $w$ 是一个矩阵（列表的列表）。
  - 计算 $y = x \cdot w^T$。
  - 代码实现：双重列表推导式，手动进行点积求和。

- **`softmax(logits)`**: 归一化函数。

  - 输入是一组分数，输出是一组概率（和为 1）。
  - **数值稳定性技巧**: `max_val = max(...)`，先减去最大值再求 exp。这是为了防止 $e^{large\_number}$ 溢出（虽然 Python 整数无限大，但浮点数有上限，且大数 exp 计算不稳定）。

- **`rmsnorm(x)`**: Root Mean Square Normalization。
  - 公式: $x_i = \frac{x_i}{\sqrt{\frac{1}{n}\sum x_j^2 + \epsilon}} \times scale$
  - 作用: 强制让激活值的均方根为 1。这有助于梯度传播的稳定性，防止梯度爆炸或消失。
  - 现代 LLM（如 LLaMA）偏爱 RMSNorm 因为它比 LayerNorm 少减去均值这一步，计算更简单且效果相当。

---

## 5. GPT 模型架构 (Lines 108-144)

这是 Transformer Decoder 的实现。这里有一个非常有趣的细节：**它是逐 Token 处理的**。

```python
def gpt(token_id, pos_id, keys, values):
    # 1. Embedding
    tok_emb = state_dict['wte'][token_id]
    pos_emb = state_dict['wpe'][pos_id]
    x = [t + p for t, p in zip(tok_emb, pos_emb)] # 简单的向量加法
    x = rmsnorm(x)

    for li in range(n_layer):
        # 2. Multi-Head Attention (MHA)
        # ... (计算 Q, K, V) ...
        q = linear(x, state_dict[f'layer{li}.attn_wq'])
        k = linear(x, state_dict[f'layer{li}.attn_wk'])
        v = linear(x, state_dict[f'layer{li}.attn_wv'])

        # KV Cache 机制!
        keys[li].append(k)   # 将当前 token 的 K 存入历史
        values[li].append(v) # 将当前 token 的 V 存入历史

        # Attention 计算
        # Attention(Q, K, V) = softmax(Q * K^T / sqrt(d)) * V
        for h in range(n_head):
            # 切分 Head
            q_h = q[hs:hs+head_dim]
            # 获取所有历史 K (包括当前步)
            k_h = [ki[hs:hs+head_dim] for ki in keys[li]]
            v_h = [vi[hs:hs+head_dim] for vi in values[li]]

            # Scaled Dot-Product Attention
            # 计算注意力分数 (logits)
            attn_logits = [sum(q_h[j] * k_h[t][j] for j in ...) / sqrt(d) for t in range(len(k_h))]
            attn_weights = softmax(attn_logits)

            # 加权求和
            head_out = [sum(attn_weights[t] * v_h[t][j] ...) ...]
            x_attn.extend(head_out)

        x = linear(x_attn, state_dict[f'layer{li}.attn_wo']) # 投影回 n_embd
        x = [a + b for a, b in zip(x, x_residual)] # 残差连接 (Residual Connection)

        # 3. Feed-Forward Network (MLP)
        # Norm -> Linear -> ReLU -> Linear -> Residual
        x_residual = x
        x = rmsnorm(x)
        x = linear(x, state_dict[f'layer{li}.mlp_fc1'])
        x = [xi.relu() for xi in x] # 非线性激活
        x = linear(x, state_dict[f'layer{li}.mlp_fc2'])
        x = [a + b for a, b in zip(x, x_residual)]

    logits = linear(x, state_dict['lm_head'])
    return logits
```

### 关键解读：隐式 Causal Masking

在标准的 PyTorch 实现中，我们会传入一个矩阵，然后用一个上三角掩码（Mask）将未来位置的注意力分数设为 $-\infty$。
但在 `microgpt` 中，根本不需要 Mask！
因为它是**按时间步循环**的：

1.  计算第 $t$ 步时，`keys` 和 `values` 列表里只有 $0$ 到 $t$ 步的数据。
2.  模型**物理上**无法看到未来的数据（$t+1$ 还没计算呢）。
3.  这完美地模拟了推理时的行为（KV Cache），同时也自然满足了 GPT 的自回归性质。

---

## 6. 训练循环 (Lines 146-185)

实现了完整的训练流程，包括优化器。

### Adam 优化器 (手动实现)

```python
learning_rate, beta1, beta2, eps_adam = 0.01, 0.85, 0.99, 1e-8
# m: 一阶矩 (Momentum)，平滑梯度方向
# v: 二阶矩 (RMSProp)，自适应调整学习率（大梯度的参数学习率降低，小梯度的参数学习率增加）
m = [0.0] * len(params)
v = [0.0] * len(params)
```

Karpathy 手写了标准的 Adam 更新公式：

1.  $m_t = \beta_1 m_{t-1} + (1-\beta_1) g_t$
2.  $v_t = \beta_2 v_{t-1} + (1-\beta_2) g_t^2$
3.  偏差修正 (Bias Correction): $\hat{m} = m / (1-\beta_1^t), \hat{v} = v / (1-\beta_2^t)$
4.  参数更新: $\theta = \theta - \eta \cdot \hat{m} / (\sqrt{\hat{v}} + \epsilon)$

### Forward & Backward 流程

```python
for step in range(num_steps):
    # ...
    # 每次处理一个完整的序列 (Sequence)
    # 清空 KV Cache
    keys, values = [[] ...], [[] ...]
    losses = []

    # 逐 Token 前向传播
    for pos_id in range(n):
        # 运行 GPT，构建巨大的计算图
        logits = gpt(token_id, pos_id, keys, values)

        # 计算 Cross Entropy Loss (交叉熵损失)
        # loss = -log(prob_of_correct_token)
        probs = softmax(logits)
        loss_t = -probs[target_id].log()
        losses.append(loss_t)

    loss = (1 / n) * sum(losses) # 平均损失

    # 反向传播
    loss.backward() # 这一行代码会触发整个图的遍历，计算出所有 params 的 .grad

    # 参数更新 & 梯度清零
    # ...
```

---

## 7. 推理 (Inference) (Lines 186-200)

训练完成后，使用模型生成新的名字。

```python
# 采样循环
temperature = 0.5 # 温度：越低越保守，越高越随机
for pos_id in range(block_size):
    logits = gpt(token_id, pos_id, keys, values)

    # 温度采样技巧
    # logits / temp: 如果 temp < 1，logits 的差异被放大，softmax 后高概率的更高 -> 更保守
    # 如果 temp > 1，logits 差异被缩小，分布趋向均匀 -> 更随机
    probs = softmax([l / temperature for l in logits])

    # 根据概率分布随机选择下一个 token
    token_id = random.choices(..., weights=...)[0]

    # 自回归: 生成的 token 成为下一次的输入
```

---

## 总结

这份代码的精髓在于**Autograd 与 Transformer 的无缝结合**。它没有使用任何黑盒 API。

- 当你看到 `loss.backward()` 时，你知道它只是在执行几十行代码定义的拓扑排序和链式乘法。
- 当你看到 Attention 时，你知道它只是几行列表推导式实现的加权求和。
- 当你看到 KV Cache 时，你明白它只是两个不断 `append` 的列表。

这就是 GPT 的全部秘密：**简单的数学运算，通过巨大的计算图连接，并通过海量数据进行参数微调。**
