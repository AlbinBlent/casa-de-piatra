# Karpatisk Catering & Event

Swedish single-page GitHub Pages website for Karpatisk Catering & Event
(formerly branded Casa de Piatră Stockholm) — catering and event planning
in Stockholm.

## Live site

Enable GitHub Pages in repo Settings → Pages → Source: `main` branch, root `/`.

## Local development

```bash
python3 -m http.server 8080
# open http://localhost:8080
```

## Structure

```
/
├── index.html        ← the site (Swedish only)
├── sv/index.html     ← redirect to / (old bilingual URL)
├── ro/index.html     ← redirect to / (old bilingual URL)
└── assets/
    ├── style.css
    ├── logo.jpg   ← old dark Casa de Piatră logo, unused
    └── menu.png   ← old price-list menu image, no longer linked
```
