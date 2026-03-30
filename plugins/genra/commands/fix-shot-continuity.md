---
name: fix-shot-continuity
description: "Check and fix cross-shot continuity — character clothing, hairstyle, props, skin tone, and scene consistency between adjacent shots. Triggered by: 'character changed between shots', 'outfit inconsistent', 'check continuity', 'shots don't match', 'scene changed', 'check all shots for continuity'."
---

# Cross-Shot Continuity Check & Fix

## Mode
- **Global**: no specific shot mentioned → download all frames, compare adjacent pairs with shot 1 as baseline
- **Targeted**: user specifies shot(s) → compare those shots to their neighbors

## Dimensions to Check

| Dimension | What to Look For |
|-----------|-----------------|
| Clothing | Same color, material, cut — no items appearing or disappearing |
| Hairstyle | Length, texture, color consistent |
| Props / accessories | Same items in same positions |
| Skin tone | No noticeable shift between shots |
| Scene / background | Key elements identical; nothing appearing or disappearing |
| Lighting | Color temperature and direction roughly consistent |

## Process

1. Download frame images and view each
2. Compare each shot against the previous — note any drifted dimensions
3. Fix:
   - Single element slightly off → I2I: correct only that element, preserve everything else
   - Multiple elements or overall drift → Regenerate image with corrected description
4. Retry I2I once if it fails, then regenerate
5. Re-download to confirm consistency with adjacent shot
6. Mark fixed shots as needing video regeneration

## Output

Report per-shot comparison results and what was fixed. List shots requiring video regeneration.
