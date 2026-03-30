---
name: fix-video-intent
description: "Detect and fix videos where the motion or action does not achieve the intended outcome described in the video description — the action is performed but the result state is never reached. E.g. cloth wipes but water stays, hand reaches but object doesn't move, candle is blown but flame stays. Triggered by: 'water not wiped clean', 'action has no effect', 'result not achieved', 'video doesn't match description', 'check all videos against their descriptions'."
---

# Video vs. Description Intent Fix

## Mode
- **Global**: no specific shot mentioned → review all videos against their video descriptions
- **Targeted**: user identifies the unmet intent → fix directly

## What to Look For

The character performs the correct action, but the physical outcome described never happens:
- Cloth wipes the surface but water / stain remains at end of shot
- Hand reaches for object but object stays in place
- Character blows out candle but flame stays lit
- Lid is twisted but bottle remains closed

This is distinct from motion quality issues — the video plays fine, the action looks natural, but the end state is wrong.

## Process

1. View the video and read its video description
2. Identify the intended end state that was not achieved
3. Rewrite the video description to explicitly state the result:
   - Add the end state as a concrete visual outcome: "by the end of the shot, the surface is completely dry with no visible water"
   - If needed, break the action into stages so the AI has clearer progression to follow
4. Regenerate the video
5. Retry once if the result is still not achieved — if it fails twice, note it as a known AI limitation for that action type

## Output

Report each unmet intent, how the description was updated, and any shots where the AI could not achieve the result after two attempts.
