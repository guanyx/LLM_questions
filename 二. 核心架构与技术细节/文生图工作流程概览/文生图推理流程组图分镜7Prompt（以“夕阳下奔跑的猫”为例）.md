# 文生图推理流程组图分镜 7 Prompt（以“夕阳下奔跑的猫”为例）

Create a technical workflow diagram panel image with the following specifications:

**Main Title (Center):** latent 如何变成真正可见的图片
**Subtitle:** 以“夕阳下奔跑的猫”为例，看懂稳定 latent 如何经过解码器还原成 RGB 图像

**Layout Style:**

- Clean, minimalist technical illustration style
- Hand-drawn line art icons and elements
- Left-to-right decoding pipeline with a stable latent on the left, decoder in the center, and a visible RGB image on the right
- Nodes have varying sizes (Large/Medium/Small) for dynamic visual rhythm
- White to light gray gradient background (#F5F5F5 to #FFFFFF)

**Workflow Steps (arranged as a decoding pipeline with dynamic sizing):**
*(CRITICAL: Keep the main flow strictly as 稳定后的 latent -> latent 数值范围调整 -> 解码器 / VAE -> RGB 图片; emphasize that latent is not a visible image file)*

1. [Left, Large] 稳定后的 latent: A relatively smooth latent state appears as a compressed visual draft in latent space, more organized than earlier noisy states but still not directly viewable as a normal picture. (Icon: smooth latent tile, compressed feature field, and latent-space frame)
2. [Left-Center, Small] latent 数值范围调整: A compact normalization stage adjusts the latent values into the numerical range preferred by the decoder before conversion to pixels. (Icon: value-range adjustment panel, scaling bars, and normalization gauge)
3. [Center, Large] 解码器 / VAE: A central decoder module expands the latent representation from compressed latent space into visible pixel-space structure. (Icon: decoder chamber with expansion arrows, channel unfolding layers, and pixel reconstruction grid)
4. [Right, Large] RGB 图片: A clear final image shows a realistic cat running across grass under golden sunset back light, with motion feeling and photographic texture. (Icon: framed RGB image card with running cat, sunset glow, grass strip, and realism texture cues)

**Visual Elements to Include:**

- Hand-drawn style icons representing each step in dynamically varied sizes
- Solid directional arrows strictly following "稳定后的 latent -> 数值调整 -> 解码器 -> RGB 图片"
- A small annotation near the decoder labeled "把潜空间表示还原到像素空间"
- Soft pastel color blocks (#3498DB, #2ECC71, #F39C12, #9B59B6) highlighting key areas with 20-30% opacity
- Technical decorative elements: latent grids / numeric range markers / pixel channel hints scattered asymmetrically
- Decoder expansion arrows / numeric bars / reconstruction brackets / output frame
- A side note near the latent labeled "latent：压缩过的视觉草稿"
- A side note near the range-adjustment stage labeled "解码前：调整到解码器习惯的数值范围"
- A side note near the output image labeled "解码后：展开为肉眼可见的 RGB 图像"
- Small gear icons, abstract nodes, and circuit-like decorative elements in light gray

**Typography:**

- Main title: Bold, extra large (72-96pt equivalent), black (#1A1A1A), strictly centered in the top area
- Subtitle: Medium weight (36-48pt equivalent), below title, centered
- Step labels: Clear, dynamically sized to match their nodes, dark gray (#4A4A4A)
- Technical annotations: Small (14-18pt equivalent), light gray (#8A8A8A)
- Footer conclusion: Add a short Chinese sentence at the bottom, "用户真正看到的第一张图，是解码后的结果，不是 latent 本身"

**Color Palette:**

- Background: #F8F9FA to #FFFFFF gradient
- Accent colors: #9B59B6 for latent-space structures, #3498DB for adjustment and numeric cues, #2ECC71 for directional flow, #F39C12 for decoded image highlights
- Text: #1A1A1A (title), #4A4A4A (body), #8A8A8A (annotations)
- Icons: #2C3E50 with colored fills matching accent palette

**Bottom Element:**

- Add a centered mini workflow label "稳定后的 latent -> 数值调整 -> 解码器 / VAE -> RGB 图片" with clear unidirectional arrows

**Style Notes:**

- Use clean, professional line work with slight hand-drawn quality
- Maintain visual hierarchy: title > decoder pipeline > final RGB output > annotations > decorative elements
- Include subtle shadows and depth through layering
- Balance technical precision with approachable, friendly aesthetics
- Ensure Chinese and English text are both clearly legible
- Make the panel feel like a representation-conversion diagram from latent space to pixel space
- Do not show the sampling loop again
- Do not include super-resolution, safety filtering, or post-processing product layers

**Composition:**

- Aspect ratio: 3:4
- Leave adequate white space around elements (minimum 80px margins)
- Keep the title block compact at the top, place the latent and adjustment stages on the left, anchor the decoder in the center, and reserve the right side for the clean final RGB image so the transformation reads instantly
- Balance density: dense along the decoding pipeline, spacious in the outer background for clarity
