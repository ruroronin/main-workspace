---
name: eval
description: Run the current project's evaluation script and log the results in the notes folder.
disable-model-invocation: true
---

An eval tests the AI's answers: a set of questions with known correct answers is run through the system, each answer is graded, and the result is a score plus cost per question.

1. Identify the current project, its code repo and its notes folder. If unclear, ask.
2. Find how the project's eval is run: look in `PLAN.md`, `STATE.md` and the repo's README. **If there's no eval script yet, say so and stop.** Don't create one.
3. Before running, tell Ricardo how many questions will run, which model(s) will be called and a rough cost estimate. **Wait for his OK**, because evals cost API money.
4. Run the eval exactly as documented. Don't change the script, the questions or the thresholds.
5. Report:
   - score (e.g. 16/20) against the target in `PLAN.md`
   - cost: total and per question
   - each failed question in one line: question, expected, what came back, likely cause (retrieval missed the page / wrong page cited / answer wrong / grader issue)
6. Append to `eval-log.md` in the notes folder (create it with this header if missing):

```
| Date | Commit | Model | Score | Target | Cost | Notes |
|---|---|---|---|---|---|---|
```

   Get the commit with `git log -1 --format=%h`. Don't fix anything: fixes are planned with Ricardo.
