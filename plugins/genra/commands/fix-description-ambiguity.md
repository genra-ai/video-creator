---
name: fix-description-ambiguity
description: "Detect and fix images where ambiguous description wording caused a physically impossible or wrong-angle result — e.g. seeing back of fabric through the front, inside-out garment, impossible camera penetration. Triggered by: 'seeing through fabric', 'physical blooper', 'impossible view', 'inside showing', 'back visible from front', 'check all shots for bloppers'."
---

# Description Ambiguity & Physical Blooper Fix

## Mode
- **Global**: no specific shot mentioned → download all frame images, scan for physically impossible content
- **Targeted**: user identifies the blooper → go directly to fix

## What to Look For

AI misinterpreted description wording and generated a physically impossible view:
- Seeing through solid fabric (back of jeans visible through front)
- Inside/lining of garment visible when no opening exists
- Camera angle that would require passing through a solid object
- Structure "shown open" when it should remain closed on the outside

**Root cause**: phrases like "展示内部结构", "张开展示", "内侧可见" that the AI interprets as a physical reveal.

## Process

1. Download and view frame image(s)
2. Identify the physical impossibility in the image
3. Trace it back to the specific ambiguous phrase in the description
4. Rewrite to eliminate ambiguity — specify exactly what is visible, from which angle, and what remains closed/solid
5. Regenerate the image with the updated description
6. Confirm the blooper is gone
7. Mark fixed shots as needing video regeneration

## Output

Report which shots had bloppers, which phrases caused them, and how descriptions were rewritten.
