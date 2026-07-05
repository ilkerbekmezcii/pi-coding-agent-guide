🌍 [English](README.md) | [Türkçe](README.tr.md) | [Español](README.es.md)

# 🥧 Pi Coding Agent — General User Guide

> **The minimal, terminal-based coding assistant that fits into your everyday workflow.**

<div align="center">

![Version](https://img.shields.io/badge/version-0.80.3-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![GitHub Stars](https://img.shields.io/github/stars/earendil-works/pi?style=social)

[!["Star"](https://img.shields.io/github/stars/ilkerbekmezcii/pi-coding-agent-guide?style=social)](https://github.com/ilkerbekmezcii/pi-coding-agent-guide)

**⭐ If you find this guide useful, please star it!**

</div>

---

## 💰 Crypto Donations

```
BNB (BEP20):      0x799a799dE5C140DA95B11E2deFF2a9CA5f1F915a
Dogecoin (DOGE):  DJh5poVevoccpqPWng28hLkP775araunMf
```

---

## 📚 Table of Contents

- [What is Pi?](#what-is-pi)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Interactive Mode (TUI)](#interactive-mode-tui)
- [Providers & Models](#providers--models)
- [Sessions](#sessions)
- [Customization](#customization)
- [Settings](#settings)
- [CLI Reference](#cli-reference)
- [Tips & Tricks](#tips--tricks)
- [Resources](#resources)
- [Quick Reference Card](#quick-reference-card)

---

## What is Pi?

**Pi** is a minimal, terminal-based coding agent harness built with Node.js and TypeScript. It connects Large Language Models (LLMs) to your local files and system shell through four simple built-in tools: **read**, **write**, **edit**, and **bash**.

Unlike other heavy coding agents, Pi focuses on a **minimal core**:
- Runs directly inside your terminal.
- Performs actions only when prompted by you.
- Allows full control over your project workspace.

---

## Installation

### Via npm (recommended)

```bash
npm install -g --ignore-scripts @earendil-works/pi-coding-agent
```

> The `--ignore-scripts` flag is recommended to disable dependency lifecycle scripts.

### Via install script (curl)

```bash
curl -fsSL https://pi.dev/install.sh | sh
```

### 🪟 Windows (WinGet)
```powershell
winget install EarendilWorks.pi
```

---

## Quick Start

### 1. Authenticate with a Provider

Set your API key as an environment variable in your terminal:

```bash
# For macOS/Linux (Bash/Zsh)
export ANTHROPIC_API_KEY=sk-ant-...
export OPENAI_API_KEY=sk-...
export GEMINI_API_KEY=...

# For Windows (PowerShell)
$env:ANTHROPIC_API_KEY="sk-ant-..."
$env:OPENAI_API_KEY="sk-..."
$env:GEMINI_API_KEY="..."
```

### 2. Launch Pi

Launch the agent in the directory you want to work on:

```bash
# Launch interactive mode (TUI)
pi

# Launch with an initial prompt
pi "List all TypeScript files in this directory"

# Resume the last session
pi -c
```

### 3. Ask the Agent to Code

Once Pi is open, just describe what you want to achieve:

```
> Refactor index.js to use async/await
> Add a new endpoint to the express router for user registration
> Run the tests and fix any errors
```

---

## Interactive Mode (TUI)

```
┌─ Startup Header ─────────────────────────────────────────────┐
│ /hotkeys for shortcuts | AGENTS.md loaded | 3 skills loaded  │
├──────────────────────────────────────────────────────────────┤
│ Messages                                                     │
│ • Your prompts                                               │
│ • Assistant responses with reasoning/thinking blocks         │
│ • Tool calls and terminal command outputs                    │
├──────────────────────────────────────────────────────────────┤
│ > Editor (type your prompt here...)                          │
│   - Press Tab to autocomplete file paths                     │
│   - Type @ to search and reference project files             │
├──────────────────────────────────────────────────────────────┤
│ 📁 project/dir  📄 session-name  $0.02  claude-3-5-sonnet-latest │
└──────────────────────────────────────────────────────────────┘
```

### Editor Features

- **Reference Files:** Type `@` followed by a file name to search and inject the file contents as context.
- **Run Quick Commands:** Type `!your-command` in the editor to run a bash command and send the output to the LLM. Type `!!your-command` to run it without sending the output to the model.
- **Multi-line Prompts:** Press `Shift+Enter` (or `Ctrl+Enter` on Windows) to create a new line in the editor.

### Common Commands

Type `/` in the editor to run these commands:

| Command | Description |
|---------|-------------|
| `/model` | Open the model selector |
| `/settings` | Adjust TUI settings, themes, and thinking levels |
| `/new` | Start a fresh session |
| `/resume` | Browse and open past sessions |
| `/tree` | View the session history tree to rewind or branch out |
| `/compact` | Manually summarize older messages to save tokens |
| `/export` | Export the current session to an HTML file |
| `/quit` | Quit Pi |

### Essential Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| **Ctrl+C** | Clear the editor text |
| **Ctrl+C (twice)** | Quit Pi |
| **Escape** | Cancel a running task or close a dropdown menu |
| **Ctrl+L** | Quick model selector |
| **Shift+Tab** | Cycle between AI thinking/reasoning levels |
| **Ctrl+O** | Collapse/expand terminal tool outputs |
| **Ctrl+T** | Collapse/expand thinking/reasoning blocks |

---

## Providers & Models

Pi supports all major AI providers out of the box.

### Recommended Models

- **Claude 3.5 Sonnet** (`claude-3-5-sonnet-latest`) — Default recommendation. Excellent coding ability and reasoning.
- **GPT-4o** (`openai/gpt-4o`) — Strong code generation and speed.
- **Gemini 1.5 Pro** (`google/gemini-1.5-pro`) — Great for large contexts.

### Reasoning/Thinking Levels

For models that support reasoning (like Claude 3.7 or OpenAI o-series), you can cycle their thinking level using **Shift+Tab** in the interactive interface:
- `off` / `minimal` / `low` / `medium` (default) / `high` / `xhigh`

---

## Sessions

Pi automatically saves your conversations as JSONL files.

- **Resuming:** Use `pi -c` to continue your most recent session, or `pi -r` to browse and select a past session.
- **Auto-Compaction:** When a session gets too long, Pi automatically summarizes older parts of the conversation to save context window tokens, keeping the last few messages intact.

---

## Customization

You can personalize Pi using local directories.

### Placement Locations

- **Global Config:** Configured under `~/.pi/agent/`
- **Project Config:** Configured under `.pi/` in your project folder (active only after you trust the folder)

### Resource Types

- **Extensions:** Custom TypeScript scripts placed in `extensions/` to add new tools or TUI commands.
- **Skills:** Markdown files (`SKILL.md`) placed in `skills/` to teach the model step-by-step guides on how to interact with your codebase.
- **Prompt Templates:** Templates placed in `prompts/` to quickly insert pre-written instructions.
- **Themes:** TUI color themes (`.json`) placed in `themes/`.

---

## Settings

Create a `.pi/settings.json` file in your project or `~/.pi/agent/settings.json` globally to customize settings.

```json
{
  "defaultProvider": "anthropic",
  "defaultModel": "claude-3-5-sonnet-latest",
  "defaultThinkingLevel": "medium",
  "theme": "dark",
  "compaction": {
    "enabled": true,
    "keepRecentTokens": 20000
  }
}
```

---

## CLI Reference

```bash
pi [options] [@files...] [messages...]
```

| Flag | Description |
|------|-------------|
| *(none)* | Launch interactive TUI mode |
| `-p`, `--print` | One-shot mode: print response to console and exit |
| `-c`, `--continue` | Continue the most recent session |
| `-r`, `--resume` | Browse and choose a session to continue |
| `--model <id>` | Specify the model to use (e.g. `claude-3-5-sonnet-latest`) |
| `--provider <name>`| Specify the provider (e.g. `anthropic`, `openai`) |
| `--no-session` | Start in ephemeral mode (do not save session files) |
| `-h`, `--help` | Show command line help |

---

## Tips & Tricks

- **Pipe Terminal Outputs:** You can pipe terminal commands directly into Pi for a quick analysis:
  ```bash
  git diff | pi -p "Review these changes"
  ```
- **Context Inclusion:** Include a specific file immediately on startup:
  ```bash
  pi @package.json "What dependencies are in this project?"
  ```
- **Paste Screenshots:** In TUI mode, press `Ctrl+V` (or `Alt+V` on Windows) to paste a copied image from your clipboard to the agent.

---

## Resources

- **GitHub Repository:** [github.com/earendil-works/pi](https://github.com/earendil-works/pi)
- **Official Website:** [pi.dev](https://pi.dev)
- **Discord Community:** [Join Discord](https://discord.com/invite/3cU7Bz4UPx)
- **NPM Package:** [`@earendil-works/pi-coding-agent`](https://www.npmjs.com/package/@earendil-works/pi-coding-agent)

---

## Quick Reference Card

```
┌──────────────────────────────────────────────────────────┐
│                     🥧 Pi Quick Reference                │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  START                     MANAGE                        │
│  pi              .......  Launch TUI      /new           │
│  pi "prompt"     .......  With prompt     /resume        │
│  pi -p "..."     .......  One-shot        /tree          │
│  pi -c           .......  Continue        /quit          │
│  pi -r           .......  Resume                         │
│                                                          │
│  EDITOR                    CUSTOMIZE                     │
│  @file           .......  Reference file  /reload        │
│  !command        .......  Run bash        Extensions     │
│  Shift+Enter     .......  New line        Skills         │
│  Ctrl+V          .......  Paste image     Templates      │
│  Escape          .......  Cancel          Themes         │
│                                                          │
│  MODEL                     SESSION                       │
│  Ctrl+L          .......  Select model    /session       │
│  Ctrl+P          .......  Cycle models    /compact       │
│  Shift+Tab       .......  Thinking level  /export        │
│  /model          .......  Change model                   │
│                                                          │
│  MESSAGE QUEUE              TOOLS                        │
│  Enter (stream)  .......  Steer            read          │
│  Alt+Enter       .......  Follow-up        write         │
│  Alt+Up          .......  Retrieve         edit          │
│                                            bash          │
│                                            grep          │
│                                            find          │
│                                            ls            │
└──────────────────────────────────────────────────────────┘
```

---

> **Pi** — MIT Licensed — Made with ❤️ by the Pi Community\n
