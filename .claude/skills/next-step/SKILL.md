---
name: next-step
description: Propose the next step of the current project from its PLAN.md and STATE.md, with the decisions it involves, then wait for Ricardo.
disable-model-invocation: true
---

1. Identify the current project and its notes folder (see workspace CLAUDE.md §1). If it's unclear, ask.
2. Read `PLAN.md` and `STATE.md`. If `PLAN.md` doesn't exist, say so and stop: the plan has to be agreed first.
3. Check the current step's "done when" against the code. If it isn't met, the next step is finishing it: say what's missing and stop there.
4. Otherwise present the next step from `PLAN.md`:
   - **Step:** name and "done when"
   - **What it involves:** everything needed to reach "done when", including setup, config, error handling and anything else unglamorous. Don't under-scope.
   - **Who writes what:** in HYBRID, which parts are core (Ricardo writes) and which are boilerplate (you write, diff by diff). In PAIR, note which parts you'll explain in depth.
   - **Decisions:** for each open decision in this step, give 2–3 options, the trade-offs in one line each, and your recommendation marked as a proposal.
   - **Concepts to learn:** what Ricardo will need to understand to build and explain this step.
5. Wait. Don't start the step, write files or change `STATE.md` until Ricardo says go. Once he confirms decisions, offer to record them with `/decision`.
