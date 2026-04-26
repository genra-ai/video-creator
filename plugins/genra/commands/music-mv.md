---
name: Music MV
description: "Provide lyrics to generate a music video with synced subtitles."
agent_description: "Use this skill when the user wants to turn an LRC lyrics file (with timestamps) into a music video: parse timestamps → group into shots → match lyric imagery to visuals → sync subtitles to timing. Triggered by: 'music video', 'MV', 'lyrics video', 'make a video for this song', 'LRC to video', 'turn my lyrics into a video'."
---
# Music MV — LRC to Video

Turns an LRC-format lyrics file into a music video. Core: parse timestamps → group lyrics into shots → generate shot visuals that match lyric mood and imagery → sync lyric text as subtitles.

## Key Principles

- **LRC is the master timeline**: every shot boundary is derived from LRC timestamps, never invented
- **Lyric imagery drives visuals**: each shot description must reflect the emotional content and concrete imagery in the corresponding lyrics
- **Subtitles are mandatory**: lyric text appears as subtitle overlay on its corresponding shot, timed to the LRC timestamp
- **No tail frames**: MV style favors cut-editing; tail frames create unnatural morphing between unrelated shots
- **Audio before video**

---

## Workflow

### 1. Parse LRC Input

Accept LRC-format input from the user:

```
[mm:ss.xx] lyric line
[mm:ss.xx] lyric line
...
```

**Parsing steps**:
1. Extract all `[timestamp] lyric` pairs
2. Calculate each line's duration = next timestamp − current timestamp
3. Group consecutive lines into shots of **4–6 seconds each**
4. If a single line is longer than 6 seconds, treat it as its own shot
5. Record: shot number / start time / end time / lyric text block

**Output a parsed shot table before proceeding**:

| Shot | Start | End | Duration | Lyrics |
|------|-------|-----|----------|--------|
| 1 | 00:00.00 | 00:05.20 | 5.2s | "line 1 / line 2" |
| 2 | 00:05.20 | 00:10.80 | 5.6s | "line 3 / line 4" |
| ... | | | | |

**Ask for confirmation** before proceeding to shot planning if total shots > 10 or total duration > 60 seconds.

---

### 2. Detect Mood & Visual Style

Analyze the full lyrics to determine:

| Dimension | Examples |
|-----------|---------|
| **Genre feel** | Indie pop / dark rock / dreamy ballad / upbeat dance / cinematic epic |
| **Emotional arc** | Rising euphoria / quiet longing / raw anger / bittersweet nostalgia |
| **Key imagery** | Concrete nouns/verbs in lyrics (city lights, fire, running, ocean, falling) |
| **Color palette** | Warm gold / cold blue-grey / neon / desaturated |

Output a one-line visual style summary, e.g.:
> *Style: cinematic indie — cool blue-grey tones, urban night exteriors, slow push-ins, lens flare, film grain*

---

### 3. Plan Shot Descriptions

For each shot, write a visual description that:
- Reflects the **emotion and imagery** of the lyric text in that shot
- Is **concrete and specific** (not abstract) — name the subject, location, lighting, camera move
- Avoids literal illustration of every word — prioritize **emotional resonance**

**Shot description template**:
```
Shot N (Xs): [subject + action], [location + time of day], [lighting quality], [camera movement], subtitle: "[lyric text for this shot]"
```

**Imagery mapping guide**:

| Lyric theme | Visual direction |
|-------------|-----------------|
| Isolation / loneliness | Empty streets, single figure at distance, fog, night |
| Love / longing | Warm interiors, soft bokeh, reaching hands, window light |
| Freedom / escape | Open landscapes, running, wide skies, sunrise |
| Anger / intensity | Close-up faces, hard shadows, rapid movement, fire |
| Nostalgia | Overexposed or faded tones, domestic spaces, stillness |
| Euphoria / celebration | Bright light, motion blur, crowd energy, confetti |

---

### 4. Send Shot List

```
Art style: [one-line style summary from Step 2]

[Global constraints]
- Consistent character appearance across all shots featuring the same subject
- Subtitle text must match the lyric line exactly — no paraphrasing
- Color grade consistent with established palette throughout

Shot 1 (Xs): [description], subtitle: "[lyrics]"
Shot 2 (Xs): [description], subtitle: "[lyrics]"
...
Shot N (Xs): [description], subtitle: "[lyrics]"
```

---

### 5. Filter Check

- Shot durations match LRC-derived durations (±0.5s tolerance)
- Each shot has a subtitle field with the correct lyric line
- No tail frames set
- Art style consistent across all shots

---

### 6. Clear All Tail Frames

MV editing style does not use morphing transitions. Confirm all tail frames are cleared.

---

### 7. Generate Audio

**Option A — User provides audio file**:
Upload the audio file; use the returned asset_id as the project's audio source. Skip BGM generation.

**Option B — No audio provided**:
Generate instrumental BGM matching the detected genre/mood. Voice narration is NOT used for MV — lyrics appear as subtitles only.

BGM direction by genre:

| Genre | BGM Description |
|-------|----------------|
| Indie pop | Acoustic guitar + light percussion, warm mix |
| Dark rock | Distorted guitar, heavy drums, low-end emphasis |
| Dreamy ballad | Piano + strings, reverb-heavy, slow tempo |
| Upbeat dance | Synth-driven, 4/4 beat, energetic |
| Cinematic epic | Orchestral swell, brass + strings, building dynamics |

---

### 8. Generate Videos & Export

After audio is confirmed, generate all shots. Standard export resolutions:

| Use Case | Resolution |
|----------|-----------|
| YouTube / horizontal | 1280×720 (16:9) |
| Instagram Reels / TikTok | 720×1280 (9:16) |
| Square (Instagram feed) | 1080×1080 (1:1) |

---

## LRC Format Reference

```
[00:00.00] Line one of the lyrics
[00:03.50] Line two of the lyrics
[00:07.20] Line three
[00:10.80] Line four — this is a longer line that may form its own shot
[00:16.00] Chorus begins here
```

Blank lines and metadata tags (`[ti:]`, `[ar:]`, `[al:]`) are ignored during parsing.
