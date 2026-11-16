# Tools reference

All tools act for the signed-in learner only and change nothing outside their MDster practice. Read-only tools: `list-exams`, `get-exam-options`, `get-question`, `get-daily-questions`.

| Tool | Inputs | Returns |
| --- | --- | --- |
| `list-exams` | none | `specialities[]`, each with `speciality` (`id`, `name`) and `products[]` (`id`, `name`, `pathway`, `questions_count`, `access`) |
| `get-exam-options` | `product_id` | `question_types[]` (`value`, `name`), `categories[]` (`id`, `name`), `access`, `max_questions_per_session` |
| `start-practice` | `product_id`, `question_type` (`mcq`, `saq` or `soe`), optional `category_id`, optional `number_of_questions` | The session state with the first `question`, `progress` (`question`, `of`), and a `note` when the session is shorter than requested |
| `get-question` | `product_id` | The session state with the current `question` |
| `submit-answer` | `product_id`, `question_id`, and `true_options` (MCQ) or `text_answer` (SAQ) | The session state with the marked `question` (`correct_options` or `model_answer`, `explanation`, `references`) and `result` (`score`, `feedback`, `assessment_note`) |
| `next-question` | `product_id` | The next `question`, or `is_finished: true` |
| `get-results` | `product_id` | `overall_percent`, `grade`, `total_questions`, `answered_questions`, `correct_count`, `partial_count`, `incorrect_count`, `best_streak`, `benchmark_avg`, `category_breakdown`, `type_breakdown` |
| `get-daily-questions` | `speciality_id` | `speciality`, `date_utc`, `remaining`, `questions[]` (each with `answered_today`) |
| `answer-daily-question` | `speciality_id`, `question_id`, `true_options` | The score, the correct options and MDster's explanation |

## Sessions

- One practice session per exam product in the assistant. `start-practice` replaces an unfinished one for the same exam (sessions on the website are separate), so check with the learner before starting over a session in progress.
- `get-results` finishes the session: unanswered questions score 0, and the session is saved to the learner's MDster progress. Only call it when the learner is done or asks for results.
- A `next_step` field in a reply says which tool continues the session.

## Errors

| `error` | Meaning | What to do |
| --- | --- | --- |
| `unknown_product`, `unknown_speciality`, `unknown_category` | The ID is not valid | Call `list-exams` or `get-exam-options` again |
| `no_session` | No session for this exam | Offer to start one |
| `not_current_question` | The answer was for another question | Show the current question (`get-question`) |
| `already_answered` | This question is marked | Offer the next question |
| `not_answered` | Moving on before answering | Ask for the learner's answer, or offer to show results |
| `session_finished` | The session has ended | Offer results or a new session |
| `invalid_options` | Letters do not match the options | Ask again using the letters shown |
| `not_a_daily_question` | Not one of today's questions | Call `get-daily-questions` |
| `rate_limited` | Too many requests or short answers | Wait, or switch to MCQs |
| `trial_question_limit` | This account's new-question allowance for the day is used | Say when more are available (`next_available_at`) |
| `bundle_not_practicable` | A bundle ID was used | Practise with the pathway's own product ID |
| `access: members_only` | The exam needs full access | Relay `message`; offer the questions of the day when available |
