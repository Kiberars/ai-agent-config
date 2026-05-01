# PROJECT_CONSTITUTION.md

> This file defines WHAT we are building. It is the single source of truth for project scope, architecture, and boundaries.
> AI agents must read this before any implementation work.

---

## Project Overview

**Name:** <!-- Project name -->
**Purpose:** <!-- One sentence: what problem does this solve? -->
**Target users:** <!-- Who will use this? -->

---

## Scope

### In scope
- <!-- Feature 1 -->
- <!-- Feature 2 -->

### Out of scope (explicit)
- <!-- What we are NOT building -->
- <!-- What can be added later, but not now -->

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

---

## Architecture

```
<!-- ASCII diagram or description of system components -->
```

### Key architectural decisions
<!-- Why this architecture? What were the alternatives? -->

---

## Domain Model

```
<!-- Core entities and their relationships -->
Entity A
  - field: type
  - field: type

Entity B
  - field: type
```

---

## API / Interfaces

<!-- Key endpoints, CLI commands, or public interfaces -->

---

## Quality Requirements

- **Performance:** <!-- e.g., "API responses < 200ms at p95" -->
- **Security:** <!-- e.g., "All endpoints require auth, no PII in logs" -->
- **Reliability:** <!-- e.g., "99.9% uptime, retries on failure" -->

---

## Constraints & Prohibitions

- Do not use <!-- banned dependency/pattern -->
- Do not store <!-- banned data type -->
- Always <!-- mandatory pattern -->

---

## AES Compliance

- [ ] L1 — Constitution defined (this file)
- [ ] L2 — Implementation plan exists
- [ ] L3 — Architecture is being followed
- [ ] L4 — Production ready

---

*Last updated: <!-- date --> by <!-- who/what -->*
