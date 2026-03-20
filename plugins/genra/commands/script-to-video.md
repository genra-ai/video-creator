---
name: genra:script-to-video
description: Use this skill when the user provides a multi-shot script with multiple characters and scenes to convert directly to video. Script is never rewritten. Triggered by: "short drama", "script to video", "剧本转视频".
---

# Script to video

Converts a multi-shot script (6–15 shots, multiple characters, multiple scenes) into a video. Does not rewrite the script — only supplements visual information before sending.

## Key Principles

- **Art style has top priority**: declare on the very first line of the project message. Default: `Art style: realistic cinematic`
- **Do not rewrite the user's script** — the pipeline auto-parses any format; Claude only supplements visual descriptions
- **Show Step 1 supplementation to the user, then proceed to Step 2 immediately** — no need to wait for confirmation
- **Clear all tail frames** (opposite of voiceover): tail frames cause blending artifacts at cuts
- **Check images grouped by character**, not sequentially — same-character side-by-side comparison catches drift far better
- **Audio before video**

## Workflow

### 1. Analyze Script, Supplement Visual Information

Extract art style from user input. If none specified, default to `Art style: realistic cinematic`. If descriptions conflict (e.g., "anime" alongside "real portrait"), ask the user.

**Character description**: `[age + gender] + [hair: length/texture/color/styling] + [skin tone + distinctive features] + [top: color/material/cut] + [bottom] + [signature detail]`

A signature detail (glasses, earring, ring, patterned clothing) acts as a cross-shot anchor — be precise with colors: "pure white (like printer paper)", "deep navy (not black)".

**Scene description**: `[location] + [light source] + [light quality + color temp] + [key elements] + [atmospheric tone]`

| Situation | Lighting |
|-----------|----------|
| Warm and homey | Warm side-lamp, soft diffused, orange-yellow (3000K), no hard shadows |
| Tense confrontation | Single harsh side light, high contrast, cool white or blue-gray |
| Romantic outdoors | Golden hour backlight, rim light on hair, warm orange, subtle lens flare |
| Sad / oppressive | Overcast diffused, blue-gray, low saturation, no strong highlights |
| Urban night | Street lamp orange downlight + neon fill, bokeh background, wet reflections |
| Formal business | Even front white light, neutral color temp, clear environment |

**BGM mood**: "low strings + piano (oppressive/suspenseful)", "upbeat guitar (everyday warmth)", "epic orchestral (grand emotion)".

Show the user a brief supplement preview (character settings + scene settings), then proceed to Step 2.

### 2. Create Project & Send Script

Send one message with all character/scene definitions + the original script unmodified. Include in the message:
- Art style on the first line
- Each shot needs only a start frame; no tail frames
- Each shot must be a single point-in-time cinematic composition — one continuous scene, no panel dividers or multi-angle juxtaposition

For **>12 shots**: split into two messages — first 8 shots with all character/scene definitions in message 1; remaining shots with a character appearance reminder in message 2.

### 3. Filter Check

Fix any issues immediately; don't save them for the end.

- **Characters** (most critical): `identity_anchor` for the same character must be word-for-word identical across all shots — hair color, clothing color, and signature detail especially. Fix inconsistencies with `edit`
- **Dialogs**: verify each line is attributed to the correct character; narration must not be assigned to a specific character
- **Shots**: confirm framing (wide/medium/close-up) was parsed correctly; dialog shot duration must be ≥ natural reading time + 0.5s; reaction shots 2–3s minimum

### 4. Check Image Consistency (Grouped by Character)

Check which frames already have images — the editor auto-generates start frames; only regenerate missing ones.

Group all shots by character and preview them together. Focus on:

| Issue | Common Deviation | Fix |
|-------|-----------------|-----|
| Clothing color | White → off-white, dark blue → black | Regenerate; specify color with a reference object |
| Hairstyle | Long becomes short, bangs disappear | Regenerate; re-emphasize |
| Signature detail | Glasses / jewelry disappears | Regenerate; explicitly emphasize |
| Age feel | Character looks older / younger | Regenerate; add age anchor word |
| Glassy eyes | Close-up / extreme close-up shots | I2I: "eyes sharp and clear, focused" |
| Distorted hands | Gripping / pointing shots | Regenerate; simplify hand description |
| Same-direction dialogue | Shot-reverse-shot | Specify facing direction for each character explicitly |
| Multi-panel composition | Action-sequence shot descriptions | Rewrite as a single static moment using present-tense language |

For consecutive shots in the same scene: also verify depth-of-field consistency. Retry at most once per shot; if still off, accept and move on.

### 5. Clear All Tail Frames

Send a message asking the pipeline to clear all tail frames — keep only start frames. Verify afterward. If auto-clearing fails, manually deselect tail frames in the generation panel.

### 6. Generate Audio

**Voice description**: `[gender + age] + [voice texture] + [emotional baseline] + [pace]`

| Character Type | Example |
|---------------|---------|
| Young female lead (suppressed emotion) | Young female, bright tone, restrained suppression, slow pace, strong pauses |
| Middle-aged male (tired / guilty) | Mature male, low slightly hoarse, weary quality, slow, trailing ends |
| Young person (relaxed) | Young male, bright tone, casual natural delivery, moderate pace |
| Dominant / antagonist | Mature male, deep and powerful, fast pace, firm delivery |

Pace follows the scene's emotion — do **not** default to "fast pace" (that's for voiceover-style content only). Voice cloning: upload 5–10s reference audio; use the returned asset_id as the character's voice field.

### 7. Generate Videos

After all audio completes, generate all videos.

### 8. Preview & Export

- Scene transitions: cuts clean, no blending artifacts
- Multi-character dialog: lip sync matches the correct character
- Framing matches script intent (wide / medium / close-up)
- If tail frames are still causing artifacts: clear them again, regenerate only the affected shot

Export once all shots pass.

---

## Shot Description Reference

**Formula**: `[framing] + [subject position / facing direction] + [action / expression / emotion] + [key visual elements] + [lighting] + [depth of field]`

| Framing | Purpose | Description focus |
|---------|---------|----------|
| Wide / Establishing | Spatial feel, isolation | Environment dominates; describe environment first, then character's position within it (small, off-center) |
| Medium | Primary dialog framing | Waist-up; specify facing direction; two-person: left character faces right, right character faces left |
| Over-the-shoulder | Conversation POV | Name who is foreground (back to camera, blurred) and who is mid-ground (faces camera, in focus) |
| Close-up / Extreme | Emotional peak, inner state | Shoulders-up or face only; always include "eyes sharp and clear" — omitting this causes glassy eyes |
| Shot-reverse-shot | Standard dialog structure | Axis rule: once A=left/B=right is established, A always faces right and B always faces left across all cuts |

## Supported Script Formats

The pipeline auto-recognizes: Chinese multi-character dialogue scripts, English shot lists / screenplays (INT./EXT., timecodes, framing annotations), and narrative text drafts in other languages (auto-converted to shotlist).
