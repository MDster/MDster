<p align="center">
  <img src="assets/icon.png" alt="MDster" width="96" height="96">
</p>

<h1 align="center">MDster for AI assistants</h1>

<p align="center">
  Practise medical exam questions with your AI assistant: MCQs, short answers and SOE cases,<br>
  marked by MDster, explained step by step, and saved to your progress.
</p>

<p align="center">
  <a href="https://mdster.com/ai-assistants">Website</a> ·
  <a href="#install">Install</a> ·
  <a href="#what-you-can-do">What you can do</a> ·
  <a href="#privacy-and-data">Privacy</a> ·
  <a href="#support">Support</a>
</p>

---

[MDster](https://mdster.com) is a medical exam preparation platform for doctors and medical trainees. This repository is the official MDster plugin for **Claude** (Claude Code, Claude Desktop and claude.ai), **ChatGPT**, **Codex** and **Cursor**, plus Agent Skills for any assistant that reads them.

It connects your assistant to your own MDster account through the MDster MCP server at `https://mdster.com/mcp`, so you can practise MDster's questions in the chat, get them marked by MDster, and talk through the reasoning with your assistant.

> [!IMPORTANT]
> MDster is for **education and exam preparation only**. It is not medical advice, and it is not a substitute for clinical judgement, local guidelines or senior advice. Never enter patient information.

## What you can do

| | |
| --- | --- |
| 🩺 **Practise by exam and topic** | Multiple-choice questions (MCQ), short-answer questions (SAQ) and structured oral exam (SOE) cases, filtered by category, at your own pace |
| ✅ **Get marked by MDster** | Every answer is marked by MDster, with the correct answer, MDster's explanation and references |
| 💡 **Learn the why** | Your assistant explains the reasoning, why the other options are wrong, and the one take-away worth remembering |
| 📊 **See your results** | Score, grade and a breakdown by category and question type, saved to your MDster progress |
| 📅 **Questions of the day** | A few questions per speciality every day for every signed-in learner |

### Example prompts

- "Which MDster exams can I practise?"
- "Start 10 pharmacology MCQs for my anaesthesia exam."
- "Give me a short-answer question on airway management."
- "Run an SOE case for me, one part at a time."
- "Explain why option C is wrong."
- "How did I do? What should I revise next?"

### How it looks

The included skills tell your assistant to present practice as clear cards that read well on a phone:

```text
🩺 Anaesthesia Core · Pharmacology        Question 3 of 10 · MCQ
> A 64-year-old man is given ...

Mark each statement true or false (select all that are true):
  A. ...   B. ...   C. ...   D. ...   E. ...
```

```text
✅ Correct · score 1/1
Why: MDster's explanation, in short points
Why not the others: option by option
📚 References: as provided by MDster
💡 Take-away: the one fact to remember
Next: Next question · Explain more · Show results
```

Where your assistant supports interactive choices, it offers the answer options and next steps as buttons, so you can tap instead of typing.

## Install

You need an [MDster](https://mdster.com) account with a verified email. You sign in to MDster with OAuth the first time the assistant uses a tool.

**Claude Code**

```text
/plugin marketplace add MDster/MDster
/plugin install mdster@mdster
```

**Codex**

```text
codex plugin marketplace add MDster/MDster
codex plugin add mdster@mdster
```

**Cursor**: [add the MDster MCP server](https://cursor.com/install-mcp?name=mdster&config=eyJ1cmwiOiJodHRwczovL21kc3Rlci5jb20vbWNwIn0=).

**Claude (claude.ai and Claude Desktop) and ChatGPT**: install MDster from the assistant's directory, or add a custom connector with the URL `https://mdster.com/mcp`. Step-by-step guides: [Claude](https://mdster.com/ai-assistants/claude) · [ChatGPT](https://mdster.com/ai-assistants/chatgpt).

**Skills only** (any assistant that reads Agent Skills):

```text
npx skills add MDster/MDster
```

The skills need the MDster connection to work, so add the MCP server too.

## What this plugin contains

| Part | Purpose |
| --- | --- |
| MCP connection | The MDster server at `https://mdster.com/mcp` (Streamable HTTP, OAuth 2.1 with PKCE) |
| `working-with-mdster` skill | The rules for safe practice (questions shown exactly, answers never revealed early, education only) and the card layouts for questions, feedback and results |
| `mdster-practice-session` skill | A full session, from choosing the exam and topic to the results |
| `mdster-daily-questions` skill | The questions of the day, one at a time |
| `mdster-results-review` skill | A results dashboard with strengths, areas to revise and a suggested next session |

### Tools

| Tool | What it does | Changes data |
| --- | --- | --- |
| `list-exams` | Lists your specialities and exams and your access to each | No |
| `get-exam-options` | Shows the question types and categories for an exam | No |
| `start-practice` | Starts a practice session with the type, category and number of questions you choose | Yes: replaces an unfinished session for that exam started from an assistant (answers already given stay in your stats) |
| `get-question` | Shows the current question, without its answer | No |
| `submit-answer` | Sends your answer for marking and returns the score, correct answer and explanation | Yes, your answer |
| `next-question` | Moves to the next question | Yes, your session position |
| `get-results` | Finishes the session and returns your results | Yes, saves the session to your progress |
| `get-daily-questions` | Shows the questions of the day for a speciality | No |
| `answer-daily-question` | Marks your answer to a question of the day | Yes, your answer |

Every tool works only inside your own MDster practice and reaches no other service. Only `start-practice` replaces anything: an unfinished assistant session for the same exam, so your assistant checks with you first.

## Privacy and data

- You choose to connect by signing in to MDster and approving the connection. You can disconnect at any time from your assistant's settings.
- MDster receives only the tool requests your assistant sends: never your conversation, chat history or files.
- Your assistant receives the questions, your answers, scores, explanations and access information it needs. It never sees your password or payment details.
- MDster never asks for patient information. Do not enter any.

Details: [Privacy Policy](https://mdster.com/privacy) (section 6.1) · [Terms of Service](https://mdster.com/terms) (section 6.3) · [AI Transparency Notice](https://mdster.com/ai-transparency).

## Limitations

- Practice covers the exams, question types and categories available on your MDster account. OSCE stations are not available in assistants.
- Full practice for an exam uses the access on your MDster account; without it, the questions of the day are available.
- Short answers are marked by AI, with an hourly limit on submissions.
- Your assistant writes its own wording around MDster's content. MDster's questions, answers and explanations are returned exactly; anything else the assistant adds is its own and may be wrong.
- Results reflect practice performance, not a prediction of a real exam result.

## Support

- Help and setup guides: https://mdster.com/ai-assistants
- Contact: https://mdster.com/contact · support@mdster.com

## License

The plugin files in this repository (manifests and skills) are released under the [MIT License](LICENSE). MDster's questions, answers, explanations and other content are not part of this repository and remain the property of Anesthesia Zone, LLC (d/b/a MDster); they are available only through your MDster account under the [Terms of Service](https://mdster.com/terms).
