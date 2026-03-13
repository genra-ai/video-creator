# Script to Video

Converts a multi-shot script provided by the user (6–15 shots, multiple characters, multiple scenes) into a video. **Does not rewrite the script** — only supplements visual information, then sends it directly to the S0 Pipeline for execution.

## Workflow Overview

```
Step 1: Analyze script, supplement character/scene visual descriptions
Step 2: Create project, send the complete script message (including supplemented information)
Step 3: Filter check (focus: character consistency, dialogue attribution)
Step 4: Check and supplement images, check appearance consistency grouped by character
Step 5: Clear all tail frames (keep only start frames)
Step 6: Generate audio (individual voice for each character)
Step 7: Generate all videos
Step 8: Preview verification
Step 9: Export
```

---

## Step 1: Analyze Script, Supplement Visual Information

**Do not rewrite the user's script**. The S0 Pipeline will automatically convert script/shotlist into ICT; Claude's task is to **supplement visual information before sending**.

### ⚠️ Art style takes highest priority

**Art style is the highest-priority setting** and must never be overridden by the default "realistic cinematic" style.

- Extract art style keywords from anywhere in the user's input (anime, 2D animation, Chinese animation, comic, realistic, cinematic, etc.)
- User-specified art style > default realistic; if descriptions conflict (e.g., "anime" alongside "real portrait"), ask the user before proceeding
- In the Step 2 prompt, write the art style on its own on the **first line**: `Art style: [user-specified art style description]`

---

### Character Description Formula

Character descriptions directly determine visual consistency across shots. The vaguer the description, the more room the generator has to improvise, and the more severe the appearance drift.

**Formula**: `[approximate age + gender] + [hair: length + texture + color + styling] + [skin tone + distinctive features] + [top: color + material + style] + [bottom] + [signature detail]`

| Dimension | ❌ Too vague | ✅ Sufficient |
|-----------|-------------|--------------|
| Hair | Black hair | Shoulder-length slightly wavy straight hair, pure black, no bangs |
| Clothing | White shirt | Off-white loose cotton shirt (rolled sleeves), not tucked in |
| Skin tone | Fair | Fair and smooth, no freckles, light pink lip color |
| Signature detail | — | Small silver round stud earring on the left ear (only accessory) |

**The role of a signature detail**: gives the model a **cross-shot anchor** — each time the model generates, it will try to reproduce this detail, which maintains consistency far better than vague descriptions like "white shirt". Recommended choices: glasses, specific hair accessory, ring, necklace, pattern on clothing.

**Colors must be precise**: AI frequently generates white as off-white, and dark blue as black. Use reference objects to assist:
- "Pure white (like printer paper white)"
- "Deep navy blue (not black)"
- "Brick red (like vintage red brick)"

### Scene Description Formula

**Formula**: `[location type] + [time / light source] + [light quality + color temperature] + [key environmental elements] + [atmospheric tone]`

**Lighting is the core of scene mood**. Common scene lighting references for dramatic content:

| Situation | Lighting Description |
|-----------|----------------------|
| Warm and homey | Warm side-lamp light, soft diffused, orange-yellow tone (3000K), no hard shadows |
| Tense confrontation | Single harsh side light, high-contrast shadows, cool white or blue-gray tone |
| Romantic outdoors | Golden hour backlight, hair rim light, warm orange tone, subtle lens flare at edges |
| Sad and oppressive | Overcast diffused light, blue-gray diffusion, low saturation, no strong highlights |
| Urban night scene | Street lamp orange downlight + neon color fill, background bokeh, wet ground reflections |
| Formal business | Even front white light, neutral color temperature, clear environment, soft shadows |

### Global Information Supplement

- **Visual style**: affects the overall visual tone. Common options: "realistic cinematic," "Japanese fresh-realistic," "Hong Kong film aesthetic (film grain + high contrast)," "Western TV drama quality," "light animated style"
- **BGM mood**: "low strings + piano (oppressive/suspenseful)," "upbeat guitar (everyday warmth)," "epic orchestral (grand emotion)"

### Confirm Language and Resolution

Determine from the script language; default is 16:9 landscape (specify if vertical is needed).

### Output: Show supplementation results to user, then proceed directly to Step 2

Show the user the following format as a supplementation preview, **then proceed directly to Step 2 without waiting for confirmation**. If the user has changes, they can send a message:

```
[Visual Supplement Preview]

Global visual style: Realistic cinematic, cool-leaning tone
BGM: Low piano + thin strings, with a sense of oppressive suspense

Character settings:
- Lin Xiao: Asian female, approx. 25, shoulder-length slightly wavy hair, pure black, no bangs, fair skin,
  off-white loose cotton shirt (rolled sleeves) + light gray straight-leg trousers, small silver round stud on left ear
- Chen Ming: Male, approx. 32, short side-parted hair, dark brown, slightly weary appearance, deep navy blue blazer +
  white shirt (no tie), black dress trousers, no accessories

Scene settings:
- Café: interior, wooden table and chairs by floor-to-ceiling windows, afternoon diagonal natural light (entering from left), warm yellow
  tone, simple Nordic style, blurred figures in background
- Street: exterior at night, orange downlight from street lamps, light puddle reflections on ground, neon
  signage softly blurred in background, sparse pedestrians

(The above is the visual supplement. Sending script now...)
```

---

## Step 2: Create Project, Send Complete Script Message

Use `chat.btn_send` to send the message.

### Shot count ≤ 12: send all at once

```
Please create a video project based on the following script, [language], [resolution].

Global visual style: [style description]
BGM: [mood description]

Character settings:
- [character name]: [complete appearance description supplemented using the formula]
- [character name]: [appearance description]

Scene settings:
- [scene name]: [complete lighting + environment description supplemented using the formula]
- [scene name]: [environment description]

Image generation requirements: Each shot corresponds to a single point-in-time complete cinematic composition; the whole image is one continuous scene with no dividing lines or multi-angle juxtaposition. Each shot requires only the start frame; **do not set a tail frame (tail_frame)**.

--- Original script follows below ---
[User's original script, unmodified]
```

### Shot count > 12: send in two messages

**First message** (first 8 shots + all character/scene definitions):

```
Please create a video project based on the following script, [language], [resolution].

Global visual style: [style description]
BGM: [mood description]

Character settings:
- [character name]: [complete appearance description]
...

Scene settings:
- [scene name]: [complete environment + lighting description]
...

--- Part 1 of the script follows below (total [N] shots, sending first 8) ---
[Original text of the first 8 shots]
```

After waiting for completion, send the **second message** (remaining shots + repeat character appearances to reinforce consistency):

```
Please continue adding the remaining shots:

Character appearance reminder (keep exactly consistent with the above):
- [character name]: [repeat key appearance details, especially signature details]

--- Part 2 of the script follows below ---
[Original text of remaining shots]
```

Send and wait for completion, then retrieve project status.

---

## Step 3: Filter Check

Check the following filters in order; fix any issues immediately using `edit` on editableFields — **do not save them all for the end**:

Check shots (whether framing and camera movement are parsed correctly)
Check dialogue (whether dialogue attribution is correct)
Check characters (identity_anchor must be consistent across all shots)
Check scenes

### Check Focus

**`filter_characters`** (most important):
- The `identity_anchor` description for the same character must be completely identical across all shots
- Pay special attention to: hair color, clothing color, signature details — must be word-for-word the same in all shots
- If a shot's character description is inconsistent with others, immediately use `edit` to unify it

**`filter_dialogs`**:
- Is each line's `character_id` attributed to the correct character (in dialogue scenes, who said what cannot be mixed up)
- Narration-type lines (narrator) must not be incorrectly attributed to a specific character

**`filter_shots`**:
- Is the framing parsed correctly (wide / medium / close-up / extreme close-up corresponding to the script description)
- Duration of dialogue shots: must be ≥ the natural reading time of the line + 0.5s buffer; check for shots that are too short
- Reaction shots (no dialogue): recommend 2–3 seconds; too short and the emotion cannot land

---

## Step 4: Check and Supplement Images, Verify Appearance Consistency Grouped by Character

**Check first, then generate as needed** — the editor automatically generates start frame images when the ICT is created; do not blindly regenerate everything.

### ① Check which frames already have images

Check shots

- If there are frames with `img: false` → select only the missing frames and regenerate via `sidebar.btn_generate`
- Once all start frames have `img: true`, proceed to consistency check

### ② Check appearance consistency grouped by character

List all shots in which each character appears from the project state or character filter, and preview them group by group:

Preview frames one by one

**Compare all shots of the same character side by side**, focusing on:

| Check Item | Common Deviation | Action |
|------------|------------------|--------|
| Clothing color | White → off-white, dark blue → black | Regenerate immediately; specify color clearly during I2I |
| Hairstyle | Long hair becomes short, bangs disappear | Regenerate; re-emphasize hairstyle in description |
| Signature detail | Glasses / jewelry disappears | Regenerate; explicitly emphasize in description |
| Age feel | Character looks older / younger | Regenerate; add age anchor word in description |

**AI-specific image issues in dramatic content** — proactively check per shot:

- **Glassy eyes**: AI tends to generate glass-eyed characters in close-up / extreme close-up shots that appear emotionless. If this occurs → add "eyes sharp and clear, focused on the eyes" during I2I correction
- **Distorted hands**: hands in gripping, pointing, or holding shots are prone to 6-finger or skeletal errors. For close-up shots with hand movement → check carefully during preview; if distorted, regenerate and simplify the hand movement description
- **Ghostly background figures**: in scenes with blurred crowds, background figures can appear with strange bodies. Check backgrounds; if abnormal → add "background figures completely blurred, no discernible details" when correcting
- **Both characters facing the same direction in dialogue shots**: in shot-reverse-shot dialogue scenes, both characters sometimes face the same direction (as if looking at a wall). If this occurs → specify facing direction explicitly during regeneration (see appendix for dialogue shot formula)
- **Multi-panel composition**: a shot description should correspond to a single point-in-time complete cinematic composition with no dividing lines or multi-angle juxtaposition. AI sometimes misinterprets shot descriptions containing action sequences ("first... then...") as storyboards and outputs multi-panel composites. Shot descriptions should use present-tense language describing a single static state, not a narrative sequence; if the output has panels, remove sequence words from the description and rewrite using static composition language

**Correction method**:
```
Send message: "Please reference the character [character name] in Shot N, regenerate Shot M, [specific correction], everything else unchanged"
```
**Retry at most 1 time** — if there is still deviation after regeneration, accept and move on; do not loop repeatedly.

### ③ Check depth-of-field consistency for consecutive shots in the same scene

For **consecutive shots within the same scene** (excluding framing changes), additionally check:
- Whether the degree of background blur is consistent (the same scene should not have shallow depth of field in one shot and a sharp background in the next)
- No need for this comparison between different scenes

---

## Step 5: Clear All Tail Frames

**Strategy: keep only start frames, clear all tail frames.**

Tail frames cause abnormal visual blending effects at video boundaries. The standard practice is not to use them. Step 2 already declares in the prompt not to use tail frames, but the S0 Pipeline sometimes auto-generates them, so they must be manually cleared in this step.

### Check whether tail frames exist

From `filter_shots` or the `get_state` result from the previous step, check whether there are frames with `type: "tail frame"` and `img: true`. If any exist, proceed with clearing.

### Clearing operation

Send a message for batch clearing:

```
Send message: "Please clear the tail frame (tail_frame) of all shots, keeping only the start frame"
```

After receiving the response, use `get_state` or `filter_shots` again to confirm all frames with `type: "tail frame"` have been removed.

If the message approach does not work, switch to manually confirming via the `sidebar.btn_generate` panel: do not check any tail frame items; keep only start frames.

---

## Step 6: Generate Audio (Multi-Character Voices)

**Audio must be generated before video** (audio duration determines video duration):

Generate audio

### Multi-character voice direction

Voice descriptions for dialogue scenes affect emotional perception; do not just write "male voice / female voice":

**Description formula**: `[gender + approximate age] + [voice texture] + [emotional baseline] + [pace]`

| Character Type | Description Example |
|----------------|---------------------|
| Young female lead (emotionally suppressed) | Young female voice, bright vocal tone, with a restrained sense of suppression, slower pace, strong sense of pauses |
| Middle-aged male (tired and guilty) | Mature male voice, low-pitched slightly hoarse, weary quality, slow pace, trailing ends |
| Young person (relaxed and everyday) | Young male voice, bright vocal tone, casual and natural delivery, moderate pace |
| Antagonist / dominant character | Mature male voice, deep and powerful, faster pace, firm delivery with no pauses |

**Pace selection principles** (do not use voiceover-style "fast pace" for dialogue scenes):
- Angry / excited scene → faster pace, forceful delivery
- Sad / guilty scene → slow pace, strong sense of pauses
- Tense and oppressive scene → slow pace, deliberate pauses and silences
- Relaxed everyday scene → moderate pace, natural and casual

### Voice cloning (optional)

Upload a 5–10 second reference audio clip; write the returned `$asset_id` into the character's `.voice` field:
```
Send message: "Please set the voice for character [character name] to $<audio_asset_id>"
```

Wait for all audio to finish generating.

---

## Step 7: Generate All Videos

Once audio is complete, generate all videos and wait for completion.

---

## Step 8: Preview Verification

Preview each shot, focusing on **scene transition points** and **continuity within the same scene**:

**Check points**:
- **Scene transitions**: are the cuts clean and natural
- **Multi-character dialogue**: is dialogue attribution correct; do lip sync and characters match
- **Framing changes**: do wide / medium / close-up framings match the script's intent
- **Confirm no remaining tail frames**: if tail frames are still causing visual anomalies, return to Step 5, clear them again, then only regenerate the affected shot's video

---

## Step 9: Export

Export once all shots have been verified.

---

## Key Learnings

- **Do not rewrite the user's script**: S0 automatically parses script/shotlist; Claude only needs to supplement visual descriptions and send the original text
- **Show the Step 1 supplementation results to the user, then proceed directly to Step 2** without waiting for confirmation; if the user has changes they can send a message
- **`filter_characters` is the most important check for multi-character scripts**: identity_anchor must be identical across all shots; if inconsistencies are found, immediately use `edit` to unify them
- **Dialogue attribution must be verified**: mixed-up dialogue in multi-character scenes is a serious problem; confirm each line with `filter_dialogs`
- **Do not use tail frames**: Step 2 prompt already declares no tail frames; Step 5 is responsible for clearing any residual tail frames auto-generated by S0; tail frames cause abnormal blending at video boundaries
- **Check images grouped by character**, not in sequential order — putting all shots of the same character together for comparison makes deviations much easier to spot
- **Close-up / extreme close-up shots must have their eyes checked**: AI close-up characters are prone to glassy eyes; fix with I2I immediately when found
- **Check the axis line in dialogue shots**: in shot-reverse-shot sequences, the speaker's and listener's facing directions must not be confused; if found, regenerate and explicitly specify the facing direction
- **Multi-character voice descriptions must have an emotional direction** — do not just write "male / female voice"; vocal texture and emotional baseline are the key
- **undo/redo**: `workspace.btn_undo` / `workspace.btn_redo` can revert accidental operations
- BGM description goes in the `global.bgm` field; don't forget to set it

---

## Appendix: Shot Description Reference

### Effective writing for each framing type

S0 parses scripts by inferring framing and composition from shot descriptions; the more precise the description, the more the generated image matches the intent.

**Description formula**: `[framing] + [subject position / facing direction] + [action / expression / emotion] + [key visual elements] + [lighting] + [depth of field]`

---

**Wide / Establishing Shot**
- Purpose: establishes spatial feel, opening orientation, expresses isolation
- Writing focus: environment dominates, person is small; describe environment first, then person's position
```
Example:
Wide interior of a café, afternoon warm sunlight streaming in at an angle, wooden tables and chairs, Lin Xiao sitting alone
at a window seat on the left, figure relatively small, background is blurred other patrons and interior furnishings, overall frame spacious and quiet
```

---

**Medium Shot**
- Purpose: primary framing for dialogue scenes, shows both expression and body language simultaneously
- Writing focus: character from waist up, specify facing direction (in dialogue, two people face each other)
```
Single-person medium shot example:
Medium shot, Chen Ming from waist up, facing left of frame, brow slightly furrowed and lips pressed tight (suppressed emotion),
gray-blue blazer, background is a softly blurred café environment, shallow depth of field

Two-person medium shot example (both in frame):
Medium shot, Lin Xiao sitting on the left side of the frame facing right looking at Chen Ming, Chen Ming sitting on the right side of the frame facing left looking at Lin Xiao,
a tabletop between them, each with a preoccupied expression, afternoon side light, background shallow depth of field blur
```

---

**Over-the-Shoulder Shot**
- Purpose: establishes the relationship between two people in conversation, places the viewer in one character's perspective
- Writing focus: specify clearly who is in the foreground (back to camera) and who is in the mid-ground (facing the camera)
```
Example:
Over-the-shoulder shot, Chen Ming's right shoulder and back of head in the left foreground (blurred), Lin Xiao in the mid-ground on the right,
facing the camera directly, expression attentive with a hint of hesitation, café environment blurred in background
```

---

**Close-up / Extreme Close-up**
- Purpose: emotional peak, key dialogue landing, revealing inner state
- Writing focus: shoulders-up or face only; **must** add "eyes sharp and clear," otherwise AI tends to generate glassy eyes
```
Emotional close-up example:
Close-up, Lin Xiao's face, eyes slightly reddened, gaze complex and hesitant, faint glimmer of tears,
lips lightly pressed, eyes sharp and clear (focus on the eyes), background fully blurred,
afternoon warm light from the side, rim light outlining hair

Object close-up example:
Close-up, a cup of coffee on a table, slight condensation on the rim, Lin Xiao's hand beside it (
resting naturally, not the focus), background blurred, warm lighting, composition leaning left
```

---

**Shot-Reverse-Shot**

Shot-reverse-shot is the standard structure for dialogue scenes, but AI most commonly makes the error of both characters facing the same direction.
**Axis rule**: once the two characters' spatial positions are established (e.g., A on the left, B on the right), in all shot-reverse-shot cuts A always faces right and B always faces left — this cannot be swapped arbitrarily.

```
Shot A (Lin Xiao speaking):
Medium shot, Lin Xiao on the left side of the frame, facing right looking at Chen Ming, brow slightly furrowed, [expression],
Chen Ming's back / profile softly blurred at the right edge of the frame

Shot B (Chen Ming reacting):
Medium shot, Chen Ming on the right side of the frame, facing left looking at Lin Xiao, corner of mouth lightly pressed, [expression],
Lin Xiao's back / profile softly blurred at the left edge of the frame
```

---

### Common AI pitfalls in generating dramatic content

| Problem | Trigger Scenario | Prevention / Fix |
|---------|-----------------|-----------------|
| Glassy, expressionless eyes | Close-up, extreme close-up shots | Add "eyes sharp and clear, focus on the eyes" to description |
| Distorted hands (6 fingers) | When hands are relatively clear in frame | Avoid hand close-ups; if necessary, be extremely specific ("right hand five fingers naturally wrapped around the cup") |
| Both characters facing the same direction | Two-person dialogue shot | Explicitly specify both characters' facing directions ("A faces right, B faces left") |
| Ghostly / distorted background figures | Scenes with blurred crowds | Add "background figures completely blurred, no discernible details" |
| Clothing color drift | Can happen every generation | Assist descriptions with reference objects; focus on color during filter_characters check |
| Inconsistent lighting style across shots | Multiple shots in the same scene | Repeat key lighting keywords in each shot description (e.g., "afternoon diagonal natural light from the left") |
| Character age feel drifting | Same character across different shots | Add age anchor word to description ("approximately 25 years old") rather than relying on appearance alone |

---

## Supported Script Formats

The S0 Pipeline can automatically recognize and convert the following formats; Claude does not need to handle them manually:
- **Chinese multi-character dialogue script** ("Character: line" format)
- **English shot list / screenplay** (with timecodes, framing annotations: INT./EXT., CLOSE-UP, etc.)
- **Vietnamese / Russian and other narrative text drafts** (automatically processed as novel type; S0 auto-converts to shotlist)
