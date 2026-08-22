# Jackie-Jeans
 A mobile-first onboarding experience for Jackie Jeans, it has two complete flows — manual and AI voice — that guide a new customer through the Jackie Jeans Fit Quiz and hand them off to the main product.
 What’s Built
Flow 1 — Manual Onboarding
A clean, step-by-step form experience optimized for mobile.
	•	One question at a time with a denim-stitch progress bar
	•	Correct input type per question — dropdowns, button choices, chip multi-select, number entry
	•	Weight question is skippable with zero friction
	•	Brand multi-select (Q8) dynamically injects one size question per brand selected (Q9)
	•	Validation on every step with clear error messages
	•	Back button lets users review and edit any previous answer
	•	Completion screen with a fit summary, then redirect to Jackie Jeans
Flow 2 — AI Voice Onboarding
A genuine voice-to-voice conversation that replaces the form entirely.
	•	AI speaks each question naturally using the browser’s Text-to-Speech engine
	•	User answers out loud — no typing required
	•	Speech recognition converts spoken answers to structured data in real time
	•	Parses natural language: “five foot six” → 5’6”, “about thirty inches” → 30”, “high rise” → High rise
	•	Handles multi-brand answers in one sentence: “Levi’s, Madewell, and Gap”
	•	Skipping weight feels natural: just say “skip” or “prefer not to”
	•	Confirms each answer out loud before moving on
	•	Falls back to tappable chips after 2 failed recognition attempts — never gets stuck
	•	Repeat question and Switch to typing buttons always available
