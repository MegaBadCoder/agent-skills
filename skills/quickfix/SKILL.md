---
name: quickfix
description: Small bugs and single-file edits without ceremony — reproduce → hypothesis → minimal fix → test. Use when the user invokes /quickfix, or when a task turns out trivial (one-file CSS tweak, typo, missing import, single-line logic fix). Never commits — the user commits.
---

# Quickfix

For small bugs and single-file edits. No design phase, no plan document, no refactor.

The point is not speed for its own sake. It is that a one-line fix reviewed against a written plan costs more attention than the bug did, and the extra ceremony hides the one thing that matters: whether you actually found the cause.

## When to use

- **Use quickfix**: single-file change, obvious symptom, no API or schema change, no new tests beyond regression coverage of this bug.
- **Don't use quickfix**: multi-file refactor, new feature, contract or schema change, anything where you'd have to guess at intent. Those need design first — the wrong small fix in the wrong place is worse than a slow one.

## Protocol

1. **Reproduce** — describe the symptom in your own words and point at the failing path (`file:line`, command, screenshot). If you cannot reproduce it, say so and stop; a fix for a bug you never saw is a guess.
2. **Hypothesize** — state the suspected root cause with `file:line`, in one sentence: "I think X is the cause because Y." Wait for the user to confirm before editing.
3. **Fix** — the minimal change. No surrounding cleanup, no renaming, no new abstraction. Everything you touch beyond the cause is unreviewed work.
4. **Test** — run the smallest command that covers the change (`npx vitest run path/to.spec.ts`, `pytest path/to_test.py::test_name`). If no test covers the bug, add a regression test next to the fix.
5. **Report** — what changed, file by file, one line of rationale each. Do **not** commit or push; the user commits.

## Stop conditions

**If the first fix doesn't work, stop.** Do not try a second fix blindly — a guess stacked on a guess makes the next diagnosis harder, because now you cannot tell which change caused what you're seeing. Revert, re-diagnose with the user, and say plainly what you no longer believe.

**If the cause turns out to be elsewhere,** say so and stop. A bug that reproduces in one file but originates in another is not a quickfix — it needs the wider look you skipped.

**If you find yourself writing a fallback** — a default value, a swallowed exception, a `try/except: pass` to make the symptom go away — stop. That is not a fix, that is hiding the failure from the next person.
