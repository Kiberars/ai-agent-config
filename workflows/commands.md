# Commands & Workflow

All available agent commands with expected inputs and outputs.

---

## `/init`

**Trigger:** First task on any new project, or `PROJECT_CONSTITUTION.md` missing.

**Process:** See `workflows/init.md` for full interview + file generation flow.

**Output:**
- `PROJECT_CONSTITUTION.md` — filled from interview
- `CLAUDE.md` — filled from interview
- `docs/adr/ADR-000-initial-setup.md`
- `CHANGELOG.md`
- `mcp/active-servers.json`

---

## `/plan <task description>`

**Process:**
1. Read `PROJECT_CONSTITUTION.md` to understand constraints
2. Read relevant source files (do NOT modify them)
3. Identify affected files and dependencies
4. Write plan

**Output:** File `plans/YYYY-MM-DD-<slug>.md` with this structure:

```markdown
# Plan: <task title>
Date: YYYY-MM-DD
AES Level: L?

## Summary
One paragraph: what will be done and why.

## Files to Change
| File | Action | Reason |
|------|--------|--------|
| src/foo.ts | Modify | Add validation |
| src/bar.ts | Create | New module |
| tests/foo.test.ts | Modify | Cover new cases |

## Steps
1. ...
2. ...
3. ...

## Risks & Tradeoffs
- Risk: ... / Mitigation: ...

## Out of Scope
- ...

## Estimated Effort
S / M / L
```

**Wait for explicit approval before `/code`.**

---

## `/code`

**Requires:** Approved plan from `/plan`.

**Process:**
1. Implement exactly what the plan specifies — nothing more.
2. Write or update tests for every changed function.
3. Run linter before finishing.
4. Update `CHANGELOG.md` under `[Unreleased]`.

**Output:**
- Changed source files
- Updated/new test files
- Updated `CHANGELOG.md`

**End message:**
```
✅ Implementation complete.
Changed: <list of files>
Tests: <pass/fail count>
Lint: <clean / N warnings>
Next: /review
```

---

## `/review`

**Process:** Review the diff or specified files against:
- `PROJECT_CONSTITUTION.md` constraints
- AGENTS.md hard rules
- Language best practices
- Test coverage

**Output:** Inline comments + summary:

```markdown
## Review Summary
Files reviewed: N
Issues found: N critical, N minor, N suggestions

### Critical (must fix before merge)
- [ ] file.ts:42 — ...

### Minor (should fix)
- [ ] file.ts:88 — ...

### Suggestions (optional)
- [ ] ...

### Verdict: ✅ Approve / 🔁 Request changes
```

---

## `/fix <description or error>`

**Process:**
1. Reproduce or understand the error
2. Find root cause (not just symptom)
3. Fix the root cause only — no opportunistic refactoring
4. Verify fix doesn't break adjacent logic

**Output:**
```
Root cause: ...
Fix applied: <file:line> — <what changed>
Verified: <how verified>
```

---

## `/deploy`

**Process:**
1. Run AES compliance check (all 4 levels)
2. Run `{{TEST_COMMAND}}` and `{{LINT_COMMAND}}`
3. Generate deployment checklist

**Output:** File `deploy/checklist-YYYY-MM-DD.md`:

```markdown
# Deployment Checklist — YYYY-MM-DD

## AES Compliance
- [x] L1: PROJECT_CONSTITUTION.md present and filled
- [x] L2: Last plan was approved
- [x] L3: Architecture documented (ADR exists)
- [x] L4: Tests pass, lint clean, CHANGELOG updated

## Pre-Deploy
- [ ] Environment variables set in prod
- [ ] Database migrations applied
- [ ] Feature flags configured
- [ ] Rollback plan defined

## Deploy Steps
1. ...

## Post-Deploy Verification
- [ ] Health check passes
- [ ] Smoke test passes
- [ ] Monitoring alerts active
```

---

## `/update-rules`

**Trigger:** After a mistake was made, understood, and fixed.

**Process:**
1. Identify what rule was missing or unclear
2. Propose a patch to `AGENTS.md`
3. Show diff, wait for approval
4. Apply patch
5. Add entry to `CHANGELOG.md`

**Output:** Diff of `AGENTS.md` changes + `CHANGELOG.md` entry.

---

## `/status`

**Output:**

```markdown
## Project Status — YYYY-MM-DD

### AES Level: L?
- L1 ✅ PROJECT_CONSTITUTION.md present
- L2 ✅ / ⬜ Last plan: ...
- L3 ✅ / ⬜ ADRs: N documents
- L4 ✅ / ⬜ Tests: ? / Lint: ?

### Open Work
- plans/: N pending plans
- TODOs in code: N (run: grep -r "TODO" src/)

### Tech Debt
- ...

### Last 3 CHANGELOG entries
- ...
```

---

## `/explore`

**Output:**

```markdown
## Repository Map

### Structure
<tree of key directories>

### Entry Points
- ...

### Key Modules
- ...

### Config Files
- ...

### Observations
- ...
```

---

## `/clear`

**Process:**
1. If session > 30 min: run `skills/context-snapshot/SKILL.md` first
2. Print: "Session ended. Context saved. Start fresh with /plan <task>."
3. No further output.

---

## BMAD Cycle Reference

```
B — Brief      → /plan (understand + design)
M — Make       → /code (implement)
A — Assess     → /review (check quality)
D — Deploy     → /deploy (ship)
```

Run the full cycle for every non-trivial task.
