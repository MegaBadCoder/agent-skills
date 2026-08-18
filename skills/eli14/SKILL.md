---
name: eli14
description: >-
  Explain at the level of a bright fourteen-year-old — real terms allowed but each one unpacked
  on first use, analogies to support the mechanism rather than replace it. Use when the user says
  "eli14", "объясни как школьнику", "попроще, но по-настоящему", or when ELI5 landed and they
  want the actual mechanism next. The middle rung between eli5 (no terms at all) and eli-intern
  (full technical, just no project context assumed).
argument-hint: "[что объяснить — тема, файл, вопрос; пусто = последнее обсуждавшееся]"
---

# ELI14

Explain in the language the user is writing in.

## Before you explain: get the facts

If the subject is code in this repo, read it first. Quote real lines with `file:line` links.
Building an explanation on a remembered mechanism is how wrong mental models get installed.

## The shape of a good ELI14

**Terms are allowed — each unpacked once, where it first appears.** "Реактивность — это когда
кто-то запоминает, кто чем пользовался, и будит только тех, кого это касается." Then use the
term freely. Don't re-explain it three times; don't use it before unpacking it.

**Analogy supports, not replaces.** In ELI5 the analogy *is* the explanation. Here it's a way in
— after it lands, show the real mechanism and the real names.

**Cause before sequence.** Say *why* it has to work this way before *what happens in what
order*. A pipeline of steps with no cause is a transcript; the user can read that themselves.

**Show the real thing.** One real code fragment beats three paragraphs about it. Quote 3–8
lines, not a whole file.

**Contrast is the strongest teaching tool at this level.** "На боевой работает, в превью нет" —
and then what differs. The difference carries more information than either case alone.

## Length

One to two screens. If it needs more, split: explain the mechanism now, offer the edge cases
next.

## Never

- Use a term before unpacking it, or unpack a term nobody needs here.
- Present a design decision as inevitable. Say what the alternative was and why it lost —
  at this level that's the most valuable part.
- Invent motivation. If you don't know why something was built that way, check `git log`,
  or say you don't know.
- Give the answer to a question you're about to ask.

## Finish with one check

One question that requires applying the idea, not recalling it. "Если мы поменяем X, что
сломается первым?" or "где та же ошибка может случиться ещё раз?"

If they miss it, re-teach from a different angle — new example, smaller piece — then ask a
*different* question. Never re-ask the one they just failed.
