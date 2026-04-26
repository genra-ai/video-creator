---
name: AI Shorts Explainer
description: "Provide a topic to create bite-sized knowledge shorts."
agent_description: "Use this skill when the user wants to quickly generate a multi-shot knowledge short from a one-sentence topic: single input auto-expands into 5–20 independent knowledge point shots, one concept per shot, subtitle-driven. Suitable for educational, science communication, and skill-sharing fragmented short videos. Triggered by: 'generate video from one sentence', 'knowledge short', 'educational short video', 'AI shorts', 'quick explainer'."
---
# AI Knowledge Shorts

Auto-expands a single topic into a multi-shot knowledge short. Core: AI handles topic breakdown, shot planning, and narration writing — the user only needs to provide a one-sentence topic, no shot-by-shot design required.

## Key Principles

- **User only needs to provide the topic**: AI automatically completes content breakdown, shot planning, and narration writing
- **Each shot covers one knowledge point**: strictly one shot, one concept — no splitting or merging
- **Subtitles are the information carrier**: each shot's core keyword appears in large subtitle text
- **Total length control**: 5 shots ≈ 30s, 10 shots ≈ 60s, max 20 shots ≈ 120s
- **No tail frames; audio before video**

## Workflow

### 1. Receive Topic, Auto-Plan Shots

After the user provides a topic, AI completes the following steps (**no user confirmation needed — output the full shot list directly**):

**Step A: Break down topic into knowledge points**

Break the topic into 5–20 independent, parallel, progressive knowledge points. Principles:
- Each knowledge point can be summarized in one sentence
- Knowledge points have a logical order (simple to complex / parallel categories / chronological)
- No repetition; each point is independent

**Step B: Plan visuals for each knowledge point**

| Knowledge Point Type | Corresponding Visual |
|---|---|
| Definition / concept | Typical scene or metaphor scene for that concept |
| Data / facts | Corresponding visual scene (intuitive display of big/small/many/few) |
| Steps / methods | Action demonstration or operational scene |
| Comparison / difference | Contrasting scenes of two situations |
| History / time | Corresponding historical period or scene recreation |

**Step C: Write narration for each shot**

Each narration line: 15–30 words, conversational, clear and direct, directly related to the corresponding visual.

### 2. Send Shot List

```
Art style: [choose based on topic: tech feel / natural realistic / clean animation feel / documentary style]
BGM direction: light and knowledgeable, BPM 100–110, does not overpower narration

[Global constraints]
- All shots have unified style
- Each shot's subtitle keyword appears in large text (subtitle content = 3–5 core words for that knowledge point)
- No people on screen (pure scenes / objects / illustrative visuals)

Shot 1 (Xs): [visual description], narration: "[narration text]", subtitle: "[keyword]"
Shot 2 (Xs): [visual description], narration: "[narration text]", subtitle: "[keyword]"
...(N shots total)
```

### 3. Filter Check

- Are all shots' subtitle keywords filled in
- Is narration conversational and matched to the visuals
- Is there logical progression between adjacent knowledge points

### 4. Clear All Tail Frames

### 5. Generate Audio

Narration voice: clear, rhythmic, moderately fast pace (knowledge content is dense, shouldn't be too slow).

### 6. Generate Videos & Export

---

## Quick Mode (5-shot version)

For when the user just wants a brief introduction: directly generate the 5 most essential knowledge points, done in 30 seconds.

---

## Resolution

| Use Case | Resolution |
|---|---|
| Douyin / TikTok / Reels | 720×1280 (9:16) |
| YouTube | 1280×720 (16:9) |
