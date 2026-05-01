# PROJECT_CONSTITUTION.md

> Copy this file to your project root and fill in all sections.
> AI agents read this before every session.

---

## Project Overview

**Name:** [project-name]
**Purpose:** [One sentence: what problem does this solve and for whom?]
**Target users:** [Who uses this?]
**Status:** [Planning | In Progress | Production]

---

## Scope

### In scope
- [Core feature 1]
- [Core feature 2]
- [Core feature 3]

### Explicitly out of scope
- [Thing we're NOT building — be specific]
- [Future feature — label it "Future: X" so it's not forgotten]

---

## Tech Stack

| Layer | Choice | Reason |
|---|---|---|
| Language | | |
| Framework | | |
| Database | | |
| Auth | | |
| Deployment | | |
| Testing | | |
| CI/CD | | |

---

## Architecture

```
[ASCII diagram or description of how components connect]

Example:
Browser → Next.js → FastAPI → PostgreSQL
                 ↓
              Redis (cache)
```

### Key architectural decisions
See `artifacts/adr/` for detailed ADRs.

---

## Domain Model

```
[Core entities]

User
  - id: UUID
  - email: string
  - created_at: datetime

Project
  - id: UUID
  - owner_id: UUID → User
  - name: string
```

---

## API / Interfaces

```
[Key endpoints or CLI commands]

POST /api/auth/login
GET  /api/projects
POST /api/projects
```

---

## Quality Requirements

- **Performance:** [e.g., API p95 < 200ms]
- **Security:** [e.g., all endpoints require JWT auth]
- **Reliability:** [e.g., retries on third-party failures]
- **Observability:** [e.g., structured JSON logs, error tracking]

---

## Hard Constraints

- Do not use [banned dependency or pattern]
- Do not store [banned data — e.g., plaintext passwords, PII in logs]
- Always [mandatory pattern — e.g., "validate input at API boundary"]
- All database writes must go through [repository layer / ORM]

---

## Development Standards

- Files must stay under 800 lines — split into modules if larger
- Functions: max 50 lines, max cyclomatic complexity 10
- Tests required for: all business logic, all API endpoints
- No `TODO` comments without linked task number

---

## AES Compliance

- [ ] L1 — Constitution defined (this file)
- [ ] L2 — Implementation plan exists and approved
- [ ] L3 — Architecture is being followed in all PRs
- [ ] L4 — Production ready (tests pass, linters pass, runbook exists)

---

*Created: [date] | Last updated: [date]*
