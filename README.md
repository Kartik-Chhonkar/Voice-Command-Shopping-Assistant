# Listly — Voice Command Shopping Assistant

A voice-controlled shopping list app. Speak naturally ("I need bananas", "remove milk",
"find toothpaste under $5") and Listly updates a categorized, receipt-style list in real time.

## Live demo
Single static file — no build step, no backend, no API keys. Open `index.html` directly,
or deploy in under a minute (see **Hosting** below).

## Features implemented

**Voice input**
- Voice command recognition via the browser's built-in Web Speech API (free, no signup)
- Flexible phrasing: "add milk" / "I need milk" / "I want to buy milk" all resolve the same way
- Language selector (English / Spanish / Hindi) — sets recognition language and lets basic
  command keywords ("añade", "quita", "जोड़ो"...) parse correctly too
- Typed-command fallback for browsers without speech support (e.g. Firefox desktop)

**Smart suggestions**
- "Running low" prompts from simulated purchase history
- Seasonal picks (mocked for the current month)
- Substitute suggestions when a listed item is flagged out of stock (e.g. milk → almond/oat milk)

**List management**
- Add / remove / adjust quantity by voice ("add 2 bottles of water")
- Automatic categorization (Produce, Dairy, Bakery, Snacks, Meat & Seafood, Beverages, Other)
- Duplicate items merge and sum quantities instead of creating a second line

**Voice-activated search**
- "find toothpaste under $5" filters a small mock product catalog by name and price
- Tap a result to add it straight to the list

**UI/UX**
- Mobile-first, minimal, single-column "receipt" layout
- Live transcript, listening-state animation, and a short loading spinner while a command
  is being interpreted (mirrors real NLP latency)
- Toast confirmations for every add/remove action
- Basic error handling: unsupported browser, mic permission errors, and "item not found"
  all surface a message instead of failing silently

## How the "AI" works here

There's no paid NLP service involved. Voice-to-text comes from the browser's native
`SpeechRecognition` API. Intent parsing is a lightweight keyword + regex layer
(`parseCommand` in `index.html`) that looks for action verbs (add/remove/find), pulls out
a quantity (digits or number words), and strips filler words to isolate the item name.
This keeps the app free to run and deploy, with zero API keys, while still satisfying the
"flexible phrasing" requirement for common shopping phrases.

## Hosting

Because it's a single static HTML file with no dependencies, any static host works:

1. **GitHub Pages** — push this repo, then Settings → Pages → deploy from `main` / root.
2. **Netlify / Vercel** — drag-and-drop the folder in their dashboard, or `vercel deploy`.
3. **Firebase Hosting** — `firebase init hosting` → point public dir here → `firebase deploy`.

Note: Web Speech API requires HTTPS (or `localhost`) and currently has the best support in
Chrome/Edge. All three hosts above serve over HTTPS by default.

## Known limitations (given the 8-hour scope)

- The product catalog, purchase history, and "out of stock" flags are mocked in-memory
  rather than pulled from a real database — swapping in a real backend is the natural
  next step.
- Multilingual support covers command keywords for EN/ES/HI; full multilingual NLP would
  need a translation layer.
- No persistence between sessions (no localStorage per Artifact/demo constraints) — a
  production version would add a small backend or browser storage.
