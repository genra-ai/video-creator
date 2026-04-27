---
name: Persona Switch
description: "Upload a portrait to transform into a new character."
agent_description: "Use this skill when the user wants to transform a portrait photo into a specific character or look: upload a portrait as img2img reference, generate the transformed image or video in the target form (superhero, fantasy character, baby, cartoon etc.), with optional before/after comparison output. Triggered by: 'transform', 'turn into superhero', 'change my look', 'persona switch', 'character transformation', 'turn me into XX'."
---

# Persona Switch

Transforms a user portrait photo into a specified target character. Core: uses img2img to preserve the user's facial features as much as possible, then re-renders under the target character's appearance settings — letting the user "become" another character.

## Key Principles

- **User's facial features are the img2img reference**: face contour and facial proportions remain recognizable as the same person after transformation
- **Target character description must be specific**: don't just write "superhero" — describe the outfit, power feel, and environment clearly
- **Single shot as default**: generates the transformed static image or short animated video (3–5s)
- **Comparison version optional**: when generating before/after comparison, use two shots to show original and target character separately

## Supported Transformation Types & Prompt Templates

| Transformation Type | Core Prompt Elements | Effect Description |
|---|---|---|
| Superhero | `[hero name] costume/armor, superpower light effects, urban/battlefield background, heroic composition` | Batman/Iron Man/Black Widow looks, powerful feel |
| Fantasy warrior | `[fantasy setting] armor, magic light effects, fantasy scene, epic feel` | Medieval knight, elven archer, dark mage etc. |
| Baby transformation | `baby version, chubby cheeks, large eyes, small nose, toddler proportions, same hair color` | Transforms adult into baby/toddler version |
| Ancient / historical character | `[dynasty] costume, ancient scene, [general/scholar/immortal] temperament` | Hanfu, armor, xianxia style etc. |
| Anime character | `[specific anime style] character design, [anime name] art style` | Transforms into a specific anime's character appearance |
| Zombie / monster | `zombie/monster transformation, pale skin, decayed details, horror aesthetic` | Halloween/horror style transformation |
| Muscular version | `extremely muscular physique, bodybuilder, defined muscles, same face` | Adds exaggerated muscles to the person |

## Workflow

### 1. Upload Portrait, Confirm Transformation Target

Upload user portrait photo, record asset_id. Confirm target transformation character and specific style details.

### 2. Send Shot List

**Single shot transformation version**:
```
Art style: [choose based on target: realistic / cinematic / anime feel]

Shot 1:
- Start frame: reference original image [asset_id], preserve facial features and contour
- Transformation setting: [full target character prompt, see templates above]
- Scene: [background scene matching the target character]
- Composition: half-body or full-body, showing complete transformed look
- Duration: 5s
- Video description: [based on character] person slowly turns body to show full look; or light effect sweeps across body for transformation dynamic feel
```

**Before/after comparison version** (2 shots):
```
Shot 1 (original): reference original image [asset_id], original appearance, natural background, duration 3s, video description: static waiting feel
Shot 2 (transformed): reference original image [asset_id], [target character prompt], duration 5s, video description: [transformation dynamic]
```

### 3. Check Output

| Check Item | Standard |
|---|---|
| Face recognizability | After transformation, can still see the same person's facial contour |
| Target character accuracy | Outfit/appearance matches the transformation target |
| Image quality | Light effects/scene matches the target character |

If face is distorted: increase img2img similarity. If target character feel is insufficient: strengthen the target character keywords in the prompt.

### 4. Export

---

## Resolution

| Use Case | Resolution |
|---|---|
| Social sharing / vertical | 720×1280 (9:16) |
| Square / universal | 720×720 (1:1) |
