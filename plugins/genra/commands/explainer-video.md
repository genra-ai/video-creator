---
name: Explainer Video
description: "Provide a topic to create 60-second explainer videos."
agent_description: "Use this skill when the user wants to explain a concept, product, or process clearly through video: structure is problem → why it matters → step-by-step solution → summary. Works in animated or realistic style, narration-driven. Suitable for education, product feature walkthroughs, and brand concept communication. Triggered by: 'explainer video', 'explain what XX is', 'animated explanation', 'educational video', 'how-to video'."
---

# Explainer Video

Turns complex concepts, products, or processes into easy-to-understand explanatory videos. Core: use clear narrative structure + visual imagery to make "hard to understand" into "obvious at a glance."

## Key Principles

- **Answer "why watch this" first**: the first shot must make the viewer feel "this is relevant to me"
- **One shot, one point**: do not cram multiple pieces of information into the same shot
- **Visualize information**: every narration point must have a corresponding visual — not just background footage
- **Keep language simple and direct**: narration should be understandable to a middle schooler, avoid jargon
- **No tail frames; audio before video**

## Workflow

### 1. Analyze Topic, Output Explanation Structure

**Required info**: name of concept/product/process to explain + target audience (determines language difficulty and example choice).

**Standard structure** (6–8 shots, 60–90 seconds):

| Shot | Segment | Content | Duration |
|---|---|---|---|
| 1 | Pose the problem | Open with a pain point or question familiar to the audience | 5–8s |
| 2 | Why it matters | Explain consequences of not solving it, or benefits of solving it | 5–8s |
| 3–5 | Solution | Explain core content step by step / layer by layer, one key point per shot | 8–12s each |
| 6–7 | Additional details | Common misconceptions, applicable scenarios, caveats | 5–8s each |
| 8 | Summary + CTA | One-sentence summary + action prompt | 5–8s |

**Visualization reference**:

| Information Type | Corresponding Visual |
|---|---|
| Abstract concept | Metaphor scene (water flow to represent data flow) |
| Steps / process | Action demonstration or diagram-style visuals |
| Data / comparison | Charts, magnified comparison of objects |
| Persona explanation | Person in corresponding role/scene |
| Product feature | Feature operation close-up |

### 2. Send Shot List

```
Art style: [choose based on content: realistic / clean animation / tech feel / warm lifestyle feel]
BGM direction: light and knowledgeable, does not overpower narration, BPM 90–110

[Global constraints]
- All shot visuals directly correspond to narration
- Subtitles: key words from each shot appear in large text (optional)

Shot 1 (Xs): [visual description], narration: "[narration text]"
Shot 2 (Xs): [visual description], narration: "[narration text]"
...
```

### 3. Filter Check

- Does each shot's visual truly visualize the corresponding narration information
- Is the structure complete (problem → cause → solution → summary)
- Is the total duration within 90 seconds

### 4. Clear All Tail Frames

### 5. Generate Audio

**Narration voice**: clear, friendly, rhythmic. Moderate pace — not too fast (sounds like reading a script) and not too slow (sounds hypnotic).

| Audience | Voice Style |
|---|---|
| General / consumer | Light and friendly, like a friend explaining, moderate pace |
| Professionals | Professional and clear, weighty, slightly fast |
| Children / students | Lively and bright, slightly slower, obvious pauses |
| Business / B2B | Calm and confident, professional feel, moderate pace |

### 6. Generate Videos & Export

---

## Resolution

| Use Case | Resolution |
|---|---|
| YouTube / horizontal | 1280×720 (16:9) |
| Douyin / TikTok | 720×1280 (9:16) |
| Xiaohongshu / square | 720×720 (1:1) |
