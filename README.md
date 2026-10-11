# mordentplayer.github.io — the Mordent landing page

The public single-page site for [Mordent](https://github.com/mordentplayer/mordent),
a native, fast Apple Music client. The repository root **is** the site: `index.html`
is served as-is, with no build step.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole site: inline CSS, inline SVG icon, no frameworks, no external requests, no web fonts, no trackers. |
| `404.html` | Matching "page not found" page (GitHub Pages serves it for unknown paths). |
| `.nojekyll` | Tells GitHub Pages to skip Jekyll processing, so every file is served verbatim. |
| `.gitignore` | Keeps local review screenshots (`preview-*.png`) out of the repo. |

Nothing is fetched at load time. The only network call is a small optional
`fetch()` of the GitHub releases API, which upgrades the per-OS buttons
(AppImage / macOS `.app` / Windows zip) to direct asset URLs — with JavaScript
off, blocked, or the API failing, every button still points at the releases
page and the site works unchanged.

## Hosting — GitHub Pages

Pages is served from the `main` branch, repository root:

> **Settings → Pages → Build and deployment → Source: _Deploy from a branch_ →
> Branch: `main` → Folder: `/ (root)` → Save.**

Published URL: **https://mordentplayer.github.io/mordentplayer/**

Because the repository is named `mordentplayer` (not `mordentplayer.github.io`),
Pages serves the site under the `/mordentplayer/` path. A clean root URL
(`https://mordentplayer.github.io/`) would require renaming this repository to
`mordentplayer.github.io` — a user/org Pages repo — which also changes every
absolute link, so it is not done here.

## Preview locally

```sh
xdg-open index.html                       # file:// — everything works
# or serve it, to preview 404 handling and the /mordentplayer/ path too:
python3 -m http.server 8080               # then open http://localhost:8080/
```

The optional releases-API call works from `file://` and `http(s)://` alike; if it
is skipped, the fallback links are used.

## Footnote — Cloudflare Pages (alternative)

The same folder also deploys unchanged to Cloudflare Pages (direct upload with
`wrangler pages deploy .`, or git-connected). GitHub Pages is the primary path;
Cloudflare is only an option if a custom domain or Cloudflare's edge is wanted.
