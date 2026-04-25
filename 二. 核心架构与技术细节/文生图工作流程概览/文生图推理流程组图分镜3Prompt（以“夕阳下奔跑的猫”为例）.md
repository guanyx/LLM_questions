# 文生图推理流程组图分镜 3 Prompt（以“夕阳下奔跑的猫”为例）

Create a technical workflow diagram panel image with the following specifications:

**Main Title (Center):** 正式采样前，先准备 latent 画布
**Subtitle:** 以“夕阳下奔跑的猫”为例，看懂 seed、尺寸、sigma 时间表、采样器如何决定起点

**Layout Style:**

- Clean, minimalist technical illustration style
- Hand-drawn line art icons and elements
- Centralized dashboard composition with a dominant latent canvas in the middle and four preparation modules arranged around it
- Nodes have varying sizes (Large/Medium/Small) for dynamic visual rhythm
- White to light gray gradient background (#F5F5F5 to #FFFFFF)

**Workflow Steps (arranged around a central latent canvas with dynamic sizing):**
*(CRITICAL: All four preparation items must point into the central "初始 latent（随机噪声）"; do not introduce text-condition routing or 去噪模块 internals in this panel)*

1. [Center, Large] 初始 latent（随机噪声）: A central latent canvas appears as an abstract noise matrix in latent space, shown as a structured purple field of compressed visual information rather than visible pixels. (Icon: latent tensor grid, layered noise cloud, and matrix coordinate frame)
2. [Top-Left, Medium] seed: A preparation module defines the random starting point, emphasizing reproducible initialization rather than semantic meaning. (Icon: seed register panel with numeric seed slots, random-state dial, and reset indicator)
3. [Top-Right, Medium] 输出尺寸 / 宽高比: A size module determines the latent canvas shape and resolution footprint before sampling begins. (Icon: aspect-ratio frame selector, width-height ruler marks, and bounding-box presets)
4. [Bottom-Left, Medium] sigma 时间表: A schedule module describes how the process moves from high noise to low noise over time, represented as a descending curve rather than a final image path. (Icon: sigma decay chart, descending curve axis, and high-to-low noise markers)
5. [Bottom-Right, Medium] 采样器 / 求解器: A solver module controls how each update step will be calculated during the later iterative process. (Icon: sampler control panel with stepper knobs, solver branching options, and update-rule symbol blocks)

**Visual Elements to Include:**

- Hand-drawn style icons representing each step in dynamically varied sizes
- Four solid directional arrows from the preparation modules into the central latent canvas
- A visible sigma side curve labeled "高噪声 -> 低噪声" near the sigma 时间表 module
- Soft pastel color blocks (#3498DB, #2ECC71, #F39C12, #9B59B6) highlighting key areas with 20-30% opacity
- Technical decorative elements: latent tensor coordinates / random seed digits / schedule ticks scattered asymmetrically
- Matrix cells / axis labels / parameter dials / compact solver symbols
- A short note near seed labeled "决定随机起点"
- A short note near size labeled "决定 latent 空间大小"
- A short note near sigma labeled "从高噪声走向低噪声"
- A short note near sampler labeled "决定每一步怎么更新"
- Small gear icons, abstract nodes, and circuit-like decorative elements in light gray

**Typography:**

- Main title: Bold, extra large (72-96pt equivalent), black (#1A1A1A), strictly centered in the top area
- Subtitle: Medium weight (36-48pt equivalent), below title, centered
- Step labels: Clear, dynamically sized to match their nodes, dark gray (#4A4A4A)
- Technical annotations: Small (14-18pt equivalent), light gray (#8A8A8A)
- Footer conclusion: Add a short Chinese sentence at the bottom, "模型不是直接在像素画布上起稿，而是在潜空间里从噪声出发"

**Color Palette:**

- Background: #F8F9FA to #FFFFFF gradient
- Accent colors: #9B59B6 for latent/noise structures, #3498DB for parameter panels, #2ECC71 for schedule and directional cues, #F39C12 for emphasis highlights
- Text: #1A1A1A (title), #4A4A4A (body), #8A8A8A (annotations)
- Icons: #2C3E50 with colored fills matching accent palette

**Bottom Element:**

- Add a centered mini workflow label "seed / 尺寸 / sigma 时间表 / 采样器 -> 初始 latent" with clear unidirectional arrows

**Style Notes:**

- Use clean, professional line work with slight hand-drawn quality
- Maintain visual hierarchy: title > central latent canvas > four preparation modules > annotations > decorative elements
- Include subtle shadows and depth through layering
- Balance technical precision with approachable, friendly aesthetics
- Ensure Chinese and English text are both clearly legible
- Make the panel feel like a setup console for latent-space generation rather than a result page
- Do not show text-condition routing, CFG composition, 去噪模块 internals, or final decoded RGB images

**Composition:**

- Aspect ratio: 3:4
- Leave adequate white space around elements (minimum 80px margins)
- Keep the title block compact at the top, place the large latent canvas in the center, and arrange the four preparation modules around it like a clean instrument dashboard
- Balance density: dense around the center and module ring, spacious in the outer background for clarity
