# `/learn`

Part of [agents](../) — vibe-coding skills for Cursor, Claude Code, and Codex.

**English** · [Русский](README.ru.md)

> Socratic code teacher — verifies you *understand* code, not just that it runs. Progress persists in `.learning/` checklists.

---

## Install

```bash
npx skills add MegaBadCoder/agent-skills --skill learn -g -a claude-code -a cursor -a codex -y
```

Or manually — copy `../skills/learn/SKILL.md` to `~/.claude/skills/learn/`, `~/.cursor/skills/learn/`, and `~/.codex/skills/learn/`.

---

## Quick start

```bash
/learn session                 # what we just built this session
/learn src/auth/               # deep dive on a module
/learn -m src/processing/      # structure map
/learn -r                      # resume unfinished topic
/learn -l                      # list progress
```

Auto-triggers on "explain this code", "check my understanding", "how are these connected", etc.

---

## Modes

| Flag | Mode |
|---|---|
| _(default)_ | **teach** — full cycle: scope → checklist → map → layers → quizzes → exercises → mastery gate |
| `-q` | **quiz** — spaced recall + weak spots |
| `-m` | **map** — functions, classes, call graph |
| `-r` | **resume** — continue from `.learning/<topic>.md` |
| `-l` | **list** — all topics and status |

Modifiers: `-t <topic/paths>`, `-f <focus>`, `-n <count>`.

---

## Full docs

| Language | File |
|---|---|
| English | [README.en.md](README.en.md) |
| Русский | [README.ru.md](README.ru.md) |
| Source | [SKILL.md](../skills/learn/SKILL.md) |
