# Skills Index

AI agents: scan this file to find the right skill. Load the skill file only when needed — don't load all skills at once.

---

## How to Use Skills

**Automatic:** Agent reads keywords and activates relevant skill.

**Explicit (recommended):**
```
"Apply the parsing skill. Read skills/parsing/SKILL.md and parse this YouTube page."
```

Explicit activation is 100% reliable. Automatic activation depends on keyword matching.

---

## Available Skills

### 1. Parsing (`skills/parsing/SKILL.md`)

**Keywords:** parse, scrape, extract, YouTube, kwork, HH, HeadHunter, web data, API data
**Use when:** Extracting structured data from websites, APIs, or documents
**What it covers:** YouTube metadata, job boards (HH.ru, kwork), HTML parsing, rate limiting, output formats

---

### 2. Text-to-Speech (`skills/text-to-speech/SKILL.md`)

**Keywords:** text to speech, TTS, voice, audio, narration, read aloud, synthesize
**Use when:** Converting text content to audio files
**What it covers:** API selection, audio formats, voice selection, chunking long text

---

### 3. Context Snapshot (`skills/context-snapshot/SKILL.md`)

**Keywords:** context, memory, project state, remember, session, ADR, architecture decision, snapshot
**Use when:** Preserving project context between AI sessions (Skaro-like approach)
**What it covers:** ADR creation, session notes, auto-commit context, kanban tracking

---

### 4. Update Rules (`skills/update-rules/SKILL.md`)

**Keywords:** update rules, learn from mistake, add rule, prevent recurrence, self-update, AGENTS.md
**Use when:** After a mistake — updating AGENTS.md to prevent it from happening again
**What it covers:** Mistake → rule extraction → AGENTS.md update → verification

---

## Adding New Skills

1. Create `skills/your-skill/SKILL.md`
2. Add entry to this index with: name, keywords, use-when, what-it-covers
3. Keep each SKILL.md under 200 lines

Skills are loaded on-demand. The index is always loaded.
