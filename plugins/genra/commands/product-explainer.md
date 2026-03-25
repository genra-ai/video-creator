---
name: product-explainer
description: "Use this skill when the user wants to create a product explainer video: a presenter demonstrates and uses the product in a single scene, with engaging expressions and commentary. Triggered by: 'product explainer', 'product showcase video', 'make a demo video', 'explain my product'."
---

# Product explainer video

Turn a product image into a presenter-led showcase video: the presenter introduces and uses the product within one consistent scene.
Reference style: authentic handheld feel, lively expressions, genuinely engaging — like a friend sharing a find, not a scripted ad.

## Key Principles

- **Product identity is non-negotiable**: color, style, material, logo must match the reference image exactly in every shot — this is the top priority
- **One scene throughout**: all shots take place in the same space; background elements (furniture, lighting, wall tone) are identical across every shot — no location changes
- **Presenter appearance locked**: outfit, hairstyle, makeup, and accessories are word-for-word identical in every shot; define once as `identity_anchor` and reuse
- **Three shot types only**: ① mid-shot commentary (facing camera, holding or showing the product) ② full/half-body display (wearing or using the product) ③ product close-up (hands touching or highlighting a detail) — no other framing
- **Keep it lively and engaging**: presenter has expressive, natural reactions; every commentary shot must specify an expression state (surprise, excitement, confident approval, curious teasing); dialogue is conversational, like sharing with a friend — not reciting copy
- **Eyes are the hook**: every shot description must specify the eye state — eyes should feel alive, bright, and sharp, as if light is catching in the pupils; the gaze must feel like it's reaching through the lens directly at the viewer; dead or unfocused eyes kill engagement regardless of expression
- **Emotion drives movement, not the other way around**: every commentary shot must name what emotion triggers the presenter's physical action — leaning forward from surprise, a shoulder pop from excitement, stillness from confidence. Static descriptions like "presenter stands and talks" are forbidden; every shot must show how the body responds to the emotional beat
- **Audio before video**

## Workflow

### 1. Analyze the product

After the user uploads a product image, identify:
- Category (apparel / beauty / tech / food / home / other)
- Core visual features (color, material, key details, logo placement)
- Target audience and typical use context

### 2. Determine presenter

**If the user has described a presenter**: use it directly, no questions.

**If not**: recommend one based on the product, show it to the user, and wait for confirmation before proceeding:

| Product category | Recommended presenter |
|------------------|-----------------------|
| Women's fashion / beauty / skincare | Asian female, 25–30, natural makeup, warm and approachable |
| Men's fashion / tech / tools | Male, 28–35, clean and capable, trustworthy feel |
| Sports / outdoor gear | 25–32, athletic build, full of energy |
| Baby / home goods | Young mother, 28–35, warm and relatable |
| Food / beverage | Match product tone — can be upbeat or friendly |

Presenter description must specify: age range + gender + hair (length/color) + skin tone + top (color/material/cut) + one signature detail (ring, earring, hair clip) to serve as a cross-shot anchor.

**Attractiveness is part of the pitch**: the more camera-ready and conventionally attractive the presenter, the more credible and persuasive the product feels. Always default to a highly photogenic presenter unless the brief calls otherwise.

### 3. Write the storyboard

Up to 10 shots. Use only the three shot types. Follow this structure:

| Section | Shot type | Content | Shots |
|---------|-----------|---------|-------|
| Hook | Mid-shot commentary | Presenter appears, product revealed — lead with a hook ("This thing completely changed how I think about jeans") | 1–2 |
| Explain | Mid-shot + close-up alternating | Hold product, walk through key features one by one; close-ups for material, craft, logo | 3–4 |
| Demo | Full/half-body display | Presenter actually wears or uses the product, showing real fit or function | 2–3 |
| Close | Mid-shot commentary | Wrap-up recommendation, confident tone, one memorable line; presenter ends by pointing one finger downward toward the bottom of the screen — the TikTok CTA gesture directing viewers to the link below | 1 |

**Expression states** — every commentary shot must specify one:

| State | Visual description |
|-------|--------------------|
| Surprise | Eyebrows raised, eyes blown wide open with light catching in the pupils, mouth slightly open, body weight lurches forward as if pulled by the reaction |
| Excited sharing | Big teeth-showing smile, eyes bright and laser-focused on the lens — the gaze feels like it's reaching out of the screen; hands fly outward on the key word, shoulder pops with the energy |
| Confident approval | Slight chin dip, slow knowing nod, eyes steady and sharp — soft but unblinking, the kind of gaze that says "trust me"; body stills, letting presence do the work |
| Curious teasing | Head tilts, one brow lifts, smirk plays at the corner of the mouth; eyes narrow slightly with a glint — playful but pointed; finger moves toward product detail like revealing a secret |

**Product description rules** — required in every shot where the product appears:
- Exact color ("matte black, not dark grey") + material ("glossy coated denim with leather-like sheen") + key detail ("double-button waist, side zip")
- Never write "presenter holds the product" without describing the product itself

### 4. Create project and send script

Upload the product reference image and reference it in the script (`$asset_id`). Instruct the editor that all shots featuring the product must strictly match the reference image.

Send the complete script in one message: global style + scene definition + presenter identity_anchor + all shots.

### 5. Filter check

- All shots share the same `location_id` and `character_id`
- `identity_anchor` description is word-for-word identical across all shots
- Every product shot includes color + material + detail in the description
- Every commentary shot specifies an expression state

### 6. Generate audio → generate video

Voiceover pace: moderate-to-fast, conversational. Voice style should match the presenter (reference the presenter definition when describing the voice).
