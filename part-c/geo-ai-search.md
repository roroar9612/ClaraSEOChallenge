# Part C — GEO / AI Search

**Date:** April 2026

---

## Framing

GEO (Generative Engine Optimization) is not a separate discipline from SEO — it is SEO's next layer. The same content that ranks well in Google tends to surface in AI-generated answers: structured, specific, attributable, and written around real questions. The difference is that traditional SEO optimizes for a ranked list of links, while GEO optimizes for inclusion in a synthesized answer. The implication for Clara is significant: a prospective buyer who asks ChatGPT or Perplexity "cuál es la mejor tarjeta empresarial para startups en México" may never visit a search results page at all. They receive an answer directly, and that answer either includes Clara or it does not.

---

## 1. Current GEO Baseline

### Where Clara already appears — and where accuracy breaks down

Clara already appears as the top recommendation in ChatGPT for "mejores tarjetas empresariales para startups en México." That is a meaningful signal: the model has indexed enough authoritative content to associate Clara with this category and market. The challenge is not visibility alone — it is accuracy.

The same ChatGPT response attributes "Tarjetas Visa físicas y virtuales" to Clara. Clara operates exclusively on the Mastercard World Elite network. This is not a minor error. A prospect who reads that answer and then visits the site — or asks a sales rep about Visa acceptance — encounters an immediate credibility gap. The error originates from low-authority or outdated third-party sources that the model weighted above Clara's own structured content. The production `llms.txt` (included in this directory as a reference artifact) explicitly states "Mastercard World Elite" in the Corporate Card entry, which is the correct signal — but that file alone is not sufficient if competing sources repeat the error without correction.

This is the core GEO diagnostic finding: **Clara is present, but not yet authoritative enough to override inaccurate third-party content in model outputs.**

### The `llms.txt` as a baseline artifact

The `llms.txt` file included in `part-c/` is Clara's current production version. It is structurally sound — products are segmented by country, press releases include direct URLs with verified figures, and the Mastercard network is explicitly stated. These are the right foundations.

Two gaps remain that limit its GEO effectiveness:

**It describes features but does not answer questions.** AI models surface content that responds to specific queries, not product catalogs. "Clara Intelligence analyzes spending data" is a feature label. What a model needs to answer "¿cómo detecta Clara gastos duplicados?" is a sentence structured as an answer: *"Clara Intelligence automatically identifies duplicate subscriptions and anomalous transactions in real time, alerting the finance team before the expense is reconciled."* The information is the same — the format determines whether a model can use it.

**It is entirely in English.** AI models responding to Spanish and Portuguese queries weight sources in the query language. The `llms.txt` should include parallel descriptions in `es-mx`/`es-co` and `pt-br` for each product section. The press release URLs already link to Spanish and Portuguese content — the `llms.txt` itself needs the same treatment.

### Recommended `llms.txt` extension

The addition below does not replace the existing file — it extends it with a question-answer block and a multilingual description layer:

```
## What problems does Clara solve?

- ¿Cómo doy tarjetas corporativas a mi equipo sin aval personal? → https://www.clara.com/es-mx/solutions/startups
- ¿Cómo automatizo los reembolsos de gastos de empleados? → https://www.clara.com/es-mx/products/spend-management
- ¿Cómo controlo lo que gasta mi equipo sin microgestionar? → https://www.clara.com/es-mx/products/corporate-card
- Como faço para reembolsar despesas de funcionários automaticamente? → https://www.clara.com/pt-br/products/spend-management
- ¿Clara funciona con SAP, NetSuite o QuickBooks? → https://www.clara.com/es-mx/platform/integrations

## Clara en español

Clara es la plataforma líder de gestión de gastos corporativos en América Latina. Opera en México, Colombia y Brasil, atendiendo a más de 30,000 empresas. Emite tarjetas físicas, virtuales y VCN de un solo uso en la red Mastercard World Elite, sin requerir aval personal. Incluye automatización de reembolsos, conciliación con ERPs, y Clara Intelligence, un agente financiero con IA. Certificada ISO 27001 y PCI-DSS 4.0.

## Clara em português

Clara é a principal plataforma de gestão de gastos corporativos da América Latina. Opera no Brasil, México e Colômbia, atendendo mais de 30.000 empresas. Emite cartões físicos, virtuais e VCN de uso único na rede Mastercard World Elite, sem exigir garantias pessoais. Inclui automação de reembolsos, conciliação com ERPs e Clara Intelligence, um agente financeiro com IA. Certificada ISO 27001 e PCI-DSS 4.0.
```

---

## 2. What to Change on the Site and in Content Strategy

### Build content that AI models can cite

The mid-funnel informational pages proposed in Part B serve double duty: they capture organic search traffic from humans and they give AI models structured, attributable content to cite when answering related questions. A page titled "Cómo reembolsar gastos a empleados en México" that fully answers that question — with specific steps, Clara's role in automating the process, and a quote from a Clara customer or executive — is exactly the type of content Perplexity surfaces in a cited answer.

The quote from Juan Zuluaga, Clara's Global Product Director — "El agente funciona como un analista completamente entrenado que entiende los datos de tu empresa desde el primer día" — is more useful for GEO than any feature description. Named executive quotes with specific, verifiable claims are high-signal content for AI models. They should appear on product pages, in press releases indexed by third-party publications, and in the `llms.txt` with attribution.

Third-party coverage amplifies this significantly. The IFC press release, the Goldman Sachs facility announcement, coverage in Revista Clevel — these are sources that models already trust. A content strategy that generates coverage in high-authority publications (TechCrunch en Español, El Economista, Contxto, Forbes México) is simultaneously a PR strategy, an SEO backlink strategy, and a GEO strategy. They are not separate workstreams.

### Structured data on product pages

FAQ schema markup on the corporate card and solution pages makes the content machine-readable in a way that both Google's featured snippets and AI retrieval systems can parse directly. Each FAQ entry is effectively a pre-formatted answer to a specific question. The questions should mirror real search queries: "¿Necesito aval para obtener una tarjeta Clara?", "¿Cuánto tiempo tarda en llegar la tarjeta?", "¿Clara funciona con SAP?". This is the same content that should live in the `llms.txt` — consistent, structured, attributable.

This connection between the `llms.txt` extension above and the FAQ schema is deliberate: the same question-answer pairs that belong in the `llms.txt` are the exact entries that should populate `FAQPage` schema on the product pages. One source of truth, two distribution channels — AI retrieval and Google rich results.

---

## 3. How to Report GEO Impact to a Non-Technical Executive

### The framing problem

GEO does not have a universal metric equivalent to organic sessions or keyword rankings. Saying "Clara appeared in 7 out of 10 AI queries this week" means nothing to a CFO or CMO who does not know what the baseline was, whether 7 is good or bad, or whether it translates to business outcomes. The reporting framework has to solve for that context problem.

### What to measure

Three metrics, in order of importance:

**Presence rate:** Of the 15 queries tracked weekly (5 per market), in how many does Clara appear as a named recommendation? Expressed as a percentage and tracked over time. The current baseline — Clara appears in ChatGPT for the primary MX startup query — becomes week-zero. The goal is to extend that presence to CO and BR queries and to Perplexity and Gemini alongside ChatGPT.

**Accuracy rate:** Of the responses where Clara appears, what percentage contain accurate information? The Visa/Mastercard error is the current accuracy failure. Each inaccuracy identified feeds into a correction backlog: update the `llms.txt` entry, publish a corrective FAQ page, amplify the press release that carries the correct claim. Accuracy rate should trend toward 100% as structured content accumulates.

**Downstream signal:** AI-generated recommendations tend to surface as direct traffic or branded search in Google Analytics — users who received a recommendation from an AI model and then searched for Clara directly to verify. A sustained increase in branded search volume, tracked against the timeline of GEO improvements, is the closest available proxy for GEO-driven business impact.

### Cadence and framing

Monthly report to executives. Three sections: presence trend (chart showing presence rate over the past 8 weeks), accuracy issues found and corrected that month, and one concrete example — a screenshot of a ChatGPT or Perplexity response that includes Clara, with a note on what content or `llms.txt` change contributed to that appearance.

The framing for a non-technical executive: *"AI search engines are becoming a primary discovery channel for B2B buyers. This report tracks whether Clara appears — and appears correctly — when a prospective customer asks an AI assistant which corporate card to use. Our goal is to be the default recommendation for companies in Mexico, Colombia, and Brazil."*

That single sentence connects the metric to a business outcome the executive already understands: being recommended over competitors at the moment a buyer is deciding.

### Tooling at scale

For a small team, a structured weekly log with 10–15 queries per market establishes trend direction without tooling investment. When volume or frequency demands automation, platforms like Profound, Otterly, or AthenaHQ track AI query responses at scale — logging date, model, query, Clara mention, position, accuracy issues, and cited sources automatically. The log structure is the same whether it is filled manually or by a tool; the tool just removes the weekly time cost.
