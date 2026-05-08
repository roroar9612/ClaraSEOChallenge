# Part A — SEO Audit: clara.com

**Scope:** Technical SEO issues, on-page review of the homepage, and content opportunities for MX and BR.  
**Tools used:** SEMrush (traffic data, organic overview), Browser DevTools (manual verification of `lang`, `hreflang`, and page source), Stackoptic (structured technical audit), Google Trends (12-month export by country), and sitemap analysis.  
**Date:** April 2026

---

## Context Note

This audit was developed on top of an earlier preparation report in Spanish: `part-a/context/initial-audit-baseline-es.pdf`. That baseline was used to frame initial hypotheses and was then refined and expanded for this challenge submission.

---

## Assumption Log

**Assumption 1 — `/empresas` is a challenge label, not the production URL.** In production, the equivalent route is `/es-mx/solutions/small-business`. In the challenge demo, that page was later renamed to `/empresas`. Part D works on the two real page types behind the challenge prompt: `/es-mx/products/corporate-card` and `/es-mx/solutions/small-business`.

**Assumption 2 — Vocabulary strategy requires coexistence, not substitution.** Clara uses "tarjeta corporativa" as the official product name. Google Trends shows that "tarjeta empresarial" consistently outperforms "tarjeta corporativa" in search volume in MX and CO — in Colombia, "corporativa" has close to zero search volume. The right approach is not to abandon "corporativa" but to work with both terms in distinct layers: "empresarial" as the anchor in the highest-weight SEO elements (title, H1, meta description), and "corporativa" as a secondary semantic signal in subheadings and body text. Brazil is the exception — "cartão corporativo" leads and the site already uses it correctly.

This strategy resolves the tension between what the brand calls the product and what users actually search for, without creating brand inconsistency.

**Assumption 3 — English URL slugs affect localization signals.** Pages like `/es-mx/products/corporate-card` and `/es-mx/cards/black-card` within Spanish-language paths generate an inconsistent localization signal. The slug impact alone is modest, but the inconsistency amplifies the hreflang and duplicate content issues that already exist. Any slug migration must include 301 redirects and pre/post validation in Google Search Console.

---

## Audit Methodology Note

The audit followed a deliberate sequence: symptom first, then manual verification, then structured analysis.

**SEMrush first** — to establish whether an organic traffic problem actually exists before diagnosing causes. The 11% traffic drop (235,528 visits, April 2026) confirmed the analysis had a real business context, not a hypothetical one.

**DevTools second** — manual inspection of `lang` attributes, `hreflang` tags, canonical URLs, and page source across `/es-mx`, `/es-co`, `/pt-br`, and the global `clara.com`. This step is specifically what prevented a false positive: Stackoptic flagged `lang` inconsistency broadly, but DevTools confirmed that the localized pages are correctly implemented — `clara.com/es-mx` returns `lang="es-MX"`, `clara.com/es-co` returns `lang="es-CO"`. The value `es-MX` is more precise than a generic `es` and is the correct implementation for regional signaling. The `lang="en-US"` issue is scoped to the global domain `clara.com` and unlocalized internal pages — not a site-wide failure. Tools surface signals; judgment determines scope.

**Stackoptic third** — structured scoring across technical dimensions: hreflang, structured data, performance, readability, martech maturity. Used to prioritize and quantify, not to discover.

---

## 1. Top 3 Critical Technical SEO Issues

### Issue 1 — Incomplete hreflang on internal pages

Clara operates in three markets (MX, CO, BR) with content in Spanish and Portuguese. Stackoptic confirms that the global homepage (`clara.com`) has hreflang correctly implemented — with language-country pairs and `x-default` pointing to the global version (score 10/10). The problem is on internal pages: `hreflang` and `canonical` attributes use relative URLs instead of absolute ones, which prevents Google from resolving which version belongs to each page and serving the correct one per market.

**Why it is high priority:** This is not an isolated bug — it is the root cause that amplifies all other localization issues. A CFO in Colombia searching "tarjeta empresarial" may receive the Mexican version, or the global English homepage, depending on what Google resolves. The 11% organic traffic drop observed in SEMrush (235,528 visits, April 2026) has a structural explanation here: the site cannibalizes its own versions.

**Expected impact when fixed:** Hreflang with absolute URLs allows Google to index and serve the correct version to each market. It stops cannibalization between `/es-mx/`, `/es-co/`, and `/pt-br/` and recovers organic impressions lost to version confusion.

**Implementation note:** One hreflang tag per page per language-country pair, with `x-default` pointing to the global version. Must be consistent in both the HTML `<head>` and the sitemap. In Webflow, this is managed via Custom Code > Head in Page Settings.

---

### Issue 2 — Structured data absent (score 0/100)

Stackoptic detected a complete absence of structured data on product pages. No `Organization`, `FAQPage`, `BreadcrumbList`, or `LocalBusiness` schema is present. The score for this dimension is 0/100.

**Why it matters:** Structured data is how the site communicates to Google — and to AI search engines — what type of entity each page is, what questions it answers, and how it relates to the rest of the site. Without it, Google cannot display rich results (FAQ accordions in SERP, visual breadcrumbs, company data). For GEO, the absence of structured schema reduces the probability that AI models will cite site content correctly — models prioritize structured, attributable content.

`FAQPage` schema on the corporate card page is the highest-return immediate intervention: it enables rich results in the SERP for the questions prospects are already asking.

**Expected impact when fixed:** Rich results in the SERP for product pages, stronger entity signal for the Google Knowledge Graph, and more citable content for AI search engines. FAQ schema is implemented as JSON-LD in the `<head>` — no visible HTML changes required, no design changes.

---

### Issue 3 — Inconsistent localization signals

This issue has multiple expressions that point to the same underlying problem: the site grew fast across markets without a centralized localization process.

**Note on `html lang`:** The localized versions of the site have the `lang` attribute correctly implemented — verified manually with DevTools: `clara.com/es-mx` → `lang="es-MX"`, `clara.com/es-co` → `lang="es-CO"`. The value `es-MX` is more precise than a generic `es` and is the correct implementation for regional signaling. The `lang="en-US"` finding applies specifically to the global domain `clara.com` and pages without a localization prefix — not to the per-market versions.

The concrete manifestations identified in the audit include:

- `clara.com` (global domain) has `lang="en-US"` even though it serves as the entry point for Spanish and Portuguese-speaking users, and its navigation paths lead to Spanish and Portuguese versions.
- 404 error pages appear in English within `/es-mx/` paths, exposing CMS text: "0 results found for this URL".
- Product names in English within Portuguese-language pages on `/pt-br/`.
- The country selector on the global homepage mixes countries with languages (中文 listed alongside country names), with most selections redirecting to a Spanish version designed for a different market.
- No IP-based detection to suggest the correct market version to a new visitor.

**Why it matters:** Each inconsistency sends a contradictory signal about the language and market each page serves. This reinforces the hreflang problem and creates additional confusion about which version should rank for which query. 404 pages in English within Spanish-language paths also fail WCAG 3.1.1.

**Expected impact when fixed:** Correcting `lang` on the global domain, adding localized error pages, fixing the country selector, and implementing IP-based version suggestions would reduce friction at every stage of the journey and strengthen the localization signal per market.

---

## 2. On-Page SEO Review — Homepage

Two versions reviewed: `clara.com` (global) and `clara.com/es-mx` (Mexico).

### Global homepage — `clara.com`

| Element | Current state | Evaluation |
|---|---|---|
| Title tag | `Clara \| Spend Management for LatAm` | In English. "LatAm" is an industry abbreviation, not a search term used by Spanish or Portuguese-speaking users. |
| Meta description | `The financial operating system for Latin America. Corporate cards, expense automation, AP, and banking — built for companies in MX, BR, and CO.` | In English. Feature list format. Mentions MX, BR, CO (positive geographic signal), but not written to answer any real organic search query. |
| H1 | `The partner to Latin America's leading finance teams` | In English. Positioning statement, not a search-oriented phrase. "Leading finance teams" signals enterprise aspiration but does not correspond to any real query. |

**The problem is not that the global homepage is in English.** It is a defensible brand decision — the global homepage serves investors, partners, and press, audiences for whom English functions as a shared language in fintech. The problem is structural: `clara.com` is the highest-authority URL on the domain, and it is completely disconnected from any organic search intent in the markets that generate real traffic. Its internal linking does not efficiently distribute authority toward the Spanish and Portuguese pages that compete for real queries.

### Mexico homepage — `clara.com/es-mx`

| Element | Current state | Evaluation |
|---|---|---|
| Title tag | `Clara \| Gestión Financiera Inteligente para LatAm` | In Spanish. "Gestión Financiera Inteligente" is a brand tagline, not a search query. No keyword target present. |
| Meta description | `Tarjetas corporativas, gestión de gastos y banking en una sola plataforma. Clara ayuda a empresas en Latinoamérica a controlar gastos y escalar con confianza.` | In Spanish. More descriptive than the global version. Still not written around a specific search intent. |
| H1 | `Gestión de gastos para equipos financieros exigentes` | In Spanish. Accurately describes the platform but functions as a tagline. "Equipos financieros exigentes" is not a phrase any user types into Google. |

**What to change and why:**

The title tag and H1 must incorporate the primary search term for the market, preserve the brand name, and maintain Clara's characteristic second-person tone. Proposed title: `Clara — Tarjeta corporativa y gestión de gastos para tu empresa en México`. This keeps the brand, uses "tarjeta corporativa" as the official product name with a geographic signal, without repeating the noun in the modifying adjective.

The H1 must reflect search intent without sounding generic. A direction that respects Clara's tone: `El control de gastos que tu empresa necesitaba desde el primer día`. Second-person address (tuteo, consistent with the style guide), anchors the page in the real product category, and communicates the value differentiator without empty superlatives.

The meta description must function as a conversion asset in the SERP: `Emite tarjetas para tu equipo, automatiza reembolsos y cierra el mes sin caos. Sin aval, sin historial crediticio. Más de 30,000 empresas ya lo hacen con Clara.`

The **internal linking** on the Mexico homepage is oriented primarily toward registration. There are no prominent links to product pages (`/es-mx/products/corporate-card`) or solution pages, which limits authority distribution and shortens the discovery journey for users who are not yet ready to sign up.

---

## 3. Additional Stackoptic Findings

**Flesch Reading Ease: 18/100.** The site copy has an extremely high complexity level — equivalent to an academic paper. For a platform targeting finance directors at SMEs and startups, this creates unnecessary friction. Clara's style guide points in the opposite direction: concrete benefits over features, second-person address, no superlatives. "Tu equipo gasta, tú apruebas, el sistema reconcilia" — not "la solución optimiza los flujos de gestión del gasto empresarial". The Flesch score is also an indirect SEO signal: time on page and scroll depth drop when copy is hard to read.

**Font sizes in pure `vw`.** Font size units defined exclusively in `vw` without `clamp()` or `rem` fallback break browser zoom. Fails WCAG 1.4.4 (Resize Text). The fix is technical and does not affect visual design.

**Marketing tech stack maturity: 32/100.** Stackoptic only detected Google Analytics and GTM active on the site. No heatmap, A/B testing, or CRO tools present. For a growth team making decisions about site changes, the absence of user behavior data limits the ability to validate hypotheses — including those raised in this challenge.

---

## 4. Two Content Opportunities in MX and BR

### Opportunity 1 — Capturing demand for "tarjeta empresarial" in MX and CO

Google Trends over the last 12 months shows a consistent and significant gap between search volume for "tarjeta empresarial" and "tarjeta corporativa" in Mexico and Colombia. "Tarjeta empresarial" outperforms "tarjeta corporativa" in every month of the period. In Colombia, "tarjeta corporativa" registers near-zero volume. Brazil is the exception — "cartão corporativo" leads and the site already uses it correctly.

The URL `/es-mx/landing/tarjeta-de-credito-empresarial` already exists and signals the opportunity was partially identified, but it exists as an isolated landing page without a coherent content architecture behind it.

High-intent terms currently unaddressed: "tarjeta empresarial sin aval", "tarjeta corporativa sin historial crediticio", "tarjeta de gastos para empleados México". These describe Clara's specific differentiators against traditional banks and have low organic competition.

### Opportunity 2 — Mid-funnel content around expense management processes

A prospective buyer who has the problem Clara solves but does not yet know Clara exists will not search for "Clara tarjeta empresarial." They search for process-level queries instead: "cómo reembolsar gastos a empleados en México", "proceso de reembolso de viáticos empresas", and "cómo controlar gastos de equipo en campo". None of these queries is answered by any page on the site today.

The product release blog contains precise descriptions of exactly the features that answer these questions — but written as internal product announcements, not as responses to user searches. The opportunity is to build a mid-funnel content layer between the blog and the product pages, written around specific operational problems using the vocabulary of search.

Brazil is an additional focus. The `/pt-br/` site has the correct vocabulary ("cartão corporativo") but the same absence of mid-funnel content. Searches like "como reembolsar despesas de funcionários" or "controle de gastos empresariais Brasil" represent real demand that no page currently captures.
