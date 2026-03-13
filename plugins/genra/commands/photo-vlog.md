# Photo Vlog — AI Bridge Workflow

Turn 3-10 real photos uploaded by the user into a 30-60 second narrative Vlog short video.
If no photos are provided, autonomously design character appearance and scenes, entering no-photo mode.
Reference perception: travel Vlog, daily life records, party recaps, food exploration.

## Workflow Overview

```
Step 0: Obtain connection information
Step 1: Analyze photo set → design Vlog plan (self-review, then present, continue directly)
Step 2: Upload photos in parallel → create project → send complete script at once
Step 3: Filter check
Step 4: Clear all tail frames (Vlog hard-cut style)
Step 5: Generate audio (BGM as primary)
Step 6: Generate video (video only; photos serve directly as start frames, no regeneration)
```

---

## Step 0: Obtain Connection Information

Call `get_state` to get login status. If not logged in, show the `login_url` to the user; after authorization, enter the project list.

---

## Step 0.5 (when no photos): Autonomously Design Character Appearance + Scenes

**Trigger condition**: Execute when the user has not provided any photos; if photos are provided, skip directly to Step 1.

> Claude does not generate images; this step produces text descriptions, and the video editor AI is responsible for generating the actual images.

### ① Character Appearance Design

Based on user cues (or entirely at your own discretion), design a memorable character:

| Element | Example |
|------|------|
| Gender/age feel | Female in her 20s |
| Appearance features | Short curly hair, warm smile, natural makeup |
| Outfit style | White oversized hoodie + jeans + canvas shoes |
| Theme/scene | Weekend city stroll: café, alley, park, bookstore |

Write a **unified character appearance description** (reused across all subsequent shots):

```
Character base description:
An Asian female in her early-to-mid 20s, short curly hair, natural makeup, white oversized hoodie with jeans,
expression warm and natural, image style bright Japanese film grain feel
```

### ② Scene List Design (6-8 scenes)

| # | Segment | Scene Description (used directly in script) |
|---|------|----------------------|
| 1 | Opening tone-setter | In front of floor-to-ceiling café window, girl holding a latte, turning sideways to look out, warm light, medium close-up |
| 2-5 | Process highlights | [descriptions for each scene] |
| 6 | Emotional freeze frame | Evening street, girl turns back and smiles, golden-hour backlight |
| 7 | Closing | Wide-angle city skyline, sunset afterglow |

> **Description formula**: `[location/environment] + [character action/state] + [lighting/atmosphere] + [composition/shot size]`
> Each description 20-40 characters; the more specific the details, the better the generation result.

### ③ Present Plan, Proceed Directly to Step 2

```
[No-Photo Mode — Auto-Designed Plan]

Character appearance: [...]
Theme: [...], approx. N seconds
Style: [...]
BGM: [...]

Scene list:
#1 (3s) - slow pull back: [scene description]
#2 (4s) - horizontal pan: [scene description]
...
```

---

## Step 1: Analyze Each Photo → Finalize Each Shot → Narrative Ordering

**Three steps in sequence — do not mix them up**: first understand each photo, then produce a plan for each photo, then assemble them along an emotional arc.

---

### ① Analyze Each Photo (understand each one)

Read each photo in turn and build one record per photo:

| No. | Content Description | Emotional Intensity | Composition Type | Narrative Role Candidates |
|------|---------|--------|--------|-----------|
| P1 | Café by the window, warm side-light profile | ★★★★ High | Character medium close-up | Opening / Emotional freeze frame |
| P2 | Street wide shot, blurred crowd | ★★☆ Medium-low | Environmental wide shot | Transition / Closing |
| ... | ... | ... | ... | ... |

**Analysis points for each photo**:
- **Subject**: Character / scenery / food / architecture / detail object
- **Composition type**: Wide/establishing shot / character close-up / detail close-up / group photo
- **Lighting/atmosphere**: Warm light/cool light/backlight/flat light; what is the atmospheric feel
- **Emotional intensity**: 1-5 stars; how strong an emotional resonance this photo can evoke

---

### ② Finalize Each Shot (content determines camera movement and copy)

Based on the analysis of each photo, determine the plan shot by shot, with **a causal logic between content → camera movement/copy**:

| Composition Type | Recommended Camera Movement | Reason |
|--------|--------|------|
| Wide/establishing shot/landmark | Slow pull back or horizontal pan | Macro feel needs time to unfold |
| Character close-up/expression | Slow push in | Moving toward the emotional focal point |
| Group photo | Horizontal pan (left → right) | Scanning feel, letting the audience see each person |
| Food/detail close-up | Slow push in (focus on detail) | Guide the eye to the most appealing part |
| The most emotionally intense photo | Static freeze frame | Empty space, letting the audience linger in this moment |
| Joyful/lively/party | Slight handheld shake | Adds immediacy and joyful atmosphere |

**Voiceover judgment**: **Default is no voiceover for the entire film**; BGM tells the story. Voiceover breaks the immersion of a Vlog and makes it feel like a talking-head video.
- When the user explicitly requests voiceover: a maximum of 1-3 sentences, only at the opening or closing to mark the theme; all other shots have no voiceover
- Voiceover style: conversational, no more than 10 characters per sentence, lightly touching the theme

Output for each photo:
```
P1: [brief content description]
→ Camera movement: slow push in (character emotion close-up, moving toward focal point)
→ Duration: 4s (high emotion, slightly longer for breathing room)
→ Voiceover: "Finally here, three days in Kyoto" (opening theme-setter)

P2: [brief content description]
→ Camera movement: horizontal pan right (wide street, opening up the sense of space)
→ Duration: 3s
→ Voiceover: none
```

---

### ③ Narrative Ordering (assemble finalized shots along an emotional arc)

Take the shots with finalized camera movement + voiceover and reorder them according to the following structure — **not necessarily in the order they were taken**:

| Segment | Number of Shots | Selection Principle |
|------|------|--------|
| Opening tone-setter | 1-2 | Highest emotional intensity, or best at conveying location/atmosphere |
| Process highlights | 3-6 | Medium emotional intensity, rhythm has rise and fall, camera movements should alternate |
| Emotional freeze frame | 1-2 | Highest emotional intensity, static freeze frame, slightly longer breathing room |
| Closing | 1 | Wide shot/group photo/most representative, clean and crisp |

**Camera movement alternation check**: After ordering, check whether adjacent shots alternate camera movements (push in → pan → pull back → push in). If consecutive shots have the same movement, adjust the order.

---

### ④ Infer Theme + Determine BGM

| Theme | Photo Signals |
|------|--------|
| Travel record | Landmarks, scenery, transportation, multi-scene switching |
| Party/activity | Group photos, happy expressions, dining table/party |
| Food exploration | Food close-ups, restaurant environment, holding food |
| Daily life | Home, street shots, coffee, everyday objects |
| Sports/outdoors | Equipment, natural scenery, physical activity state |

| Vlog Theme | BGM Description |
|---------|---------|
| Travel/outdoors | Light acoustic guitar + light percussion, BPM 110, open and breezy, has breathing feel, no lyrics |
| Party/birthday | Upbeat piano + light drums, BPM 120, warm and joyful, lively rhythm, no lyrics |
| Daily life/coffee | Lazy jazz guitar, BPM 80, warm and soothing, afternoon café atmosphere |
| Food exploration | Light cheerful whistle + strings, BPM 100, relaxed and curious, sense of discovery, no lyrics |
| Sports/nature | Fresh electronic + natural sound feel, BPM 115, full of energy, open feel |

**BGM tempo determines duration baseline**: Fast tempo (BPM 120+) → 2-3s per shot; relaxed (BPM 80-100) → 4-5s per shot

---

### ⑤ Present Plan to User, Proceed Directly to Step 2

```
[Photo Vlog Plan]
Theme: [...], approx. N seconds
Style: [light/warm/healing]
BGM: [...]
Voiceover: none (default pure BGM; only added if user requests)

Shot order (arranged along emotional arc):
#1 (4s) - [content description] - camera: slow pull back
Voiceover: "[opening copy]"

#2 (3s) - [content description] - camera: horizontal pan right
Voiceover: none

...

#N (4s) - [content description] - camera: static freeze frame
Voiceover: "[closing copy]"

(Uploading photos now...)
```

---

## Step 2: Upload Photos in Parallel → Create Project → Send Script

### ① Upload All Photos in Parallel

**Upload all photos simultaneously, do not wait in sequence**; record asset_id after all are complete:

```
Parallel upload:
photo1.jpg → asset_id_1
photo2.jpg → asset_id_2
photo3.jpg → asset_id_3
...(all photos initiated at the same time)
```

### ② Create Project

Create a new project; set: name, language zh-CN.

### ③ Send Script (all shots in one single message)

**[With photos]**

```
Please create a Vlog video project based on the following script, in Chinese.

Style: [light/warm/daily record], handheld feel, photo flow feel
BGM: [specific description, e.g., "warm and light acoustic guitar music, BPM 100, no lyrics"]
Voiceover: no voiceover; BGM tells the story (add only if user has specific request)

Each shot only needs a start frame; do not set a tail frame (tail_frame).

--- Storyboard script below ---

[Shot 1] 3s | Opening tone-setter
Visual description: Reference original image $asset_id_1, retain the composition, color tone, and subject of the original image, use this photo as the basis for generating the start frame. [supplementary visual description]
Camera movement: slow pull back, slowly push outward from center

[Shot 2] 4s | Process record
Visual description: Reference original image $asset_id_2, retain the composition, color tone, and subject of the original image, use this photo as the basis for generating the start frame. [supplementary visual description]
Camera movement: horizontal pan slowly to the right

...

[Shot N] 4s | Closing
Visual description: Reference original image $asset_id_N, retain the composition, color tone, and subject of the original image, use this photo as the basis for generating the start frame. [supplementary visual description]
Camera movement: static freeze frame
```

> **Note**: The asset_id goes in `Visual description` (i.e., `{frameId}.description`), which is the prompt read directly during image generation; the system will use the uploaded photo as an img2img reference to generate the start frame. `[supplementary visual description]` should be filled with the specific content for that shot analyzed in Step 1 (lighting, composition, subject) — the more detailed, the better, helping the system more accurately reproduce the original image.

**[No photos]**

Do not upload files; send the script directly, replacing asset_id with the scene descriptions from Step 0.5:

```
(Format is the same as with photos; remove "Reference original image $asset_id", keep only the scene text description)

Important note: This project has no user-uploaded photos; please generate images based on the visual descriptions, and do not set tail frames.
```

Send and wait for completion.

---

## Step 3: Filter Check

Call `sidebar.filter.shots` to check shots:
- Does each shot's start_frame correspond to a user photo (img tag)?
- Do camera movement descriptions alternate; not all the same type?
- Are shots with voiceover long enough for the dialogue to be spoken?

Call `sidebar.filter.dialogs` to check dialogue:
- No more than 3 voiceover shots, and only at the opening or closing
- Dialogue is conversational and naturally relaxed

**Fix any issues immediately using `edit`; do not accumulate them until the end.**

---

## Step 4: Clear All Tail Frames

Send one message: "Please clear all tail frames (tail_frame) from all shots, keeping only the start frame"

After waiting for completion, call `filter.shots` again to verify:
- All shots have only a start_frame, no end_frame entries
- **Only proceed to Step 5 after verification passes**

---

## Step 5: Generate Audio

Click `workspace.btn_pipeline_dialogs`, confirm all items, click generate, and wait for completion.

**BGM description formula**: `[instrument texture] + [BPM/rhythm] + [emotional arc] + [overall atmosphere]`

> **Default no voiceover**. The Vlog tells its story through visuals + BGM; voiceover breaks the immersion. Add it only when the user explicitly requests it, and at most 1-2 sentences (opening theme-setter or closing summary), conversational, lightly touched on.

---

## Step 6: Generate Video

Click `workspace.btn_pipeline_videos`.

**[With photos]**: Select only the video items, **do not check frame/image generation** (real photos already exist; do not let AI regenerate and overwrite the images)

**[No photos — Step 0.5 mode]**: Check both frame/image + video generation

Select all shots and confirm; wait for completion.

---

## Key Learnings

- **Photo ordering is the soul**: Open with the most visually striking photo, not necessarily the first taken chronologically; save the warmest photo for the emotional freeze frame
- **Camera movements must alternate**: Push in → pan → pull back → push in; do not use the same movement consecutively, or there will be no sense of rhythm
- **BGM tempo determines shot duration**: Decide the BGM first, then determine each shot's duration based on the tempo
- **asset_id must be written into the visual description**: Put `Reference original image $asset_id` in `{frameId}.description` (i.e., the "visual description" field in the script); this is the prompt read directly during image generation, and only then will the system use the uploaded photo as an img2img reference. Writing it anywhere else (e.g., metadata, global notes) does not guarantee it will be read during the image generation stage
- **Default no voiceover**: Unless the user explicitly requests it, BGM tells the story; voiceover turns the Vlog into a talking-head video
- **No tail frames**: Hard cuts are more natural for Vlogs; Step 4 must be cleared before proceeding to Step 5
- **Only select video for video generation**: After images are complete, only generate video; do not regenerate frames
- **Upload in parallel**: Upload all photos simultaneously; do not wait in sequence
- **Duration control**: 3-10 photos → 30-60 second finished product, average 4s per shot

---

## Appendix

### Narrative Structure Quick Reference

| Vlog Type | Recommended Narrative Structure |
|---------|-----------|
| Travel | Departure/transportation → landmark check-ins → food/experiences → night view/wide-shot closing |
| Party/birthday | Venue/decorations → group gathering → peak interaction → group photo closing |
| Food exploration | Exterior/sign → dish close-ups → tasting/enjoying → favorite dish as closing |
| Daily record | Morning/waking up → daily activities → small happy moments → evening/ending |
