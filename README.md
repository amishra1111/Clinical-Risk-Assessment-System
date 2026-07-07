# VigilAI — Health Risk Prediction App

A single-page, client-side web app (login/register + a mock health-risk predictor with history and Chart.js trend analysis). No backend — everything is stored in the browser's `localStorage`.

## Project structure

```
.
├── index.html      # the entire app (HTML + Tailwind CDN + Chart.js CDN + JS)
├── vercel.json     # SPA rewrite rule so all routes serve index.html
└── .gitignore
```

## Push to GitHub

```bash
cd vigilai-deploy
git init
git add .
git commit -m "Initial commit: VigilAI app"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

(Create the empty repo on GitHub first at https://github.com/new — don't initialize it with a README so there's no merge conflict.)

## Deploy live on Vercel

**Option A — Dashboard (easiest)**
1. Go to https://vercel.com/new
2. Import the GitHub repo you just pushed
3. Framework preset: "Other" (it's static, no build step needed)
4. Click **Deploy** — Vercel detects `index.html` at the root and serves it directly

**Option B — Vercel CLI**
```bash
npm install -g vercel
cd vigilai-deploy
vercel        # follow prompts, links project + deploys a preview
vercel --prod # promotes to your production URL
```

Either way you'll get a live URL like `https://<project-name>.vercel.app`.

## Notes / things worth knowing before you rely on this in production

- **Login is not secure.** Usernames/passwords are stored in plain text in `localStorage` on the visitor's own browser. Anyone using the same browser/profile could open dev tools and read them, and data doesn't sync across devices. Fine for a demo/prototype, not for real user accounts or real health data.
- **Predictions are mocked.** `handlePredict()` uses a simple randomized formula, not a real model — good for showing the UI/UX, not for actual health guidance.
- **No real backend/database.** If you later want real accounts and persistent, cross-device data, you'd want to add a backend (e.g. Vercel Serverless Functions + a database, or an auth provider like Clerk/Auth0/Supabase).
