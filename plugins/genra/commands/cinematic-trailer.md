---
name: Cinematic Trailer
description: "Describe a core concept to generate high-impact trailers."
agent_description: "Use this skill when the user wants to create a cinematic trailer-style promotional short: suspense build → conflict escalation → climax → open ending. Emphasizes fast-slow editing rhythm and dramatic composition. Suitable for drama promotion, brand films, event teasers, and personal project promotion. Triggered by: 'trailer', 'cinematic video', 'blockbuster style', 'trailer', 'promo film'."
---

# Cinematic Trailer

Turns a core conflict or story into a trailer-style promotional short. Core: use fast-slow editing rhythm within 30–60 seconds to build suspense, escalate emotion, cut to black at the climax — making viewers desperate to see the full version.

## Key Principles

- **Fast-slow mixed cuts are the soul**: slow opening to establish the world, fast cuts in the middle to build tension, sudden slow-motion or freeze at the climax
- **Don't explain, just show**: trailers don't tell the full story — only show the most exciting moments, leaving questions unanswered
- **Every shot must have dramatic tension**: composition, lighting, and expression must have emotional peak points
- **Subtitles are a rhythm tool**: key text appears at the breathing moments between fast cuts — not on every shot
- **Sound effects and music are the emotional engine**: BGM rhythm strictly synced with editing rhythm
- **No tail frames; audio before video**

## Workflow

### 1. Extract Core Conflict, Plan Shot List

**Required info**: core conflict of the story/project (1 sentence) + main characters (1–2) + genre (action/romance/mystery/fantasy etc.).

**Shot structure** (8–12 shots, 30–60 seconds):

| Segment | Shot Count | Rhythm | Purpose |
|---|---|---|---|
| Opening establishment | 2–3 | Slow (3–4s) | Establish world and characters, calm feel |
| Conflict escalation | 3–4 | Gradually faster (2s→1s→0.5s) | Build tension, hint at danger |
| Climax burst | 2–3 | Extreme fast cuts (0.5s) then sudden slow-mo | Emotional peak, maximum drama |
| Open ending | 1–2 | Slow / still (2–3s) | Question mark ending, create suspense |

**Subtitle keyframes** (choose 3–5 key words):
- Appear at "breathing frames" within fast-cut sections
- Each subtitle paired with a sound impact effect
- The last subtitle is usually the project name or a suspense question

### 2. Send Shot List

```
Art style: [cinematic / realistic / fantasy / noir, matching story genre]
Color tone: [cold blue / warm orange / high-contrast black & white etc.]
BGM direction: [tense orchestral / electronic / epic orchestral etc.]

[Global constraints]
- All shots maintain cinematic composition (letterbox black bars 2.35:1 or 2.39:1 ratio)
- Character shots: emotions at the extreme, not performative — use environment/action/detail to convey emotion
- High-contrast lighting, emphasize silhouette

Shot 1 (slow, Xs): [world-building scene description], subtitle: none
Shot 2 (slow, Xs): [character state], subtitle: none
Shot 3 (accelerating, Xs): [conflict signal], subtitle: "[keyword]"
...
Shot N (open ending, Xs): [freeze / fade / suspense image], subtitle: "[project name or question]"
```

### 3. Filter Check

- Is the fast-slow rhythm planning reflected in duration settings
- Do climax shots have clear dramatic tension
- Do subtitles appear outside densely cut sections (avoid one subtitle per frame)

### 4. Clear All Tail Frames

### 5. Generate Audio

**BGM formula**: `[instrument texture] + [emotional arc] + [beat point synced with editing rhythm]`

| Story Genre | BGM Example |
|---|---|
| Action / adventure | Orchestral + electronic mix, BPM accelerates with edits, drums hit on fast-cut beats |
| Mystery / thriller | Low-frequency strings, irregular rhythm, sudden silence + impact sound effects |
| Romance / drama | Piano main melody, strings underneath, full swell at emotional peak |
| Fantasy / epic | Epic orchestral, grand scale, optional vocal chorus |

No dialog or minimal dialog (subtitles only); if character voiceover is used, choose the single most powerful line.

### 6. Generate Videos & Export

---

## Resolution

Default **16:9 horizontal** (cinematic format), with letterbox bars for widescreen ratio: 1280×720
