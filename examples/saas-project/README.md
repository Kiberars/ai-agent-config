# Example: SaaS Project Config

This is a complete example of how to configure the repo for a SaaS application.

## PROJECT_CONSTITUTION.md (example)

```markdown
# PROJECT_CONSTITUTION.md

## Project Overview
**Name:** TaskFlow
**Purpose:** Lightweight project management SaaS for solo developers and small teams
**Target users:** Indie developers, small teams (2–10 people)
**Status:** In Progress

## Scope
### In scope
- User auth (email + password, JWT)
- Projects, tasks, and subtasks CRUD
- Kanban board view
- REST API + React frontend

### Out of scope
- Mobile apps (Future: v2)
- Integrations (GitHub, Slack) (Future: v2)
- Real-time collaboration (Future: v3)

## Tech Stack
| Layer | Choice | Reason |
|---|---|---|
| Language | Python 3.12 | Team familiarity |
| Framework | FastAPI | Async, auto-docs |
| Database | PostgreSQL 16 | Relational data, ACID |
| Auth | JWT (python-jose) | Stateless |
| Frontend | React + Vite | Fast iteration |
| Deployment | Railway | Simple PaaS |
| Testing | pytest | Standard |

## Architecture
Browser → React → FastAPI → PostgreSQL
                         → Redis (sessions, rate limit)

## Hard Constraints
- Do not store passwords in plaintext (use bcrypt)
- Do not log PII (email, names) in application logs
- All API routes require auth except /auth/login and /auth/register
- Database access only through SQLAlchemy ORM, never raw SQL strings
```

## CLAUDE.md (example)

```markdown
# CLAUDE.md

## Stack
Python 3.12 + FastAPI + PostgreSQL + React — REST API + SPA

## Commands
uv run uvicorn app.main:app --reload   # dev server
uv run pytest                           # tests
uv run ruff check .                     # lint
uv run ruff format .                    # format
npm run dev                             # frontend dev
npm run build                           # frontend build

## Hard Rules
- Do not start coding without /plan approval
- All endpoints must have auth middleware (except /auth/*)
- Use repository pattern for all DB access
- Keep files under 800 lines
```

## Folder Structure

```
taskflow/
├── AGENTS.md
├── CLAUDE.md
├── PROJECT_CONSTITUTION.md
├── artifacts/
│   ├── prd.md
│   ├── architecture.md
│   ├── adr/
│   │   └── 001-jwt-auth.md
│   └── stories/
│       ├── 001-user-signup.md
│       └── 002-project-crud.md
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── auth/
│   │   ├── projects/
│   │   └── users/
│   └── tests/
├── frontend/
│   ├── src/
│   └── ...
└── .pre-commit-config.yaml
```
