# Part B — Keyword Strategy & Content Architecture

**Target searches:**
- "tarjeta corporativa para empresas México"
- "gestão de despesas empresariais"
- "gastos corporativos Colombia"

**Date:** April 2026

---

## Framing: Narrative-First Architecture

Before mapping keywords or pages, a framing decision that shapes everything that follows.

SEO is not the strategy — it is the result of a content strategy well executed. If the site's narrative reflects how a real user discovers, evaluates, and decides to use Clara, then pages naturally answer the right questions, use the right vocabulary, and interlink in ways that make sense for both the user and the crawler. Keyword targeting is not something applied on top of content — it emerges from understanding what question a user is asking at each moment of their journey.

Clara's core narrative is underutilized. The product is genuinely differentiated: it covers the complete lifecycle of corporate spend, from the moment an employee makes a purchase to the moment a CFO sees it reconciled, categorized, and tax-deductible — all within one platform. That narrative does not appear anywhere in the current landing pages. It lives in product release posts written for existing users, disconnected from the discovery journey of a prospective buyer.

The architecture proposed here is built around that narrative, structured by user journey stage.

---

## The User Journey: Four Moments of Search

A prospective buyer searching for a solution like Clara moves through four distinct moments, each with a different question and a different search behavior.

**Moment 1 — Problem awareness.** The user has an operational problem but does not know Clara exists. They search for process-level answers: "cómo controlar gastos de empleados en campo", "como reembolsar despesas de funcionários Brasil", "proceso de reembolso de viáticos empresas Colombia". These are informational queries with low competition and high strategic value because they capture the user before any competitor does.

**Moment 2 — Category evaluation.** The user understands that a solution exists and is evaluating the category. They search for product terms: "tarjeta empresarial para empresas México", "gestão de despesas empresariais", "tarjeta corporativa sin aval Colombia". These are transactional queries — the user is actively looking for a product, not just an answer.

**Moment 3 — Fit assessment.** The user has shortlisted options and wants to understand if Clara works for their specific company. They search for contextualized terms: "Clara para startups México", "tarjeta empresarial PyME Colombia", "cartão corporativo para médias empresas Brasil". These are navigational-transactional queries where the user already knows the brand and is evaluating fit.

**Moment 4 — Decision.** The user is ready to commit. They look for pricing, comparisons, and social proof. They search for "precio tarjeta corporativa Clara", "Clara vs banco tradicional", or simply navigate directly to pricing and customer pages.

The current site is built almost entirely for Moment 4. The homepage hero presents a registration form before establishing any narrative. Moments 1, 2, and 3 are largely unaddressed.

---

## 1. Content Architecture Proposal

### Pages to Optimize (existing)

**`/es-mx` and `/es-co` homepages**

These pages go directly to a registration form without a narrative layer. The hero communicates a tagline ("Gestión de gastos para equipos financieros exigentes") but does not show the user what Clara actually does before asking them to sign up.

Optimization: Add a narrative section between the hero and the CTA that visualizes the complete spend lifecycle — from employee purchase to CFO reconciliation. This section does not need to be long; it needs to be sequential and specific. It should link internally to product and solution pages based on user profile (by company size, by role). The H1 should incorporate the primary search term for each market ("tarjeta empresarial" for MX and CO) while preserving the brand's positioning language in subheadings.

**`/es-mx/products/corporate-card` (and equivalent in CO and BR)**

This is the highest-intent product page and the one most likely to rank for transactional queries. It currently shares components with three other card pages (Black, White, Virtual) and the small-business solution page, diluting its semantic focus.

Optimization: Consolidate the individual card pages (`/cards/black-card`, `/cards/white-card`, `/cards/virtual-card`) into this page as anchored sections with 301 redirects from the individual URLs. This concentrates link equity into one URL and eliminates the thin content problem. The page should be restructured around the H1 "Tarjeta empresarial para equipos que escalan con control", with H2s that cover card types, use cases, and differentiators against traditional bank cards. The FAQ section should be expanded with high-intent questions: "¿Puedo dar tarjeta corporativa a mis empleados sin aval?", "¿Cómo controlo los límites de gasto por empleado?", "¿Qué diferencia a Clara de una tarjeta de banco tradicional?".

**`/es-mx/solutions/small-business` (and equivalents; demo slug later renamed to `/empresas`)**

Currently a near-duplicate of the corporate card page with a different H1. The solution pages need a fundamentally different content type than the product pages — they should answer "is Clara right for my company?" not "what does Clara do?".

Optimization: Rewrite around a specific user profile. For small-business: a finance manager at a 10-50 person company dealing with manual expense reports, employees paying out of pocket, and month-end reconciliation chaos. The content should narrate that specific problem, show how Clara's platform resolves each friction point in sequence, and include a customer story from a comparable company. This page should link to the product page for feature details and to the pricing page for the decision moment.

**`/pt-br/` homepage and product pages**

Brasil already uses the correct vocabulary ("cartão corporativo") but has the same absence of mid-funnel narrative. The optimization logic is identical to MX and CO — add the spend lifecycle narrative, restructure the product page around consolidated card content, and build solution pages with real user profiles.

---

### New Pages to Create

**Content cluster 1 — Mid-funnel informational pages (MX priority)**

These pages target Moment 1 searches. They are written around specific operational problems, answer the user's question in full, and position Clara as the solution at the end — not as a product pitch, but as the natural conclusion to the narrative.

Pages to create:

- `/es-mx/recursos/como-reembolsar-gastos-a-empleados` — targets "cómo reembolsar gastos a empleados México". Covers the full reimbursement process, the problems with manual approaches (receipts, transfers, reconciliation), and how an automated platform changes the workflow. Links to `/es-mx/products/corporate-card` and `/es-mx/solutions/small-business`.

- `/es-mx/recursos/control-de-gastos-corporativos` — targets "cómo controlar gastos de equipo en campo". Covers card controls, approval flows, and real-time visibility. Links to the consolidated corporate card page.

- `/es-mx/recursos/politica-de-viaticos-empresas` — targets "política de viáticos empresas México". Covers how to structure a travel expense policy, what tools support enforcement, and how Clara's TravelPay solves the reconciliation problem. Links to the TravelPay product page.

**Content cluster 2 — Mid-funnel informational pages (BR priority)**

- `/pt-br/recursos/como-reembolsar-despesas-funcionarios` — targets "como reembolsar despesas de funcionários". Same logic as the MX reimbursement page, adapted to Brazilian regulatory context (NF-e, CNPJ requirements).

- `/pt-br/recursos/gestao-de-despesas-empresariais` — targets "gestão de despesas empresariais". Category-level informational page that explains the discipline of corporate expense management and positions Clara's platform as the solution.

**Content cluster 3 — "Operating system" narrative page**

A page that does not currently exist and that no competitor has built well: a visual, sequential explanation of the complete corporate spend lifecycle. Not a feature list — a narrative that shows what happens from the moment an employee swipes a card to the moment the finance team closes the month. This page targets users in Moment 2 who are evaluating whether Clara covers their full workflow, and it is the primary content asset for GEO — it is the kind of structured, specific, attributable content that AI-powered search engines surface when someone asks "what is the best expense management platform for companies in Mexico."

Proposed URL: `/es-mx/plataforma` or `/es-mx/como-funciona`

---

### Interlinking Architecture

The interlinking should reflect the user journey sequence, not the site's internal folder structure.

```
Homepage (es-mx)
├── → /es-mx/products/corporate-card        [primary product, transactional]
├── → /es-mx/solutions/small-business       [fit assessment, by size]
├── → /es-mx/solutions/enterprise           [fit assessment, by size]
└── → /es-mx/como-funciona                  [narrative/operating system page]

/es-mx/products/corporate-card
├── → /es-mx/solutions/small-business       [if you're a growing team]
├── → /es-mx/solutions/enterprise           [if you're scaling fast]
├── → /es-mx/recursos/control-de-gastos-corporativos  [go deeper on a use case]
└── → /es-mx/planes                         [decision moment]

/es-mx/recursos/como-reembolsar-gastos-a-empleados
├── → /es-mx/products/corporate-card        [the solution]
├── → /es-mx/solutions/small-business       [is this right for my company?]
└── → /es-mx/planes                         [decision CTA, lower in the page]

/es-mx/como-funciona
├── → /es-mx/products/corporate-card
├── → /es-mx/customers/[customer-case]
└── → /es-mx/planes
```

The key principle: every informational page has a path to a transactional page. Every product page has a path to a solution page. Every solution page has a path to pricing and registration. No page is a dead end.

---

## 2. Search Intent Mapping

| Cluster | Example queries | Intent | Page design implications | CTA strategy |
|---|---|---|---|---|
| Mid-funnel informational (MX/CO) | "cómo reembolsar gastos a empleados", "control de gastos corporativos PyME" | Informational | Long-form, problem-first structure. Answer the question fully before introducing Clara. No registration form above the fold. | Secondary CTA: "Ver cómo Clara lo resuelve" → links to product page. Primary CTA at bottom: "Empieza gratis". |
| Mid-funnel informational (BR) | "como reembolsar despesas funcionários", "gestão de despesas empresariais" | Informational | Same as above, adapted to BR regulatory context. | Same pattern. |
| Primary product page | "tarjeta empresarial México", "tarjeta corporativa sin aval", "cartão corporativo Brasil" | Transactional | Feature-focused but narrative-led. Show the spend lifecycle, not just a feature list. Registration form present but not dominant. | Primary CTA: "Regístrate gratis". Secondary: "Explora la plataforma". |
| Solution pages (by size) | "tarjeta empresarial para startups", "Clara para PyMEs Colombia" | Transactional-navigational | User-profile-first. Open with the specific problem of that company type. Include one customer story from a comparable company. | Primary CTA: "Empieza gratis". Social proof (customer logo + quote) adjacent to CTA. |
| Operating system / platform page | "plataforma gestión de gastos empresas", "mejor solución gastos corporativos México" | Informational-transactional | Visual, sequential. Show the full lifecycle. Designed to be scannable and citable — structured for both humans and AI search engines. | Mid-page CTA: "Ver demo". Bottom CTA: "Regístrate". |
| Fit / comparison | "Clara vs banco tradicional", "tarjeta corporativa sin historial crediticio" | Transactional | Comparison-format. Be explicit about what Clara does that banks cannot. | Primary CTA: "Empieza gratis — sin aval". |

---

## 3. Prioritization Rationale

Given a small team with limited bandwidth, the prioritization principle is: fix what is losing traffic first, then build what captures new demand.

**First: Fix the technical foundation (Weeks 1–3)**

Nothing built on top of a broken hreflang and sitemap structure will reach its potential. The hreflang implementation, sitemap restructure, and 301 redirects for card page consolidation are the prerequisites for everything else. These changes require engineering time but minimal content production. Without them, new pages may not be indexed in the right markets even if the content is excellent.

**Second: Optimize the primary product page (Weeks 3–6)**

`/es-mx/products/corporate-card` is the highest-intent page on the site and the most direct path to recovering organic traffic. Rewriting the H1, restructuring the FAQ with high-intent questions, consolidating the card subpages, and adding internal links to solution pages is a contained project with direct impact on the queries Clara most needs to rank for. The same template applies to `/es-co/` and `/pt-br/` with market-specific vocabulary.

**Third: Build the narrative layer (Weeks 6–10)**

The mid-funnel informational pages and the platform narrative page are the highest-leverage content investment for long-term organic growth and GEO presence. They take longer to rank but they address the moments of the user journey that no current page covers. Starting with one page per market — "cómo reembolsar gastos a empleados" for MX, "como reembolsar despesas de funcionários" for BR — allows the team to establish the content template before scaling it.

**What to defer**

Solution pages by industry (the site has them but they are empty) and comparison pages require either customer data or competitive research that takes time to do well. Building them quickly with generic content creates the same thin-content problem that already exists. These should be built after the primary product page and informational cluster are producing results and the team has signal from Search Console about which queries are gaining traction.

The operating system narrative page is strategically important but requires design and content collaboration — it is not a quick win. It should be scoped as a Q2 project once the technical foundation is stable.
