# Quickstart — 5 Minutes to Working AI Agent

This guide gets any AI agent (Claude Code, Codex, Cursor, Gemini CLI) configured and ready.

---

## Option A: Global Config (applies to all your projects)

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/ai-agent-config.git

# Link AGENTS.md globally (Claude Code / Codex)
cp ai-agent-config/AGENTS.md ~/AGENTS.md

# Link Claude Code hooks
mkdir -p ~/.claude
cp ai-agent-config/quality/hooks/settings.json ~/.claude/settings.json
```

Now every project you open will use these rules.

---

## Option B: Per-Project Config

```bash
# Copy essential files to your project
cp ai-agent-config/AGENTS.md your-project/
cp ai-agent-config/CLAUDE.md your-project/
cp ai-agent-config/templates/PROJECT_CONSTITUTION.template.md your-project/PROJECT_CONSTITUTION.md

# Fill in PROJECT_CONSTITUTION.md — takes ~10 minutes
# This is the most important step. Don't skip it.
```

---

## Set Up Quality Gates (Optional but Recommended)

```bash
cd your-project

# Install pre-commit
pip install pre-commit
# or
uv add --dev pre-commit

# Copy config
cp ai-agent-config/quality/.pre-commit-config.yaml .

# Install hooks
pre-commit install
```

Now every `git commit` will run linters automatically.

---

## Set Up MCP Servers (Optional)

```bash
# Copy recommended MCP config for Claude Code
cat ai-agent-config/mcp/recommended-servers.json >> ~/.claude/claude_desktop_config.json
```

Edit the file to keep only the servers you need.

---

## How to Talk to the Agent

### Starting a session
```
Read AGENTS.md and PROJECT_CONSTITUTION.md, then tell me what you understand 
about this project and what the current AES level is.
```

### Assigning a task
```
/plan — implement user authentication

(Wait for plan, approve it)

/code — implement the approved plan step by step
```

### After a mistake
```
You just did X wrong. Apply the update-rules skill. 
Read skills/update-rules/SKILL.md and update AGENTS.md to prevent this.
```

---

## File Hierarchy

```
Your computer:
~/.claude/settings.json       ← Claude Code hooks (global)
~/AGENTS.md                   ← Global rules (all projects)

Your project:
PROJECT_CONSTITUTION.md       ← What we're building
CLAUDE.md                     ← Project overrides
AGENTS.md                     ← Full rules (or symlink to global)
```

---

## Checklist

- [ ] `PROJECT_CONSTITUTION.md` filled in
- [ ] `CLAUDE.md` commands section updated for your stack
- [ ] Pre-commit hooks installed
- [ ] Claude Code hooks copied to `~/.claude/settings.json`
- [ ] MCP servers configured (optional)
- [ ] First session: run `/explore` to let agent map the codebase
