# Execution Roadmap — Clara SEO Challenge

---

## Current Status

| Part | Document | Repo status |
|---|---|---|
| A | `part-a/audit.md` | ✅ In repo |
| B | `part-b/keyword-strategy.md` | ⏳ Draft ready — pending commit |
| C | `part-c/geo-ai-search.md` | ⏳ Draft ready — pending commit |
| D | `part-d/before/` + `part-d/after/` + `part-d/notes.md` | ✅ In repo |
| — | `README.md` | ✅ In repo |
| — | Webflow MCP setup (`.mcp.json`, `CLAUDE.md`, `context/`) | ✅ In repo — OAuth auth pending |

---

## Pending Execution

### Phase 1 — Repo setup (30 min)

```bash
mkdir -p clara-seo-challenge/{part-a,part-b,part-c,part-d/{before,after}}

cp audit.md clara-seo-challenge/part-a/
cp keyword-strategy.md clara-seo-challenge/part-b/
cp geo-ai-search.md clara-seo-challenge/part-c/

cd clara-seo-challenge
git init
git remote add origin [repo URL]
```

---

### Phase 2 — Capture before/ pages (15 min)

Pages were captured directly via the Webflow Designer MCP — not via `wget`. This gives the `before/` files the real production structure with intact CSS classes and component context, not a static snapshot with broken assets.

Commit: `"feat: add before/ pages — current state of clara.com via Webflow MCP"`

---

### Phase 3 — Implement changes with Claude Code MCP (1–2 hrs)

Open Claude Code in the repo with `SKILL-claude-code.md` as context.

**Execution order:**

1. Copy `before/corporate-card.html` → `after/corporate-card.html`
2. Apply changes to `after/corporate-card.html`:
   - [x] Title tag → `Clara — Tarjeta corporativa y gestión de gastos para tu empresa en México`
   - [x] Meta description → benefits-oriented with "sin aval" and social proof
   - [x] H1 → "La tarjeta empresarial que escala con tu equipo"
   - [x] New H2 → "Lo que tu banco no puede darte"
   - [x] FAQ schema JSON-LD in `<head>`
   - [x] Interlinking section → `/es-mx/solutions/small-business`
3. Copy `before/small-business.html` → `after/small-business.html`
4. Apply changes to `after/small-business.html`:
   - [x] Title tag → "Tarjeta Empresarial para PyMEs en México | Clara"
   - [x] H1 → "El control de gastos que tu PyME necesitaba desde el día uno"
   - [x] User profile section
   - [x] Interlinking back → `/es-mx/products/corporate-card`
5. `part-d/notes.md` with hypotheses and validation metrics

Commit: `"feat: implement SEO improvements and narrative interlinking (part-d/after)"`

---

### Phase 4 — Webflow (optional but recommended) (2–3 hrs)

1. Create new project in Webflow
2. Replicate the visual structure of `after/corporate-card.html` using Clara's components as reference
3. Connect Webflow to the repo via Webflow Git
4. Publish from Webflow → code syncs to `/part-d/after/`
5. Claude Code applies final SEO adjustments on top of exported code

**Note:** Webflow → Git sync is one-directional. Changes made by Claude Code that only live in the repo will be overwritten if a new Webflow publish happens.

---

### Phase 5 — README.md (45 min)

The README is the first thing the evaluator reads. It is not an index — it is your voice explaining decisions.

Structure used:

```markdown
# Clara — Technical Challenge: Website Specialist (SEO)

## Challenge Requirements — Compliance Checklist
## The Actual Problem: A Matrioshka Site
## Audit Approach: Symptom → Verification → Diagnosis
## Keyword Strategy: Coexistence, Not Substitution
## GEO Baseline Finding
## Part D: What Was Built and Why
## Toolchain
## Repository Structure
```

Commit: `"docs: add README with approach and decisions"`

---

### Phase 6 — Final push and review (30 min)

```bash
git add .
git commit -m "chore: final review and cleanup"
git push origin main
```

Verify on GitHub:
- [ ] The diff between `before/` and `after/` is readable and shows exactly what changed
- [ ] README renders correctly
- [ ] All `.md` files are clean and in English
- [ ] No temporary files or unnecessary assets

---

## For the Live Session

Most likely questions:

**"Why did you work on two pages instead of one?"**
→ Because the real problem is not the content of a single page — it's that the pages aren't in conversation. The challenge mentions `/empresas` but that URL doesn't exist on the site. I chose to work the real architectural problem instead of simulating a hypothetical URL.

**"How would you validate that these changes worked?"**
→ Search Console for impressions and CTR on queries containing "tarjeta empresarial". Google Analytics for bounce rate and pages per session for users who entered via `/products/corporate-card`. Compare 30 days before vs 30 days after the change.

**"Why did you replace 'corporativa' with 'empresarial'?"**
→ Google Trends with 12-month CSV exports by country shows "tarjeta empresarial" consistently outperforming "tarjeta corporativa" in Mexico and Colombia. It's not an opinion — it's data. The strategy is not to remove "corporativa" from the site but to use "empresarial" as the primary keyword in the highest-weight SEO elements (title, H1) and keep "corporativa" as a secondary semantic signal in body copy.

**"Show me the FAQ schema you implemented."**
→ Open `after/corporate-card.html`, find `application/ld+json`, explain each field and why those specific questions were chosen.

**"What would you do differently with more time?"**
→ Build the platform / "how it works" page that describes the complete expense lifecycle. That's the piece the site is most missing and the one with the highest GEO impact. I'd also work on a `llms.txt` in Spanish and Portuguese with the accuracy corrections identified in the GEO baseline (Mastercard vs Visa in Perplexity's response about Clara).
