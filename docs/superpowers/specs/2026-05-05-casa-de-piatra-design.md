# Casa de Piatră Stockholm — Website Design Spec

## Overview

A bilingual (Swedish / Romanian) static GitHub Pages website advertising Casa de Piatră Stockholm, a Romanian catering and event organisation business. The restaurant itself is closed since the pandemic; the business operates exclusively via pre-order/reservation.

---

## Architecture

**Approach:** Pure HTML/CSS/JS, no build tools, no dependencies beyond Google Fonts.

**File structure:**

```
/
├── index.html              ← language detector (no visible content)
├── sv/
│   └── index.html          ← Swedish single-page site
├── ro/
│   └── index.html          ← Romanian single-page site
└── assets/
    ├── logo.jpg            ← casa_be_piatra.jpg (the logo)
    ├── menu.png            ← menu image
    └── style.css           ← shared stylesheet
```

**Language detection (`index.html`):**
- Reads `navigator.language`
- Redirects to `/sv/` if Swedish (sv), otherwise `/ro/` if Romanian (ro), defaults to `/sv/`
- Saves choice to `localStorage` under key `cdp-lang` so returning visitors are not redirected again
- Each language page includes both `lang` attribute and `hreflang` link tags pointing to the other language version

---

## Visual Design

Inspired by the existing logo:

| Element | Value |
|---|---|
| Background | `#0a0a0a` (near-black) |
| Primary accent | `#FCD116` (Romanian flag gold) |
| Secondary accent | `#002B7F` (Romanian flag blue) |
| Tertiary accent | `#CE1126` (Romanian flag red) |
| Text | `#f0ece4` (warm off-white) |
| Heading font | Dancing Script (Google Fonts) — matches logo script |
| Body font | Inter or system sans-serif |
| Decorative motif | Diamond folk-art pattern (SVG) used as section dividers |

---

## Page Sections (both language versions)

### 1. Header
- Logo (small, left-aligned)
- Navigation links: About · Menu · Contact
- Language toggle top-right: `SV / RO` (links to the other language version)

### 2. Hero
- Full logo centred
- Tagline:
  - SV: *"Rumänsk husmanskost — catering & event i Stockholm"*
  - RO: *"Mâncare românească ca acasă — catering & evenimente în Stockholm"*
- CTA button scrolls to Contact section:
  - SV: "Boka nu"
  - RO: "Rezervă acum"

### 3. About
- Based on Facebook bio
- SV: "Vi bjuder in er att smaka på rumänsk mat som hemma hos mamma! Vi är verksamma inom catering och eventorganisation — enbart via förbeställning."
- RO: "Vă invităm să gustați mâncărurile românești ca la mama acasă! Activăm în catering și organizare evenimente — doar prin comandă/rezervare din timp."
- Prominent note that they are catering/events only (not walk-in)

### 4. Menu
Menu items displayed as styled text (SEO-friendly, mobile-readable), with the menu image also available for download/reference.

Categories and items (prices in SEK):

**Salate Tradiționale**
- Salată de boeuf 1 kg — 250 kr
- Salată de vinete 1 kg — 250 kr
- Salată de ciuperci 1 kg — 200 kr

**Preparate din Carne & Rulade**
- Șnițele de pui 1 kg — 400 kr
- Chifteluțe 1 kg — 400 kr
- Rulada de pui în bacon 1 kg — 450 kr
- Rulada de spanac cu ton 1,5 kg — 450 kr
- Drob 1 kg — 300 kr

**Ciorbe Tradiționale**
- Ciorbă de burtă / de miel 5 L — 800 kr
- Ciorbă de perișoare / văcuță / pui 5 L — 700 kr

**Sarmale & Ardei Umpluți**
- Sarmale 50 buc — 700 kr
- Ardei umpluți 20 buc — 700 kr

**Papanași**
- 60 kr/buc (comandă min. 5 buc.)

**Platouri Aperitiv**
- 5 pers — 750 kr
- 12 pers — 1 500 kr

**Cofetăria Dulce și Personalizat**
- Cozonaci proaspeți — 370 kr/buc
- Pașcă cu aluat — 450 kr / fără aluat — 400 kr

### 5. Contact
Four contact elements:
- **Phone:** 0735844751 — clickable `tel:` link
- **Email:** placeholder `[email@casadepiatra.se]` — owner to fill in
- **Facebook:** link to https://www.facebook.com/casadepiatrastockholm/
- **Tally.so form:** embedded `<iframe>` — owner to provide form URL (placeholder in code)

### 6. Footer
- © Casa de Piatră Stockholm
- Thin decorative line in Romanian flag colours (blue / yellow / red)

---

## SEO

- Each language page has `<html lang="sv">` / `<html lang="ro">`
- Each page has `<link rel="alternate" hreflang="sv" href="/sv/">` and `<link rel="alternate" hreflang="ro" href="/ro/">`
- Meta description in the respective language
- Menu items in HTML text (not image-only) for indexability

---

## GitHub Pages Deployment

- Repo pushed to GitHub with GitHub Pages enabled on `main` branch, root `/`
- `index.html` at root handles language detection and redirect
- No build step required — deploy by pushing to `main`

---

## Out of Scope

- CMS or admin interface
- Online ordering / payment
- Photo gallery (placeholder section only — owner adds photos later)
- Blog or news section
