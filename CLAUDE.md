# humanizer-zh

Claude skill for removing AI-generated, translated, or mechanical phrasing from Chinese prose (blogs, essays, newsletters, product analysis).

## Structure

| File | Purpose |
|------|---------|
| `SKILL.md` | Core skill definition — full workflow, rules, and constraints |
| `references/patterns.md` | Common AI writing patterns and their fixes |
| `references/corpus.md` | Chinese reference corpus organized by text type |
| `references/corpus-quickpick.md` | Quick-reference lookup for common fixes |
| `agents/openai.yaml` | Codex UI metadata (display only, not functional) |

## How It Works

The skill guides rewriting through 5 stages:
1. **Text type detection** — blog, spec doc, newsletter, etc.
2. **Main line identification** — opening thesis, body segments, closing
3. **AI-flavor marker detection** — translation-ease, mechanical structure, empty words, slogans
4. **Rewriting intensity calibration** — light polish vs. deep restructuring
5. **Final reading check** — native Chinese flow verification

## Key Conventions

- All resource paths are relative (portable across skill directories)
- Chinese quotes: `「」` (not `""`)
- No long dashes `——`; prefer commas or sentence splits
- Minimize colons `：`; use natural sentence transitions
- Standard English terms kept as-is: token, API
- `PR` → `代码审查` in Chinese narrative context

## Installation

Copy this directory to any supported skills location:
- `~/.claude/skills/humanizer-zh` — Claude Code personal skills
- `./.claude/skills/humanizer-zh` — Claude Code project skills
- `~/.codex/skills/humanizer-zh` — Codex
- `~/.openclaw/skills/humanizer-zh` — OpenClaw

## Modifying the Skill

- Edit `SKILL.md` to change the rewriting workflow or rules
- Edit files in `references/` to update pattern libraries and corpus examples
- Version tracked in `VERSION` file; changes logged in `CHANGELOG.md`
