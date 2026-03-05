# Genra Video Creator

AI skills that allow autonomous agents to control the [Genra](https://genra.ai) video editor.

## Overview

[Genra](https://genra.ai) is an AI video editor for creating and editing video projects, generating clips, voiceovers, background music, and exporting final videos.

Genra already includes a **built-in AI agent** inside the editor — most users can start creating videos immediately without any setup.

However, many developers prefer to work from their own AI agents. This repository exposes Genra's capabilities as **skills** — markdown instruction files that teach external agents how to control the editor via API.

## Built-in Genra Agent

Genra ships with an AI agent directly in the editor. Open a project, use the chat panel, and start editing. No configuration required.

## Using Genra from External Agents

If you use tools like **Claude Code**, **OpenClaw**, **Codex**, **Gemini CLI**, or other autonomous agents, you can integrate Genra into your existing workflow.

This repo provides skill files that teach your agent:

- How to authenticate with Genra
- How to read editor state, click UI elements, and edit text
- How to handle async operations
- How to upload assets

Your agent talks to Genra through a simple HTTP API — no SDK needed.

## Repository Structure

```
plugins/genra/
  .claude-plugin/
    plugin.json                # Claude Code plugin metadata
  commands/
    start.md                   # Core skill: auth, API, state polling
    script-to-video.md         # Workflow: multi-shot script → video
    ad-to-video.md             # Workflow: brand atmosphere ad
    product-showcase.md        # Workflow: e-commerce product showcase
    voiceover.md               # Workflow: talking-head video
.claude-plugin/
  marketplace.json             # Claude Code marketplace config
```

## Skills

Skills are markdown instruction files. An AI agent reads them to learn how to operate Genra.

### `start.md`

The core skill. Required for all external agents. It covers:

- **Authentication** — Call `get_state` without a session key, show the returned login URL to the user, poll until authorized
- **Core actions** — `get_state` (read current state), `click` (interact with UI), `edit` (modify text fields)
- **API format** — All interactions use `curl` POST requests to `https://agent.genra.ai/`
- **Async handling** — Quick ops return immediately; long ops return a job ID, poll `get_state` at 10s intervals
- **Asset uploads** — Upload files via multipart form, reference returned asset IDs in messages

### Workflow Skills

Workflow skills are end-to-end video creation pipelines. Each one handles a specific video type — from script analysis through image/audio/video generation to export.

| Skill | Description |
|-------|-------------|
| [`script-to-video.md`](plugins/genra/commands/script-to-video.md) | Convert a multi-shot script (6–15 shots, multiple characters and scenes) into video. Preserves the original script, auto-completes visual descriptions for characters, scenes, and lighting. |
| [`ad-to-video.md`](plugins/genra/commands/ad-to-video.md) | Create brand atmosphere ads from a product/brand and mood direction. Focuses on emotion arcs, visual worlds, and fast/slow editing rhythm — inspired by Nike, Red Bull, Apple brand films. |
| [`product-showcase.md`](plugins/genra/commands/product-showcase.md) | Generate e-commerce product showcase videos. Structures shots around selling points with hero shots, feature demos, usage scenes, and CTA endings. |
| [`voiceover.md`](plugins/genra/commands/voiceover.md) | Produce 20–30s talking-head videos. Fixed framing, single character facing camera, with frame-to-frame continuity for seamless shot transitions. |

All workflow skills work with both external agents and the Genra built-in agent.

## Usage

### Option 1 — Built-in Genra Agent

Open [Genra](https://genra.ai) and use the chat panel. No setup needed.

### Option 2 — Any AI Agent (copy & paste)

Copy the contents of [`start.md`](plugins/genra/commands/start.md) into your agent's system prompt or context.

The file teaches your agent the full auth flow, the three core actions (`get_state`, `click`, `edit`), async polling, and asset uploads — everything needed to control the Genra editor.

### Option 3 — Claude Code (plugin)

```bash
# Install
/plugin marketplace add genra-ai/video-creator
/plugin install genra@genra-ai

# Run
/genra:start
```

Claude Code loads `start.md` as a skill automatically. Workflow skills are available as commands:

```bash
/genra:script-to-video
/genra:ad-to-video
/genra:product-showcase
/genra:voiceover
```
