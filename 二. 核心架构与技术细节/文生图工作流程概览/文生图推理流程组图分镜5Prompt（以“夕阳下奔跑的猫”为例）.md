# 文生图推理流程组图分镜 5 Prompt（以“夕阳下奔跑的猫”为例）

Create a technical workflow diagram panel image with the following specifications:

**Main Title (Center):** 去噪器到底看到了什么，又输出什么
**Subtitle:** 以“夕阳下奔跑的猫”为例，看懂当前 latent、时间阶段、文本条件如何变成预测修正方向

**Layout Style:**

- Clean, minimalist technical illustration style
- Hand-drawn line art icons and elements
- Center-focused module diagram with one large 去噪器 block, three inputs from the left, and one output to the right
- Nodes have varying sizes (Large/Medium/Small) for dynamic visual rhythm
- White to light gray gradient background (#F5F5F5 to #FFFFFF)

**Workflow Steps (arranged as a central module interface diagram with dynamic sizing):**
*(CRITICAL: All three inputs must merge into the central 去噪器 module, and the output must be "预测修正方向"; do not depict latent updating or final image decoding inside this panel)*

1. [Left-Top, Medium] 当前 latent: The current latent state enters as the present hidden visual draft, representing what the model has already formed so far. (Icon: latent state tile, purple feature patch, and structured tensor frame)
2. [Left-Center, Medium] 当前时间 / sigma: The current timestep and noise stage enter as a control signal telling the model where this iteration sits in the overall process. (Icon: sigma dial, timestep marker strip, and stage gauge)
3. [Left-Bottom, Medium] 文本条件: The prompt-derived condition enters as the target description for what should eventually appear in the image. (Icon: semantic condition card, text feature strip, and attribute tag bundle)
4. [Center, Large] 去噪器: A large central module fuses the three inputs and produces a prediction about how the latent should be corrected next, shown as a technical reasoning block rather than a literal image generator. (Icon: core processing chamber with feature fusion lanes, stacked blocks, and condition injection channels)
5. [Inside-Center, Small] cross-attention / 条件调制: Inside the module, subtle internal arrows indicate that text condition continuously influences intermediate feature layers without exposing full internal math. (Icon: thin internal routing arrows, feature modulation gates, and attention hint overlays)
6. [Right, Large] 预测修正方向: The output is a correction signal rather than a picture, indicating how the latent should move next in the sampling trajectory. (Icon: update vector panel, epsilon-v-x0 label strip, and directional delta arrow)

**Visual Elements to Include:**

- Hand-drawn style icons representing each step in dynamically varied sizes
- Three solid input arrows converging into the central 去噪器 block
- One solid output arrow from 去噪器 to 预测修正方向
- Fine internal arrows from the text condition path to middle feature layers, labeled "持续影响中间特征"
- Soft pastel color blocks (#3498DB, #2ECC71, #F39C12, #9B59B6) highlighting key areas with 20-30% opacity
- Technical decorative elements: feature maps / vector channels / intermediate layer strips scattered asymmetrically
- Compact attention hints / modulation gates / delta symbols / signal brackets
- A side note near the inputs labeled "它同时知道现在长什么样、现在处于哪一步、最终想画成什么"
- A side note near the output labeled "可表示为 epsilon / v / x0，名字不同，作用相近"
- Small gear icons, abstract nodes, and circuit-like decorative elements in light gray

**Typography:**

- Main title: Bold, extra large (72-96pt equivalent), black (#1A1A1A), strictly centered in the top area
- Subtitle: Medium weight (36-48pt equivalent), below title, centered
- Step labels: Clear, dynamically sized to match their nodes, dark gray (#4A4A4A)
- Technical annotations: Small (14-18pt equivalent), light gray (#8A8A8A)
- Footer conclusion: Add a short Chinese sentence at the bottom, "去噪器不是直接吐出最终图，而是告诉求解器下一步往哪推"

**Color Palette:**

- Background: #F8F9FA to #FFFFFF gradient
- Accent colors: #9B59B6 for latent and model internals, #3498DB for text-condition input, #2ECC71 for control and routing cues, #F39C12 for output emphasis highlights
- Text: #1A1A1A (title), #4A4A4A (body), #8A8A8A (annotations)
- Icons: #2C3E50 with colored fills matching accent palette

**Bottom Element:**

- Add a centered mini workflow label "当前 latent + 当前时间 / sigma + 文本条件 -> 去噪器 -> 预测修正方向" with clear unidirectional arrows

**Style Notes:**

- Use clean, professional line work with slight hand-drawn quality
- Maintain visual hierarchy: title > 去噪器 block > input/output paths > internal modulation hints > decorative elements
- Include subtle shadows and depth through layering
- Balance technical precision with approachable, friendly aesthetics
- Ensure Chinese and English text are both clearly legible
- Make the panel feel like an interface and signal-flow diagram for the core image-generation brain
- Do not show the solver updating latent inside this module
- Do not show a final RGB image anywhere in the panel

**Composition:**

- Aspect ratio: 3:4
- Leave adequate white space around elements (minimum 80px margins)
- Keep the title block compact at the top, place the large 去噪器 module in the center, align the three inputs clearly on the left, and reserve the right side for the single output so the information flow reads instantly
- Balance density: dense in the center and on the input/output lanes, spacious in the outer background for clarity
