# Roadmap de ejecución — Clara SEO Challenge

---

## Estado actual (mayo 2026 — iteración 2 completada)

| Part | Documento | Estado |
|---|---|---|
| A | `part-a/audit.md` | ✅ En repo |
| B | `part-b/keyword-strategy.md` | ✅ En repo |
| C | `part-c/geo-ai-search.md` | ✅ En repo |
| D | `part-d/before/` + `part-d/after/` + `part-d/notes.md` | ✅ En repo |
| — | `README.md` | ✅ En repo |
| — | Webflow MCP setup (`.mcp.json`, `CLAUDE.md`, `context/`) | ✅ En repo |
| — | Webflow demo publicado | ✅ Live en `clara-seo-challenge.webflow.io` |

### Webflow demo — estado publicado

**corporate-card** (`/corporate-card`):
- Navbar Clara (componente global) ✅
- Hero con H1 correcto ✅
- Stats bar ✅
- Logos strip — 11 clientes con CSS background-image ✅
- Features grid ✅
- Diferenciadores ✅
- FAQ accordion ✅
- Interlinking → small-business ✅
- CTA final ✅
- Footer Clara (componente global) — logo blanco, 3 awards, 4 columnas, App Store + Google Play ✅
- SEO: title, meta description (sin "sin aval"), canonical, hreflang, FAQ schema JSON-LD ✅

**small-business** (`/small-business`):
- Navbar Clara (componente global) ✅
- Hero sin "sin aval" en copy y meta description ✅
- Logos strip — 11 clientes ✅
- Perfil de usuario ✅
- Features grid ("Alta 100% digital" en lugar de "Sin aval ni historial") ✅
- Interlinking → corporate-card ✅
- CTA final ✅
- Footer Clara (componente global) ✅

### Componentes Webflow creados

| Componente | ID | Grupo |
|---|---|---|
| Navbar Clara | `1458fdd9-2ea2-f3f7-2342-cd55a0df2fc4` | Global |
| Footer Clara | `594c8515-0263-6f17-987b-6375305f4759` | Global |

---

## Lo que falta para la entrega final

### Iteración 3 — Polish visual (prioridad alta)

- [ ] **Imágenes hero** — corporate-card y small-business no tienen imagen en el hero. Asset listo: `69fcec93c6b5fa35b5651982` (Corporate credit cards hero img). Insertar con CSS background-image en el hero section.
- [ ] **Responsive** — navbar y footer se ven bien en desktop. Revisar mobile portrait y tablet en Webflow Designer (breakpoints medium, small, tiny).
- [ ] **Open Graph image** (`og:image`) — añadir via Page Settings para ambas páginas. Usar la imagen hero de corporate-card como OG image.
- [ ] **Formulario de registro** — el CTA final tiene un botón pero no un form funcional. Webflow Forms puede capturar leads sin backend.
- [ ] **Navbar dropdowns** — el sitio real tiene dropdowns para Productos, Soluciones, Recursos. El demo tiene links planos. Mejorar si el tiempo lo permite.

### Iteración 3 — Fixes de compliance (bloqueante)

- [ ] **"sin aval" en copy de corporate-card** — verificar que no quede ninguna instancia en el canvas. Buscar en el FAQ accordion y secciones de diferenciadores.
- [ ] **hreflang como HTML estático** — actualmente se inyecta via JS custom code. Mover a Page Settings > SEO para que funcione como HTML nativo.

### Para la sesión siguiente — cómo retomar

1. Abrir Webflow Designer en `clara-seo-challenge.webflow.io`
2. Verificar que el MCP está corriendo: `npx mcp-remote http://localhost:1339/sse`
3. Leer este archivo + `part-d/notes.md` sección "Lo que falta"
4. Leer `context/style-guide.md` y `context/framework-principles.md` antes de tocar el canvas
5. Usar el skill `designer-tools` para cualquier operación de canvas

**Contexto crítico para la siguiente sesión:**
- Site ID Webflow: `69f57ff4021a4f2250a9fbd4`
- corporate-card page ID: `69f592e365ffb17eb53e7488`
- small-business page ID: `69fc967c3d0867342deac6eb`
- Navbar Clara component ID: `1458fdd9-2ea2-f3f7-2342-cd55a0df2fc4`
- Footer Clara component ID: `594c8515-0263-6f17-987b-6375305f4759`
- Las imágenes DEBEN insertarse con CSS `background-image` en divs contenedores — los elementos `<img>` (imgraw en Webflow) no persisten el `src` en el modelo de datos y no renderizan en publish.
- Los assets del proyecto CDN: `https://cdn.prod.website-files.com/69f57ff4021a4f2250a9fbd4/`

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
