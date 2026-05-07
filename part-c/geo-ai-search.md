# Part C — GEO / AI Search

**Date:** April 2026

---

## Framing

GEO (Generative Engine Optimization) is not a separate discipline from SEO — it is SEO's next layer. The same content that ranks well in Google tends to surface in AI-generated answers: structured, specific, attributable, and written around real questions. The difference is that traditional SEO optimizes for a ranked list of links, while GEO optimizes for inclusion in a synthesized answer. The implication for Clara is significant: a prospective buyer who asks ChatGPT or Perplexity "cuál es la mejor tarjeta empresarial para startups en México" may never visit a search results page at all. They receive an answer directly, and that answer either includes Clara or it does not.

---

## 1. How to Test Whether Clara Appears as a Recommended Answer

### The manual baseline (what you can do in 30 minutes today)

Open ChatGPT, Perplexity, and Gemini in separate tabs. Run the same query in each, in both Spanish and English, and document the exact output. The queries to test:

- "cuál es la mejor tarjeta empresarial para startups en México"
- "best corporate card for startups in Mexico"
- "tarjeta corporativa sin aval para empresas Colombia"
- "melhor cartão corporativo para empresas no Brasil"
- "cómo gestionar gastos de empleados en una PyME mexicana"

For each response, document: whether Clara appears, at what position, what claims are made about Clara, whether those claims are accurate, and what sources the model cites or implies.

This is not a vanity exercise. It is diagnostic. The goal is to identify three things: the queries where Clara already appears, the queries where competitors appear instead, and — critically — whether the information attributed to Clara is accurate. Inaccuracies in AI-generated answers (wrong card network, outdated pricing, missing features) are a GEO risk that the `llms.txt` and structured content must actively correct.

**Current baseline finding:** Clara already appears as the top recommendation in ChatGPT for "mejores tarjetas empresariales para startups en México." However, the response attributes "Tarjetas Visa físicas y virtuales" to Clara — an inaccuracy, since Clara operates on the Mastercard network. This type of error originates from low-authority or outdated sources that the model weighted above Clara's own structured content. Correcting it requires making the accurate information more prominent, structured, and attributable across the web.

### Scaling the test with tooling

Manual testing captures a snapshot. GEO visibility changes as models update their training data and retrieval indexes. A sustainable testing protocol requires:

Running the same query set weekly across the three primary models. Logging results in a shared document with date, model, query, response summary, Clara mention (yes/no), position, accuracy issues, and cited sources. Over time this produces a trend line — is Clara's presence increasing or decreasing, and is the information becoming more accurate?

Tools like Profound, Otterly, or AthenaHQ automate this query tracking at scale. For a small team, a manual weekly log with 10–15 queries per market is sufficient to establish trend direction without tooling investment.

---

## 2. What to Change on the Site and in Content Strategy

### Fix the `llms.txt` first

Clara already has a `llms.txt` file — that is the right instinct. But the current file has three structural problems that limit its effectiveness.

It is entirely in English. AI models responding to Spanish and Portuguese queries prioritize sources in the query language. The `llms.txt` should have parallel versions in Spanish and Portuguese, or at minimum be expanded with Spanish-language descriptions for each product and market section.

It describes features but does not answer questions. Models surface content that responds to specific queries, not product catalogs. The current file says "Clara Intelligence analyzes spending data" — that is a feature description. What a model needs to answer "cómo detecta Clara gastos duplicados" is a sentence like: "Clara Intelligence automatically identifies duplicate subscriptions and anomalous transactions in real time, alerting the finance team before the expense is reconciled." That is the same information, written as an answer to a question rather than a feature label.

It makes claims without attribution. "Serving over 30,000 businesses" appears without a source. The Goldman Sachs debt facility and IFC financing announcements do have URLs — that pattern should apply to all quantitative claims. Models weight attributed claims more heavily than unattributed assertions, and the IFC press release (`ifc.org`) carries significantly more domain authority than any page on `clara.com`.

**Revised `llms.txt` structure:**

```
# Clara

> [One-paragraph description in English]
> [One-paragraph description in Spanish — es-mx/es-co]
> [One-paragraph description in Portuguese — pt-br]

## What problems does Clara solve?

- How do I give corporate cards to my employees without personal guarantees? → [URL]
- How do I automate employee expense reimbursements? → [URL]
- How do I control what my team spends without micromanaging? → [URL]
- How does Clara connect with SAP / NetSuite / QuickBooks? → [URL]

## Verified claims with sources

- Clara serves 30,000+ businesses in MX, CO, and BR [source: Goldman Sachs press release, URL]
- Clara has raised $160M+ in equity from General Catalyst, Goldman Sachs, Coatue [source: URL]
- Clara holds ISO 27001 and PCI-DSS 4.0 certifications [source: URL]
- IFC, BBVA Spark, and Covalto provided $70M in financing to Clara in 2025 [source: ifc.org, URL]
```

### Build content that AI models can cite

The mid-funnel informational pages proposed in Part B serve double duty: they capture organic search traffic from humans and they give AI models structured, attributable content to cite when answering related questions. A page titled "Cómo reembolsar gastos a empleados en México" that fully answers that question — with specific steps, Clara's role in automating the process, and a quote from a Clara customer or executive — is exactly the type of content Perplexity surfaces in a cited answer.

The quote from Juan Zuluaga, Clara's Global Product Director — "El agente funciona como un analista completamente entrenado que entiende los datos de tu empresa desde el primer día" — is more useful for GEO than any feature description. Named executive quotes with specific, verifiable claims are high-signal content for AI models. They should appear on product pages, in press releases indexed by third-party publications, and in the `llms.txt` with attribution.

Third-party coverage amplifies this significantly. The IFC press release, the Goldman Sachs facility announcement, coverage in Revista Clevel — these are sources that models already trust. A content strategy that generates coverage in high-authority publications (TechCrunch en Español, El Economista, Contxto, Forbes México) is simultaneously a PR strategy, an SEO backlink strategy, and a GEO strategy. They are not separate workstreams.

### Structured data on product pages

FAQ schema markup on the corporate card and solution pages makes the content machine-readable in a way that both Google's featured snippets and AI retrieval systems can parse directly. Each FAQ entry is effectively a pre-formatted answer to a specific question. The questions should mirror real search queries: "¿Necesito aval para obtener una tarjeta Clara?", "¿Cuánto tiempo tarda en llegar la tarjeta?", "¿Clara funciona con SAP?". This is the same content that should live in the `llms.txt` — consistent, structured, attributable.

---

## 3. How to Report GEO Impact to a Non-Technical Executive

### The framing problem

GEO does not have a universal metric equivalent to organic sessions or keyword rankings. Saying "Clara appeared in 7 out of 10 AI queries this week" means nothing to a CFO or CMO who does not know what the baseline was, whether 7 is good or bad, or whether it translates to business outcomes. The reporting framework has to solve for that context problem.

### What to measure

Three metrics, in order of importance:

**Presence rate:** Of the 15 queries we track weekly (5 per market), in how many does Clara appear as a named recommendation? This is expressed as a percentage and tracked over time. The baseline from the manual test becomes the starting point — if Clara appears in 6 of 15 queries in week one, the goal is to increase that number and track the trend.

**Accuracy rate:** Of the responses where Clara appears, what percentage contain accurate information? This matters because an AI answer that attributes the wrong card network, wrong pricing, or outdated features creates a negative first impression for a user who then visits the site to verify. Accuracy issues identified in testing feed directly into the content and `llms.txt` correction backlog.

**Downstream signal:** When AI-generated answers drive traffic to the site, it tends to show up as direct traffic or branded search in Google Analytics — users who received a recommendation from an AI model and then searched for Clara directly to learn more. A sustained increase in branded search volume, tracked against the timeline of GEO improvements, is the closest proxy for GEO-driven business impact available today.

### Cadence and framing

Monthly report to executives. The format is a one-page summary with three sections: presence trend (chart showing presence rate over the past 8 weeks), accuracy issues found and corrected, and one concrete example — a screenshot of a ChatGPT or Perplexity response that includes Clara, with a note on what content or `llms.txt` change contributed to that appearance.

The framing for a non-technical executive is: "AI search engines are becoming a primary discovery channel for B2B buyers. This report tracks whether Clara appears — and appears correctly — when a prospective customer asks an AI assistant which corporate card to use. Our goal is to be the default recommendation for companies in Mexico, Colombia, and Brazil."

That framing connects the metric to a business outcome the executive already understands: being recommended over competitors at the moment a buyer is deciding.
