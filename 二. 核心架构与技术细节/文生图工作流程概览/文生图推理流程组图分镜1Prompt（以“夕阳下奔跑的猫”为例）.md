# 文生图推理流程组图分镜 1 Prompt（以“夕阳下奔跑的猫”为例）

Create a technical workflow diagram panel image with the following specifications:

**Main Title (Center):** Prompt 如何变成模型输入
**Subtitle:** 以“夕阳下奔跑的猫”为例，看懂文本如何被切分并映射成 token ID

**Layout Style:**

- Clean, minimalist technical illustration style
- Hand-drawn line art icons and elements
- Left-to-right three-stage pipeline composition with strong directional flow
- Nodes have varying sizes (Large/Medium/Small) for dynamic visual rhythm
- White to light gray gradient background (#F5F5F5 to #FFFFFF)

**Workflow Steps (arranged as a linear pipeline with dynamic sizing):**
*(CRITICAL: Keep the main flow strictly as Prompt text -> token sequence -> token ID sequence, and do not introduce image generation modules)*

1. [Left, Large] Prompt 预处理: A Chinese prompt card displays "一只在夕阳下奔跑的猫，金色逆光，草地，动态感，写实风格", with subtle normalization marks indicating punctuation cleanup and wording standardization before tokenization. (Icon: hand-drawn text prompt panel with edit marks, bracket guides, and a preprocessing filter strip)
2. [Center, Medium] 切分为 token: The prompt is split into discrete token blocks such as "一只", "夕阳", "奔跑", "猫", and "写实风格", shown as separated modular text tiles with clear spacing and segmentation cues. (Icon: segmented token tiles, dashed cutting guides, and a tokenization splitter module)
3. [Right, Large] 映射成 token ID: The token blocks are transformed into neat rows of abstract integer IDs such as "1024", "381", and "9088", emphasizing machine-readable discrete inputs rather than semantic understanding. (Icon: ordered numeric ID blocks, embedding index grid, and a lookup table panel)

**Visual Elements to Include:**

- Hand-drawn style icons representing each step in dynamically varied sizes
- Solid directional arrows connecting the three stages strictly from left to right
- Soft pastel color blocks (#3498DB, #2ECC71, #F39C12, #9B59B6) highlighting key areas with 20-30% opacity
- Technical decorative elements: prompt text snippets / token boundary markers / vocabulary index tables scattered asymmetrically
- Monospace ID grids / preprocessing annotations / discrete sequence brackets
- A small side note near the first stage labeled "统一写法，减少表达扰动"
- Small gear icons, abstract nodes, and circuit-like decorative elements in light gray

**Typography:**

- Main title: Bold, extra large (72-96pt equivalent), black (#1A1A1A), strictly centered in the top area
- Subtitle: Medium weight (36-48pt equivalent), below title, centered
- Step labels: Clear, dynamically sized to match their nodes, dark gray (#4A4A4A)
- Technical annotations: Small (14-18pt equivalent), light gray (#8A8A8A)
- Footer conclusion: Add a short Chinese sentence at the bottom, "这一步还没有开始画图，只是把人话变成机器输入"

**Color Palette:**

- Background: #F8F9FA to #FFFFFF gradient
- Accent colors: #3498DB for prompt text and condition hints, #2ECC71 for token segmentation guides, #9B59B6 for discrete sequence structure, #F39C12 for attention accents
- Text: #1A1A1A (title), #4A4A4A (body), #8A8A8A (annotations)
- Icons: #2C3E50 with colored fills matching accent palette

**Bottom Element:**

- Add a centered mini workflow label "Prompt 文本 -> token 序列 -> token ID 序列" with clear unidirectional arrows

**Style Notes:**

- Use clean, professional line work with slight hand-drawn quality
- Maintain visual hierarchy: title > three-stage pipeline > annotations > decorative elements
- Include subtle shadows and depth through layering
- Balance technical precision with approachable, friendly aesthetics
- Ensure Chinese and English text are both clearly legible
- Make the diagram feel educational and precise, like an annotated systems infographic
- Do not show text encoder internals, semantic cards, latent noise, decoded images, or any downstream generation modules

**Composition:**

- Aspect ratio: 3:4
- Leave adequate white space around elements (minimum 80px margins)
- Keep the title block compact at the top, place the three-stage pipeline in the main body, and reserve a narrow bottom area for the concluding sentence and mini workflow label
- Balance density: dense in the central pipeline, spacious around the outer edges for clarity
