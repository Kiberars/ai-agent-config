# BMAD Cycle

Breakthrough Method for Agile AI-Driven Development.
Structured process that turns vibe coding into a predictable engineering workflow.

---

## When to Use BMAD

✅ **Use BMAD for:**
- SaaS products and long-lived projects
- Multi-feature systems with complex data models
- Anything that will grow over time

❌ **Skip BMAD for:**
- One-off scripts
- Prototypes "for tonight"
- Tasks under 2 hours

---

## The Four Phases

### Phase 1: Analysis
**Agent:** Product Manager (`agents/product-manager.md`)

```
Goal: Understand the problem before touching code.

1. Run /plan — PM agent asks clarifying questions
2. Brainstorm and research options
3. Write PRD → save to artifacts/prd.md
4. Get human approval on PRD
```

Output: `artifacts/prd.md`

---

### Phase 2: Planning
**Agent:** Planner (`agents/planner.md`)

```
Goal: Break PRD into executable tasks.

1. Read approved PRD
2. Create user stories with acceptance criteria
3. Save stories → artifacts/stories/
4. Estimate complexity (S/M/L per story)
5. Get human approval on story list
```

Output: `artifacts/stories/*.md`

---

### Phase 3: Solutioning
**Agent:** Architect (`agents/architect.md`)

```
Goal: Design the system before writing code.

1. Read PRD + stories
2. Design architecture
3. Write ADRs for key decisions
4. Save → artifacts/architecture.md + artifacts/adr/
5. Get human approval on architecture
```

Output: `artifacts/architecture.md`, `artifacts/adr/`

---

### Phase 4: Implementation
**Agent:** Developer (`agents/developer.md`)

```
Goal: Implement one story at a time, verified.

For each story:
1. /plan — implementation steps
2. Approval
3. /code — implement
4. /review — self-review
5. Tests pass (automated via Stop hook)
6. Move story to done
```

Output: Working code, passing tests, updated docs

---

## Artifacts Directory

```
artifacts/
├── prd.md                   ← Phase 1 output
├── architecture.md          ← Phase 3 output
├── adr/
│   ├── 001-database.md
│   └── 002-auth-strategy.md
└── stories/
    ├── 001-user-signup.md
    ├── 002-login-api.md
    └── 003-dashboard.md
```

---

## Key Insight

Each phase produces a document. Each document is an AI agent's context for the next phase. Context never gets lost — it lives in the repo, not in chat history.
