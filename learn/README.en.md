# `/learn` — deep code understanding skill for Claude Code

**English** | [Русский](README.ru.md)

A Socratic teacher inside Claude Code (or any agent you wire it into). Its job is not to explain code, but to **verify you actually understand it**: the problem, the solution, the architecture, and the consequences. Understanding is proven through demonstration (restatements, quizzes, exercises) — not through "got it". Progress persists across sessions in `.learning/` checklists.

Why it exists: when an agent writes most of your code, it's easy to own a system you don't understand. This skill turns every session (or any existing code) into study material — and won't let you go until the understanding is yours.

---

## Installation

```bash
mkdir -p ~/.claude/skills/learn
cp SKILL.md ~/.claude/skills/learn/SKILL.md
```

- **Global** (`~/.claude/skills/learn/`) — available in all projects. Recommended.
- **Local** (`.claude/skills/learn/` in the repo) — this project only; commit and share with the team.

If `skills/` didn't exist before — restart Claude Code once. Further edits to `SKILL.md` are picked up live, no restart needed.

Want a different command name? The name comes from the **folder**, not the file:

```bash
mv ~/.claude/skills/learn ~/.claude/skills/study   # → command /study
```

---

## Quick start

```bash
/learn session                 # unpack what we just built this session
/learn src/auth/               # deep dive on a module
/learn -m src/processing/      # quick map: functions, classes, relationships
/learn -r                      # resume an unfinished topic
/learn -l                      # what I'm studying and where I left off
```

The skill also triggers **automatically** — on phrases like "explain this code", "how are these classes connected", "check my understanding", "walk me through what we built".

---

## Command and flags

```
/learn [-q|-m|-r|-l] [-t <topic/paths>] [-f <focus>] [-n <count>]
```

| Flag | Purpose |
|---|---|
| _(none)_ | Full teaching cycle (**teach** mode) |
| `-t <topic>` | What to study: file paths, module name, PR/commit ref, the word `session` (current session), or a saved topic slug. Works positionally too: `/learn src/auth/` |
| `-q` | **Quiz** only — verification without teaching |
| `-m` | **Map** only — function/class structure and relationships |
| `-r` | **Resume** a topic from a saved checklist |
| `-l` | **List** all topics: status, unchecked items, last session date |
| `-f <focus>` | Emphasize: `edge-cases`, `structure`, `why`. Focus deepens an area but does not waive the other layers |
| `-n <count>` | Quiz: number of questions (default 5–8) |

Parsing is forgiving: `--quiz` instead of `-q`, a path without `-t`, a topic in any language — intent is parsed, not syntax-policed. No arguments → interactive topic picker.

---

## Modes

### Teach — full cycle (default)

The main mode. Works stage by stage; **each stage closes only after you've demonstrated understanding**.

1. **Scope selection.** Session / file-module / PR diff / repo onboarding. The skill reads the code, `git log`/`git blame`, and traces calls — it teaches from real code, not conversation memory. Large topics split into units: depth beats coverage.

2. **Understanding checklist** in `.learning/<topic>.md` — three layers:
   - **Problem**: what we're solving, *why* the problem existed (root cause, not symptom), alternative branches and why they were rejected.
   - **Solution**: chosen approach and trade-offs, main execution path, edge cases, **invariants** — what must stay true for correctness.
   - **Context**: what this work changes — for callers, performance, deploys, other people; extension points and fragile spots.

3. **Structure map** (for units larger than a couple of functions): first **you** sketch relationships with text arrows (`upload → validate → parse → save`), then the skill shows the correct map — Mermaid saved in the doc, ASCII in the terminal. One line of responsibility per node, including what it *deliberately does not* do.

4. **Layer-by-layer teaching.** Order is strict: problem → solution → context — no "how the code works" before you can say why it exists. Within each layer:
   - first **you restate** your current understanding — gaps show up in the restatement;
   - the skill fills gaps, one concept per exchange;
   - for every "what", at least one "why"; for important decisions, second-order whys;
   - before running code or revealing an answer — **prediction**: "what do you expect to see?". The gap between expectation and reality is the main learning signal.

5. **Quizzes** at stage boundaries: open-ended and multiple choice with plausible distractors; answers hidden until submission; correct option position randomized.

6. **Active exercises** (at least one before finish): trace an input through the code, break-and-fix, predict the effect of changing a line, reconstruct the map from memory, teach-back (you explain the unit to a "new intern", the skill plays the intern with naive pointed questions), "requirements changed — what moves?".

7. **Mastery Gate.** Session doesn't end until: all three layers checked off via demonstration, at least one exercise done, and you've given a coherent restatement of the whole unit in your own words. If you must stop — progress is saved honestly; unchecked stays unchecked.

Calibration anytime: ask for **ELI5**, **ELI14**, or **ELII** (explain like I'm an intern).

### Quiz (`-q`) — verification without teaching

```bash
/learn -q -t orbital -n 10
```

Uses the saved checklist: first "Mistakes & weak spots", then spaced recall on mastered items — fresh wording, no repeats from the quiz log. Every miss explained against actual code lines. Results written to the doc: quiz log, unchecked items you clearly forgot, new weak spots. Quiz doesn't slide into teaching — when done, offers `-r` for gaps. Without `-t`, lists topics to pick from; if no docs exist, asks what to quiz on and reads that code first.

Quiz is user-initiated only — Claude won't spring one mid-task.

### Map (`-m`) — code map

```bash
/learn -m src/processing/
```

Fast standalone artifact without the full cycle: inventory of key functions/classes (5–15 nodes), relationships (calls, ownership, inheritance/composition, data flow), entry points and boundaries, responsibility per node. **Load-bearing** edges (changes ripple through the graph) vs incidental ones; blurry responsibility boundaries flagged. Mermaid → `.learning/`, ASCII → terminal. If you wrote the code — you're asked to sketch the map first.

### Resume (`-r`) — continue

```bash
/learn -r            # lists unfinished topics
/learn -r -t orbital # resume a specific one
```

Before resuming, the skill checks **staleness**: `git log` since the last session date. If the code changed materially — says what changed and adds checklist items instead of teaching outdated code. Then 1–2 spaced-recall questions on mastered items (a miss → checkbox honestly unchecked) and continue from the first open item.

### List (`-l`) — progress overview

All `.learning/*.md` docs: topic, status, unchecked count, last session date.

---

## The `.learning/` folder

Created at the repo root. One doc per topic:

```markdown
# Understanding: <topic>
_Last session: <date> · Status: in progress_

## 1. The Problem
- [x] Can state the problem in their own words
- [ ] Knows WHY the problem existed (root cause, not symptom)
...

## 2. The Solution
...code map (Mermaid), invariants, edge cases...

## 3. The Broader Context
...

## Mistakes & weak spots (revisit next time)
- Confused SatelliteManager ownership with the Three.js scene

## Quiz log
- 2026-06-10: Q on ground-track interpolation — miss, see weak spots
```

Your personal study notes: checkboxes only for demonstrated understanding, mistakes logged verbatim, diagrams render in the editor. Add `.learning/` to `.gitignore` (the skill will suggest it) — or commit it if you want learning history in the repo.

---

## Use cases

**After a work session with an agent.** Claude shipped a feature in an hour — before you commit, `/learn session`. Twenty minutes later you understand every decision and can defend the code in review.

**Onboarding into someone else's module.** `/learn -m src/legacy/billing/` for the map, then `/learn -t src/legacy/billing/` for a deep dive in parts.

**Reviewing a colleague's PR.** `/learn -t PR#142 -f why` — emphasis on decision motivation.

**Interview prep on your pet project.** `/learn -q -t snake-dqn -n 10` every few days: spaced repetition on weak spots surfaces what you can't explain cleanly.

**Long topic across evenings.** First evening — `/learn`, stop anywhere; each time after — `/learn -r`.

---

## What the skill will and won't do

Will:
- require restatement **before** explanation and drill "why" deep;
- show real code lines and ask you to predict behavior before running;
- say "not sure" honestly when decision motivation can't be verified in code/git;
- save progress after every exchange.

Won't:
- lecture for ten paragraphs before hearing you;
- accept "got it" as evidence;
- hint at answers in question wording or always put the correct option in the same position;
- jump to "how the code works" before "why it exists";
- end a session with an open checklist without your explicit "stop".

---

## Customization

Open `SKILL.md` and edit — changes apply immediately, no restart:

- **Softer Mastery Gate**: relax wording in the "Mastery Gate" section if the hard "won't let go" is tiring.
- **Default quiz size**: the number in quiz mode.
- **Notes path**: replace `.learning/` with your own (e.g. shared `~/notes/learning/`).
- **Auto-trigger**: triggers live in `description` frontmatter. Too aggressive — remove phrases; manual-only — add `disable-model-invocation: true` (but you lose useful auto-triggers like "explain this code").

## Troubleshooting

| Symptom | Cause / fix |
|---|---|
| `/learn` missing from autocomplete | File must live as `<folder>/SKILL.md`, not `learn.md`. If `skills/` was just created — restart the session |
| Skill doesn't fire on "explain this code" | Auto-trigger is probabilistic: simple requests Claude may handle alone. For certainty — explicit `/learn` |
| Name conflict | If `.claude/commands/learn.md` exists, the skill takes priority; remove the duplicate to avoid confusion |
| `-r` can't find topic | Make sure you're in the same repo: `.learning/` lives at the project root |
| Lessons too easy/hard | Say it in the dialog: "ELI5" / "ELII" / "go harder" — the skill calibrates |
