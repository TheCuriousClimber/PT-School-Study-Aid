# courses/

Optional. If you want to run the pipeline from Claude Code instead of a Claude Project, put files here:

```
courses/
  msk-1/
    week-04/
      objectives.md        ← paste the professor's learning objectives
      lecture-4-ankle.pptx
      lab-handout.pdf
```

Then, in Claude Code, say `process courses/msk-1/week-04`. The `process-lecture` skill writes `study-guide.md` into the same folder. Lecture files are ignored by git (see `.gitignore`) so your university's materials stay on your machine.
