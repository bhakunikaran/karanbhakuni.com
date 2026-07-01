# karanbhakuni.com

Personal site + blog, built with Hugo, deployed free on GitHub Pages.

## What's in here

- `content/posts/` — all 86 essays migrated from the old site, one markdown file each.
- `themes/karan-theme/` — a small custom theme (no external dependencies).
- `static/images/` — images referenced by posts.
- `static/CNAME` — tells GitHub Pages to serve this repo at karanbhakuni.com.
- `.github/workflows/deploy.yml` — builds the site and deploys to GitHub Pages automatically on every push to `main`.

## One-time setup (do this once)

1. Create a new **public** GitHub repository (e.g. `karanbhakuni.com` or `personal-site`).
2. From this folder, push it up:

   ```
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```

3. On GitHub: go to the repo → **Settings → Pages** → under "Build and deployment", set **Source** to **GitHub Actions**. (You do NOT need to pick a branch/folder — the workflow handles that.)
4. Still in **Settings → Pages**, under "Custom domain", enter `karanbhakuni.com` and save. GitHub will show a DNS check — that's expected until step 5 is done.
5. At your domain registrar (wherever karanbhakuni.com is registered), add these DNS records:

   For the apex domain (`karanbhakuni.com`), add four **A** records pointing to:
   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```

   For `www.karanbhakuni.com`, add a **CNAME** record pointing to:
   ```
   <your-username>.github.io
   ```

6. Back in GitHub Pages settings, once DNS propagates (can take a few minutes to a few hours), check "Enforce HTTPS".

That's the only manual, one-time setup. After this, everything is code:

## Writing a new post

Create a new markdown file in `content/posts/`, e.g.:

```
---
title: "Your Post Title"
date: "2026-07-05"
slug: "your-post-title"
---

Your essay text here. Paragraphs separated by a blank line.

![](/images/some-photo.jpg)
```

Drop any images into `static/images/`. For videos, just embed a YouTube link/iframe directly in the markdown (don't upload video files to the repo — see below).

Commit and push:

```
git add .
git commit -m "New post: Your Post Title"
git push
```

GitHub Actions rebuilds and redeploys automatically. Live in ~1 minute.

## Local preview (optional)

```
hugo server
```

Then open http://localhost:1313

## Keeping this scalable (1 GB repo limit)

- Keep images web-optimized (compress/resize before adding to `static/images/`).
- Never commit video files — host videos on YouTube (unlisted if you want) and embed the player/link in the post instead.
- Text content itself is negligible in size — thousands of posts is fine as long as media stays external.

## Search Console / SEO

- `sitemap.xml` is generated automatically by Hugo at build time.
- Verify the domain in Google Search Console and Bing Webmaster Tools using DNS TXT record verification (domain-level, at your registrar) — works independent of GitHub Pages.
- Submit `https://karanbhakuni.com/sitemap.xml` in Search Console after verifying.
