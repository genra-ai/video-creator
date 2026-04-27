---
name: Cast Script to Video
description: "Describe a script to generate multi-character drama videos."
agent_description: "Use this skill when the user wants to produce a multi-character drama video with guaranteed character consistency — first generates a front-facing reference image for each character to lock their appearance, then proceeds to full drama production using those reference images as I2I anchors throughout. Triggered by: 'cast then shoot', 'character reference first', 'drama with character refs'."
---

# Cast First, Then Shoot

Two-phase drama production workflow. Phase 1: before creating any story shots, generate one front-facing reference image for each character to lock their appearance. Phase 2: use those reference images as I2I anchors throughout the full drama production.

## Core Principles

- **Phase 1 must be completed and confirmed by the user before moving to Phase 2** — if a reference image does not match the character description, regenerate it
- **Art style has the highest priority**: must be written on the first line of the project message. Default: `Art style: realistic cinematic`
- **Do not rewrite the user's script** — only add visual information
- **Phase 1 generates images only — never generate video for reference shots**
- **Each character has exactly one shot (front-facing only), each shot has only a start frame, no tail frame**
- **Drama shots use start frames only** — after Phase 2 setup is complete, clear all tail frames
- **Review images grouped by character**, not in shot order
- **Ethnicity must match the source material** — read the character file carefully; "Western character" means Western/Caucasian appearance, not East Asian

---

## Phase 1: Character Reference Shots

### Step 1: Prepare the Shot List

If the user provides a character description file, **do not send it verbatim**. Extract only the appearance- and voice-related information for each character, simplify it, and send it to the platform. Keep: identity / ethnicity (vampire, elf, etc. — directly affects appearance), facial features, hairstyle and color, skin tone, body type, clothing, signature accessories, voice / demeanor. Remove: personality details, backstory, relationships, plot roles, and anything else not related to visual appearance.

After the simplified character descriptions, append a shot list specifying only:
- Shot number
- Character name

Example:
```
Shot 1: SELENE STERLING front reference, 1 second
Shot 2: WILLIAM DE VILLE front reference, 1 second
Shot 3: MINA MURDOCK front reference, 1 second
...(one shot per character, N shots total)
```

Do not add any extra appearance details, costume specifics, or lighting notes — the platform will extract those from the character descriptions above.

### Step 2: Create the Reference Project and Send Character Shots

Create a new project named `[original project name] — Cast`. Send a single message containing:
- Art style on the first line
- **One shot per character** — front-facing only (N characters = N shots)
- Each shot has a **start frame only, no tail frame**
- Shot duration: **1 second each**
- **No video description** — Phase 1 generates images only; never generate video for reference shots

Write the visual constraints as **global requirements** before the shot list — do not repeat them in each individual shot:

```
[Global constraint] All reference shot start frame descriptions: full-body portrait, facing forward,
looking directly into the camera, natural relaxed expression, arms resting naturally at sides.
Pure white background with no environmental elements or props,
even front lighting with no shadows, full body from head to toe fully in frame, subject centered.

Shot 1: [Character name] front reference, 1 second
Shot 2: [Character name] front reference, 1 second
Shot 3: [Character name] front reference, 1 second
...(one shot per character, N shots total)
```

> Do not add any appearance details (hair color, clothing, etc.) inside individual shot descriptions — the platform will extract those from the character file above.

### Step 3: Review Reference Shots

Once images are generated, download and inspect each character's front-facing reference frame:

| Check item | Requirement |
|---|---|
| Clothing color | Exactly matches the description — regenerate if off |
| Hairstyle | Length, texture, and color correct |
| Signature details | Visible and correct (glasses, jewelry, etc.) |
| Full body visible | Head to toe fully in frame |
| Background | Clean white, no props or scene elements |
| Orientation | Fully frontal, not turned or angled |

Keep regenerating (with more explicit descriptions) until every character's appearance is locked.

**No video may be generated for Phase 1 reference shots. Do not proceed to Phase 2 until all reference images are confirmed.**

---

## Phase 2: Drama Production

### Step 4: Send the Script in Segments

**Do not create a new project.** Continue in the same Cast project. **Do not write your own shot descriptions** — send the raw script segments directly and let the platform parse shots automatically.

**Segmentation rules**:
- Each message should cover approximately **10 shots' worth** of script content (roughly 10–12 lines of action / dialogue)
- Break at scene boundaries or natural paragraph breaks — **never split mid-scene**
- Include the full character reference block with the first segment; include a brief character appearance reminder with subsequent segments

**Language rules**:
- **Scene descriptions, actions, narration**: send in **Chinese**
- **Character dialogue lines**: preserve the original language of the dialogue (Chinese lines stay in Chinese, English lines stay in English)
- Translate any English scene descriptions / stage directions to Chinese before sending; do not translate dialogue

**Message structure per segment**:
```
Art style: [identical to Phase 1]

Character references for this episode (maintain the following character appearances consistent with their reference shots when generating images):
- [Character name] → reference Shot [N] start frame in this project
- [Character name] → reference Shot [M] start frame in this project
...(list only characters who appear in this segment)

---

[Script segment — scene descriptions / actions / narration in Chinese, dialogue lines unchanged in original language]
```

> **Why use the same project**: The character reference frames (shots 1–N) already exist in this project. Referencing them directly as I2I anchors is the most reliable way to lock appearance. Creating a new project loses this direct reference.

> **Audio and video generation**: Generate audio and video only for drama shots (shot N+1 onward). Reference shots (shots 1–N) have images only — never generate audio or video for them.

> **Sending pace**: After sending each segment, wait for the platform to finish parsing before sending the next segment to avoid shot order confusion.

> **Splitting dialogue shots**: When the script contains dialogue lines, add a note at the end of the sent script segment instructing the platform to split each dialogue line into its own individual shot — do not merge multiple lines into one shot.

### Step 5: Filter Review

Fix problems as soon as they are found.

- **Dialogue**: verify that each dialogue line is attributed to the correct character; narration must not be attributed to a specific character
- **Shots**: confirm that shot scale is parsed correctly; dialogue shot duration must be ≥ natural reading time + 0.5 seconds; reaction shots minimum 2–3 seconds

### Step 6: Clear All Tail Frames

Send a message instructing the platform to clear all tail frames from the drama project — keep start frames only. Confirm afterward. If auto-clear fails, manually uncheck tail frames in the generation panel.

### Step 7: Review Image Consistency Grouped by Character

Compare each character's drama frames against their **Phase 1 reference frame** one by one. The reference frame is the only standard.

| Issue | Common deviation | Fix |
|---|---|---|
| Clothing color | White → off-white, navy → black | Use reference frame as I2I; re-specify color |
| Hairstyle | Long hair shortens, bangs disappear | Use reference frame as I2I; re-emphasize |
| Signature details | Glasses / jewelry disappear | Use reference frame as I2I; explicitly emphasize |
| Age appearance | Character looks older / younger | Regenerate; add age anchor word |
| Glass eyes | Close-up / extreme close-up shots | I2I: "eyes clear and sharp, full of life" |
| Hand distortion | Holding / pointing shots | Regenerate; simplify hand description |
| Same dialogue direction | Shot-reverse-shot scenes | Explicitly specify facing direction for each character |

For consecutive shots in the same scene: also verify depth-of-field consistency. Maximum one retry per shot; accept and move on if still imperfect.

### Step 8: Generate Audio

**Voice description formula**: `[gender + age] + [timbre quality] + [emotional tone] + [pace]`

| Character type | Example |
|---|---|
| Young female lead (suppressed emotion) | Young female, bright timbre, restrained and suppressed, slow pace, strong sense of pauses |
| Middle-aged male (weary / guilty) | Mature male, low and slightly raspy, weary texture, slow pace, trailing ends |
| Young person (relaxed) | Young male, bright timbre, casual and natural, moderate pace |
| Dominant / villain | Mature male, deep and forceful, faster pace, firm enunciation |

Speaking pace follows scene emotion — **do not** default to "fast." Voice cloning: upload a 5–10 second reference audio clip; fill the returned asset_id into the voice field for that character.

### Step 9: Generate Video

Once all audio is complete, generate all drama videos.

### Step 10: Preview and Export

- Scene cuts: clean transitions, no blending artifacts
- Multi-character dialogue: lip sync matches the correct character
- Shot scale matches script intent (wide / medium / close-up)
- If tail frames still cause visual glitches: clear them again and regenerate only the affected shots

Export once all shots pass review.
