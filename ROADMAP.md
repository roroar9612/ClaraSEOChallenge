# Roadmap de ejecución — Clara SEO Challenge

---

## Estado actual

| Part | Documento | Estado en repo |
|---|---|---|
| A | `part-a/audit.md` | ⏳ Draft listo — pendiente de mover al repo |
| B | `part-b/keyword-strategy.md` | ⏳ Draft listo — pendiente de mover al repo |
| C | `part-c/geo-ai-search.md` | ⏳ Draft listo — pendiente de mover al repo |
| D | `part-d/before/` + `part-d/after/` + `part-d/notes.md` | ✅ En repo |
| — | `README.md` | ✅ En repo |
| — | Webflow MCP setup (`.mcp.json`, `CLAUDE.md`, `context/`) | ✅ En repo — pendiente auth OAuth |

---

## Lo que falta ejecutar

### Fase 1 — Setup del repo (30 min)

```bash
# Crear estructura de carpetas
mkdir -p clara-seo-challenge/{part-a,part-b,part-c,part-d/{before,after}}

# Copiar documentos ya producidos
cp audit.md clara-seo-challenge/part-a/
cp keyword-strategy.md clara-seo-challenge/part-b/
cp geo-ai-search.md clara-seo-challenge/part-c/

# Inicializar git
cd clara-seo-challenge
git init
git remote add origin [URL del repo en GitHub]
```

---

### Fase 2 — Clonar páginas para before/ (15 min)

```bash
wget --mirror --convert-links --adjust-extension --no-parent \
  -P part-d/before/ \
  https://www.clara.com/es-mx/products/corporate-card

wget --mirror --convert-links --adjust-extension --no-parent \
  -P part-d/before/ \
  https://www.clara.com/es-mx/solutions/small-business
```

Renombrar los archivos resultantes:
- → `part-d/before/corporate-card.html`
- → `part-d/before/small-business.html`

Commit: `"feat: add before/ pages — current state of clara.com"`

---

### Fase 3 — Implementar cambios con Claude Code MCP (1-2 hrs)

Abrir Claude Code en el repo. Pasarle el `SKILL-claude-code.md` como contexto.

**Orden de ejecución:**

1. Copiar `before/corporate-card.html` → `after/corporate-card.html`
2. Aplicar cambios en `after/corporate-card.html`:
   - [ ] Title tag → "Tarjeta Empresarial para Empresas en México | Clara"
   - [ ] Meta description → versión orientada a beneficios con "sin aval"
   - [ ] H1 → "La tarjeta empresarial que escala con tu equipo"
   - [ ] H2 nuevo → "Lo que tu banco no puede darte"
   - [ ] FAQ schema JSON-LD en `<head>`
   - [ ] Sección de interlinking → "/es-mx/solutions/small-business"
3. Copiar `before/small-business.html` → `after/small-business.html`
4. Aplicar cambios en `after/small-business.html`:
   - [ ] Title tag → "Tarjeta Empresarial para PyMEs en México | Clara"
   - [ ] H1 → "El control de gastos que tu PyME necesitaba desde el día uno"
   - [ ] Sección de perfil de usuario real
   - [ ] Interlinking de regreso → "/es-mx/products/corporate-card"
5. Crear `part-d/notes.md` con hipótesis y métricas

Commit: `"feat: implement SEO improvements and narrative interlinking (part-d/after)"`

---

### Fase 4 — Webflow (opcional pero recomendado) (2-3 hrs)

Si se quiere mostrar la versión con fidelidad visual:

1. Crear proyecto nuevo en Webflow
2. Replicar la estructura visual de `after/corporate-card.html` usando los componentes de Clara como referencia
3. Conectar Webflow al repo via Webflow Git
4. Publicar desde Webflow → el código se sincroniza automáticamente al repo en `/part-d/after/`
5. Claude Code aplica los ajustes SEO finales encima del código exportado

**Nota:** La sincronización Webflow → Git es unidireccional. Los cambios de Claude Code que vivan solo en el repo se perderán si se vuelve a publicar desde Webflow. Documentar esto en `notes.md`.

---

### Fase 5 — README.md (45 min)

El README es lo primero que lee quien evalúa. No es un índice — es tu voz explicando las decisiones.

Estructura sugerida:

```markdown
# Clara — Technical Challenge: Website Specialist (SEO)

## Approach
[2-3 párrafos explicando el hilo conductor: narrative-first architecture,
por qué el SEO es el resultado y no la estrategia, qué te pareció
más interesante del problema]

## Assumptions
[Las mismas del Assumption Log de Part A — centralizadas aquí también]

## Structure
[Descripción breve de qué hay en cada carpeta]

## Part A — SEO Audit
[1 párrafo con el hallazgo más importante]

## Part B — Keyword Strategy & Content Architecture
[1 párrafo con la decisión de arquitectura más importante]

## Part C — GEO / AI Search
[1 párrafo con el baseline finding y la propuesta]

## Part D — Quick Win
[1 párrafo explicando por qué trabajaste dos páginas en lugar de una,
y qué demuestra el before/after]

## Tools used
- Browser DevTools + view-source
- Google Trends (CSV export, últimos 12 meses por país)
- SEMrush (tráfico orgánico)
- Screaming Frog / Sitemap analysis
- wget (clonado de páginas)
- Claude Code MCP (implementación de cambios)
- Webflow (si aplica)
- ChatGPT / Perplexity (GEO baseline testing)
```

Commit: `"docs: add README with approach and decisions"`

---

### Fase 6 — Push final y revisión (30 min)

```bash
git add .
git commit -m "chore: final review and cleanup"
git push origin main
```

Revisar en GitHub que:
- [ ] El diff entre `before/` y `after/` es legible y muestra exactamente qué cambió
- [ ] El README se renderiza correctamente
- [ ] Todos los `.md` tienen formato limpio
- [ ] No hay archivos temporales o assets innecesarios del wget

---

## Para la sesión en vivo

Lo que te van a pedir con mayor probabilidad:

**"Explica por qué elegiste estas dos páginas y no una sola."**
→ Porque el problema real no es el contenido de una página — es que las páginas no están en conversación. El challenge dice `/empresas` pero el sitio no tiene esa URL. Tomé la decisión de trabajar el problema real de arquitectura en lugar de simular una página hipotética.

**"¿Cómo validarías que estos cambios funcionaron?"**
→ Search Console para impresiones y CTR en queries con "tarjeta empresarial". Google Analytics para bounce rate y páginas por sesión en usuarios que entraron por `/products/corporate-card`. Comparar 30 días antes vs 30 días después del cambio.

**"¿Por qué cambiaste 'corporativa' por 'empresarial'?"**
→ Google Trends con exportación CSV de los últimos 12 meses muestra que "tarjeta empresarial" supera consistentemente a "tarjeta corporativa" en México y Colombia. No es una opinión — es un dato. La estrategia no es eliminar "corporativa" del sitio sino usar "empresarial" como keyword primario en los elementos de mayor peso SEO (title, H1) y dejar "corporativa" como señal semántica secundaria en el cuerpo.

**"Muéstrame el FAQ schema que implementaste."**
→ Abrir `after/corporate-card.html`, buscar `application/ld+json`, explicar cada campo y por qué esas preguntas específicas.

**"¿Qué harías diferente si tuvieras más tiempo?"**
→ Construir la página de plataforma / "cómo funciona" que describe el lifecycle completo del gasto — esa es la pieza que más falta en el sitio y la que más impacto tendría en GEO. También trabajaría el `llms.txt` en español y portugués con las correcciones de accuracy que identificamos (Mastercard vs Visa en la respuesta de Perplexity).
