---
name: process-lecture
description: Turn a week's lecture files plus the professor's learning objectives into a blueprint, a budgeted flashcard deck, practical prep, an exam simulation, and a time-boxed study plan, following prompts/project-instructions.md. Use when the user says "process", names a course folder under courses/, or drops lecture PDFs or PowerPoints in the repo.
---

# Process a week of lectures

1. Read `prompts/project-instructions.md` in full. Those are the rules. Follow them exactly, including the card budget and the "You are allowed to skip" paragraph.
2. Find the inputs. If the user named a folder such as `courses/msk-1/week-04/`, use every `.pdf`, `.pptx`, `.docx`, and `.md` in it. Treat a file named `objectives.*` as the learning objectives. Otherwise use the files the user pointed at.
3. Extract the text. PDFs can be read directly. For PowerPoint files use the `anthropic-skills:pptx` skill to pull slide text and speaker notes. Keep slide numbers so the blueprint's "Covered in" column can cite them.
4. Run the `Process` pipeline from the instructions, Parts 0 through 5, and write the whole output to `study-guide.md` inside the week folder. Do not print it to the chat as well.
5. Print only the Deck stats line and the coverage gaps, then tell the user to paste `study-guide.md` into the study app under Add deck.

Never invent content the source does not contain. If the objectives are missing, infer them and mark each one `INFERRED`.
