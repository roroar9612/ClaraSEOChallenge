# SEO Implementation — Clara SEO Challenge

**Proyecto:** Clara SEO Challenge  
**Sitio demo:** `clara-seo-challenge.webflow.io`  
**Última actualización:** 2026-05-08

---

## 1) Alcance y trazabilidad

Este documento resume la implementación de SEO ejecutada en Webflow y su conexión directa con:

- `part-a/audit.md` (diagnóstico técnico + on-page)
- `part-b/keyword-strategy.md` (arquitectura de contenido e intención de búsqueda)
- `part-d/notes.md` (cambios aplicados en páginas)

---

## 2) Problemas detectados (Part A)

Los cambios se priorizaron para corregir tres fallas base:

1. Señales de localización/indexación incompletas (`hreflang` y `canonical` relativos).
2. Ausencia de schema estructurado en páginas críticas.
3. Mensaje on-page orientado a tagline y no a intención de búsqueda.

También se confirmó un problema estructural de navegación: páginas con poco interlinking entre etapa de descubrimiento, evaluación y decisión.

---

## 3) Principios aplicados (Part B)

La implementación sigue la arquitectura narrativa propuesta en Part B:

- Resolver primero la base técnica para que Google interprete bien idioma/versión/canonical.
- Optimizar páginas transaccionales con vocabulario de demanda real por mercado.
- Evitar páginas aisladas: cada página debe conducir a la siguiente etapa del journey.

---

## 4) Cambios implementados (Part D)

### A. Señales técnicas SEO

- Corrección de `hreflang` y `canonical` con URLs absolutas en páginas objetivo.
- Corrección semántica de jerarquía de headings (segundo `h1` -> `h2`).
- Implementación de `FAQPage` en JSON-LD en página de producto con FAQ visible.

### B. Optimización on-page

- Reescritura de `title`, `meta description` y headings principales con intención transaccional.
- Alineación de `og:title` y `twitter:title` con el title final.
- Ajustes de copy para reforzar diferenciadores reales del producto.

### C. Arquitectura de navegación

- Interlinking bidireccional entre `corporate-card` y `small-business`.
- Refuerzo de módulos de prueba social para mejorar escaneabilidad en evaluación de fit.

---

## 5) Matriz de decisión (análisis -> implementación)

| Decisión | Soporte en Part A | Soporte en Part B | Implementación |
|---|---|---|---|
| `hreflang`/`canonical` absolutos | Hallazgo técnico de localización inconsistente | Base técnica previa a expansión de contenido | Aplicado en páginas objetivo (`part-d/notes.md`) |
| Title/meta orientados a intención | Hallazgo on-page: etiquetas no alineadas a query real | Estrategia por momentos de búsqueda | Actualización de metadatos en páginas transaccionales |
| `h1` duplicado -> `h2` | Hallazgo semántico | Claridad temática por URL | Cambio de tag sin alterar estilo visual |
| `FAQPage` JSON-LD | Ausencia de datos estructurados | Mejor cobertura en momento de evaluación | Script JSON-LD en `head` |
| Interlinking entre páginas clave | Problema estructural de navegación | Journey sin dead ends | CTAs narrativas cruzadas |

---

## 6) Limitaciones conocidas

- **Webflow Designer API (`DynamoWrapper`):** no permite poblar templates CMS hijos de forma programática en este flujo.
  - **Workaround aplicado:** estructura estática con contenido real, pendiente de binding manual en Designer.
- **Scripts vía MCP:** pueden no reflejarse visualmente en el panel de Custom Code aunque sí estén registrados.
- **Enterprise-only features:** ciertas configuraciones avanzadas de robots/sitemap no están disponibles en este entorno.

---

## 7) Estado del avance

- Base técnica SEO: **corregida** en páginas objetivo.
- On-page transaccional: **actualizado**.
- Interlinking principal: **implementado**.
- Publicación final: **pendiente de confirmación**.

---

## 8) Validación sugerida post-publicación

- Search Console: impresiones/CTR de consultas con `tarjeta empresarial`.
- Search Console + Rich Results Test: cobertura y elegibilidad de `FAQPage`.
- GA4: rebote y páginas por sesión en landings orgánicas de producto.
- Seguimiento sugerido: corte a 2, 4 y 8 semanas.
