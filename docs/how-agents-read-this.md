# How AI Agents Read This Repository

Understanding the reading order helps you write better prompts.

---

## Reading Order (Default)

```
1. AGENTS.md          (or CLAUDE.md for Claude Code)
      ↓
2. PROJECT_CONSTITUTION.md  (if present in project)
      ↓
3. skills/SKILLS_INDEX.md   (scan for relevant skills)
      ↓
4. Load specific skill file  (only when needed)
      ↓
5. Load specific agent file  (only when activated)
```

The agent should NOT load all files at session start — only what's needed for the current task.

---

## What Each File Does

| File | Purpose | When loaded |
|---|---|---|
| `AGENTS.md` | Rules, workflow, hard constraints | Always |
| `PROJECT_CONSTITUTION.md` | Scope, stack, architecture | Always |
| `skills/SKILLS_INDEX.md` | Skill catalog (no detail) | Always |
| `skills/*/SKILL.md` | Skill implementation | On-demand |
| `agents/*.md` | Role definitions | When role is activated |
| `workflows/*.md` | Process reference | When process is invoked |
| `mcp/README.md` | MCP setup | When configuring tools |
| `quality/*` | Linter config | Automated (not by agent) |

---

## Token Budget Strategy

Files are sized deliberately:

- `AGENTS.md` — ~150 lines (always in context)
- `PROJECT_CONSTITUTION.md` — ~100 lines (always in context)
- `SKILLS_INDEX.md` — ~60 lines (always in context)
- Each `SKILL.md` — ~100–150 lines (loaded on-demand)
- Each `agents/*.md` — ~80–120 lines (loaded on-demand)

Total base context: ~310 lines (~2500 tokens)
With one skill + one agent: ~550 lines (~4000 tokens)

This leaves plenty of room for code context in the conversation window.

---

## File Size Rule

Keep all files under **800 lines**. If a file grows past 800 lines:

1. Split into smaller modules
2. Create an `index.md` that maps what's where
3. Agent reads `index.md` first, then loads only the relevant module

This pattern drastically reduces token usage on large projects.

---

## How to Reference This Repo in a Prompt

### For Claude Code
```
CLAUDE.md is in the project root. Read it first.
```

### For other agents
```
Read AGENTS.md in this repository. It contains all rules, roles, and workflow 
instructions for working on this project.
```

### For a fresh project
```
This repository is my AI agent configuration. 
Read AGENTS.md, then read PROJECT_CONSTITUTION.md, 
then tell me the current AES level and what's needed to advance.
```

---

## Limitations

- AI agents cannot execute pre-commit hooks — these run via git
- MCP servers must be configured outside the conversation
- Claude Code hooks (`settings.json`) run outside the conversation
- Context is NOT preserved between sessions — use the context-snapshot skill
