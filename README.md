# Clara — Technical SEO Challenge

**Candidate:** Armando Rodríguez Romero  
**Role:** Website Specialist (SEO)  
**Submitted:** May 2026

---

## Submission Map

- `part-a/` — Quick SEO audit of `clara.com` (technical issues, homepage review, content opportunities)
- `part-b/` — Keyword strategy and content architecture (what to optimize, what to build, interlinking)
- `part-c/` — GEO / AI search plan (testing approach, improvements, executive reporting model)
- `part-d/` — Webflow quick win with before/after artifacts, SEO hypothesis, and validation metrics

---

## Challenge Requirements — Compliance Checklist

The challenge asked: *"Imagine the `/empresas` page on clara.com has a high bounce rate and isn't ranking well for 'tarjeta corporativa empresas'. Propose and execute one concrete improvement."*

The minimum deliverable options were:

| Requirement | Status | Where |
|---|---|---|
| Restructure the H1/H2 hierarchy | ✅ Done | `part-d/after/corporate-card.html` — duplicate H1 fixed, heading hierarchy corrected |
| Add FAQ schema markup | ✅ Done | `part-d/after/corporate-card.html` — 8-question JSON-LD `FAQPage` schema in `<head>` |
| Rewrite the meta title and description | ✅ Done | Both `after/` pages — title, meta description, and canonical rewritten |
| Improve hero copy for conversion and SEO | ✅ Done | H1 rewritten for search intent + brand tone; hero copy reframed around user pain |

All four were implemented. The work goes further — see [Part D notes](part-d/notes.md) for the full rationale.

---

## The Actual Problem: A Matrioshka Site

Before writing a single recommendation, the first question was: *why does `/empresas` have a high bounce rate?*

The instinctive answer is "bad copy" or "wrong keyword." Those are symptoms. The structural diagnosis is different.

Clara's site is built like a [Matrioshka](https://en.wikipedia.org/wiki/Matryoshka_doll) — nested layers that each look complete from the outside, but when you open one, there's another inside with no connecting thread. The homepage links to product pages. Product pages list features. Features link to... registration. There is no middle layer: no "how does this work for a company like mine," no path from awareness to consideration, no content that earns the click before asking for commitment.

A user searching "tarjeta corporativa empresas" lands on `/es-mx/products/corporate-card`. The page is visually polished. But it doesn't answer the implicit question behind that search: *"Is this actually for my type of business? What happens after I sign up? Why not just use my bank?"* The page doesn't answer any of those questions — it asks for a registration. The user bounces.

The bounce rate is not a copywriting problem. It's an architecture problem. Fixing the H1 without fixing the journey is polishing one doll without opening the next one.

**That is why the `/empresas` page doesn't exist in the production sitemap** — and why working on the two real pages that exist (`/es-mx/products/corporate-card` and `/es-mx/solutions/small-business`) is more honest and more useful than fabricating a URL.

---

## Audit Approach: Symptom → Verification → Diagnosis

The audit followed a deliberate sequence. The order matters.

### Step 1 — SEMrush: establish that a real problem exists

Before diagnosing causes, confirm there's a symptom worth diagnosing. SEMrush showed a consistent 11% drop in organic traffic (235,528 estimated visits, April 2026). That number gave the analysis a real business context — not a hypothetical exercise.

### Step 2 — DevTools: verify manually before trusting tools

Stackoptic flagged `lang` attribute inconsistencies across the site. Before writing that as a finding, DevTools confirmed the actual state:

- `clara.com/es-mx` → `lang="es-MX"` ✅
- `clara.com/es-co` → `lang="es-CO"` ✅

The issue is scoped to the global `clara.com` domain — not a site-wide failure. This distinction matters: if someone from the Clara team opens DevTools on `/es-mx` and sees `es-MX`, a document that claims otherwise loses all credibility. **Tools surface signals. Judgment determines scope.**

### Step 3 — Stackoptic: structured scoring to prioritize

With the manual baseline established, Stackoptic provided structured evidence across dimensions: hreflang implementation, structured data, performance, readability, and martech maturity. The key scores:

- **Hreflang:** 10/10 on the global homepage — broken specifically on internal pages (relative URLs instead of absolute)
- **Structured data:** 0/100 — no `FAQPage`, no `Organization`, no `BreadcrumbList` anywhere on the site
- **Flesch Reading Ease: 18/100** — equivalent to an academic paper, for a product aimed at SME finance directors
- **Martech maturity: 32/100** — only GA and GTM detected; no heatmaps, no A/B testing tools

---

## Keyword Strategy: Coexistence, Not Substitution

The most consequential decision in the keyword work was how to handle the gap between what Clara calls its product ("tarjeta corporativa") and what users search for ("tarjeta empresarial").

Google Trends data over 12 months (CSV exports, MX and CO) shows "tarjeta empresarial" consistently outperforming "tarjeta corporativa" in Mexico and Colombia. In Colombia, "tarjeta corporativa" has near-zero search volume. Brazil is the exception — "cartão corporativo" leads, and the site already uses it correctly.

The wrong response to this data is to rename the product. The right response is to work both terms in separate layers:

- **"empresarial"** anchors the highest-weight SEO elements: title tag, H1, meta description — the signals Google weighs most heavily for ranking
- **"corporativa"** reinforces brand identity in subheadings and body copy — maintaining the product name as Clara uses it

This resolves the tension between brand naming and search behavior without creating inconsistency. The URL `/es-mx/landing/tarjeta-de-credito-empresarial` already exists, which confirms the opportunity was partially identified — but it exists as an isolated landing page with no content architecture behind it.

**On pleonasms:** "tarjeta empresarial para empresas" — the word "empresas" is already implied by "empresarial." Writing it out is redundant and signals low editorial quality. The corrected title: `Clara — Tarjeta corporativa y gestión de gastos para tu empresa en México`.

---

## GEO Baseline Finding

Testing Clara's presence in ChatGPT, Perplexity, and Google AI Overviews revealed a specific accuracy problem: some models identify Clara as a Visa issuer when it operates on the Mastercard network. The company appears in AI search responses — but without control over the framing.

This is the GEO risk for a fintech: AI models cite information that's confidently wrong about a product detail that affects purchase decisions. A prospect asking "what network does Clara operate on?" gets a wrong answer from a tool they trust.

The structural fix is not ad-hoc: it's a `llms.txt` file in Spanish and Portuguese with verifiable, citable facts, combined with a "how it works" page that gives AI models a clean, structured source to pull from.

---

## Part D — What Was Built and Why

### Why two pages instead of one

`/es-mx/products/corporate-card` answers "what is the product." `/empresas` (demo slug for `/es-mx/solutions/small-business`) answers "is this for a company like mine." Neither page linked to the other originally. A user in the consideration stage needs both — and the absence of a path between them is the architectural cause of the bounce.

The `before/` and `after/` demonstrate two things simultaneously:
1. **Technical fixes** — hreflang with absolute URLs, duplicate H1 corrected, FAQ schema added
2. **Narrative architecture** — interlinking between the two pages, differentiator section, user profile framing

### How the pages were obtained

The `before/` pages were not obtained with `wget` or a static site crawler. Claude Code connected directly to Clara's live Webflow site via the Webflow Designer MCP. This means the structure reflects the actual production site — not a snapshot with broken assets and missing CSS classes. The changes in `after/` were built on top of that real structure.

### The four mandatory improvements — executed

**1. H1/H2 hierarchy restructure**  
The original `corporate-card` page had two `<h1>` elements — a technical SEO error that dilutes the primary keyword signal and confuses Google's heading interpretation. The second `<h1>` was corrected to `<h2>`. No visual change. Zero implementation risk.

**2. FAQ schema markup**  
Eight questions added as `FAQPage` JSON-LD in the `<head>` — covering the questions actual prospects ask before signing up: credit requirements, card limits, how reimbursements work, and multi-currency support. This enables rich-result accordions in SERP and gives AI search models structured, citable answers about Clara's product.

**3. Meta title and description rewrite**

| Element | Before | After |
|---|---|---|
| Title | `Clara \| Gestión Financiera Inteligente para LatAm` | `Clara — Tarjeta corporativa y gestión de gastos para tu empresa en México` |
| Meta description | Features list, no conversion intent | `Tarjeta empresarial para equipos en México. Crédito ilimitado, controles por empleado y conciliación automática con SAT e integración ERP. Más de 30,000 empresas confían en Clara.` |

**4. Hero copy rewrite**  
Original: `Gestión de gastos para equipos financieros exigentes` — a brand tagline, not a search phrase.  
Revised: `El control de gastos que tu empresa necesitaba desde el primer día` — second person (consistent with Clara's voice guidelines), benefit-first, no empty superlatives.

The copy follows Clara's documented tone of voice principles: tuteo, concrete benefits over feature lists, no corporate filler, proof through specificity not adjectives.

---

## Live Demo

**Review starting point (do not use home):** [https://clara-seo-challenge.webflow.io/empresas](https://clara-seo-challenge.webflow.io/empresas)

| Page | URL |
|---|---|
| Empresas (after, formerly Small Business) | `https://clara-seo-challenge.webflow.io/empresas` |
| Corporate Card (after) | `https://clara-seo-challenge.webflow.io/corporate-card` |

The demo is built in a real Webflow project using Clara's production CSS classes (`fbl-`/`uui-` naming system). Both pages include the four mandatory improvements plus full narrative interlinking, a logos strip (11 enterprise clients), and reusable Navbar/Footer components.

---

## Toolchain

| Tool | Role |
|---|---|
| **SEMrush** | Organic traffic baseline — confirmed 11% drop context before any diagnosis |
| **Browser DevTools** | Manual verification of `lang`, `hreflang`, canonical — prevented false positives from automated tools |
| **Stackoptic** | Structured technical audit — hreflang, schema, WCAG, Core Web Vitals, readability, martech maturity |
| **Google Trends** | 12-month CSV exports by country — evidence base for keyword coexistence strategy |
| **Claude Code + Webflow MCP (Designer)** | Live connection to Clara's production site; built `before/` pages on real site structure. Built Webflow demo pages using MCP Designer Tools. |
| **Cursor** | Code audits — semantic validation, JSON-LD well-formedness, regression check on `before/after/` |
| **ChatGPT / Perplexity / Gemini** | GEO baseline — presence, framing accuracy, and factual errors in AI-attributed information |

---

## Repository Structure

```
ClaraSEOChallenge/
├── README.md
├── part-a/
│   └── audit.md
├── part-b/
│   └── keyword-strategy.md
├── part-c/
│   ├── geo-ai-search.md
│   └── llms.txt
└── part-d/
    ├── before/
    ├── after/
    │   ├── README.md
    │   ├── corporate-card.html
    │   └── small-business.html
    └── notes.md
```

---

## Current Status

**Current status (May 2026):** Parts A-D are complete. Review should start on `/empresas` and then move to `/corporate-card` (the homepage is not used as the evaluation entry point for this challenge). Navbar and Footer were extracted as reusable Webflow components, and copy/metadata updates were applied to both pages.

**Latest sync (May 8, 2026):** The Webflow page previously labeled "Small Business" now uses slug `/empresas` (page ID `69fc967c3d0867342deac6eb`). Documentation and navigation references were updated accordingly.
