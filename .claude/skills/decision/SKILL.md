---
name: decision
description: Record a decision Ricardo has confirmed into the current project's DECISIONS.md.
disable-model-invocation: true
---

1. Identify the current project and its notes folder. If unclear, ask.
2. Confirm which decision to record. **Only record decisions Ricardo has explicitly confirmed.** If the decision is still a proposal, say so and stop.
3. Append a row to `DECISIONS.md` in the notes folder (create the file with the header below if it doesn't exist):

```
| Date | Decision | Options considered | Why | Decided by |
|---|---|---|---|---|
```

   - **Decision:** one line, concrete (e.g. "Chunk by manual section, max 800 tokens, 100 overlap").
   - **Options considered:** the alternatives, short.
   - **Why:** the reason in one or two lines, in plain terms a client would understand.
   - **Decided by:** "Ricardo".
4. Show Ricardo the row you added. Don't change anything else.
