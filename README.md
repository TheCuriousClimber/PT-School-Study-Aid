# PT School Study Aid

A two-part tool for studying physical therapy coursework in less time: a rewritten set of Claude Project instructions that build a **small, blueprint-driven deck** from each week's lectures, and a **time-boxed study app** that stops you at 25 minutes and shows which learning objectives you are actually ready for.

**Study app (hosted):** https://claude.ai/code/artifact/50da0498-ebbd-4b9f-94d3-ae1a06da3814
**Study app (local):** open `app/study.html` in any browser. No install, no account.

## Why you were at six hours

The old instructions said "never summarize", "zero omission", "every row and every item". That is a specification for the maximum possible number of cards, and Tier 3 was generated and studied just like Tier 1. Six hours on one course is that prompt doing exactly what it was told. It is not a sign that you are slow or that you need to memorize harder.

Three things change here:

1. **The learning objectives are the filter.** Every card must point at one of the professor's objectives. Material with no objective behind it goes into a reference section you can look up, and the output tells you in plain words what you are allowed to skip and why.
2. **The deck has a budget.** One to four cards per objective, 30 to 60 per course per week, a hard ceiling of 80. Over the ceiling, the prompt cuts Low-weight material first.
3. **Sessions have a stop rule.** The app runs 25 minutes, reviews due cards first, adds new cards only as time allows, and then ends. Whatever is left rolls into tomorrow. Stopping on time is the skill being trained.

The exhaustive reference tables still exist. Type `Reference` and you get them, formatted for your spreadsheet. They are just no longer the default, and they are not study material.

## Setup, about five minutes

1. Open each course project in Claude. Replace the project instructions with the contents of [`prompts/project-instructions.md`](prompts/project-instructions.md) (everything below the horizontal rule).
2. Open the study app. It loads with a sample ankle-sprain deck so you can try a session immediately.
3. Optional: in the app, under Settings, set the exam date for each deck. Review intervals are then capped so every card is seen at least once before the exam.

## The weekly loop

| When | What | Minutes |
|---|---|---|
| Day the lectures post | Upload slides plus the professor's learning objectives to the course project. Type `Process`. Paste the reply into the app under Add deck. | 10 |
| Day 1 | Read the Clinical Primer once, then a session. Tier 1 cards, new only. | 5 + 25 |
| Day 2 | Session. Due cards, then Tier 2. Read the Practical Prep table once. | 25 + 10 |
| Day 3 | Session. Then practice the skills in Practical Prep on a partner or yourself. | 15 + 20 |
| Day 4 | Session. Then do the Exam Simulation closed-book. | 15 + 20 |
| Day 5 | Session. Due cards only. | 10 |

That is about 2.5 hours per course per week, including practical practice. The output's Part 5 prints this plan tailored to the week, and the app's Today page shows the due and new counts plus an estimate in minutes.

## What the output contains

`Process` produces seven parts, in order:

- **Part 0, Blueprint.** Each learning objective with its level (recall, explain, apply, perform), where it is covered in the slides, and an exam weight with a one-line reason. Objectives the material barely covers are marked THIN so you can ask the professor instead of memorizing harder.
- **Part 1, Triage map.** Each slide cluster marked LEARN, UNDERSTAND, REFERENCE, or SKIP, with the reason. Ends with a paragraph headed **You are allowed to skip**.
- **Part 2, Core deck.** The budgeted flashcards, tiered and tagged to objectives. Same `<br>•` cell format as before, so it still pastes into a spreadsheet.
- **Part 3, Practical prep.** Set-up, steps, positive finding, and what the examiner watches for, per skill. Practice material, not cards.
- **Part 4, Exam simulation.** Eight to twelve predicted questions with answers and the trap in each wrong option.
- **Part 5, Study plan and stats.** Card count, objectives covered, coverage gaps, and the time-boxed plan.
- **Part 6, Clinical primer.** A five-minute cheat sheet: the week's clinical story in plain English, a differential matrix contrasting the conditions covered, and three to five safety tripwires. Read it before the first session so you never meet a card cold.

Other commands: `Primer` for Part 6 alone, `Reference` for the exhaustive tables, `Cut it down` to shrink a deck by about 40% with a list of what was cut, `Quiz me` for ten questions one at a time, `Practical` for expanded skill prep, and `Why did you cut X?` to see the reasoning or promote an item into the deck.

## How the app decides what to show

- Cards are scheduled with a spaced-repetition algorithm (an SM-2 variant). Grade each card Again, Hard, Good, or Easy. Again brings the card back later in the same session.
- Due cards come first, sorted by tier. New cards are introduced in tier order, up to 20 per deck per day by default.
- **Tier 3 is off by default.** Turn it on in Settings only once every objective on the Today page reads "ready".
- The coverage table on the Today page groups cards by learning objective and shows solid, learning, and untouched for each. Two days before an exam, anything still "shaky" or "not started" is where the remaining time goes.
- Progress is saved in the browser. Export a backup from Settings before switching devices. Anki users can export a tab-separated file per deck.

## When the fear shows up

You will feel the urge to make more cards. When it does:

- Re-read the **You are allowed to skip** paragraph. It was written from the professor's own objectives.
- Ask the project `Why did you cut X?`. If the answer does not convince you, say "promote it" and it becomes a card. This is a fast, bounded action. Making forty extra cards is not.
- Check the coverage table. If every objective reads "ready", you are ready. The feeling of not being ready is not data.

If the burnout does not ease once the hours drop, that is worth a conversation with your program's student support or counselling service. Most PT programs have one, and week 2 is a normal time to use it.

## Running the pipeline from Claude Code instead

If you prefer files to a chat window, drop lecture files and an `objectives.md` into `courses/<course>/<week>/` and say `process courses/<course>/<week>` in Claude Code. The `process-lecture` skill in `.claude/skills/` writes `study-guide.md` next to them. Lecture files are git-ignored so university material stays on your machine. See [`courses/README.md`](courses/README.md).

## Repository layout

```
prompts/project-instructions.md   the Claude Project instructions (paste into each course project)
app/study.html                    the study app, single file
examples/sample-deck.md           a hand-written example of the output format
courses/                          optional local folders for the Claude Code workflow
.claude/skills/process-lecture/   the Claude Code skill that runs the pipeline on local files
```
