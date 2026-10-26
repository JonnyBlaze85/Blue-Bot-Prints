# Instant AI receptionist demo (Cloudflare Worker `bbp-demo`)

Live: https://bbp-demo.jblazzinc.workers.dev (embedded on bluebotprints.com at #try).
A salon owner types their website; the worker reads up to 5 pages, builds a signed fact sheet, and "Luna" answers as that salon's receptionist by chat or by voice.

- `src/app.js`: all logic (scan, chat, voice, greet). `src/demo.html`: the page. `src/index.js`: entry.
- `wrangler.toml`: Workers AI binding `AI`, voice `DEMO_VOICE` (any Deepgram Aura-2 English speaker). Secret `SIGNING_KEY` is set in the Cloudflare dashboard (never in this repo).
- Tests: `node test/test.mjs` (no network; models are mocked).
- Deploys: Cloudflare Workers Builds, root directory `_demo-worker`, on every push to `main`.
- The underscore keeps this folder out of the GitHub Pages website.

Connected to Cloudflare Workers Builds on Oct 22, 2026 (root directory /_demo-worker).

## Demo view counter (optional)

Tells Jarvis when a salon opens its personal demo link (`?site=their-site.com`).
Stores only the salon's website host plus counters (scans, link opens, chats, voice turns) and first/last time. No names, IPs or chat text. Expires after 90 days.

1. Cloudflare dashboard > Storage & Databases > KV > Create a namespace (name it `bbp-demo-views`).
2. Workers & Pages > bbp-demo > Settings > Bindings > Add > KV namespace: variable name `VIEWS`, pick that namespace.
3. Settings > Variables and Secrets > Add secret `VIEWS_KEY` (any long random string).
4. Read it: `GET /api/views` with header `x-views-key: <your key>`.

Without the binding everything works as before and nothing is counted. Opening a demo with `&preview=1` (Jonny checking his own link) is never counted.
