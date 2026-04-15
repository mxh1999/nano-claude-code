# Recipes — Common Use Cases

Practical examples to get started with CheetahClaws after installation.

---

## 1. Code Review with a Local Ollama Model

Use a free, local model to review code without sending anything to the cloud.

```bash
# Pull a capable model
ollama pull qwen2.5-coder:14b

# Start CheetahClaws with Ollama
cheetahclaws --model ollama/qwen2.5-coder:14b
```

```
[project] » Review the code in src/api.py for security issues, performance 
             problems, and potential bugs. Be specific with line numbers.
```

For a full project audit:
```
[project] » Read all Python files in this project and give me a prioritized 
             list of the 10 most important issues to fix before shipping.
```

**Tip:** Ollama models run locally — your code never leaves your machine.

---

## 2. Remote Control via Telegram

Control CheetahClaws from your phone while it runs on your server/workstation.

**Setup (one time):**
1. Message [@BotFather](https://t.me/BotFather) on Telegram, create a bot, get the token
2. Get your chat ID from [@userinfobot](https://t.me/userinfobot)
3. Configure:
```bash
cheetahclaws
/config telegram_token=YOUR_BOT_TOKEN
/config telegram_chat_id=YOUR_CHAT_ID
/telegram start
```

**Usage from phone:**
```
You (Telegram): What files changed in the last commit?
Bot: [reads git log, shows diff summary]

You: Fix the bug in auth.py line 42
Bot: [edits file, shows diff, confirms]

You: !git status
Bot: [runs command, returns output]
```

**Tip:** Use `!command` prefix to run shell commands directly from Telegram.

---

## 3. Autonomous Research Agent

Let CheetahClaws research a topic independently while you do other work.

```
[project] » /agent
```

Select **"Research Assistant"** from the wizard, then:
```
Research topic: Compare React Server Components vs Next.js App Router 
                for a production e-commerce site

Output: Write findings to research_output.md
```

The agent will:
- Search the web for current information
- Read documentation and blog posts
- Synthesize findings into the output file
- Continue iterating until the research is complete

**Monitor progress:**
```
/agents              # see running agents
/tasks               # see task progress
```

---

## 4. Quick Bug Fix Workflow

```bash
# Start with the bug context
cheetahclaws -p "Fix the TypeError in utils.py:42 where None is passed to len()"
```

Or interactively:
```
[project] » There's a crash when users submit an empty form. The error is 
             TypeError: argument of type 'NoneType' is not iterable in 
             handlers/form.py. Find and fix it.
```

CheetahClaws will:
1. Read the file
2. Identify the root cause
3. Apply the fix
4. Show you the diff for approval

---

## 5. Multi-Model Brainstorm

Get perspectives from different models on a design decision.

```
[project] » /brainstorm

Topic: Should we use PostgreSQL or MongoDB for our user activity tracking 
       system? We expect 10M events/day with complex aggregation queries.
```

The brainstorm spawns multiple sub-agents that discuss and debate, then synthesizes a final recommendation.

---

## 6. Session Persistence Across Days

Work on a long-running project across multiple sessions:

```bash
# Day 1: Start working
cheetahclaws
[project] » Let's refactor the authentication module. Start by analyzing 
             the current auth flow...
# ... work happens ...
# Ctrl+D to exit (auto-saves)

# Day 2: Resume where you left off
cheetahclaws
[project] » /resume
# Your full conversation context is restored
[project] » Continue with the auth refactor. What's left?
```

**Tip:** Use `/save my-refactor` to name a session for easy retrieval later with `/load my-refactor`.

---

## 7. Monitoring AI Research Papers

Stay updated on topics that matter to you:

```
[project] » /monitor
```

Select **"Add subscription"**, then:
```
Topic: ai_research
Schedule: daily
Notification: --telegram
```

Every day, CheetahClaws will:
- Fetch the latest papers from arXiv
- Summarize the most relevant ones
- Send you a digest via Telegram

Other subscription types: `stock_TSLA`, `crypto_BTC`, `world_news`, `custom:<query>`

---

## 8. Project Bootstrap with /init

Start a new project with AI-readable context:

```bash
mkdir my-new-project && cd my-new-project
git init
cheetahclaws
[my-new-project] » /init
```

This creates a `CLAUDE.md` file that CheetahClaws reads on every startup — containing project conventions, tech stack, and guidelines that shape all future interactions.

---

## Tips

- **`/status`** — quick overview: model, token usage, cost, session stats
- **`/doctor`** — diagnose connectivity, dependencies, and configuration issues
- **`/compact`** — manually compress conversation when context gets large
- **`/copy`** — copy the last response to clipboard
- **`/export`** — export the full conversation to a Markdown file
- **`Ctrl+C`** — interrupt a long response without losing conversation
- **`!command`** — run a shell command inline (e.g., `!git status`)
