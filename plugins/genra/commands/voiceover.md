# Voiceover

Generate a 20–30 second talking-head video: single character speaking directly to camera, fixed medium shot, seamless continuity between adjacent shots.

## Key Principles

- **Art style has top priority**: declare on the very first line of the project message. Default: `Art style: realistic live-action`
- **Send all shots + dialogs in one message** — adding dialog later is painful
- **Set tail frames, do NOT clear them**: each shot's tail frame = next shot's start frame. Opposite of script-to-video
- **Check image consistency before setting tail frames**: compare shot by shot from shot 2; fix immediately (I2I, max 1 retry per shot)
- **Audio before video**

## Workflow

### 1. Write Script

4–6 shots, 4–6s each. Colloquial tone. Output: script lines + character appearance + scene description + BGM direction.

**Character description**: `[age + gender] + [hairstyle: length/texture/color] + [skin tone] + [top: color/material/cut] + [one signature detail]`

Signature detail (glasses, earring, hair clip) acts as a cross-shot anchor. Be precise with colors: "pure white (like printer paper)", "deep navy (not black)".

**Scene description**: `[location] + [light source] + [light quality + color temp] + [key elements]`

| Context | Lighting |
|---------|---------|
| Skincare / beauty | Front soft light, warm (4000K), no strong shadows, light background |
| Tech / professional | Even front white light, neutral (5500K), dark background |
| Warm lifestyle | Warm side lamp, soft diffuse, orange-yellow (3000K) |
| Energetic / entertainment | Bright front light, saturated colors |

### 2. Create Project & Send Script

Send one message with all shots. Include these constraints in the message:

- All shots: same character, same scene, fixed medium shot
- Character centered, occupying ~70% of frame height, always facing camera
- Focal length, depth of field, and shooting distance identical across all shots — no push/pull effects
- Background environment completely identical across all shots — no element may appear or disappear

### 3. Filter Check

- All shots use the same `character_id` and `location_id`
- `identity_anchor` description must be word-for-word identical across all shots — fix with `edit` if not
- Each shot has one dialog entry; verify content and character attribution

### 4. Check Image Consistency

Use shot 1 as baseline. From shot 2 onward, compare each shot against the previous:

- Depth of field / background blur level consistent
- Character size and vertical position consistent
- No push/pull feel between shots
- Character appearance (hair, clothing, signature detail) consistent

Fix immediately with I2I when inconsistent. Retry at most once; if still off, accept and move on.

**Common voiceover AI issues:**

| Issue | Fix |
|-------|-----|
| Glazed / glassy eyes | I2I: "sharp eyes with focus, glossy look" |
| Face drift | I2I using previous shot as reference: "keep face shape consistent with reference" |
| Depth-of-field mismatch | Root cause of push/pull feel; must resolve before step 5 |

### 5. Set Tail Frames

Each shot's tail frame = next shot's start frame asset_id. Last shot: no tail frame needed.

**Procedure**:
1. `get_state` → record every shot's `start_frame` asset_id
2. For shots 1 through N-1: send one message per shot to set its tail frame, then `get_state` to verify the `tail_frame` field is correct — retry up to 3 times if not set. Only move to the next shot after confirming.

### 6. Generate Audio

**Voice description**: `[gender + age] + [voice texture] + [emotional tone] + [pace]`

Default pace: **relatively fast**. Slower only for emotional/literary styles.

| Type | Example |
|------|---------|
| Skincare / beauty | Young female, clear and soft, warm, fast pace |
| Tech / professional | Mature male, deep and powerful, confident, moderately fast |
| Energetic promo | Young voice, bright and lively, infectious, fast |
| Literary / artistic | Young female, gentle, slightly slower, natural pauses |

Voice cloning: upload 5–10s reference audio; use the returned asset_id as the character's voice field.

### 7. Generate Videos

After audio completes, generate all videos.

### 8. Preview & Export

Check each shot transition — image should be continuous with no jump cuts. If a transition is broken, reset that shot's tail frame and regenerate only that shot's video.
