# Token Optimization

Techniques to reduce token consumption when working with AI agents.

---

## The Problem

More context = smarter answers, but also:
- Higher cost
- Slower responses
- Context window overflow on large tasks

Goal: load exactly what's needed, nothing more.

---

## Technique 1: File Size Limits

**Rule:** Keep all files under 800 lines.

When a file exceeds 800 lines:
1. Split into modules of ~200 lines each
2. Create `index.md` — catalog of what's in each module
3. Agent reads `index.md` → navigates to right module → loads only 200 lines

**Savings:** 87% token reduction on large files (load 200 lines instead of 1500).

```
Before: agent loads entire 1500-line file for one function
After:  agent reads 50-line index → loads 200-line module
```

---

## Technique 2: /clear Before New Tasks

Conversation history is dead weight. It consumes tokens without adding value — everything the agent needs is in the files, not the chat.

Start every new task with a fresh session.

In Claude Code: `/clear`
In other agents: start a new conversation

---

## Technique 3: RTK (Rust Token Killer)

CLI proxy that reduces token consumption 60–90% for file operations.

```bash
# Install
brew install rtk
# or
curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh

# Connect to Claude Code
rtk init -g

# Connect to Cursor
rtk init -g --agent cursor
```

RTK replaces file commands with token-efficient alternatives:

```bash
rtk ls .              # instead of: list all files
rtk read file.py      # instead of: read entire file
rtk grep "pattern" .  # instead of: search through files
rtk git diff          # instead of: show full git diff
```

Track savings: `rtk gain`

---

## Technique 4: Load Skills On-Demand

Don't load all skill files at session start. Let the agent scan `SKILLS_INDEX.md` (60 lines) and load specific skill files only when needed.

Bad prompt:
```
Read all the files in skills/ and tell me...
```

Good prompt:
```
Check SKILLS_INDEX.md for parsing skills, then apply the relevant one.
```

---

## Technique 5: Context Compression Threshold

In Claude Code, set the compression threshold higher to preserve more context before compression kicks in:

```json
// ~/.claude/settings.json
{
  "contextCompressionThreshold": 0.8
}
```

Default is lower — this gives extra buffer for large tasks.

---

## Technique 6: Targeted Questions

Instead of loading large files, ask targeted questions:

```
In auth/login.py, what does the `validate_token` function return?
```

vs.

```
Read auth/login.py and tell me about it.
```

The first loads one function; the second loads the entire file.

---

## Summary: Token Budget Per Session

| Item | Lines | Tokens (approx) |
|---|---|---|
| AGENTS.md | 150 | 1,200 |
| PROJECT_CONSTITUTION.md | 100 | 800 |
| SKILLS_INDEX.md | 60 | 480 |
| One skill | 120 | 960 |
| One agent role | 100 | 800 |
| **Base total** | **530** | **~4,200** |
| Remaining for code | — | ~190,000+ |

Claude has a 200K token context window. With proper organization, you'll rarely hit the limit.
