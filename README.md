# Test Site

A small test page that checks a free website can go live on Cloudflare Workers. Cloudflare's Workers Builds deploys it from this repo's `main` branch.

- **Live address:** added here after the first deploy.
- **Privacy:** the site saves nothing about visitors. It has no trackers, ads or accounts, and its pages make no outside requests. Cloudflare hosts it and handles each visit, like any web host.
- **Feedback:** freeforgood-apps+testsite@proton.me

## What's here

| Path | Job |
|---|---|
| `public/` | The pages (`index.html`, `about.html`, `accessibility.html`, `404.html`), `style.css` and `_headers` |
| `wrangler.jsonc` | Cloudflare settings: static pages only, workers.dev on, preview URLs off |
| `package.json`, `package-lock.json` | Wrangler, pinned exactly |
| `.github/workflows/tag-new-versions.yml` | Adds a version tag when a new version reaches `main` |
| `PROGRESS.md` | Where things stand and why |
| `how-to-update.md` | How to make a change safely |

## Run it locally

```
npm ci
npx wrangler dev
```

Then open the address it prints.
