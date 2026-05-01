# AI Agent Config

Universal configuration repository for AI coding agents.
Point any AI agent at this repo and it gets: rules, roles, skills, workflow, quality gates, and MCP setup.

**Works with:** Claude Code · Codex · Cursor · Gemini CLI · GitHub Copilot · Qwen · Minimax · any LLM

---

## Quick Start

```bash
git clone https://github.com/YOUR_USERNAME/ai-agent-config.git
```

Then tell your agent:

```
Read AGENTS.md in this repository.
It contains all rules, roles, and workflow for working with me.
```

**Full setup guide:** [docs/quickstart.md](docs/quickstart.md)

---

## What's Inside

```
ai-agent-config/
├── AGENTS.md                    ← Universal entry point (read this first)
├── CLAUDE.md                    ← Claude Code specific config
├── PROJECT_CONSTITUTION.md      ← Project scope & architecture template
│
├── agents/                      ← Specialized agent roles
│   ├── product-manager.md       ← Requirements & PRD
│   ├── architect.md             ← System design & ADRs
│   ├── developer.md             ← Implementation rules
│   ├── reviewer.md              ← Code review
│   ├── tester.md                ← Test writing
│   ├── planner.md               ← Task breakdown
│   └── simplifier.md            ← Complexity reduction
│
├── workflows/
│   ├── commands.md              ← /plan /code /review /fix /deploy /update-rules
│   ├── bmad-cycle.md            ← BMAD Method: Analysis → Planning → Design → Code
│   └── aes-levels.md            ← L1–L4 project maturity criteria
│
├── skills/
│   ├── SKILLS_INDEX.md          ← Skill catalog (loaded every session)
│   ├── parsing/SKILL.md         ← YouTube, HH.ru, web scraping
│   ├── text-to-speech/SKILL.md  ← TTS with OpenAI / Edge TTS
│   ├── context-snapshot/SKILL.md ← Persistent context between sessions
│   └── update-rules/SKILL.md    ← Self-updating AGENTS.md after mistakes
│
├── mcp/
│   ├── README.md                ← MCP setup guide
│   ├── recommended-servers.json ← Context7, Serena, Playwright
│   └── custom-template.json     ← Template for custom MCP servers
│
├── quality/
│   ├── .pre-commit-config.yaml  ← Ruff, Lizard, Xenon, markdownlint, shellcheck
│   └── hooks/settings.json      ← Claude Code PostToolUse + Stop hooks
│
├── templates/
│   ├── PROJECT_CONSTITUTION.template.md
│   ├── CLAUDE.md.template
│   ├── adr-template.md
│   └── bmad-story.template.md
│
├── docs/
│   ├── quickstart.md
│   ├── how-agents-read-this.md
│   └── token-optimization.md
│
└── examples/
    ├── saas-project/            ← Full SaaS config example
    └── solo-script/             ← Minimal script config
```

---

## Key Concepts

**AGENTS.md** — the single file any AI agent reads first. Contains rules, roles index, and workflow. Kept under 150 lines intentionally (based on Boris Cherny's Claude Code configuration philosophy).

**PROJECT_CONSTITUTION.md** — defines *what* you're building. Fill this in for every project. AI agents refuse to start implementation without it (AES L1).

**Skills** — on-demand capabilities. Agent reads `SKILLS_INDEX.md` every session, loads specific skills only when needed. Zero token waste.

**Agent Roles** — activate specific roles for specific tasks. One role = one Markdown file with responsibilities, rules, and output templates.

**Hooks** — code quality runs automatically. `PostToolUse` formats files on save. `Stop` runs tests after every task. You never think about formatting.

---

## Core Commands

| Command | Action |
|---|---|
| `/plan` | Plan before coding. Always. |
| `/code` | Implement approved plan |
| `/review` | Code review |
| `/fix` | Fix bugs (root cause only) |
| `/update-rules` | Learn from mistakes, update AGENTS.md |
| `/clear` | Fresh session before new task |

---

## Philosophy

Based on:
- **Boris Cherny** (creator of Claude Code): minimal config, hooks > rules, self-updating
- **BMAD Method**: structured agent roles, PRD → architecture → stories → code
- **AES (AI Engineering Standard)**: L1–L4 project maturity levels
- **Skaro 2.0**: persistent context via ADRs and session notes

> *"Every line must earn its place. No ballast."*

---

## License

MIT — use freely, adapt for your projects.
