# Rules for eman-deutsch (Eman's app)

The engine rules in `karteikarten-engine/CLAUDE.md` apply here in full. This file adds what is specific to this app.

## What this repo holds
- `index.html`: everything personal: `lang="ar" dir="rtl"`, title "كروت ألماني", header "كلمات ألماني", home-screen
  name "Deutsch", green "Aä" icon, her palette and fonts, all UI texts in Egyptian Arabic (`window.APP.t`), card
  `fields` (with `tr`, the Arabic translation of the example), Gemini `rules`, `phrases`, `practice`, `remind` with
  Arabic number forms (`num()` helper), public `vapid` key. The engine is loaded from `/karteikarten-engine/app.js`
  with a `?v=` cache buster through the `data-loader` script tags (keep them; the tools skip them).
- `cards.js`: her word list (storage key `kk-eman-v2`, migrate from `wohnen-cards-v1` on first start), one card per
  line. `manifest.json`, `sw.js` (Arabic fallbacks), `.github/workflows/remind.yml`.
- Branch `progress`: `progress.json`, `push.json`, `sent.json`. Never edit by hand unless asked.

## Rules
1. **Language**: every text is Egyptian Arabic (عامية مصرية), not Modern Standard Arabic, addressed to her in the
   feminine (اعملي، قوليها، متأكدة إنك). Gemini rules say the same for everything Arabic Gemini writes (`ar`, `tr`,
   `note`, practice tasks and tips). German stays only in card content and tech names (GitHub, Gemini, token).
   The engine's e2e check "No German UI text in any captured state" guards this; a new text key must be added here
   in Arabic in the same change as the German one in de-karteikarten.
2. **RTL**: the page is `dir="rtl"`; German text is marked `.de` (LTR, isolated); inputs use `dir="auto"`. Check new
   layouts in the RTL screenshots of the e2e suite before pushing.
3. The inline `<script>` blocks must run in Node's `vm` without `document` (the reminder executes them): only
   `window.APP = { … }` and small pure helpers like `num()`.
4. Gemini rules: the learner is Egyptian, input may be German, English or Arabic; `tr` translates the example
   naturally; `note` only for a real trap, in Egyptian Arabic, feminine, never about the scanned sheet; `ex` uses the
   target word in the needed form, every part bold.
5. Colours for new UI states must stay distinct from her teal accent (`--accent`) and from the correct/again
   greens and reds.
6. Changes go through a branch and a PR; merge when the user says so. Secrets only in repository secrets or on the
   phone. Before a PR, run the engine's `npm test` with this checkout next to the engine.
