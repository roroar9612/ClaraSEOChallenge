# Execution Roadmap — Clara SEO Challenge

---

## Current Status (May 7, 2026)

| Part | Document | Status |
|---|---|---|
| A | `part-a/audit.md` | ✅ Complete |
| B | `part-b/keyword-strategy.md` | ✅ Complete |
| C | `part-c/geo-ai-search.md` | ✅ Complete |
| D | `part-d/before/` + `part-d/after/` + `part-d/notes.md` | ✅ Complete |
| — | `README.md` | ✅ Complete |
| — | Webflow demo | ✅ Published at `clara-seo-challenge.webflow.io` |

---

## Webflow Demo — Published State

**Site URL:** `clara-seo-challenge.webflow.io`  
**Site ID:** `69f57ff4021a4f2250a9fbd4`

### Pages

| Page | Slug | Webflow Page ID |
|---|---|---|
| Corporate Card | `/corporate-card` | `69f592e365ffb17eb53e7488` |
| Small Business | `/small-business` | `69fc967c3d0867342deac6eb` |

### Reusable Components

| Component | Webflow Component ID |
|---|---|
| Navbar Clara | `1458fdd9-2ea2-f3f7-2342-cd55a0df2fc4` |
| Footer Clara | `594c8515-0263-6f17-987b-6375305f4759` |

### Sections built (corporate-card)

1. ✅ Hero — H1, CTA "Regístrate gratis", lead copy
2. ✅ Logos strip — 11 enterprise clients (Telefónica, Schneider, MAPFRE, Krispy Kreme, MINISO, SmartFit, GNC, Rappi, Pan American, Viva, OCESA)
3. ✅ Features grid — 4 features (Control por empleado, Conciliación SAT, Crédito a nombre de empresa, Integraciones ERP)
4. ✅ "Lo que tu banco no puede darte" — differentiators section
5. ✅ FAQ accordion — 8 questions
6. ✅ Interlinking CTA → `/small-business`
7. ✅ CTA final (registro form placeholder)
8. ✅ Navbar Clara component
9. ✅ Footer Clara component (with logos, awards, app store badges via CSS background-image)

### Sections built (small-business)

1. ✅ Hero — H1, CTA, lead copy (no compliance issues)
2. ✅ Logos strip — same 11 enterprise clients
3. ✅ Perfil de usuario — "Hecha para equipos que están escalando"
4. ✅ Features PyME — adapted for SME context
5. ✅ Interlinking CTA → `/corporate-card`
6. ✅ CTA final
7. ✅ Navbar Clara component
8. ✅ Footer Clara component

### Custom Code injected (Page Settings > Head)

Both pages have canonical, hreflang, and meta description via Webflow Page Settings.  
Corporate-card also has `FAQPage` JSON-LD schema injected via custom script.

---

## Iteration 3 — Pending

### High priority (before live session)

- [ ] **Hero image** — corporate-card hero background image not wired. Asset uploaded to project CDN (`69fcec93c6b5fa35b5651982`). Apply via CSS `background-image` on hero section div.
- [ ] **Compliance pass** — verify no "sin aval" or "sin historial crediticio" remaining in FAQ accordion text or differentiadores section on corporate-card.
- [ ] **og:image** — add Open Graph image for both pages via Page Settings (Webflow: SEO tab → OG image).
- [ ] **hreflang as HTML** — currently injected via JS. Move to Page Settings > Custom Code > Head as static `<link rel="alternate" hreflang="es-MX" ...>`.

### Medium priority

- [ ] **Navbar dropdowns** — real Clara navbar has dropdowns for Productos, Soluciones, Recursos. Current version has placeholder links only.
- [ ] **Registro form** — CTA final has a form placeholder. Wire up a real form (Webflow native form or HubSpot embed).
- [ ] **Responsive review** — check navbar and footer at tablet and mobile breakpoints in Webflow Designer.

### Low priority

- [ ] **parts B and C** — confirm `part-b/keyword-strategy.md` and `part-c/geo-ai-search.md` are in repo with correct content.

---

## Critical Context for Next Session

### Ghost element pattern
`remove_element` in Webflow MCP sometimes reports success but elements persist across sessions. At session start, always query the page's body direct children to distinguish true standalone elements from component-internal elements before attempting any delete.

### imgraw limitation
`whtml_builder` converts `<img>` tags to `imgraw` DOM elements. The `src` attribute is **not stored** in Webflow's data model — images will be blank in the Designer and in published output. Fix: use CSS `background-image` on div containers. All current images on both pages use this pattern.

### CSS background-image pattern (project CDN)
```
https://cdn.prod.website-files.com/69f57ff4021a4f2250a9fbd4/{asset_id}_{original_filename}
```
Asset IDs for key images can be found in the `asset_tool` or from uploaded asset metadata.

### Compliance rule (HARD)
Never use "sin aval", "sin historial crediticio", "sin garantías patrimoniales" or any variant. This is a compliance risk, not a style preference. Use verified differentiators: control de gastos por empleado, conciliación automática SAT, tarjetas ilimitadas, integración ERP, proceso 100% digital.

---

## For the Live Session

**"Why did you work on two pages instead of one?"**  
→ Because the real problem is not the content of a single page — it's that the pages aren't in conversation. The challenge mentions `/empresas` but that URL doesn't exist on the site. I chose to work the real architectural problem instead of simulating a hypothetical URL.

**"How would you validate that these changes worked?"**  
→ Search Console for impressions and CTR on queries containing "tarjeta empresarial". Google Analytics for bounce rate and pages per session for users who entered via `/products/corporate-card`. Compare 30 days before vs 30 days after.

**"Why did you replace 'corporativa' with 'empresarial'?"**  
→ Google Trends 12-month CSV exports show "tarjeta empresarial" consistently outperforming "tarjeta corporativa" in Mexico and Colombia. The strategy is not to remove "corporativa" — it's coexistence: "empresarial" anchors the highest-weight SEO elements (title, H1, meta description), "corporativa" stays in body copy as a secondary semantic signal and brand name.

**"Show me the FAQ schema you implemented."**  
→ Open `after/corporate-card.html`, find `application/ld+json`, explain each question and why those were chosen. Or open the Webflow demo and view source.

**"What would you do differently with more time?"**  
→ Build the platform / "how it works" page that describes the complete expense lifecycle. That's the piece the site is most missing and the one with the highest GEO impact. I'd also write a `llms.txt` in Spanish and Portuguese with the accuracy corrections identified in the GEO baseline (Mastercard vs Visa in Perplexity's response about Clara).
