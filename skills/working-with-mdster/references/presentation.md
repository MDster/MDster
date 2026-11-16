# Presentation: cards, choices and layouts

MDster practice should feel like a well-designed study app inside the chat: calm, consistent and easy to scan on a phone. Use these layouts every time, so the learner always knows where to look.

## General style

- **One question per message.** Never show the next question in the same message as feedback.
- **Same order every time**: header, content, then the choices.
- Short headings, bold labels and generous line breaks. No walls of text.
- Use emoji only as signposts (🩺 ✅ 🟡 ❌ 💡 📚 📊 🎯), never as decoration inside medical content.
- Tables for comparisons (options, categories). Lists for options and steps, because they read better on narrow screens.
- Show maths and units exactly as returned. If the content contains LaTeX and your interface renders it, render it; otherwise show it as returned.
- If formatting does not render, keep the same order in plain text.

## Choices: let the learner tap, not type

When your interface offers interactive choices (buttons, option pickers, multi-select questions or forms), use them for:

| Moment | Choices to offer |
| --- | --- |
| Picking an exam | The exams from `list-exams` with `full` access (and the questions of the day) |
| Session setup | Question type, category (or "All categories"), number of questions |
| Answering an MCQ | **Multi-select** of the option letters: each option is true or false, and the learner selects every one they think is true |
| After feedback | Next question · Explain more · Show results |
| After results | Practise weak areas · New session · Questions of the day |

Without interactive choices, end the message with a short lettered or numbered list the learner can reply to with a letter or number. Never pre-select or highlight an answer option.

## Question card

```markdown
### 🩺 Anaesthesia Core · Pharmacology
**Question 3 of 10** · MCQ

> {stem, exactly as returned}

**Mark each statement true or false** (select all that are true):

- **A.** {option A text}
- **B.** {option B text}
- **C.** {option C text}
- **D.** {option D text}
- **E.** {option E text}

*Reply with the letters you mark as true, for example: A, C.*
```

- Put `sub_title` under the stem in italics when present.
- SOE: show the case title (`soe_case`) above the first part as **Case:**, and keep it in the header for later parts ("Case: Post-operative hypoxia · Part 2").
- SAQ: replace the options with "✍️ **Your answer:** write it in your own words."
- Never add hints, highlights or "tricky" warnings.

## Feedback card (after `submit-answer`)

Verdict from `result.score` (0 to 1):

| Score | Verdict line |
| --- | --- |
| 1 | ✅ **Correct** |
| between 0 and 1 | 🟡 **Partly correct** (show the score, for example 0.6) |
| 0 | ❌ **Not quite** |

If `result.assessment_note` is present, say the mark is provisional.

```markdown
### ✅ Correct · score 1/1

| Option | Answer | You said |
| --- | --- | --- |
| A | True | True ✅ |
| B | False | False ✅ |
| C | True | False ❌ |

**Why**
{MDster's explanation, in short paragraphs or bullets. Keep its meaning; do not contradict it.}

**Why not the others**
- **B:** {option explanation from MDster, when present}

📚 **References**
- {each item from `references`, exactly as returned}

> 💡 **Take-away:** {one sentence, the single fact worth remembering, drawn from MDster's explanation}

**Next:** Next question · Explain more · Show results
```

- MCQ: build the table from `options[].is_correct` and the learner's own letters. `correct_options` lists the true letters.
- SAQ: replace the table with a two-column comparison:

  | Your answer | MDster model answer |
  | --- | --- |
  | {your_text_answer} | {model_answer, key points as short lines} |

  Then add `result.feedback` as **Marker feedback** when present.
- Only show **References** when the tool returned them. Never add references of your own.
- **Explain more** means a deeper teaching answer: mechanisms, a memory aid, or a comparison table of the options, still grounded in MDster's explanation and labelled as background where you go beyond it.

## Results dashboard (after `get-results`)

```markdown
## 📊 Session results · Anaesthesia Core

**78%** · Grade **B** · 7/9 answered · best streak 4

| Category | Questions | Score |
| --- | --- | --- |
| Pharmacology | 4 | 88% |
| Physiology | 3 | 67% |

**💪 Strengths:** {categories at or above 80%}
**🎯 Revise next:** {lowest categories, with one line each on what to review, from this session's explanations}

**Next:** Practise {weakest category} · New session · Questions of the day
```

- Use `overall_percent`, `grade`, `answered_questions`/`total_questions`, `best_streak`, `category_breakdown` and `type_breakdown`. Quote numbers exactly; never invent them.
- If `benchmark_avg` is present, show it as "MDster learners' average" for context, without judging the learner.
- Results are practice performance, not a prediction of a real exam result.

## Members-only and errors

- Members-only: one short, factual line from `message`, then offer the questions of the day if `daily_3_remaining` is above 0. No selling.
- Errors: explain the `message` in plain words and offer the obvious next step (for example, "That session has ended. Show results or start a new one?").
