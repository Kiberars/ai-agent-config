# CLAUDE.md

> This file configures Claude Code behavior for this project.
> It extends the universal configuration in AGENTS.md.

## Stack
<!-- Fill in: language, framework, database, deployment -->

## Commands
- `npm run dev` — start development server
- `npm run test` — run tests
- `npm run lint` — run linter
- `npm run build` — production build

## Architecture
<!-- One-line description of the architecture -->

## Hard Rules
- Do not start coding without an approved plan (`/plan` first)
- Do not touch files outside the current task scope
- Do not add code style rules here — handled by hooks
- Do not use temporary fixes

## Skills
See `skills/SKILLS_INDEX.md` — reference skills explicitly in prompts.

## Agents
See `agents/` — activate roles explicitly:
> "Act as the Reviewer agent. Read agents/reviewer.md and review this PR."

## Full Config
See `AGENTS.md` for complete rules, workflow, and MCP configuration.
