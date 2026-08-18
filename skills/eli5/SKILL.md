---
name: eli5
description: >-
  Explain something as if to a five-year-old — one physical-world analogy carried all the way
  through, no jargon, short sentences. Use when the user says "eli5", "explain like I'm five",
  "объясни как пятилетнему", "как для ребёнка", "совсем просто", or when their questions show
  they're lost in terminology rather than in the idea. Also use proactively mid-explanation when
  the user says "не понимаю" / "I don't get it" twice about the same thing — switch levels
  instead of repeating yourself louder.
argument-hint: "[что объяснить — тема, файл, вопрос; пусто = последнее обсуждавшееся]"
---

# ELI5

Explain in the language the user is writing in.

## Before you explain: get the facts

If the subject is code in this repo, **read it first**. Never build an analogy on top of a
half-remembered mechanism — a wrong analogy is worse than no analogy, because the user will
reason from it later. If you find you don't actually know how something works, go read it, or
say plainly that you don't know.

## The shape of a good ELI5

**One analogy, carried all the way through.** Pick something physical the user has touched:
boxes on a shelf, labels, a kitchen, mail, Excel. Then keep using *that* one. Switching
analogies mid-explanation is where people get lost.

**Short sentences.** One idea each. If a sentence has "which", "тем самым", or a semicolon,
split it.

**No terms.** Not "reactive", not "descriptor", not "dependency graph". If a term is
unavoidable because it's a name in the code, say the name and immediately give the everyday
word for it: `mapControls` — «полка, где лежат пульты».

**Concrete over general.** Not "components can conflict" but "три плагина вешают одинаковую
бирку, и выпадашка предлагает все три как равные". Name the actual three.

**Tie the analogy back to real lines.** After the picture lands, point at the file:
"вот эта бирка — [manifest.ts:11](path#L11)". The analogy is a handle, not a substitute.

## Length

An ELI5 that runs three screens is not an ELI5. Aim for one screen. If the subject genuinely
needs more, explain one piece now and offer the next.

## Never

- Talk down. "Как пятилетнему" is about vocabulary, not about respect. No "ну смотри, малыш",
  no exclamation points doing emotional work.
- Answer a different question than asked. If they asked what the *problem* is, do not explain
  the solution — that's the next message.
- Hedge. "В некотором смысле можно сказать, что как бы" — pick a claim and make it.
- Dump the mechanism as a list of steps. A numbered pipeline is not an explanation, it's a
  transcript. The user wants to know *why it has to work that way*.

## Finish with one check

End with a single question the user can answer in a sentence — one that only works if the idea
landed. Not "понятно?" (they'll say yes). Something like: "если у нас три коробки с одной
биркой, что помешает менеджеру выбрать не ту?"

If they miss it, do not repeat the same explanation. Change the analogy.
