# Sprechpartner

German speaking practice with no audience. Browser does the ears and the voice, Gemini does the talking and the corrections.

Built for one problem: B1 on paper, frozen in the room. The partner never comments on your mistakes mid-conversation — corrections collect quietly in a side ledger you read afterwards. No score, no streak, no character looking disappointed.

Total running cost: **€0.**

> **Key safety:** the API key lives in `localStorage` on your own device and is never committed. That is safe while you are the only user of your deployment. If you share the URL, move the key behind a proxy first — see *About the key* below.

---

## 1. Get a key (2 minutes, free, no card)

Go to <https://aistudio.google.com/apikey>, create a key, copy it.

## 2. Run it

**Laptop, right now:** open `index.html` in Chrome. Click **Schlüssel**, paste the key, done.
Note: from `file://` the mic sometimes refuses. If it does, jump to step 3 — `localhost` counts as secure.

**Local server:**
```bash
cd sprechpartner
python3 -m http.server 8000
```
Then <http://localhost:8000>. Mic, service worker and install prompt all work here.

## 3. Put it on the internet (still free)

Any static host. Cloudflare Pages is the least friction:

1. Push this folder to a GitHub repo.
2. Cloudflare dashboard → Workers & Pages → Create → Pages → connect the repo.
3. Build command: none. Output directory: `/`.

You get an HTTPS URL. HTTPS is required for the mic and for installing to the home screen.

## 4. Install on Android

Open the URL in Chrome → menu → **Add to Home screen**. It gets its own icon and opens without browser chrome. No Play Store, no €25 fee.

---

## About the key

The key lives in the browser, in `localStorage`, and is sent only to Google. Nobody else can read it — as long as **you are the only person using your deployment**.

If you ever share the URL, move the key server-side: a Cloudflare Worker that holds the key and forwards requests. ~20 lines, free tier, and the frontend change is one URL.

## Free tier, honestly

- Requests per day are capped and Google has adjusted the numbers more than once. A normal practice session is nowhere near the ceiling.
- Free-tier prompts may be used to improve Google's models. Fine for `Small talk im Büro`. Think twice before rehearsing anything private.
- Hit a 429 and it resets at midnight Pacific.

## Things worth building next

- Persist the ledger, and feed yesterday's errors back as tomorrow's warm-up. This is the piece that turns practice into progress.
- Word-level diffs in the ledger instead of whole-phrase.
- A "sag das nochmal" button that re-runs your last sentence and checks whether the fix stuck.
