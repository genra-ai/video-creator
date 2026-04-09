---
name: product-showcase
description: "Use this skill when the user wants to create an e-commerce product showcase video: each shot highlights one selling point with voiceover, suitable for Taobao/JD/Shopify main image videos. Triggered by: 'product video', 'showcase'."
---

# Product feature showcase

Converts product images and selling points into an e-commerce showcase video. Core focus: feature demonstration and selling-point visualization — not brand atmosphere. Reference: Apple product page videos, Shopify/JD product main-image videos.

## Key Principles

- **Each shot serves one selling point** — list selling points first, then assign one shot per point
- **Product must be clearly visible in every shot** — specify its proportion and clarity in every description
- **Voiceover is the information backbone** — not atmosphere; each selling-point shot must have a matching line
- **Voiceover line must fit shot duration** — ~15 chars per 3s shot, ~25 chars per 5s shot; extend if it exceeds
- **Feature demo shots: be specific** — write exact state (water level, battery %, fold angle) so AI generates informative visuals
- **Opening hero shot needs 2–4s** — enough time for the product's first impression to land
- **CTA closing must be explicit** — full product view + core selling points or price/action info
- **Audio before video**; **no tail frames**

## Workflow

### 1. Analyze Product + Output Storyboard

**Only the product image is mandatory.** For missing info, use WebSearch first, then infer from image/category. If truly unknown, ask the user once — all questions at once.

**Before storyboarding**, run 1–2 WebSearch queries to find structural references for similar products:

| Category | Search Terms |
|----------|-------------|
| Electronics/3C | `"[category]" product demo video structure shot list ecommerce` |
| Beauty/Skincare | `"[category]" product showcase video skincare ecommerce structure` |
| Apparel/Accessories | `"[category]" fashion product video shot list ecommerce` |
| Home/Kitchen | `"[category]" product feature demo video structure homepage` |
| Food/Health | `"[category]" product video ecommerce food showcase structure` |

Extract: industry-standard selling-point order, which features are commonly visualized, common usage scenario templates. Do not show this search process to the user.

**Core value proposition** (1 sentence, determines the entire video's focus):
- Functional → before/after comparison, feature demo
- Quality → detail close-ups, texture comparison
- Scenario → usage scenes, emotional connection
- Efficiency → speed, ease-of-use demo

**Selling point order** (conversion logic): strongest pain-point solver first → 3–4 supporting points → brand/quality endorsement → CTA closing.

**Product's role per shot** — must be explicit for every shot:

| Role | Description |
|------|-------------|
| Product close-up | Showcase appearance, material, details |
| Product in use | Hand-held / worn / operated — real usage state |
| Feature demo | Exaggerate one feature (waterproof submersion, charging speed, etc.) |
| Scene integration | Product naturally present in environment, not the emphasis |
| Effect comparison | Before vs. after, or side-by-side with ordinary product |

**Storyboard structure** (8–12 shots, 30–60s total):

| Section | Shots | Purpose | Duration |
|---------|-------|---------|----------|
| Opening hero | 1–2 | Best product angle, first impression | 2–4s |
| Selling point showcase | 4–8 | One shot per selling point | 3–5s each |
| Usage scenarios | 2–3 | Real usage, emotional resonance | 3–4s each |
| CTA closing | 1–2 | Full product view + brand/price/action | 2–4s |

**Shot types** (adapt freely to product):

| Shot Type | Use For |
|-----------|---------|
| Product hero shot | Opening — clean background, product fills frame |
| Material detail close-up | Fabric, surface craftsmanship, seam/button |
| Feature demo | Waterproofing, charging, folding, one-touch operation |
| Hand operation | Grip/touch posture, single-hand comfort |
| Usage scenario | Person in real setting (café / gym / kitchen) |
| Effect comparison | Before/after, or vs. ordinary product |
| CTA closing | Front-facing freeze, brand/price/slogan |

**Self-review before showing to user** — fix issues directly, then show:

| Check | Pass Criteria |
|-------|--------------|
| Feature clarity | Each shot communicates one specific selling point, not just "feels nice" |
| Product visibility | Not obscured, too small, or too dark in any shot |
| Selling point coverage | Each of the 3–5 core selling points has a corresponding shot |
| Voiceover feasibility | Each selling-point shot has a line that fits within its duration |
| CTA completeness | Last 1–2 shots include full product view + action prompt |

Show the storyboard to the user, then proceed to Step 2 immediately — no need to wait for confirmation.

### 2. Upload Images & Send Script

Upload all provided product images (each separately) and record each asset_id. Multi-angle images give the pipeline better product-appearance consistency across shots.

Send one message with: global style + voiceover/BGM description + product reference image asset_ids in the description field + all shots.

**Shot description principle — write function, not atmosphere:**
- State the product's angle, background, lighting, and what feature is visible
- For usage shots: describe the grip/posture/operation detail, not the emotional vibe
- For feature demos: be precise about the exact state — the more specific, the more informative the generated visual:

| Feature Demo | Example Description |
|---|---|
| Waterproofing | Product fully submerged in clear water tank, water surface clearly visible, product screen still lit underwater, filmed from 45° front-side angle, water ripple reflections, no bubbles obscuring key areas |
| Fast charging | Product lying flat on desk, charging cable inserted, screen showing battery percentage (sense of change from 15% to 45%), 45° top-down angle, pure white desk surface, even lighting |
| Folding/unfolding | Product mid-fold at 90°, hinge mechanism clearly visible, hand holding one panel, shot from side angle showing the fold angle, clean background |

**Product states in frame:**

| State | Description Focus |
|-------|-----------------|
| Standalone display | Pure background (white/light gray), product fills 70–80% of frame, front/side/top-down angle |
| Hand-held operation | Grip/touch posture details, product facing camera, background blurred |
| Scene integration | Real environment, product at golden-ratio point, usage state clearly identifiable |

Each shot must be a single point-in-time cinematic composition — no dividing lines or multi-angle juxtaposition. Each shot needs only a start frame; no tail frames.

### 3. Filter Check

Check shots, dialogs, and characters. Showcase-specific points:
- Every selling-point shot has a matching voiceover line
- Product shots are at least 3s — enough for the line to be spoken
- If scene characters appear: identity description consistent across all shots

### 4. Clear All Tail Frames

Send a message asking the pipeline to clear all tail frames, keep only start frames. Verify afterward.

### 5. Generate Audio

**Voiceover formula**: `[gender + warmth] + [pace] + [tone style]`

| Product Type | Voiceover Example |
|---|---|
| Mass consumer goods | Young female, moderate pace, warm and natural, like recommending to a friend |
| Electronics/3C | Young male, clear and strong, slightly faster, professional but not stiff |
| High-end / luxury | Female, slightly slower, understated and elegant, quality pauses |
| Mother & baby | Female, gentle and caring, slow pace, full of reassurance |

**BGM formula**: `[instrument texture] + [mood] + [background level — must not overpower voiceover]`

| Mood | BGM Example |
|------|------------|
| Tech / modern | Upbeat minimal electronic, BPM 120, no lyrics |
| Lifestyle quality | Warm guitar + light piano, BPM 90, background level |
| Sports / energy | Rhythmic electronic, BPM 130, does not overpower voiceover |
| High-end / premium | Minimal piano or strings, understated, background level |

### 6. Generate All Videos

After audio completes, generate all videos.

---

## Category Shot Structure Reference

| Category | Recommended Structure |
|----------|-----------------------|
| Electronics/3C | Hero → exterior details → feature demos (2–3) → usage scenario → specs → CTA |
| Beauty/Skincare | Product close-up → texture display (pour/apply) → usage steps → before/after → CTA |
| Apparel/Accessories | Flat lay → detail close-up (fabric/craftsmanship) → worn effect → styled scene → CTA |
| Home/Kitchen | Overall exterior → core feature demo → usage scenario → differentiating details → CTA |
| Food/Beverage | Product close-up → ingredients/contents → preparation/unboxing → consumption scene → CTA |

## Resolution

Default: **9:16 vertical** (product main image format)

| Use Case | Resolution |
|----------|------------|
| Taobao / JD / TikTok product card | 720×1280 (9:16) |
| Independent store / YouTube | 1280×720 (16:9) |
| Xiaohongshu square | 720×720 (1:1) |
