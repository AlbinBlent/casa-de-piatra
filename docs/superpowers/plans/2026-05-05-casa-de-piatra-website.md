# Casa de Piatră Stockholm Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a bilingual (Swedish/Romanian) static GitHub Pages site for Casa de Piatră Stockholm catering & events.

**Architecture:** Pure HTML/CSS/JS, no build tools. Root `index.html` auto-detects browser language and redirects to `/sv/` or `/ro/`. Each language is a self-contained single-page site. Shared stylesheet lives in `assets/style.css`.

**Tech Stack:** HTML5, CSS3 (custom properties), vanilla JS, Google Fonts (Dancing Script), GitHub Pages

---

## File Map

| File | Purpose |
|---|---|
| `index.html` | Language detector — redirects to `/sv/` or `/ro/` |
| `assets/style.css` | Shared stylesheet — all design tokens, layout, components |
| `assets/logo.jpg` | Logo image (copy of `casa_be_piatra.jpg`) |
| `assets/menu.png` | Menu image |
| `sv/index.html` | Full Swedish single-page site |
| `ro/index.html` | Full Romanian single-page site |

---

## Task 1: Copy Assets into Place

**Files:**
- Create: `assets/logo.jpg` (copy of `casa_be_piatra.jpg`)
- Create: `assets/menu.png` (copy of `menu.png`)

- [ ] **Step 1: Create assets directory and copy files**

```bash
mkdir -p assets sv ro
cp casa_be_piatra.jpg assets/logo.jpg
cp menu.png assets/menu.png
```

- [ ] **Step 2: Verify files exist**

```bash
ls assets/
```

Expected output:
```
logo.jpg   menu.png
```

- [ ] **Step 3: Commit**

```bash
git add assets/
git commit -m "feat: add logo and menu assets"
```

---

## Task 2: Create Shared Stylesheet

**Files:**
- Create: `assets/style.css`

- [ ] **Step 1: Create `assets/style.css` with the full contents below**

```css
/* ── Design Tokens ── */
:root {
  --bg: #0a0a0a;
  --text: #f0ece4;
  --gold: #FCD116;
  --blue: #002B7F;
  --red: #CE1126;
  --font-heading: 'Dancing Script', cursive;
  --font-body: Inter, system-ui, -apple-system, sans-serif;
  --max-w: 900px;
}

/* ── Reset ── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body { background: var(--bg); color: var(--text); font-family: var(--font-body); line-height: 1.65; }
a { color: inherit; text-decoration: none; }
img { max-width: 100%; display: block; }

/* ── Typography ── */
h2 { font-family: var(--font-heading); font-size: clamp(2rem, 5vw, 3rem); color: var(--gold); margin-bottom: 1.25rem; }
h3 { font-family: var(--font-heading); font-size: 1.5rem; }
p { margin-bottom: 0.9rem; }
p:last-child { margin-bottom: 0; }

/* ── Header ── */
.site-header {
  position: sticky;
  top: 0;
  z-index: 100;
  background: rgba(10, 10, 10, 0.96);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  border-bottom: 1px solid rgba(252, 209, 22, 0.15);
  padding: 0.65rem 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}
.site-header .logo { height: 44px; border-radius: 4px; }
.site-nav { display: flex; gap: 1.75rem; align-items: center; }
.site-nav a {
  font-size: 0.8rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  opacity: 0.75;
  transition: opacity 0.2s, color 0.2s;
}
.site-nav a:hover { opacity: 1; color: var(--gold); }
.lang-toggle { display: flex; gap: 0.3rem; font-size: 0.8rem; }
.lang-toggle a {
  padding: 0.2rem 0.55rem;
  border: 1px solid rgba(252, 209, 22, 0.3);
  border-radius: 3px;
  transition: background 0.2s, border-color 0.2s;
}
.lang-toggle a.active { background: var(--gold); color: #000; font-weight: 700; border-color: var(--gold); }
.lang-toggle a:not(.active):hover { border-color: var(--gold); }

/* ── Hero ── */
.hero {
  min-height: 100svh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 5rem 2rem 4rem;
  gap: 1.75rem;
}
.hero .hero-logo { width: min(300px, 75vw); border-radius: 8px; }
.hero .tagline {
  font-family: var(--font-heading);
  font-size: clamp(1.2rem, 3.5vw, 1.9rem);
  opacity: 0.88;
  max-width: 580px;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  padding: 0.8rem 2.2rem;
  background: var(--gold);
  color: #000;
  font-weight: 700;
  border-radius: 4px;
  letter-spacing: 0.07em;
  text-transform: uppercase;
  font-size: 0.85rem;
  transition: background 0.2s, transform 0.15s;
}
.btn:hover { background: #e5bc10; transform: translateY(-2px); }

/* ── Section Divider ── */
.divider {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.6rem;
  padding: 1.5rem 2rem;
}
.divider-line {
  flex: 1;
  max-width: 220px;
  height: 1px;
  background: linear-gradient(to right, transparent, rgba(252, 209, 22, 0.35), transparent);
}
.divider-diamond { width: 10px; height: 10px; transform: rotate(45deg); }
.divider-diamond.gold  { background: var(--gold); }
.divider-diamond.blue  { background: var(--blue); }
.divider-diamond.red   { background: var(--red);  }

/* ── Sections ── */
.section-inner { max-width: var(--max-w); margin: 0 auto; padding: 4rem 2rem; }

/* ── About ── */
.about-note {
  margin-top: 1.25rem;
  padding: 0.85rem 1.1rem;
  border-left: 3px solid var(--gold);
  background: rgba(252, 209, 22, 0.06);
  border-radius: 0 4px 4px 0;
  font-size: 0.95rem;
}

/* ── Menu ── */
.menu-categories { display: grid; gap: 2.25rem; margin-top: 1.5rem; }
@media (min-width: 640px) { .menu-categories { grid-template-columns: 1fr 1fr; } }
.menu-category h3 {
  color: var(--gold);
  border-bottom: 1px solid rgba(252, 209, 22, 0.2);
  padding-bottom: 0.5rem;
  margin-bottom: 0.85rem;
}
.menu-items { list-style: none; display: grid; gap: 0.35rem; }
.menu-items li {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 0.75rem;
  font-size: 0.92rem;
  padding: 0.25rem 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}
.menu-items li:last-child { border-bottom: none; }
.price { color: var(--gold); white-space: nowrap; font-weight: 600; font-size: 0.9rem; }
.menu-image-wrap {
  grid-column: 1 / -1;
  text-align: center;
  margin-top: 1rem;
}
.menu-image-wrap a { display: inline-block; }
.menu-image-wrap img { max-width: min(380px, 100%); margin: 0 auto; border-radius: 8px; opacity: 0.85; transition: opacity 0.2s; }
.menu-image-wrap a:hover img { opacity: 1; }
.menu-image-caption { font-size: 0.78rem; opacity: 0.45; margin-top: 0.5rem; }

/* ── Contact ── */
.contact-intro { margin-bottom: 1.5rem; }
.contact-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
  gap: 1.25rem;
  margin-bottom: 2.5rem;
}
.contact-card {
  padding: 1.1rem 1.25rem;
  border: 1px solid rgba(252, 209, 22, 0.2);
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
  transition: border-color 0.2s;
}
.contact-card:hover { border-color: rgba(252, 209, 22, 0.5); }
.contact-card .label {
  font-size: 0.7rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--gold);
  opacity: 0.65;
}
.contact-card a:hover { color: var(--gold); }
.tally-form iframe {
  width: 100%;
  border: none;
  border-radius: 8px;
  min-height: 520px;
  background: transparent;
}

/* ── Footer ── */
.flag-bar {
  height: 3px;
  background: linear-gradient(to right, var(--blue) 33.33%, var(--gold) 33.33% 66.66%, var(--red) 66.66%);
}
footer { text-align: center; padding: 2rem 1rem; font-size: 0.82rem; opacity: 0.45; }

/* ── Mobile ── */
@media (max-width: 600px) {
  .site-header { padding: 0.65rem 1rem; }
  .site-nav { gap: 1rem; }
  .section-inner { padding: 3rem 1.25rem; }
  .hero { padding: 4rem 1.25rem 3rem; gap: 1.5rem; }
}
```

- [ ] **Step 2: Start a local server to prepare for visual verification in later tasks**

```bash
python3 -m http.server 8080 --directory /Users/albin/development/casa-de-piatra
```

Leave this running in a separate terminal. All pages are at `http://localhost:8080`.

- [ ] **Step 3: Commit**

```bash
git add assets/style.css
git commit -m "feat: add shared stylesheet with design tokens and components"
```

---

## Task 3: Create Language Detector (`index.html`)

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create `index.html` with the following content**

```html
<!DOCTYPE html>
<html lang="sv">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Casa de Piatră Stockholm</title>
  <script>
    (function () {
      var saved = localStorage.getItem('cdp-lang');
      if (saved === 'ro') { location.replace('/ro/'); return; }
      if (saved === 'sv') { location.replace('/sv/'); return; }
      var lang = (navigator.language || '').toLowerCase();
      if (lang.startsWith('ro')) {
        localStorage.setItem('cdp-lang', 'ro');
        location.replace('/ro/');
      } else {
        localStorage.setItem('cdp-lang', 'sv');
        location.replace('/sv/');
      }
    })();
  </script>
</head>
<body>
  <noscript>
    <p style="font-family:sans-serif;padding:2rem">
      <a href="/sv/">Svenska</a> &nbsp;|&nbsp; <a href="/ro/">Română</a>
    </p>
  </noscript>
</body>
</html>
```

- [ ] **Step 2: Verify redirect logic manually**

Open `http://localhost:8080/` in a browser.

Expected: you are immediately redirected to `http://localhost:8080/sv/` (or `/ro/` if your browser is set to Romanian). The page will show a 404 because `sv/index.html` doesn't exist yet — that is expected at this stage.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add language detector with localStorage persistence"
```

---

## Task 4: Create Swedish Page (`sv/index.html`)

**Files:**
- Create: `sv/index.html`

- [ ] **Step 1: Create `sv/index.html` with the following content**

```html
<!DOCTYPE html>
<html lang="sv">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Casa de Piatră Stockholm — Rumänsk catering &amp; event</title>
  <meta name="description" content="Rumänsk husmanskost — catering och eventorganisation i Stockholm. Beställ traditionell rumänsk mat: sarmale, ciorbe, rulade och mer.">
  <link rel="alternate" hreflang="sv" href="/sv/">
  <link rel="alternate" hreflang="ro" href="/ro/">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="../assets/style.css">
</head>
<body>

  <header class="site-header">
    <a href="#hero"><img class="logo" src="../assets/logo.jpg" alt="Casa de Piatră Stockholm logotyp"></a>
    <nav class="site-nav" aria-label="Huvudnavigation">
      <a href="#om-oss">Om oss</a>
      <a href="#meny">Meny</a>
      <a href="#kontakt">Kontakt</a>
    </nav>
    <div class="lang-toggle" aria-label="Välj språk">
      <a href="/sv/" class="active" onclick="localStorage.setItem('cdp-lang','sv')">SV</a>
      <a href="/ro/" onclick="localStorage.setItem('cdp-lang','ro')">RO</a>
    </div>
  </header>

  <section class="hero" id="hero">
    <img class="hero-logo" src="../assets/logo.jpg" alt="Casa de Piatră Stockholm">
    <p class="tagline">Rumänsk husmanskost — catering &amp; event i Stockholm</p>
    <a class="btn" href="#kontakt">Boka nu</a>
  </section>

  <div class="divider" aria-hidden="true">
    <div class="divider-line"></div>
    <div class="divider-diamond blue"></div>
    <div class="divider-diamond gold"></div>
    <div class="divider-diamond red"></div>
    <div class="divider-line"></div>
  </div>

  <section id="om-oss">
    <div class="section-inner">
      <h2>Om oss</h2>
      <p>Vi bjuder in er att smaka på rumänsk mat som hemma hos mamma! Vi lagar traditionell rumänsk husmanskost med kärlek och autenticitet, och erbjuder catering och eventorganisation i Stockholm.</p>
      <p class="about-note">Vi tar enbart emot förbeställningar — ingen walk-in. Kontakta oss i god tid för bokning via telefon eller formuläret nedan.</p>
    </div>
  </section>

  <div class="divider" aria-hidden="true">
    <div class="divider-line"></div>
    <div class="divider-diamond blue"></div>
    <div class="divider-diamond gold"></div>
    <div class="divider-diamond red"></div>
    <div class="divider-line"></div>
  </div>

  <section id="meny">
    <div class="section-inner">
      <h2>Meny</h2>
      <div class="menu-categories">

        <div class="menu-category">
          <h3>Traditionella Sallader</h3>
          <ul class="menu-items">
            <li><span>Boeuf-sallad 1 kg</span><span class="price">250 kr</span></li>
            <li><span>Auberginesallad 1 kg</span><span class="price">250 kr</span></li>
            <li><span>Svampsallad 1 kg</span><span class="price">200 kr</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Kött &amp; Rulader</h3>
          <ul class="menu-items">
            <li><span>Kycklingschnitzel 1 kg</span><span class="price">400 kr</span></li>
            <li><span>Köttbullar 1 kg</span><span class="price">400 kr</span></li>
            <li><span>Kycklingrulad med bacon 1 kg</span><span class="price">450 kr</span></li>
            <li><span>Spenat- &amp; tonrulad 1,5 kg</span><span class="price">450 kr</span></li>
            <li><span>Drob (lammpaté) 1 kg</span><span class="price">300 kr</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Traditionella Soppor</h3>
          <ul class="menu-items">
            <li><span>Ciorbă de burtă / lammmagsoppa 5 L</span><span class="price">800 kr</span></li>
            <li><span>Perișoare / nöt- / kycklingbuljong 5 L</span><span class="price">700 kr</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Sarmale &amp; Fyllda Paprikor</h3>
          <ul class="menu-items">
            <li><span>Sarmale 50 st</span><span class="price">700 kr</span></li>
            <li><span>Fyllda paprikor 20 st</span><span class="price">700 kr</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Papanași</h3>
          <ul class="menu-items">
            <li><span>Papanași (min. 5 st)</span><span class="price">60 kr/st</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Aptitretarbrickor</h3>
          <ul class="menu-items">
            <li><span>5 pers</span><span class="price">750 kr</span></li>
            <li><span>12 pers</span><span class="price">1 500 kr</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Konditori &amp; Bakverk</h3>
          <ul class="menu-items">
            <li><span>Färsk cozonac (brioche)</span><span class="price">370 kr/st</span></li>
            <li><span>Pașcă med deg</span><span class="price">450 kr</span></li>
            <li><span>Pașcă utan deg</span><span class="price">400 kr</span></li>
          </ul>
        </div>

        <div class="menu-image-wrap">
          <a href="../assets/menu.png" target="_blank" rel="noopener">
            <img src="../assets/menu.png" alt="Fullständig meny">
            <p class="menu-image-caption">Klicka för att se fullständig meny</p>
          </a>
        </div>

      </div>
    </div>
  </section>

  <div class="divider" aria-hidden="true">
    <div class="divider-line"></div>
    <div class="divider-diamond blue"></div>
    <div class="divider-diamond gold"></div>
    <div class="divider-diamond red"></div>
    <div class="divider-line"></div>
  </div>

  <section id="kontakt">
    <div class="section-inner">
      <h2>Kontakt</h2>
      <p class="contact-intro">Bokning och beställning sker enbart via förhandsreservation. Kontakta oss gärna i god tid.</p>

      <div class="contact-grid">
        <div class="contact-card">
          <span class="label">Telefon</span>
          <a href="tel:+46735844751">0735 844 751</a>
        </div>
        <div class="contact-card">
          <span class="label">E-post</span>
          <a href="mailto:email@casadepiatra.se">email@casadepiatra.se</a>
        </div>
        <div class="contact-card">
          <span class="label">Facebook</span>
          <a href="https://www.facebook.com/casadepiatrastockholm/" target="_blank" rel="noopener noreferrer">Casa de Piatră Stockholm</a>
        </div>
      </div>

      <div class="tally-form">
        <!-- Replace TALLY_FORM_URL_HERE with your Tally.so embed URL, e.g. https://tally.so/embed/XXXXXX -->
        <iframe src="TALLY_FORM_URL_HERE" title="Bokningsformulär" loading="lazy"></iframe>
      </div>
    </div>
  </section>

  <div class="flag-bar"></div>
  <footer>
    <p>&copy; Casa de Piatră Stockholm</p>
  </footer>

</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

Open `http://localhost:8080/sv/` and check:
- Dark background, gold headings, Dancing Script font loads
- Header: logo visible, nav links present, SV active in toggle
- Hero: logo large and centred, tagline readable, "Boka nu" button visible
- Diamond dividers between sections
- Menu: two-column grid on desktop, prices right-aligned in gold
- Contact: three cards visible, tel: link works
- Footer: flag bar (blue/gold/red stripe) above copyright text

- [ ] **Step 3: Commit**

```bash
git add sv/index.html
git commit -m "feat: add Swedish single-page site"
```

---

## Task 5: Create Romanian Page (`ro/index.html`)

**Files:**
- Create: `ro/index.html`

- [ ] **Step 1: Create `ro/index.html` with the following content**

```html
<!DOCTYPE html>
<html lang="ro">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Casa de Piatră Stockholm — Catering &amp; evenimente românești</title>
  <meta name="description" content="Mâncare românească ca acasă — catering și organizare de evenimente în Stockholm. Sarmale, ciorbe, rulade și alte delicatese tradiționale.">
  <link rel="alternate" hreflang="sv" href="/sv/">
  <link rel="alternate" hreflang="ro" href="/ro/">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="../assets/style.css">
</head>
<body>

  <header class="site-header">
    <a href="#hero"><img class="logo" src="../assets/logo.jpg" alt="Casa de Piatră Stockholm logo"></a>
    <nav class="site-nav" aria-label="Navigație principală">
      <a href="#despre">Despre</a>
      <a href="#meniu">Meniu</a>
      <a href="#contact">Contact</a>
    </nav>
    <div class="lang-toggle" aria-label="Alegeți limba">
      <a href="/sv/" onclick="localStorage.setItem('cdp-lang','sv')">SV</a>
      <a href="/ro/" class="active" onclick="localStorage.setItem('cdp-lang','ro')">RO</a>
    </div>
  </header>

  <section class="hero" id="hero">
    <img class="hero-logo" src="../assets/logo.jpg" alt="Casa de Piatră Stockholm">
    <p class="tagline">Mâncare românească ca acasă — catering &amp; evenimente în Stockholm</p>
    <a class="btn" href="#contact">Rezervă acum</a>
  </section>

  <div class="divider" aria-hidden="true">
    <div class="divider-line"></div>
    <div class="divider-diamond blue"></div>
    <div class="divider-diamond gold"></div>
    <div class="divider-diamond red"></div>
    <div class="divider-line"></div>
  </div>

  <section id="despre">
    <div class="section-inner">
      <h2>Despre noi</h2>
      <p>Vă invităm să gustați mâncărurile românești ca la mama acasă! Gătim cu dragoste și autenticitate, oferind servicii de catering și organizare de evenimente în Stockholm.</p>
      <p class="about-note">Activăm exclusiv prin comandă și rezervare din timp — fără acces walk-in. Contactați-ne în avans pentru rezervare prin telefon sau formularul de mai jos.</p>
    </div>
  </section>

  <div class="divider" aria-hidden="true">
    <div class="divider-line"></div>
    <div class="divider-diamond blue"></div>
    <div class="divider-diamond gold"></div>
    <div class="divider-diamond red"></div>
    <div class="divider-line"></div>
  </div>

  <section id="meniu">
    <div class="section-inner">
      <h2>Meniu</h2>
      <div class="menu-categories">

        <div class="menu-category">
          <h3>Salate Tradiționale</h3>
          <ul class="menu-items">
            <li><span>Salată de boeuf 1 kg</span><span class="price">250 kr</span></li>
            <li><span>Salată de vinete 1 kg</span><span class="price">250 kr</span></li>
            <li><span>Salată de ciuperci 1 kg</span><span class="price">200 kr</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Preparate din Carne &amp; Rulade</h3>
          <ul class="menu-items">
            <li><span>Șnițele de pui 1 kg</span><span class="price">400 kr</span></li>
            <li><span>Chifteluțe 1 kg</span><span class="price">400 kr</span></li>
            <li><span>Rulada de pui în bacon 1 kg</span><span class="price">450 kr</span></li>
            <li><span>Rulada de spanac cu ton 1,5 kg</span><span class="price">450 kr</span></li>
            <li><span>Drob 1 kg</span><span class="price">300 kr</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Ciorbe Tradiționale</h3>
          <ul class="menu-items">
            <li><span>Ciorbă de burtă / de miel 5 L</span><span class="price">800 kr</span></li>
            <li><span>Ciorbă de perișoare / văcuță / pui 5 L</span><span class="price">700 kr</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Sarmale &amp; Ardei Umpluți</h3>
          <ul class="menu-items">
            <li><span>Sarmale 50 buc</span><span class="price">700 kr</span></li>
            <li><span>Ardei umpluți 20 buc</span><span class="price">700 kr</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Papanași</h3>
          <ul class="menu-items">
            <li><span>Papanași (comandă min. 5 buc)</span><span class="price">60 kr/buc</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Platouri Aperitiv</h3>
          <ul class="menu-items">
            <li><span>5 pers</span><span class="price">750 kr</span></li>
            <li><span>12 pers</span><span class="price">1 500 kr</span></li>
          </ul>
        </div>

        <div class="menu-category">
          <h3>Cofetăria Dulce și Personalizat</h3>
          <ul class="menu-items">
            <li><span>Cozonaci proaspeți</span><span class="price">370 kr/buc</span></li>
            <li><span>Pașcă cu aluat</span><span class="price">450 kr</span></li>
            <li><span>Pașcă fără aluat</span><span class="price">400 kr</span></li>
          </ul>
        </div>

        <div class="menu-image-wrap">
          <a href="../assets/menu.png" target="_blank" rel="noopener">
            <img src="../assets/menu.png" alt="Meniu complet">
            <p class="menu-image-caption">Apăsați pentru a vedea meniul complet</p>
          </a>
        </div>

      </div>
    </div>
  </section>

  <div class="divider" aria-hidden="true">
    <div class="divider-line"></div>
    <div class="divider-diamond blue"></div>
    <div class="divider-diamond gold"></div>
    <div class="divider-diamond red"></div>
    <div class="divider-line"></div>
  </div>

  <section id="contact">
    <div class="section-inner">
      <h2>Contact</h2>
      <p class="contact-intro">Comenzile și rezervările se fac exclusiv în avans. Contactați-ne din timp.</p>

      <div class="contact-grid">
        <div class="contact-card">
          <span class="label">Telefon</span>
          <a href="tel:+40735844751">0735 844 751</a>
        </div>
        <div class="contact-card">
          <span class="label">Email</span>
          <a href="mailto:email@casadepiatra.se">email@casadepiatra.se</a>
        </div>
        <div class="contact-card">
          <span class="label">Facebook</span>
          <a href="https://www.facebook.com/casadepiatrastockholm/" target="_blank" rel="noopener noreferrer">Casa de Piatră Stockholm</a>
        </div>
      </div>

      <div class="tally-form">
        <!-- Replace TALLY_FORM_URL_HERE with your Tally.so embed URL, e.g. https://tally.so/embed/XXXXXX -->
        <iframe src="TALLY_FORM_URL_HERE" title="Formular de rezervare" loading="lazy"></iframe>
      </div>
    </div>
  </section>

  <div class="flag-bar"></div>
  <footer>
    <p>&copy; Casa de Piatră Stockholm</p>
  </footer>

</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

Open `http://localhost:8080/ro/` and check:
- RO is active in language toggle, SV is not
- All text is in Romanian
- Section anchors: `#despre`, `#meniu`, `#contact`
- Nav links match anchors
- "Rezervă acum" CTA button is present
- Menu items match Romanian names from the spec
- Contact section visible with phone, email, Facebook

- [ ] **Step 3: Verify language switching**

1. Open `http://localhost:8080/ro/` — click "SV" toggle — should go to `/sv/`
2. Open `http://localhost:8080/sv/` — click "RO" toggle — should go to `/ro/`
3. Open `http://localhost:8080/` — verify redirect goes to `/sv/` (default)
4. In browser console on `http://localhost:8080/`, run: `localStorage.setItem('cdp-lang', 'ro')` then reload — should redirect to `/ro/`

- [ ] **Step 4: Commit**

```bash
git add ro/index.html
git commit -m "feat: add Romanian single-page site"
```

---

## Task 6: Owner Customisation Notes (README)

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Update README.md with deployment and customisation instructions**

Replace the contents of `README.md` with:

```markdown
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
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add deployment and customisation instructions"
```

---

## Task 7: Final Verification Checklist

No new files. Manual checks before calling this done.

- [ ] **Step 1: Check all pages load without console errors**

Open browser DevTools (F12) → Console tab, then visit:
- `http://localhost:8080/` — no errors, redirects to `/sv/`
- `http://localhost:8080/sv/` — no errors, Dancing Script font loaded
- `http://localhost:8080/ro/` — no errors

- [ ] **Step 2: Check mobile layout**

In DevTools, toggle device toolbar (Ctrl+Shift+M) and set to iPhone SE (375px wide). Verify:
- Header doesn't overflow
- Hero logo fits within viewport
- Menu items don't overflow (flex wraps correctly)
- Contact cards stack vertically

- [ ] **Step 3: Verify hreflang tags are present**

In browser DevTools → Elements tab, confirm each language page `<head>` contains:
```html
<link rel="alternate" hreflang="sv" href="/sv/">
<link rel="alternate" hreflang="ro" href="/ro/">
```

- [ ] **Step 4: Verify smooth scroll**

On `http://localhost:8080/sv/`, click each nav link (Om oss, Meny, Kontakt) — page should scroll smoothly to each section.

- [ ] **Step 5: Final commit**

```bash
git status
```

If any files are uncommitted, add and commit them:

```bash
git add -A
git commit -m "chore: final cleanup"
```
