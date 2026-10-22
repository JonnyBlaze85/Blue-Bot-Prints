# Instant AI receptionist demo (Cloudflare Worker `bbp-demo`)

Live: https://bbp-demo.jblazzinc.workers.dev (embedded on bluebotprints.com at #try).
A salon owner types their website; the worker reads up to 5 pages, builds a signed fact sheet, and "Zuri" answers as that salon's receptionist by chat or by voice.

- `src/app.js`: all logic (scan, chat, voice, greet). `src/demo.html`: the page. `src/index.js`: entry.
- `wrangler.toml`: Workers AI binding `AI`, voice `DEMO_VOICE` (any Deepgram Aura-2 English speaker). Secret `SIGNING_KEY` is set in the Cloudflare dashboard (never in this repo).
- Tests: `node test/test.mjs` (no network; models are mocked).
- Deploys: Cloudflare Workers Builds, root directory `_demo-worker`, on every push to `main`.
- The underscore keeps this folder out of the GitHub Pages website.
