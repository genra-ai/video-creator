---
name: Historical Reenactment
description: "Describe a historical event to generate reenactment videos."
agent_description: "Use this skill when the user wants to recreate historical events or historical figures as dynamic video: split into shots along a timeline, narration paired with scene visuals, documentary-style composition. Suitable for history education, cultural science communication, and historical theme short video creation. Triggered by: 'historical reenactment', 'historical scene', 'historical documentary', 'make a video of a historical event', 'history explainer'."
---

# Historical Scene Reenactment Video

Turns historical events or historical figures into documentary-style dynamic videos. Core: timeline as the main narrative thread, narration drives the historical progression, each shot visually recreates the corresponding historical scene, style is serious and authentic.

## Key Principles

- **Historical accuracy first**: scene descriptions must match the costume, architecture, and prop style of the corresponding historical period
- **Narration is objective and plain**: documentary tone, stating facts, not overly dramatized
- **Visual not text-heavy**: use visuals to recreate historical scenes, not just relying on text explanations
- **Timeline must be clear**: each major time node marked with subtitle (year/dynasty/event name)
- **No tail frames; audio before video**

## Workflow

### 1. Confirm Historical Topic, Plan Timeline

**Required info**: historical event/person name + key time nodes (3–5).

If the user hasn't provided detailed information, do brief knowledge preparation before planning (can use WebSearch to confirm key time nodes and historical details), ensuring scene descriptions are historically accurate.

**Timeline planning principles**:
- Choose 3–5 key nodes with the strongest visual representation
- Each node corresponds to 1–2 shots
- Nodes have clear causal or chronological progression relationships

**Historical period visual reference**:

| Period / Region | Costume Reference | Architecture / Environment |
|---|---|---|
| Ancient China (Han/Tang) | Hanfu/Tang robes, wide sleeves | Palaces/courtyards/city walls, red walls and yellow tiles |
| Ancient China (Song/Ming/Qing) | Corresponding dynasty costumes | Gardens/academies/markets |
| Ancient Rome/Greece | Long robes (toga/chiton), metal armor | Stone columns/arenas/temples |
| Medieval Europe | Knight armor/long dresses, rough linen | Castles/cobblestone streets/churches |
| Modern era (Republican/WWII etc.) | Corresponding period clothing | Corresponding city/battlefield environments |

### 2. Plan Shot Structure

**Standard structure** (8–12 shots, 60–120 seconds):

| Segment | Shot Count | Content | Duration |
|---|---|---|---|
| Opening positioning | 1–2 | Establish historical period and geographical context | 4–6s |
| Time node 1 | 1–2 | Recreate first key event scene | 5–8s |
| Time node 2 | 1–2 | Recreate second key event scene | 5–8s |
| Time node 3 | 1–2 | Recreate third key event scene | 5–8s |
| (More nodes...) | ... | ... | ... |
| Historical significance closing | 1–2 | Show impact or result of the historical event | 4–6s |

> **Narration length limit**: When writing narration, plan it short from the start — **≤ 10 words per shot** (documentary pace ~120 wpm = 2 words/sec, so a 5s shot fits ~10 words). Write concise narration at the planning stage; do not write long and trim later.

### 3. Send Shot List

```
Art style: realistic documentary style, slightly historical texture (can add light film grain), stable tones

[Global constraints]
- All shots match the visual style of [historical period]
- Costumes/architecture/props historically accurate
- Narration tone: objective statement, documentary style

Shot 1 (Xs): [opening scene establishing historical period], subtitle: "[dynasty/era/location]", narration: "[historical background introduction]"
Shot 2 (Xs): [first time node scene recreation], subtitle: "[year/event name]", narration: "[corresponding historical description]"
...
Shot N (Xs): [historical impact/closing scene], narration: "[historical significance summary]"
```

### 4. Filter Check

- Do costumes and architecture match the corresponding historical period
- Is narration objective and plain, without excessive emotionalization
- Do time node subtitles appear at key shots

### 5. Clear All Tail Frames

### 6. Generate Audio

**Narration voice**: mature, steady, weighty, moderate pace, like a documentary narrator.

**BGM**:
- Matches historical period atmosphere
- Volume lower than narration, serves as backdrop
- Chinese historical themes: traditional instruments as main
- Western historical themes: orchestral as main

### 7. Generate Videos & Export

---

## Resolution

| Use Case | Resolution |
|---|---|
| YouTube / horizontal | 1280×720 (16:9) |
| Douyin / TikTok | 720×1280 (9:16) |
