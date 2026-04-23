---
name: weekly-digest
description: Generate a filtered weekly briefing of what shipped in AI. Signal only, no noise.
---

# Weekly AI Digest

Generate a weekly briefing of what shipped, what matters, and what to ignore in AI.

## Sources

Sources as of April 2026. Customize to your own.

### Works out of the box

- Official blogs: Anthropic, OpenAI, Google Gemini, DeepMind, Grok, DeepSeek, Qwen, Moonshot (Kimi)
- HackerNews: Top 20 AI-tagged posts from the week

### Requires API access (add if you have it)

- Twitter/X: Needs API key. Suggested follows: @karpathy, @fchollet, @jeremyphoward, @simonw, @HamelHusain, @natolambert, @rasbt, @chipro, @eugeneyan, @_jasonwei, @lilianweng, @emollick, @swyx, @ylecun, @AndrewYNg, @_akhaliq
- Reddit: Needs API key. Suggested: r/ClaudeAI, r/Codex, r/GeminiAI, r/automation top weekly

## Classification rules

- **Shipped**: Usable today. Has docs or a download link. This is signal.
- **Announced**: Roadmap, waitlist, demo only. Mention once, move on.
- **Noise**: Takes, drama, benchmarks without real-world proof. Skip entirely.

## Output format

For each "shipped" item:
- What it is (one line)
- Why it matters or doesn't for someone building with AI tools (one line)
- Action needed? Yes/No. If yes, what changes in my workflow

## Rules

- Maximum 10 items. If the week had 30 releases, pick the 10 that matter.
- No summaries of summaries. Go to the source.
- If unsure whether something is signal or noise, it's noise.
- End with: "One thing to try this week." A single concrete experiment.
