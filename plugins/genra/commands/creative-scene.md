---
name: Creative Scene
description: "Describe ideas to generate surreal visual scenes."
agent_description: "Use this skill when the user has a vivid image in their mind and wants to turn it into a video — no brand, no plot, no narration, just the scene itself brought to life. Pure imagination-to-visuals. Triggered by: 'imagine this scene', 'generate a scene', 'make a video of', 'visualize', 'cinematic scene', 'I want to see', 'create a visual of', 'bring this to life', 'turn this into a video', 'generate a video of'."
---

# Creative Scene

Turns a mental image into a video. No brand, no story arc, no narration — just the scene the user sees in their head, made real. The output is visual, atmospheric, and self-contained.

## Key Principles

- **The scene is the content**: no voiceover, no subtitles, no explanation needed
- **Light, texture, and color come first**: these carry the mood more than any action
- **Camera movement must be intentional**: every move (or stillness) is a choice
- **Keep it short and precise**: 1–3 shots is almost always enough; do not pad
- **Image input = start frame**: if the user provides a photo, the video begins from that state and evolves

## Workflow

### 1. Analyze the User's Description

Extract four elements from what the user wrote:

| Element | What to identify |
|---|---|
| **Subject** | Person / animal / object / natural phenomenon / abstract / location |
| **Visual style** | Realistic / cinematic / 3D animation / cartoon / surreal / historical engraving / etc. |
| **Motion type** | Purely atmospheric (slow drift, light shift) / moving subject / environmental change |
| **Mood / tone** | Dark, dreamlike, epic, playful, melancholic, tense, serene, etc. |

If any of these is genuinely ambiguous and would meaningfully change the output, ask one focused question. Do not ask about things that can be inferred from context.

### 2. Decide Shot Count

| Scenario | Shots | Duration per shot |
|---|---|---|
| Single strong image, atmosphere-driven | 1 | 5–8s, slow push or locked-off |
| Movement or transformation present | 2 | 4–6s each, different angle or phase |
| Small narrative moment (not a full story) | 3 | 4–6s each |

Do not exceed 3 shots. This is not a narrative film — it is a visual impression.

### 3. Build Shot Descriptions

Each shot description must include all of the following:

- **Subject detail**: material, color, scale, position within frame
- **Lighting**: source, quality (hard/soft/ambient), color temperature, shadows
- **Color palette**: dominant tones, contrast level
- **Camera**: position (angle, height), movement (locked / slow push / arc / follow), focal length feel (wide / normal / close)
- **Atmosphere detail**: particles, haze, depth-of-field, texture of air

Do NOT write narration, dialogue, or subtitles. Do NOT describe what something "means" — only what it looks like.

**Style reference vocabulary** (choose what fits):

| Style | Key visual language |
|---|---|
| Cinematic realistic | anamorphic lens flare, shallow depth of field, film grain, muted highlights |
| 3D animation | smooth subsurface scattering, stylized proportions, clean ambient occlusion |
| Historical engraving / printmaking | high contrast black-and-white, cross-hatching texture, flat depth |
| Surreal / dreamlike | impossible scale, oversaturated bloom, soft edge blur |
| Dark fantasy | deep shadow pools, desaturated palette, rim lighting in cold blue or amber |
| Cartoon / hand-drawn | flat color fills, visible line weight, bouncy motion anticipation |

### 4. Image Input Handling

If the user provides one or more images:

- Treat each image as a **start frame** for a shot
- Describe the visual change that unfolds from that starting state (e.g., petals begin to fall, the figure turns, light shifts from dawn to midday)
- Do not re-describe what is already in the image — only describe what changes or is added

### 5. Shot List Format

```
Visual style: [one clear descriptor]
Mood: [one or two words]
BGM direction: [optional — ambient texture / orchestral swell / silence / etc.]

Shot 1 (Xs): [full visual description — subject / lighting / color / camera / atmosphere]
Shot 2 (Xs): [full visual description]
Shot 3 (Xs): [full visual description — if needed]
```

### 6. Filter Check

Before generating, confirm:

- No shot contains restricted content (real named individuals depicted in harmful contexts, graphic violence beyond stylistic convention, etc.)
- Style and mood are internally consistent across shots
- Total duration is between 5s and 24s

### 7. Clear All Tail Frames

Remove any auto-generated end frames or fade-to-black padding that was not part of the shot design.

### 8. Generate Video

---

## Resolution

| Use Case | Resolution |
|---|---|
| Default (most creative scenes) | 1280×720 (16:9) |
| Portrait / vertical (user requests it) | 720×1280 (9:16) |
| Square (user requests it) | 720×720 (1:1) |
