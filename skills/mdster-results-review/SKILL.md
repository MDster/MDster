---
name: mdster-results-review
description: "Use when the learner finishes an MDster practice session or asks how they did: shows MDster's results as a clear dashboard (score, grade, category and question-type breakdown), names strengths and areas to revise from the session, and suggests a focused next session."
---

# MDster results review

Turns MDster's session results into a short, motivating dashboard and a concrete plan for the next session.

## Steps

1. **Get the results.** Call `get-results` with the exam's `product_id`. This finishes the session: unanswered questions score 0 and the session is saved to the learner's MDster progress. If the learner is mid-session and only asked "how am I doing?", tell them this ends the session and ask first.
2. **Show the dashboard** (layout in the [presentation guide](../working-with-mdster/references/presentation.md)):
   - headline: `overall_percent`, `grade`, answered of total, `best_streak`;
   - a table from `category_breakdown`, and from `type_breakdown` when there is more than one question type;
   - `benchmark_avg`, when present, as "MDster learners' average", for context only.
3. **Strengths and revision.** Name the strongest categories, then the two or three to revise, each with one line on what to review, drawn from the explanations in this session. Do not invent facts or references.
4. **Next session.** Offer choices: practise the weakest category (`start-practice` with that `category_id`), a new mixed session, or the questions of the day.

## Rules

Quote numbers exactly as returned and never invent them. Present the results as practice performance, never as a prediction of a real exam result or a certification. Follow the `working-with-mdster` skill when it is installed: never accept real patient details, never give medical advice, and never promote MDster plans or sell anything. If the MDster tools are not available, tell the user to add the MDster MCP server at `https://mdster.com/mcp` and sign in to [MDster](https://mdster.com) when asked; the setup for each assistant is at https://mdster.com/ai-assistants.
