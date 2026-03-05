# Genra Video Creator

AI skills for controlling the [Genra](https://genra.ai) video editor. Works with any autonomous AI agent — OpenClaw, Claude Code, and more.

## Table of Contents

- [What is this?](#what-is-this)
- [Usage](#usage)
  - [Any AI agent (copy & paste)](#option-1-any-ai-agent-copy--paste)
  - [Claude Code (plugin)](#option-2-claude-code-plugin)
  - [Genra built-in agent](#option-3-genra-built-in-agent)
## What is this?

Genra is an AI video editor. This repo provides **skills** (markdown instruction files) that teach AI agents how to operate it:

- `start.md` — Connection driver: auth flow, API format (curl), state polling. **Required for external agents.**
- Other skills — Reusable workflows: create a project, generate a trailer, etc. **Work with both external and built-in agents.**

## Usage

### Option 1: Any AI agent (copy & paste)

Copy the content of [`start.md`](plugins/genra/commands/start.md) into your agent's system prompt or context. The file teaches the agent:

1. How to authenticate (get a login URL, poll for auth)
2. The 3 core actions: `get_state`, `click`, `edit`
3. How to handle async operations
4. How to upload assets

Works with OpenClaw, Claude Code, or any autonomous agent that can execute HTTP requests.

### Option 2: Claude Code (plugin)

```bash
# Install
/plugin marketplace add genra-ai/video-creator
/plugin install genra@genra-ai

# Run
/genra:start
```

Claude Code loads `start.md` as a skill automatically. Additional workflow skills are also available as `/genra:<skill-name>` commands.

### Option 3: Genra built-in agent

[Genra](https://genra.ai) has a built-in AI agent in the editor. You can enable workflow skills directly from the chat panel — no setup needed.
