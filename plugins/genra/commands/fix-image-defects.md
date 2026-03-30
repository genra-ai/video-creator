---
name: fix-image-defects
description: "Detect and fix visual defects in generated images — watermarks, shot number labels bleeding into image, black/white borders, text overlays, finger distortion, local color errors. Triggered by: 'remove watermark', 'shot number showing in image', 'black border', 'fix fingers', 'remove all watermarks', 'check all images for defects'."
---

# Image Defect Check & Fix

## Mode
- **Global**: no specific shot mentioned → download and check all frame images
- **Targeted**: user specifies shot(s) → check only those frames

## Defect Types & Fix Methods

| Defect | Fix |
|--------|-----|
| Shot label / number bleeding in | I2I: remove label, preserve everything else |
| Black / white border | I2I: remove border, extend content to edges |
| Watermark or text overlay | I2I: remove only the overlay, preserve composition |
| Finger distortion (wrong count / fused) | I2I: correct fingers, preserve everything else |
| Local color or body part error | I2I: correct only that area |
| Overall poor quality | Regenerate image (update description if needed first) |

## Process

1. Download frame image(s) and view each
2. Identify defects using the table above
3. Apply fix — retry I2I once if it fails, then switch to full regeneration
4. Re-download to confirm the defect is gone
5. Mark fixed shots as needing video regeneration

## Output

Report what was found and fixed per shot. List shots requiring video regeneration.
