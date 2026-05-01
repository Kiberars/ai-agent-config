# Skill: Update Rules

## Purpose
After a mistake, update `AGENTS.md` to prevent recurrence. Implements self-improving configuration.

## Trigger
Use when: agent made a mistake, bad pattern repeated, want to prevent specific behavior.

Command: `/update-rules`

---

## The Loop

```
Agent made mistake
    ↓
Human fixes it (or agent fixes with guidance)
    ↓
"Update AGENTS.md so this doesn't happen again"
    ↓
Agent extracts the rule
    ↓
AGENTS.md gets smarter
    ↓
Next session: mistake doesn't repeat
```

---

## How to Invoke

After correcting a mistake:

```
"You just [did X wrong]. Update AGENTS.md with a rule to prevent this."
```

Or use the command:
```
/update-rules
```

Agent will:
1. Identify what went wrong
2. Extract the generalizable rule
3. Find the right section in `AGENTS.md`
4. Add the rule in `Do not...` format
5. Show you the diff for approval

---

## Rule Writing Guide

**Good rules:**
- Specific and actionable
- Written as prohibitions (`Do not...`)
- Address root cause, not symptom

**Bad rules:**
- Vague (`Be careful with X`)
- Too broad (`Always think before coding`)
- Symptom-level (`Don't delete files`)

**Examples:**

❌ Bad: "Be careful with database migrations"
✅ Good: "Do not run destructive migrations (DROP, TRUNCATE) without a confirmed backup and rollback plan"

❌ Bad: "Don't break things"
✅ Good: "Do not modify files outside the current task's explicitly stated scope"

---

## Rule Placement in AGENTS.md

- **Hard Rules** section — prohibitions that are always active
- **Agent-specific** — add to the relevant `agents/*.md` file
- **Workflow** — add to `workflows/commands.md` if it's process-related

---

## Verification

After adding the rule:
1. Re-read the section where you added it
2. Confirm the rule would have prevented the original mistake
3. Commit: `git commit -m "rules: prevent [what was fixed]"`
