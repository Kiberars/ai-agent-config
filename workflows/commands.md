# Commands & Workflow

Standard commands for all AI agents in this repository.

---

## Commands

### `/plan`
Create an implementation plan. Wait for human approval before writing any code.

**Output:** Numbered list of steps with verification criteria.

```
/plan — add user authentication to the API
```

### `/code`
Implement the approved plan. Reference the plan explicitly.

```
/code — implement step 2 from the approved plan
```

### `/review`
Code review of current changes or specified diff.

Activates the Reviewer agent. See `agents/reviewer.md`.

### `/fix`
Find and fix an error. Root cause only — no temporary patches.

**Process:** Reproduce → diagnose → fix → verify tests pass.

### `/deploy`
Prepare for deployment. Check environment config, migrations, rollback plan.

### `/update-rules`
Update `AGENTS.md` based on the last mistake to prevent recurrence.

**Process:**
```
Agent made mistake
    ↓
Fix it
    ↓
"Update AGENTS.md so this doesn't happen again"
    ↓
Agent writes the rule
    ↓
AGENTS.md gets smarter
```

### `/status`
Print current project status: AES level, open tasks, blockers.

### `/explore`
Analyze repository structure. Output a summary of what exists and where.

### `/clear`
Reminder: start a new chat session for a new task. Conversation history wastes tokens.

---

## Standard Task Workflow

```
1. /clear          (new chat session)
2. /plan           (create plan, get approval)
3. /code           (implement step by step)
4. /review         (self-review before presenting)
5. Run tests       (automated via Stop hook)
6. /update-rules   (if a mistake was made)
```

---

## Parallel Sessions

For large tasks, run multiple sessions simultaneously:

```
Session A: feature/auth-api (git worktree)
Session B: feature/user-model (git worktree)
Session C: bugfix/login-edge-case (git worktree)
```

Each session is isolated. Use `git worktree add` for isolation.

---

## Context Optimization

- Run `/clear` before each new task
- Keep files under 800 lines (split + create `index.md`)
- Use `SKILLS_INDEX.md` to load only relevant skills
- Use RTK (`rtk read`, `rtk grep`) instead of full file loads when possible
