# Clara — Technical Challenge: Website Specialist (SEO)

## Approach

El challenge pedía un quick win sobre una página hipotética `/empresas`. Esa URL no existe en el sitio real. La decisión fue trabajar el problema real de arquitectura: el sitio tiene dos páginas que deberían estar en conversación y no lo están.

`/products/corporate-card` responde "¿qué es el producto?" y `/solutions/small-business` responde "¿es para una empresa como la mía?" — pero ninguna lleva a la otra. El usuario que llega por búsqueda orgánica aterriza en una, no recibe dirección hacia el siguiente paso de su journey, y sale sin convertir.

El argumento central de este trabajo no es SEO técnico — es arquitectura narrativa. El SEO es el resultado de que las páginas tengan sentido como un journey, no como destinos aislados.

## Assumptions

- `/empresas` no existe como URL real en clara.com. La intervención trabaja sobre las dos URLs equivalentes que sí existen.
- Los datos de keyword volume son de Google Trends (exportación CSV, últimos 12 meses, México). "Tarjeta empresarial" supera consistentemente a "tarjeta corporativa" — el cambio en title/H1 está basado en datos, no en opinión.
- Las métricas de "30,000 empresas" aparecen en el copy del sitio real; se usan como prueba social en la meta description.
- Los cambios de `after/` son implementables en producción directamente en Webflow (Custom Code para head, canvas para contenido). No requieren acceso al repositorio de código del equipo.

## Structure

```
clara-seo-challenge/
├── README.md                          ← este archivo
├── CLAUDE.md                          ← configuración del agente Webflow MCP
├── ROADMAP.md                         ← estado de ejecución y checklist
├── .mcp.json                          ← servidor MCP de Webflow (Claude Code)
├── .claude/
│   └── settings.json                  ← permisos y plugins del agente
├── context/
│   ├── style-guide.md                 ← tokens de color, tipografía y clases de Clara
│   └── framework-principles.md       ← convenciones Webflow del sitio real
├── part-a/
│   └── audit.md                       ← auditoría SEO completa
├── part-b/
│   └── keyword-strategy.md            ← estrategia de keywords y arquitectura de contenido
├── part-c/
│   └── geo-ai-search.md               ← baseline GEO y propuesta para AI search
└── part-d/
    ├── before/                        ← páginas clonadas con wget (estado actual del sitio)
    │   └── www.clara.com/es-mx/...
    ├── after/                         ← versiones mejoradas con los cambios implementados
    │   ├── corporate-card.html
    │   └── small-business.html
    └── notes.md                       ← hipótesis, cambios documentados y métricas de validación
```

## Part A — SEO Audit

El hallazgo más importante no fue técnico: fue que el sitio tiene baja densidad de contenido orientado a intención de búsqueda. Las páginas de producto son mayoritariamente visuales — copy corto, features listadas, sin responder las preguntas reales del prospecto. El bug técnico más grave fue el hreflang `es-MX` con URL relativa en todas las páginas del dominio, lo que hace que Google no pueda resolver la señal de localización para México.

## Part B — Keyword Strategy & Content Architecture

La decisión más importante fue reemplazar "corporativa" por "empresarial" como keyword primaria. Google Trends muestra una ventaja consistente para "empresarial" en México y Colombia. Más importante: se identificó una página estructuralmente ausente — la página de "cómo funciona" / lifecycle del gasto — que es la que más falta en el sitio y la que más impacto tendría tanto en SEO como en GEO.

## Part C — GEO / AI Search

ChatGPT, Perplexity y Google AI Overviews mencionan a Clara con información inconsistente: algunos modelos la identifican como emisora Visa cuando es Mastercard. El baseline muestra que Clara aparece en respuestas de AI search pero sin control sobre el framing. La propuesta es un `llms.txt` en español y portugués con los hechos clave verificables, y una página de "cómo funciona" que los modelos puedan citar con precisión.

## Part D — Quick Win

Se trabajaron dos páginas en lugar de una porque el problema real no era el contenido de una página — era que las páginas no estaban en conversación. El `before/after` demuestra dos cosas simultáneamente: corrección de bugs técnicos (hreflang relativo, H1 duplicado, FAQ sin schema) y arquitectura narrativa (interlinking, sección de diferenciadores, perfil de usuario).

### Cambios implementados (resumen)

**corporate-card.html:**
- hreflang `es-MX` y canonical → URLs absolutas (bug técnico)
- Title: "Tarjeta Empresarial para Empresas en México | Clara"
- Meta description con diferenciadores y prueba social
- H1: "La tarjeta empresarial que escala con tu equipo"
- Segundo H1 → `<h2>` (corrección semántica, cero riesgo visual)
- FAQ schema JSON-LD (8 preguntas → rich results habilitados)
- Sección nueva "Lo que tu banco no puede darte"
- Interlinking narrativo hacia `/small-business`

**small-business.html:**
- hreflang + canonical → URLs absolutas
- Title: "Tarjeta Empresarial para PyMEs en México | Clara"
- H1 orientado al dolor del usuario
- Sección de perfil "Hecha para equipos que están escalando"
- Interlinking de regreso hacia `/corporate-card`

Ver `part-d/notes.md` para la justificación detallada de cada cambio y las métricas de validación.

## Tools used

- Browser DevTools + view-source
- Google Trends (exportación CSV, últimos 12 meses, México y Colombia)
- SEMrush (tráfico orgánico estimado)
- wget (clonado de páginas con assets relativos convertidos)
- Python 3 (extracción de tokens del CSS vivo, aplicación de cambios en after/)
- Claude Code + Webflow MCP (construcción del demo visual en Webflow)
- ChatGPT / Perplexity (GEO baseline testing)

## Descargar assets de una página

Se agregó el script `scripts/download-assets.sh` para clonar una URL y descargar sus assets útiles (CSS, JS, imágenes y fuentes) con `wget`.

```bash
# URL por defecto: https://www.clara.com/es-mx/products/corporate-card
./scripts/download-assets.sh

# URL y carpeta custom
./scripts/download-assets.sh "https://www.clara.com/es-mx/products/corporate-card" "downloads/corporate-card"
```

El resultado queda dentro de `downloads/` (o la carpeta que indiques).

Para aislar solo las imágenes y preparar una carpeta limpia para subirlas a Webflow con drag and drop:

```bash
./scripts/prepare-webflow-images.py "downloads/corporate-card" "downloads/webflow-images"
```

Esto copia las imágenes a `downloads/webflow-images/` y genera `downloads/webflow-images/manifest.csv` con ruta original, extensión y texto alt sugerido.

## Auditar páginas publicadas en Webflow

Para correr una auditoría completa en una sola pasada sobre las páginas del demo publicado:

```bash
./scripts/audit-webflow-pages.py
```

El reporte se genera en `reports/webflow-full-published-audit.md` e incluye SEO metadata, canonical/hreflang, JSON-LD, headings, links, imágenes y señales básicas de accesibilidad.

También puedes pasar URLs custom:

```bash
./scripts/audit-webflow-pages.py \
  "https://clara-seo-challenge.webflow.io/corporate-card" \
  "https://clara-seo-challenge.webflow.io/small-business" \
  --output "reports/webflow-full-published-audit.md"
```

## Para retomar este trabajo

Ver `CLAUDE.md` para el setup del Webflow MCP y el estado de la construcción del demo visual.  
Ver `ROADMAP.md` para el checklist completo de lo que está hecho y lo que falta.

**Estado actual (mayo 2026 — iteración 2 publicada):**
- Parts A, B, C: documentos completos en sus carpetas
- Part D: `before/` y `after/` implementados, `notes.md` completo
- Webflow demo: publicado en `clara-seo-challenge.webflow.io`
  - `/corporate-card`: navbar, logos strip (11 clientes), 7 secciones, footer — todos los assets renderizando
  - `/small-business`: mismos componentes globales, copy sin referencias a "sin aval"
  - Navbar y Footer convertidos a **componentes reutilizables** en Webflow
- Git: en repo, rama `main`

Ver `ROADMAP.md` para el checklist detallado de lo hecho y lo pendiente (iteración 3).
