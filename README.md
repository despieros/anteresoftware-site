# anteresoftware.com

Static site for ANTERE SOFTWARE LTD. Plain HTML and CSS, no build step, no external requests.

## Files

- `index.html` — home: what the company does, legal details, contact
- `support.html` — contact and data-request instructions
- `privacy.html` — privacy policy for the website (apps get their own)
- `terms.html` — terms of use for the website
- `404.html` — served by GitHub Pages for unknown paths
- `style.css`, `favicon.svg`
- `CNAME` — custom domain for GitHub Pages
- `apps/carob-health/` — product page, app privacy policy, terms, support FAQ,
  `policy.json` (document versions for the app to check), app icon

Per-app pages are not linked from the home page until the app is live; add a
link in `index.html` when the store listing exists.

## Deploy on GitHub Pages

1. Create a repository (public or private, both work) and push these files to `main`.
2. Repository → Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
3. Under "Custom domain" enter `anteresoftware.com`, save, then tick "Enforce HTTPS" once the certificate is issued (a few minutes to an hour).

## DNS (Namecheap → Advanced DNS)

Keep every existing MX and TXT record for Google Workspace. Add:

| Type  | Host | Value                   |
|-------|------|-------------------------|
| A     | @    | 185.199.108.153         |
| A     | @    | 185.199.109.153         |
| A     | @    | 185.199.110.153         |
| A     | @    | 185.199.111.153         |
| CNAME | www  | `<github-user>.github.io.` |

Delete Namecheap's default "URL Redirect" / parking record for `@` if present.

## Embedding in an app

Append `?embed=1` to any page URL to hide the site header and footer, e.g.
`https://anteresoftware.com/privacy.html?embed=1`. The pages follow the system
light/dark setting (`prefers-color-scheme`), so they match a dark app theme in
WKWebView and Android WebView. Nothing else changes: no scripts beyond the
one-line class toggle, no external requests.

## Before going live

- Add a public phone number if you want one shown (commented block in `index.html`).
- If you host somewhere other than GitHub Pages, update the hosting provider named in `privacy.html`.
- Carob Health: decide the ML Kit question (see launch checklist) and pick the matching
  paragraph in `apps/carob-health/privacy.html`; decide the minimum age in `terms.html`.
- When a policy changes: bump `version`/`effective` in `policy.json`, change the date at the
  top of the page, and keep the previous version at `apps/<app>/privacy/<old-version>.html`.
