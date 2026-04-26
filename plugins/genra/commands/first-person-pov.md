---
name: First-Person POV
description: "Describe a scene to create an immersive POV video."
agent_description: "Use this skill when the user wants to create a fully immersive first-person perspective video: the main subject never appears on screen, camera simulates handheld or natural eye movement. Suitable for dream sequences, travel, gaming, and immersive experience content. Triggered by: 'first person POV', 'POV video', 'immersive perspective', 'first person view', 'first person', 'what the eyes see'."
---

# First-Person POV Video

Turns scene descriptions into a fully first-person perspective (POV) immersive video. Core: the frame is always "what the eyes see" — the viewer is the protagonist, no subject character appears on screen.

## Key Principles

- **No complete human figure ever appears on screen**: hands holding objects can appear (e.g., hands holding a coffee cup), but no human face or body
- **Camera simulates eye movement**: natural subtle shake, gaze shifts, looking down / looking up dynamics
- **Scene description must specify gaze direction**: each shot must clarify "where the eyes are looking / what they're looking at"
- **Immersion comes from details**: gaze movement, hand interactions, and ambient sound are the keys to immersion
- **No tail frames**

## Applicable Scene Types

| Scene Type | Camera Feel Characteristics |
|---|---|
| Dream / fantasy | Drifting feel, floating perspective, slight edge vignette |
| Travel / exploration | Forward movement feel, scanning environment, pausing on interesting details |
| Everyday life | Low angle, looking at tabletop/hand operations, real-life feel |
| Gaming / adventure | Directional movement feel, rapid perspective scan, tense feel |
| Mystery / suspense | Cautious, gaze shifts slowly, voyeuristic feel |

## Workflow

### 1. Confirm Scene, Plan Gaze Path

**Required info**: scene theme (dream/travel/everyday/adventure etc.) + key scenes/objects to experience (3–5).

**Gaze path planning**: design where the viewer's "eyes" will look and in what order they move.

**Shot structure** (5–8 shots, 30–60 seconds):

| Shot | Content | Characteristics |
|---|---|---|
| 1 | Scene opening, gaze from blurry to clear (or directly looking at main scene) | Establish environmental feel |
| 2–5 | Gaze moves through scene, pausing on key details | Immersive exploration |
| 6–7 | Gaze encounters core event or picks up / touches an object | Emotional peak |
| 8 | Gaze slowly moves away, scene fades out | Closing |

### 2. Send Shot List

```
Art style: [realistic / dreamy / cinematic, chosen based on scene]

[Global constraints]
- Full first-person perspective throughout, no human faces or bodies on screen
- Camera simulates real human eye movement: slight natural handheld shake, not mechanical gimbal effect
- Hands/hand-held objects can enter the edge of frame

Shot 1 (Xs): perspective looking at [specific direction + content], [environmental state description]
  Video description: gaze slowly shifts from [starting point] to [ending point], slight natural shake, [environmental dynamic details]

Shot 2 (Xs): perspective pausing on [a detail object/scene]
  Video description: gaze focuses, subtle breathing-rhythm shake, [object/scene dynamics]

Shot 3 (Xs): [hand enters frame / gaze shifts to another location]
  Video description: [hand action description] or [gaze quickly scans then focuses]

...
```

### 3. Filter Check

- Confirm all shots have no human faces
- Is gaze direction and movement description clear for each shot
- Are there enough detail descriptions to create immersion

### 4. Clear All Tail Frames

### 5. Generate Audio

**Ambient sound as primary**: choose ambient sound matching the scene (city/nature/indoor), light BGM underneath.

| Scene | Sound Effects Suggestion |
|---|---|
| Dream | Ethereal reverb, soft piano, reverb-heavy feel |
| Travel / outdoor | Natural ambient sound, wind, footsteps |
| Everyday indoor | Indoor background ambient sound, quiet feel |
| Adventure / tense | Heartbeat sound effect, low strings, ambient sound |

### 6. Generate Videos & Export

---

## Resolution

| Use Case | Resolution |
|---|---|
| Immersive vertical | 720×1280 (9:16) |
| Horizontal / cinematic | 1280×720 (16:9) |
