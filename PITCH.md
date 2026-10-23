# Wingu pitch — slide script (about 4 minutes)

Use these with the hackathon's Canva template. Each slide maps to a pitch judging criterion.

---

### Slide 1 — Title
**Wingu: the AZ-900 coach that knows when you're guessing**
Your name · PLP Software Engineering · #1MillionDevs
*Say:* "Wingu means cloud in Swahili. It helps the next cohort pass AZ-900 by catching the thing that fooled me: lucky guesses."

### Slide 2 — Problem (Problem Understanding, 20%)
- Practice scores lie: a guess that lands counts the same as real knowledge.
- Explanations are abstract and feel far from our everyday life.
- Learners don't know when they're ready to book.
*Say:* tell your real moment. Example: "I scored 80% on a practice test, booked the exam, then realised I'd guessed half the storage questions."

### Slide 3 — Who it's for (Target Users, 15%)
- PLP and #1MillionDevs learners taking AZ-900, often studying on a phone, on limited data, in the evenings.
- Career switchers and non-technical learners new to cloud.
- Mentors who want to see where a cohort is weak (next phase).

### Slide 4 — Solution (Solution & Product, 25%)
One loop, four tools:
1. **Practice** with confidence: Sure / Think so / Guessing
2. **Review** brings back wrong answers *and* lucky guesses
3. **Readiness** weighted by the real exam domains
4. **Study plan** from your exam date and weak areas
Plus a **study buddy prompt** in Swahili, Sheng, Yoruba, Hausa, isiZulu and more.

### Slide 5 — Live demo (90 seconds)
1. Answer a question, tap **Guessing**, get it right → "Lucky guess" → it lands in Review.
2. Show the minibus taxi / motorbike taxi example for CapEx vs OpEx.
3. Open **Ask a study buddy** → switch language to Swahili → copy prompt → paste into Claude.
4. Readiness → **Load sample progress** → ring, domain bars, "Right when you said Sure".
5. Study plan → change exam date → plan updates.

### Slide 6 — How it's built (technical creativity / prompt engineering)
- Single-file web app, no backend, works offline after load, light & dark, phone-first.
- 48 original questions mapped to the July 2026 skills outline.
- AI used three ways: question writer, independent accuracy reviewer, live study buddy prompt (see PROMPTS.md).

### Slide 7 — Impact & scale (20%)
- Swap the question bank to support AI-900, SC-900, AWS Cloud Practitioner: scoring, review, readiness and planner stay the same.
- Next: Supabase backend for cohort dashboards, mentor view, community questions with peer review, daily WhatsApp review reminders.
- Low data, mobile-first: built for how African learners actually study.

### Slide 8 — Close
"Little by little fills the measure. Wingu makes every little bit of study count."
GitHub link · live demo link · QR code to the demo

---

## Likely judge questions
- **Is the content accurate?** Written against the official outline, then checked by a separate review prompt; every question shows its explanation so errors are visible and reportable by ID.
- **Why not just show percent correct?** Because a guessed right answer isn't knowledge. Confidence-weighted mastery and "Right when you said Sure" measure what you actually know.
- **Is it official?** No. Labelled unofficial, original questions, no Microsoft logos.
