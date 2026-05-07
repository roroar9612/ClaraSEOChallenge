# Clara — Technical Challenge: Website Specialist (SEO)

## Approach

El challenge pedía un quick win sobre una página hipotética `/empresas`. Esa URL no existe en el sitio real. La decisión fue trabajar el problema real de arquitectura: el sitio tiene dos páginas que deberían estar en conversación y no lo están.

`/products/corporate-card` responde "¿qué es el producto?" y `/solutions/small-business` responde "¿es para una empresa como la mía?" — pero ninguna lleva a la otra. El usuario que llega por búsqueda orgánica aterriza en una, no recibe dirección hacia el siguiente paso de su journey, y sale sin convertir.

El argumento central de este trabajo no es SEO técnico — es arquitectura narrativa. El SEO es el resultado de que las páginas tengan sentido como un journey, no como destinos aislados.

## Toolchain y división de responsabilidades

Este trabajo usa tres herramientas especializadas en roles distintos. Esa separación no fue arbitraria — refleja cómo funciona el trabajo real de SEO técnico en producción.

**Stackoptic** — auditoría técnica de entrada. Antes de escribir una línea de recomendaciones, Stackoptic generó un análisis estructurado del estado real del sitio: hreflang, schema markup, Core Web Vitals, accesibilidad (WCAG), señales de localización, y madurez del marketing tech stack. Sus hallazgos forman la evidencia técnica de la Parte A. Sin este paso, las recomendaciones serían intuiciones, no diagnósticos.

**Cursor** — audits de código. Las páginas `before/` y `after/` de la Parte D fueron revisadas en Cursor para verificar que los cambios fueran semánticamente correctos, que el JSON-LD del FAQ schema estuviera bien formado, y que no se introdujeran regresiones técnicas. Cursor actúa como el segundo par de ojos que garantiza que lo que se propone es implementable y está libre de errores.

**Claude Code + Webflow MCP (Designer)** — construcción del demo visual. En lugar de clonar páginas con `wget`, Claude Code se conecta directamente al sitio de Clara en producción a través del MCP de Webflow Designer. Esto permite trabajar sobre la estructura real del sitio — no sobre una copia estática con assets rotos — y producir un demo `after/` que refleje fielmente cómo se verían los cambios en producción. Claude Code hace el build; Cursor audita el resultado.

## Assumptions

- `/empresas` no existe como URL real en clara.com. La intervención trabaja sobre las dos URLs equivalentes que sí existen.
- Los datos de keyword volume son de Google Trends (exportación CSV, últimos 12 meses, México y Colombia). "Tarjeta empresarial" supera consistentemente a "tarjeta corporativa" — el cambio en title/H1 está basado en datos, no en opinión.
- Las métricas de "30,000 empresas" aparecen en el copy del sitio real; se usan como prueba social en la meta description.
- **Hreflang:** Stackoptic confirma implementación correcta en la homepage global (score 10/10, con `x-default`). El problema real está en las páginas internas, donde los atributos `hreflang` y `canonical` usan URLs relativas en lugar de absolutas — esto es lo que Google no puede resolver.
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
│   └── framework-principles.md        ← convenciones Webflow del sitio real
├── part-a/
│   └── audit.md                       ← auditoría SEO completa
├── part-b/
│   └── keyword-strategy.md            ← estrategia de keywords y arquitectura de contenido
├── part-c/
│   └── geo-ai-search.md               ← baseline GEO y propuesta para AI search
└── part-d/
    ├── before/                        ← estado actual del sitio (vía Webflow MCP)
    │   └── www.clara.com/es-mx/...
    ├── after/                         ← versiones mejoradas con los cambios implementados
    │   ├── corporate-card.html
    │   └── small-business.html
    └── notes.md                       ← hipótesis, cambios documentados y métricas de validación
```

## Part A — SEO Audit

El hallazgo más importante no fue técnico: fue que el sitio tiene baja densidad de contenido orientado a intención de búsqueda. Las páginas de producto son mayoritariamente visuales — copy corto, features listadas, sin responder las preguntas reales del prospecto.

Los bugs técnicos más graves, confirmados con Stackoptic, fueron tres: hreflang con URLs relativas en páginas internas (lo que impide que Google resuelva la señal de localización para México y Colombia); ausencia total de structured data local — sin `Organization`, sin `FAQPage`, sin `BreadcrumbList` (score 0/100 en schema); y el atributo `html lang="en-US"` en todas las versiones del sitio, incluyendo las páginas en español y portugués.

## Part B — Keyword Strategy & Content Architecture

La decisión más importante fue reemplazar "corporativa" por "empresarial" como keyword primaria. Google Trends muestra una ventaja consistente para "empresarial" en México y Colombia. En Colombia, "tarjeta corporativa" tiene volumen cercano a cero. Más importante: se identificó una página estructuralmente ausente — la página de "cómo funciona" / lifecycle del gasto — que es la pieza que más falta en el sitio y la que más impacto tendría tanto en SEO como en GEO.

## Part C — GEO / AI Search

ChatGPT, Perplexity y Google AI Overviews mencionan a Clara con información inconsistente: algunos modelos la identifican como emisora Visa cuando opera en la red Mastercard. El baseline muestra que Clara aparece en respuestas de AI search pero sin control sobre el framing. La propuesta es un `llms.txt` en español y portugués con los hechos clave verificables, y una página de "cómo funciona" que los modelos puedan citar con precisión.

## Part D — Quick Win

Se trabajaron dos páginas en lugar de una porque el problema real no era el contenido de una página — era que las páginas no estaban en conversación. El `before/after` demuestra dos cosas simultáneamente: corrección de bugs técnicos (hreflang relativo, H1 duplicado, FAQ sin schema) y arquitectura narrativa (interlinking, sección de diferenciadores, perfil de usuario).

Las páginas `before/` se obtuvieron directamente desde Webflow Designer vía MCP — no copias estáticas con assets rotos, sino la estructura real del sitio en producción. Los cambios en `after/` fueron construidos por Claude Code y auditados en Cursor antes del commit.

### Cambios implementados (resumen)

**corporate-card.html:**
- hreflang `es-MX` y canonical → URLs absolutas (bug técnico confirmado por Stackoptic)
- Title: "Tarjeta Empresarial para Empresas en México | Clara"
- Meta description con "sin aval" y prueba social
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

| Herramienta | Rol en este trabajo |
|---|---|
| **Stackoptic** | Auditoría técnica automatizada — hreflang, schema, WCAG, Core Web Vitals, marketing tech stack |
| **SEMrush** | Tráfico orgánico estimado, análisis de caída (235,528 visitas, abril 2026, −11%) |
| **Google Trends** | Exportación CSV 12 meses por país — evidencia del gap "empresarial" vs "corporativa" |
| **Browser DevTools + view-source** | Verificación manual de implementación de hreflang, canonical y structured data |
| **Claude Code + Webflow MCP (Designer)** | Conexión al sitio real en producción, construcción del demo `after/` |
| **Cursor** | Audits de código — validación semántica, JSON-LD, revisión de regresiones en `before/after/` |
| **ChatGPT / Perplexity / Gemini** | GEO baseline testing — presencia, posición y accuracy de información atribuida a Clara |

## Para retomar este trabajo

Ver `CLAUDE.md` para el setup del Webflow MCP y el estado de la construcción del demo visual.  
Ver `ROADMAP.md` para el checklist completo de lo que está hecho y lo que falta.

**Estado actual (mayo 2026):**
- Parts A, B, C: documentos completos en sus carpetas
- Part D: `before/` y `after/` implementados, `notes.md` completo
- Webflow MCP: configurado, conectado vía Designer MCP al sitio real de Clara
- Cursor: configurado para audits en `.cursor/`
- README: completo
