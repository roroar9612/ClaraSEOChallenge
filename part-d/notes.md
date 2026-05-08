# Part D — Webflow Quick Win (SEO)

## Scope and Assumption

The prompt references `/empresas`. In production, the equivalent route is `/es-mx/solutions/small-business`.

Because the challenge prioritizes `/empresas`, the implementation and review order used in this submission is:

1. `/empresas` (demo page for the SMB/fit stage)
2. `/corporate-card` (product-detail stage)

To keep the intervention grounded in real pages and measurable behavior, the technical work focused on:

- `/es-mx/products/corporate-card` (product intent)
- `/es-mx/solutions/small-business` (fit-by-company-size intent)

The `before/` and `after/` files document that change set. Interlinking between both pages is deliberate and designed to support the user journey from fit assessment to product depth (and back).

---

## SEO Hypothesis

Bounce rate and weak ranking were not caused by a single headline or metadata issue. The root problem was architectural:

1. Missing semantic and localization signals (`hreflang`, `canonical`, heading hierarchy, schema)
2. Weak search-intent alignment in titles and hero messaging
3. No narrative interlinking between product-level and solution-level pages

Hypothesis: a focused update across those three dimensions would improve search relevance, CTR, and post-landing navigation depth without requiring a full redesign.

---

## Implemented Changes

### A) `after/corporate-card.html`

1. **Absolute `hreflang` + canonical**
   - Fixed relative URLs to absolute URLs for `/es-mx/products/corporate-card`
   ```html
   <link rel="alternate" hrefLang="es-MX" href="https://www.clara.com/es-mx/products/corporate-card"/>
   <link href="https://www.clara.com/es-mx/products/corporate-card" rel="canonical"/>
   ```
2. **Title and meta description rewrite**
   - Shifted from generic/marketing phrasing to query-aligned, market-specific wording
   ```html
   <title>Clara — Tarjeta corporativa y gestión de gastos para tu empresa en México</title>
   <meta content="Tarjeta empresarial para equipos en México. Crédito ilimitado, controles por empleado y conciliación automática con SAT e integración ERP. Más de 30,000 empresas confían en Clara." name="description"/>
   ```
3. **Social metadata alignment**
   - Updated `og:title` and `twitter:title` to match the final title strategy
   ```html
   <meta content="Clara — Tarjeta corporativa y gestión de gastos para tu empresa en México" property="og:title"/>
   <meta content="Clara — Tarjeta corporativa y gestión de gastos para tu empresa en México" property="twitter:title"/>
   ```
4. **H1 optimization**
   - Hero H1 rewritten to keep primary keyword and improve role/team fit
   ```html
   <h1 class="fbl-hero-19-title"><strong>La tarjeta empresarial que escala con tu equipo</strong></h1>
   ```
5. **Heading semantics**
   - Second `<h1>` converted to `<h2>` to restore a clean hierarchy
   ```html
   <h2 class="fbl-heading-h1-17">Acelera tu crecimiento con Clara</h2>
   ```
6. **FAQ structured data**
   - Added `FAQPage` JSON-LD in `<head>` with pre-purchase intent questions
   ```html
   <script type="application/ld+json">
   {
     "@context": "https://schema.org",
     "@type": "FAQPage",
     "mainEntity": [
       {
         "@type": "Question",
         "name": "¿Cuánto tiempo tarda el proceso de alta en Clara?",
         "acceptedAnswer": {
           "@type": "Answer",
           "text": "El proceso de alta es 100% digital..."
         }
       }
     ]
   }
   </script>
   ```
7. **Differentiator section**
   - Added copy block focused on “why Clara vs traditional bank flow”
   ```html
   <div class="fbl-section-banco-vs-clara">
     <h2 class="fbl-heading-h3-6">Lo que tu banco no puede darte</h2>
     <p class="fbl-lead-text-26">A diferencia de una tarjeta bancaria tradicional, puedes emitir tarjetas ilimitadas para tu equipo en minutos...</p>
   </div>
   ```
8. **Interlinking to solution page**
   - Added direct internal path from this page to the small-business solution URL
   ```html
   <a href="https://www.clara.com/es-mx/solutions/small-business" class="uui-navbar02_dropdown-link-2 w-inline-block">...</a>
   ```

### B) `after/small-business.html`

1. **Absolute `hreflang` + canonical**
2. **Title update**
   - Reframed to a clearer transactional query pattern for SMB audience
3. **H1 rewrite**
   - Shifted from brand-centric wording to problem-state wording
4. **User profile clarity**
   - Added profile-oriented framing to reduce “is this for me?” friction
5. **Interlinking back to product page**
   - Added reciprocal navigation path to `corporate-card`

---

## Why This Qualifies as a Quick Win

- No full template rebuild required
- No backend or engineering dependency
- High-impact SEO fundamentals addressed in one pass
- Changes can be implemented via Webflow page settings + targeted content updates

---

## Validation Plan

| Metric | Tool | Expected Direction | Observation Window |
|---|---|---|---|
| Organic impressions for “tarjeta empresarial” queries | Search Console | Up | 4–8 weeks |
| CTR on corporate-card entry queries | Search Console | Up | 2–4 weeks |
| Bounce rate on product entry page | GA4 | Down | 2–4 weeks |
| Pages/session from organic product landings | GA4 | Up | 2–4 weeks |
| FAQ rich result eligibility/appearance | Rich Results Test + Search Console | Up | 1–3 weeks |

---

## Constraints and What Was Intentionally Not Changed

- **Slug migration** (`/products/corporate-card` -> localized slug) was deferred due to redirect/link-equity risk for a quick-win scope.
- **Visual redesign** was out of scope; this intervention prioritizes SEO performance signals over layout overhaul.
- **Large CMS template refactors** were deferred to preserve delivery speed.

---

## Deliverable Mapping

- **Before snapshots (archival):** `part-d/before/*`
- **After reference (primary):** `https://clara-seo-challenge.webflow.io/empresas` and `https://clara-seo-challenge.webflow.io/corporate-card`
- **Local HTML artifacts (secondary):** `part-d/after/*.html` (archival snapshots from early capture/diff workflow; not the primary review source)
- **Hypothesis and rationale:** this document
- **Validation metrics:** table above
