# Solo AI Builder Skills

**Production-grade skills for solo builders shipping products with AI coding tools.**

Built from 18+ months of daily usage shipping 3 complete apps. These are skills I actually run in my workflow, not templates I wrote for a repo.

## Installation

```bash
npx skills add dashthird-0/solo-ai-builder-skills
```

Works with Claude Code, Cursor, and any tool that supports the [agent skills](https://github.com/vercel-labs/skills) standard.

## Skills

### Product Thinking

| Skill | Description |
|-------|-------------|
| [`steel-man`](skills/steel-man/SKILL.md) | Poke holes in a product idea before you commit to building it |
| [`stress-test`](skills/stress-test/SKILL.md) | Simulate focus groups, pre-mortems, and stakeholder pushback on a feature |
| [`blind-spot`](skills/blind-spot/SKILL.md) | Surface the assumptions you haven't validated yet |

### Go to Market

| Skill | Description |
|-------|-------------|
| [`first-glance`](skills/first-glance/SKILL.md) | Run a 5-second test on your landing page or README without needing real users |
| [`say-it-better`](skills/say-it-better/SKILL.md) | Rewrite your copy so it talks about your customer's problem, not your features |

### Execution

| Skill | Description |
|-------|-------------|
| [`claude-md-review`](skills/claude-md-review/SKILL.md) | Audit your instruction files for bloat, gaps, and stale rules |
| [`safety-check`](skills/safety-check/SKILL.md) | Catch common safety gaps in your project before an agent run goes sideways |

### Solo Builder Survival

| Skill | Description |
|-------|-------------|
| [`rabbit-hole`](skills/rabbit-hole/SKILL.md) | Check how far you've drifted from what you actually sat down to do |
| [`session-wrap`](skills/session-wrap/SKILL.md) | End-of-session ritual that persists decisions, updates memory, and logs your work so you don't rebuild context from scratch every morning |

### Staying Current

| Skill | Description |
|-------|-------------|
| [`weekly-digest`](skills/weekly-digest/SKILL.md) | Weekly AI news briefing filtered down to what actually matters |

## Usage

Ask naturally. Claude applies the right skill:

```
Steel-man this idea: an AI-powered calorie tracker that uses your camera to log food.
```

```
Run a stress-test on this feature. We want to add social sharing to a parenting app.
```

```
Review my CLAUDE.md. Is it too bloated?
```

```
Run a safety check on this project before I let the agent run autonomously.
```

```
Give me this week's AI digest.
```

```
How deep am I in the rabbit hole right now?
```

```
Run a first-glance test on this landing page copy.
```

```
What blind spots am I missing in this business model?
```

```
Wrap this session. I'm done for today.
```

```
Rewrite this app store listing. It's all features, no benefits.
```

## License

[MIT](LICENSE)
