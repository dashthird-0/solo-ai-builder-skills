---
name: claude-md-review
description: Audit your instruction files for bloat, gaps, and stale rules
---

# CLAUDE.md Review

You are auditing the user's CLAUDE.md (or equivalent instruction file like .cursorrules) for quality. A good instruction file is lean, specific, and prevents mistakes. A bad one is worse than having no file at all.

## How to review

Read the user's instruction file and any files it references (@CONTEXT.md, @CODEBASE.md, etc.). Evaluate against these checks.

### Line-by-line test

For every line, ask: **"Would the agent make a mistake without this line?"**
- If no, flag it for removal.
- If yes, check that it's specific enough to actually prevent the mistake.

### Structure check

Flag if the file is over 150 lines. If it is, suggest splitting context by job (e.g., separate files for guardrails, business context, and architecture). A tight single file under 150 lines is fine. The split is a solution to bloat, not a universal requirement.

### Staleness check

- Flag rules that reference files, functions, or APIs that no longer exist in the codebase
- Flag rules that duplicate what the codebase already enforces through linters, types, or CI
- Flag auto-generated content that was never curated

### Specificity check

- Flag vague instructions ("be careful with auth") that should be specific ("use ensureAuth() before reading auth state")
- Flag missing non-negotiables. Common ones: build commands, deploy constraints, files that should never be committed, version bumping rules

## Output

- Lines to cut, with reason
- Missing rules to add, with reason
- Structural suggestions if needed
- Target: under 150 lines for the main file

## Rules

- Bias toward cutting. Bloated instruction files dilute the rules that actually matter.
- Only suggest additions that prevent specific, real mistakes. No "nice to have" context.
- If the file is already lean and effective, say so. Don't invent feedback.
