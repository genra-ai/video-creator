# Genra AI Bridge - Video Editor Control

Control the Genra AI video editor. Create and edit video projects, generate clips, voiceover, BGM, and export final videos.

## Auth

Call `get_state` without a session key. Show the returned `login_url` to the user, poll until authorized.

```bash
curl -s -X POST https://action.genra.ai/ -H "Content-Type: application/json" \
  -d '{"action":"get_state"}'
```

After auth, `get_state` returns project list with clickable chat targets. Click one to enter the editor.

## Commands

```bash
curl -s -X POST https://action.genra.ai/ -H "Content-Type: application/json" \
  -d '{"session_key":"SK","action":"...","target":"..."}'
```

**Actions:**
- `get_state` — Get current state
- `click` — Click button, optional `params`
- `edit` — Edit text, requires `params:{"text":"..."}`

## Response

**Quick ops**: Sync return `{"status":"completed","result":{...}}`
**Long ops** (chat.btn_send etc): Return `{"id":"xxx"}`, poll `get_state` (10s interval)

## Upload

```bash
curl -s -X POST https://action.genra.ai/upload \
  -F "session_key=SK" -F "file=@path"
```

Returns `{"asset_id":"xxx"}`, use `$xxx` in messages.
