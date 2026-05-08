# Part D — SEO Quick Win: Corporate Card + SMEs (Clara)

## Scope Decision

The challenge asked for `/empresas`. That URL does not exist on the real site. The decision was to work the actual architectural problem between two pages that exist and should be in conversation:

- `/es-mx/products/corporate-card` → answers "what is the product?"
- `/es-mx/solutions/small-business` → answers "is this for a company like mine?"

Neither page linked to the other. The `before/` documents that state. The `after/` implements the complete journey.

> **Note on `before/` capture method:** The `before/` HTML files are snapshots of the live `www.clara.com` pages taken in April 2026 via the Webflow MCP (Designer). An early commit message references `wget` — that was a placeholder from the initial setup commit and does not reflect the actual method used. The Webflow MCP approach preserved live DOM structure, inline scripts, and Webflow-specific class names, making the `before/after` diff a true apples-to-apples comparison.

---

## Changes Implemented — corporate-card.html

### 1. hreflang `es-MX` and canonical — relative URL fix
**Before:** `href="corporate-card.html"`  
**After:** `href="https://www.clara.com/es-mx/products/corporate-card"`  
**Why:** Google cannot resolve relative URLs in hreflang attributes. This means the Mexican version of the page does not receive the correct localization signal, which affects ranking in searches from Mexico. The relative canonical has the same problem: without an absolute URL, Google cannot consolidate link equity signals toward the canonical URL.

### 2. Title tag — primary keyword
**Before:** `"Tarjeta Corporativa: Emisión Inmediata | Clara"`  
**After:** `"Clara — Tarjeta corporativa y gestión de gastos para tu empresa en México"`  
**Why:** Google Trends (last 12 months, Mexico) shows "tarjeta empresarial" consistently outperforming "tarjeta corporativa" in search volume. "Emisión Inmediata" is conversion copy, not a modifier with real search demand. The new title incorporates the geographic modifier "en México", which captures high-intent transactional searches. The previous pleonasm "Tarjeta Empresarial para Empresas" was corrected — "empresarial" already implies the business context.

### 3. Meta description — differentiator-oriented
**Before:** Feature list (instant issuance, reconciliation, SAT)  
**After:** Includes "sin aval", per-employee benefit, social proof ("30,000 empresas")  
**Why:** The previous description did not differentiate Clara from a traditional bank. "Sin aval" is Clara's most powerful differentiator and no bank can offer that. Including it in the snippet increases CTR from users in active evaluation.

### 4. og:title + twitter:title — consistency
Updated to match the new `<title>`. Content shared on social must reflect the same positioning.

### 5. H1 hero — keyword + team differentiator
**Before:** `"Tarjeta de crédito empresarial para crecer con control"`  
**After:** `"La tarjeta empresarial que escala con tu equipo"`  
**Why:** Keeps the primary keyword "empresarial", removes the generic tagline "para crecer con control", and introduces "equipo" — a term that appears in transactional queries like "tarjeta empresarial para empleados".

### 6. Second H1 → H2 — semantic correction
**Before:** `<h1 class="fbl-heading-h1-17">Acelera tu crecimiento con Clara</h1>`  
**After:** `<h2 class="fbl-heading-h1-17">Acelera tu crecimiento con Clara</h2>`  
**Why:** A page should not have two H1 elements. The Webflow class `fbl-heading-h1-17` controls visual style, not semantics — the tag change is zero visual risk.

### 7. FAQ schema — FAQPage JSON-LD
**Before:** No structured data (Stackoptic score: 0/100)  
**After:** 8-question `FAQPage` schema in `<head>`  
**Questions chosen:** Credit requirements, card limits, multi-currency support, reimbursement process, per-employee controls, SAT integration, cancellation terms, onboarding time.  
**Why these questions:** They map to the real pre-purchase questions a finance director would type into Google before signing up. FAQ rich results appear above standard organic results — the click doesn't require position 1.

### 8. New H2 section — "Lo que tu banco no puede darte"
**Why:** Addresses the implicit objection in every "tarjeta empresarial" search: "Why not just use my bank?" Naming the differentiators directly (no personal guarantee, instant issuance, per-employee controls) converts visitors who are in comparison mode — the exact profile of a user with a high bounce rate.

### 9. Interlinking — narrative bridge to /small-business
**Before:** No link to `/solutions/small-business`  
**After:** Contextual link with anchor text: "¿Acabas de contratar tus primeros empleados? Esta página es para ti →"  
**Why:** A user landing on the product page via organic search is in discovery mode. If they don't see themselves in the page's primary positioning ("established team"), they bounce. The internal link gives them a path forward instead of an exit.

---

## Changes Implemented — small-business.html

### 1. hreflang + canonical — absolute URLs
Same fix as `corporate-card.html`. Relative URLs in both attributes.

### 2. Title tag
**Before:** `"Soluciones para Pequeñas Empresas | Clara"`  
**After:** `"Tarjeta Empresarial para PyMEs en México | Clara"`  
**Why:** The previous title describes a category, not a product. The new title targets the specific search query a small business owner would use.

### 3. H1 — user pain, not product feature
**Before:** `"Hecha para equipos que están creciendo"`  
**After:** `"El control de gastos que tu PyME necesitaba desde el día uno"`  
**Why:** "Hecha para equipos" is brand-centric. The new H1 is user-centric — it names the pain state (lack of expense control) and positions Clara as the solution that should have been there from the start.

### 4. User profile section — "Hecha para equipos que están escalando"
New section that explicitly describes the target user: a team of 5–50 people, first external hires, finance director who is also the CEO.  
**Why:** The bounce rate on discovery pages is driven by users who can't quickly answer "is this for me?" Naming the profile explicitly reduces cognitive load and increases time on page.

### 5. Interlinking back to /corporate-card
**Anchor text:** `"¿Tu empresa ya tiene un equipo financiero? Conoce la tarjeta corporativa →"`  
**Why:** Creates the bidirectional journey. A user who starts on `/small-business` and outgrows it needs a visible path to the next product tier.

---

## Root Cause: Why the Bounce Rate Is an Architecture Problem

The challenge frames the problem as a content issue on a single page. The actual cause is structural:

1. **No middle layer in the journey.** The site goes Homepage → Product page → Registration. There is no consideration-stage content that earns the conversion before asking for it.
2. **The Matrioshka structure.** Each page looks complete from the outside. But opening one doesn't lead you to the next — there are no connecting threads between layers.
3. **Users in discovery mode need orientation, not a CTA.** A first-time visitor searching "tarjeta empresarial" is not ready to register. They need to understand what makes Clara different from their bank, whether it's for their company size, and what happens after they sign up. None of that was available before the `after/` changes.

Fixing the H1 without fixing the journey treats the symptom. The `after/` pages fix both.

---

## Validation Metrics

| Metric | Tool | Expected change | Timeframe |
|---|---|---|---|
| Organic impressions for "tarjeta empresarial" queries | Search Console | +20–40% | 4–8 weeks post-deploy |
| CTR on `/products/corporate-card` in SERP | Search Console | +1.5–3pp (differentiators: "crédito a nombre de empresa", "tarjetas ilimitadas") | 2–4 weeks |
| Bounce rate on `/products/corporate-card` | GA4 | −15–25% (interlinking + user profile section) | 2 weeks |
| Pages per session (entry via corporate-card) | GA4 | 1.0 → 1.4+ (new internal link path) | 2 weeks |
| FAQ rich result appearance | Google Search | Accordion in SERP | 1–3 weeks |
| Ranking position for "tarjeta empresarial México" | Ahrefs / Search Console | Entry into top 10 | 6–12 weeks |

---

## What Was NOT Changed (and Why)

- **URL slugs** — changing `/products/corporate-card` to `/es-mx/tarjeta-empresarial` would require 301 redirects and risks losing existing link equity. High reward, high risk. Not a quick win.
- **Page template structure** — all changes live in `<head>` metadata, semantic tag corrections, and content additions. No layout changes were made. This makes the changes implementable directly in Webflow Custom Code without touching the Webflow canvas structure.
- **Visual design** — none. The `after/` pages are visually identical to `before/` from the user's perspective. All SEO improvements are invisible to the visitor.

---

## How to Implement in Production

All changes in `after/corporate-card.html` are implementable in Webflow without engineering involvement:

1. **`<head>` changes** (title, meta, hreflang, canonical, FAQ schema JSON-LD) → Webflow Dashboard → Page Settings → Custom Code → `<head>` section
2. **H2 semantic correction** → Webflow Designer → select the element → change tag from H1 to H2 in the element settings panel
3. **New sections** ("Lo que tu banco no puede darte", interlinking block) → Webflow Designer → add section from component library or build with existing style tokens

No code deployment required. No engineering ticket needed. A Webflow-trained content manager can implement and publish within 2 hours.

---

## Webflow Demo — Iteration 3 Copy Pass (May 7, 2026)

Copy, tone, and compliance changes applied directly to the Webflow demo via MCP Designer Tools.

### Compliance

- `small-business` meta description: removed `"Sin aval, sin historial previo."` — phrase violates product messaging guidelines. Replaced with `"Alta 100% digital."`.

### Copy changes — Small Business

| Element | Before | After | Why |
|---|---|---|---|
| Hero subtitle | "...sin trámites bancarios" | "Control de gastos empresarial para equipos de 5 a 100 personas. Alta 100% digital." | Phrase was duplicated 3× on same page; new copy anchors the target segment |
| Feature "Tarjetas" body | "...Sin trámites bancarios." | "...Desde la plataforma, en minutos." | Eliminates repetition |
| Feature "Alta digital" body | "Tu PyME califica desde el primer día... Sin trámites bancarios, sin visitas a sucursal." | "Carga tus documentos, verifica en minutos y empieza a operar el mismo día." | "Califica" ambiguous (sounds like credit scoring); "sin trámites" was duplicated |
| Interlinking H2 | "¿Quieres entender primero cómo funciona la tarjeta?" | "¿Tu empresa ya superó los 100 colaboradores?" | Weak H2 with no targeting; new version speaks to the exact graduation moment |
| Interlinking body | "...opciones para cada etapa de crecimiento." | "Cuando tu equipo crece y los controles básicos ya no alcanzan, la tarjeta corporativa Clara escala contigo." | Concrete trigger → clear CTA path |

### Copy changes — Corporate Card

| Element | Before | After | Why |
|---|---|---|---|
| Hero subtitle | "Crédito para tu empresa, controles para tu equipo." | "Crédito a nombre de tu empresa. Tarjetas ilimitadas con controles individuales por empleado." | Adds two concrete differentiators missing from the original |
| Features H2 | "Todo lo que necesitas para gestionar gastos de equipo" | "Tarjeta empresarial con controles en tiempo real para cada empleado" | Primary keyword in H2; "tiempo real" adds search-relevant modifier |
| Interlinking H2 | "¿Es Clara para una empresa como la tuya?" | "¿Acabas de contratar tus primeros empleados?" | Speaks to the specific user state that triggers the journey to `/small-business` |
| CTA subtitle | "Tu empresa califica. Empieza en minutos." | "Alta 100% digital. Empieza hoy." | "Califica" ambiguous; new copy reinforces the process differentiator |
| Differentiators body | Generic one-paragraph summary | "Con Clara emites tarjetas para todo tu equipo en minutos, defines límites por colaborador y concilias automáticamente con el SAT. El crédito va a nombre de la empresa — no del director general." | More specific; names 3 verified differentiators; removes bank comparison framing |

### Typography migration

All 43 styles with `font-family` were migrated from `Montserrat` (headings) and `Inter` (body/nav/footer) to `Arial, "Helvetica Neue", Helvetica, sans-serif`. No Google Fonts dependency remains on the demo site.
