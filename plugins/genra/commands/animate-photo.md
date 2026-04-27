---
name: Animate Photo
description: "Upload a photo to make it speak, dance, or smile."
agent_description: "Use this skill when the user wants to animate a still photo — bringing a person, animal, or object to life as a short video. The uploaded image is always used as the start frame anchor. Supports four motion types: body motion (dance, flip, walk, fly), micro animation (nod, shake, blink, smile, wind-blown hair), lip sync / talking head (character speaks or syncs to audio), and background effect (dynamic environment while subject stays mostly still). Triggered by: 'animate my photo', 'make photo move', 'bring image to life', 'photo to video', 'make character dance', 'lip sync', 'make him walk', 'animate my picture', 'img2video', 'make her talk', 'add motion to image', 'living photo', 'portrait animation'."
---

# Animate Photo

Turns a still image into a short video by specifying motion, effect, or speech. The uploaded photo is always treated as the **start frame** — every video description must be consistent with what is already visible in the image.

## Key Principles

- **Image = start frame**: the video begins exactly as the photo looks. Never describe an initial state that contradicts the photo (e.g., do not write "character stands up from a chair" if they are already standing in the image).
- **Describe motion, not result**: narrate what happens during the clip, not the end pose. The motion itself is the content.
- **Be specific about motion parameters**: always state magnitude (subtle / moderate / large), speed (slow / normal / fast), and direction (left–right, forward, upward, etc.).
- **One dominant motion per clip**: mixing too many simultaneous actions produces incoherent output — choose the primary motion and let secondary details be minor.
- **Lip sync requires audio first**: if the user wants a talking character, obtain or generate the audio track before writing the video description, then align mouth movement cues to the audio rhythm.

---

## Workflow

### Step 1 — Receive Image & Analyze Content

Ask the user to upload their photo if not already provided. Analyze the image and identify:

| Attribute | What to Detect |
|---|---|
| Subject type | Person / animal / object / scene |
| Subject pose | Standing, sitting, facing camera, profile, etc. |
| Body visibility | Full body / half body / close-up / face only |
| Background | Simple / complex / indoor / outdoor |
| Lighting & style | Realistic / illustrated / anime / 3D render |

Summarize the image analysis in one short paragraph and confirm with the user before proceeding.

---

### Step 2 — Identify Motion Type

Classify the user's requested animation into one of four categories:

#### A. Body Motion
Large-scale physical movement: dancing, backflip, walking, running, jumping, flying, fighting pose sequence.

- **Best with**: full-body or half-body shots
- **Requires**: clear body posture visible in the photo; clothing and limbs must be unobstructed for the intended motion
- **Description focus**: which body parts move, motion trajectory, rhythm/speed, number of repetitions

#### B. Micro Animation
Subtle facial or surface effects: nodding, head-shaking, blinking, smiling, wind-blown hair, eye movement, slight body sway.

- **Best with**: portrait / close-up shots
- **Requires**: face or target area clearly visible
- **Description focus**: specific micro-movement, amplitude (very subtle / light / moderate), speed, and looping behavior

#### C. Lip Sync / Talking
Character opens mouth and speaks, either free-form or synced to a provided audio clip.

- **If audio is provided**: upload the audio first; analyze its rhythm, pauses, and approximate syllable count; then write lip movement + facial expression description synchronized to the audio
- **If no audio**: generate or describe speech content first, then produce the video description
- **Description focus**: mouth open/close pattern, facial expression during speech (earnest, cheerful, emotional), head micro-movements that accompany natural speech

#### D. Background Effect
The subject stays mostly static while the environment comes alive: falling leaves, light rays, rain, bokeh shimmer, water ripple, snow, fire glow, wind effect on trees.

- **Best with**: any shot type; subject does not need to move significantly
- **Requires**: identifiable background region in the photo
- **Description focus**: which background elements animate, direction and speed of movement, intensity, whether any ambient light change occurs

---

### Step 3 — Clarify Missing Parameters

Before generating the description, confirm any unknowns:

| Parameter | Ask If Missing |
|---|---|
| Motion magnitude | Subtle / moderate / exaggerated? |
| Speed | Slow / normal / fast? |
| Loop or single-pass | Should the motion loop seamlessly or play once? |
| Duration | Short (2–4 s) / standard (4–6 s) / extended (6–8 s)? |
| Audio | Does the user want background music, speech audio, or silence? |
| Aspect ratio | Vertical 9:16 / square 1:1 / horizontal 16:9? |

---

### Step 4 — Write Video Description

Compose the video description following these rules:

```
[Reference]: uploaded image used as start frame

[Subject]: [exact description matching what is in the photo — same clothes, pose, expression]
[Motion]: [precise motion description — body parts involved, direction, speed, magnitude]
[Secondary details]: [minor complementary effects — slight fabric movement, ambient light flicker, etc.]
[Background]: [static / or animated background description]
[Camera]: [locked-off / very slow push-in / gentle handheld — avoid dramatic camera moves for animate-photo tasks]
[Duration]: [X seconds]
[Loop]: [yes / no]
```

**Start-frame consistency checklist** (verify before sending):
- [ ] Subject's clothing matches the photo exactly
- [ ] Subject's starting pose matches the photo exactly
- [ ] No description implies a prior action that contradicts the photo state
- [ ] Motion described is physically possible from the starting pose in the image

---

### Step 5 — Lip Sync Specific Sub-workflow

If the motion type is **C. Lip Sync / Talking**, follow this additional sub-workflow:

1. **Obtain audio**: user uploads audio file, or generate TTS from a provided script
2. **Analyze audio**: note total duration, speech rhythm, key pauses, emotional tone
3. **Write synced description**:
   - Match mouth movement pattern to audio cadence
   - Describe natural head micro-movements that accompany speech (slight tilt, nod on emphasis)
   - Describe facial expression consistent with audio emotion
4. **Set video duration** = audio duration + 0.3 s tail
5. **Confirm audio–video alignment** before generation

---

### Step 6 — Generate Video

Send the finalized description to the video generation model with the uploaded image as the start frame.

**Generation parameters reference**:

| Setting | Recommended Value |
|---|---|
| Start frame | Uploaded user photo (required) |
| Motion strength | Match to requested magnitude: low / medium / high |
| Seed | Lock seed if user wants consistent style across multiple clips |

---

### Step 7 — Motion Quality Check

After the video is generated, review for these failure modes:

| Issue | Symptom | Action |
|---|---|---|
| Start-frame drift | First frame looks different from the uploaded photo | Re-generate with higher start-frame weight |
| Over-deformation | Face or body morphs unnaturally | Reduce motion strength; simplify description |
| Motion too stiff | Barely any movement | Increase motion strength; add more explicit motion cues |
| Lip sync mismatch | Mouth movement out of sync with audio | Rewrite description with more granular timing cues |
| Background bleeds into subject | Background animation distorts the subject | Add "subject remains sharp and stable" constraint to description |

If any issue is found, adjust the description or parameters and re-generate. Present the final video to the user with a brief summary of the motion applied.

---

## Resolution Reference

| Platform | Resolution |
|---|---|
| TikTok / Douyin / Reels | 720×1280 (9:16) |
| YouTube / horizontal | 1280×720 (16:9) |
| Instagram square | 720×720 (1:1) |
| Xiaohongshu portrait | 1080×1350 (4:5) |
