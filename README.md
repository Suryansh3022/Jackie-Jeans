### Jackie Jeans — Smart Fit Onboarding

A mobile-first onboarding experience for Jackie Jeans built as part of the Humanity Founders Hackathon challenge. Two complete flows — manual and AI voice — that guide a new customer through the Jackie Jeans Fit Quiz and hand them off to the main product.

---

## What's Built

### Flow 1 — Manual Onboarding
A clean, step-by-step form experience optimised for mobile.

- One question at a time with a denim-stitch progress bar
- Correct input type per question — dropdowns, button choices, chip multi-select, number entry
- Weight question is skippable with zero friction
- Brand multi-select (Q8) dynamically injects one size question per brand selected (Q9)
- Validation on every step with clear error messages
- Back button lets users review and edit any previous answer
- Completion screen with a fit summary, then redirect to Jackie Jeans

### Flow 2 — AI Voice Onboarding
A genuine voice-to-voice conversation that replaces the form entirely.

- AI speaks each question naturally using the browser's Text-to-Speech engine
- User answers out loud — no typing required
- Speech recognition converts spoken answers to structured data in real time
- Parses natural language: "five foot six" → 5'6", "about thirty inches" → 30", "high rise" → High rise
- Handles multi-brand answers in one sentence: "Levi's, Madewell, and Gap"
- Skipping weight feels natural: just say "skip" or "prefer not to"
- Confirms each answer out loud before moving on
- Falls back to tappable chips after 2 failed recognition attempts — never gets stuck
- Repeat question and Switch to typing buttons always available

Both flows redirect to **https://jackie-jeans.vercel.app/** on completion, with the full fit profile base64-encoded in the URL so the main site can read it.

---

## Tech Stack

| Layer | Choice | Why |
|---|---|---|
| Framework | Vanilla HTML/CSS/JS | Zero build step — deploy a single file |
| Fonts | Fraunces (display) + Inter (body) | Premium, editorial feel via Google Fonts |
| Speech output | Web Speech API — `SpeechSynthesisUtterance` | Free, no API key, works in all modern browsers |
| Speech input | Web Speech API — `SpeechRecognition` | Free, no API key, best support in Chrome |
| Hosting | Vercel / Netlify | Static drop — live in under 2 minutes |
| Backend | None | Everything runs client-side |

No npm, no bundler, no environment variables.

---

## Project Structure

```text
Jackie-Jeans/
│
├── index.html        ← Main HTML structure and application entry point
├── style.css         ← Complete styling, layout, animations and responsive design
├── script.js         ← Quiz logic, manual flow, voice flow and fit-profile handling
└── README.md         ← Project documentation
