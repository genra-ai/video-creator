---
name: YouTube Intro
description: "Provide channel themes to create eye-catching intros."
agent_description: "Use this skill when the user wants to create a branded YouTube channel intro or outro: intro is 3–5 shots showcasing channel style and name, outro includes subscribe prompt and recommendation cards, total duration 5–15 seconds, style consistent with channel theme. Triggered by: 'YouTube intro', 'channel opening animation', 'outro subscribe prompt', 'channel intro/outro'."
---
# YouTube Channel Intro / Outro

Creates a branded opening animation (Intro) and subscribe-prompt ending (Outro) for a YouTube channel. Core: establish channel visual identity in minimal time, and clearly guide user actions at the end.

## Key Principles

- **Intro must not exceed 15 seconds**: viewers will skip anything longer
- **Channel name must appear**: at least one shot in the intro must clearly display the channel name
- **Style consistent with channel content**: tech channel = clean and modern; lifestyle = warm and lively; gaming = dynamic and flashy
- **Outro CTA must be explicit**: subscribe button area, recommended video area, and/or social media links — include at least one
- **No tail frames; audio before video**

## Workflow

### 1. Confirm Channel Information

**Required info**: channel name + channel topic/type + visual style preference (can be inferred from channel type).

**Style reference**:

| Channel Type | Recommended Visual Style | Color Reference |
|---|---|---|
| Tech / digital | Clean and modern, geometric shapes, cool tones | Dark blue/black + white/cyan |
| Beauty / lifestyle | Warm and soft, flowing light effects | Warm pink / off-white / gold |
| Gaming / entertainment | Dynamic and flashy, fast-paced, neon feel | Dark background + saturated bright colors |
| Education / knowledge | Clean and professional, infographic feel | White / light grey + brand color |
| Food / travel | Bright and vivid, natural feel | Warm tones + high saturation |
| Fitness / sports | Powerful, dynamic | Dark + red/orange |

### 2. Plan Shot Structure

**Intro structure** (3–5 shots, 5–12 seconds):

| Shot | Content | Duration |
|---|---|---|
| 1 | Brand animation / logo reveal or visual impact opening | 2–3s |
| 2–3 | Channel content preview / style showcase | 2–3s each |
| 4–5 | Channel name in large text + tagline (optional) | 2–3s |

**Outro structure** (3–4 shots, 8–15 seconds):

| Shot | Content | Duration |
|---|---|---|
| 1 | Thank-you closing screen | 2–3s |
| 2 | Subscribe prompt screen (subscribe button area, with channel name) | 3–4s |
| 3 | Recommended video card area (leave blank space on sides for YouTube cards) | 3–4s |
| 4 (optional) | Social media accounts display | 2s |

### 3. Send Shot List

```
Art style: [corresponding style description: clean / warm / dynamic etc.]
Brand color: [primary color]
Channel name: [channel name]

[Global constraints]
- Unified style, consistent with channel tone
- Channel name clearly shown in the last shot of the intro
- Outro leaves space for YouTube cards (approx. 20% blank on left and right sides)

Intro Shot 1: ..., duration Xs
...
Outro Shot 1: ..., duration Xs
...
```

### 4. Clear All Tail Frames

### 5. Generate Audio

**Intro BGM**: matches channel style, has rhythm, ends with a clear resolution within 5–12 seconds.
**Outro BGM**: mellower version, gradually fades out, does not steal the spotlight.

### 6. Generate Videos

---

## Resolution

Default **16:9 horizontal** (YouTube standard format): 1280×720
