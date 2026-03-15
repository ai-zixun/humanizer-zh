# humanizer-zh

[中文](./README.md) | [English](./README.en.md)

`humanizer-zh` is a Chinese writing cleanup skill for Codex, Claude Code, and OpenClaw. It rewrites AI-sounding, translated, or overly mechanical Chinese prose so it reads like native Chinese writing instead of a stitched-together model draft.

This repository uses a single-directory skill layout: the repository root is the skill directory. After publishing it online, users can clone it directly into each agent's skills folder.

## Use Cases

- Humanizing Chinese blog posts, essays, commentary, product analysis, and newsletters
- Removing translation-like phrasing, formulaic contrast frames, and inflated closing lines
- Explaining why a Chinese passage feels AI-written, with before/after examples
- Preserving facts and intent while improving paragraph rhythm and idiomatic phrasing

## Scope

- Detects and rewrites translation artifacts, rigid sentence patterns, and empty big words
- Normalizes punctuation, dates, English term casing, and mixed Chinese/English typography
- Adjusts rewrite intensity by text type instead of flattening everything into one tone
- Loads `references/patterns.md` only when a deeper diagnostic rewrite is needed

## Compatibility

| Platform | Status | Notes |
| --- | --- | --- |
| Codex | Supported | Reads the root `SKILL.md`; `agents/openai.yaml` is only UI metadata for Codex. |
| Claude Code | Supported | Uses the same `SKILL.md`; works as a personal or project skill. |
| OpenClaw | Supported | Uses the same AgentSkills-style `SKILL.md`; works in managed or workspace skill directories. |

The runtime behavior lives in `SKILL.md` and `references/`, not in this README.

## Repository Layout

```text
humanizer-zh/
├── .gitignore
├── LICENSE
├── SKILL.md
├── README.md
├── README.en.md
├── agents/
│   └── openai.yaml
└── references/
    └── patterns.md
```

## Installation

Clone this repository directly into the target agent's skills directory.

### Codex

If `CODEX_HOME` is set, install into `$CODEX_HOME/skills`. The common default is `~/.codex/skills`.

```bash
mkdir -p ~/.codex/skills
git clone <your-repo-url> ~/.codex/skills/humanizer-zh
```

### Claude Code

Personal skill:

```bash
mkdir -p ~/.claude/skills
git clone <your-repo-url> ~/.claude/skills/humanizer-zh
```

Project skill:

```bash
mkdir -p ./.claude/skills
git clone <your-repo-url> ./.claude/skills/humanizer-zh
```

### OpenClaw

Managed skill:

```bash
mkdir -p ~/.openclaw/skills
git clone <your-repo-url> ~/.openclaw/skills/humanizer-zh
```

Workspace skill:

```bash
mkdir -p ./skills
git clone <your-repo-url> ./skills/humanizer-zh
```

After the repo is published, OpenClaw installations that support GitHub skill installs may also accept:

```bash
openclaw skills install github:<your-user>/humanizer-zh
```

## Usage

All three platforms use the same runtime entry point, but discovery differs by agent.

### Codex

You can mention the skill explicitly:

```text
Use $humanizer-zh to rewrite this Chinese draft so it reads like native Chinese writing and loses the translation feel.
```

### Claude Code

Claude Code skills are usually model-invoked, so a direct request is often enough:

```text
Rewrite this Chinese draft so it sounds like native writing. Remove translation-like phrasing, empty big words, and stiff paragraph rhythm.
```

### OpenClaw

OpenClaw can auto-match the skill and may also expose it as a user-invocable command depending on local settings:

```text
Use humanizer-zh to rewrite this Chinese draft so it reads like native Chinese writing.
```

## Runtime Notes

- `SKILL.md` is the runtime entry point
- `agents/openai.yaml` is Codex-specific UI metadata
- `references/patterns.md` is loaded on demand for deeper rewrite and diagnosis work

## Acknowledgements

This skill is inspired by [blader/humanizer](https://github.com/blader/humanizer), which packaged AI-writing cleanup guidance as a reusable Claude Code skill. `humanizer-zh` extends that idea into Chinese writing, with extra attention to translation artifacts, Chinese paragraph rhythm, punctuation, and long-form nonfiction style.

## License

This repository is licensed under the [MIT License](./LICENSE).
