---
name: fix-video-motion
description: "Detect and fix video generation quality issues — character frozen, excessive shaking, character drifts out of frame, unnatural or clipping limb movement. Focus is on motion quality itself, not whether the content matches the description. Triggered by: 'character frozen', 'video shaking', 'exits frame', 'motion looks wrong', 'unnatural movement', 'check all videos for motion issues'."
---

# Video Motion Quality Fix

## Mode
- **Global**: no specific shot mentioned → review all generated videos
- **Targeted**: user identifies the problem video → fix directly

## What to Look For

| Issue | Description |
|-------|-------------|
| Frozen | Character has no movement at all |
| Shaking / jitter | Camera or character vibrates unnaturally |
| Exits frame | Character or subject drifts out of the shot boundary |
| Unnatural movement | Limbs bend wrong, clip through objects, or snap between positions |

## Process

1. View the video and identify the motion issue type
2. Adjust the video description to constrain movement — add explicit direction, speed, and range
3. Regenerate the video
4. Retry once if the issue persists — if it fails twice, note it as a known generation limitation

## Output

Report each video's issue type, what was changed, and any shots where the problem persisted after two attempts.
