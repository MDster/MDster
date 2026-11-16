# Question types

## MCQ (multiple true/false)

- Each MDster MCQ has lettered options, and **each option is true or false**. The learner selects every option they think is true; unselected options count as false.
- Submit with `submit-answer` (or `answer-daily-question`) and `true_options`: the letters the learner marked true, for example `["A", "D"]`. An empty list means the learner marked every option false.
- The score runs from 0 to 1 and gives credit per option, so a partly right answer scores between 0 and 1.
- After marking, every option has `is_correct` and may have its own `explanation`. `correct_options` lists the true letters.
- If the learner replies in words ("the first and last"), map them to letters and confirm the letters back in your feedback card.

## SAQ (short answer)

- The learner writes their own answer. Submit it unchanged as `text_answer`: no corrections, additions or formatting.
- MDster marks it against its model answer. The result can include `feedback` from the marker and an `assessment_note` when the mark is still provisional.
- After marking, compare the learner's answer with `model_answer` point by point, then teach from `explanation`.
- Short answers are marked by AI, and there is an hourly limit on how many can be submitted (`rate_limited`). If it is reached, suggest MCQs meanwhile.

## SOE (structured oral exam cases)

- An SOE case is a short clinical scenario (`soe_case`) followed by parts, asked one at a time. Each part is answered like an MCQ or an SAQ, according to its `type`.
- Keep the case title visible on every part, and present the parts as a viva: "Part 2: the examiner now asks…".
- Do not reveal later parts or the case outcome early. Each part's feedback card can end with "Next part" instead of "Next question".

## Questions of the day

- Every signed-in learner can answer a few MCQs per speciality each day (`get-daily-questions`), the same for everyone, refreshed at 00:00 UTC.
- Each can be answered once per day. Already answered ones come back with their answers and `answered_today: true`.
