# Video Continuation

Reads an existing video project, identifies its type, and extends it with new shots following the same style, characters, and narrative logic.

## Key Principles

- **Copy continuity elements verbatim** — read `identity_anchor` and scene descriptions from the filter, paste them into the continuation script word-for-word; any change causes character drift
- **Type determination is semantic** — ad-to-video is identified by emotion/atmosphere drive; product-showcase by selling-points/features/narration drive; a product can appear in both
- **Only generate audio and video for the new shots** — never regenerate existing shots
- **voiceover seam requires special handling** — the tail_frame of the last existing shot must be set to the start_frame of the first new shot
- **Narrative must flow naturally** — the first new shot picks up directly from the last existing shot

## Workflow

### 1. Read Project → Determine Type → Extract Continuity Elements

Read the project filters in sequence and record everything:
- All: global style, BGM description, total shot count
- Shots: all descriptions, durations, last 2 shots (the continuation connection points)
- Dialogs: content, character attribution, narration vs. character dialog
- Characters: `identity_anchor` for every character — exact original text, do not alter
- Locations: all scene descriptions — exact original text, do not alter

**Type determination:**

| Characteristics | Type |
|----------------|------|
| ≥2 characters in conversation | script-to-video |
| 1 character/narrator, fixed framing, speaks to camera | voiceover |
| Narration + product features/selling points | product-showcase |
| No characters/dialog, pure visuals + BGM, emotion/brand atmosphere | ad-to-video |
| No characters/dialog, shot descriptions contain reference photo asset_ids | photo-vlog |

> **ad-to-video vs. product-showcase**: judge by shot description focus — emotion/light/atmosphere → ad-to-video; product angle/feature/narration line → product-showcase.

Show the analysis to the user: determined type, shot count, style, BGM, characters (if any), last 2 shots.

### 2. Design Continuation Shots

Follow the storyboard logic of the identified type. Continuity requirements:
- Style, BGM, and color tone remain consistent with the original
- Narrative flows naturally from the last existing shot — no content jumps
- script-to-video / voiceover: character and scene definitions must be verbatim identical

Show the shot plan to the user, then proceed to Step 3 immediately.

### 3. Send Continuation Script

Send one message. The message header must include continuity elements:

**All types**: re-state global style and BGM from the original. Declare: each shot needs only a start frame, no tail frames.

**script-to-video**: include word-for-word character `identity_anchor` and scene descriptions as a reminder. If >8 new shots, split into two messages and repeat the character reminder in the second.

**voiceover**: include character identity and scene verbatim. State: medium shot fixed framing, character size/position identical to existing shots.

**product-showcase**: state product must be clearly visible in every shot.

**photo-vlog**: upload new photos first, record asset_ids. Write `Reference original image $asset_id` at the start of each shot's visual description.

### 4. Filter Check

Check shots: new shots correctly parsed, durations sufficient for dialog.

Check dialogs: attribution correct; for script-to-video, multi-character lines not mixed up.

Check characters (script-to-video / voiceover): `identity_anchor` for new shots is word-for-word identical to existing shots. Fix any discrepancy immediately.

### 5. Tail Frame Handling

**voiceover**: set tail frames across the seam and within all new shots.
- The last existing shot's tail_frame → start_frame of new shot 1
- Each new shot's tail_frame → start_frame of the next new shot
- Last new shot: no tail frame needed
- Send one message per tail frame, wait for response before sending the next — do not batch. Verify the `tail_frame` field is correct after each; retry up to 3 times if not set. Only move to the next shot after confirming.

**All other types**: check new shots for any auto-generated tail frames; if found, send a message to clear them. Verify afterward.

### 6. Generate Audio

Select only audio items for the new shots — do not regenerate existing audio. If total duration increased and BGM is now too short, regenerate BGM only.

### 7. Generate Video

Select only video items for the new shots — do not regenerate existing videos.

**photo-vlog**: select video only, never frame/image (reference photos already exist).
