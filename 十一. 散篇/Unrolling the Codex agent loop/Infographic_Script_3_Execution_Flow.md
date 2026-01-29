# 信息图脚本 3：执行流与工具调用

**文件名**: `Infographic_Script_3_Execution_Flow.md`
**尺寸**: 1280 x 1714 px
**背景色**: #F8F9FA
**主题**: 实时数据流与工具交互的微观过程

## 1. 标题区 (0, 0) - (1280, 250)
- **背景**: #F3E5F5 (浅紫渐变)
- **主标题**: "执行流：从 SSE 到工具调用"
  - 字体: 粗体无衬线, 72pt, #4A148C
- **副标题**: "Unrolling the Codex Agent Loop - Part 3/4"
  - 字体: 中等无衬线, 36pt, #7B1FA2

## 2. SSE 流式传输 (50, 280) - (1230, 600)
- **标题**: "Server-Sent Events (SSE) 实时流"
- **视觉**: 数据管道图
  - 左侧: 模型服务器
  - 右侧: Codex Client UI
  - 管道内容 (粒子流):
    1. `output_text.delta` (文本块) -> **实时显示在屏幕**
    2. `reasoning_summary` (推理) -> **后台记录 (Encrypted)**
    3. `output_item.done` (完成信号) -> **触发下一步**

## 3. 推理与思维链 (50, 650) - (1230, 900)
- **背景**: #E1BEE7 (微弱紫背景块)
- **概念**: "保持思维连续性"
- **图示**:
  - 步骤 A: 模型输出推理 (`reasoning_summary_text`)
  - 步骤 B: 客户端加密保存
  - 步骤 C: 下一轮次作为 `type=reasoning` (含 `encrypted_content`) 回传给模型
- **意义**: "让模型‘记得’之前的思考过程，同时保持零数据保留 (ZDR) 合规。"

## 4. 工具调用循环详解 (50, 950) - (1230, 1450)
- **视觉**: 详细的步骤分解图 (Step-by-Step)
- **Step 1: 触发 (Trigger)**
  - 收到 `function_call` 事件
  - 示例: `name: "run_shell", args: "ls -la"`
- **Step 2: 执行 (Execute)**
  - Codex 本地执行命令
  - 视觉: 终端窗口图标，显示命令输出
- **Step 3: 回填 (Backfill)**
  - 将执行结果 (`function_call_output`) 格式化
  - 追加到 Prompt 尾部
- **Step 4: 递归 (Recurse)**
  - 发起新的 HTTP 请求 (带上更新后的 Prompt)
  - **关键点**: 新请求包含旧请求作为**精确前缀** -> 触发缓存！

## 5. 底部信息 (0, 1614) - (1280, 1714)
- **背景**: #ECEFF1
- **导航**: "1. 核心机制 | 2. Prompt 构建 | 3. 执行流 | 4. 性能优化"
  - 当前高亮: "3. 执行流" (#6A1B9A)

## 配色方案
- **主色调**: 紫色系 (#F3E5F5, #E1BEE7, #6A1B9A)
- **流数据**: 动态感的粉紫色 (#AB47BC)
- **代码/终端**: 深色背景块 (#263238) 配亮色文字 (#80CBC4) 以展示技术细节
