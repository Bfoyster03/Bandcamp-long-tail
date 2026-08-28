# Forgotten on Bandcamp

A Forgotify-style Bandcamp discovery toy that biases toward low-public-attention releases. Supports fine-grained and combined tags such as **drum and bass + jungle**, liquid drum and bass, breakcore, IDM, dark ambient, free jazz, and arbitrary custom tags.

## Free hosting: GitHub Pages + Cloudflare Worker

GitHub Pages hosts the frontend for free. GitHub Pages cannot run a Python/backend process, so the tiny Bandcamp proxy lives in a free Cloudflare Worker. **All source code still lives in this GitHub repository.**

### 1. Put this repository on GitHub

Create an empty GitHub repo, then from this folder:

```bash
git init
git add .
git commit -m "Initial Forgotten on Bandcamp"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/forgotten-bandcamp.git
git push -u origin main
```

### 2. Deploy the free backend

Install Node.js, then:

```bash
cd worker
npx wrangler login
npx wrangler deploy
```

Wrangler prints a URL like `https://forgotten-bandcamp.YOUR_SUBDOMAIN.workers.dev`.

### 3. Connect the frontend

Open `docs/index.html` and replace:

```js
const API_BASE = localStorage.getItem('fb_api') || 'YOUR_WORKER_URL';
```

with your Worker URL. Commit and push.

### 4. Turn on GitHub Pages

In the GitHub repo: **Settings → Pages → Build and deployment → Deploy from a branch → `main` → `/docs` → Save**.

Your app will appear at `https://YOUR_USERNAME.github.io/forgotten-bandcamp/`.

## Notes

Bandcamp does not expose general public play counts here. The app therefore never claims a release has zero plays. It samples Bandcamp Discover and, when public release HTML is readable, biases toward fewer visible fan/supporter markers. Bandcamp can change private/public web endpoints, so the Worker may occasionally need maintenance.
