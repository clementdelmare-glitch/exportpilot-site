# ExportPilot Homepage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the ExportPilot homepage as a single-page HTML/CSS/JS site matching the ChatSEO aesthetic (Montserrat, blue #3B82F6, rounded sections, white backgrounds).

**Architecture:** Single `index.html` file with embedded `<style>` and `<script>` blocks. No build tools, no framework — pure vanilla for Hostinger Horizons compatibility. CSS custom properties for the design system. IntersectionObserver for scroll animations.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox), vanilla JS, Google Fonts (Montserrat), Lucide Icons (CDN)

**Spec:** `docs/superpowers/specs/2026-04-01-exportpilot-homepage-design.md`

---

## File Structure

```
index.html          — Complete single-page site (HTML + embedded CSS + embedded JS)
```

Single file by design — no build step, drag-and-drop deploy to Hostinger. All CSS in a `<style>` block, all JS in a `<script>` block at the end.

---

### Task 1: HTML scaffold + CSS design system + Header

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create the base HTML with design system CSS and header markup**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ExportPilot — L'ultime outil pour votre développement export</title>
  <meta name="description" content="ExportPilot combine expertise terrain, data et digital pour ouvrir vos marchés à l'international. Audit export, accompagnement mensuel, missions terrain.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    /* ========== DESIGN SYSTEM ========== */
    :root {
      --color-primary: #3B82F6;
      --color-primary-dark: #1E40AF;
      --color-primary-light: #DBEAFE;
      --color-primary-lighter: #EFF6FF;
      --color-text: #111827;
      --color-text-secondary: #6B7280;
      --color-bg: #FFFFFF;
      --color-bg-alt: #F8FAFC;
      --color-border: #E5E7EB;
      --color-dark: #111827;
      --font-family: 'Montserrat', sans-serif;
      --radius-sm: 8px;
      --radius-md: 16px;
      --radius-lg: 48px;
      --radius-full: 999px;
      --shadow-card: 0 1px 3px rgba(0,0,0,0.08);
      --shadow-card-hover: 0 4px 12px rgba(0,0,0,0.12);
      --max-width: 1140px;
    }

    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    html { scroll-behavior: smooth; }

    body {
      font-family: var(--font-family);
      color: var(--color-text);
      background: var(--color-bg);
      line-height: 1.6;
      -webkit-font-smoothing: antialiased;
    }

    .container { max-width: var(--max-width); margin: 0 auto; padding: 0 24px; }

    h1 { font-size: 52px; font-weight: 800; line-height: 1.15; }
    h2 { font-size: 38px; font-weight: 700; line-height: 1.2; }
    h3 { font-size: 22px; font-weight: 700; line-height: 1.3; }

    .btn {
      display: inline-flex; align-items: center; gap: 8px;
      padding: 14px 28px; border-radius: var(--radius-sm);
      font-family: var(--font-family); font-size: 16px; font-weight: 600;
      text-decoration: none; cursor: pointer; border: 2px solid transparent;
      transition: all 0.2s ease;
    }
    .btn-primary {
      background: var(--color-primary); color: #fff; border-color: var(--color-primary);
    }
    .btn-primary:hover { background: var(--color-primary-dark); border-color: var(--color-primary-dark); }
    .btn-secondary {
      background: transparent; color: var(--color-primary); border-color: var(--color-primary);
    }
    .btn-secondary:hover { background: var(--color-primary-lighter); }
    .btn-lg { padding: 18px 36px; font-size: 18px; }

    .pill {
      display: inline-block; padding: 6px 16px; border-radius: var(--radius-full);
      background: var(--color-primary-light); color: var(--color-primary-dark);
      font-size: 14px; font-weight: 600;
    }

    .badge {
      display: inline-block; padding: 4px 12px; border-radius: var(--radius-full);
      background: var(--color-primary-light); color: var(--color-primary-dark);
      font-size: 12px; font-weight: 600; text-transform: uppercase; letter-spacing: 0.5px;
    }

    .section { padding: 100px 0; }
    .section-rounded {
      border-radius: var(--radius-lg);
      margin: 0 16px;
    }
    .section-title { text-align: center; margin-bottom: 16px; }
    .section-subtitle {
      text-align: center; color: var(--color-text-secondary);
      font-size: 18px; max-width: 600px; margin: 0 auto 60px;
    }

    /* Fade-in animation */
    .fade-in {
      opacity: 0; transform: translateY(24px);
      transition: opacity 0.6s ease, transform 0.6s ease;
    }
    .fade-in.visible { opacity: 1; transform: translateY(0); }

    /* ========== HEADER ========== */
    .header {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      background: rgba(255,255,255,0.95); backdrop-filter: blur(8px);
      transition: box-shadow 0.3s ease;
    }
    .header.scrolled { box-shadow: 0 1px 8px rgba(0,0,0,0.08); }
    .header-inner {
      display: flex; align-items: center; justify-content: space-between;
      height: 72px;
    }
    .logo {
      font-size: 22px; font-weight: 800; color: var(--color-text);
      text-decoration: none;
    }
    .logo span { color: var(--color-primary); }
    .nav { display: flex; align-items: center; gap: 32px; }
    .nav a {
      color: var(--color-text-secondary); text-decoration: none;
      font-size: 15px; font-weight: 500; transition: color 0.2s;
    }
    .nav a:hover { color: var(--color-primary); }
    .header-cta .btn { padding: 10px 22px; font-size: 14px; }
  </style>
</head>
<body>
  <!-- HEADER -->
  <header class="header" id="header">
    <div class="container header-inner">
      <a href="#" class="logo">Export<span>Pilot</span></a>
      <nav class="nav">
        <a href="#offre">Offre</a>
        <a href="#methode">Méthode</a>
        <a href="#temoignages">Témoignages</a>
        <a href="#faq">FAQ</a>
      </nav>
      <div class="header-cta">
        <a href="#cta" class="btn btn-primary">Demander un audit</a>
      </div>
    </div>
  </header>

  <!-- Sections will be added in subsequent tasks -->

  <script>
    // Header scroll shadow
    const header = document.getElementById('header');
    window.addEventListener('scroll', () => {
      header.classList.toggle('scrolled', window.scrollY > 10);
    });

    // Fade-in on scroll
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible');
        }
      });
    }, { threshold: 0.1 });

    document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));
  </script>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

Run: `open /Users/delmareclement/Desktop/CLAUDE/ProjetExport/index.html`
Expected: White page with sticky header showing "ExportPilot" logo, 4 nav links, and blue "Demander un audit" button. Header gains shadow on scroll.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: scaffold ExportPilot homepage with design system and sticky header"
```

---

### Task 2: Hero section

**Files:**
- Modify: `index.html` — add hero HTML after `</header>`, add hero CSS before `</style>`

- [ ] **Step 1: Add hero CSS before the closing `</style>` tag**

```css
/* ========== HERO ========== */
.hero {
  padding: 160px 0 100px;
  text-align: center;
  background: linear-gradient(180deg, var(--color-primary-lighter) 0%, rgba(219,234,254,0.2) 40%, var(--color-bg) 100%);
  position: relative;
  overflow: hidden;
}
.hero-pill { margin-bottom: 24px; }
.hero h1 { margin-bottom: 24px; }
.hero h1 .accent { color: var(--color-primary); }
.hero-subtitle {
  color: var(--color-text-secondary); font-size: 18px;
  max-width: 640px; margin: 0 auto 40px; line-height: 1.7;
}
.hero-buttons { display: flex; gap: 16px; justify-content: center; margin-bottom: 40px; }
.hero-proof {
  display: flex; align-items: center; justify-content: center; gap: 12px;
  color: var(--color-text-secondary); font-size: 14px; font-weight: 500;
}
.hero-flags { display: flex; gap: 6px; font-size: 20px; }

/* World map background */
.hero-map {
  position: absolute; bottom: -20px; left: 50%; transform: translateX(-50%);
  width: 900px; height: 400px; opacity: 0.08; pointer-events: none;
}
.hero-map svg { width: 100%; height: 100%; }
```

- [ ] **Step 2: Add hero HTML after `</header>`**

```html
<!-- HERO -->
<section class="hero">
  <div class="hero-map">
    <svg viewBox="0 0 900 400" fill="none" xmlns="http://www.w3.org/2000/svg">
      <!-- Simplified world map dots -->
      <!-- Europe -->
      <circle cx="420" cy="120" r="4" fill="#3B82F6"/>
      <circle cx="440" cy="130" r="3" fill="#3B82F6"/>
      <circle cx="460" cy="115" r="3" fill="#3B82F6"/>
      <circle cx="430" cy="140" r="3" fill="#3B82F6"/>
      <circle cx="450" cy="145" r="2" fill="#3B82F6"/>
      <!-- Africa -->
      <circle cx="430" cy="200" r="4" fill="#3B82F6"/>
      <circle cx="450" cy="220" r="3" fill="#3B82F6"/>
      <circle cx="420" cy="240" r="3" fill="#3B82F6"/>
      <circle cx="460" cy="250" r="2" fill="#3B82F6"/>
      <circle cx="440" cy="270" r="3" fill="#3B82F6"/>
      <!-- Middle East -->
      <circle cx="520" cy="160" r="3" fill="#3B82F6"/>
      <circle cx="540" cy="170" r="3" fill="#3B82F6"/>
      <circle cx="510" cy="175" r="2" fill="#3B82F6"/>
      <!-- Americas -->
      <circle cx="220" cy="140" r="3" fill="#3B82F6"/>
      <circle cx="240" cy="180" r="3" fill="#3B82F6"/>
      <circle cx="260" cy="250" r="3" fill="#3B82F6"/>
      <!-- Asia -->
      <circle cx="620" cy="150" r="3" fill="#3B82F6"/>
      <circle cx="680" cy="160" r="3" fill="#3B82F6"/>
      <circle cx="700" cy="180" r="2" fill="#3B82F6"/>
      <!-- Connection lines -->
      <line x1="420" y1="120" x2="430" y2="200" stroke="#3B82F6" stroke-width="1" stroke-dasharray="4 4" opacity="0.5"/>
      <line x1="420" y1="120" x2="520" y2="160" stroke="#3B82F6" stroke-width="1" stroke-dasharray="4 4" opacity="0.5"/>
      <line x1="420" y1="120" x2="220" y2="140" stroke="#3B82F6" stroke-width="1" stroke-dasharray="4 4" opacity="0.4"/>
      <line x1="420" y1="120" x2="620" y2="150" stroke="#3B82F6" stroke-width="1" stroke-dasharray="4 4" opacity="0.3"/>
      <line x1="430" y1="200" x2="520" y2="160" stroke="#3B82F6" stroke-width="1" stroke-dasharray="4 4" opacity="0.4"/>
      <line x1="430" y1="200" x2="450" y2="220" stroke="#3B82F6" stroke-width="1" stroke-dasharray="4 4" opacity="0.5"/>
      <!-- Pulse circles on key nodes -->
      <circle cx="420" cy="120" r="8" fill="none" stroke="#3B82F6" stroke-width="1" opacity="0.3">
        <animate attributeName="r" values="8;16;8" dur="3s" repeatCount="indefinite"/>
        <animate attributeName="opacity" values="0.3;0;0.3" dur="3s" repeatCount="indefinite"/>
      </circle>
      <circle cx="430" cy="200" r="8" fill="none" stroke="#3B82F6" stroke-width="1" opacity="0.3">
        <animate attributeName="r" values="8;16;8" dur="3s" begin="1s" repeatCount="indefinite"/>
        <animate attributeName="opacity" values="0.3;0;0.3" dur="3s" begin="1s" repeatCount="indefinite"/>
      </circle>
    </svg>
  </div>
  <div class="container">
    <div class="hero-pill">
      <span class="pill">La plateforme export digitalisée</span>
    </div>
    <h1>L'ultime outil pour votre<br>développement <span class="accent">EXPORT</span></h1>
    <p class="hero-subtitle">ExportPilot combine expertise terrain, data et digital pour ouvrir vos marchés à l'international. Vous restez l'acteur commercial, nous ouvrons les portes.</p>
    <div class="hero-buttons">
      <a href="#cta" class="btn btn-primary btn-lg">Demander mon audit export</a>
      <a href="#offre" class="btn btn-secondary btn-lg">Découvrir l'offre</a>
    </div>
    <div class="hero-proof">
      <span>Accompagnement de PME françaises vers 15+ pays</span>
      <div class="hero-flags">
        <span>🇫🇷</span><span>🇲🇦</span><span>🇸🇳</span><span>🇨🇮</span><span>🇩🇪</span><span>🇦🇪</span>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Refresh browser and verify**

Expected: Hero section with blue gradient background, pill badge, large headline with "EXPORT" in blue, subtitle, two CTA buttons (blue solid + blue outline), social proof line with flags. Subtle animated world map dots in background.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add hero section with world map SVG and CTAs"
```

---

### Task 3: Stats banner

**Files:**
- Modify: `index.html` — add stats CSS + HTML after hero section

- [ ] **Step 1: Add stats CSS before `</style>`**

```css
/* ========== STATS ========== */
.stats { padding: 60px 0; }
.stats-grid {
  display: flex; justify-content: center; align-items: center; gap: 0;
}
.stat {
  text-align: center; padding: 0 48px;
  border-right: 1px solid var(--color-border);
}
.stat:last-child { border-right: none; }
.stat-number {
  font-size: 44px; font-weight: 800; color: var(--color-primary);
  line-height: 1;
}
.stat-label {
  font-size: 15px; color: var(--color-text-secondary);
  margin-top: 8px; font-weight: 500;
}
```

- [ ] **Step 2: Add stats HTML after the hero `</section>`**

```html
<!-- STATS -->
<section class="stats fade-in">
  <div class="container">
    <div class="stats-grid">
      <div class="stat">
        <div class="stat-number">44 500</div>
        <div class="stat-label">exportateurs français chaque année</div>
      </div>
      <div class="stat">
        <div class="stat-number">26%</div>
        <div class="stat-label">abandonnent en cours de route</div>
      </div>
      <div class="stat">
        <div class="stat-number">8+</div>
        <div class="stat-label">ans d'expérience terrain</div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Refresh browser and verify**

Expected: 3 stats in a row with blue numbers, gray labels, vertical dividers between them. Fades in on scroll.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add key stats banner section"
```

---

### Task 4: 4 pillars / offer section

**Files:**
- Modify: `index.html` — add pillars CSS + HTML after stats

- [ ] **Step 1: Add pillars CSS before `</style>`**

```css
/* ========== PILLARS ========== */
.pillars { padding: 100px 0 40px; }
.pillar {
  display: flex; align-items: center; gap: 60px;
  padding: 60px 0;
}
.pillar:nth-child(even) { flex-direction: row-reverse; }
.pillar-content { flex: 1; }
.pillar-content .badge { margin-bottom: 16px; }
.pillar-content h3 { margin-bottom: 16px; font-size: 28px; }
.pillar-content p {
  color: var(--color-text-secondary); font-size: 17px;
  line-height: 1.7; margin-bottom: 16px;
}
.pillar-price {
  font-size: 15px; font-weight: 600; color: var(--color-primary);
  margin-bottom: 20px;
}
.pillar-link {
  color: var(--color-primary); font-weight: 600; text-decoration: none;
  font-size: 16px; transition: gap 0.2s;
  display: inline-flex; align-items: center; gap: 6px;
}
.pillar-link:hover { gap: 10px; }
.pillar-visual {
  flex: 1; min-height: 300px; border-radius: var(--radius-md);
  background: var(--color-primary-lighter);
  display: flex; align-items: center; justify-content: center;
}
.pillar-icon { font-size: 64px; opacity: 0.6; }

/* Mini pricing cards inside pillar */
.mini-pricing {
  display: flex; gap: 12px; margin: 20px 0;
}
.mini-price-card {
  flex: 1; padding: 16px; border-radius: var(--radius-sm);
  border: 1px solid var(--color-border); text-align: center;
  background: var(--color-bg); transition: border-color 0.2s, box-shadow 0.2s;
}
.mini-price-card:hover { border-color: var(--color-primary); box-shadow: var(--shadow-card-hover); }
.mini-price-card.popular {
  border-color: var(--color-primary); position: relative;
}
.mini-price-card.popular::before {
  content: 'Populaire';
  position: absolute; top: -10px; left: 50%; transform: translateX(-50%);
  background: var(--color-primary); color: white;
  font-size: 11px; font-weight: 600; padding: 2px 10px;
  border-radius: var(--radius-full);
}
.mini-price-name { font-size: 14px; font-weight: 600; margin-bottom: 4px; }
.mini-price-amount { font-size: 20px; font-weight: 800; color: var(--color-primary); }
.mini-price-unit { font-size: 12px; color: var(--color-text-secondary); }
```

- [ ] **Step 2: Add pillars HTML after the stats `</section>`**

```html
<!-- OFFRE — 4 PILIERS -->
<section class="pillars" id="offre">
  <div class="container">
    <h2 class="section-title fade-in">Une offre complète pour chaque étape de votre export</h2>
    <p class="section-subtitle fade-in">De l'audit initial à l'accompagnement terrain, ExportPilot structure votre développement international.</p>

    <!-- Pillar 1: Audit -->
    <div class="pillar fade-in">
      <div class="pillar-visual">
        <div class="pillar-icon">📋</div>
      </div>
      <div class="pillar-content">
        <span class="badge">Point d'entrée obligatoire</span>
        <h3>Le diagnostic qui change tout</h3>
        <p>Un audit complet de votre potentiel export : marchés cibles, positionnement concurrentiel, capacité opérationnelle. Le socle de toute stratégie réussie.</p>
        <div class="pillar-price">À partir de 990 € HT</div>
        <a href="#cta" class="pillar-link">Demander mon audit →</a>
      </div>
    </div>

    <!-- Pillar 2: Abonnements -->
    <div class="pillar fade-in">
      <div class="pillar-content">
        <span class="badge">Accompagnement continu</span>
        <h3>Un copilote, pas un coup d'éclat</h3>
        <p>Choisissez la formule adaptée à votre ambition. Engagement 6 mois minimum pour des résultats mesurables.</p>
        <div class="mini-pricing">
          <div class="mini-price-card">
            <div class="mini-price-name">Starter</div>
            <div class="mini-price-amount">590 €</div>
            <div class="mini-price-unit">/mois HT</div>
          </div>
          <div class="mini-price-card popular">
            <div class="mini-price-name">Business</div>
            <div class="mini-price-amount">790 €</div>
            <div class="mini-price-unit">/mois HT</div>
          </div>
          <div class="mini-price-card">
            <div class="mini-price-name">Expert</div>
            <div class="mini-price-amount">2 490 €</div>
            <div class="mini-price-unit">/mois HT</div>
          </div>
        </div>
        <a href="#" class="pillar-link">Comparer les formules →</a>
      </div>
      <div class="pillar-visual">
        <div class="pillar-icon">📊</div>
      </div>
    </div>

    <!-- Pillar 3: Missions terrain -->
    <div class="pillar fade-in">
      <div class="pillar-visual">
        <div class="pillar-icon">🌍</div>
      </div>
      <div class="pillar-content">
        <span class="badge">Représentation</span>
        <h3>Votre présence là où ça se joue</h3>
        <p>Représentation en salon, prospection terrain, rencontres acheteurs. Des missions ponctuelles, vendues séparément, pour un impact maximal.</p>
        <a href="#" class="pillar-link">En savoir plus →</a>
      </div>
    </div>

    <!-- Pillar 4: Services complémentaires -->
    <div class="pillar fade-in">
      <div class="pillar-content">
        <span class="badge">À la carte</span>
        <h3>Formation, conformité, recrutement agents</h3>
        <p>Des services one-shot pour renforcer votre capacité export : formation interne, conformité documentaire, aide au financement, recrutement d'agents locaux.</p>
        <a href="#" class="pillar-link">Découvrir les services →</a>
      </div>
      <div class="pillar-visual">
        <div class="pillar-icon">🎓</div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Refresh browser and verify**

Expected: Section title + subtitle centered, then 4 feature blocks alternating image-left/text-right. Each has a badge, title, description, CTA link. Pillar 2 has 3 mini pricing cards with "Populaire" badge on Business.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add 4 pillars offer section with pricing cards"
```

---

### Task 5: "Why ExportPilot" section

**Files:**
- Modify: `index.html` — add why CSS + HTML after pillars

- [ ] **Step 1: Add why CSS before `</style>`**

```css
/* ========== WHY ========== */
.why {
  padding: 100px 0;
  background: var(--color-bg-alt);
  border-radius: var(--radius-lg);
  margin: 0 16px;
}
.why-grid {
  display: grid; grid-template-columns: repeat(3, 1fr); gap: 40px;
  margin-bottom: 48px;
}
.why-card {
  text-align: center; padding: 32px 24px;
}
.why-icon {
  width: 56px; height: 56px; border-radius: 12px;
  background: var(--color-primary-light);
  display: flex; align-items: center; justify-content: center;
  margin: 0 auto 20px; font-size: 24px;
}
.why-card h3 { font-size: 18px; margin-bottom: 12px; }
.why-card p { color: var(--color-text-secondary); font-size: 15px; line-height: 1.6; }
.why-cta { text-align: center; }
.why-mention {
  display: block; margin-top: 12px;
  color: var(--color-text-secondary); font-size: 14px;
}
```

- [ ] **Step 2: Add why HTML after pillars `</section>`**

```html
<!-- POURQUOI EXPORTPILOT -->
<section class="why section-rounded fade-in">
  <div class="container">
    <h2 class="section-title">Pas un cabinet de conseil classique.<br>Votre passeur digital vers l'export.</h2>
    <p class="section-subtitle">Ce qui nous différencie des approches traditionnelles.</p>
    <div class="why-grid">
      <div class="why-card">
        <div class="why-icon">📈</div>
        <h3>Transparence totale</h3>
        <p>Des ratios de conversion transparents, pas des promesses de volume. Vous savez exactement ce que vous obtenez.</p>
      </div>
      <div class="why-card">
        <div class="why-icon">💻</div>
        <h3>Méthodologie digitalisée</h3>
        <p>Une méthodologie digitalisée, pas des PowerPoint. Des outils concrets et un suivi en temps réel.</p>
      </div>
      <div class="why-card">
        <div class="why-icon">🤝</div>
        <h3>Passeur terrain</h3>
        <p>Un passeur terrain, pas un commercial à votre place. On ouvre les portes, vous concluez les deals.</p>
      </div>
    </div>
    <div class="why-cta">
      <a href="#cta" class="btn btn-primary btn-lg">Demander mon audit export</a>
      <span class="why-mention">Sans engagement · Premier échange gratuit</span>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Refresh and verify**

Expected: Light gray rounded section with 3 cards in a row (icon, title, description), CTA button centered below.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add why ExportPilot value proposition section"
```

---

### Task 6: "How it works" section

**Files:**
- Modify: `index.html` — add steps CSS + HTML after why section

- [ ] **Step 1: Add steps CSS before `</style>`**

```css
/* ========== STEPS ========== */
.steps { padding: 100px 0; }
.steps-grid {
  display: flex; align-items: flex-start; gap: 24px;
  position: relative;
}
.steps-grid::before {
  content: ''; position: absolute;
  top: 32px; left: calc(16.66% + 12px); right: calc(16.66% + 12px);
  height: 2px; background: var(--color-primary-light);
}
.step {
  flex: 1; text-align: center; position: relative; z-index: 1;
}
.step-number {
  width: 64px; height: 64px; border-radius: 50%;
  background: var(--color-primary); color: white;
  display: flex; align-items: center; justify-content: center;
  font-size: 24px; font-weight: 800;
  margin: 0 auto 20px;
}
.step h3 { margin-bottom: 12px; }
.step p {
  color: var(--color-text-secondary); font-size: 15px;
  line-height: 1.6; max-width: 280px; margin: 0 auto;
}
```

- [ ] **Step 2: Add steps HTML after why `</section>`**

```html
<!-- COMMENT ÇA MARCHE -->
<section class="steps section" id="methode">
  <div class="container">
    <h2 class="section-title fade-in">3 étapes pour lancer votre export</h2>
    <p class="section-subtitle fade-in">Un parcours clair, structuré, sans surprise.</p>
    <div class="steps-grid fade-in">
      <div class="step">
        <div class="step-number">1</div>
        <h3>Audit export</h3>
        <p>On analyse votre potentiel, vos marchés et votre capacité opérationnelle.</p>
      </div>
      <div class="step">
        <div class="step-number">2</div>
        <h3>Plan d'action</h3>
        <p>Vous recevez une feuille de route claire : marchés cibles, stratégie, outils.</p>
      </div>
      <div class="step">
        <div class="step-number">3</div>
        <h3>Accompagnement</h3>
        <p>On vous accompagne avec un abonnement mensuel et des missions terrain ciblées.</p>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Refresh and verify**

Expected: 3 steps in a row, numbered circles (blue), connected by a light blue line. Each with title and description.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add 3-step how it works section"
```

---

### Task 7: Testimonials section

**Files:**
- Modify: `index.html` — add testimonials CSS + HTML after steps

- [ ] **Step 1: Add testimonials CSS before `</style>`**

```css
/* ========== TESTIMONIALS ========== */
.testimonials {
  padding: 100px 0;
  background: var(--color-bg-alt);
  border-radius: var(--radius-lg);
  margin: 0 16px;
}
.testimonials-grid {
  display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px;
}
.testimonial-card {
  background: var(--color-bg); border-radius: var(--radius-md);
  padding: 32px; box-shadow: var(--shadow-card);
  transition: box-shadow 0.2s;
}
.testimonial-card:hover { box-shadow: var(--shadow-card-hover); }
.testimonial-quote {
  color: var(--color-text); font-size: 15px;
  line-height: 1.7; margin-bottom: 24px;
  font-style: italic;
}
.testimonial-quote::before { content: '"'; }
.testimonial-quote::after { content: '"'; }
.testimonial-author {
  display: flex; align-items: center; gap: 12px;
}
.testimonial-avatar {
  width: 44px; height: 44px; border-radius: 50%;
  background: var(--color-primary-light);
  display: flex; align-items: center; justify-content: center;
  font-weight: 700; color: var(--color-primary-dark); font-size: 16px;
}
.testimonial-name { font-size: 14px; font-weight: 700; }
.testimonial-role { font-size: 13px; color: var(--color-text-secondary); }
```

- [ ] **Step 2: Add testimonials HTML after steps `</section>`**

```html
<!-- TÉMOIGNAGES -->
<section class="testimonials section-rounded fade-in" id="temoignages">
  <div class="container">
    <h2 class="section-title">Ils ont franchi le pas de l'export</h2>
    <p class="section-subtitle">Des dirigeants de PME qui ont structuré leur développement international.</p>
    <div class="testimonials-grid">
      <div class="testimonial-card">
        <p class="testimonial-quote">Grâce à ExportPilot, nous avons identifié 3 marchés prioritaires en Afrique de l'Ouest et signé notre premier contrat en 4 mois.</p>
        <div class="testimonial-author">
          <div class="testimonial-avatar">ML</div>
          <div>
            <div class="testimonial-name">Marc L.</div>
            <div class="testimonial-role">Dirigeant, PME agroalimentaire</div>
          </div>
        </div>
      </div>
      <div class="testimonial-card">
        <p class="testimonial-quote">L'audit export a mis en lumière des opportunités au Maghreb qu'on n'avait pas envisagées. L'accompagnement mensuel nous a donné la structure qui nous manquait.</p>
        <div class="testimonial-author">
          <div class="testimonial-avatar">SD</div>
          <div>
            <div class="testimonial-name">Sophie D.</div>
            <div class="testimonial-role">DG, industrie mécanique</div>
          </div>
        </div>
      </div>
      <div class="testimonial-card">
        <p class="testimonial-quote">Ce qui change avec ExportPilot, c'est la transparence. On sait exactement où on en est, quels sont les ratios, et ce qui reste à faire.</p>
        <div class="testimonial-author">
          <div class="testimonial-avatar">PB</div>
          <div>
            <div class="testimonial-name">Pierre B.</div>
            <div class="testimonial-role">Fondateur, startup cleantech</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Refresh and verify**

Expected: Light gray rounded section, 3 testimonial cards in a row with quote, avatar initials, name and role.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add testimonials section with placeholder quotes"
```

---

### Task 8: FAQ accordion section

**Files:**
- Modify: `index.html` — add FAQ CSS + HTML after testimonials, add JS before `</script>`

- [ ] **Step 1: Add FAQ CSS before `</style>`**

```css
/* ========== FAQ ========== */
.faq { padding: 100px 0; }
.faq-list { max-width: 720px; margin: 0 auto; }
.faq-item {
  border-bottom: 1px solid var(--color-border);
}
.faq-question {
  width: 100%; background: none; border: none; cursor: pointer;
  display: flex; justify-content: space-between; align-items: center;
  padding: 24px 0; font-family: var(--font-family);
  font-size: 17px; font-weight: 600; color: var(--color-text);
  text-align: left;
}
.faq-question:hover { color: var(--color-primary); }
.faq-icon {
  font-size: 24px; color: var(--color-primary);
  transition: transform 0.3s ease;
  flex-shrink: 0; margin-left: 16px;
}
.faq-item.open .faq-icon { transform: rotate(45deg); }
.faq-answer {
  max-height: 0; overflow: hidden;
  transition: max-height 0.3s ease, padding 0.3s ease;
}
.faq-item.open .faq-answer {
  max-height: 300px; padding-bottom: 24px;
}
.faq-answer p {
  color: var(--color-text-secondary); font-size: 15px; line-height: 1.7;
}
```

- [ ] **Step 2: Add FAQ HTML after testimonials `</section>`**

```html
<!-- FAQ -->
<section class="faq section" id="faq">
  <div class="container">
    <h2 class="section-title fade-in">Toutes les réponses à vos questions</h2>
    <p class="section-subtitle fade-in">Tout ce que vous devez savoir avant de vous lancer.</p>
    <div class="faq-list fade-in">
      <div class="faq-item">
        <button class="faq-question">Combien coûte un audit export ?<span class="faq-icon">+</span></button>
        <div class="faq-answer"><p>L'audit export est proposé entre 990 € et 2 990 € HT selon la complexité de votre projet et le nombre de marchés à analyser. C'est un investissement qui pose les bases de toute votre stratégie export.</p></div>
      </div>
      <div class="faq-item">
        <button class="faq-question">Quelle est la durée d'engagement ?<span class="faq-icon">+</span></button>
        <div class="faq-answer"><p>Les abonnements mensuels ont un engagement minimum de 6 mois. Ce délai est nécessaire pour obtenir des résultats mesurables à l'international. L'audit, lui, est un service ponctuel sans engagement de suite.</p></div>
      </div>
      <div class="faq-item">
        <button class="faq-question">En quoi ExportPilot est différent d'un cabinet de conseil ?<span class="faq-icon">+</span></button>
        <div class="faq-answer"><p>Nous sommes un « passeur », pas un cabinet traditionnel. Notre approche est 100% digitalisée, transparente sur les ratios de conversion, et orientée terrain. Pas de rapports PowerPoint interminables — des actions concrètes et des résultats mesurables.</p></div>
      </div>
      <div class="faq-item">
        <button class="faq-question">Quels marchés couvrez-vous ?<span class="faq-icon">+</span></button>
        <div class="faq-answer"><p>Notre expertise couvre l'Afrique, le Maghreb, le Moyen-Orient et l'Europe de l'Est. Nous sommes également ouverts à d'autres zones géographiques selon votre projet et nos partenaires locaux.</p></div>
      </div>
      <div class="faq-item">
        <button class="faq-question">Je n'ai jamais exporté, c'est pour moi ?<span class="faq-icon">+</span></button>
        <div class="faq-answer"><p>Absolument. L'audit export est justement conçu pour évaluer votre potentiel et structurer votre première démarche. Beaucoup de nos clients en sont à leur premier projet export.</p></div>
      </div>
      <div class="faq-item">
        <button class="faq-question">Que comprend l'abonnement mensuel ?<span class="faq-icon">+</span></button>
        <div class="faq-answer"><p>Selon la formule choisie (Starter, Business ou Expert), l'abonnement inclut : sourcing de prospects, campagnes de prospection digitale, suivi des leads, reporting mensuel, et un accès à notre dashboard client. Les missions terrain sont vendues séparément.</p></div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Add FAQ toggle JS before `</script>`**

```javascript
// FAQ accordion
document.querySelectorAll('.faq-question').forEach(btn => {
  btn.addEventListener('click', () => {
    const item = btn.parentElement;
    const wasOpen = item.classList.contains('open');
    // Close all
    document.querySelectorAll('.faq-item').forEach(i => i.classList.remove('open'));
    // Toggle clicked
    if (!wasOpen) item.classList.add('open');
  });
});
```

- [ ] **Step 4: Refresh and verify**

Expected: 6 FAQ items, each clickable to expand/collapse. "+" icon rotates to "×" when open. Only one open at a time.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add FAQ accordion section with 6 questions"
```

---

### Task 9: Final CTA + Footer

**Files:**
- Modify: `index.html` — add CTA + footer CSS + HTML after FAQ

- [ ] **Step 1: Add CTA + footer CSS before `</style>`**

```css
/* ========== CTA FINAL ========== */
.cta-final {
  padding: 100px 0; text-align: center;
  background: linear-gradient(180deg, var(--color-primary-lighter) 0%, var(--color-primary-light) 100%);
  border-radius: var(--radius-lg);
  margin: 0 16px 60px;
}
.cta-final h2 { margin-bottom: 16px; }
.cta-final .section-subtitle { margin-bottom: 40px; }
.cta-mention {
  display: block; margin-top: 16px;
  color: var(--color-text-secondary); font-size: 14px;
}

/* ========== FOOTER ========== */
.footer {
  background: var(--color-dark); color: #fff;
  padding: 60px 0 32px;
}
.footer-grid {
  display: grid; grid-template-columns: 2fr 1fr 1fr 1fr;
  gap: 40px; margin-bottom: 48px;
}
.footer-brand .logo { color: #fff; font-size: 20px; display: inline-block; margin-bottom: 12px; }
.footer-brand .logo span { color: var(--color-primary); }
.footer-tagline { color: #9CA3AF; font-size: 14px; line-height: 1.6; }
.footer-col h4 {
  font-size: 14px; font-weight: 700; text-transform: uppercase;
  letter-spacing: 0.5px; margin-bottom: 16px; color: #D1D5DB;
}
.footer-col a {
  display: block; color: #9CA3AF; text-decoration: none;
  font-size: 14px; padding: 4px 0; transition: color 0.2s;
}
.footer-col a:hover { color: var(--color-primary); }
.footer-bottom {
  border-top: 1px solid #1F2937;
  padding-top: 24px;
  display: flex; justify-content: space-between; align-items: center;
}
.footer-copy { color: #6B7280; font-size: 13px; }
.footer-social a {
  color: #9CA3AF; text-decoration: none; font-size: 14px;
  transition: color 0.2s;
}
.footer-social a:hover { color: var(--color-primary); }
```

- [ ] **Step 2: Add CTA + footer HTML after FAQ `</section>`**

```html
<!-- CTA FINAL -->
<section class="cta-final section-rounded fade-in" id="cta">
  <div class="container">
    <h2>Prêt à ouvrir de nouveaux marchés ?</h2>
    <p class="section-subtitle">Commencez par un audit export. Sans engagement, sans surprise.</p>
    <a href="mailto:contact@exportpilot.fr" class="btn btn-primary btn-lg">Demander mon audit export</a>
    <span class="cta-mention">Premier échange gratuit · Réponse sous 48h</span>
  </div>
</section>

<!-- FOOTER -->
<footer class="footer">
  <div class="container">
    <div class="footer-grid">
      <div class="footer-brand">
        <a href="#" class="logo">Export<span>Pilot</span></a>
        <p class="footer-tagline">Votre passeur digital vers l'export. On ouvre les portes, vous restez l'acteur commercial.</p>
      </div>
      <div class="footer-col">
        <h4>Navigation</h4>
        <a href="#offre">Offre</a>
        <a href="#methode">Méthode</a>
        <a href="#temoignages">Témoignages</a>
        <a href="#faq">FAQ</a>
      </div>
      <div class="footer-col">
        <h4>Légal</h4>
        <a href="#">Mentions légales</a>
        <a href="#">CGV</a>
        <a href="#">Politique de confidentialité</a>
      </div>
      <div class="footer-col">
        <h4>Contact</h4>
        <a href="mailto:contact@exportpilot.fr">contact@exportpilot.fr</a>
        <a href="https://linkedin.com" target="_blank" rel="noopener">LinkedIn</a>
      </div>
    </div>
    <div class="footer-bottom">
      <span class="footer-copy">© 2026 ExportPilot. Tous droits réservés.</span>
    </div>
  </div>
</footer>
```

- [ ] **Step 3: Refresh and verify**

Expected: Blue gradient CTA section with headline, subtitle, large button, and mention. Dark footer with 4 columns (brand, navigation, legal, contact) and copyright bar.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add final CTA section and dark footer"
```

---

### Task 10: Re-initialize IntersectionObserver and final polish

**Files:**
- Modify: `index.html` — move observer init to end of `<script>`, verify all fade-in elements work

- [ ] **Step 1: Replace the observer code in `<script>` to ensure it runs after all DOM is loaded**

Replace the entire `<script>` block content with:

```javascript
document.addEventListener('DOMContentLoaded', () => {
  // Header scroll shadow
  const header = document.getElementById('header');
  window.addEventListener('scroll', () => {
    header.classList.toggle('scrolled', window.scrollY > 10);
  });

  // Fade-in on scroll
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));

  // FAQ accordion
  document.querySelectorAll('.faq-question').forEach(btn => {
    btn.addEventListener('click', () => {
      const item = btn.parentElement;
      const wasOpen = item.classList.contains('open');
      document.querySelectorAll('.faq-item').forEach(i => i.classList.remove('open'));
      if (!wasOpen) item.classList.add('open');
    });
  });

  // Smooth scroll for anchor links
  document.querySelectorAll('a[href^="#"]').forEach(link => {
    link.addEventListener('click', (e) => {
      const target = document.querySelector(link.getAttribute('href'));
      if (target) {
        e.preventDefault();
        target.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
    });
  });
});
```

- [ ] **Step 2: Full page test**

Open `index.html` in browser and verify:
1. Header is sticky with shadow on scroll ✓
2. Nav links smooth-scroll to sections ✓
3. Hero displays with pill, headline, subtitle, CTAs, flags, world map ✓
4. Stats banner shows 3 numbers ✓
5. 4 pillars alternate layout correctly ✓
6. Why section has 3 value cards + CTA ✓
7. Steps show 1-2-3 with connecting line ✓
8. Testimonials show 3 cards ✓
9. FAQ accordion opens/closes ✓
10. Final CTA section with button ✓
11. Footer with 4 columns ✓
12. All sections fade in on scroll ✓

- [ ] **Step 3: Final commit**

```bash
git add index.html
git commit -m "feat: consolidate JS, add smooth scroll, finalize homepage"
```
