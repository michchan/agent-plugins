# agent-plugins

A collection of Claude Code plugins extending AI agent capabilities for personal use.

## Plugins

### `personal-finance`

Skills and commands for personal finance — investing, portfolio management, and financial planning. Wraps Anthropic's `equity-research:*` and `financial-analysis:*` skills with a personal investor lens.

**Skills**
- `equity-analysis-workflow` — Full 5-phase workflow: screening → deep dive → comparison → thesis → ongoing review
- `accounting-workflow` *(planned)*
- `portfolio-management-workflow` *(planned)*

**Commands** (`/equity:...`)
| Command | Description |
|---------|-------------|
| `phase-1-screen` | Screen for equity ideas (top-down / bottom-up / event-driven) |
| `phase-2-deep-dive` | Full deep-dive initiation on a stock |
| `phase-3-compare` | Compare a stock against peers (comps + competitive analysis) |
| `phase-4-thesis` | Write or update an investment thesis |
| `phase-5-review` | Ongoing position review (pre/post-earnings, between-earnings, annual) |

## Structure

```
<plugin-name>/
  .claude-plugin/
    plugin.json          # Plugin metadata
  commands/              # Slash commands
  skills/                # Reusable skill definitions
    <skill-name>/
      SKILL.md           # Skill prompt and instructions
      references/        # Supporting reference docs
```
