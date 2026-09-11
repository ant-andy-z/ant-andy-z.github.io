# Personal blog

Astro Markdown blog with KaTeX, published as a GitHub user site.

- **Local folder:** this repo
- **GitHub repo:** `YudongZhangAndy/YudongZhangAndy.github.io`
- **Live URL (after the first successful deploy):** https://YudongZhangAndy.github.io

## Run locally

```bash
npm install
npm run dev
```

Open the URL printed in the terminal (usually `http://localhost:4321`).

```bash
npm run build
npm run preview
```

builds the static site and serves `dist/`.

## Add a post

1. Create `src/content/blog/your-slug.md`.
2. Use this frontmatter:

   ```yaml
   ---
   title: Your title
   description: One-sentence summary for the homepage and RSS.
   pubDate: 2026-09-12
   draft: false
   tags:
     - optional
   ---
   ```

3. Write Markdown. Inline math uses `$...$`; display math uses `$$...$$`.
4. Commit and push `main`. GitHub Actions builds and deploys.

Set `draft: true` to keep a post off the homepage, RSS, and `/blog/` routes.

## Deploy on GitHub Pages

GitHub CLI (`gh`) is installed locally but not logged in yet. From this folder:

```bash
gh auth login
gh repo create YudongZhangAndy.github.io --public --source=. --remote=origin --push
```

If you prefer the website: create a **public** repo named `YudongZhangAndy.github.io`, then:

```bash
git remote add origin https://github.com/YudongZhangAndy/YudongZhangAndy.github.io.git
git push -u origin main
```

Then in the repo: **Settings → Pages**. Set **Source** to **GitHub Actions** (not “Deploy from a branch”). The workflow in `.github/workflows/deploy.yml` builds with `withastro/action` and publishes `dist/`.

Do not use the legacy Jekyll branch deploy. This site is static Astro output.

Node 22.12+ is required (`package.json` `engines`).
