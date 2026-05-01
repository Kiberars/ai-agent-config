# AI Agent Configuration

Universal configuration repository for AI coding agents (Claude Code, Codex, Qwen, Gemini CLI, Cursor, Copilot, etc.).

> **How to use:** Point your AI agent to this repository. It will read rules, roles, skills, and workflow automatically.

---

## Quick Reference

| What | Where |
|---|---|
| Roles / Agents | `agents/` |
| Commands & Workflow | `workflows/commands.md` |
| Skills | `skills/SKILLS_INDEX.md` |
| MCP Servers | `mcp/README.md` |
| Quality Gates | `quality/` |
| Project Template | `templates/PROJECT_CONSTITUTION.template.md` |

---

## Core Principles

1. **Minimalism** — every change is as small as possible. Deleting lines is better than adding.
2. **Root cause, not symptom** — no temporary fixes, only root cause resolution.
3. **Precision** — touch only what is required. No side effects.
4. **Plan before coding** — never start implementation without an approved plan.
5. **Verify, don't assume** — if uncertain, ask. Surface tradeoffs explicitly.

---

## Hard Rules

- Do not start implementation without a plan approved by the user.
- Do not add features beyond what was explicitly requested.
- Do not refactor code that is not part of the current task.
- Do not write code style rules — use linters (deterministic, reliable).
- Do not leave TODOs without a linked task.
- Do not use temporary fixes (`# type: ignore`, `any`, `pass`).

---

## Agent Workflow

```
1. Read PROJECT_CONSTITUTION.md (if present in project root)
2. Read AGENTS.md (this file)
3. Check SKILLS_INDEX.md for relevant skills
4. Plan → get approval → implement → verify
```

### Standard Commands

| Command | Action |
|---|---|
| `/plan` | Create implementation plan, wait for approval |
| `/code` | Implement approved plan |
| `/review` | Code review |
| `/fix` | Find and fix errors (root cause only) |
| `/deploy` | Prepare for deployment |
| `/update-rules` | Update AGENTS.md based on last mistake |
| `/status` | Project status summary |
| `/explore` | Analyze repository structure |
| `/clear` | Start fresh session (use before each new task) |

---

## Context Compression

- Use `/clear` before each new task — conversation history is not needed.
- Everything the agent needs is in `AGENTS.md` and the codebase.
- Keep files under 800 lines — split into modules with `index.md` if larger.

---

## Roles

See `agents/` directory. Activate a role explicitly:

> "Act as the Architect agent. Read `agents/architect.md` and design the solution."

---

## Skills

Skills are activated by keywords in the task description, or explicitly:

> "Apply the `parsing` skill. Read `skills/parsing/SKILL.md`."

See full index: `skills/SKILLS_INDEX.md`

---

## Quality Gates

All quality checks run automatically via pre-commit hooks.
See `quality/.pre-commit-config.yaml` for full configuration.

Claude Code hooks: `quality/hooks/settings.json`

---

## AES Compliance Levels

| Level | Criteria |
|---|---|
| L1 | PROJECT_CONSTITUTION.md defined |
| L2 | Implementation plan exists and approved |
| L3 | Architecture is being followed |
| L4 | Production ready |

Agent must not advance to L2 without L1 being complete.
