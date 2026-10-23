# Wingu ☁️ — the AZ-900 coach that knows when you're guessing

> **Unofficial study tool.** Not affiliated with or endorsed by Microsoft. All questions are original, written against the public AZ-900 skills outline on Microsoft Learn (skills measured as of July 2026). No real exam questions are used.

*Wingu* means "cloud" in Swahili. Built for the PLP #1MillionDevs Vibe Coding Hackathon: AZ-900 Exam Prep Edition.

**Live demo:** `https://<your-username>.github.io/wingu/`
**Pitch deck:** `<link to your Canva deck>`

---

## The problem

When I studied for AZ-900, I kept "passing" practice quizzes without really knowing the material. A lucky guess counted the same as a real answer, so my scores looked better than my understanding. Explanations were dry, and I couldn't tell whether I was ready to book the exam.

*(Replace this paragraph with your own story: one specific moment from your AZ-900 prep.)*

## What Wingu does

Wingu combines four hackathon challenges into one learning loop:

| Challenge | Wingu feature |
|---|---|
| 🏠 (all) | **Home dashboard:** estimated readiness, three domain cards, a "Your next challenge" card that picks your weakest topic, and one-tap entry to every tool. |
| 📝 Smart Quiz Builder | **Practice:** 48 original questions across all three exam domains and 11 topics. Instant feedback, a clear explanation, and an everyday African analogy for every answer. |
| 🧠 Flashcard Coach | **Review:** a Leitner-style spaced-repetition queue. Wrong answers *and* lucky guesses go into Box 1 and return until you answer them right and sure. |
| 📊 Readiness Tracker | **Readiness:** a score weighted by each domain's share of the exam, plus per-domain bars, weakest topics, lucky guesses caught and a calibration stat ("right when you said Sure"). |
| 📅 Study Planner | **Study plan:** enter your exam date and weekly hours; Wingu splits time by exam weight × your weakness and adds an exam-week routine. |
| 🤖 AI Study Buddy | **Buddy prompt:** after any question, Wingu builds a tuned prompt with the question, your answer and your confidence, in your language (Swahili, Sheng, Yoruba, Hausa, isiZulu, Amharic and more) with examples from your country. |

### The unique idea: confidence-aware scoring

After choosing an answer, the learner taps **Sure**, **Think so** or **Guessing**.

| Result | Mastery value | What happens |
|---|---|---|
| Right + Sure | 1.0 | Moves up a review box |
| Right + Think so | 0.7 | Stays in Box 2 for one more check |
| Right + Guessing | 0.3 | **Lucky guess**: sent back to Box 1 |
| Wrong (any) | 0 | Box 1; "wrong and sure" is flagged as a misconception |

Mastery for each question is the average of its last two attempts. Readiness = Σ (domain mastery × domain weight), using the midpoints of the official ranges (25–30%, 35–40%, 30–35%). Wingu's "Book the exam" target is 80% overall and 70%+ in every domain — our own rule of thumb, not Microsoft's scoring.

### Cultural touches
- Every explanation ends with a real-life example: buying a minibus taxi versus paying per motorbike-taxi trip for CapEx vs OpEx, a mobile money PIN for MFA, a savings group's store for tags, county → ward → household for the Azure hierarchy.
- A short proverb with a study tip changes daily in the sidebar (for example, "Fix the crack now, or rebuild the wall later").

## Run it

It's a single HTML file with no build step and no backend.

```bash
git clone https://github.com/<your-username>/wingu.git
cd wingu
# open index.html in a browser, or:
python3 -m http.server 8000   # then visit http://localhost:8000
```

**Deploy to GitHub Pages:** repo → Settings → Pages → Source: `main` branch, `/ (root)` → Save.

**Tip for the demo:** go to Readiness → *Load sample progress* to show the dashboard and planner instantly.

Keyboard: `1–4` choose, `S` / `T` / `G` lock in confidence, `N` next.

## Tech and structure

- Vanilla HTML, CSS and JavaScript in `index.html`, organized in six labelled sections: content, state, quiz runner, study buddy, views, events.
- Progress is stored in `localStorage` (private to the learner's browser, works offline after first load).
- App layout: left sidebar on laptops; compact top bar and bottom tab bar on phones, with no sideways scrolling.
- Azure-and-navy design system defined as CSS tokens, with a matching dark mode, inline SVG icons and no image files.
- Keyboard support, visible focus states and reduced-motion support.
- Font: Plus Jakarta Sans (Google Fonts), with system fallbacks.

## How AI was used

Built with **Claude** (claude.ai) as pair programmer and content reviewer. See [`PROMPTS.md`](PROMPTS.md) for the prompts used to draft questions, check accuracy against the skills outline, and power the study buddy.

## Scaling beyond AZ-900

The question bank is a plain array with `domain`, `topic` and `weight`. Swapping in AI-900, SC-900 or AWS Cloud Practitioner means replacing `DOMAINS` and `QUESTIONS`; the scoring, review, readiness and planner work unchanged. Next steps: a Supabase backend for cohort leaderboards, a teacher view for PLP mentors, and community-submitted questions with peer review.

## Content accuracy

Questions were written against the AZ-900 study guide on Microsoft Learn and reviewed for accuracy. If you find an error, open an issue with the question ID (e.g. `a14`).

## Licence

MIT. Azure, Microsoft Entra and related names are trademarks of Microsoft, used here only to describe exam topics. No Microsoft logos are used.
