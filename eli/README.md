# `/eli5` · `/eli14` · `/eli-intern`

Part of [agents](../) — vibe-coding skills for Cursor, Claude Code, and Codex.

**English** · [Русский](README.ru.md)

> Three rungs of the same ladder. When an explanation doesn't land, the fix is usually not more words — it's a different level.

---

## The problem

An agent explains what it built, and you nod. Then a week later you open the file and realise you never understood it — you understood the *summary*.

The usual failure is a mismatch of level. The explanation assumed terms you don't hold, or it assumed context about *this* codebase you were never given. Asking again gets you the same explanation, louder.

These three skills pick a rung deliberately:

| Skill | Assumes | Gives up |
|---|---|---|
| `/eli5` | nothing | all jargon — one physical analogy carried the whole way |
| `/eli14` | general curiosity | nothing technical, but every term is unpacked on first use |
| `/eli-intern` | general programming skill | only project context — the mechanism stays complete |

`eli-intern` is the one to reach for when onboarding someone onto a subsystem: it does not simplify how the thing works, only what you're assumed to already know about *this* repo.

---

## Install

```bash
npx skills add MegaBadCoder/agent-skills --skill eli5 --skill eli14 --skill eli-intern -g -a claude-code -a cursor -a codex -y
```

Or install the whole set as a Claude Code plugin — see the [root README](../README.md#install).

---

## Use

```
/eli5 how does the auth middleware decide who's logged in
/eli14 what does this reducer actually do
/eli-intern src/processing/
```

They also trigger without the command: "объясни как пятилетнему", "explain like I'm five", "как новому разработчику", "введи в контекст".

Mid-conversation switching is the intended use. If the same question comes back twice, that is the signal to change rung rather than repeat yourself — `eli5` also self-triggers when the user says "не понимаю" / "I don't get it" twice about the same thing.

---

## Source

| Skill | File |
|---|---|
| eli5 | [SKILL.md](../skills/eli5/SKILL.md) |
| eli14 | [SKILL.md](../skills/eli14/SKILL.md) |
| eli-intern | [SKILL.md](../skills/eli-intern/SKILL.md) |
