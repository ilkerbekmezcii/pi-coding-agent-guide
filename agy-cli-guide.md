# 🥧 Antigravity CLI (`agy`) — General User Guide

> **The keyboard-centric, terminal-based interface for Google Antigravity agentic workflows.**

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.16-blue)
![License](https://img.shields.io/badge/license-Proprietary-red)
![Platform](https://img.shields.io/badge/platform-Google%20Antigravity-darkgreen)

**⭐ Fast, secure, and developer-first terminal agent control.**

</div>

---

## 📚 Table of Contents

- [What is agy?](#what-is-agy)
- [Getting Started](#getting-started)
- [Interactive Mode (TUI)](#interactive-mode-tui)
- [Configuration](#configuration)
- [Slash Commands](#slash-commands)
- [Essential Keyboard Shortcuts](#essential-keyboard-shortcuts)
- [Tips & Tricks](#tips--tricks)
- [Resources](#resources)
- [Quick Reference Card](#quick-reference-card)

---

## What is agy?

The **Antigravity CLI** (invoked with the command `agy`) is a lightweight, terminal-based interface designed for fast, direct, and keyboard-centric interaction with Google Antigravity agents. 

Rather than working through a browser or separate window, `agy` integrates directly into your local shell workspace. It gives you instant access to agent capabilities, parallel subagent orchestration, and background task management right from your command line.

---

## Getting Started

### 1. Launch the CLI

To start the Antigravity terminal session, open your terminal and run:

```bash
agy
```

On your first run, `agy` will present on-screen prompts to guide you through the initial setup and authentication.

### 2. Enter Your Prompts

Just like any standard assistant interface, you can type your coding requests naturally:

```
> Create a new React component called TaskList
> Run standard formatting on src/utils.js
> Check the git status and summarize modifications
```

### 3. Exit the CLI

To close the CLI session:
* Type `/quit` or `/exit` in the prompt box.
* Or press **Ctrl+D** twice (**Ctrl+D Ctrl+D**).

---

## Interactive Mode (TUI)

```
┌─ Startup Header ─────────────────────────────────────────────┐
│ /help for commands | keybindings.json loaded | active agent  │
├──────────────────────────────────────────────────────────────┤
│ Conversation Panel                                           │
│ • Your prompts and inputs                                    │
│ • Agent reasoning processes and terminal output logs         │
│ • Task results and background execution states               │
├──────────────────────────────────────────────────────────────┤
│ > Prompt Box (type your request here...)                      │
│   - Press Tab to autocomplete file paths                     │
│   - Type @ to suggest and reference workspace files          │
│   - Type ! to execute terminal commands directly            │
├──────────────────────────────────────────────────────────────┤
│ 📁 workspace/dir  📄 session-id  $0.15 remaining              │
└──────────────────────────────────────────────────────────────┘
```

### Prompt Box Features

- **Reference Files:** Type `@` followed by a file name to search and inject the file contents into the agent's context.
- **Run Terminal Commands:** Start a prompt with `!your-command` to run a shell command directly and send its output to the agent.
- **Multi-line Input:** Press `Shift+Enter` to add a new line inside the prompt box.

---

## Configuration

You can customize the behavior, interface, and keybindings of the `agy` CLI using the configuration files located in your local application directory.

- **Global Settings:** Located at `~/.gemini/antigravity-cli/settings.json`. Controls default providers, safety profiles, and interface theme settings.
- **Keybindings:** Located at `~/.gemini/antigravity-cli/keybindings.json`. Used to customize keyboard shortcuts. If you want to reset them to default settings, you can safely delete this file.

---

## Slash Commands

Type `/` in the prompt box to open the typeahead command menu, or type `/help` (or `?`) to view the interactive help panel.

| Command | Description |
|---------|-------------|
| `/resume` | Open the session list to resume or switch conversations |
| `/switch` | Quick-switch between active sessions |
| `/rewind` | Roll back conversation history to a previous step |
| `/undo` | Undo the last turn in the conversation |
| `/fork` | Create a new isolated workspace or branch from this session |
| `/clear` | Clear the prompt area and start a new session |
| `/agents` | Open the subagents panel to monitor active parallel agents |
| `/tasks` | Inspect, manage, or terminate running background tasks |
| `/config` | Open the settings panel to configure behavior |
| `/permissions`| Manage security profiles and agent run permissions |
| `/keybindings`| Open the keybindings utility to view/edit shortcuts |
| `/quit` | Exit the Antigravity CLI |

---

## Essential Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| **Escape** | Immediately interrupt a running agent or clear the prompt box |
| **Tab** | Trigger path completions when typing file paths |
| **Shift+Tab** | Navigate between tabs (General, Commands, Shortcuts) in the `/help` menu |
| **Ctrl+D (twice)** | Quick exit from the CLI |

---

## Tips & Tricks

- **Direct File Querying:** Ask questions about specific files instantly:
  ```bash
  agy @app.py "Analyze the database connection logic in this file"
  ```
- **One-Shot Execution:** Run a command directly from your terminal shell without entering the TUI:
  ```bash
  agy "Explain the current git diff"
  ```
- **Subagent Monitoring:** If you spawn parallel subagents, type `/agents` to inspect their individual logs and progression states.

---

## Resources

- **Main Documentation Home:** [antigravity.google/docs](https://antigravity.google/docs)
- **CLI Reference Guide:** [antigravity.google/docs/cli/reference](https://antigravity.google/docs/cli/reference)
- **CLI Best Practices:** [antigravity.google/docs/cli/best-practices](https://antigravity.google/docs/cli/best-practices)
- **Changelog & Releases:** [antigravity.google/changelog](https://antigravity.google/changelog)

---

## Quick Reference Card

```
┌──────────────────────────────────────────────────────────┐
│                   🥧 agy Quick Reference                 │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  START                     MANAGE                        │
│  agy             .......  Launch TUI      /resume        │
│  agy "prompt"    .......  With prompt     /fork          │
│  agy --help      .......  Show help       /clear         │
│                                           /quit          │
│                                                          │
│  EDITOR                    MONITOR                       │
│  @file           .......  Reference file  /agents        │
│  !command        .......  Run shell       /tasks         │
│  Shift+Enter     .......  New line        /permissions   │
│  Escape          .......  Interrupt                      │
│                                                          │
│  CONFIG                    SESSION                       │
│  /config         .......  Settings Panel  /rewind        │
│  /keybindings    .......  Edit shortcuts  /switch        │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

---

> **Antigravity CLI** — Proprietary — Developed with ❤️ by Google
