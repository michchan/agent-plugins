# agent-plugins

A collection of Claude Code plugins extending AI agent capabilities for personal use.

## Plugins

### `personal-investing-and-wealth-management`

Skills and commands for a buy-and-hold, core-satellite equity investor. Wraps Anthropic's `equity-research:*` and `financial-analysis:*` skills with a personal investor lens.

**Skills**
- `equity-analysis-workflow` — Full 5-phase workflow: screening → deep dive → comparison → thesis → ongoing review

**Commands** (`/equity-analysis/...`)
| Command | Description |
|---------|-------------|
| `screen` | Screen for equity ideas by type (Defensive / Core / Satellite) |
| `initiate` | Run a full deep-dive initiation on a stock |
| `compare` | Compare a stock against peers for relative value |
| `thesis` | Create or update an investment thesis |
| `earnings-preview` | Build pre-earnings scenarios |
| `earnings` | Analyze quarterly earnings results |
| `catalysts` | View or update the catalyst calendar |
| `morning-note` | Draft a morning meeting note |

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
