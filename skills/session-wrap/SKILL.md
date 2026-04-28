---
name: session-wrap
description: End-of-session ritual that saves context so tomorrow you can pick up where you left off
---

# Session Wrap

You are helping the user close out a work session cleanly. The goal is simple: make sure tomorrow's session starts with full context instead of 10 minutes of "where was I?"

## Why this exists

Every AI coding session starts from zero. The model doesn't remember what you decided yesterday, what you tried and abandoned, or what you were halfway through. All of that context either lives in files or it's gone.

Without a close ritual, here's what actually happens:

**You waste the first 15-20 minutes of every session re-orienting.** Pasting context, re-explaining decisions, re-reading files. For a daily builder, that's 75-100 minutes a week spent not building anything.

**The model suggests things you already tried and rejected.** If you spent 40 minutes figuring out that approach A doesn't work, but that's only in yesterday's conversation history, tomorrow's session will confidently suggest approach A again. You'll burn time going down the same dead end.

**Decisions lose their reasoning.** "We're using Postgres" survives in code. "We're using Postgres because the client's DBA only supports it" does not. Without the reasoning, the next session will argue you out of decisions you already made for good reasons.

**Context compaction is lossy.** When a long session fills up, the model summarizes the conversation to free space. That summary keeps the gist but drops precision: specific error messages, nuanced tradeoffs, the exact moment you corrected the model's approach. If you don't extract what matters before that happens, it's gone.

**You pay for re-orientation in tokens too.** The first 10,000+ tokens of a cold session go to the model reading files and finding its footing. With a structured handoff, that drops significantly. Across a month of daily sessions, that adds up.

A 2-minute close ritual at the end of each session is the cheapest fix for all of this. You persist what matters to durable storage, log where you left off, and tomorrow you start building instead of searching.

## How to run

Run this in three phases. Don't skip ahead.

## Phase 1 - Capture what happened

Scan the conversation for anything worth persisting. You're looking for four things:

- **Decisions made** - technical choices, scope calls, things ruled out and why
- **Learnings** - something that worked, something that didn't, a preference the user expressed (especially through corrections)
- **Open tasks** - things started but not finished, or explicitly deferred
- **References** - URLs, docs, tools, or external resources that came up

Only capture what's actually useful. If the session was a quick bug fix with no decisions or learnings, say so and move on. Don't manufacture entries.

### Update memory files

For each item worth keeping, update the appropriate memory file in `~/.claude/projects/.../memory/`:

| What you found | Where it goes |
|---|---|
| User preferences, role, working style | `user_*.md` |
| Corrections, "do this not that" guidance | `feedback_*.md` |
| Project state, deadlines, goals, who's doing what | `project_*.md` |
| External URLs, docs, tools, dashboards | `reference_*.md` |

If a relevant memory file already exists, update it. Don't create duplicates. If you create a new file, add a one-line entry to `MEMORY.md`.

Tell the user what you updated and why. Keep it brief.

## Phase 2 - Housekeeping

### Git

Check if you're in a git repo. If yes:

1. Run `git status --short` and `git diff --stat HEAD`
2. If there are uncommitted changes, show them and suggest a commit message. Use plain English in imperative mood (e.g., "add session-wrap skill", "fix pricing page layout"). Don't commit without asking.
3. If everything is already committed, say so and move on.

### Session log

Prepend a new entry to `SESSION_LOG.md` at the root of the git repo. Create the file if it doesn't exist.

Format:

```
## 2026-04-28 | Short title of what happened

One or two sentences covering what got done and what's still open.

Main artifact: `path/to/the/main/thing/you/worked/on`

---
```

Newest entries go at the top. The file should read like a reverse-chronological work log.

## Phase 3 - Close

Print two things:

1. A session rename suggestion the user can copy-paste:
   `[2026-04-28] project-name - what was done`

2. A one-line summary with counts:
   `3 memory updates · 1 commit · SESSION_LOG updated`

That's it. Don't editorialize. Don't suggest next steps unless the user asks.

## Rules

- Don't create memory entries for things that are already in the code or git history. Memory is for context that isn't obvious from the repo.
- Don't commit without asking. Show the diff summary and proposed message, then wait.
- If the session was short or trivial, the wrap should be short too. A 5-minute typo fix doesn't need 4 memory updates.
- Keep session log entries to 2-3 lines max. This is a scannable log, not a journal.
- When updating memory files, follow the frontmatter format that already exists in the memory directory. Read an existing file first if you're unsure.
