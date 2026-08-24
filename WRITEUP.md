# Approach write-up (200 words)

I built Listly as a single static HTML file so it needs no backend, no build step, and no
paid API keys — just the browser's native Web Speech API for voice-to-text, which keeps
hosting trivial (any static host works) and satisfies the "free tier only" constraint by
using no external service at all.

Intent parsing is a lightweight keyword + regex layer rather than a full NLP model: it
looks for action verbs (add/remove/find), extracts quantity from digits or number words,
and strips filler phrases to isolate the item name. This handles the flexible phrasing in
the brief ("add milk" vs. "I want to buy milk") without external dependencies, while
staying transparent and easy to extend.

Categorization, seasonal suggestions, "running low" prompts, and substitute recommendations
are driven by small local dictionaries and a mock purchase-history array — realistic stand-ins
for what would be a recommendation service and product database in production.

The UI is a mobile-first, receipt-styled single list with live transcript feedback, a
listening-state animation on the mic button, and a short loading state while a command is
interpreted, to make the voice interaction feel responsive rather than instantaneous.

Given the 8-hour cap, I prioritized a working, coherent core experience over breadth —
real persistence and a live product API are the clear next steps.
