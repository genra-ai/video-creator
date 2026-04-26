---
name: UGC Ads
description: "Provide product features to create authentic seeding ads."
agent_description: "Use this skill when the user wants to create a UGC-style product seeding ad that mimics authentic user-generated content: handheld camera feel, real-user tone, hook opening to grab attention. Structure: hook → pain point → product reveal → result → CTA. Best for TikTok/Reels/Douyin. Triggered by: 'UGC ad', 'product seeding video', 'user perspective ad', 'make it look real'."
---

# UGC Product Seeding Ad

Turns a product's selling points into an authentic-sounding user-generated seeding ad. Core: real-life feel, handheld camera aesthetic, hook in the first 3 seconds. Reference: Xiaohongshu unboxing, Douyin product recommendations, TikTok authentic review style.

## Key Principles

- **First 3 seconds must be the hook**: open with a question, contrast, or bold conclusion — no brand intro
- **Sound like a real user, not the brand**: say "after I used it" not "this product features"
- **Handheld camera feel**: slightly tilted/shaky framing, not perfectly centered commercial shoot
- **Product must appear early**: product must be visible within the 2nd shot after the hook
- **No tail frames; audio before video**

## Workflow

### 1. Analyze Product, Output Script Structure

**Required info**: product name + core selling points (1–3) + target user pain points. Infer from product category if not provided — do not keep asking.

**Shot structure** (6–8 shots, 30–45 seconds):

| Shot | Type | Content | Duration |
|---|---|---|---|
| 1 | Hook | Strong question/contrast/conclusion, create curiosity | 3–5s |
| 2–3 | Pain point | Describe real user frustrations before using the product | 3–4s each |
| 4–5 | Product reveal + use | Product appears naturally, show usage process | 4–5s each |
| 6–7 | Result showcase | Change/comparison/outcome after use | 3–4s each |
| 8 | CTA | Recommendation and call to action, casual and natural tone | 2–3s |

**Hook type reference**:
- Question: "Do you know why I only bring this one thing when I go out?"
- Contrast: "I thought this was a waste of money — then I reordered immediately after"
- Conclusion-first: "This thing has genuinely changed my daily routine"

### 2. Send Shot List

Send one message with all shots. Global constraints go before the shot list:

```
Art style: realistic lifestyle feel, handheld shooting, natural lighting, not commercial studio style

[Global constraints]
- Character: [age+gender]+[appearance]+[clothing style: casual everyday]
- Scene: [real life setting: home / café / outdoor]
- Camera feel: slight handheld shake, not perfect rule-of-thirds, life-feels-real priority
- When product appears: handheld, not carefully posed

Shot 1: [hook content], duration Xs
Shot 2: ...
```

**Dialog writing style**: conversational, with pauses, like talking to a friend. Avoid: "This product uses XX technology". Use: "Honestly, after using it once I immediately wanted to buy another one."

### 3. Filter Check

- All shots share the same character description
- Product appears within the first 3 shots
- Dialog uses user voice, not brand voice

### 4. Clear All Tail Frames

Send a message to clear all tail frames, keep only start frames, then confirm before continuing.

### 5. Generate Audio

**Voice formula**: `[gender+age] + [voice texture] + [tone: casual, like talking to a friend] + [pace: slightly fast, energetic]`

| Product Type | Voice Example |
|---|---|
| Beauty / skincare | Young female, bright and natural, casual and warm, moderately fast |
| Tech / tools | Young male or female, crisp and clean, has a sense of surprise, fast |
| Food / snacks | Light and cheerful, slightly exaggerated, everyday feel, fast |
| Home / lifestyle | Warm and natural, like chatting at home, moderate pace |

**BGM**: upbeat background music, does not overpower the voice, BPM 100–120.

### 6. Generate Videos & Export

---

## Resolution

Default **9:16 vertical** (Douyin/Reels/TikTok)

| Use Case | Resolution |
|---|---|
| Douyin / TikTok / Reels | 720×1280 (9:16) |
| Xiaohongshu | 720×720 (1:1) |
