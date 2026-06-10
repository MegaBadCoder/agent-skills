# agents

**English** · [Русский](i18n/README.ru.md)

> A curated set of Claude Code skills for **vibe coding** — ship fast with an agent, stay in control of what you actually built.

Vibe coding works until you need to debug, extend, or defend code you didn't write. These skills close that gap: they automate the boring parts of working with an agent without turning you into a passive reviewer.

---

## Skills

| Skill | Command | What it does |
|---|---|---|
| [**learn**](learn/) | `/learn` | Socratic teacher — verifies you *understand* the code (problem → solution → context), not just that it runs. Checklists in `.learning/`, quizzes, spaced recall. |

More skills coming. Each lives in its own folder with `SKILL.md` + docs.

---

## Install any skill

```bash
# global — all projects (recommended)
mkdir -p ~/.claude/skills/<skill-name>
cp <skill-name>/SKILL.md ~/.claude/skills/<skill-name>/SKILL.md

# local — share with the team via repo
mkdir -p .claude/skills/<skill-name>
cp <skill-name>/SKILL.md .claude/skills/<skill-name>/SKILL.md
```

Restart Claude Code once if `~/.claude/skills/` didn't exist before. Further `SKILL.md` edits apply live.

Rename the command by renaming the folder: `mv learn study` → `/study`.

---

## Repo layout

```
agents/
├── README.md          # this file (EN)
├── i18n/
│   └── README.ru.md   # Russian
└── learn/
    ├── SKILL.md
    ├── README.md      # quick overview
    ├── README.en.md   # full docs (EN)
    └── README.ru.md   # full docs (RU)
```
