# `/quickfix`

Part of [agents](../) — vibe-coding skills for Cursor, Claude Code, and Codex.

**English** · [Русский](README.ru.md)

> Small bugs without ceremony: reproduce → hypothesis → minimal fix → test. Never commits.

---

## Why

A one-line fix reviewed against a written plan costs more attention than the bug did. Worse, the ceremony hides the only thing that matters — whether the cause was actually found, or whether the symptom just stopped showing.

`quickfix` strips the process down to the part that carries the risk: state the hypothesis out loud, get it confirmed, change one thing.

---

## Install

```bash
npx skills add MegaBadCoder/agent-skills --skill quickfix -g -a claude-code -a cursor -a codex -y
```

Or install the whole set as a Claude Code plugin — see the [root README](../README.md#install).

---

## Protocol

1. **Reproduce** — symptom in your own words, `file:line`. Can't reproduce → stop.
2. **Hypothesize** — "I think X is the cause because Y." Wait for confirmation.
3. **Fix** — minimal. No cleanup, no rename, no new abstraction.
4. **Test** — smallest command covering the change; add a regression test if none exists.
5. **Report** — what changed, one line each. The user commits, not the agent.

## Stop conditions

The three places it refuses to keep going:

- **First fix didn't work** → revert and re-diagnose. A guess stacked on a guess destroys the evidence: you can no longer tell which change caused what you're seeing.
- **Cause is somewhere else** → not a quickfix any more; it needs the wider look you skipped.
- **About to add a fallback** — a default value, a swallowed exception, `try/except: pass` → that hides the failure from the next person rather than fixing it.

## When not to use

Multi-file refactors, new features, schema or contract changes. Those need design first — the wrong small fix in the wrong place is worse than a slow one.

---

## Source

[SKILL.md](../skills/quickfix/SKILL.md)
