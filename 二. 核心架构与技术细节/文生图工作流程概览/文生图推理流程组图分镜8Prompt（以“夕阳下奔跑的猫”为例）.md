# 文生图推理流程组图分镜 8 Prompt（以“夕阳下奔跑的猫”为例）

Create a technical workflow diagram panel image with the following specifications:

**Main Title (Center):** 为什么有时会跑偏
**Subtitle:** 以“夕阳下奔跑的猫”为例，看懂同一句 prompt 为什么有时画得准、有时不稳定

**Layout Style:**

- Clean, minimalist technical illustration style
- Hand-drawn line art icons and elements
- Single-page problem breakdown layout with a flawed central result image and multiple surrounding cause labels
- Nodes have varying sizes (Large/Medium/Small) for dynamic visual rhythm
- White to light gray gradient background (#F5F5F5 to #FFFFFF)

**Workflow Steps (arranged as a cause-analysis board with dynamic sizing):**
*(CRITICAL: The panel should analyze why results drift or fail; do not redraw the full generation pipeline, and do not introduce extra product-layer modules)*

1. [Center, Large] 异常结果示意: A central image shows a mostly correct running cat under sunset light, but with several visible local problems, making it clear that the image is close yet imperfect. (Icon: framed image card with running cat, sunset grass scene, and highlighted error callouts)
2. [Left-Top, Medium] seed 不同: A cause label explains that different random starting points can lead to different final outcomes even under the same prompt. (Icon: seed variation card with shuffled number states and branching random paths)
3. [Left-Center, Medium] prompt 约束不够强: A cause label shows that vague or insufficiently specified prompt constraints can leave too much room for the model to guess. (Icon: prompt card with weak constraint brackets, missing attribute slots, and ambiguity markers)
4. [Left-Bottom, Medium] guidance 过强或过弱: A cause label indicates that guidance strength can be imbalanced, either forcing artifacts or failing to enforce the prompt strongly enough. (Icon: guidance scale gauge with under-driven and over-driven zones)
5. [Right-Top, Medium] 模型先验有限: A cause label indicates that the model's learned prior knowledge is incomplete and may fail on difficult structures or fine details. (Icon: prior-knowledge card with incomplete pattern library and uncertainty markers)
6. [Right-Bottom, Medium] 步数 / 求解器选择不同: A cause label shows that different sampling step counts and solver choices can change stability and fidelity. (Icon: step-count panel with solver selector, tick ladder, and path variation markers)
7. [Center-Inner, Small] 腿部异常: A central error callout highlights distorted or anatomically incorrect leg structure in the cat image. (Icon: red callout tag with limb distortion outline)
8. [Center-Inner, Small] 逆光不自然: A central error callout highlights awkward lighting direction or unrealistic back light glow. (Icon: red callout tag with inconsistent light rays)
9. [Center-Inner, Small] 动作不够像奔跑: A central error callout highlights posture or motion cues that fail to convincingly resemble running. (Icon: red callout tag with broken motion arc)

**Visual Elements to Include:**

- Hand-drawn style icons representing each step in dynamically varied sizes
- Five short arrows from the surrounding cause labels into the central flawed image
- Red problem callouts attached to the central image for "腿部异常", "逆光不自然", and "动作不够像奔跑"
- Soft pastel color blocks (#3498DB, #2ECC71, #F39C12, #9B59B6) highlighting key areas with 20-30% opacity
- Technical decorative elements: seed values / solver ticks / prompt constraint notes scattered asymmetrically
- Cause arrows / warning markers / comparison brackets / issue tags
- A summary note on the left labeled "同一句 prompt，不一定每次都得到完全相同的画面"
- A closing sentence at the bottom labeled "整条流程到解码成图为止，结果是否稳定，取决于前面每一步条件约束和采样推进是否足够准确"
- Small gear icons, abstract nodes, and circuit-like decorative elements in light gray

**Typography:**

- Main title: Bold, extra large (72-96pt equivalent), black (#1A1A1A), strictly centered in the top area
- Subtitle: Medium weight (36-48pt equivalent), below title, centered
- Step labels: Clear, dynamically sized to match their nodes, dark gray (#4A4A4A)
- Technical annotations: Small (14-18pt equivalent), light gray (#8A8A8A)
- Error callouts: Use compact red labels for the three visible failure points in the central image

**Color Palette:**

- Background: #F8F9FA to #FFFFFF gradient
- Accent colors: #3498DB for neutral technical notes, #9B59B6 for generation factors, #F39C12 for emphasis highlights, #E74C3C for risks, failures, and anomaly callouts
- Text: #1A1A1A (title), #4A4A4A (body), #8A8A8A (annotations)
- Icons: #2C3E50 with colored fills matching accent palette

**Bottom Element:**

- Add a centered mini summary label "seed / prompt / guidance / 模型先验 / 步数与求解器 都会影响最终稳定性" with subtle divider lines

**Style Notes:**

- Use clean, professional line work with slight hand-drawn quality
- Maintain visual hierarchy: title > central flawed result image > cause labels > anomaly callouts > decorative elements
- Include subtle shadows and depth through layering
- Balance technical precision with approachable, friendly aesthetics
- Ensure Chinese and English text are both clearly legible
- Make the panel feel like a postmortem analysis board for generation quality
- Do not redraw the complete generation pipeline
- Do not introduce extra application-layer features or product UX content

**Composition:**

- Aspect ratio: 3:4
- Leave adequate white space around elements (minimum 80px margins)
- Keep the title block compact at the top, place the flawed central image in the middle, cluster the five cause labels around it with short inward arrows, and reserve the bottom area for the final takeaway sentence
- Balance density: dense around the center and cause labels, spacious in the outer background for clarity
