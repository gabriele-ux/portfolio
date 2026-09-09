# Portfolio Site — Requirements v2

**Versione:** 2.0 (draft, in costruzione)
**Data inizio:** 2026-08-21
**Stato:** Reset in corso — struttura e design system vengono ricostruiti da zero
**Versione precedente:** vedi `REQUIREMENTS-v1.md`

---

## 1. Obiettivo del refactor

Ricostruire il portfolio partendo da nuovi componenti riusabili e nuovi token di design forniti dall'utente. Lo stack tecnologico resta invariato (Astro + CSS vanilla con custom properties); cambia tutto il livello UI.

**Principi guida:**
- **Componenti riusabili prima di tutto** — ogni pezzo di UI viene definito una volta e riutilizzato attraverso le pagine.
- **Token-driven** — colori, tipografia, spacing, radius, ombre vivono in un unico posto (`src/styles/tokens.css`) e le pagine/componenti li consumano via CSS custom properties.
- **Zero speculation** — nessun componente o token viene aggiunto senza un riferimento concreto (Figma frame, screenshot, codice).

---

## 2. Stack tecnologico

- **Framework:** Astro (invariato dalla v1)
- **Styling:** CSS vanilla con custom properties (invariato). Da valutare a valle se introdurre Tailwind o altro.
- **Hosting:** deploy statico self-hosted (invariato)
- **Analytics:** da riconfermare in v2 (Plausible/Umami restano candidati)

---

## 3. Struttura del sito

Route esistenti mantenute come contenitori vuoti in attesa dei nuovi contenuti:

```
/                       → Homepage
/about                  → Pagina About
/case-study/[slug]      → Pagina dettaglio case study (route dinamica)
```

Sitemap e sezioni verranno ridefinite man mano che i nuovi componenti vengono introdotti.

---

## 4. Design system

### 4.1 Token

_Da definire. I token vivono in `src/styles/tokens.css`._

Categorie previste:
- Colori
- Tipografia (font families, scale, line-height, letter-spacing)
- Spacing
- Radius
- Ombre
- Breakpoint

### 4.2 Tipografia

_Da definire (font family, pesi, self-hosting via `@fontsource/*` o altro)._

### 4.3 Breakpoint

_Da definire._

---

## 5. Componenti riusabili

_Elenco vuoto. Ogni componente verrà aggiunto qui quando l'utente fornisce riferimenti concreti._

Convenzioni:
- Directory: `src/components/` (senza sotto-cartelle per pagina finché non serve).
- File `.astro` con Props tipizzate via `interface Props`.
- Consumo di token via `var(--...)` — mai hex/px hardcoded se esiste un token.

---

## 6. Struttura cartelle attuale

```
src/
├── components/          # vuota — riempita man mano
├── layouts/
│   └── BaseLayout.astro # shell minimale
├── pages/
│   ├── index.astro
│   ├── about.astro
│   └── case-study/
│       └── [slug].astro
└── styles/
    ├── tokens.css       # vuoto — token aggiunti man mano
    └── global.css       # reset minimale
```

---

## 7. Requisiti funzionali e non funzionali

_Ripresi dalla v1 quando pertinenti (performance, accessibilità, SEO, privacy). Ridiscussi caso per caso durante la ricostruzione._

---

## 8. Out of scope (v2 draft)

Stessi della v1 salvo diversa indicazione:
- CMS / admin
- Form di contatto con backend
- Blog
- i18n
- Animazioni scroll-driven complesse
