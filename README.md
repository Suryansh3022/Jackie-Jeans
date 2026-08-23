Jackie Jeans — Smart Fit Onboarding

A mobile-first onboarding experience for Jackie Jeans built with two complete flows — manual and AI voice — that guide a new customer through the Jackie Jeans Fit Quiz and hand them off to the main product.

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

Both flows redirect to **https://jackie-jeans-ten.vercel.app/** on completion, with the full fit profile base64-encoded in the URL so the main site can read it.

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

No npm, no bundler, no environment variables. One file.

---

## Project Structure

```
index.html        ← entire app (HTML + CSS + JS in one file)
README.md         ← this file
```

---

## How to Deploy

### Option A — Vercel (recommended)

```bash
npm i -g vercel     # install CLI once
vercel              # run from this folder, accept defaults
```

Or drag-and-drop the folder at **https://vercel.com/new → Import → Deploy**.

### Option B — Netlify Drop

1. Go to **https://app.netlify.com/drop**
2. Drag this folder onto the page
3. Copy the live link — done

No build command. No publish directory to configure. It's a static file.

---

## Browser Support

| Browser | Manual | Voice |
|---|---|---|
| Chrome (desktop) | ✅ | ✅ Best |
| Chrome (Android) | ✅ | ✅ |
| Safari (iOS) | ✅ | ⚠️ Limited — app detects this and offers manual instead |
| Firefox | ✅ | ❌ No SpeechRecognition — falls back to manual |
| Edge | ✅ | ✅ |

The app checks for speech recognition support on load. If unavailable, the Voice option shows a clear message and the user can switch to the manual flow with one tap.

---

## How the Code Works

### Single source of truth
All 10 quiz questions live in one `BASE_QUESTIONS` array. Both flows read from it — so a question changed once updates everywhere.

### Dynamic Q9
`buildSteps()` inserts a size question for every brand the user selected in Q8, right before the final question. If they pick 3 brands, they get 3 size questions. If they pick none, Q9 is skipped entirely.

### Manual flow
`renderManual()` draws the current question, `onManualNext()` validates and saves the answer, increments `state.step`, and re-renders. No framework — just state → innerHTML.

### Voice loop
```
speak(question) → listen() → parseVoiceAnswer() → confirm() → next step
                                    ↓ (fail x2)
                              showFallback() — tap chips
```

### Answer parsing
Each question type has its own parser. Heights like "five foot six" are regex-matched word by word, converted to total inches, then snapped to the nearest valid dropdown value. Fit preferences match on keywords: "snug", "relax", "tight", "high", "mid", "low".

### Handoff
On completion, `state.answers` is JSON-stringified, base64-encoded, and appended to the Jackie Jeans URL as `?fitProfile=...`. The main site can decode and read it to pre-fill a recommendation.

---

## Quiz Questions Covered

| # | Question | Input type |
|---|---|---|
| 1 | Height | Dropdown 4'10" – 6'2" |
| 2 | Weight (optional) | Number entry or skip |
| 3 | Waist measurement | Dropdown 24" – 52" |
| 4 | Hip measurement | Dropdown 32" – 60" |
| 5 | Waist fit preference | 3-option choice |
| 6 | Rise preference | 3-option choice |
| 7 | Thigh fit preference | 3-option choice |
| 8 | Previous brands | Multi-select chips (20 brands) |
| 9 | Size per selected brand | One text input per brand from Q8 |
| 10 | Biggest fit frustration | 6-option choice |

All 10 are present in both flows. No questions dropped.





