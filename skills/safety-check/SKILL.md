---
name: safety-check
description: Audit a project for common AI coding safety gaps before they cost you an afternoon
---

# Safety Check

You are auditing the user's project for safety gaps that commonly cause problems when working with AI coding agents. Focus on gaps that cause real damage, not theoretical risks.

## What to check

### Instruction specificity

Read the CLAUDE.md or equivalent. Flag:
- Vague instructions that leave room for creative interpretation ("handle auth", "clean up the module")
- Missing boundaries on destructive operations (database changes, file deletions, production config)
- Missing constraints on what NOT to modify

### Hook coverage

Check for hooks (pre-commit, post-edit, pre-command) that enforce guardrails structurally.
- Are critical rules enforced by hooks, or only by prompt instructions?
- Prompts are suggestions the agent can creatively reinterpret. Hooks are deterministic. Flag anything critical that relies only on prompts.

### Git discipline

- Is there a .gitignore? Does it cover secrets, build artifacts, platform directories (ios/, android/, node_modules/)?
- Are there uncommitted changes that would be lost if the agent goes sideways?
- Recommend: commit before every autonomous run. That's the reset button.

### Secrets and permissions

- Scan for hardcoded secrets, API keys, or credentials in tracked files
- Check if sensitive files (.env, credentials, service accounts) are gitignored
- Flag instructions that grant overly broad file or command permissions

### Commit history

- Scan recent commit messages for leaked secrets, credentials, API keys, or anything that shouldn't be visible if the repo goes public
- Check for sensitive data in diffs of recent commits (hardcoded tokens, passwords, connection strings)
- Flag unprofessional or embarrassing commit messages that would undermine credibility on a public repo

### Context grounding

- Are important decisions documented in files (CONTEXT.md, decision logs)?
- Decisions that only exist in chat history degrade through context compaction. Flag anything critical that lives only in conversation.

## Output

Rate each area: **Good**, **Needs attention**, or **Risk**.
For each risk, give a specific fix. Not "consider improving your .gitignore" but "your .gitignore is missing ios/ and android/."

## Rules

- Don't flag theoretical risks. Focus on gaps that cause real problems in practice.
- Be specific in every finding. Generic advice is not useful.
- If the project is well set up, say so. Don't manufacture findings.
