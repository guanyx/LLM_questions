# 文生图推理流程组图分镜 6 Prompt（以“夕阳下奔跑的猫”为例）

Create a technical workflow diagram panel image with the following specifications:

**Main Title (Center):** 为什么会越来越像那只猫
**Subtitle:** 以“夕阳下奔跑的猫”为例，看懂 guidance 和求解器如何把 latent 从高噪声推向低噪声

**Layout Style:**

- Clean, minimalist technical illustration style
- Hand-drawn line art icons and elements
- Left-to-right progression layout with dual branches on the left, guidance fusion in the center, and a solver-driven noise-reduction trajectory on the right
- Nodes have varying sizes (Large/Medium/Small) for dynamic visual rhythm
- White to light gray gradient background (#F5F5F5 to #FFFFFF)

**Workflow Steps (arranged as a guided transition pipeline with dynamic sizing):**
*(CRITICAL: The conditional and unconditional branches must merge into guidance 合成 first, then flow into the solver, then advance the latent from sigma_k to sigma_{k+1}; do not re-explain tokenization or draw the decoder)*

1. [Left-Top, Medium] 条件分支输出: A conditional prediction branch represents the model output when it listens to the prompt-derived condition, preserving the desired subject, motion, lighting, and style cues. (Icon: conditioned branch panel with semantic tags, guided vector strip, and highlighted prompt markers)
2. [Left-Bottom, Medium] 无条件分支输出: An unconditional prediction branch represents the model output without the prompt condition, providing a baseline direction for comparison and control. (Icon: neutral branch panel with muted vector strip, baseline markers, and unlabeled feature path)
3. [Center, Large] guidance 合成: The two branches are combined through a controllable guidance mechanism that determines how strongly the process follows the prompt signal. (Icon: guidance fusion block with dual-input mixer, scale slider, and weighted combination arrows)
4. [Center-Lower, Small] guidance scale: A compact control element indicates how strongly the conditional branch pulls the result toward the desired prompt. (Icon: adjustable scale knob, control slider, and amplification gauge)
5. [Right-Center, Large] 求解器: The solver takes the guided update direction and moves the latent to the next timestep according to the numerical update rule. (Icon: solver module with step-update arrow, integration brackets, and state transition block)
6. [Right-Top, Medium] latent @ sigma_k: The current latent state is shown at a higher-noise stage before the solver update. (Icon: coarse latent thumbnail, high-noise halo, and sigma_k marker)
7. [Right-Middle, Medium] latent @ sigma_{k+1}: The next latent state is shown after one update step, slightly more organized and closer to the target structure. (Icon: refined latent thumbnail, reduced-noise ring, and sigma_{k+1} marker)
8. [Right-Bottom, Medium] 更低噪声阶段: A continuation track indicates that the same process keeps pushing the latent toward lower-noise, more coherent states. (Icon: descending noise trajectory, sequential state dots, and lower-noise arrow band)
9. [Bottom, Large] 三阶段时间轴: A horizontal timeline summarizes the visual evolution across "前期 / 中期 / 后期" using three latent thumbnails labeled "粗结构 / 中间态 / 细节增强". (Icon: three-stage latent strip with evolving detail blocks and high-to-low noise guide)

**Visual Elements to Include:**

- Hand-drawn style icons representing each step in dynamically varied sizes
- Two solid arrows from 条件分支输出 and 无条件分支输出 into guidance 合成
- One clear arrow from guidance 合成 into 求解器
- A forward update arrow from 求解器 to latent @ sigma_{k+1}
- A rightward or downward trajectory showing "高噪声 -> 低噪声" aligned with the latent progression direction
- Soft pastel color blocks (#3498DB, #2ECC71, #F39C12, #9B59B6) highlighting key areas with 20-30% opacity
- Technical decorative elements: guidance weights / sigma labels / update ticks scattered asymmetrically
- Trajectory arrows / state markers / control gauges / latent transition brackets
- A side note near guidance labeled "控制有多听 prompt"
- A side note near the solver labeled "按预测方向把 latent 推到下一时刻"
- A timeline note for "前期：先稳住构图和大结构"
- A timeline note for "中期：稳定主体、动作、光影关系"
- A timeline note for "后期：补局部细节、质感和边缘"
- Small gear icons, abstract nodes, and circuit-like decorative elements in light gray

**Typography:**

- Main title: Bold, extra large (72-96pt equivalent), black (#1A1A1A), strictly centered in the top area
- Subtitle: Medium weight (36-48pt equivalent), below title, centered
- Step labels: Clear, dynamically sized to match their nodes, dark gray (#4A4A4A)
- Technical annotations: Small (14-18pt equivalent), light gray (#8A8A8A)
- Progress annotation: Add the Chinese label "高噪声 -> 低噪声" along the main trajectory

**Color Palette:**

- Background: #F8F9FA to #FFFFFF gradient
- Accent colors: #3498DB for conditional guidance information, #9B59B6 for latent states and noise trajectory, #2ECC71 for solver updates and forward movement, #F39C12 for emphasis highlights
- Text: #1A1A1A (title), #4A4A4A (body), #8A8A8A (annotations)
- Icons: #2C3E50 with colored fills matching accent palette

**Bottom Element:**

- Add a centered mini workflow label "条件分支 + 无条件分支 -> guidance 合成 -> 求解器 -> latent @ sigma_{k+1}" with clear unidirectional arrows

**Style Notes:**

- Use clean, professional line work with slight hand-drawn quality
- Maintain visual hierarchy: title > guidance and solver flow > latent transition trajectory > stage timeline > decorative elements
- Include subtle shadows and depth through layering
- Balance technical precision with approachable, friendly aesthetics
- Ensure Chinese and English text are both clearly legible
- Make the panel feel like a controlled optimization path rather than a black-box magic step
- Do not re-explain token, 文本编码器, or prompt preprocessing
- Do not draw the decoder or final RGB image

**Composition:**

- Aspect ratio: 3:4
- Leave adequate white space around elements (minimum 80px margins)
- Keep the title block compact at the top, place the branch fusion and solver path in the main body, and anchor the three-stage timeline at the bottom so the eye reads from control to transition to visual evolution
- Balance density: dense in the central transition path, spacious in the outer background for clarity
