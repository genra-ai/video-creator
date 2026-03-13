# Video Continuation — AI Bridge Workflow

Read an existing video project, determine the content type, incorporate the user's continuation requirements, generate subsequent shots, and complete the full generation pipeline for the corresponding type.

## Workflow Overview

```
Step 0: Retrieve connection info, open the existing project
Step 1: Read project content → determine type → extract continuity elements
Step 2: Understand continuation requirements → design subsequent shots (show to user, proceed immediately)
Step 3: Send the continuation script (with continuity elements)
Step 4: Filter check
Step 5: Tail frame handling (varies by type)
Step 6: Generate audio
Step 7: Generate video
```

---

## Step 0: Retrieve Connection Info, Open the Existing Project

Call `get_state` to get login status. If not logged in, show `login_url`.

After login, locate the target project in the project list and click to enter the corresponding draft:

```
click: dashboard.chat.{projectId}.{chatId}
```

---

## Step 1: Read Project Content → Determine Type → Extract Continuity Elements

Call the following filters in sequence, **recording each item in full**:

```
sidebar.filter.all        → global style, BGM description, total shot count
sidebar.filter.shots      → all shot descriptions, durations, last 2 shots (continuation connection points)
sidebar.filter.dialogs    → dialog content, character attribution, narration/character dialog type
sidebar.filter.characters → identity_anchor for all characters (exact original text, do not alter)
sidebar.filter.locations  → all scene descriptions (exact original text, do not alter)
```

### Type Determination (inferred from content semantics)

| Characteristics | Determined Type |
|------|---------|
| Has character + dialog, dialog involves ≥2 characters in conversation | **script-to-video** |
| Has character + dialog, only 1 character/narrator, fixed framing, speaks directly to camera | **voiceover** |
| Has narration + product feature/selling point descriptions, core is feature demonstration | **product-showcase** |
| No characters/dialog, pure visuals + BGM, emotion/brand atmosphere driven, no product feature description | **ad-to-video** |
| No characters/dialog, pure visuals + BGM, shot descriptions contain reference photo asset_id | **photo-vlog** |

> **Core distinction between ad-to-video and product-showcase**: ad-to-video is a brand atmosphere ad (builds the brand's emotional world, product naturally integrated); product-showcase is an e-commerce product feature ad (each shot serves a visualizable selling point). Judge by the focus of shot descriptions — writing about emotion/light/atmosphere → ad-to-video; writing about product angles/features/narration lines → product-showcase.

### Show Analysis Results to User

```
[Existing Project Analysis]

Type: [determined type]
Existing shot count: N shots, approx. Xs
Global style: [...]
BGM: [...]

Characters: (list for script-to-video / voiceover)
- [Character name]: [identity_anchor original text]

Scenes: (list for script-to-video / voiceover)
- [Scene name]: [description original text]

Last 2 shots (continuation connection points):
- Shot N-1: [description summary]
- Shot N: [description summary]
```

---

## Step 2: Understand Continuation Requirements → Design Subsequent Shots

Based on the user's continuation requirements (content direction, shot count, ending, etc.), design the subsequent shots following the storyboard logic of the corresponding type.

**Continuity requirements**:
- Style, BGM, and color tone must remain consistent with the original project
- Narrative must flow naturally from the last shot without content jumps
- script-to-video / voiceover: character appearance and scene definitions must remain unchanged verbatim

Show the shot draft to the user, **proceed directly to Step 3 without waiting for confirmation**:

```
[Continuation Shot Plan]

Continuation shot count: N shots, approx. Xs (continuing after shot M of the original project)
Narrative continuation point: [explain where the continuation picks up]

Continuation shot N+1 (Xs) - [shot type/content summary]
Continuation shot N+2 (Xs) - [...]
...

(Sending continuation script now...)
```

---

## Step 3: Send the Continuation Script

Edit via `chat.input` and send. The message header must include the continuity elements.

### [script-to-video Continuation]

Character definitions must be **word-for-word identical** to the original project; scene definitions likewise:

```
Please continue the current project by adding the following continuation shots.

Character appearance reminder (exactly identical to existing shots, cannot be changed):
- [Character name]: [identity_anchor full original text]
- [Character name]: [identity_anchor full original text]

Scene reminder:
- [Scene name]: [original description]

Image generation requirements: each shot corresponds to a complete cinematic composition at a single point in time, with no dividing lines or multi-angle collages. Each shot requires only a start frame; do not set a tail frame (tail_frame).

--- Continuation Shots ---

[Shot N+1] [duration]s | [framing/shot type]
Visual: [description]
Line: "[dialog]" (include when there is dialog; omit otherwise)

[Shot N+2] [duration]s | [framing/shot type]
Visual: [description]
Line: "[dialog]"
...
```

> Send ≤8 continuation shots in one message; if >8, split into two messages and repeat the character appearance reminder in the second message.

### [voiceover Continuation]

Character and scene definitions must be exactly identical to the original project:

```
Please continue the current project by adding the following continuation shots.

Character (exactly identical to existing shots):
- [Character name]: [identity_anchor full original text], speaking directly to camera, relatively fast pace

Scene (exactly identical to existing shots):
- [Scene name]: [original description]

Image generation requirements: framing fixed at medium shot, the character's size and position in the frame must be completely identical to existing shots. Each shot requires only a start frame; do not set a tail frame (tail_frame).

--- Continuation Shots ---

[Shot N+1] [duration]s
Visual: medium shot, [character name] facing camera, [expression/action state]
Line: "[dialog]"

[Shot N+2] [duration]s
Visual: medium shot, [character name] facing camera, [expression/action state]
Line: "[dialog]"
...
```

### [product-showcase Continuation]

```
Please continue the current project by adding the following continuation shots.

Continuation style: [global visual style original text read from the existing project]
Product: consistent with existing shots

Image generation requirements: product must always be clearly visible. Each shot requires only a start frame; do not set a tail frame (tail_frame).

--- Continuation Shots ---

[Shot N+1] [duration]s | [shot type]
Visual: [description]
Narration: "[line]"

[Shot N+2] [duration]s | [shot type]
Visual: [description]
Narration: "[line]"
...
```

### [ad-to-video Continuation]

```
Please continue the current project by adding the following continuation shots.

Continuation style: [global visual style original text read from the existing project]
Continuation BGM: [BGM description original text]

Image generation requirements: each shot corresponds to a complete cinematic composition at a single point in time, with no dividing lines or multi-angle collages. Each shot requires only a start frame; do not set a tail frame (tail_frame).

--- Continuation Shots ---

[Shot N+1] [duration]s | [shot type]
Visual: [description]

[Shot N+2] [duration]s | [shot type]
Visual: [description]
...
```

### [photo-vlog Continuation]

Upload the new photos first and record the asset_id:

```
upload: new_photo.jpg → asset_id_new
```

Then send the script with the asset_id written into the shot description:

```
Please continue the current project by adding the following continuation shots. Each shot requires only a start frame; do not set a tail frame (tail_frame).

--- Continuation Shots ---

[Shot N+1] [duration]s
Shot description: Reference original photo $asset_id_new1, preserve the original photo's composition, color tone, and main subject; use this photo as the basis for generating the start frame. [supplementary description]
Camera movement: [camera movement description]
...
```

Wait for completion after sending.

---

## Step 4: Filter Check

Call `sidebar.filter.shots` to check the continuation shots:
- Whether the shot descriptions were correctly parsed
- Whether the duration is sufficient to deliver the dialog (when dialog is present)

Call `sidebar.filter.dialogs` to check dialog:
- Whether dialog attribution is correct (script-to-video: multi-character lines must not be mixed up)
- Whether narration shot content is complete

Call `sidebar.filter.characters` (script-to-video / voiceover):
- Whether the character identity_anchor for continuation shots is completely identical to existing shots
- If any discrepancy is found, correct it immediately using `edit`

**Fix issues immediately using `edit` as they are found — do not save them up for the end.**

---

## Step 5: Tail Frame Handling

### voiceover — Set Start and Tail Frames (Adjacent Shot Continuity)

First call `get_state` or `sidebar.filter.shots` to record the start_frame asset_id of **all shots** (both existing and continuation).

Send one message per tail frame setting, **send each message separately, wait for a response before sending the next**:

```
Send message: "Please set the tail frame (tail_frame) of shot [shot_id of last existing shot] to $<start_frame_asset_id of continuation shot 1>"
Send message: "Please set the tail frame (tail_frame) of shot [shot_id of continuation shot 1] to $<start_frame_asset_id of continuation shot 2>"
Send message: "Please set the tail frame (tail_frame) of shot [shot_id of continuation shot 2] to $<start_frame_asset_id of continuation shot 3>"
...(the last continuation shot is not set; leave as default)
```

After setting, call `get_state` to verify: each shot (except the last) has a tail_frame, and the asset_id matches the start frame of the next shot.

### script-to-video / product-showcase / ad-to-video / photo-vlog — Clear All Tail Frames

Check whether the continuation shots have any tail frames; if so, send a message to clear them:

```
Send message: "Please clear the tail frames (tail_frame) of all continuation shots, keeping only the start frame"
```

Call `sidebar.filter.shots` to confirm that all continuation shots have only a start_frame and no end_frame / tail_frame.

---

## Step 6: Generate Audio

Click `workspace.btn_pipeline_dialogs`, **select only the audio items for the continuation shots** (existing shots already have audio generated; do not regenerate):

- Projects with BGM: BGM usually already exists. If the total duration changes after continuation and BGM becomes insufficient, regenerate the BGM
- Projects with dialog/narration: select only the dialog items corresponding to the continuation shots

Confirm and wait for completion.

---

## Step 7: Generate Video

Click `workspace.btn_pipeline_videos`, **select only the video items for the continuation shots** (existing shot videos are already generated; do not regenerate):

- photo-vlog: check only video, do not check frame/image (reference photos already exist; do not have AI regenerate images)
- Other types: select all video items for the continuation shots

Confirm and wait for completion.

---

## Key Learnings

- **Type determination is semantic**: ad-to-video is identified by emotion/atmosphere/brand drive; product-showcase by selling points/features/narration drive; do not judge by whether a product is present (both can have a product)
- **Copy continuity elements verbatim**: read the character identity_anchor and scene descriptions from the filter, then paste them into the script exactly as-is without changing any word — any change will inevitably cause character appearance drift
- **voiceover start/tail frames must cover the seam between existing and continuation**: in addition to the start/tail frames within the continuation shots themselves, the tail_frame of the last existing shot must also be set to the start_frame of the first continuation shot; otherwise there will be a jump cut at the seam
- **Only generate audio and video for the continuation portion**: do not regenerate existing shots to avoid unnecessary consumption and overwriting existing content
- **The narrative continuation point must be explicit**: the storyboard design in Step 2 must flow naturally from the content of the last existing shot, and the relationship to the preceding shot must be noted in the script
- **undo/redo**: `workspace.btn_undo` / `workspace.btn_redo` can reverse accidental operations
