---
name: eli-intern
description: >-
  Explain like to a competent intern — technically complete and precise, assuming general
  programming skill but zero knowledge of *this* codebase, its history, and its conventions.
  Use when the user says "elii", "eli-intern", "объясни как стажёру", "как новому разработчику",
  "введи в контекст", or when onboarding someone onto a subsystem. The top rung above eli14 —
  no simplification of the mechanism, only of the assumed context.
argument-hint: "[что объяснить — модуль, подсистема, поток данных; пусто = последнее обсуждавшееся]"
---

# ELI-Intern

Explain in the language the user is writing in.

## What "intern" means here

Assume they can read code, know their language, and understand common patterns. Assume they know
**nothing** about this repo: not its layout, not its vocabulary, not which decisions were
deliberate and which are leftovers. That last distinction is the single most valuable thing you
can transfer — a newcomer cannot tell a load-bearing invariant from an accident.

## Before you explain: get the facts

Read the code. Check `git log` / `git blame` for anything whose rationale you're about to state.
If the history doesn't explain it and the code doesn't either, say so — "не знаю, почему так;
похоже на остаток от X" is far more useful than an invented rationale that the intern will
repeat to someone else next week.

## The shape of a good intern explanation

**Start with the boundary.** What this unit is responsible for, and — equally — what it
deliberately does *not* do. Blurry responsibility boundaries are the top source of newcomer
mistakes.

**Then the path.** Entry point → what calls what → where data lands. Real function names, real
`file:line` links. If it's more than ~7 nodes, split the unit.

**Then the invariants.** What must stay true for this to be correct. Say what breaks if each is
violated, concretely — "тумблер будет переключать мок и не тронет слой", not "могут быть баги".

**Then the traps.** Silent failures, `?.` that swallows a missing object, fallbacks that hide a
misconfiguration, two names for one concept. Everything a newcomer will lose an afternoon to.

**Mark what's deliberate.** For each notable decision: what the alternative was, why it lost, and
whether that reasoning still holds. Say plainly when it doesn't — "так решили, когда карты в
превью не было вовсе; карта появилась, допущение устарело".

## Length

Two to three screens for a subsystem. Prefer depth on one unit over a tour of five.

## Never

- State a rationale you didn't verify in code, comments, or git history.
- Present accumulated accident as design. If it's a leftover, call it a leftover.
- Skip the failure modes because they're embarrassing — they're the highest-value part.
- Produce a call-graph dump with no "why". Structure without cause doesn't transfer.

## Finish with one check

An applied question, not a recall one: "требования изменились — надо N экземпляров этого
плагина на странице. Что придётся тронуть?" or "где здесь сломается, если данные придут
пустыми?"

If they miss it, that's a gap in the explanation, not in them — find which part you left
implicit, fill it, and ask something different.
