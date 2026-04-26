---
name: Faceless Video
description: "Provide educational content to create faceless narration videos."
agent_description: "Use this skill when the user wants to create a fully faceless video with voiceover narration and B-roll footage only: each line of narration matches one scene shot, no real person on screen. Suitable for educational, review, storytelling, and knowledge-sharing content. Triggered by: 'faceless video', 'no face video', 'voiceover with footage', 'narration only'."
---

# Faceless Narration Video

Turns a voiceover script into a fully faceless B-roll narration video. Core: each line of narration precisely matches one scene shot — visuals serve the narration content, not decoration.

## Key Principles

- **Visuals serve the narration, not decorate it**: each shot's content must be directly related to the corresponding narration
- **No people on screen at all**: all shots are scenes, objects, environments, close-ups — no full human faces or bodies
- **Narration pace determines shot duration**: shot duration = corresponding narration length + 0.5s buffer
- **No tail frames; audio before video**

## Workflow

### 1. Organize Narration, Plan Shot List

**If user provides a script**: split directly by sentence/paragraph into shots, one visual description per sentence.

**If user only provides a topic**: first generate the narration script (conversational, concise), then split into shots.

**Shot planning principles**:

| Narration Type | Corresponding Visual |
|---|---|
| Introducing a concept/thing | Close-up or scene shot of that thing |
| Describing a process/steps | Mid or close shot of the action process |
| Expressing emotion/atmosphere | Abstract natural scenery, light and shadow, space |
| Data/facts | Visual representation of related scene or object |
| Storytelling | Scene recreation, environment establishing |

**Duration reference**: 3–5s per shot, 30–90s total is ideal.

### 2. Send Shot List

One message with all content:

```
Art style: [realistic / animated / cinematic / documentary, choose based on content type]

[Global constraints]
- No people on screen (no faces, no full bodies)
- All shots are scenes / objects / environments / close-ups
- Visuals directly correspond to narration content

Shot 1 (Xs): [scene description], narration: "[corresponding narration text]", duration Xs
Shot 2 (Xs): [scene description], narration: "[corresponding narration text]", duration Xs
...
```

### 3. Filter Check

- Confirm all shots have no people on screen
- Each shot's narration text is correctly filled in
- Shot duration matches narration length

### 4. Clear All Tail Frames

### 5. Generate Audio

**Narration voice formula**: `[gender+age] + [voice texture] + [emotional tone] + [pace]`

| Content Type | Voice Example |
|---|---|
| Educational / knowledge | Mature male or female, clear and steady, objective and neutral, moderate pace |
| Storytelling | Warm male or female, slightly emotional, slightly slower, rhythmic |
| Fun content | Young voice, light and lively, slightly fast |
| Commercial / brand | Professional feel, confident, moderately fast |

**BGM**: chosen based on content atmosphere, volume lower than narration, serves as backdrop.

### 6. Generate Videos & Export

---

## Resolution

| Use Case | Resolution |
|---|---|
| Douyin / TikTok / Reels | 720×1280 (9:16) |
| YouTube / horizontal | 1280×720 (16:9) |
| Xiaohongshu | 720×720 (1:1) |
