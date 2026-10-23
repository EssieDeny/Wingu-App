# Wingu ☁️ — The AZ-900 Coach That Knows When You're Guessing

> **An unofficial study tool.** Wingu is not affiliated with or endorsed by Microsoft. Its original practice questions are designed around the public AZ-900 skills outline in the [official Microsoft AZ-900 study guide](https://learn.microsoft.com/credentials/certifications/resources/study-guides/az-900) (skills measured as of July 20, 2026). It does not use real exam questions or Microsoft logos.

Wingu means "cloud" in Swahili. Built for the PLP #1MillionDevs Vibe Coding Hackathon: AZ-900 Exam Prep Edition.

**Live demo:** https://essiedeny.github.io/Wingu-App/  
**Source code:** https://github.com/EssieDeny/Wingu-App  
📄 [Pitch and demo notes](PITCH.md)  
🧠 [Prompt engineering notes](PROMPTS.md)

<!-- Add your presentation link here when the deck is ready, for example:
🎤 [Pitch presentation](https://your-presentation-link)
-->

---

## The problem

Preparing for a cloud fundamentals exam involves more than remembering definitions or selecting the correct answer. A learner can answer correctly by guessing and still misunderstand the underlying concept. Practice scores alone may not reveal that gap, and learners can struggle to decide which topics deserve more revision.

Wingu was designed around this learning problem. It helps learners reflect on their confidence, revisit incorrect answers and lucky guesses, and use progress across exam domains to guide their revision. The goal is to encourage genuine understanding rather than simply chasing a high quiz score.

## What Wingu does

Wingu brings five learning tools together in one study experience, covering four of the hackathon challenges plus a home dashboard that connects them:

| Hackathon challenge | In the app | What it does |
|---|---|---|
| — | **Home** | Shows estimated readiness, progress in each of the three exam domains, a "Your next challenge" card that picks your weakest topic, and one-tap access to every tool. |
| Smart Quiz Builder | **Practice** | Offers 48 original practice questions across three exam domains and 11 topics, with instant feedback, an explanation for every answer, and a relatable real-life example. Answer options are shuffled each time, and unseen questions come first. |
| Flashcard Coach | **Review** | A spaced-repetition review queue with three boxes. Incorrect answers and lucky guesses go to Box 1 and return until you answer them correctly and confidently. Each card shows why it is back: *Wrong but sure*, *Missed last time* or *Lucky guess*. |
| Readiness Tracker | **Readiness** | Estimates readiness using domain-weighted mastery, shows a score for each domain, highlights weaker topics, suggests next steps, and tracks confidence calibration ("Right when you said Sure"). |
| Study Planner | **Study plan** | Uses your exam date, weekly study hours and weaker areas to build a week-by-week plan, with a "Start here" task and an exam-week routine. Tap any topic in the plan to practise it. |
| AI Study Buddy | **Study buddy prompt** (inside each question) | Creates a ready-to-copy prompt using the question, your answer and your confidence level. You can choose the explanation language (English, Swahili, Sheng, Yoruba, Hausa, Igbo, isiZulu, Amharic, Luganda, Kinyarwanda or French) and the country for examples. |

### The key idea: confidence-aware learning

After answering a question, learners choose **Sure**, **Think so**, or **Guessing**. This adds context to the result instead of treating every correct answer as proof of mastery.

| Result | Mastery value | What happens |
|---|---:|---|
| Correct + Sure | 1.0 | Moves up a review box |
| Correct + Think so | 0.7 | Stays in Box 2 for another confidence check |
| Correct + Guessing | 0.3 | Flagged as a lucky guess and returned to Box 1 |
| Incorrect, any confidence | 0 | Returned to Box 1; incorrect answers marked Sure are flagged as a likely misconception |

### How the readiness estimate is calculated

- Mastery for each question is the average of its last two attempts.
- Domain mastery is the average mastery of all questions in that domain (unseen questions count as 0).
- Each domain is given the midpoint of its official exam-weight range. These midpoints total 97.5, so the code **normalises** them: each weight is divided by 97.5 before it is applied. The effective weights therefore add up to 100%.

| Exam domain | Official weight range | Midpoint used | Effective weight after normalising |
|---|---|---:|---:|
| Describe cloud concepts | 25–30% | 27.5 | 28.2% |
| Describe Azure architecture and services | 35–40% | 37.5 | 38.5% |
| Describe Azure management and governance | 30–35% | 32.5 | 33.3% |

In the code (`readiness()` in `index.html`):

```js
const total = Object.values(DOMAINS).reduce((s, d) => s + d.w, 0); // 97.5
return Object.entries(DOMAINS).reduce((s, [k, d]) => s + domainMastery(k) * d.w / total, 0);
```

A learner with full mastery in every domain therefore scores exactly 100%.

Wingu's suggested readiness target is an **80% overall estimate and at least 70% in each domain**. These are Wingu's own study guidelines, not Microsoft's scoring, and they do not guarantee exam success.

**About the real exam score:** Microsoft reports technical exam scores on a scale of 1 to 1,000, and a passing score is **700 or greater**. Because this is a scaled score, 700 does not necessarily equal 70% of the available points. See Microsoft's [exam scoring and score reports](https://learn.microsoft.com/en-us/certifications/exam-scoring-reports) page.

## Learning through relatable examples

Wingu uses everyday examples to make cloud concepts easier to understand, including:

- Multi-factor authentication explained through a mobile money PIN.
- Capital expenditure versus operating expenditure through transport choices: buying a minibus taxi versus paying per motorbike-taxi trip.
- Azure resource hierarchy through familiar administrative structures: county → ward → household.
- Resource tags through labelled boxes in a community savings group's store.
- Short study tips and proverbs in the sidebar to encourage consistent revision.

## Getting started

Wingu is a static web app built with HTML, CSS, and JavaScript. It requires no build step or backend server.

**Option 1: Run it locally**

1. Download or clone the repository.
2. Open `index.html` in a modern web browser.

Or use a local server:

```bash
git clone https://github.com/EssieDeny/Wingu-App.git
cd Wingu-App
python3 -m http.server 8000
```

Then open `http://localhost:8000` in your browser.

**Option 2: Use the live demo**

Visit https://essiedeny.github.io/Wingu-App/

**Deploying your own copy to GitHub Pages:** in the repository, go to **Settings → Pages**, set the source to the `main` branch and the `/ (root)` folder, then select **Save**.

**Demo tip:** for a presentation, select **Load a demo learner** on the Readiness page (it also appears on Home before any questions have been answered). This fills the dashboard, readiness report and study plan with example progress, so you can demonstrate them without completing a full quiz first. Use **Reset my progress** at the bottom of the page (tap twice to confirm) to start again.

**Keyboard shortcuts:** `1`–`4` choose an answer, `S` / `T` / `G` choose Sure, Think so or Guessing, and `N` moves to the next question.

## Technology and design

- **Frontend:** Vanilla HTML, CSS, and JavaScript in a single `index.html`, with no framework or build step.
- **Code structure:** the script is organised into six labelled sections: content (domains and questions), state, quiz runner, study buddy, views, and render and events.
- **Storage:** Browser `localStorage` saves learner progress locally. The app works offline after the first load.
- **Layout:** a left sidebar on laptops; a compact top bar and bottom tab bar on phones, with no sideways scrolling.
- **Accessibility:** Keyboard support, visible focus states, and reduced-motion support.
- **Appearance:** Azure-inspired colours defined as design tokens, a matching dark mode, inline SVG icons (no image files), and the Plus Jakarta Sans font with system-font fallbacks.

Progress is stored in the learner's browser and is not synchronised between devices.

## Project files

| File | Purpose |
|---|---|
| `index.html` | The complete app: questions, logic, styles and layout |
| `README.md` | This guide |
| `PROMPTS.md` | Prompts used to write questions, check accuracy and power the study buddy |
| `PITCH.md` | Slide-by-slide pitch script and live demo steps |
| `LICENSE` | MIT License |

## How AI was used

Claude (claude.ai) was used as a pair-programming and content-development assistant during the project. AI was used in three ways, each documented in the [prompt engineering notes](PROMPTS.md):

1. **Question writer:** drafting original questions, explanations and examples against the AZ-900 skills outline.
2. **Accuracy reviewer:** a separate review prompt that checks each answer key and explanation.
3. **Study buddy prompt:** the prompt the app builds for learners to paste into an AI assistant.

The AI Study Buddy feature prepares a prompt for further exploration; it does not mean that a separate AI service is built into the app.

## Future possibilities

Wingu could be extended to support other entry-level cloud certifications, such as AI-900, SC-900 or AWS Cloud Practitioner, by replacing the `DOMAINS` and `QUESTIONS` data in `index.html`. The scoring, review queue, readiness estimate and study planner work unchanged with a new question bank.

Possible future improvements include a backend (such as Supabase) for shared progress across devices, mentor dashboards for study groups, daily review reminders, and community-contributed questions reviewed for accuracy.

## Content accuracy

Practice questions are original learning materials informed by the AZ-900 skills outline in the [official Microsoft AZ-900 study guide](https://learn.microsoft.com/credentials/certifications/resources/study-guides/az-900) (skills measured as of July 20, 2026). Microsoft may update its exam objectives, so learners should also consult the current version of that study guide.

If you find an issue, please open a GitHub issue and include the relevant question ID where possible (for example, `a14`).

## Licence

This project is released under the MIT License. Microsoft, Azure, and Microsoft Entra are trademarks of Microsoft and are referenced only to describe the exam topics. No Microsoft logos are used.
