---
name: mdster-daily-questions
description: "Use when the learner wants a quick daily practice with MDster, asks for today's questions or the questions of the day for a medical speciality, or has no exam with full access in MDster. Runs MDster's few daily MCQs per speciality one at a time, with marking and explanations."
---

# MDster questions of the day

Every signed-in MDster learner can answer a few MCQs per speciality each day: the same questions for everyone, refreshed at 00:00 UTC. It is a short, focused daily habit.

## Steps

1. **Pick the speciality.** If you don't have its ID yet, call `list-exams` and offer the specialities as choices.
2. **Get the questions.** Call `get-daily-questions` with the `speciality_id`. Say how many are left today (`remaining`). If none are left, say new ones arrive at 00:00 UTC and offer a summary of today's answers instead.
3. **Ask one at a time.** Show the first unanswered question (`answered_today: false`) as a question card, with its options exactly as returned. MCQ options are each true or false: let the learner select all they think are true.
4. **Mark.** Call `answer-daily-question` with the learner's letters as `true_options`. Each question can be answered once per day.
5. **Teach.** Show the feedback card: verdict and score, the correct options, MDster's explanation and one 💡 take-away.
6. **Repeat** for the next unanswered question, then finish with a one-line summary (for example "2 of 3 correct today") and offer what to do next: another speciality's questions of the day, or a full practice session when the learner has `full` access to an exam (skill `mdster-practice-session`).

## Rules

Follow the `working-with-mdster` skill when it is installed; its [presentation guide](../working-with-mdster/references/presentation.md) has the card layouts. Show questions exactly as returned, never reveal or hint at an answer before the learner submits, submit only the learner's own answer, never accept real patient details, and never promote MDster plans or sell anything. If the MDster tools are not available, tell the user to add the MDster MCP server at `https://mdster.com/mcp` and sign in to [MDster](https://mdster.com) when asked; the setup for each assistant is at https://mdster.com/ai-assistants.
