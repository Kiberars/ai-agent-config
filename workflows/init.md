# /init — Project Initialization Workflow

This workflow runs when the user calls `/init` on a new project.
The agent conducts an interview, then **automatically generates** all config files.

---

## When to Run

- First time using this config on a project
- `PROJECT_CONSTITUTION.md` is absent or contains `{{` placeholders
- User explicitly requests re-initialization

---

## Phase 1 — Interview (ask ALL questions before writing anything)

Ask the user the following questions **in a single message** grouped by section.
Do not generate any files until all answers are received.

```
I'll set up your project configuration. Please answer these questions
(skip any that don't apply — write "skip"):

### Project
1. Project name?
2. One-sentence description of what it does?
3. Primary programming language(s) and framework(s)?
4. Target environment? (web app / mobile / CLI / library / API / desktop / other)

### Architecture
5. Database(s) used? (PostgreSQL / MongoDB / Redis / none / other)
6. External services or APIs integrated? (Stripe, Auth0, S3, etc.)
7. Monorepo or separate repos? Folder structure?
8. Any existing architecture decisions or constraints I should know?

### Team & Process
9. Solo developer or team? If team — approximate size?
10. Branching strategy? (main+feature / gitflow / trunk-based)
11. Deployment target? (Vercel / AWS / GCP / Docker / bare metal / other)
12. CI/CD already set up? If yes — which platform?

### Quality
13. Test framework? (pytest / jest / vitest / rspec / none)
14. Any linters/formatters already configured?
15. Code coverage requirement? (e.g., > 80% / none)

### Agent Preferences
16. Preferred response language? (English / Russian / other)
17. Any tools or MCP servers to enable? (browser / filesystem / database / custom)
18. Any hard constraints I must never violate in this project?
```

---

## Phase 2 — Auto-Generate Files

After receiving answers, generate the following files **in this order**:

### Step 1 — `PROJECT_CONSTITUTION.md`

Use template `templates/PROJECT_CONSTITUTION.template.md`.
Replace ALL `{{PLACEHOLDER}}` variables with answers from the interview.
If the user skipped a field, write `— not defined —` as the value.

### Step 2 — `CLAUDE.md`

Use template `templates/CLAUDE.md.template`.
Fill in:
- `{{PROJECT_NAME}}` → answer to Q1
- `{{STACK}}` → answer to Q3 + Q5 + Q6
- `{{DEV_COMMAND}}`, `{{TEST_COMMAND}}`, `{{LINT_COMMAND}}`, `{{BUILD_COMMAND}}` → infer from stack or ask
- `{{ARCHITECTURE_SUMMARY}}` → 2-3 sentence summary from Q7 + Q8
- `{{LANGUAGE}}` → answer to Q16

### Step 3 — `docs/adr/ADR-000-initial-setup.md`

Use template `templates/adr-template.md`.
Fill in:
- Title: "Initial project setup and architecture decisions"
- Context: summary of Q3–Q8
- Decision: key technology choices made
- Status: Accepted
- Date: today's date

### Step 4 — `CHANGELOG.md`

Create if absent:

```markdown
# Changelog

## [Unreleased]
### Added
- Initial project configuration via /init
```

### Step 5 — `mcp/active-servers.json`

Based on Q17, create a file listing only the MCP servers relevant to this project.
Copy relevant entries from `mcp/recommended-servers.json`.

### Step 6 — Verification Report

After generating all files, print:

```
✅ Initialization complete. Files created:
   • PROJECT_CONSTITUTION.md
   • CLAUDE.md
   • docs/adr/ADR-000-initial-setup.md
   • CHANGELOG.md
   • mcp/active-servers.json

📋 AES Status: L1 ✅  L2 ⬜  L3 ⬜  L4 ⬜

⚠️  Review PROJECT_CONSTITUTION.md — confirm it matches your project before /plan.

Next step: /plan <your first task>
```

---

## Phase 3 — Auto-Detect (Optional Enhancement)

If the project already has code, before asking questions the agent should:

1. Run `ls` / `find` to detect existing files
2. Auto-fill what can be inferred:
   - Language from file extensions (`.py`, `.ts`, `.rb`, etc.)
   - Framework from `package.json`, `pyproject.toml`, `Gemfile`, `go.mod`
   - Test setup from `jest.config.*`, `pytest.ini`, `*.spec.*`
   - Existing commands from `package.json` scripts or `Makefile`
3. Present detected values to user for confirmation before using them:

```
I detected the following — confirm or correct:
- Language: TypeScript
- Framework: Next.js 14
- Tests: Jest + React Testing Library
- Dev command: npm run dev
- Test command: npm test

Correct? (yes / list corrections)
```

---

## Rules for This Workflow

- Never skip Phase 1 entirely — always confirm at least the project name and stack.
- Never leave `{{PLACEHOLDER}}` text in generated files.
- Never overwrite existing `PROJECT_CONSTITUTION.md` without explicit user confirmation.
- If re-initializing: show diff of what will change and ask for approval first.
