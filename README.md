# agents

**English** · [Русский](i18n/README.ru.md)

> A curated set of agent skills for **vibe coding** — Cursor, Claude Code, Codex, and more. Ship fast with an agent, stay in control of what you actually built.

Vibe coding works until you need to debug, extend, or defend code you didn't write. These skills close that gap: they automate the boring parts of working with an agent without turning you into a passive reviewer.

---

## Skills

| Skill | Command | What it does |
|---|---|---|
| [**learn**](learn/) | `/learn` | Socratic teacher — verifies you *understand* the code (problem → solution → context), not just that it runs. Checklists in `.learning/`, quizzes, spaced recall. |

More skills coming. Each lives in its own folder with `SKILL.md` + docs.

---

## Install

Via [skills CLI](https://github.com/vercel-labs/skills) (recommended):

```bash
# list skills in this repo
npx skills add MegaBadCoder/agent-skills --list

# install learn globally for Claude Code, Cursor, and Codex
npx skills add MegaBadCoder/agent-skills --skill learn -g -a claude-code -a cursor -a codex -y
```

Manual copy:

```bash
for dir in ~/.claude/skills ~/.cursor/skills ~/.codex/skills; do
  mkdir -p "$dir/learn"
  cp skills/learn/SKILL.md "$dir/learn/SKILL.md"
done
```

Restart the agent once if its `skills/` folder didn't exist before. Further `SKILL.md` edits apply live.

---

## Repo layout

```
agents/
├── README.md
├── i18n/README.ru.md
├── skills/            # installable skills (npx skills add scans here)
│   └── learn/SKILL.md
└── learn/             # docs only
    ├── README.md
    ├── README.en.md
    └── README.ru.md
```
