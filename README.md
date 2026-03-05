# Genra Video Creator

AI skills that allow autonomous agents to control the [Genra](https://genra.ai) video creation platform.

## Table of Contents

- [Overview](#overview)
- [Built-in Genra Agent](#built-in-genra-agent)
- [Using Genra from External Agents](#using-genra-from-external-agents)
- [Usage (Quick Start)](#usage-quick-start)

## Overview

[Genra](https://genra.ai) is an AI video creation platform for creating and editing video projects, generating clips, voiceovers, background music, and exporting final videos.

Genra already includes a **built-in AI agent** inside the editor — users can start creating videos immediately without any setup.

However, many developers prefer to work from their own AI agents. This repository exposes Genra's capabilities as **skills** — markdown instruction files that teach external agents how to control the editor via API.

## Built-in Genra Agent

Genra ships with an AI agent directly in the editor. Open a project, use the chat panel, and start editing. No configuration required.

## Using Genra from External Agents

If you use tools like **Claude Code**, **OpenClaw**, **Codex**, **Gemini CLI**, or other autonomous agents, you can integrate Genra into your existing workflow. This repo provides skill files that teach your agent how to do so.

Your agent talks to Genra through a simple HTTP API — no SDK needed.

## Usage (Quick Start)

### Option 1 — Built-in Genra Agent

Open [Genra](https://genra.ai) and use the chat panel. No setup needed.

### Option 2 — Any AI Agent

Paste this URL into your agent's context, and now it understands:

```
https://github.com/genra-ai/video-creator/blob/main/plugins/genra/commands/start.md
```

### Option 3 — Claude Code (plugin)

```bash
# Install
/plugin marketplace add genra-ai/video-creator
/plugin install genra@genra-ai

# Run
/genra:start
```

Claude Code loads Genra skills automatically.

