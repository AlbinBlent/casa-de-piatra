# Casa de Piatră Stockholm

Bilingual (Swedish/Romanian) GitHub Pages website for Casa de Piatră Stockholm catering & events.

## Live site

Enable GitHub Pages in repo Settings → Pages → Source: `main` branch, root `/`.

## Before going live — fill in these placeholders

1. **Email address** — search for `email@casadepiatra.se` in `sv/index.html` and `ro/index.html` and replace with the real email.
2. **Tally.so form** — replace `TALLY_FORM_URL_HERE` in both `sv/index.html` and `ro/index.html` with your Tally embed URL (e.g. `https://tally.so/embed/XXXXXX?alignLeft=1&hideTitle=1&transparentBackground=1`).

## Local development

```bash
python3 -m http.server 8080
# open http://localhost:8080
```

## Structure

```
/
├── index.html        ← language detector (redirects to /sv/ or /ro/)
├── sv/index.html     ← Swedish page
├── ro/index.html     ← Romanian page
└── assets/
    ├── style.css
    ├── logo.jpg
    └── menu.png
```
