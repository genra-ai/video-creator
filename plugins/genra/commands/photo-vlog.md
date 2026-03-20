---
name: genra:photo-vlog
description: Use this skill when the user wants to convert 3–10 real photos into a 30–60 second narrative vlog video using img2img. Triggered by: "photo vlog", "make my photos into a video", "照片转视频".
---

# Photos to Vlog

Turns 3–10 real photos into a 30–60s narrative Vlog short video. If no photos are provided, design character appearance and scenes autonomously (no-photo mode).

## Key Principles

- **Photo ordering is the soul** — open with the most visually striking photo, not chronological order; save the warmest for the emotional freeze frame
- **Camera movements must alternate** — push in → pan → pull back → push in; same movement twice = no rhythm
- **BGM tempo determines shot duration** — BPM 120+: 2–3s per shot; BPM 80–100: 4–5s per shot
- **asset_id must go into the shot's visual description field** — write `Reference original image $asset_id` in the shot description (the image generation prompt); writing it anywhere else won't reach the generation pipeline
- **Default: no voiceover** — BGM tells the story; voiceover turns the Vlog into a talking-head video
- **No tail frames** (hard cuts are more natural for Vlogs)
- **When generating video, select video only** — never regenerate frame/image when real photos exist

## Workflow

### 1. Analyze Photos → Storyboard Plan

**No-photo mode**: Design a character appearance (gender/age/hair/outfit/signature detail) and 6–8 scenes. Description formula: `[location] + [character action/state] + [lighting/atmosphere] + [shot size]`. Then proceed to Step 2 with text descriptions in place of asset_ids.

**With photos** — three steps in order:

**① Analyze each photo:**

| No. | Content | Emotional Intensity | Composition Type | Narrative Role Candidates |
|-----|---------|--------------------|-----------------|-----------------------------|
| P1 | ... | ★★★★ | Character close-up | Opening / Emotional freeze frame |
| P2 | ... | ★★ | Wide/establishing | Transition / Closing |

Assess: subject, composition type, lighting/atmosphere, emotional intensity (1–5★).

**② Plan each shot** — camera movement follows from composition type:

| Composition Type | Camera Movement | Reason |
|-----------------|----------------|--------|
| Wide/establishing/landmark | Slow pull back or horizontal pan | Macro feel needs time to unfold |
| Character close-up/expression | Slow push in | Moving toward emotional focal point |
| Group photo | Horizontal pan (left → right) | Scanning feel |
| Food/detail close-up | Slow push in | Guide eye to most appealing part |
| Most emotionally intense photo | Static freeze frame | Let the audience linger |
| Joyful/party | Slight handheld shake | Adds immediacy |

Voiceover: default none. If user requests it, max 1–3 sentences at opening or closing only — conversational, ≤10 chars per sentence, lightly touching the theme.

**③ Narrative ordering** — reassemble shots along an emotional arc (not chronological):

| Segment | Shots | Selection Principle |
|---------|-------|-------------------|
| Opening tone-setter | 1–2 | Highest emotional intensity or best at conveying location/atmosphere |
| Process highlights | 3–6 | Medium intensity, alternating camera movements |
| Emotional freeze frame | 1–2 | Highest intensity, static freeze, slightly longer |
| Closing | 1 | Wide shot or most representative, clean and crisp |

After ordering, verify adjacent shots alternate camera movements. If two consecutive shots share the same movement, adjust the order.

**BGM** — infer from photo content:

| Theme | Photo Signals | BGM |
|-------|--------------|-----|
| Travel/outdoors | Landmarks, scenery, transportation | Light acoustic guitar + percussion, BPM 110, open and breezy |
| Party/birthday | Group photos, dining, celebrations | Upbeat piano + light drums, BPM 120, warm and joyful |
| Daily life/café | Home, street, coffee, everyday objects | Lazy jazz guitar, BPM 80, afternoon café feel |
| Food exploration | Food close-ups, restaurant environment | Light whistle + strings, BPM 100, relaxed and curious |
| Sports/nature | Equipment, natural scenery, activity | Fresh electronic, BPM 115, full of energy |

Show the plan to the user, then proceed to Step 2 immediately.

### 2. Upload Photos & Send Script

Upload all photos simultaneously (not sequentially) — record each asset_id after all complete.

Send one message with all shots. For each shot with a photo, the visual description must begin with:
`Reference original image $asset_id_N, retain the composition, color tone, and subject of the original image, use this photo as the basis for generating the start frame.` followed by supplementary details from the Step 1 analysis (lighting, composition, subject).

No-photo mode: omit the reference line, use scene text descriptions only.

Include in the message: style, BGM description, no tail frames instruction.

### 3. Filter Check

Check shots: camera movements alternate, no two consecutive shots use the same type; voiceover shots are long enough for dialog.

Check dialogs: ≤3 voiceover lines total, only at opening or closing; tone is conversational.

Fix any issues immediately.

### 4. Clear All Tail Frames

Send a message to clear all tail frames, keep only start frames. Verify before proceeding.

### 5. Generate Audio

Generate BGM (and voiceover if present). **BGM formula**: `[instrument texture] + [BPM/rhythm] + [emotional arc] + [overall atmosphere]`

### 6. Generate Video

**With photos**: select video only — do NOT select frame/image (real photos already exist; regenerating overwrites them).

**No-photo mode**: select both frame/image and video.

---

## Narrative Structure Reference

| Vlog Type | Recommended Structure |
|-----------|----------------------|
| Travel | Departure/transport → landmark check-ins → food/experiences → night view/wide-shot closing |
| Party/birthday | Venue/decorations → group gathering → peak interaction → group photo closing |
| Food exploration | Exterior/sign → dish close-ups → tasting → favorite dish as closing |
| Daily record | Morning → daily activities → small happy moments → evening/ending |
