# 文生图推理流程组图分镜 4 Prompt（以“夕阳下奔跑的猫”为例）

Create a technical workflow diagram panel image with the following specifications:

**Main Title (Center):** 采样不是一次出图，而是一个循环
**Subtitle:** 以“夕阳下奔跑的猫”为例，看懂 step k 到 step k+1 的 latent 迭代骨架

**Layout Style:**

- Clean, minimalist technical illustration style
- Hand-drawn line art icons and elements
- Circular loop workflow composition with a changing latent preview in the center and four loop stages around it
- Nodes have varying sizes (Large/Medium/Small) for dynamic visual rhythm
- White to light gray gradient background (#F5F5F5 to #FFFFFF)

**Workflow Steps (arranged as a closed sampling loop with dynamic sizing):**
*(CRITICAL: The loop arrows must close to show step k -> step k+1; keep the panel at the skeleton level of the iteration and do not explain 去噪器 internals or guidance formulas)*

1. [Center, Large] 当前 latent: A central latent thumbnail shows the evolving hidden state at step k, changing gradually instead of becoming a final image. (Icon: evolving latent patch, layered purple feature cloud, and step marker ring)
2. [Top, Medium] 读取当前时间 / sigma: The loop reads the current noise stage and timestep metadata for this iteration. (Icon: sigma clock dial, timestep indicator arc, and stage marker panel)
3. [Right, Medium] 准备当前 latent: The current latent state is packaged as the model input for the current iteration, preserving structure from the previous step. (Icon: latent packet frame, state buffer panel, and tensor snapshot tile)
4. [Bottom, Large] 送入去噪器: The current latent, current stage, and text condition are sent into the 去噪器 module to compute the next update direction. (Icon: input fusion block with latent inlet, sigma inlet, text-condition side port, and processing chamber)
5. [Left, Medium] 得到更新方向，进入下一步: The model returns a correction direction that moves the latent from step k toward step k+1 rather than generating a visible picture directly. (Icon: update vector arrow, delta panel, and transition marker from k to k+1)
6. [Far-Right, Small] 文本条件: A side input representing the prompt-derived text condition enters only as an auxiliary input to the 去噪步骤. (Icon: semantic condition card, side-channel connector, and labeled text feature strip)
7. [Lower-Right, Small] optional: A small placeholder branch indicates an optional unconditional path, but without expanding any classifier-free guidance combination details. (Icon: faint optional branch node, dashed placeholder line, and muted auxiliary slot)

**Visual Elements to Include:**

- Hand-drawn style icons representing each step in dynamically varied sizes
- A fully closed circular arrow loop connecting the four main stages around the center
- A visible step transition label such as "step k -> step k+1" along one segment of the loop
- A side arrow from "文本条件" into the 去噪步骤 only
- A faint dashed optional branch near the 去噪步骤 labeled "optional"
- Soft pastel color blocks (#3498DB, #2ECC71, #F39C12, #9B59B6) highlighting key areas with 20-30% opacity
- Technical decorative elements: timestep ticks / sigma labels / latent state boxes scattered asymmetrically
- Loop arrows / state buffers / update vectors / compact process brackets
- A central note labeled "每一步都在回答：现在画到哪了？下一步往哪修？"
- Small gear icons, abstract nodes, and circuit-like decorative elements in light gray

**Typography:**

- Main title: Bold, extra large (72-96pt equivalent), black (#1A1A1A), strictly centered in the top area
- Subtitle: Medium weight (36-48pt equivalent), below title, centered
- Step labels: Clear, dynamically sized to match their nodes, dark gray (#4A4A4A)
- Technical annotations: Small (14-18pt equivalent), light gray (#8A8A8A)
- Current step annotation: Add a Chinese label "当前时间 / sigma_k" near the top stage

**Color Palette:**

- Background: #F8F9FA to #FFFFFF gradient
- Accent colors: #9B59B6 for latent and loop state, #3498DB for text-condition input, #2ECC71 for directional updates, #F39C12 for loop emphasis highlights
- Text: #1A1A1A (title), #4A4A4A (body), #8A8A8A (annotations)
- Icons: #2C3E50 with colored fills matching accent palette

**Bottom Element:**

- Add a centered mini workflow label "读取当前时间 / sigma -> 准备当前 latent -> 送入去噪器 -> 得到更新方向 -> 下一步" with loop emphasis

**Style Notes:**

- Use clean, professional line work with slight hand-drawn quality
- Maintain visual hierarchy: title > central latent state > loop stages > side condition input > decorative elements
- Include subtle shadows and depth through layering
- Balance technical precision with approachable, friendly aesthetics
- Ensure Chinese and English text are both clearly legible
- Make the panel feel like an iterative process map rather than a component deep dive
- Do not explain cross-attention internals, guidance scale tuning, or classifier-free guidance formulas
- Do not show a final RGB image anywhere in the panel

**Composition:**

- Aspect ratio: 3:4
- Leave adequate white space around elements (minimum 80px margins)
- Keep the title block compact at the top, place the changing latent state in the center, distribute the four loop stages evenly around it, and keep side inputs visually secondary to the main closed loop
- Balance density: dense along the circular loop, spacious in the outer background for clarity
