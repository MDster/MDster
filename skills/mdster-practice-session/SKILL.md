---
name: mdster-practice-session
description: "Use when the learner wants to practise or revise for a medical exam with MDster: run a full practice session of MCQs, short-answer questions or SOE/viva cases, from choosing the exam and topic to question-by-question marking with MDster's explanations and a results summary."
---

# MDster practice session

A guided practice session: the learner picks what to practise, answers one question at a time, gets MDster's marking and explanation after each, and finishes with a results dashboard.

## Steps

1. **Find the exam.** Call `list-exams`. Offer the exams with `full` access as choices (use your interface's choice buttons when it has them). If the learner has no exam with `full` access, offer the questions of the day instead (skill `mdster-daily-questions`).
2. **Set up.** Call `get-exam-options` for the chosen exam. Offer the question types (MCQ, short answer, SOE cases), the categories (or "All categories") and a number of questions up to `max_questions_per_session`. If the learner already said what they want ("10 pharmacology MCQs"), skip straight to starting.
3. **Start.** Call `start-practice`. If a session for this exam may still be in progress from earlier in the conversation, ask before replacing it. Pass on any `note` (for example a shorter session than requested).
4. **Ask.** Show the question as a question card: the stem and options exactly as returned, with no hints. Wait for the learner's answer. If they ask for the answer first, say MDster reveals it right after they answer, and invite a guess.
5. **Mark.** Call `submit-answer` with the learner's own letters (`true_options`) or their written answer unchanged (`text_answer`).
6. **Teach.** Show the feedback card: verdict and score, the correct answer, **Why** from MDster's explanation, **Why not the others**, **References** when returned, and one 💡 take-away. Offer: Next question · Explain more · Show results.
7. **Continue.** On "next", call `next-question` and repeat from step 4. When `is_finished` is true or the learner wants to stop, go to step 8.
8. **Results.** Call `get-results` and show the results dashboard (skill `mdster-results-review`).

## Rules

Follow the `working-with-mdster` skill when it is installed; its [presentation guide](../working-with-mdster/references/presentation.md) has the card layouts. In short:

- Show every question exactly as returned, one per message, and never reveal, hint at or guess an answer before the learner submits.
- Submit only the learner's own answer. Ground explanations in MDster's explanation, and never invent references.
- MDster is for education only: never accept real patient details and never give medical advice.
- If an exam needs full access (`members_only`), relay the message factually, and offer the questions of the day; never promote MDster plans or sell anything.
- If the MDster tools are not available, tell the user to add the MDster MCP server at `https://mdster.com/mcp` and sign in to [MDster](https://mdster.com) when asked; the setup for each assistant is at https://mdster.com/ai-assistants.
