# AI Agent Configuration

Universal configuration for AI coding agents.
Works with: Claude Code · Codex · Cursor · Gemini CLI · GitHub Copilot · any LLM

---

## ⚡ First Time on a New Project?

Run `/init` — the agent will ask questions and fill in all configs automatically.
Takes ~3 minutes. After that, everything is ready.

---

## Quick Reference

| What                 | Where                                        |
|----------------------|----------------------------------------------|
| **Init new project** | `/init` → runs `workflows/init.md`           |
| Roles / Agents       | `agents/`                                    |
| Commands             | `workflows/commands.md`                      |
| Skills               | `skills/SKILLS_INDEX.md`                     |
| MCP Servers          | `mcp/README.md`                              |
| Quality Gates        | `quality/`                                   |
| Project Template     | `templates/PROJECT_CONSTITUTION.template.md` |

---

## Core Principles

1. **Minimalism** — every change is as small as possible. Delete > add.
2. **Root cause, not symptom** — no temporary fixes.
3. **Precision** — touch only what the task requires. No side effects.
4. **Plan before coding** — never start without an approved plan.
5. **Verify, don't assume** — surface tradeoffs explicitly.

---

## Hard Rules

- Do not start implementation without a user-approved plan.
- Do not add features beyond what was explicitly requested.
- Do not refactor code outside the current task scope.
- Do not write code style rules — use linters.
- Do not leave TODOs without a linked task ID.
- Do not use temporary fixes (`# type: ignore`, `any`, `pass`).
- Do not write to production configs without explicit user confirmation.
- Do not run destructive commands (`rm -rf`, `DROP`, `truncate`) without confirmation.

---

## Agent Workflow

```
1. Read PROJECT_CONSTITUTION.md  (if absent → run /init first)
2. Read CLAUDE.md                (project-specific overrides)
3. Check SKILLS_INDEX.md         (load relevant skills on demand)
4. /plan → get approval → /code → /review → verify
5. After task: update CHANGELOG.md, run context-snapshot if session > 30 min
```

---

## Standard Commands

| Command         | Action                                              | Output                        |
|-----------------|-----------------------------------------------------|-------------------------------|
| `/init`         | **Interview + auto-fill all project configs**       | `PROJECT_CONSTITUTION.md`, `CLAUDE.md` |
| `/plan`         | Create implementation plan, wait for approval       | `plans/YYYY-MM-DD-{task}.md`  |
| `/code`         | Implement approved plan                             | Code + updated `CHANGELOG.md` |
| `/review`       | Code review against project standards               | Inline comments + summary     |
| `/fix`          | Find and fix errors (root cause only)               | Fix + root cause explanation  |
| `/deploy`       | AES check → prepare deployment checklist            | `deploy/checklist-{date}.md`  |
| `/update-rules` | Learn from last mistake → patch `AGENTS.md`        | Diff of changes made          |
| `/status`       | Project status: AES level, open tasks, debt         | Summary table                 |
| `/explore`      | Analyse repository structure, build mental map      | Tree + key observations       |
| `/clear`        | End session. Snapshot context, flush history        | —                             |

---

## Roles

Activate explicitly: `"Act as the Architect agent. Read agents/architect.md."`

Available: `product-manager` · `architect` · `developer` · `reviewer` · `tester` · `planner` · `simplifier`

---

## Skills

Load on demand: `"Apply the parsing skill. Read skills/parsing/SKILL.md."`

See catalog: `skills/SKILLS_INDEX.md`

---

## Quality Gates

Config: `quality/.pre-commit-config.yaml`
Claude Code hooks: `quality/hooks/settings.json`

---

## AES Compliance

| Level | Gate                                                     |
|-------|----------------------------------------------------------|
| L1    | `PROJECT_CONSTITUTION.md` filled (not template)         |
| L2    | Implementation plan exists and approved                  |
| L3    | Architecture documented, ADR-000 exists                  |
| L4    | Tests pass, linters clean, `CHANGELOG.md` up to date    |

Agent must not advance to next level without completing the current one.

---

## Context Budget

- Use `/clear` before each new task — history is ballast.
- Keep all files under 800 lines.
- At > 60% context used: warn user, suggest `/clear` + continue in new session.
