# 浏览器里的 LLM：WebGPU 推理全流程（WASM → WGSL 着色器 → 零后端部署）

目标：从用户打开网页加载模型开始，串起浏览器端推理的完整链路：模型下载与转换 → 引擎初始化（WASM + WebGPU）→ 算子编译（WGSL）→ 数据搬运 → GPU 并行计算 → 结果回传

---

## 1. 模型加载与格式准备（把“大象”装进浏览器）

1. **格式转换（Hugging Face → ONNX/GGUF）**：把 PyTorch/Safetensors 权重转换为浏览器能读取的通用格式（ONNX）或量化格式（如 .q4f16.onnx）（为了跨平台兼容且压缩体积，让普通笔记本显存能塞下）
2. **分块下载与缓存（Cache API）**：利用浏览器 Cache API 分块下载模型权重（shard），并存入本地硬盘（为了避免每次刷新网页都重新下载 2GB 文件）
3. **精度适配（DataType Selection）**：根据设备能力选择 fp32（默认）、fp16 或 int4/int8 量化版本（为了在显存有限的集显/手机上也能跑起来）

---

## 2. 推理引擎初始化（WASM 胶水与 GPU 握手）

1. **WASM 虚拟机启动（Transformers.js / ONNX Runtime Web）**：加载 `.wasm` 文件，启动一个轻量级的 WebAssembly 运行时（为了在 JS 和底层 C++ 引擎之间架起桥梁，因为 JS 跑不动重计算）
2. **请求 GPU 适配器（Navigator.gpu.requestAdapter）**：JS 向浏览器申请访问物理显卡（为了确认设备是否有 GPU 以及支持哪些特性）
3. **创建 WebGPU 设备（Device & Queue）**：获取逻辑设备实例和命令队列（为了建立一条向 GPU 发送指令的专用通道）

---

## 3. 算子编译与管线构建（把计算图翻译成“显卡语”）

1. **计算图解析（Graph Capture）**：ONNX Runtime 解析模型的计算图（MatMul, Softmax, RMSNorm 等算子）（为了知道一共有多少步工序，谁先谁后）
2. **WGSL 着色器生成（Shader Generation）**：把每一个算子逻辑翻译成 WebGPU Shading Language (WGSL) 代码（为了让 GPU 核心能听懂计算指令，因为 GPU 不懂 Python 或 JS）
3. **管线编译（CreateComputePipeline）**：浏览器驱动把 WGSL 编译成显卡机器码（Async Pipeline Creation）（为了极致性能，通常是异步进行避免卡死主线程）

---

## 4. 输入传输（CPU → GPU 的“零拷贝”搬运）

1. **Tokenization（在 CPU 完成）**：JS 运行分词器把文本转成 ID 列表（Int32Array）（这一步计算量小，通常在 CPU 做）
2. **创建映射缓冲区（Mapped Buffer）**：在显存里申请一块 GPU 和 CPU 都能访问的内存区域（为了数据交换）
3. **数据写入与解映射（Write & Unmap）**：把 Token ID 写入缓冲区，然后切断 CPU 访问，把控制权交给 GPU（为了防止读写冲突，WebGPU 要求数据在计算时 CPU 不能乱动）

---

## 5. GPU 并行计算（Compute Pass：全速运转）

这一步是浏览器的“黑科技”时刻，数千个 GPU 核心同时开工。

1. **指令编码（Command Encoding）**：JS 录制一系列 GPU 指令（SetPipeline, SetBindGroup, DispatchWorkgroups）（为了减少 JS 与 GPU 的交互开销，一次性打包发送）
2. **派发工作组（Dispatch Workgroups）**：启动 Compute Shader，将大矩阵乘法拆分成无数个 4x4 或 8x8 的小块，分发给 GPU 的计算单元（EU/CUDA Cores）（为了利用 GPU 的海量并发能力）
3. **层层推进（Kernel Execution）**：每一层 Transformer 的输出直接作为下一层的输入留在显存里（为了避免数据在 CPU 和 GPU 之间反复倒腾，通过“显存驻留”实现零拷贝）

---

## 6. 结果回传与解码（从“黑盒”里捞出答案）

1. **读取回传缓冲区（Readback Buffer）**：计算结束后，将最后一层的 Logits 从显存复制回可读缓冲区（MapAsync & GetMappedRange）（这是最耗时的一步之一，因为 PCIe 总线带宽有限）
2. **采样与解码（Sampling & Detokenization）**：在 CPU（JS/WASM）上根据 Logits 选出下一个 Token，并转回文本（为了处理 Top-k/Top-p 等复杂的逻辑分支，这部分逻辑简单更适合 CPU）
3. **KV Cache 更新（显存内操作）**：把新计算的 K/V 向量留在显存里，供下一个 Token 生成时复用（为了不重算历史）

---

## 7. 工程级优化（让网页不卡顿的魔法）

1. **IO Binding**：强制让所有中间结果都留在 GPU 显存，只有最后的 Logits 回传（为了彻底消灭 CPU-GPU 传输瓶颈）
2. **WebGPU PagedAttention（前沿）**：在显存里实现类似 vLLM 的分页内存管理（为了在浏览器有限的显存里跑长文本）
3. **WASM 多线程与 SIMD**：如果用户没有 GPU，回退到 WASM 时利用多线程和 SIMD 指令加速 CPU 推理（为了保底体验）

一句话总结：浏览器端 LLM 推理就是把浏览器变成了一个“临时显卡驱动”，通过 WebGPU 这条专线，指挥本地显卡直接替网页干重活，彻底告别了“云端排队”和“隐私裸奔”。
