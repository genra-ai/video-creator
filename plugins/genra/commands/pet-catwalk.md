---
name: Pet Catwalk
description: "Upload a pet photo to generate a fashion runway walk video."
agent_description: "Use this skill when the user wants to generate a fashion runway video of their pet: upload a pet photo, generate a video of the pet wearing an outfit and walking the runway with confident catwalk steps, complete with professional runway lighting and background. Triggered by: 'pet catwalk', 'pet runway', 'make my cat/dog walk the runway', 'pet catwalk'."
---

# Pet Catwalk Video

Turns a user's pet photo into a fashion runway video. Core: img2img preserves the pet's real appearance, adds an outfit, places the pet on a professional runway, and generates an animated video of the pet strutting confidently.

## Key Principles

- **Pet appearance preserved**: fur color and face shape match the original — outfit is layered on top of the pet
- **Runway scene must be professional**: runway lighting, blurred audience background or clean show backdrop
- **Gait must have presence**: pet walking posture is confident and powerful, with "commanding presence" — not casual strolling
- **Outfit must be memorable**: choose visually striking outfits (haute couture, sportswear, vintage style etc.)
- **No tail frames**

## Workflow

### 1. Upload Pet Photo

Upload pet photo, record asset_id. Ideally a photo of the pet standing or walking, to make generating catwalk posture easier.

### 2. Confirm Outfit Style and Runway Scene

**Outfit style reference**:

| Outfit Type | Visual Effect |
|---|---|
| Haute couture | Gorgeous lace/silk, luxurious feel, suits cats |
| Sporty streetwear | Hoodie/joggers, street style, suits dogs |
| Vintage suit | Fine suit and tie, gentleman feel |
| Fantasy armor | Metallic armor, epic feel |
| Traditional Chinese outfit | Hanfu/cheongsam, classical beauty |
| Astronaut suit | White spacesuit, sci-fi feel |

**Runway scene reference**:

| Scene | Description |
|---|---|
| Professional fashion week | White or black runway track, blurred audience on both sides, overhead spotlights |
| Red carpet | Red carpet, flashbulb backdrop |
| Outdoor show | Natural light, grass or architectural ruin background, artistic feel |

### 3. Plan Shot Structure

**Full catwalk structure** (3–4 shots):

| Shot | Content | Duration |
|---|---|---|
| 1 | Wide shot: pet walks from far end toward camera, full outfit visible | 4–5s |
| 2 | Medium shot: pet walking sideways, gait showcase | 3–4s |
| 3 | Close-up: pet face + upper body, confident expression freeze | 3–4s |
| 4 (optional) | Wide shot: pet turns and walks away, back view closing | 3s |

**Single shot quick version** (only 1 shot needed): wide shot walking toward camera, 4–6s.

### 4. Send Shot List

```
Art style: realistic feel, fashion photography texture, professional lighting

[Global constraints]
- Pet start frame references original image [pet photo asset_id], preserve fur color and face shape
- Pet wearing [outfit description], outfit naturally fits pet's body shape
- Scene: [runway scene description]

Shot 1:
- Start frame: reference original image [asset_id], full body standing, wearing [outfit]
- Composition: wide shot, runway angle, pet walking from depth toward camera
- Lighting: overhead spotlights, rim lighting, professional show feel
- Duration: 5s
- Video description: pet walks toward camera with head held high, steps steady and powerful, head slightly raised, tail upright, catwalk gait

Shot 2 (optional): ...
```

### 5. Check Output

| Check Item | Standard |
|---|---|
| Pet appearance | Fur markings match original photo |
| Outfit plausibility | Outfit fits pet's body shape, not distorted |
| Gait presence | Pet's walking posture is powerful and confident, not casual |
| Scene professionalism | Runway lighting and background have fashion show atmosphere |

### 6. Export

---

## Resolution

| Use Case | Resolution |
|---|---|
| Douyin / TikTok / Reels | 720×1280 (9:16) |
| Horizontal / cinematic | 1280×720 (16:9) |
