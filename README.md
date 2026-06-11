# 🥧 Pi Coding Agent — The Complete Guide

> **The terminal coding harness that adapts to *your* workflow — not the other way around.**

<div align="center">

![Version](https://img.shields.io/badge/version-0.79.1-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![GitHub Stars](https://img.shields.io/github/stars/earendil-works/pi?style=social)

[!["Star"](https://img.shields.io/github/stars/ilkerbekmezcii/pi-coding-agent-guide?style=social)](https://github.com/ilkerbekmezcii/pi-coding-agent-guide)

**⭐ If you find this guide useful, please star it!**

</div>

---

## ₿ Crypto Donations

```
Bitcoin (BTC):       bc1qck3e9dwqkj9qnmwzut43sv48wwat7mhywd0rwr
BNB / USDT (BEP20):  0x799a799dE5C140DA95B11E2deFF2a9CA5f1F915a
Dogecoin (DOGE):     DJh5poVevoccpqPWng28hLkP775araunMf
```

> 💡 **Recommended:** USDT (BEP20) — fee ~$0.03, instant.

---

## 📚 Table of Contents

- [What is Pi?](#what-is-pi)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Interactive Mode](#interactive-mode)
  - [Editor](#editor)
  - [Commands](#commands)
  - [Keyboard Shortcuts](#keyboard-shortcuts)
  - [Message Queue](#message-queue)
- [Providers & Models](#providers--models)
- [Sessions](#sessions)
  - [Management](#management)
  - [Branching with /tree](#branching-with-tree)
  - [Forking & Cloning](#forking--cloning)
  - [Compaction](#compaction)
- [Customization](#customization)
  - [Extensions](#extensions)
  - [Skills](#skills)
  - [Prompt Templates](#prompt-templates)
  - [Themes](#themes)
  - [Pi Packages](#pi-packages)
- [Settings](#settings)
- [Programmatic Usage](#programmatic-usage)
  - [SDK](#sdk)
  - [RPC Mode](#rpc-mode)
- [CLI Reference](#cli-reference)
- [Philosophy](#philosophy)
- [Tips & Tricks](#tips--tricks)
- [FAQ](#faq)
- [Resources](#resources)

---

## What is Pi?

**Pi** is a minimal, terminal-based coding agent harness built with Node.js/TypeScript. It gives Large Language Models (LLMs) four built-in tools — **read**, **write**, **edit**, and **bash** — and lets them fulfill your requests directly in your terminal.

Unlike many other coding agents, Pi follows a **"minimal core, everything is an extension"** philosophy:

- ❌ **No MCP** built-in (add it via extension if you want it)
- ❌ **No sub-agents** (build them with extensions or use tmux)
- ❌ **No permission popups** (run in a container or build your own confirmation flow)
- ❌ **No plan mode** (write plans to files, or build it with extensions)
- ❌ **No built-in to-dos** (they confuse models — use a TODO.md file)
- ❌ **No background bash** (use tmux for full observability)

Pi believes you should adapt the tool to **your workflow**, not the other way around. Extend it with:

- **🧩 Extensions** — TypeScript modules that add tools, commands, events, and UI
- **📋 Skills** — Markdown-based capability packages (Agent Skills standard)
- **📝 Prompt Templates** — Reusable prompts as Markdown files
- **🎨 Themes** — Custom TUI color themes (hot-reload capable)
- **📦 Pi Packages** — Share extensions, skills, prompts, and themes via npm or git

Pi runs in four modes:
1. **Interactive (TUI)** — Full terminal user interface
2. **Print** — Non-interactive, single response
3. **JSON** — Event stream as JSON lines
4. **RPC** — Process integration over stdin/stdout

---

## Installation

### Via npm (recommended)

```bash
npm install -g --ignore-scripts @earendil-works/pi-coding-agent
```

> `--ignore-scripts` disables dependency lifecycle scripts — Pi doesn't need them.

### Via install script (curl)

```bash
curl -fsSL https://pi.dev/install.sh | sh
```

### Platform-Specific Guides

| Platform | Guide |
|----------|-------|
| 🪟 Windows | [docs/windows.md](https://github.com/earendil-works/pi/blob/main/docs/windows.md) |
| 📱 Termux (Android) | [docs/termux.md](https://github.com/earendil-works/pi/blob/main/docs/termux.md) |
| 🖥️ tmux | [docs/tmux.md](https://github.com/earendil-works/pi/blob/main/docs/tmux.md) |
| 🎨 Terminal Setup | [docs/terminal-setup.md](https://github.com/earendil-works/pi/blob/main/docs/terminal-setup.md) |
| 🔗 Shell Aliases | [docs/shell-aliases.md](https://github.com/earendil-works/pi/blob/main/docs/shell-aliases.md) |

---

## Quick Start

### 1. Authenticate with a Provider

```bash
# API key (set as environment variable)
export ANTHROPIC_API_KEY=sk-ant-...
export OPENAI_API_KEY=sk-...
export GEMINI_API_KEY=...

# Or use OAuth login inside Pi
pi
/login
```

### 2. Launch Pi

```bash
# Interactive mode (default)
pi

# With an initial prompt
pi "List all .ts files in src/"

# One-shot, non-interactive
pi -p "Summarize this codebase"

# Continue your last session
pi -c

# Pipe input
cat README.md | pi -p "Summarize this text"
```

### 3. Start Coding

Just talk to Pi naturally:

```
> Show me all the TypeScript files in this project
> Refactor this function to use async/await
> Write unit tests for the auth module
> What's the current git status?
```

Pi will use its built-in tools (`read`, `write`, `edit`, `bash`) to accomplish your requests.

---

## Interactive Mode

![Interactive Mode](https://pi.dev/interactive-mode.png)

The interface from top to bottom:

```
┌─ Startup Header ─────────────────────────────────────────────┐
│ /hotkeys for shortcuts | AGENTS.md loaded | 3 skills loaded  │
├──────────────────────────────────────────────────────────────┤
│ Messages                                                     │
│ • Your prompts                                               │
│ • Assistant responses with thinking blocks (if enabled)      │
│ • Tool calls and results (collapsible with Ctrl+O)           │
│ • Notifications and errors                                   │
│ • Extension UI components                                    │
├──────────────────────────────────────────────────────────────┤
│ > Editor (type here...)                            [border]  │
│   - @ to fuzzy-find files                                   │
│   - !command to run bash                                    │
│   - !!command to run bash without sending to LLM            │
│   - Ctrl+V / drag to paste images                           │
├──────────────────────────────────────────────────────────────┤
│ 📁 working/dir  📄 session-name  ↑2.5K ↓1.2K  $0.03  70%   │
│ R 500 W 200 CH 85%  claude-sonnet-4-20250514                │
└──────────────────────────────────────────────────────────────┘
```

### Editor

| Feature | How |
|---------|------|
| **File reference** | Type `@` to fuzzy-search project files |
| **Path completion** | Tab to complete paths |
| **Multi-line** | Shift+Enter (or Ctrl+Enter on Windows Terminal) |
| **Images** | Ctrl+V to paste (Alt+V on Windows), or drag onto terminal |
| **Bash commands** | `!command` runs and sends output to LLM, `!!command` runs without sending |
| **Clear editor** | Ctrl+C |
| **Abort/cancel** | Escape (Escape twice opens `/tree`) |

### Commands

Type `/` in the editor to trigger commands:

| Command | Description |
|---------|-------------|
| `/login`, `/logout` | OAuth authentication |
| `/model` | Switch models |
| `/scoped-models` | Enable/disable models for Ctrl+P cycling |
| `/settings` | Thinking level, theme, message delivery, transport |
| `/resume` | Pick from previous sessions |
| `/new` | Start a new session |
| `/name <name>` | Set session display name |
| `/session` | Show session info (file, ID, messages, tokens, cost) |
| `/tree` | Jump to any point in the session and continue from there |
| `/trust` | Save project trust decision |
| `/fork` | Create a new session from a previous user message |
| `/clone` | Duplicate the current active branch into a new session |
| `/compact [prompt]` | Manually compact context |
| `/copy` | Copy last assistant message to clipboard |
| `/export [file]` | Export session to HTML file |
| `/share` | Upload as private GitHub gist with shareable HTML link |
| `/reload` | Reload keybindings, extensions, skills, prompts, and context files |
| `/hotkeys` | Show all keyboard shortcuts |
| `/changelog` | Display version history |
| `/quit` | Quit pi |

### Keyboard Shortcuts

| Key | Action |
|-----|--------|
| **Ctrl+C** | Clear editor |
| **Ctrl+C ×2** | Quit |
| **Escape** | Cancel/abort |
| **Escape ×2** | Open `/tree` |
| **Ctrl+L** | Open model selector |
| **Ctrl+P / Shift+Ctrl+P** | Cycle scoped models forward/backward |
| **Shift+Tab** | Cycle thinking level |
| **Ctrl+O** | Collapse/expand tool output |
| **Ctrl+T** | Collapse/expand thinking blocks |
| **Ctrl+G** | Open external editor (uses `$VISUAL` or `$EDITOR`) |
| **@** | Trigger file autocomplete |

All keybindings are customizable in `~/.pi/agent/keybindings.json`. Run `/reload` after editing.

### Message Queue

While the agent is working, you can queue messages:

| Action | Result |
|--------|--------|
| **Enter** (while streaming) | Queues a **steering** message — delivered after current tool calls finish |
| **Alt+Enter** (while streaming) | Queues a **follow-up** message — delivered only after all tools finish |
| **Escape** (while queued) | Restores queued messages back to editor |
| **Alt+Up** | Retrieves queued messages back to editor |

---

## Providers & Models

Pi supports a wide range of AI providers:

### 🔑 API Key Providers

| Provider | Environment Variable |
|----------|---------------------|
| **Anthropic** (Claude) | `ANTHROPIC_API_KEY` |
| **OpenAI** (GPT-4o, o-series) | `OPENAI_API_KEY` |
| **Google Gemini** | `GEMINI_API_KEY` |
| **DeepSeek** | `DEEPSEEK_API_KEY` |
| **Mistral** | `MISTRAL_API_KEY` |
| **Groq** | `GROQ_API_KEY` |
| **Cerebras** | `CEREBRAS_API_KEY` |
| **xAI** (Grok) | `XAI_API_KEY` |
| **OpenRouter** | `OPENROUTER_API_KEY` |
| **Together AI** | `TOGETHER_API_KEY` |
| **Fireworks** | `FIREWORKS_API_KEY` |
| **NVIDIA NIM** | `NVIDIA_NIM_API_KEY` |
| **Hugging Face** | `HUGGINGFACE_API_KEY` |
| **Amazon Bedrock** | AWS credentials |
| **Azure OpenAI** | `AZURE_OPENAI_API_KEY` |
| **Google Vertex** | GCP credentials |
| **Cloudflare** | `CLOUDFLARE_API_TOKEN` |
| **and more...** | 30+ total providers |

### 📋 Subscription Providers

| Provider | Login Command |
|----------|---------------|
| **Anthropic Claude Pro/Max** | `/login` → select subscription |
| **OpenAI ChatGPT Plus/Pro (Codex)** | `/login` → select subscription |
| **GitHub Copilot** | `/login` → select subscription |

### 🎯 Selecting a Model

```bash
# Via CLI
pi --model claude-sonnet-4-20250514
pi --model openai/gpt-4o
pi --model sonnet:high  # with thinking level

# Via interactive commands
pi          # then type: /model
            # or press: Ctrl+L
```

### Thinking Levels

| Level | Description |
|-------|-------------|
| `off` | No thinking tokens |
| `minimal` | Minimal reasoning |
| `low` | Light reasoning |
| `medium` | Balanced reasoning (default) |
| `high` | Deep reasoning |
| `xhigh` | Maximum reasoning |

Cycle with `Shift+Tab` in interactive mode.

---

## Sessions

Pi saves your work sessions as JSONL files with a built-in **tree structure**. Each entry has an `id` and `parentId`, which allows in-place branching without creating multiple files.

### Management

```
Storage:  ~/.pi/agent/sessions/<project-dir>/
Format:   JSONL (line-delimited JSON)
Auto-save: Yes, after every turn
```

```bash
pi -c              # Continue most recent session
pi -r              # Browse and select a past session
pi --no-session    # Ephemeral mode (don't save anything)
pi --name "task"   # Name your session
pi --session <id>  # Load a specific session
pi --fork <id>     # Fork a session
```

### Branching with /tree

`/tree` is Pi's superpower — it lets you navigate your session history like a version control system:

```
● [current] Implement login feature
├─○ Add tests for login
├─○ Fix edge case in validation
│  └─○ (current) Refactor validation
└─○ Update documentation
```

**Tree Navigation:**
- **Type** to search entries
- **Ctrl+← / Ctrl+→** (or Alt+←/Alt+→) to jump between branches
- **← / →** to page through entries
- **Ctrl+O** to cycle filter modes (default → no-tools → user-only → labeled-only → all)
- **Shift+L** to label entries as bookmarks
- **Shift+T** to toggle label timestamps

Select any previous point, continue from there, and switch between branches — all history is preserved in a single file.

### Forking & Cloning

- **`/fork`** — Creates a new session file from a previous user message. Select a point in history, modify the prompt, and start fresh.
- **`/clone`** — Duplicates the current active branch into a new session file. The new session keeps full history up to that point.
- **`--fork <path|id>`** — Fork a session directly from the CLI.

### Compaction

Long sessions can exhaust context windows. Compaction solves this by summarizing older messages while keeping recent ones intact.

**Manual:**
```bash
/compact                          # Default compaction
/compact "Focus on error handling"  # Custom instructions
```

**Automatic:** Enabled by default. Triggers on context overflow (recovers and retries) or when approaching the limit (proactive).

**What happens:**
1. Older messages are summarized into a compact form
2. Recent messages (configurable, default 20K tokens) are kept verbatim
3. Full history remains in the JSONL file — use `/tree` to revisit
4. Customize via settings or extensions

---

## Customization

Pi's superpower is its extensibility. Here's how to customize every aspect:

### 🧩 Extensions

Extensions are TypeScript modules that add:
- Custom tools (callable by the LLM)
- Event handlers (intercept tool calls, modify messages, etc.)
- Custom commands (like `/mycommand`)
- UI components (widgets, status bars, custom editors)
- Keyboard shortcuts
- Custom providers

**Example — a simple "greet" tool:**

```typescript
// ~/.pi/agent/extensions/greet.ts
import type { ExtensionAPI } from "@earendil-works/pi-coding-agent";
import { Type } from "typebox";

export default function (pi: ExtensionAPI) {
  pi.registerTool({
    name: "greet",
    label: "Greet",
    description: "Greet someone by name",
    parameters: Type.Object({
      name: Type.String({ description: "Name to greet" }),
    }),
    async execute(toolCallId, params, signal, onUpdate, ctx) {
      return {
        content: [{ type: "text", text: `Hello, ${params.name}! 🌟` }],
        details: {},
      };
    },
  });
}
```

**Key capabilities:**
| Capability | Description |
|------------|-------------|
| `pi.registerTool()` | Register a tool the LLM can call |
| `pi.registerCommand()` | Register a `/command` |
| `pi.registerShortcut()` | Register a keyboard shortcut |
| `pi.on(event, handler)` | Subscribe to lifecycle events |
| `pi.registerProvider()` | Add a custom AI provider |
| `pi.sendMessage()` | Inject messages into the session |
| `pi.appendEntry()` | Persist extension state across restarts |
| `ctx.ui` | Interact with user (confirm, select, input, notify) |

**Event Lifecycle:**
```
pi starts
  ├─► project_trust
  ├─► session_start
  ├─► resources_discover
  │
user sends prompt
  ├─► input (can intercept/transform)
  ├─► before_agent_start (inject messages, modify system prompt)
  ├─► agent_start
  │   ┌── turn loop ──┐
  │   ├─► turn_start
  │   ├─► context (modify messages)
  │   ├─► before_provider_request
  │   ├─► tool_call (can block)
  │   ├─► tool_result (can modify)
  │   └─► turn_end
  └─► agent_end
```

**Placement:**
- Global: `~/.pi/agent/extensions/*.ts` (or `*/index.ts`)
- Project: `.pi/extensions/*.ts` (only after project trust)
- Packages: via Pi Packages
- CLI: `pi -e ./my-ext.ts`

See the [extensions documentation](https://github.com/earendil-works/pi/blob/main/docs/extensions.md) for the complete API reference.

### 📋 Skills

Skills are Markdown-based capability packages following the [Agent Skills standard](https://agentskills.io). They teach the model how to perform specific tasks.

**Example — a Docker skill:**

```markdown
<!-- ~/.pi/agent/skills/docker/SKILL.md -->
# Docker Commands
Use this skill when the user asks about Docker operations.

## Steps
1. Check if Docker is running: `docker info`
2. List containers: `docker ps -a`
3. Build an image: `docker build -t <name> .
4. Run a container: `docker run -d --name <name> <image>
```

**Invocation:**
- Type `/skill:docker` in the editor
- Or let the agent auto-load the skill when relevant

**Placement:**
- `~/.pi/agent/skills/` (global)
- `.pi/skills/` (project, after trust)
- `~/.agents/skills/` (global, Agent Skills standard location)
- Or in a Pi Package

### 📝 Prompt Templates

Reusable prompts as Markdown files. Type `/name` to expand.

**Example — a code review template:**

```markdown
<!-- ~/.pi/agent/prompts/review.md -->
Review this code for:
- Bugs and logic errors
- Security vulnerabilities
- Performance bottlenecks
- Code style issues

Focus on: {{focus}}
```

```
/review → expands to the template content
/review security → passes "security" as {{focus}}
```

**Placement:**
- `~/.pi/agent/prompts/` (global)
- `.pi/prompts/` (project)
- Or in a Pi Package

### 🎨 Themes

Custom color themes for the TUI. Themes **hot-reload** — modify the file and Pi applies changes immediately.

**Example — a custom theme:**

```json
{
  "name": "my-theme",
  "type": "dark",
  "colors": {
    "background": "#1a1b26",
    "foreground": "#a9b1d6",
    "primary": "#7aa2f7",
    "secondary": "#bb9af7",
    "success": "#9ece6a",
    "warning": "#e0af68",
    "error": "#f7768e",
    "info": "#7dcfff",
    "border": "#3b4261",
    "selection": "#2f3a60"
  }
}
```

**Built-in themes:** `dark`, `light`

**Placement:**
- `~/.pi/agent/themes/` (global)
- `.pi/themes/` (project)
- Or in a Pi Package

### 📦 Pi Packages

Bundle and share extensions, skills, prompts, and themes via npm or git.

**Package structure:**
```
my-pi-tools/
├── package.json
├── extensions/
│   └── my-tool.ts
├── skills/
│   └── my-skill/
│       └── SKILL.md
└── prompts/
    └── review.md
```

**package.json:**
```json
{
  "name": "my-pi-tools",
  "keywords": ["pi-package"],
  "pi": {
    "extensions": ["./extensions"],
    "skills": ["./skills"],
    "prompts": ["./prompts"],
    "themes": ["./themes"]
  }
}
```

**Install & manage:**
```bash
pi install npm:@foo/pi-tools
pi install git:github.com/user/repo@v1
pi remove npm:@foo/pi-tools
pi list
pi config                   # Enable/disable resources
```

---

## Settings

Pi uses JSON settings with global and project-level scoping:

| Location | Scope |
|----------|-------|
| `~/.pi/agent/settings.json` | Global (all projects) |
| `.pi/settings.json` | Project (overrides global) |

### Key Settings

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `defaultProvider` | string | — | Default provider name |
| `defaultModel` | string | — | Default model ID |
| `defaultThinkingLevel` | string | — | `off`, `minimal`, `low`, `medium`, `high`, `xhigh` |
| `theme` | string | `"dark"` | Theme name |
| `compaction.enabled` | boolean | `true` | Enable auto-compaction |
| `compaction.keepRecentTokens` | number | `20000` | Recent tokens to preserve |
| `retry.enabled` | boolean | `true` | Automatic retry on errors |
| `steeringMode` | string | `"one-at-a-time"` | How steering messages are sent |
| `transport` | string | `"auto"` | Provider transport (`sse`, `websocket`, `auto`) |

**Example:**
```json
{
  "defaultProvider": "anthropic",
  "defaultModel": "claude-sonnet-4-20250514",
  "defaultThinkingLevel": "medium",
  "theme": "dark",
  "compaction": {
    "enabled": true,
    "reserveTokens": 16384,
    "keepRecentTokens": 20000
  },
  "retry": {
    "enabled": true,
    "maxRetries": 3
  },
  "enabledModels": ["claude-*", "gpt-4o"]
}
```

Use `/settings` in interactive mode to modify common options.

---

## Programmatic Usage

### SDK

Pi provides a TypeScript SDK for embedding in your own applications:

```typescript
import {
  AuthStorage,
  createAgentSession,
  ModelRegistry,
  SessionManager,
} from "@earendil-works/pi-coding-agent";

const authStorage = AuthStorage.create();
const modelRegistry = ModelRegistry.create(authStorage);
const { session } = await createAgentSession({
  sessionManager: SessionManager.inMemory(),
  authStorage,
  modelRegistry,
});

await session.prompt("What files are in the current directory?");
```

For advanced multi-session runtime replacement, use `createAgentSessionRuntime()` and `AgentSessionRuntime`.

### RPC Mode

For non-Node.js integrations, Pi speaks a JSONL-based RPC protocol over stdin/stdout:

```bash
pi --mode rpc
```

**Protocol:** Strict LF-delimited JSONL. Clients must split records on `\n` only.

See the [RPC documentation](https://github.com/earendil-works/pi/blob/main/docs/rpc.md) for the full protocol specification.

---

## CLI Reference

### Basic Usage

```bash
pi [options] [@files...] [messages...]
```

### Modes

| Flag | Description |
|------|-------------|
| *(default)* | Interactive TUI mode |
| `-p`, `--print` | Print response and exit |
| `--mode json` | JSON event stream (line-delimited) |
| `--mode rpc` | RPC mode for process integration |
| `--export <in> [out]` | Export session to HTML |

### Model Options

| Option | Description |
|--------|-------------|
| `--provider <name>` | Provider (anthropic, openai, google, etc.) |
| `--model <pattern>` | Model ID or pattern (supports `provider/id` and `:<thinking>`) |
| `--api-key <key>` | API key (overrides env vars) |
| `--thinking <level>` | `off`, `minimal`, `low`, `medium`, `high`, `xhigh` |
| `--models <patterns>` | Comma-separated patterns for Ctrl+P cycling |
| `--list-models [search]` | List available models |

### Session Options

| Option | Description |
|--------|-------------|
| `-c`, `--continue` | Continue most recent session |
| `-r`, `--resume` | Browse and select session |
| `--session <path\|id>` | Use specific session file or partial UUID |
| `--fork <path\|id>` | Fork a session into a new session |
| `--no-session` | Ephemeral mode (don't save) |
| `--name <name>` | Set session display name |

### Tool Options

| Option | Description |
|--------|-------------|
| `--tools <list>` | Allowlist specific tool names |
| `--exclude-tools <list>` | Disable specific tool names |
| `--no-builtin-tools` | Disable built-in tools |
| `--no-tools` | Disable all tools |

Built-in tools: `read`, `bash`, `edit`, `write`, `grep`, `find`, `ls`

### Resource Options

| Option | Description |
|--------|-------------|
| `-e`, `--extension <source>` | Load extension (repeatable) |
| `--no-extensions` | Disable extension discovery |
| `--skill <path>` | Load skill (repeatable) |
| `--no-skills` | Disable skill discovery |
| `--theme <path>` | Load theme (repeatable) |
| `--no-themes` | Disable theme discovery |
| `--no-context-files` | Disable AGENTS.md/CLAUDE.md loading |
| `--system-prompt <text>` | Replace default system prompt |
| `--append-system-prompt <text>` | Append to system prompt |

### Other Options

| Option | Description |
|--------|-------------|
| `--verbose` | Force verbose startup |
| `--approve` / `-a` | Trust project-local files for this run |
| `--no-approve` / `-na` | Ignore project-local files |
| `--offline` | Disable all network operations at startup |
| `--help` / `-h` | Show help |
| `--version` / `-v` | Show version |

### Environment Variables

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_API_KEY` | Anthropic API key |
| `OPENAI_API_KEY` | OpenAI API key |
| `GEMINI_API_KEY` | Google Gemini API key |
| `PI_CODING_AGENT_DIR` | Override config directory (default: `~/.pi/agent`) |
| `PI_CODING_AGENT_SESSION_DIR` | Override session directory |
| `PI_OFFLINE` | Disable startup network operations |
| `PI_SKIP_VERSION_CHECK` | Skip version check |
| `PI_TELEMETRY` | Override telemetry (`1`/`0`) |
| `PI_CACHE_RETENTION` | Extended prompt cache (`long`) |
| `VISUAL`, `EDITOR` | External editor for Ctrl+G |

---

## Philosophy

Pi is built on a simple belief: **you should adapt your tools to your workflow, not the other way around.**

Most coding agents come with a mountain of built-in features — permission popups, plan modes, MCP, sub-agents, to-do lists, background bash — that dictate *how* you should work. Pi takes the opposite approach:

- **Minimal core** — Only the essentials: read, write, edit, bash, sessions
- **Everything is an extension** — Features like MCP, sub-agents, plan mode, permission gates, git checkpoints, custom compaction — all built with extensions
- **Composable** — Mix and match extensions, skills, prompt templates, and themes to create your perfect workflow
- **Shareable** — Package your customizations as Pi Packages and share them with the community via npm or git

> *"Don't fork Pi to change its behavior. Extend it."*

---

## Tips & Tricks

### ⚡ Productivity

- **Session naming** — Use `--name "fix login bug"` to keep sessions organized
- **Quick one-shots** — `pi -p "Explain this function"` for instant answers
- **File context** — `pi @error.log "What caused this error?"` to include files
- **Piped input** — `git diff | pi -p "Review these changes"`
- **Image analysis** — Paste screenshots with Ctrl+V and ask Pi to analyze them
- **@ references** — Type `@` in the editor to fuzzy-find and include project files

### 🛠️ Development Workflow

- **Extensions first** — Before asking Pi for a feature, ask it to build the extension
- **Skills for repetitive tasks** — Create skills for common workflows (deploy, test, lint)
- **Prompt templates for reviews** — `review` template for code reviews, `debug` for debugging
- **Branch freely** — Use `/tree` to experiment without fear; every branch is preserved
- **Compact strategically** — Manually compact with `/compact "project overview"` for better summaries

### 🔒 Security

- Use `--tools read,grep,find,ls` for read-only sessions
- Build permission gates with extensions for dangerous commands
- Run untrusted projects in containers
- Review third-party extensions and skills before installing

### 🎨 Customization

- **Hot-reload themes** — Edit your theme file and Pi applies changes instantly
- **Custom keybindings** — `~/.pi/agent/keybindings.json` lets you remap everything
- **Project config** — Each project can have its own `.pi/settings.json`
- **Global context** — Put shared instructions in `~/.pi/agent/AGENTS.md`

---

## FAQ

### General

**Q: What's the difference between Pi and Claude Code / Aider?**
> Pi is minimal by default. It doesn't have MCP, sub-agents, plan mode, or permission popups built-in — you add them via extensions if you want them. Pi also has more providers (30+) and a rich extension ecosystem.

**Q: Is Pi free?**
> Pi itself is free and open source (MIT). You pay for the AI model usage through your provider (Anthropic, OpenAI, etc.).

**Q: Does Pi collect telemetry?**
> Pi sends an anonymous version ping on first install and after updates. This is optional and can be disabled with `PI_TELEMETRY=0` or `enableInstallTelemetry: false` in settings.

### Technical

**Q: Which model should I use?**
> Claude Sonnet 4 is a great all-rounder. For complex reasoning, use Claude Opus or OpenAI o-series with high thinking. For quick tasks, use Groq or Gemini.

**Q: How do I add a custom provider?**
> Add it via `~/.pi/agent/models.json` for OpenAI/Anthropic/Google-compatible APIs, or build an extension with `pi.registerProvider()`.

**Q: Can I use Pi in CI/CD?**
> Yes! Use `-p` for one-shot responses, `--mode json` for event streaming, or `--mode rpc` for full process integration.

**Q: How do I share my session?**
> Use `/share` to upload as a private GitHub gist, or `/export` to save as an HTML file.

**Q: Can I use Pi without a terminal?**
> Use `--mode rpc` or the SDK to embed Pi in your own applications.

### Troubleshooting

**Q: Pi says "no tool-capable model found"**
> Make sure your API key is set and the provider supports tool calling. Try `pi --list-models` to see available models.

**Q: My session is getting too long**
> Use `/compact` to summarize older messages. Auto-compaction is enabled by default.

**Q: An extension isn't loading**
> Check the file is in the right location. Use `pi --verbose` to see startup logs. Run `/reload` after adding extensions.

---

## Resources

- **📖 Official Docs:** [github.com/earendil-works/pi](https://github.com/earendil-works/pi)
- **📦 npm Package:** [`@earendil-works/pi-coding-agent`](https://www.npmjs.com/package/@earendil-works/pi-coding-agent)
- **💬 Discord Community:** [Join Discord](https://discord.com/invite/3cU7Bz4UPx)
- **📺 Session Data (HF):** [badlogicgames/pi-mono](https://huggingface.co/datasets/badlogicgames/pi-mono)
- **🔧 Pi Packages on npm:** [Search "pi-package"](https://www.npmjs.com/search?q=keywords%3Api-package)
- **📝 Blog Post:** [Why Pi?](https://mariozechner.at/posts/2025-11-30-pi-coding-agent/)
- **🌐 Website:** [pi.dev](https://pi.dev)

---

## Quick Reference Card

```
┌──────────────────────────────────────────────────────────┐
│                     🥧 Pi Quick Reference                │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  START                     MANAGE                       │
│  pi              .......  Launch TUI      /new           │
│  pi "prompt"     .......  With prompt     /resume        │
│  pi -p "..."     .......  One-shot        /tree          │
│  pi -c           .......  Continue        /fork          │
│  pi -r           .......  Resume          /clone         │
│                                                          │
│  EDITOR                    CUSTOMIZE                     │
│  @file           .......  Reference file  /reload        │
│  !command        .......  Run bash        Extensions     │
│  Shift+Enter     .......  New line        Skills         │
│  Ctrl+V          .......  Paste image     Templates      │
│  Escape          .......  Cancel          Themes         │
│  Escape ×2       .......  Open /tree      Packages       │
│                                                          │
│  MODEL                     SESSION                       │
│  Ctrl+L          .......  Select model    /session       │
│  Ctrl+P          .......  Cycle models    /compact       │
│  Shift+Tab       .......  Thinking level  /export        │
│  /model          .......  Change model    /share         │
│                                                          │
│  MESSAGE QUEUE              TOOLS                        │
│  Enter (stream)  .......  Steer            read          │
│  Alt+Enter       .......  Follow-up        write         │
│  Alt+Up          .......  Retrieve         edit          │
│                                                           bash          │
│                                                           grep          │
│                                                           find          │
│                                                           ls            │
└──────────────────────────────────────────────────────────┘
```

---

> **Pi** — MIT Licensed — Made with ❤️ by the Pi Community
