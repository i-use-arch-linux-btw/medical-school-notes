# Setup

## Run locally

No server needed. Open either file directly in a browser:

```
y4/osce_atlas.html   — main reference app
y4/quiz.html         — spaced-repetition quiz
```

If you need a local server (e.g. to test Vercel rewrites):

```bash
cd y4 && python3 -m http.server 3000
# → http://localhost:3000
```

## Adding or correcting content

The authoritative data source is `y4/data/database.example.json`. Edit there first, then mirror the changes into both HTML files:

- `osce_atlas.html` → `const SIGNS`, `const POOLS`, `const TEST_INFO` blocks near the top of the `<script>`
- `quiz.html` → `const SIGNS` block (same array, verbatim copy)

All content must be grounded in the two PDFs in `y4/sources/`. If the app contradicts them, the PDFs win.

## Deploy

Push to `main` → Vercel auto-deploys to `msn.arshpatankar.com`.

The publish root is `y4/` (set in `vercel.json`). Both `osce_atlas.html` and `quiz.html` are served directly.
