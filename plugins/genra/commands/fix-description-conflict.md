---
name: fix-description-conflict
description: "Detect and fix conflicts where an action required in the video description has already been completed in the still frame — the action would be skipped or repeated during video generation. Triggered by: 'action already done in the image', 'check description conflicts', 'video description doesn't match the frame', 'check all shots for description conflicts'."
---

# Description vs. Image Conflict Fix

## Mode
- **Global**: no specific shot mentioned → download all frames, compare each against its video description
- **Targeted**: user specifies shot(s) → check only those frames

## Conflict Pattern

The video description asks for an action, but the still frame already shows that action completed:
- Description: "character raises the cup" — frame: cup already raised
- Description: "character turns to camera" — frame: already facing camera
- Description: "character opens the box" — frame: box already open

## Process

1. Download frame image(s) and view each
2. Read the video description for each shot
3. Identify any action in the description that is already completed in the frame
4. Rewrite the description only — no image regeneration needed:
   - Remove the completed action
   - Replace with: continuing naturally from the current state toward the next beat
   - Principle: "does X" → "continues from [current state shown], [next natural motion]"
5. Mark fixed shots as needing video regeneration

## Output

Report which shots had conflicts and how descriptions were updated. List shots requiring video regeneration.
