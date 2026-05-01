# AES Compliance Levels

AI Engineering Standard — four levels that define project maturity.

Reference: https://github.com/LENA-EE/AI-Engineering-Standard-AES

---

## Levels

### L1 — Constitution Defined
**Criteria:**
- [ ] `PROJECT_CONSTITUTION.md` exists in project root
- [ ] Scope is defined (what is in / out)
- [ ] Tech stack is chosen and documented
- [ ] Hard prohibitions are listed

**AI behavior at L1:** Agent reads constitution before every session. Refuses to implement anything that violates scope.

---

### L2 — Plan Exists
**Criteria:**
- [ ] Implementation plan created and approved
- [ ] User stories defined with acceptance criteria
- [ ] Priorities assigned
- [ ] No L1 violations

**AI behavior at L2:** Agent works from the plan, not from improvisation. `/plan` is always run before `/code`.

---

### L3 — Architecture Followed
**Criteria:**
- [ ] `artifacts/architecture.md` exists
- [ ] All ADRs documented for key decisions
- [ ] Code matches the documented architecture
- [ ] Reviews check architecture compliance
- [ ] No L2 violations

**AI behavior at L3:** Agent refuses to create architectural shortcuts. Reviewer checks constitution + architecture on every PR.

---

### L4 — Production Ready
**Criteria:**
- [ ] All tests pass (unit + integration)
- [ ] All linters pass (0 warnings)
- [ ] No hardcoded secrets or credentials
- [ ] Deployment runbook exists
- [ ] Rollback procedure documented
- [ ] No L3 violations

**AI behavior at L4:** Before any deploy task, agent verifies all L4 criteria.

---

## Checking Current Level

```
/status
```

Agent will output current AES level and what is blocking the next level.

---

## Enforcement

Agent must not advance to L2 without completed L1.
Agent must not begin implementation without completed L2.
