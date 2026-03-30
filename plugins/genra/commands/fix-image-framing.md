---
name: fix-image-framing
description: "Detect and fix images where the generated result does not match the image description — wrong shot scale, wrong camera angle, wrong subject crop, or key content missing/wrong. Triggered by: 'wrong shot scale', 'should be close-up but shows full body', 'angle is wrong', 'wrong crop', 'image doesn't match description', 'check all images against their descriptions'."
---

# Image vs. Description Mismatch Fix

## Mode
- **Global**: no specific shot mentioned → check all frame images against their image descriptions
- **Targeted**: user identifies the mismatch → fix directly

## What to Check

| Issue | Example |
|-------|---------|
| Wrong shot scale | Description: extreme close-up on hands; Generated: full body |
| Wrong camera angle | Description: low angle looking up; Generated: eye level |
| Wrong subject crop | Description: face only; Generated: includes full torso |
| Key content missing | Description: gold button on waistband; Generated: no button visible |

## Process

1. Read the image description's framing and content spec
2. Compare against the actual generated image
3. If mismatch found, rewrite the description to be more explicit:
   - Specify exactly what fills the frame and what must not appear
   - Vague: "close-up on waistband" → Explicit: "frame filled entirely with waistband area, no face visible, hands visible only from wrists down"
4. Regenerate the image
5. Confirm the result matches the intent
6. Mark fixed shots as needing video regeneration

## Output

Report each mismatch found, what was rewritten, and confirmation of the fix.
