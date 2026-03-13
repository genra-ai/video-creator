# Voiceover

Generate a 20–30 second talking-head video: speaking directly to camera, fixed framing, seamless start/tail frame continuity between adjacent shots.

## Workflow Overview

```
Step 1: Generate script based on user's topic (4–6 lines of dialog)
Step 2: Create project, send ICT in one message
Step 3: Filter check
Step 4: Generate all shot images, check consistency shot by shot
Step 5: Set start/tail frames (adjacent shot continuity)
Step 6: Generate audio
Step 7: Generate all videos
Step 8: Preview and verify
Step 9: Export
```

---

## Step 1: Generate Script

### ⚠️ Art Style Has Top Priority

**Art style is the highest-priority setting** and must never be overridden by a default of "realistic live-action".

- Extract art style keywords from user input (anime, 2D, traditional Chinese, realistic, cinematic, etc.)
- A user-specified style takes precedence over the default realistic style; if the description is contradictory (e.g., "anime" but also "real portrait"), ask the user first
- In the ICT message in Step 2, write the style on a **dedicated first line**: `Art style: [user-specified style description]`
- If not specified, default to: `Art style: realistic live-action`

---

Based on the user's described topic, generate the voiceover script:

**Output**:
- Voiceover copy (colloquial, completable in 20–30 seconds at a natural reading pace)
- Split into **4–6 lines of dialog**, each corresponding to one shot (each completable in 4–6 seconds)
- **Character appearance** (filled in using the formula below; reused for all subsequent shots, must not be changed)
- **Scene description** (filled in using the formula below; same for all shots)
- **BGM emotional direction**

### Character Description Formula

The character description directly determines visual consistency across shots. The vaguer the description, the more freedom the generator has, and the more severe the appearance drift.

**Formula**: `[age feel + gender] + [hairstyle: length + texture + color + styling] + [skin tone + distinctive features] + [top: color + material + cut] + [signature detail]`

| Dimension | Too vague | Good enough |
|------|----------|--------|
| Hairstyle | Black hair | Shoulder-length straight hair with slight wave, pure black, no bangs |
| Clothing | White shirt | Off-white loose cotton shirt (cuffed sleeves), untucked |
| Skin tone | Fair | Fair and delicate, no freckles, soft pink lip color |
| Signature detail | — | Small silver round stud in left ear (only accessory) |

**The role of signature details**: gives the model a cross-shot anchor — the model will try to reproduce this detail on every generation. Recommended: glasses, a specific hair accessory, ring, necklace.

**Colors must be precise** (AI often renders white as off-white):
- "Pure white (similar to printer paper white)"
- "Deep navy blue (not black)"

### Scene Description Formula

**Formula**: `[location type] + [time/light source] + [light quality + color temperature] + [key environmental elements] + [atmospheric tone]`

**Lighting is the core of scene mood**. Common lighting references for voiceover scenes:

| Context | Lighting description |
|------|---------|
| Fresh skincare/beauty | Front soft light, warm color temperature (4000K), no strong shadows, simple light-colored background |
| Tech/professional business | Even front white light, neutral color temperature (5500K), simple dark background, clear character silhouette |
| Warm lifestyle | Warm side lamp light, soft diffuse, orange-yellow tones (3000K), no hard shadows |
| Energetic entertainment | Bright front light, saturated colors, background may include colorful elements |

---

## Step 2: Create Project, Send ICT

Send one message via `chat.btn_send`, **including all shots at once**. **Every shot must include its dialog in the very first send** (adding it later is cumbersome):

```
Art style: [user-specified style, default: realistic live-action]

Please create a voiceover video project, language Chinese, 16:9 landscape.

BGM: [emotional description, e.g.: upbeat fresh electronic music with a sense of rhythm]

Character: [character name], [complete appearance description using the formula], speaking directly to camera, relatively fast pace

Scene: [location type], [lighting description], clean and simple, emphasizing the character

Shot 1 (5s): medium shot, character facing camera, [current expression/action state]
Dialog: "[line 1]"

Shot 2 (5s): medium shot, character facing camera, [current expression/action state]
Dialog: "[line 2]"

Shot 3 (5s): medium shot, character facing camera, [current expression/action state]
Dialog: "[line 3]"

Shot 4 (5s): medium shot, character facing camera, [current expression/action state]
Dialog: "[line 4]"

(Add up to 6 shots depending on script length)

Notes:
- All shots use the same character and the same scene
- Framing fixed at medium shot; do not change camera angle, do not push or pull
- Character size and position in the frame must be completely identical across all shots: upper body centered from chest up, character occupies approximately 70% of frame height, character always faces directly into the camera
- Focal length, depth of field, and shooting distance are completely identical across all shots; background blur level is consistent
- No pull-in/pull-out/push-in effect on any shot; maintain fixed focal length
- Background environment is completely identical across all shots: the arrangement of objects, decorative details, lighting position and color in the background must remain unchanged; no background element may appear or disappear between shots
```

Wait for completion after sending, then retrieve project state.

---

## Step 3: Filter Check

Check the following filters in sequence; fix any issues immediately using `edit` on editable fields — do not wait until the end:

Check shots
Check dialogs
Check characters (confirm character description is consistent across all shots)
Check scenes

**Key checks**:
- All shots have consistent framing (medium shot, fixed camera)
- All shots use the same character_id and location_id
- Each shot corresponds to one dialog entry with correct dialog content
- Character description is completely identical across all shots (verify identity_anchor shot by shot)

---

## Step 4: Check and Complete Images, Calibrate Depth of Field Consistency Shot by Shot

**Check first, then generate as needed** — the editor automatically generates start frame images upon ICT creation; do not blindly regenerate everything.

**① Check which frames already have images** (`img: true`) and which are missing (`img: false`):

Check shots

Review the returned frames list:
- If any frames have `img: false` → select only the missing frames and generate them via `sidebar.btn_generate`
- Once all start frames have `img: true`, proceed to the next step for shot-by-shot consistency check

**② Preview shot by shot, comparing depth of field and character size against the previous shot starting from shot 2**:

**Core principle**: use shot 1 as the baseline; starting from shot 2, compare each image against the previous one, and fix any inconsistency immediately — **do not wait until the end to batch-process**.

Preview shot 1 start frame (establish baseline)
Preview shot 2 start frame (compare against shot 1)
(Continue in order, comparing each one)

**What to check for each image** (compared to the previous shot):
1. **Depth of field/focal length consistency**: is the background blur level the same? One shot cannot have a shallow depth of field while another has a sharp background
2. **Character size/position consistency**: is the character's height ratio in the frame and chest cutoff position the same?
3. **Shooting distance feel**: the character must not appear closer in some shots and farther in others, as if the camera is pushing or pulling
4. **Character appearance consistency** (hairstyle/clothing/skin tone/signature detail)

**Voiceover-specific AI issues** (actively check each shot):
- **Glazed eyes**: the most frequent issue in close-up voiceover shots; AI tends to generate glass-like eyes with no emotion. If found → in I2I, add "sharp and clear eyes with focus, eyes have a glossy look"
- **Face drift**: inconsistent face shape and facial proportion between adjacent shots (wider nose, wider eye spacing, etc.). If found → use the previous shot's image as I2I reference, add "keep face shape and facial proportion completely identical to the reference image"
- **Lighting inconsistency across shots**: the lighting angle suddenly changes between shots of the same scene. If found → repeat lighting keywords in the description (e.g., "front soft light, warm color temperature"), fix with I2I

**Judgment criteria**:
- Basically consistent → continue to the next shot, no modification needed
- Obviously inconsistent (large depth-of-field gap / clearly different character size / glazed eyes) → fix immediately with I2I

**③ When inconsistent: use the previous shot's image as a reference and regenerate via I2I**:

When a shot's image is inconsistent with the previous one:

1. Record the previous shot's image URL (retrieved from `previewPanel.imageUrl`)
2. In the I2I input field of the problematic shot's preview panel, describe the modification intent:
   ```
   Example: "Keep the character's appearance and action unchanged; adjust depth of field and shooting distance to match the reference image; character size as a proportion of the frame matches the reference image; same background blur level; eyes sharp and expressive"
   ```
3. Send a message via `chat.btn_send`, explicitly identifying which shot has the issue:
   ```
   "Please reference the image of shot N and regenerate shot M, adjusted to the same shooting distance, depth of field, and character size, with everything else unchanged"
   ```
4. Wait for generation to complete, then preview and compare
5. **Retry at most 1 time** — if the result is still inconsistent after regeneration, accept the current state and continue; do not loop repeatedly

**④ After all shots have been checked (or the retry limit has been reached), proceed to Step 5 to set start/tail frames.**

**Common issues**: the image generator may ignore clothing color/hairstyle details or veer off the lighting style — cross-check against `filter_characters` and `filter_shots` shot by shot; do not skip based on impressions. Depth-of-field inconsistency is the root cause of the push/pull feeling in video transitions and must be resolved in this step.

---

## Step 5: Set Start/Tail Frames (Critical!)

**Principle**:
```
After generating N images:
  Shot 1 [start frame=image 1, tail frame=image 2]   ← tail frame = start frame of shot 2
  Shot 2 [start frame=image 2, tail frame=image 3]   ← tail frame = start frame of shot 3
  ...
  Shot N [start frame=image N, tail frame=image N]   ← last shot start and tail are the same, keep default

→ Adjacent shots share the same image at the transition point; video is seamless with no jump cuts
```

**Steps**:

First retrieve project state and record the `first_frame` asset_id of each shot.

Then set the tail frame for each shot from shot 1 to the second-to-last shot:

```
Send message: "Please set the tail frame (tail_frame) of shot N to $<first_frame_asset_id of shot N+1>"
```

Send and wait, then call `get_state` to verify that the tail_frame field matches expectations. If inconsistent, resend the message; retry at most 3 times.

**Last shot**: tail frame stays at default (equals its own start frame); no action needed.

> ⚠️ **voiceover sets tail_frame — does not clear it** — this is the opposite of script-to-video. script-to-video clears all tail frames; voiceover relies on start/tail frames to achieve seamless continuity between adjacent shots.

---

## Step 6: Generate Audio

**Audio must be generated before video** (audio duration determines video duration):

Generate audio and wait for completion.

### Voice Description Formula

Voice quality directly affects the feel of the video; do not just fill in "female voice" or "male voice":

**Formula**: `[gender + age feel] + [voice texture] + [emotional tone] + [pace]`

| Voiceover type | Example description |
|---------|---------|
| Skincare/beauty (young female) | Young female voice, clear and soft tone, warm and approachable, fast pace, crisp articulation |
| Tech/professional (male) | Mature male voice, deep and powerful tone, professional and confident, moderately fast pace, steady rhythm |
| Energetic promo (gaming/entertainment) | Young male/female voice, bright and lively tone, full of energy, fast pace, infectious |
| Traditional Chinese/literary | Young female voice, gentle and graceful tone, strong sense of temperament, slightly slower pace, natural pauses |

**Pace principle**: voiceover videos default to "relatively fast pace" to keep the rhythm tight; emotional or literary styles may be slightly slower.

> **Voice cloning**: to clone a specific voice, upload a 5–10 second reference audio clip; write the returned `$asset_id` into the character's `.voice` field and it will be cloned automatically during generation.

---

## Step 7: Generate All Videos

After audio is complete, generate all videos and wait for completion.

---

## Step 8: Preview and Verify

Preview each shot one by one, focusing on **shot transitions**:

**Checkpoints**:
- Whether the image is continuous at the transition between adjacent shots (no jump cuts)
- Whether the character's posture/position flows naturally
- Whether each line of dialog matches the video duration

If a shot's start/tail frames are not seamless:
1. Reset the tail frame for that shot (see Step 5)
2. Regenerate only that shot's video

---

## Step 9: Export

Export after all shots have passed verification.

---

## ICT Specification

| Field | Specification |
|------|------|
| First line | `Art style: [style description]`; default for realistic voiceover: `realistic live-action` |
| Number of shots | 4–6 |
| Duration per shot | 4–6 seconds |
| Shot description | Fixed medium shot, facing camera; describe only expression/action/speaking state; no camera movement or framing changes |
| character_id | Same one for all shots |
| location_id | Same one for all shots |
| Dialog type | The character speaking (not narration) |
| Dialog line | Colloquial, completable naturally within 4–6 seconds |
| Character pace | Relatively fast (note "relatively fast pace" in the character's voice field description) |
| BGM | Fill in emotional description in the `global.bgm` field; do not leave blank |
| tail_frame | **Set** (each shot's tail frame = next shot's start frame); opposite of script-to-video's "clear" |

---

## Key Learnings

- **Include dialog in every shot's very first send** — adding it later is cumbersome
- **Run filter check immediately after sending** — do not wait until the end
- After images are generated, use `filter_characters` to centrally verify appearance consistency of the same character across shots
- **Glazed eyes are the most frequent voiceover issue**: check shot by shot in Step 4; fix immediately with I2I when found, adding "sharp and clear eyes with focus, eyes have a glossy look"
- **Face drift is the second most common voiceover issue**: use I2I + the previous shot's image as a reference for adjacent shots, explicitly stating "keep face shape and facial proportion consistent with the reference image"
- **Depth-of-field inconsistency is the root cause of the push/pull feeling in video**: in Step 4, start comparing depth of field and character size against the previous shot from shot 2 onward; fix immediately with I2I + previous shot reference if inconsistent; only proceed to Step 5 after all pass
- **After completing Step 5 start/tail frame setup, call `get_state` to verify shot by shot** and confirm tail_frame is correct before generating video
- **undo/redo**: `workspace.btn_undo` / `workspace.btn_redo` can reverse accidental operations; try undo first when a project goes wrong
- **voiceover sets tail_frame — does not clear it** — voiceover relies on start/tail frames for seamless continuity; opposite of script-to-video
- **Voiceover videos must use a relatively fast pace**: note "relatively fast pace" in the character's voice field; otherwise the generated audio will be too slow for the voiceover rhythm
- **When art style is non-realistic, check that the character matches the style**: for an anime art style, character descriptions should use anime-appropriate vocabulary (e.g., "2D anime girl, sakura-pink ponytail") rather than realistic descriptions
