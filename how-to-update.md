# How to update

## Steps

1. Edit the pages in `public/`. If the script in `index.html` changes, refresh its lock: `python3 /tmp/toolkit/lock.py public/index.html`.
2. Bump the version in three places together: `APP_VERSION` in `public/index.html`, `"version"` in `package.json`, and a new top entry in `CHANGELOG.md`.
3. Test locally:
   - `npm ci`, then `npx wrangler dev`. Open every page, plus a made-up address (it should show `404.html` with a 404 status).
   - `bash /tmp/toolkit/release-check.sh public`
   - Check the `package.json` and `CHANGELOG.md` versions by hand, since the release check can't see them.
   - Run the search patterns on everything outside `public/` that changed since the last tag.
4. Push with push-check. Workers Builds deploys `main`, and the Tag new versions workflow adds the tag.
5. On an iPhone: the build passed in Cloudflare, and the live site shows the new version.

## Must not break

- `wrangler.jsonc` keeps `"workers_dev"` and `"preview_urls"` written out, and `"preview_urls"` stays `false`. Never use `wrangler versions upload`.
- Every page keeps its privacy lock (the CSP meta tag, with `connect-src 'none'`), and `public/_headers` keeps its four headers.
- wrangler stays pinned exactly, with `package-lock.json`, and `compatibility_date` stays pinned. Update them together, on purpose.
- No secrets anywhere. `.dev.vars` and `.wrangler/` stay ignored.
- The tag workflow reads `APP_VERSION` from `public/index.html`, so that file keeps it.
