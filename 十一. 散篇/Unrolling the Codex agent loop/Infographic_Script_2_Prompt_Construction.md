# 信息图脚本 2：解构 Prompt 构建

**文件名**: `Infographic_Script_2_Prompt_Construction.md`
**尺寸**: 1280 x 1714 px
**背景色**: #F8F9FA
**主题**: Codex 如何“组装”发给模型的 Prompt

## 1. 标题区 (0, 0) - (1280, 250)
- **背景**: #E8F5E9 (浅绿渐变)
- **主标题**: "解构 Prompt：Agent 的上下文拼图"
  - 字体: 粗体无衬线, 72pt, #1B5E20
- **副标题**: "Unrolling the Codex Agent Loop - Part 2/4"
  - 字体: 中等无衬线, 36pt, #388E3C

## 2. API 接入层 (50, 280) - (1230, 500)
- **概念**: "Responses API - 连接任意模型"
- **视觉展示**: 中心辐射图
  - 中心: "Codex CLI" (#C8E6C9 圆形)
  - 射线连接四个端点:
    1. **ChatGPT**: `chatgpt.com/backend-api` (#FFF3E0)
    2. **OpenAI API**: `api.openai.com/v1` (#E1F5FE)
    3. **Local/OSS**: `localhost:11434` (Ollama/LM Studio) (#F3E5F5)
    4. **Azure/Cloud**: 托管服务 (#ECEFF1)

## 3. Prompt 结构层级 (50, 550) - (1230, 1200)
- **核心视觉**: 一个巨大的“层叠蛋糕”或“积木塔”，展示 Prompt 的组成部分。
- **层级 1 (底层/高优先级): System & Instructions**
  - 颜色: #FFECB3 (浅橙)
  - 内容: "Instructions (指令)"
    - 来源: `config.toml` 或模型默认
    - 角色: `system`
- **层级 2: Tools (工具定义)**
  - 颜色: #D1C4E9 (浅紫)
  - 内容: "Tools (工具箱)"
    - 内置: `shell`, `update_plan`
    - API: `web_search`
    - MCP: 用户自定义工具 (如 `weather`)
- **层级 3: Context Inputs (上下文输入)**
  - 颜色: #B3E5FC (浅蓝)
  - 内容: "Input (动态上下文)"
    - **沙箱说明**: `role=developer` (仅限 Shell 安全)
    - **用户指令**: `AGENTS.md`, Skills (`role=user`)
    - **环境**: CWD, Shell 类型 (`role=user`)
- **层级 4 (顶层): Conversation History**
  - 颜色: #FFCCBC (浅红)
  - 内容: "History (对话历史)"
    - 之前的问答、工具调用结果

## 4. 角色优先级阶梯 (50, 1250) - (1230, 1450)
- **视觉**: 一个简单的阶梯或金字塔，强调覆盖规则。
- **顺序**: `System` > `Developer` > `User` > `Assistant`
- **说明**: "Responses API 结构化生成 Prompt，用户无法直接指定原始文本，确保了指令遵循的层级安全。" (#455A64)

## 5. 特别提示：沙箱边界 (50, 1500) - (1230, 1600)
- **样式**: 警告/提示框 (#FFF9C4)
- **图标**: 盾牌 (线性, #FBC02D)
- **文字**: "注意：沙箱限制仅适用于内置 Shell 工具。通过 MCP 引入的第三方工具需自行负责安全边界！"

## 6. 底部信息 (0, 1614) - (1280, 1714)
- **背景**: #ECEFF1
- **导航**: "1. 核心机制 | 2. Prompt 构建 | 3. 执行流 | 4. 性能优化"
  - 当前高亮: "2. Prompt 构建" (#2E7D32)

## 配色方案
- **主色调**: 绿色系 (#E8F5E9, #C8E6C9, #2E7D32)
- **辅助色**: 橙色 (指令), 紫色 (工具), 蓝色 (上下文)
- **无障碍**: 确保所有彩色背景上的文字对比度 > 4.5:1
