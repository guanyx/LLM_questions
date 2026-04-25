# 文生图推理流程组图分镜 2 Prompt（以“夕阳下奔跑的猫”为例）

Create a technical workflow diagram panel image with the following specifications:

**Main Title (Center):** 文本编码器如何理解需求
**Subtitle:** 以“夕阳下奔跑的猫”为例，看懂 token ID 如何变成条件表征

**Layout Style:**

- Clean, minimalist technical illustration style
- Hand-drawn line art icons and elements
- Left-to-right semantic analysis layout with a central encoder module and branching output cards
- Nodes have varying sizes (Large/Medium/Small) for dynamic visual rhythm
- White to light gray gradient background (#F5F5F5 to #FFFFFF)

**Workflow Steps (arranged as a branching semantic pipeline with dynamic sizing):**
*(CRITICAL: Keep the main flow strictly as token ID -> 文本编码器 -> 条件表征, then branch into semantic cards; do not connect the encoder directly to a final image)*

1. [Left, Medium] token ID 输入: A compact strip of abstract token IDs enters from the left as discrete machine-readable input, visually aligned as ordered numeric blocks rather than natural language text. (Icon: numeric token ID bar, indexed sequence brackets, and discrete input slots)
2. [Center, Large] 文本编码器: A central encoder module transforms the ID sequence into a structured conditional representation, shown as a dense feature-processing block rather than a chatbot or language bubble. (Icon: encoder architecture block with stacked feature layers, vector channels, and attention routing lines)
3. [Upper-Right, Medium] 条件表征: The encoder emits a unified conditional vector representation that acts as a semantic specification for downstream image generation, without producing pixels yet. (Icon: vector tensor panel, embedding stripes, and labeled semantic channels)
4. [Right-Top, Small] 主体：猫: A semantic card isolates the main subject concept "猫" as the core object to be rendered later. (Icon: subject label card with abstract silhouette outline and entity tag)
5. [Right-Upper-Middle, Small] 动作：奔跑: A semantic card captures motion intent, emphasizing the action state "奔跑" rather than body details. (Icon: motion trajectory card with speed lines and kinematic arrows)
6. [Right-Center, Medium] 环境：草地 / 夕阳: A semantic card describes the scene context and location cues, combining grassland and sunset into a coherent environment condition. (Icon: layered scene card with horizon band, grass texture strip, and sun disk marker)
7. [Right-Lower-Middle, Medium] 光线氛围：金色逆光 / 动态感: A semantic card represents lighting and mood constraints, focusing on back light direction, glow direction, and cinematic motion energy. (Icon: light direction card with golden rim-light rays, glow arcs, and motion streak overlays)
8. [Right-Bottom, Small] 风格：写实: A semantic card specifies the overall rendering style as realistic rather than cartoon, sketch, or abstract. (Icon: style chip card with texture swatches and realism slider marks)
9. [Far-Right, Small] 负面条件: A separate negative condition card lists "不要模糊 / 不要多只猫 / 不要畸形肢体", visually isolated from the positive semantic cards for later guidance control. (Icon: constraint warning card with exclusion marks, red boundary frame, and forbidden attribute tags)

**Visual Elements to Include:**

- Hand-drawn style icons representing each step in dynamically varied sizes
- Solid arrows for the main flow "token ID -> 文本编码器 -> 条件表征"
- Secondary branching arrows from "条件表征" to the five positive semantic cards
- A separate dashed or lightly separated branch for the negative condition card, clearly not merged into the positive card cluster
- Soft pastel color blocks (#3498DB, #2ECC71, #F39C12, #9B59B6) highlighting key areas with 20-30% opacity
- Technical decorative elements: vector annotations / semantic channel labels / embedding strips scattered asymmetrically
- Layered feature maps / compact attention hints / condition routing nodes
- A side note near the encoder output labeled "告诉后面的生成网络该画什么、哪些特征要一起出现"
- A side note near the negative card labeled "在后续 guidance 中用于拉开想要和不想要"
- Small gear icons, abstract nodes, and circuit-like decorative elements in light gray

**Typography:**

- Main title: Bold, extra large (72-96pt equivalent), black (#1A1A1A), strictly centered in the top area
- Subtitle: Medium weight (36-48pt equivalent), below title, centered
- Step labels: Clear, dynamically sized to match their nodes, dark gray (#4A4A4A)
- Technical annotations: Small (14-18pt equivalent), light gray (#8A8A8A)
- Encoder output label: Add the Chinese annotation "条件表征（向量）" near the central output

**Color Palette:**

- Background: #F8F9FA to #FFFFFF gradient
- Accent colors: #3498DB for token IDs and text-side conditions, #2ECC71 for positive semantic cards, #9B59B6 for encoder and vector structures, #F39C12 for scene/light emphasis, #E74C3C for negative condition accents
- Text: #1A1A1A (title), #4A4A4A (body), #8A8A8A (annotations)
- Icons: #2C3E50 with colored fills matching accent palette

**Bottom Element:**

- Add a centered mini workflow label "token ID -> 文本编码器 -> 条件表征" with clear unidirectional arrows

**Style Notes:**

- Use clean, professional line work with slight hand-drawn quality
- Maintain visual hierarchy: title > encoder block > condition representation > semantic cards > decorative elements
- Include subtle shadows and depth through layering
- Balance technical precision with approachable, friendly aesthetics
- Ensure Chinese and English text are both clearly legible
- Make the diagram feel like a semantic specification board, not an image generation result page
- Do not show seed, latent noise, noise-removal steps, guidance formulas, or final RGB images
- Do not draw a direct arrow from the encoder to any finished picture

**Composition:**

- Aspect ratio: 3:4
- Leave adequate white space around elements (minimum 80px margins)
- Keep the title block compact at the top, place the token ID strip on the left, the encoder module in the center, and fan out the semantic cards on the right with a clear visual grouping between positive and negative conditions
- Balance density: dense around the encoder and semantic card cluster, spacious in the outer background for clarity
