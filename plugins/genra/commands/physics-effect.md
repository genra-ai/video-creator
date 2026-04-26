---
name: Physics Effect
description: "Describe a physical effect to animate object deformation."
agent_description: "Use this skill when the user wants to apply exaggerated physical deformation effects to a portrait or object image: supports squish, inflate, melt, and explode effects. Upload a subject photo as start frame, video description drives the corresponding physical deformation animation. Great for fun social content. Triggered by: 'squish effect', 'melt effect', 'inflate effect', 'explode effect', 'physics effect', 'squish', 'melt', 'inflate', 'explode'."
---

# Physics Deformation Effect Video

Turns a user-uploaded portrait or object photo into a short video with exaggerated physical deformation effects. Core: start frame is the real photo, video description drives the subject to squish / melt / inflate / explode.

## Key Principles

- **Start frame = original photo**: use user's photo as start frame img2img reference, initial state is normal
- **The deformation process is the core of the video**: video description precisely describes the dynamic process of deformation
- **Single shot output**: each effect produces one 3–6 second short video
- **No tail frames**

## Four Effects & Video Description Formulas

### Squish
Subject is compressed from above by a great force, body expands to the sides, like clay being pressed flat.

**Video description template**:
> "Subject is pressed by immense force from above, body is gradually squished flat, height reduced to 1/3 of original, width expands sideways, forming a flat oval shape, facial expression deforms accordingly, eyes compressed into slits, finally completely flat and frozen"

---

### Inflate
Subject inflates like a balloon from normal body shape, skin/surface becomes smooth and taut, finally can optionally float up or burst.

**Video description template**:
> "Subject's body begins inflating from inside, limbs and torso gradually become rounder and larger, skin surface becomes smooth and taut, like a balloon getting bigger and bigger, facial features stretched out, finally body floats off the ground and rises slowly"

---

### Melt
Subject melts from the bottom up, body gradually liquefies into flowing liquid and drips down, finally becomes a puddle.

**Video description template**:
> "Subject begins melting into liquid from the feet, liquefaction effect gradually spreads upward, body contour becomes blurry and flowing, colors maintain the same as original subject, melted liquid accumulates on the ground, finally the entire subject is completely liquefied, forming a puddle with reflective effect"

---

### Explode
Subject shatters from the center outward, fragments fly in all directions, finally the subject completely disintegrates into pieces or particles.

**Video description template**:
> "Subject begins cracking from the center point, cracks rapidly spread outward in all directions, subject shatters into dozens of fragments, fragments fly outward in all directions with speed, accompanied by light dust effect, finally the frame only shows floating fragments slowly falling"

---

## Workflow

### 1. Upload Photo, Confirm Effect Type

Upload subject photo, record asset_id. Confirm which of the 4 effects the user wants.

**Subject suggestions**:
- Front-facing portrait works best
- Objects (toys, food, everyday items etc.) also work perfectly
- Clean background helps the deformation effect stand out more

### 2. Send Shot List

```
Art style: realistic feel, physical effects look real and believable

Shot 1:
- Start frame: reference original image [asset_id], subject in original state
- Scene: [clean background, clearly contrasting with subject]
- Duration: 5s
- Video description: [corresponding effect video description template, can be adjusted based on subject characteristics]
```

### 3. Check Output

| Check Item | Standard |
|---|---|
| Initial state | Start frame matches original photo, deformation hasn't started yet |
| Deformation dynamics | Deformation process is clear, has obvious physical feel |
| Effect completeness | Deformation process has beginning, middle, and ending stages |

If deformation feel is insufficient: add more extreme descriptors in the video description, such as "extremely exaggerated" or "completely deformed."

### 4. Export

---

## Resolution

| Use Case | Resolution |
|---|---|
| Social sharing / vertical | 720×1280 (9:16) |
| Square | 720×720 (1:1) |
