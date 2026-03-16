---
name: genra:video-edit
description: "Execute edit operations on existing Genra video projects: single edits, systematic quality check (A/B/C three categories), or batch modifications. Triggered when the user says 'check it for me', 'remove the watermark', 'change shot X to...', 'check and fix', or 'video edit'."
---

# Video Edit

Select a mode based on user intent:
- **Single operation** ("Change shot 3's dialog to..." / "Remove the watermark from shot 5") → execute directly
- **Systematic quality check** ("Check it for me" / "See if there are any issues") → scan by A/B/C categories, then generate video in bulk
- **Batch modification** ("Replace X with Y in all shots") → execute per shot, then generate video in bulk

---

## Systematic Quality Check

### Step 1: Get State + Download All Images (A-category prerequisite, cannot be skipped)

**Note**: `workspace.frame_preview` only displays images in the browser UI; the API does not return image content. A-category checks require obtaining the real image URL via the WebSocket script in Appendix A first, downloading and viewing with the Read tool; otherwise A-category cannot be executed.

Execution order:

1. `get_state` to get all frameIds
2. Use Bash tool to run the Python WebSocket script in Appendix A (replace SESSION_KEY) to get the image URL for each shot
3. Use Bash tool to batch download: `curl -s --noproxy "genra.ai" {URL} -o /tmp/shot_N.jpg`
4. Use Read tool to open `/tmp/shot_N.jpg` frame by frame and view image content

Build a checklist:
```
Shot N: frameId=xxx  A-category=pending  B-category=pending  C-category=pending  needs video regeneration=no
```

Also check: for non-voiceover projects that have a tail_frame, send the message "Please clear all shot tail frames, keeping only the start frame".

### Step 2: A-category — Image Defects (must be based on images downloaded in Step 1)

After viewing the actual images with the Read tool, check each item (three mandatory checks per frame):

- **① Numbers/shot numbers bleeding into the image** (e.g., "SHOT 01" in the upper left corner)
- **② Black borders/white borders/frames**
- **③ Watermarks/text overlays**

Other issues: finger distortion or other local defects → I2I; overall poor quality/seriously incorrect content → regenerate image.

After fixing, record "needs video regeneration=yes", and re-download that shot's image to confirm the fix.

### Step 3: B-category — Cross-Shot Continuity

Compare adjacent shots to check whether character appearance (clothing/hairstyle/props/skin tone) and scene are consistent.
- Locally fixable → I2I; overall drift → regenerate image

Record "needs video regeneration=yes".

### Step 4: C-category — Description vs. Image Conflict

An action required in the video description has already been completed in the still frame → it will be repeated or skipped during video generation.

Fix: modify the video_description for that shot via chat message, remove the action already completed in the still frame, and replace it with continuing from the current state (**no need to regenerate the image**).

Record "needs video regeneration=yes".

### Step 5: Generate Video in Bulk + Output Report

Batch generate all shots marked "needs video regeneration=yes" (see Appendix for video generation), then output:

```
## Quality Check Report
### A-category: Shot 1 — number "SHOT 01" → I2I ✓; no issues with others
### B-category: No issues
### C-category: Shot 2 — action overlap → modified video_description ✓
### Video: Shots 1 and 2 generated
### Conclusion: N issues found, M fixed
```

---

## Batch Targeted Modification

1. Confirm the modification target/goal/scope; if a reference image is needed, upload it first to get the asset_id
2. Download all images and assess frame by frame whether the modification target appears
3. If present → I2I replacement (local) or regenerate image (overall); if not present → skip
4. After all are done, run a consistency check and generate video in bulk

---

## Single Operation

**I2I edit**: see Appendix

**Modify description and regenerate image**:
```
edit {frameId}.description {new description}
click workspace.frame_select.{frameId} → check only image/frame → click regenerate.btn_confirm
```

**Modify dialog**: `edit dialog.{groupId}.{itemId}.text {new content}` → regenerate audio

**Clear/set tail frame**:
- Clear (script-to-video / ad-to-video, etc.): send message "Please clear all shot tail frames, keeping only the start frame"
- Set (voiceover): send message "Please set the tail frame of shot N to the start frame asset_id of shot N+1"

---

## Appendix: Core Operation Reference

### A. Get Frame Image URL

WebSocket endpoint: `wss://action.genra.ai/` (requires the current valid session_key)

```python
import asyncio, ssl, struct, urllib.parse, json, re, base64, os

async def get_frame_urls(sk):
    ctx = ssl.create_default_context()
    ws_key = base64.b64encode(os.urandom(16)).decode()  # must be 16 bytes
    r, w = await asyncio.wait_for(
        asyncio.open_connection("action.genra.ai", 443, ssl=ctx), timeout=8)
    w.write((
        f"GET /?sk={urllib.parse.quote(sk)} HTTP/1.1\r\nHost: action.genra.ai\r\n"
        f"Upgrade: websocket\r\nConnection: Upgrade\r\n"
        f"Sec-WebSocket-Key: {ws_key}\r\nSec-WebSocket-Version: 13\r\n\r\n"
    ).encode())
    await w.drain()
    buf = b""
    while b"\r\n\r\n" not in buf:
        buf += await asyncio.wait_for(r.read(2048), timeout=5)
    if b"HTTP/1.1 101" not in buf:
        w.close(); return
    fh = await asyncio.wait_for(r.read(2), timeout=10)
    plen = fh[1] & 0x7f
    if plen == 126: plen = struct.unpack('>H', await r.read(2))[0]
    elif plen == 127: plen = struct.unpack('>Q', await r.read(8))[0]
    payload = b""
    while len(payload) < plen:
        payload += await asyncio.wait_for(r.read(min(65536, plen - len(payload))), timeout=20)
    w.close()
    text = payload.decode("utf-8", errors="replace")
    m = re.search(r'"asset_resource_map"\s*:\s*(\{[^}]+\})', text)
    if not m: return
    arm = json.loads(m.group(1))
    BASE = "https://genra.ai/cdn-cgi/imagedelivery/sRnkkEKABopU93NFwT1YuA"
    for asset_key, uuid in arm.items():
        short = asset_key.replace("asset_","").replace(".png","").replace(".jpg","")
        ctx2 = text[max(0, text.find(short)-300) : text.find(short)+300]
        shot = re.search(r'v_shot_\d+_\w+', ctx2)
        print(f"{shot.group() if shot else asset_key}: {BASE}/{uuid}/public")

asyncio.run(get_frame_urls("SESSION_KEY_HERE"))
```

Download (bypass proxy): `curl -s --noproxy "genra.ai" {URL} -o /tmp/shot_N.jpg`

After downloading, use the `Read` tool to view images (supports direct display of jpg/png) and check each frame for A-category defects.

### B. I2I Image Edit (four steps, all required)

```
Step 1: click workspace.frame_preview.{frameId}
        → verify return contains [preview] mode=asset
Step 2: edit chat.input {instruction}
Step 3: click chat.btn_send → wait for panel to appear (approx. 30s)
Step 4: verify [panel] targets=1 and frames: xxx(sel)
        → click regenerate.btn_confirm
```

**Panel issues**:
- `targets=2` (both frame + video selected) → `regenerate.toggle_resource {videoId}` to deselect video
- `btn_confirm` does not appear → insufficient credits

**Instruction format**: `Based on the current image, perform I2I editing: [what to change], [what to preserve]`

| Scenario | Key instruction |
|------|---------|
| Remove number/shot label | `Remove the number "X" (shot label) appearing in the image; completely preserve all other content and composition` |
| Remove black border/frame | `Remove the border around the image; extend the image content to fill the edges; main subject and composition unchanged` |
| Remove watermark | `Remove the watermark/text overlay in the image; keep content and composition completely unchanged` |
| Fix finger distortion | `Fix distortion of the right hand fingers (currently X fingers); correct to normal 5 fingers; everything else unchanged` |
| Fix local color | `Change [body part] from [current state] to [target state]; other elements unchanged` |

I2I: retry at most 1 time; if two attempts are unsatisfactory, switch to "modify description and regenerate image".

### C. Video Generation

**Batch**: `click workspace.btn_pipeline_videos` → confirm the number selected (if any are missed, use `regenerate.toggle_resource` to add them) → `click regenerate.btn_confirm`

**Single shot**: `click workspace.frame_select.{frameId}` → check only video → confirm

Poll every 15s, check `videos: XX%` and the `(vid)` flag on each frame. If "service busy" is shown, retry individually later.
