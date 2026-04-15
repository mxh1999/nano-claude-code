# Reference — CLI, Commands, Tools, and Configuration

## CLI Reference

```
cheetahclaws [OPTIONS] [PROMPT]
# or: python cheetahclaws.py [OPTIONS] [PROMPT]

Options:
  -p, --print          Non-interactive: run prompt and exit
  -m, --model MODEL    Override model (e.g. gpt-4o, ollama/llama3.3)
  --accept-all         Auto-approve all operations (no permission prompts)
  --verbose            Show thinking blocks and per-turn token counts
  --thinking           Enable Extended Thinking (Claude only)
  --version            Print version and exit
  -h, --help           Show help
```

**Examples:**

```bash
# Interactive REPL with default model
cheetahclaws

# Switch model at startup
cheetahclaws --model gpt-4o
cheetahclaws -m ollama/deepseek-r1:32b

# Non-interactive / scripting
cheetahclaws --print "Write a Python fibonacci function"
cheetahclaws -p "Explain the Rust borrow checker in 3 sentences" -m gemini/gemini-2.0-flash

# CI / automation (no permission prompts)
cheetahclaws --accept-all --print "Initialize a Python project with pyproject.toml"

# Debug mode (see tokens + thinking)
cheetahclaws --thinking --verbose
```

---

## Slash Commands (REPL)

Type `/` and press **Tab** to see all commands with descriptions. Continue typing to filter, then Tab again to auto-complete. After a command name, press **Tab** again to see its subcommands (e.g. `/plugin ` → `install`, `uninstall`, `enable`, …).

| Command | Description |
|---|---|
| `/help` | Show all commands |
| `/clear` | Clear conversation history |
| `/model` | Show current model + list all available models |
| `/model <name>` | Switch model (takes effect immediately) |
| `/config` | Show all current config values |
| `/config key=value` | Set a config value (persisted to disk) |
| `/save` | Save session (auto-named by timestamp) |
| `/save <filename>` | Save session to named file |
| `/load` | Interactive list grouped by date; enter number, `1,2,3` to merge, or `H` for full history |
| `/load <filename>` | Load a saved session by filename |
| `/resume` | Restore the last auto-saved session (`mr_sessions/session_latest.json`) |
| `/resume <filename>` | Load a specific file from `mr_sessions/` (or absolute path) |
| `/history` | Print full conversation history |
| `/context` | Show message count and token estimate |
| `/cost` | Show token usage and estimated USD cost |
| `/verbose` | Toggle verbose mode (tokens + thinking) |
| `/thinking` | Toggle Extended Thinking (Claude only) |
| `/permissions` | Show current permission mode |
| `/permissions <mode>` | Set permission mode: `auto` / `accept-all` / `manual` |
| `/cwd` | Show current working directory |
| `/cwd <path>` | Change working directory |
| `/memory` | List all persistent memories |
| `/memory <query>` | Search memories by keyword (ranked by confidence × recency) |
| `/memory consolidate` | AI-extract up to 3 long-term insights from the current session |
| `/skills` | List available skills |
| `/agents` | Show sub-agent task status |
| `/mcp` | List configured MCP servers and their tools |
| `/mcp reload` | Reconnect all MCP servers and refresh tools |
| `/mcp reload <name>` | Reconnect a single MCP server |
| `/mcp add <name> <cmd> [args]` | Add a stdio MCP server to user config |
| `/mcp remove <name>` | Remove a server from user config |
| `/voice` | Record voice, transcribe with Whisper, auto-submit as prompt |
| `/voice status` | Show recording and STT backend availability |
| `/voice lang <code>` | Set STT language (e.g. `zh`, `en`, `ja`; `auto` to detect) |
| `/voice device` | List available input microphones and select one interactively |
| `/image [prompt]` | Capture clipboard image and send to vision model with optional prompt |
| `/img [prompt]` | Alias for `/image` |
| `/proactive` | Show current proactive polling status (ON/OFF and interval) |
| `/proactive <duration>` | Enable background sentinel polling (e.g. `5m`, `30s`, `1h`) |
| `/proactive off` | Disable background polling |
| `/cloudsave setup <token>` | Configure GitHub Personal Access Token for Gist sync |
| `/cloudsave` | Upload current session to a private GitHub Gist |
| `/cloudsave push [desc]` | Upload with an optional description |
| `/cloudsave auto on\|off` | Toggle auto-upload on `/exit` |
| `/cloudsave list` | List your cheetahclaws Gists |
| `/cloudsave load <gist_id>` | Download and restore a session from Gist |
| `/brainstorm` | Run a multi-persona AI brainstorm; prompts for agent count (2–100, default 5) |
| `/brainstorm <topic>` | Focus the brainstorm on a specific topic; prompts for agent count |
| `/ssj` | Open SSJ Developer Mode — interactive power menu with 14 workflow shortcuts |
| `/monitor` | Interactive wizard: add subscriptions, run now, start/stop scheduler, configure notifications |
| `/monitor run [topic]` | Run all (or one) subscription(s) immediately and print the AI report |
| `/monitor start` | Start the background scheduler daemon |
| `/monitor stop` | Stop the background scheduler daemon |
| `/monitor status` | Show scheduler status, subscriptions, and configured delivery channels |
| `/monitor set telegram <token> <chat_id>` | Configure Telegram delivery for monitor reports |
| `/monitor set slack <token> <channel_id>` | Configure Slack delivery for monitor reports |
| `/monitor topics` | List all built-in topics |
| `/subscribe <topic> [schedule] [--telegram] [--slack]` | Subscribe to a monitoring topic (e.g. `ai_research`, `stock_TSLA`, `crypto_BTC`, `world_news`, `custom:quantum computing`) |
| `/subscriptions` | List active subscriptions with schedule and last-run time |
| `/subs` | Alias for `/subscriptions` |
| `/unsubscribe <topic>` | Remove a subscription |
| `/agent` | Interactive wizard: choose template, answer questions, start background agent loop |
| `/agent start <template> [args]` | Direct launch — e.g. `/agent start research_assistant ~/papers/` |
| `/agent stop <name\|all>` | Stop a running agent (or all agents) |
| `/agent list` | Show all currently running agents and their status |
| `/agent status <name>` | Show recent iteration log for a named agent |
| `/agent templates` | List available templates (built-in + user-defined) |
| `/worker` | Auto-implement all pending tasks from `brainstorm_outputs/todo_list.txt` |
| `/worker <n,m,…>` | Implement specific pending tasks by number (e.g. `/worker 1,4,6`) |
| `/worker --path <file>` | Use a custom todo file path instead of the default |
| `/worker --workers <n>` | Limit the batch to N tasks per run (e.g. `/worker --workers 3`) |
| `/telegram <token> <chat_id>` | Configure and start the Telegram bot bridge |
| `/telegram` | Start the bridge using previously saved token + chat_id |
| `/telegram stop` | Stop the Telegram bridge |
| `/telegram status` | Show whether the bridge is running and the configured chat_id |
| `/wechat login` | Scan QR code with WeChat to authenticate, then start the bridge |
| `/wechat` | Start with saved credentials; triggers QR login if none saved |
| `/wechat stop` | Stop the WeChat bridge |
| `/wechat status` | Show running state and account info |
| `/wechat logout` | Clear saved credentials and stop the bridge |
| `/slack <token> <channel_id>` | Configure and start the Slack bridge |
| `/slack` | Start with saved credentials |
| `/slack stop` | Stop the Slack bridge |
| `/slack status` | Show running state and channel |
| `/slack logout` | Clear saved credentials and stop the bridge |
| `/video [topic]` | AI video factory: story → voice → images → subtitles → `.mp4` |
| `/video status` | Show video pipeline dependency availability |
| `/video niches` | List all 10 viral content niches |
| `/video --niche <id> [topic]` | Use a specific content niche |
| `/video --short [topic]` | Generate vertical short format (9:16) |
| `/tts [topic]` | TTS Content Factory: AI script → any voice style → MP3 audio file |
| `/tts status` | Show TTS dependency availability (ffmpeg, edge-tts, API keys) |
| `/checkpoint` | List all checkpoints (snapshots) for the current session |
| `/checkpoint <id>` | Rewind to checkpoint — restore files and conversation to that snapshot |
| `/checkpoint clear` | Delete all checkpoints for the current session |
| `/rewind` | Alias for `/checkpoint` |
| `/plan <description>` | Enter plan mode: read-only analysis, writes only to the plan file |
| `/plan` | Show current plan file contents |
| `/plan done` | Exit plan mode and restore original permissions |
| `/plan status` | Show whether plan mode is active |
| `/compact` | Manually compact the conversation (same as auto-compact but user-triggered) |
| `/compact <focus>` | Compact with focus instructions (e.g. `/compact keep the auth refactor context`) |
| `/init` | Create a `CLAUDE.md` template in the current working directory |
| `/export` | Export the conversation as a Markdown file to `.nano_claude/exports/` |
| `/export <filename>` | Export as Markdown or JSON (detected by `.json` extension) |
| `/copy` | Copy the last assistant response to the clipboard |
| `/status` | Show version, model, provider, permissions, session ID, token usage, and context % |
| `/doctor` | Diagnose installation health: Python, git, API key, optional deps, CLAUDE.md, checkpoint disk usage |
| `/exit` / `/quit` | Exit |

**Switching models inside a session:**

<div align=center>
<img src="https://github.com/SafeRL-Lab/cheetahclaws/blob/main/docs/multimodel_demo.gif" width="850"/>
</div>
<div align=center>
<center style="color:#000000;text-decoration:underline">Multi-Model Switching: Claude → GPT-4o → Ollama → back, full history preserved</center>
</div>

```
[myproject] ❯ /model
  Current model: claude-opus-4-6  (provider: anthropic)

  Available models by provider:
    anthropic     claude-opus-4-6, claude-sonnet-4-6, ...
    openai        gpt-4o, gpt-4o-mini, o3-mini, ...
    ollama        llama3.3, llama3.2, phi4, mistral, ...
    ...

[myproject] ❯ /model gpt-4o
  Model set to gpt-4o  (provider: openai)

[myproject] ❯ /model ollama/qwen2.5-coder
  Model set to ollama/qwen2.5-coder  (provider: ollama)
```

---

## Configuring API Keys

### Method 1: Environment Variables (recommended)

```bash
# Add to ~/.bashrc or ~/.zshrc
export ANTHROPIC_API_KEY=sk-ant-...
export OPENAI_API_KEY=sk-...
export GEMINI_API_KEY=AIza...
export MOONSHOT_API_KEY=sk-...       # Kimi
export DASHSCOPE_API_KEY=sk-...      # Qwen
export ZHIPU_API_KEY=...             # Zhipu GLM
export DEEPSEEK_API_KEY=sk-...       # DeepSeek
export MINIMAX_API_KEY=...           # MiniMax
```

### Method 2: Set Inside the REPL (persisted)

```
/config anthropic_api_key=sk-ant-...
/config openai_api_key=sk-...
/config gemini_api_key=AIza...
/config kimi_api_key=sk-...
/config qwen_api_key=sk-...
/config zhipu_api_key=...
/config deepseek_api_key=sk-...
/config minimax_api_key=...
```

Keys are saved to `~/.cheetahclaws/config.json` and loaded automatically on next launch.

### Method 3: Edit the Config File Directly

```json
// ~/.cheetahclaws/config.json
{
  "model": "qwen/qwen-max",
  "max_tokens": 8192,
  "permission_mode": "auto",
  "verbose": false,
  "thinking": false,
  "qwen_api_key": "sk-...",
  "kimi_api_key": "sk-...",
  "deepseek_api_key": "sk-...",
  "minimax_api_key": "..."
}
```

---

## Permission System

| Mode | Behavior |
|---|---|
| `auto` (default) | Read-only operations always allowed. Prompts before Bash commands and file writes. |
| `accept-all` | Never prompts. All operations proceed automatically. |
| `manual` | Prompts before every single operation, including reads. |
| `plan` | Read-only analysis mode. Only the plan file (`.nano_claude/plans/`) is writable. Entered via `/plan <desc>` or the `EnterPlanMode` tool. |

**When prompted:**

```
  Allow: Run: git commit -am "fix bug"  [y/N/a(ccept-all)]
```

- `y` — approve this one action
- `n` or Enter — deny
- `a` — approve and switch to `accept-all` for the rest of the session

**Commands always auto-approved in `auto` mode:**
`ls`, `cat`, `head`, `tail`, `wc`, `pwd`, `echo`, `git status`, `git log`, `git diff`, `git show`, `find`, `grep`, `rg`, `python`, `node`, `pip show`, `npm list`, and other read-only shell commands.

---

## Built-in Tools

### Core Tools

| Tool | Description | Key Parameters |
|---|---|---|
| `Read` | Read file with line numbers | `file_path`, `limit`, `offset` |
| `Write` | Create or overwrite file (shows diff) | `file_path`, `content` |
| `Edit` | Exact string replacement (shows diff) | `file_path`, `old_string`, `new_string`, `replace_all` |
| `Bash` | Execute shell command | `command`, `timeout` (default 30s) |
| `Glob` | Find files by glob pattern | `pattern` (e.g. `**/*.py`), `path` |
| `Grep` | Regex search in files (uses ripgrep if available) | `pattern`, `path`, `glob`, `output_mode` |
| `WebFetch` | Fetch and extract text from URL | `url`, `prompt` |
| `WebSearch` | Search the web via DuckDuckGo | `query` |

### Notebook & Diagnostics Tools

| Tool | Description | Key Parameters |
|---|---|---|
| `NotebookEdit` | Edit a Jupyter notebook (`.ipynb`) cell | `notebook_path`, `new_source`, `cell_id`, `cell_type`, `edit_mode` (`replace`/`insert`/`delete`) |
| `GetDiagnostics` | Get LSP-style diagnostics for a source file (pyright/mypy/flake8 for Python; tsc/eslint for JS/TS; shellcheck for shell) | `file_path`, `language` (optional override) |

### Memory Tools

| Tool | Description | Key Parameters |
|---|---|---|
| `MemorySave` | Save or update a persistent memory | `name`, `type`, `description`, `content`, `scope` |
| `MemoryDelete` | Delete a memory by name | `name`, `scope` |
| `MemorySearch` | Search memories by keyword (or AI ranking) | `query`, `scope`, `use_ai`, `max_results` |
| `MemoryList` | List all memories with age and metadata | `scope` |

### Sub-Agent Tools

| Tool | Description | Key Parameters |
|---|---|---|
| `Agent` | Spawn a sub-agent for a task | `prompt`, `subagent_type`, `isolation`, `name`, `model`, `wait` |
| `SendMessage` | Send a message to a named background agent | `name`, `message` |
| `CheckAgentResult` | Check status/result of a background agent | `task_id` |
| `ListAgentTasks` | List all active and finished agent tasks | — |
| `ListAgentTypes` | List available agent type definitions | — |

### Background & Autonomy Tools

| Tool | Description | Key Parameters |
|---|---|---|
| `SleepTimer` | Schedule a silent background timer; injects an automated wake-up prompt when it fires so the agent can resume monitoring or deferred tasks | `seconds` |

### Skill Tools

| Tool | Description | Key Parameters |
|---|---|---|
| `Skill` | Invoke a skill by name from within the conversation | `name`, `args` |
| `SkillList` | List all available skills with triggers and metadata | — |

### MCP Tools

MCP tools are discovered automatically from configured servers and registered under the name `mcp__<server>__<tool>`. Claude can use them exactly like built-in tools.

| Example tool name | Where it comes from |
|---|---|
| `mcp__git__git_status` | `git` server, `git_status` tool |
| `mcp__filesystem__read_file` | `filesystem` server, `read_file` tool |
| `mcp__myserver__my_action` | custom server you configured |

> **Adding custom tools:** See [Architecture Guide](docs/architecture.md#tool-registry) for how to register your own tools.

---


## AskUserQuestion Tool

Claude can pause mid-task and interactively ask you a question before proceeding.

**Example invocation by Claude:**
```json
{
  "tool": "AskUserQuestion",
  "question": "Which database should I use?",
  "options": [
    {"label": "SQLite", "description": "Simple, file-based"},
    {"label": "PostgreSQL", "description": "Full-featured, requires server"}
  ],
  "allow_freetext": true
}
```

**What you see in the terminal:**
```
❓ Question from assistant:
   Which database should I use?

  [1] SQLite — Simple, file-based
  [2] PostgreSQL — Full-featured, requires server
  [0] Type a custom answer

Your choice (number or text):
```

- Select by number or type free text directly
- Claude receives your answer and continues the task
- 5-minute timeout (returns "(no answer — timeout)" if unanswered)

---

## Task Management

The `task/` package gives Claude (and you) a structured task list for tracking multi-step work within a session.

### Tools available to Claude

| Tool | Parameters | What it does |
|------|-----------|--------------|
| `TaskCreate` | `subject`, `description`, `active_form?`, `metadata?` | Create a task; returns `#id created: subject` |
| `TaskUpdate` | `task_id`, `subject?`, `description?`, `status?`, `owner?`, `add_blocks?`, `add_blocked_by?`, `metadata?` | Update any field; `status='deleted'` removes the task |
| `TaskGet` | `task_id` | Return full details of one task |
| `TaskList` | _(none)_ | List all tasks with status icons and pending blockers |

**Valid statuses:** `pending` → `in_progress` → `completed` / `cancelled` / `deleted`

### Dependency edges

```
TaskUpdate(task_id="3", add_blocked_by=["1","2"])
# Task 3 is now blocked by tasks 1 and 2.
# Reverse edges are set automatically: tasks 1 and 2 get task 3 in their "blocks" list.
```

Completed tasks are treated as resolved — `TaskList` hides their blocking effect on dependents.

### Persistence

Tasks are saved to `.cheetahclaws/tasks.json` in the current working directory after every mutation and reloaded on first access.

### REPL commands

```
/tasks                    list all tasks
/tasks create <subject>   quick-create a task
/tasks start <id>         mark in_progress
/tasks done <id>          mark completed
/tasks cancel <id>        mark cancelled
/tasks delete <id>        remove a task
/tasks get <id>           show full details
/tasks clear              delete all tasks
```

### Typical Claude workflow

```
User: implement the login feature

Claude:
  TaskCreate(subject="Design auth schema", description="JWT vs session")  → #1
  TaskCreate(subject="Write login endpoint", description="POST /auth/login") → #2
  TaskCreate(subject="Write tests", description="Unit + integration") → #3
  TaskUpdate(task_id="2", add_blocked_by=["1"])
  TaskUpdate(task_id="3", add_blocked_by=["2"])

  TaskUpdate(task_id="1", status="in_progress", active_form="Designing schema")
  ... (does the work) ...
  TaskUpdate(task_id="1", status="completed")
  TaskList()  → task 2 is now unblocked
  ...
```

---

