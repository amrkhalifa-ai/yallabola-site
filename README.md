# Yalla Bola — the public site

Four static pages, no build step:

| Path | What |
|---|---|
| `/` | Get the app — APK download today, store badges later |
| `/g/?t=TOKEN` | Open a shared bola — tries the app, falls back to the get page, shows the pasteable code |
| `/privacy/` | Privacy policy (the same text as in the app) |
| `/terms/` | Terms |
| `/admin/` | The numbers — moderators only, see the note below |

## The `/admin/` page, and why a public URL is the right place for it

It reads the whole dashboard out of Supabase and draws it. Two things
about that are worth being explicit, because both look wrong at first:

**The page and its key are public, deliberately.** Anyone can fetch the
HTML and read the publishable key out of it — exactly as anyone can
unzip the APK and find the same two strings, which is where they have
always lived. Every figure comes from a `security definer` function that
begins by refusing anybody who is not in `public.moderators`, returning
`42501`. The boundary is the database, not the secrecy of a URL.

**It is `noindex, nofollow` but that is tidiness, not security.** If you
want a second lock, put Cloudflare Access in front of the path; it is
free up to fifty users and changes nothing about how the page works.

Deploying it is a decision, not a step: everything else in this folder is
for players, and this one is for you. It is safe to publish and it is
also fine to leave unpublished and open from a local server when needed.

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
