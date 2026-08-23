# Yalla Bola — the public site

Four static pages, no build step:

| Path | What |
|---|---|
| `/` | Get the app — APK download today, store badges later |
| `/g/?t=TOKEN` | Open a shared bola — tries the app, falls back to the get page, shows the pasteable code |
| `/privacy/` | Privacy policy (the same text as in the app) |
| `/terms/` | Terms |

## Publish on GitHub Pages (about five minutes)

1. On github.com create a **public** repository named `yallabola-site`
   (Pages on a free account needs a public repo; the app's own repo stays
   private — this folder is the only thing that goes here).
2. Put the contents of this folder at the repository root and push.
3. Replace `GITHUB_USER_PLACEHOLDER` in `index.html` with your GitHub user
   name (one find-and-replace).
4. Settings → Pages → Build and deployment → *Deploy from a branch* →
   `main` / `/ (root)` → Save. A minute later the site is at
   `https://<user>.github.io/yallabola-site/`.
5. **The APK:** Releases → *Draft a new release* → tag e.g. `v1.0.0-beta.1`
   → attach the APK **named exactly `YallaBola.apk`** → Publish. The
   download button already points at
   `releases/latest/download/YallaBola.apk`, so every new release with the
   same asset name updates the button without touching the page.

## Tell the app where the site is

In `config/dev.json` (and later `prod.json`) add:

```
"APP_LINK": "https://<user>.github.io/yallabola-site/",
"SHARE_LINK_BASE": "https://<user>.github.io/yallabola-site/g/?t="
```

then rebuild. From that build on, shared results carry "Get Yalla Bola" and
"Open this bola" links, and share codes become real links.

## Your own domain, later

Settings → Pages → Custom domain, point the DNS as GitHub instructs, and
change the two values above to the domain. Nothing else changes.
