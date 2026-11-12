# Test Site: progress

## Brief

- **What it is:** a pages-only test site (project type 10) on Cloudflare Workers static assets, on the free workers.dev address. It proves the path from GitHub to a Cloudflare build to a live page before a real site uses it.
- **Ground rules:** free plan only. No Worker code, database, forms, sign-in or domain without a plan and the owner's okay. Nothing personal in the repo. Every push goes through push-check.
- **Where things live:** pages in `public/`, settings in `wrangler.jsonc`. Workers Builds deploys `main`, and the Tag new versions workflow adds tags.

## Decisions

- **Starter:** the toolkit's `templates/cloudflare-site/` (wrangler 4.160.1, `compatibility_date` 2026-11-10). Update the two together, on purpose.
- **One front door:** `"workers_dev": true` and `"preview_urls": false`, both written out, and builds for other branches off. The site has no domain, so workers.dev is its only address.
- **One version spot:** the version lives in `APP_VERSION` in `public/index.html`, which the tag workflow and the release check read, plus `package.json` and the newest CHANGELOG entry. About says where to find it instead of repeating it, so two pages can't disagree.
- **Look:** the starter's plain look, since this is a hosting test. The shared freeforgood-apps look waits for a real site.
- **Long words wrap** (`overflow-wrap: break-word`), so the feedback address fits on a 320px screen.
- **Builds install with `npm ci`:** Cloudflare's docs don't say whether their automatic install uses the lockfile strictly, so the build sets `SKIP_DEPENDENCY_INSTALL` to `true` with `npm ci` as the build command. Deploy stays `npx wrangler deploy`, and preview builds stay off.
- **Worker name is `test-site`:** Workers Builds fails if the dashboard's Worker name doesn't match `"name"` in `wrangler.jsonc`.
- **Public repo,** so `main` can be protected on GitHub's free plan.
- **Feedback alias:** freeforgood-apps+testsite@proton.me.

## Where things stand

- **Version 1.0.0:** built, tested locally and pushed to `main`. Not deployed yet: Cloudflare isn't connected.
- **Tag workflow checked:** it found 1.0.0 in `public/` and added `v1.0.0` to the pushed commit.
- **Open until the first deploy:** the site builds on Cloudflare.

## Next up

- **Owner:** the Cloudflare account is made. Change the workers.dev subdomain to a neutral name first (on a phone the setting may be hidden, so try the desktop layout), then connect this repo with the build settings in Decisions and run the first build.
- **Done when** (the owner's iPhone check on the live site):
  1. The site's address opens the home page showing version 1.0.0, and About and Accessibility open from it.
  2. A made-up address on the site shows the friendly "page not found" page.
- **After the first deploy:** add the live address to the README and About page. Protect `main` from force-pushes and deletion, and turn on push protection and private vulnerability reporting. Then decide about joining the monthly security sweep.
