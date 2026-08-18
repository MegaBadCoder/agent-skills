# agents

**English** · [Русский](i18n/README.ru.md)

> A curated set of agent skills for **vibe coding** — Cursor, Claude Code, Codex, and more. Ship fast with an agent, stay in control of what you actually built.

Vibe coding works until you need to debug, extend, or defend code you didn't write. These skills close that gap: they automate the boring parts of working with an agent without turning you into a passive reviewer.

---

## Skills

| Skill | Command | What it does |
|---|---|---|
| [**learn**](learn/) | `/learn` | Socratic teacher — verifies you *understand* the code (problem → solution → context), not just that it runs. Checklists in `.learning/`, quizzes, spaced recall. |
| [**eli5**](eli/) | `/eli5` | Explains with one physical analogy carried all the way through. No jargon at all. |
| [**eli14**](eli/) | `/eli14` | Real terms, each unpacked on first use. Analogies support the mechanism instead of replacing it. |
| [**eli-intern**](eli/) | `/eli-intern` | Technically complete, assumes zero knowledge of *this* codebase. The onboarding rung. |
| [**quickfix**](quickfix/) | `/quickfix` | Small bugs without ceremony: reproduce → hypothesis → minimal fix → test. Never commits. |

The three `eli` rungs are one ladder — when an explanation doesn't land, the fix is usually a different level, not more words.

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

As a Claude Code plugin — installs every skill at once and keeps them updatable:

```
/plugin marketplace add MegaBadCoder/agent-skills
/plugin install agent-skills@agent-skills
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
├── .claude-plugin/        # Claude Code plugin + marketplace manifests
│   ├── plugin.json
│   └── marketplace.json
├── skills/                # installable skills (npx skills add and the plugin both read this)
│   ├── learn/SKILL.md
│   ├── eli5/SKILL.md
│   ├── eli14/SKILL.md
│   ├── eli-intern/SKILL.md
│   └── quickfix/SKILL.md
├── learn/                 # docs only
│   ├── README.md
│   ├── README.en.md
│   └── README.ru.md
├── eli/                   # docs for the three rungs
│   ├── README.md
│   └── README.ru.md
└── quickfix/
    ├── README.md
    └── README.ru.md
```

`skills/` is the single source for every install path — the plugin, `npx skills add`, and manual copy all read the same `SKILL.md` files, so there is no second copy to drift.
