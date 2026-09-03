# Portfolio Site — Requirements

**Versione:** 1.0
**Data:** 2026-06-25
**Stato:** Draft

---

## 1. Obiettivo del progetto

Realizzare un sito portfolio personale **self-hosted**, leggero, veloce e a bassa manutenzione, con **analytics di base**. Il sito deve essere completamente responsive (desktop + mobile) e supportare **light e dark mode** (dark di default).

---

## 2. Stack tecnologico

### 2.1 Framework: **Astro**

**Motivazione della scelta:**

| Criterio | Perché Astro vince |
|---|---|
| **Leggero** | Zero JS di default ("islands architecture"). Le pagine statiche pesano pochi KB. |
| **Veloce** | Output HTML statico pre-renderizzato, ottimo Lighthouse out-of-the-box. |
| **Low maintenance** | Niente backend, niente DB. Solo build statica. Update dipendenze minime. |
| **Responsive** | Nessun lock-in CSS: si integra nativamente con vanilla CSS / Tailwind. |
| **Self-hosted friendly** | Output è una cartella `dist/` statica → si serve con qualsiasi web server (Nginx, Caddy, GitHub Pages, Cloudflare Pages, VPS). |
| **DX** | Componenti `.astro`, supporto MDX per contenuti, image optimization nativa. |

**Alternative scartate:**
- *Next.js*: troppo pesante e orientato a app dinamiche; richiede Node runtime per il self-hosting ottimale.
- *Eleventy (11ty)*: ottimo ma meno ergonomico per componenti UI.
- *SvelteKit / Nuxt*: overhead non giustificato per un portfolio statico.

### 2.2 Styling
- **CSS vanilla con custom properties** (CSS variables) per gestire token di colore, spaziature, font scale.
- In alternativa **Tailwind CSS** se si preferisce utility-first (decisione da confermare).

### 2.3 Hosting
- Deploy come sito statico su VPS personale tramite **Caddy** o **Nginx** (self-hosted).
- Build via `astro build` → output `dist/`.

### 2.4 Analytics
- **Plausible** (self-hosted via Docker) oppure **Umami** (self-hosted, free, open source).
- Requisiti: GDPR-compliant, no cookie banner necessario, lightweight (<2 KB script).
- Tracciare: pageviews, referrer, browser, device, paesi. Niente tracking individuale.

---

## 3. Struttura del sito

### 3.1 Sitemap

```
/                       → Homepage
/about                  → Pagina About
/case-study/[slug]      → Pagina dettaglio case study
```

### 3.2 Stile di riferimento

Layout e tono ispirati a [jasonspielman.com](https://jasonspielman.com/): minimal, prima persona, generoso whitespace, copywriting specifico, dettagli da portfolio premium (badge stato, role inline, anno).

### 3.3 Homepage — sezioni (ordine top→bottom)

1. **Hero** — molto minimale, niente bottone CTA. Una frase di posizionamento (h1) + 1 frase su cosa sto facendo ora + un link inline alla sezione progetti.
2. **Loghi** — fascia clienti/tecnologie/collaborazioni discreta, eyebrow uppercase, loghi monocromatici inline, wrap su mobile.
3. **Progetti** — griglia di **cards** in stile Spielman:
   - Minimo **2** cards, massimo **4** cards.
   - Layout: griglia **2×2 su desktop**, **1 colonna su mobile**.
   - Card senza container/background: solo cover image (aspect 4/3, zoom on hover) sopra a metadata + titolo.
   - Metadata: roles inline ("UX Design · Visual Design"), year, status badge opzionale ("Current", "Award winner"), titolo (Bricolage Grotesque), descrizione 1-2 righe.
4. **Valori** — 3 principi, layout a colonne discrete (no card box), separati da divider sottile.

### 3.4 About — pagina dedicata

- Bio estesa, percorso professionale, contatti, eventuale CV download.

### 3.5 Navigazione
- **Header:** altezza 56px, padding orizzontale 24px, background semi-trasparente nero (`rgba(0,0,0,0.1)`). Layout: "Gabriele La Rosa" a sinistra (DM Sans Regular 16px), icona centrale 24×24 (placeholder), link "About" a destra (DM Sans Regular 16px). Nessun toggle theme (sito dark-only in v1).
- **Footer:** copyright, link social/contatti con underline animato.

### 3.6 Case Study Detail page

Pagina di dettaglio progetto, struttura BLUF (Bottom Line Up Front). **Container max-width 1100px**, padding orizzontale di sezione **160px** (desktop ≥1440), padding verticale di sezione **`--space-section` (80px)** (eccetto Hero e TL;DR che hanno override più stretti).

**Sezioni in ordine (top→bottom):**

1. **Hero** (`pt-64 pb-32`)
   - Riga **tag chips** (es. `UX/UI`, `AI`, `Personal Project`)
   - **Titolo progetto** — Space Grotesk Bold 40px, white

2. **TL;DR Card** (`pt-24 pb-32`)
   - Card unica `bg --color-surface`, `rounded-16`, padding 24px, altezza 266px
   - **3 colonne** centrate: `Problem` · `Solution` · `Impact`
   - Ogni colonna: icona 18px + label `DM Sans SemiBold 18px white` + body `DM Sans Regular 16px text-body text-center`
   - Separator: linea verticale 1px alta 177px tra le colonne (`--color-border`)

3. **Meta row** (sotto TL;DR card, `gap-32`)
   - **Left-aligned** all'interno del container (1100px), separatori ✦ inline su md+
   - Esempio: `Role: UX/Product Designer ✦ Duration: 6 weeks ✦ Team: just me ✦ Tools: Claude Code, Figjam`
   - Label: DM Sans Regular text-body · Valore: DM Sans Medium white · Separator ✦ text-muted
   - Su mobile: ogni voce su riga propria, separatori nascosti

4. **Hero Image** (`pt-24 pb-32`)
   - Visual `rounded-16`, altezza 548px, full container width
   - **Default fallback:** background con 4 ellissi sfumati arancione `--accent-2` + cyan `--accent-1` su nero, con noise overlay
   - Sostituibile con cover image reale del progetto

5. **Section: Context + Insights** (`py-42`)
   - **Section label** (vedi pattern §4.5)
   - Titolo Space Grotesk Medium 32px
   - Descrizione DM Sans 16px text-body text-center
   - Griglia **3 Insight Cards** orizzontali (`gap-32`):
     - Card `bg --color-surface`, `rounded-16`, padding 24, altezza 266px
     - Centrata: icona 32px + titolo `DM Sans SemiBold 18px` + body 16px text-body

6. **Section: Problem statement** — solo label + titolo (placeholder per contenuto custom)
7. **Section: Solution** — solo label + titolo
8. **Section: Impact** — solo label + titolo
9. **Section: Iterations & Pivots** — solo label + titolo
10. **Section: Learnings** — solo label + titolo

**Bottom padding pagina:** 120px

---

## 4. Design system

### 4.1 Colori — Dark only (v1)

| Token | Valore | Uso |
|---|---|---|
| `--color-bg` | `#323232` | Background pagina |
| `--color-surface` | `rgba(129, 139, 166, 0.1)` | Background card (TL;DR, Insight Card) |
| `--color-tag-bg` | `rgba(129, 139, 166, 0.19)` | Background tag chip |
| `--color-header-bg` | `rgba(0, 0, 0, 0.1)` | Background header |
| `--color-text-title` | `#FFFFFF` | Titoli |
| `--color-text-body` | `#CCCCCC` | Body, descrizioni |
| `--color-text-tag` | `rgba(255, 255, 255, 0.76)` | Testo tag chip |
| `--color-text-muted` | `#868686` | Separator ✦, micro-text |
| `--color-border` | `rgba(255, 255, 255, 0.1)` | Linee divider sotto i tag |
| `--color-accent-1` | `#9BE2EC` | Accent cyan (link, hover, hero gradient) |
| `--color-accent-2` | `#FC642D` | Accent orange (hero gradient, highlight) |

> **Nota:** light mode è **out of scope per v1**. Sito dark-only.

### 4.2 Tipografia

**Font famiglie:**
- **Hero / D1 (titolo progetto case study):** **Bricolage Grotesque** — `@fontsource/bricolage-grotesque`. Peso: 700 (Bold).
- **Display (titoli sezione):** **Space Grotesk** — `@fontsource/space-grotesk`. Pesi: 500 (Medium), 700 (Bold).
- **Body + UI:** **DM Sans** — `@fontsource/dm-sans`. Pesi: 400 (Regular), 500 (Medium), 600 (SemiBold).

> Self-hosting via `@fontsource/*`. Subset `latin` per minimizzare bundle.

**Type scale (px assoluti dal design Figma):**

| Token | px | Famiglia | Uso |
|---|---|---|---|
| `--text-sm` | 14 | DM Sans Regular | tag chip, micro-label (letter-spacing 0.32px) |
| `--text-base` | 16 | DM Sans Regular | body, descrizioni, meta row |
| `--text-md` | 18 | DM Sans SemiBold | titoli card (Problem/Solution/Impact, Insight) |
| `--text-section` | 32 | Space Grotesk Medium | titoli sezione |
| `--text-hero` | fluido 32→44 | Bricolage Grotesque SemiBold | titolo progetto hero (D1), `clamp(32px, calc(22.4px + 1.5vw), 44px)` — 32 su mobile, 44 da 1440px |

**Line-height:**
- Titoli display: `normal` (~1.2)
- Body 16px: 25.6px (1.6)
- Card title 18px: 25.6px

### 4.3 Spaziature

Scala 4/8-based ispirata al ritmo di [sophiayang.co](https://www.sophiayang.co/usdc-rewards) per garantire respiro verticale leggibile.

**Scala raw:**
`4, 8, 12, 16, 24, 32, 48, 64` + alias semantici per ruoli ricorrenti.

| Token | Valore | Ruolo |
|---|---|---|
| `--space-2xs` | 4 | hairline / micro |
| `--space-xs` | 8 | gap interno chip, icon+label |
| `--space-sm` | 12 | inline tag+linea |
| `--space-md` | 16 | heading → prima riga body |
| `--space-lg` | 24 | label→titolo, paragrafi, gap card stack |
| `--space-xl` | 32 | titolo → descrizione/immagine, gap insight grid |
| `--space-2xl` | 48 | tra blocchi dentro una sezione |
| `--space-3xl` | 64 | hero pt |
| `--space-section` | 80 | **default Y delle sezioni** (`Container` py) |
| `--space-block` | 48 | tra blocchi |
| `--space-stack-lg` | 32 | stack vertical large |
| `--space-stack-md` | 24 | stack vertical medium |
| `--space-stack-sm` | 16 | stack vertical small |
| `--space-inline` | 12 | gap inline |
| `--space-card-pad` | 24 | padding interno card |
| `--space-page-bottom` | 120 | padding finale pagina |

> Le sezioni del case study usano `py-[var(--space-section)]` (80px) come default — sostituisce il valore Figma di 42px che risultava troppo serrato.

### 4.4 Radius

| Token | Valore | Uso |
|---|---|---|
| `--radius-tag` | 8px | tag chip |
| `--radius-card` | 16px | card (TL;DR, Insight, Hero image) |

### 4.5 Pattern: Section Label

Componente riusabile **`SectionLabel`** all'inizio di ogni sezione (dopo l'hero):

```
[tag-chip-style label] ───────────────────────────  (linea divider full-width)
```

- Label: DM Sans Regular 14px text-tag, padding `py-8 px-0` (no bg, no radius)
- Linea: `1px` background `--color-border`, `flex: 1`, gap 12px dal label

### 4.6 Breakpoint responsive

| Nome | Min-width |
|---|---|
| `sm` | 640px |
| `md` | 768px |
| `lg` | 1024px |
| `xl` | 1280px |

Approccio **mobile-first**. Sotto `lg` (1024px): container passa a 100% con padding orizzontale 24px, sezioni a 3 colonne collassano in stack verticale, separatori verticali nella TL;DR diventano orizzontali.

---

## 5. Requisiti funzionali

| ID | Requisito |
|---|---|
| F-01 | La homepage mostra hero, loghi, progetti (2-4 cards), valori, nell'ordine specificato. |
| F-02 | La pagina `/about` è raggiungibile dalla navigazione. |
| F-03 | Toggle light/dark mode persistente. |
| F-04 | Dark mode attiva di default al primo visit (se nessuna preferenza utente). |
| F-05 | Tutti i link/CTA navigabili da tastiera (accessibilità). |
| F-06 | Analytics raccoglie pageviews senza cookie. |
| F-07 | Il sito è completamente fruibile senza JavaScript abilitato (eccetto il toggle theme). |

---

## 6. Requisiti non funzionali

| ID | Requisito | Target |
|---|---|---|
| NF-01 | Performance Lighthouse | ≥ 95 mobile, ≥ 98 desktop |
| NF-02 | Accessibility Lighthouse | ≥ 95 |
| NF-03 | SEO Lighthouse | ≥ 95 |
| NF-04 | First Contentful Paint | < 1s su connessione 4G |
| NF-05 | Peso totale pagina (homepage) | < 300 KB compresso |
| NF-06 | Compatibilità browser | Ultimi 2 versioni di Chrome, Firefox, Safari, Edge |
| NF-07 | Tempo di build | < 30s |
| NF-08 | Privacy | Nessun tracker third-party, niente cookie banner necessario |

---

## 7. Accessibilità

- Contrasto colore: rispettare **WCAG AA** (4.5:1 per body, 3:1 per titoli grandi).
- `alt` su tutte le immagini.
- Landmark semantici (`<header>`, `<main>`, `<footer>`, `<nav>`).
- Focus visibile su elementi interattivi.
- `prefers-reduced-motion` rispettato per eventuali animazioni.

---

## 8. SEO

- Meta tag base su ogni pagina (`title`, `description`).
- Open Graph + Twitter Card per condivisione social.
- `sitemap.xml` generato automaticamente (plugin Astro).
- `robots.txt`.
- URL puliti, niente trailing slash inconsistenze.

---

## 9. Struttura cartelle (proposta)

```
/
├── public/
│   ├── fonts/             # Bricolage Grotesque + IBM Plex Sans (woff2)
│   ├── images/
│   └── favicon.svg
├── src/
│   ├── components/
│   │   ├── Hero.astro
│   │   ├── Logos.astro
│   │   ├── ProjectCard.astro
│   │   ├── ProjectsGrid.astro
│   │   ├── Values.astro
│   │   ├── Header.astro
│   │   ├── Footer.astro
│   │   └── ThemeToggle.astro
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── pages/
│   │   ├── index.astro
│   │   └── about.astro
│   ├── styles/
│   │   ├── tokens.css     # CSS variables (colori, font scale, spacing)
│   │   ├── reset.css
│   │   └── global.css
│   └── content/
│       └── projects/      # MDX per ogni progetto (opzionale)
├── astro.config.mjs
├── package.json
└── REQUIREMENTS.md        # questo file
```

---

## 10. Deliverables

1. Repository Astro funzionante.
2. Build statica deployata su dominio personale.
3. Analytics (Plausible/Umami) attivo e raccolta dati.
4. Documentazione minima (`README.md`) con istruzioni build + deploy.

---

## 11. Out of scope (v1)

- CMS / area admin.
- Form di contatto con backend (eventualmente solo `mailto:` o servizio terzo come Formspree).
- Blog (rimandato a v2).
- Internazionalizzazione (i18n).
- Animazioni complesse / scroll-driven.
