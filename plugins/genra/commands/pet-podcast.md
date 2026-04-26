---
name: pet-podcast
description: "Use this skill when the user wants to generate a fun video of their pet 'hosting a podcast': upload a pet photo, generate a short video of the pet sitting in front of a microphone, speaking like a human, mimicking a real podcast recording scene. Triggered by: 'pet podcast', 'make my cat/dog talk', 'pet host', 'pet podcast'."
---

# Pet Podcast Video

Turns a user's pet photo into a fun short video of the "pet hosting a podcast." Core: img2img preserves the pet's real appearance, places the pet in a podcast recording scene, and generates an animated video of the pet opening its mouth to speak with lively expressions.

## Key Principles

- **Pet appearance must be preserved**: img2img references the original photo — fur color, markings, face shape match the original
- **Scene must have podcast feel**: microphone, headphones (optional), recording studio style background or clean desktop
- **Pet must look like it's "speaking"**: mouth slightly open, expressive face with interactive feel, eyes looking toward the camera
- **Video duration 3–6 seconds**: strong looping feel, suitable for social media sharing
- **No tail frames**

## Workflow

### 1. Upload Pet Photo

Upload pet photo, record asset_id.

**Photo requirements**:
- Pet's face clearly visible
- Front-facing or 3/4 angle works best
- Adequate lighting, clear details

### 2. Confirm Podcast Scene Style

**Scene options**:

| Scene Style | Description |
|---|---|
| Professional recording studio | Dark background, professional microphone, studio acoustic panels, strong professional feel |
| Desktop home style | Wooden desk, small desktop microphone, warm home lighting |
| Influencer style | Colorful background, ring light, RGB ambient lighting |
| Minimal white | Pure white background, clean microphone, crisp and professional |

### 3. Send Shot List

```
Art style: realistic feel, real fur texture, not cartoonified

Shot 1:
- Start frame: reference original image [pet photo asset_id], preserve pet's fur color, markings, and face shape features
- Scene: [chosen podcast scene], pet sitting in front of microphone, body upright, posture like a human host
- Pet state: facing camera, mouth slightly open, lively and animated expression, eyes looking straight ahead
- Props: [scene-appropriate microphone type] placed directly in front of the pet
- Composition: medium shot, pet occupies 60% of frame, clearly shows face and upper body
- Duration: 5s
- Video description: pet's mouth opens and closes slightly (mimicking speech), head has subtle rhythmic movement, ears have faint twitching, background remains static
```

### 4. Check Output

| Check Item | Standard |
|---|---|
| Pet appearance | Fur color and markings match the original photo |
| Podcast scene | Microphone clearly visible, scene has podcast feel |
| Animation effect | Mouth has opening and closing movement, not completely still |
| Anthropomorphic feel | Pet posture is upright, has host charisma |

### 5. Generate Audio (optional)

Can add "pet language" sound effects: rhythmic version of cat/dog sounds, or funny "pet voiceover" (user provides voiceover script).

### 6. Export

---

## Resolution

| Use Case | Resolution |
|---|---|
| Douyin / TikTok / Reels | 720×1280 (9:16) |
| WeChat / square | 720×720 (1:1) |
