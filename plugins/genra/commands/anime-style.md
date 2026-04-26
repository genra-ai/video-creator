---
name: Anime Style
description: "Upload an image to transform it into popular anime art styles."
agent_description: "Use this skill when the user wants to convert an image into a popular anime art style: uses img2img to preserve original subject content, supports high-traffic styles like Studio Ghibli, Pixar, The Simpsons, Cyberpunk Anime, Marvel Comics. Image input only — no video-to-video conversion. Triggered by: 'turn into anime', 'Ghibli style', 'Pixar style', 'Simpsons style', 'cyberpunk anime', 'cartoonify', 'anime style'."
---

# Anime Style Conversion

Converts a user-provided image into a specified anime art style using img2img, preserving the original subject content (characters, scenes, composition), and outputting a style-converted image or short animated video.

## Key Principles

- **Image input only**: no video-to-video style conversion support
- **Preserve subject, transform style**: the original image's composition, character position, and main elements are kept — only the art style changes
- **Style prompt must be precise**: different styles have fixed keyword formulas and must not be mixed
- **Single shot output as default**: static image or 3–5 second short animated video

## Supported Styles & Prompt Formulas

| Style | Core Prompt Keywords | Visual Characteristics |
|---|---|---|
| Studio Ghibli / Miyazaki | `Studio Ghibli art style, Hayao Miyazaki, hand-drawn animation, soft watercolor` | Soft watercolor feel, natural light, rounded lines, warm tones |
| Pixar / Disney 3D | `Pixar animation style, Disney 3D, expressive character, studio lighting` | Strong 3D feel, detailed skin, large eyes, bright light |
| The Simpsons | `The Simpsons cartoon style, Matt Groening, yellow skin, thick black outline` | Yellow skin, thick black outlines, flat color blocks |
| Cyberpunk Anime | `Cyberpunk anime style, neon lights, dark city, Japanese anime aesthetic` | Neon light effects, dark background, high contrast, anime line feel |
| Marvel Comics | `Marvel comic book style, Ben-Day dots, bold outlines, dynamic pose, halftone` | Thick outlines, halftone printing feel, high-saturation color blocks, dynamic composition |

## Workflow

### 1. Confirm Style and Upload Image

**Required info**: target style name + original image (upload to get asset_id).

**Image requirements**:
- Subject must be clear, background should not be overly complex
- Front-facing or 3/4 angle works best for characters
- Sufficient resolution (blurry photos convert poorly)

### 2. Upload Image, Send Shot List

Upload the original image, record asset_id.

```
Art style: [full target style prompt, see formula above]

[Global constraints]
- Reference original image [asset_id], preserve original composition, subject position, and main content
- Re-render the art style completely using the above art style
- Maintain original image aspect ratio

Shot 1: Reference original image [asset_id], [target style] art style conversion, preserve subject composition, duration [3–5s]
```

**Generate video or not**:
- Static image only: generate start frame only, no video
- Need subtle animation: generate 3–5 second short video, video description: "subtle animation, subject stays still, background has faint flowing movement"

### 3. Check Output

| Check Item | Standard |
|---|---|
| Subject preserved | Original character/subject still recognizable |
| Style accurate | Clearly matches the target style's visual characteristics |
| Composition consistent | Basically consistent with original composition |

If style feel is insufficient: strengthen the style keywords in the prompt, or lower the img2img similarity parameter.
If subject is distorted: increase img2img similarity, add `preserve subject details` to the prompt.

### 4. Export

---

## Resolution

Maintain same ratio as original image. Default output 720×1280 (9:16) or 1:1, adjusted based on original.
