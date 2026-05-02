# Skill: project-init

Automatically detects project stack from existing files and pre-fills
the interview answers for `/init`. Reduces the number of questions
the user needs to answer manually.

---

## When to Apply

Apply this skill at the **start of Phase 1** in `workflows/init.md`,
before asking the user any questions.

---

## Detection Rules

Run these checks in order. Record findings in a `detected` map.

### Language Detection

```bash
# Check for language markers in priority order
ls package.json          → language: TypeScript/JavaScript
ls pyproject.toml        → language: Python
ls go.mod                → language: Go
ls Gemfile               → language: Ruby
ls Cargo.toml            → language: Rust
ls pom.xml / build.gradle → language: Java/Kotlin
ls composer.json         → language: PHP
ls *.csproj              → language: C#
```

### Framework Detection

**JavaScript/TypeScript:**
```bash
cat package.json | grep '"next"'      → framework: Next.js
cat package.json | grep '"nuxt"'      → framework: Nuxt.js
cat package.json | grep '"react"'     → framework: React (check for vite/cra)
cat package.json | grep '"vue"'       → framework: Vue.js
cat package.json | grep '"express"'   → framework: Express.js
cat package.json | grep '"fastify"'   → framework: Fastify
cat package.json | grep '"nestjs"'    → framework: NestJS
```

**Python:**
```bash
cat pyproject.toml | grep 'django'    → framework: Django
cat pyproject.toml | grep 'fastapi'   → framework: FastAPI
cat pyproject.toml | grep 'flask'     → framework: Flask
```

**Go:**
```bash
cat go.mod | grep 'gin-gonic'         → framework: Gin
cat go.mod | grep 'go-chi'            → framework: Chi
cat go.mod | grep 'echo'              → framework: Echo
```

### Dev Commands Detection

```bash
# JavaScript — read scripts from package.json
cat package.json | python3 -c "import sys,json; s=json.load(sys.stdin).get('scripts',{}); print(s)"

# Python — check Makefile or pyproject.toml
cat Makefile 2>/dev/null | grep -E "^(dev|test|lint|build):"
cat pyproject.toml | grep -A1 '\[tool.taskipy.tasks\]'

# Generic
cat Makefile 2>/dev/null | head -40
```

### Database Detection

```bash
grep -r "postgresql\|postgres" . --include="*.toml" --include="*.json" --include="*.env*" -l
grep -r "mongodb\|mongoose" . --include="*.toml" --include="*.json" -l
grep -r "redis" . --include="*.toml" --include="*.json" -l
grep -r "sqlite" . --include="*.toml" --include="*.json" -l
```

### Test Framework Detection

```bash
# JS
cat package.json | grep '"jest"\|"vitest"\|"mocha"\|"cypress"\|"playwright"'
ls cypress.config.* playwright.config.* vitest.config.*

# Python
ls pytest.ini pyproject.toml | xargs grep '\[tool.pytest\]' 2>/dev/null
ls test_*.py tests/ spec/
```

### CI/CD Detection

```bash
ls .github/workflows/*.yml 2>/dev/null  → CI: GitHub Actions
ls .gitlab-ci.yml 2>/dev/null           → CI: GitLab CI
ls Jenkinsfile 2>/dev/null              → CI: Jenkins
ls .circleci/config.yml 2>/dev/null     → CI: CircleCI
ls bitbucket-pipelines.yml 2>/dev/null  → CI: Bitbucket
```

### Deploy Target Detection

```bash
ls vercel.json .vercel 2>/dev/null        → deploy: Vercel
ls netlify.toml 2>/dev/null              → deploy: Netlify
ls Dockerfile docker-compose.yml 2>/dev/null → deploy: Docker
ls fly.toml 2>/dev/null                  → deploy: Fly.io
ls render.yaml 2>/dev/null               → deploy: Render
ls .railway 2>/dev/null                  → deploy: Railway
ls serverless.yml 2>/dev/null            → deploy: AWS Lambda
ls k8s/ kubernetes/ 2>/dev/null          → deploy: Kubernetes
```

### Environment Variables

```bash
cat .env.example 2>/dev/null | grep -v '^#' | grep '=' | cut -d= -f1
cat .env.template 2>/dev/null | grep -v '^#' | grep '=' | cut -d= -f1
```

### Existing Constraints

```bash
# Check if any AGENTS.md or CLAUDE.md already exists
cat CLAUDE.md 2>/dev/null
cat .cursorrules 2>/dev/null
cat .github/copilot-instructions.md 2>/dev/null
```

---

## Output Format

After running detection, present findings to the user:

```
I scanned the project and detected:

✅ Auto-detected (will use unless you correct me):
   Language:      TypeScript
   Framework:     Next.js 14
   Database:      PostgreSQL (via prisma)
   Tests:         Jest + React Testing Library
   CI/CD:         GitHub Actions
   Deploy:        Vercel
   Dev command:   npm run dev
   Test command:  npm test
   Lint command:  npm run lint
   Build command: npm run build

❓ Could not detect (please answer):
   - Project name and description
   - Team size and branching strategy
   - Any hard constraints
   - Your preferred response language
```

Then proceed with the shortened interview (only unanswered questions).

---

## Skill Rules

- Never assume a value without evidence from actual files.
- If detection is ambiguous (e.g., both Jest and Vitest configs exist), list both and ask.
- Always show detected values to the user before using them — never silently fill.
- Prefer reading `package.json`, `pyproject.toml`, and `go.mod` over guessing from file names.
