---
name: product-animation
description: "Use this skill when the user wants to create a product 3D animation or pure motion showcase video — no presenter, no narration, pure product visuals: rotation, reveal, assembly/disassembly, or environment interaction. Triggered by: 'product rotation', '360 product view', 'product animation', '3D product video', 'assembly animation', 'product reveal', 'explode view', 'product spin', 'rotating product video', 'product 3D showcase', 'product disassembly animation', 'product environment animation', 'furniture open animation', 'architectural dimension video', 'device animation'."
---

# Product Animation

Creates pure product animation videos: no presenter, no narration — the product itself is the star. Covers 360° rotation, dramatic reveals, assembly/explode views, and environment interaction. Used for websites, presentations, e-commerce hero videos, trade show loops, and social media product drops.

## Key Principles

- **Product accuracy above all**: color, material, finish, proportion, and logo must be consistent across every shot — define once and lock it
- **Motion tells the story**: without a presenter or narration, camera movement and product motion carry the full visual narrative — every shot must have purposeful motion
- **Light reveals material**: the single biggest quality factor is how light interacts with the product surface — always specify light direction and how it reads on the material
- **Clean backgrounds amplify product**: avoid busy environments; the product needs visual breathing room
- **No tail frames; BGM before video**

## Workflow

### 1. Analyze Product and Showcase Goal

After the user describes or uploads a product image, identify:

- **Product category**: consumer electronics / vehicle / furniture / apparel / packaging / book / industrial equipment / architectural model / digital product / other
- **Showcase objective**: full-form overview / surface detail / internal structure / assembly process / function state change (e.g., door opening, screen lighting)
- **Reference image available?**: if yes, it becomes the start frame anchor for the first shot

### 2. Select Animation Mode

Choose one primary mode (or combine 2 for longer videos):

| Mode | Description | Best For |
|---|---|---|
| **Rotation** | Product rotates 360° in place on a clean surface or floating in space; camera may slowly orbit or stay fixed | Showing full exterior — vehicles, bottles, electronics, books |
| **Reveal** | Product emerges from darkness, packaging, or a dramatic camera push; slow cinematic approach from multiple angles | Launch videos, hero shots, premium product drops |
| **Assembly / Explode** | Components separate outward (explode view) then reassemble, or parts fly in and click into place (assembly) | Showing internal structure, craftsmanship, engineering |
| **Environment** | Product sits in a minimal scene and performs a state change: drawer opens, lid lifts, screen activates, door swings | Furniture, appliances, smart devices, architectural models |

### 3. Background and Lighting Design

Lighting is the most impactful quality lever — describe precisely.

**Background options**:

| Background | Use When |
|---|---|
| Pure color / gradient (white, black, charcoal, off-white) | Rotation and Reveal — keeps focus on product |
| Minimal surface (marble slab, matte concrete, dark wood plank) | Environment mode — adds context without clutter |
| Infinite white void | Tech products, clean industrial feel |
| Deep space / dark gradient with rim light | Premium and luxury reveals |

**Light direction and material pairing**:

| Material | Recommended Light | Effect |
|---|---|---|
| Brushed metal / aluminum | Single hard side light | Reveals directional texture lines and edge sharpness |
| Glossy plastic / coated surface | Soft box from above + rim light | Clean highlight stripe, avoids hotspot overexposure |
| Glass / transparent | Backlight + subtle edge fill | Glow-through depth, visible refraction |
| Matte rubber / fabric | Diffuse top light | Even texture detail, no distracting reflections |
| Wood / leather | Warm side light at 30–45° | Grain shadow depth, surface warmth |
| Painted automotive | Three-point studio | Paint depth, body line highlights |

### 4. Shot Structure

Typical 2–4 shot structure (4–8 seconds per shot):

| Shot | Content | Motion |
|---|---|---|
| 1 — Full form | Complete product from a flattering angle | Slow rotation or push-in |
| 2 — Detail close-up | Highlight a key material, logo, or mechanical detail | Slow macro orbit or pull-focus |
| 3 — Function / Structure | Assembly sequence, door open, screen light-up, explode view | Component-driven motion |
| 4 — Closing wide | Return to full product, light shift or final rotation stop | Gentle rotation deceleration or freeze |

Shorter videos (website loops, social): 2 shots only — Shot 1 + Shot 4.

### 5. Reference Image Handling

If the user provides a product image:
- Use it as the **start frame** (`$asset_id`) for Shot 1
- Product appearance in Shot 1 description must exactly match the uploaded image state
- Subsequent shots maintain the same product description locked from the reference

### 6. Product Description Rules

Every shot that shows the product must include:

- **Color**: specific finish, not generic ("matte olive green", not "green"; "pearl white with warm undertone", not "white")
- **Material**: surface treatment and texture ("brushed anodized aluminum", "soft-touch matte polymer", "tempered glass with anti-reflective coating")
- **Key details**: logo placement and style ("embossed silver wordmark centered on front face"), functional elements, proportions
- **Scale cue** (when needed): relative size reference to ground plane or environment object

Never write "the product rotates" without describing the product itself.

### 7. Script Format

```
Animation mode: [Rotation / Reveal / Assembly+Explode / Environment]
Background: [exact background description]
Light setup: [light direction, quality, and material intent]
BGM: [style and BPM, or "none"]
Resolution: [1280×720 / 720×1280]

[Product identity lock — define once, reuse in every shot]
Product: [full color + material + key detail description]

Shot 1 (Xs): [camera angle], [product state], [motion description], [light behavior on surface]
Shot 2 (Xs): [camera angle], [product state], [motion description], [light behavior on surface]
...
```

### 8. Filter Check

- Every shot description contains: product identity + camera motion + surface light behavior
- Background and lighting are consistent or intentionally varied with a stated reason
- Total duration: 12–32 seconds for loops; up to 60 seconds for full showcase
- No tail frames
- If reference image was provided, Shot 1 uses it as start frame

### 9. Clear All Tail Frames

### 10. BGM Selection (optional — no voiceover needed)

| Product Type | BGM Style |
|---|---|
| Tech / digital / smartphone | Low-frequency electronic, BPM 90–110, minimal and cold |
| Consumer goods / home / furniture | Soft piano or acoustic guitar, warm and natural |
| Luxury / premium / jewelry | Very slow strings, restrained and elevated |
| Industrial / architectural | No BGM, or pure ambient environment sound |

### 11. Generate Videos

No voiceover. BGM only if specified. Generate all shots, then export.

---

## Resolution

| Use Case | Resolution |
|---|---|
| Website / horizontal presentation | 1280×720 (16:9) — default |
| Vertical product (smartphone, bottle, etc.) | 720×1280 (9:16) |
| Square social loop | 720×720 (1:1) |
