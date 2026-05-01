# Skill: Context Snapshot

## Purpose
Preserve project context between AI sessions. Implements Skaro-like persistent context so each new session starts with full understanding of decisions made.

## Trigger
Use when: starting a new session on an ongoing project, needing to remember "why" behind decisions, switching between projects frequently.

---

## The Problem This Solves

AI agents have no memory between sessions. Without captured context:
- Architecture decisions get forgotten and re-made differently
- "Why did we choose X?" has no answer
- Each session re-discovers the same things

---

## Context Files Structure

```
project/
├── AGENTS.md
├── PROJECT_CONSTITUTION.md
├── artifacts/
│   ├── architecture.md         ← system design
│   ├── adr/
│   │   ├── 001-database.md     ← why PostgreSQL not MongoDB
│   │   └── 002-auth.md         ← why JWT not sessions
│   ├── session-notes/
│   │   ├── 2026-04-17.md       ← what was done, what was decided
│   │   └── 2026-04-18.md
│   └── open-questions.md       ← unresolved decisions
```

---

## ADR Template

```markdown
# ADR-NNN: [Decision Title]

**Date:** YYYY-MM-DD
**Status:** Accepted | Deprecated | Superseded by ADR-NNN

## Context
What situation required this decision?

## Decision
What did we decide to do?

## Rationale
Why this option over alternatives?

## Consequences
What becomes easier? What becomes harder?

## Alternatives Considered
- Option A: rejected because...
- Option B: rejected because...
```

Save to: `artifacts/adr/NNN-title.md`

---

## Session Note Template

```markdown
# Session: YYYY-MM-DD

## What was accomplished
- Implemented X
- Fixed bug in Y
- Decided Z

## Decisions made (→ create ADR if significant)
- Chose approach A over B because...

## Open questions (→ add to open-questions.md)
- [ ] Should we use X or Y for the auth layer?

## Next session: start here
- Continue with story #N
- Resolve question about X first
```

Save to: `artifacts/session-notes/YYYY-MM-DD.md`

---

## Auto-Commit Context

After completing each task, commit context files:

```bash
git add artifacts/
git commit -m "context: session $(date +%Y-%m-%d) — [what was done]"
```

This ensures context is version-controlled and never lost.

---

## Session Start Ritual

When beginning a new session on this project:

```
1. Read PROJECT_CONSTITUTION.md
2. Read artifacts/architecture.md
3. Read artifacts/session-notes/ (last 2-3 files)
4. Read artifacts/open-questions.md
5. Now you're ready to work
```

Agent should do this automatically at session start.
