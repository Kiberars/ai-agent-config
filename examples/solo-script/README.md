# Example: Solo Script / Minimal Config

For small scripts and one-off tools, you don't need the full setup.
Minimum viable config:

---

## Minimal CLAUDE.md (for a script)

```markdown
# CLAUDE.md

## What this is
Python script that parses HH.ru vacancies and exports to CSV.

## Commands
uv run python main.py       # run
uv run pytest               # tests
uv run ruff check .         # lint

## Hard Rules
- Do not add CLI arguments that weren't asked for
- Do not store API keys in code (use .env)
- Keep main.py under 200 lines — split if larger
```

---

## What to skip for small scripts

- `PROJECT_CONSTITUTION.md` — optional, skip it
- `agents/` — don't activate roles, just talk normally
- `workflows/` — skip BMAD, just use `/plan` and `/code`
- `pre-commit` — optional, but Ruff alone takes 2 minutes to set up
- MCP servers — only if you need browser automation or special tools

---

## What to keep even for small scripts

- **`/plan` before coding** — 2 minutes of planning saves 20 minutes of debugging
- **`/clear` at task start** — fresh context = sharper answers
- **`/update-rules` after mistakes** — makes future sessions smarter
- **Keep files under 800 lines** — split early, not after it's painful

---

## Prompt for a fresh script session

```
I need a Python script that [describe what it does].

Before coding:
1. Ask me any clarifying questions
2. Show me a plan (what functions, what the data flow looks like)
3. Wait for my approval
4. Then implement
```
