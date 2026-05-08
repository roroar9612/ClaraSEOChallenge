# Execution Roadmap — Clara SEO Challenge

---

## Current Status (May 8, 2026)

| Part | Document | Status |
|---|---|---|
| A | `part-a/audit.md` | ✅ Complete |
| B | `part-b/keyword-strategy.md` | ✅ Complete |
| C | `part-c/geo-ai-search.md` | ✅ Complete |
| D | `part-d/before/` + `part-d/after/` + `part-d/notes.md` | ✅ Complete |
| — | `README.md` | ✅ Complete |
| — | Webflow demo | ✅ Live at `clara-seo-challenge.webflow.io` (unpublished changes pending) |

---

## Webflow Demo — Real Current State

> ⚠️ **Fuente de verdad: el Designer de Webflow, no estos archivos.**
> Los .md reflejan el estado conocido al momento del último sync. Siempre hacer `get_all_elements` al inicio de sesión para verificar estado real.

**Site URL:** `clara-seo-challenge.webflow.io`
**Site ID:** `69f57ff4021a4f2250a9fbd4`

### Pages

| Page | Slug | Webflow Page ID | Last Updated |
|---|---|---|---|
| Corporate Card | `/corporate-card` | `69f592e365ffb17eb53e7488` | 2026-05-08T01:58 UTC |
| Empresas (formerly Small Business) | `/empresas` | `69fc967c3d0867342deac6eb` | 2026-05-08T04:49 UTC |
| Como Funciona | `/como-funciona` | `69fd2816de8f795304411f79` | 2026-05-08T00:04 UTC |

**Last published:** 2026-05-08T02:02 UTC
**Unpublished changes:** Corporate Card + Empresas (visual rescue, copy updates, social-proof expansion, script/motion adjustments)

### Reusable Components

| Component | Webflow Component ID |
|---|---|
| Navbar Clara | `1458fdd9-2ea2-f3f7-2342-cd55a0df2fc4` |
| Footer Clara | `594c8515-0263-6f17-987b-6375305f4759` |
| Logos Strip Clara | `049962a7-2787-8d6e-e9ce-adf1c6f85c28` |
| Interlink CTA Clara | `6c61e216-0c09-92b4-9e15-9eb852931b76` |
| CTA Section Clara | `984f67a6-1aa0-a134-ecc1-1449fbd20b3e` |

---

### Sections — `/corporate-card`

1. ✅ **Hero** — H1 "La tarjeta empresarial que escala con tu equipo", lead "Crédito a nombre de tu empresa. Tarjetas ilimitadas con controles individuales por empleado.", CTA "Regístrate gratis" + "Ver cómo funciona", social proof inline ("2K tarjetas creadas / 1M+ transacciones por minuto"), hero image vía CSS background
2. ✅ **KPIs** — H2 "Controles de tarjeta para que Finanzas se concentre donde más importa", stats: +180M pesos ahorrados, +30% deducciones fiscales, +156h ahorradas/año
3. ✅ **Logos strip** — "30,000 empresas confían en Clara" (componente `049962a7`)
4. ✅ **Features** — H2 "Para equipos financieros que ponen el foco donde más importa", 5 features: Reembolsos centralizados, Aprobaciones personalizadas, Control de tarjetas, Deducción fiscal automática, Integración con ERP + mockup finops
5. ✅ **"Lo que tu banco no puede darte"** — diferenciadores con imagen dark cards
6. ✅ **FAQ accordion** — 6 preguntas con H2 "¿Tienes preguntas?"
7. ✅ **Interlinking** — "¿Tu empresa está creciendo y necesita más control?" → `/empresas`
8. ✅ **CTA final** — formulario con Nombre, Email empresarial, Empresa, Número de empleados
9. ✅ Navbar Clara + Footer Clara (componentes)

### Sections — `/empresas`

1. ✅ **Hero** — H1 "Control financiero para empresas que están creciendo", lead copy, CTA "Regístrate gratis" + "Ver tarjetas Clara", mockup panel de gasto (Gasto mensual $1,546,736 + chips: Tarjetas por equipo, Límites por colaborador, Pagos y gastos visibles)
2. ✅ **Logos strip** — componente `049962a7`
3. ✅ **Casos de uso (editorial cards)** — H2 "Historias reales para mostrar dónde Clara genera valor", grid de tarjetas con caso destacado + casos de apoyo. Empresas integradas: SmartFit, 99 Minutos, MCM Telecom, Runa, Terranova y Truora.
4. ✅ **Perfiles** — "Para empresas que necesitan ordenar su operación financiera", 3 perfiles: Fundadores con operación activa, Equipos financieros pequeños, Empresas en crecimiento
5. ✅ **Features** — "Capacidades para controlar gastos sin frenar a tu equipo", 4 features: Tarjetas para todo el equipo, Reembolsos centralizados, Visibilidad en tiempo real, Alta 100% digital
6. ✅ **CTA final** — "Empieza a centralizar la operación financiera de tu empresa" (componente `CTA Section Clara`)
7. ✅ **Interlinking** — "Profundiza en las tarjetas Clara para tu equipo" → `/corporate-card` (componente `Interlink CTA Clara`)
8. ✅ Navbar Clara + Footer Clara (componentes)

---

### Scripts registrados en el sitio (15/15 — LÍMITE ALCANZADO)

> ⚠️ El límite de scripts registrados por la API es 15. Está al tope.
> Nuevos scripts JS deben inyectarse como elemento DOM `<script>` vía `whtml_builder`, no como scripts registrados.

| Script ID | Versión | Ubicación | Página |
|---|---|---|---|
| `claracorpseocore` | 1.0.0 | header | corporate-card |
| `claraccfaqschema` | 1.0.1 | header | corporate-card |
| `claraccseolinks` | 1.0.0 | footer | corporate-card |
| `clarafaqclean` | 1.0.0 | — | registrado, sin asignar |
| `clarasmallseocore` | 1.0.0 | header | small-business |
| `claracontentpolish` | 1.0.0 | header | small-business |
| `clarasobermotion` | 1.0.0 | header | small-business |
| `claralogostripmotion` | 1.0.0/1.1.0 | footer | small-business |
| `clarasbseolinks` | 1.0.0 | — | registrado, sin asignar confirmado |
| `clarascrollorchestrator` | 1.0.0 | — | registrado |
| `claraheropremiummotion` | 1.0.0 | — | registrado |
| `clarapremiumvisuals` | 1.0.0 | — | registrado |
| `claramotionquality` | 1.0.0 | — | registrado |
| `claraherocardmotion` | 1.0.0/1.1.0 | — | registrado |

**Tab switcher JS** (`ClaraProofTabs`) — inyectado como DOM embed en Small Business (no como script registrado, por límite).

---

## Iteraciones completadas

### Iteración 1 — Estructura base (mayo 2–5, 2026)
- Ambas páginas construidas en Webflow
- Navbar + Footer como componentes
- SEO head code (canonical, hreflang, meta description) vía Page Settings

### Iteración 2 — Componentes y assets (mayo 5–6, 2026)
- Logos strip convertido a componente
- FAQ schema JSON-LD inyectado en corporate-card
- Hero image de corporate-card subida al CDN (`69fcec93c6b5fa35b5651982`)

### Iteración 3 — Copy, compliance y tipografía (mayo 7, 2026)
- Compliance fix: removido "Sin aval, sin historial previo." de meta small-business
- 10 nodos de texto actualizados en ambas páginas (ver `part-d/notes.md`)
- 43 estilos migrados de Montserrat/Inter → Arial system font
- **Estado: aplicado en Designer, pendiente de publicar**

### Iteración 4 — Motion y scripts (mayo 8, 2026)
- Scripts de motion aplicados a small-business: ClaraSoberMotion, ClaraContentPolish, ClaraLogoStripMotion
- Scripts adicionales registrados (ClaraScrollOrchestrator, ClaraHeroPremiumMotion, ClaraPremiumVisuals, ClaraMotionQuality, ClaraHeroCardMotion) — detalles de aplicación a verificar en Designer
- Sección "Como Funciona" creada como tercera página del sitio

### Iteración 5 — Replanteamiento visual de `/empresas` (mayo 8, 2026)
- La página "Small Business" se consolidó como **`/empresas`** (mismo page ID, nuevo slug)
- Hero de `/empresas` rediseñado con visual de sistema (no duplicar patrón del hero de corporate-card)
- Interlinking consolidado hacia `/corporate-card` para profundidad de producto (Black/White/virtual/wallet)
- Sección de social proof migrada a tarjetas editoriales con contenido real y tono de customer story
- Casos integrados: SmartFit, 99 Minutos, MCM Telecom, Runa, Terranova y Truora
- **Estado: aplicado en Designer, pendiente de publicar**

---

## Pendiente — Iteración 6

- [ ] **Publicar** — correr `/safe-publish` para subir iteraciones 3+4+5+6 a `clara-seo-challenge.webflow.io`
- [ ] **og:image** — Open Graph image en ambas páginas vía Page Settings
- [ ] **hreflang estático** — mover de JS a `<link>` HTML en Page Settings > Custom Code > Head
- [ ] **Responsive review** — navbar y footer a tablet/mobile
- [ ] **Registro form** — conectar formulario de CTA final (Webflow native form)
- [ ] **FAQ costos corporate-card** — agregar Q/A: "¿Cuáles son los costos y comisiones de Clara?" con valores aprobados (Apertura $0, administración $0, White/Virtual $0, Black $5,000 MXN/año, sin costos ocultos)

---

## Critical Context para próxima sesión

### Fuente de verdad
Los .md están siempre desfasados respecto al Designer. Al iniciar sesión:
1. Conectar Designer MCP: `https://clara-seo-challenge.design.webflow.com?app=dc8209c65e3ec02254d15275ca056539c89f6d15741893a0adf29ad6f381eb99`
2. Hacer `get_all_elements` en la página activa para ver el estado real
3. Hacer `get_page_script` para ver qué scripts están aplicados

### Límite de scripts (CRÍTICO)
**15/15 registrados.** Para agregar JS nuevo: inyectar como DOM embed vía `whtml_builder` con `<script>` tag, antes del footer. No intentar `add_inline_site_script` — fallará con `max_scripts_per_block`.

### imgraw limitation
`whtml_builder` convierte `<img>` a `imgraw` — el `src` no se persiste. Siempre usar CSS `background-image` en divs. CDN pattern:
```
https://cdn.prod.website-files.com/69f57ff4021a4f2250a9fbd4/{asset_id}_{filename}
```

### Ghost element pattern
`remove_element` a veces reporta éxito pero el elemento persiste entre sesiones. Verificar con `query_elements` después de cualquier eliminación.

### Compliance (HARD)
Nunca usar "sin aval", "sin historial crediticio", "sin garantías patrimoniales". Usar solo: control de gastos por empleado, conciliación automática SAT, tarjetas ilimitadas, integración ERP, proceso 100% digital.

---

## Para la presentación en vivo

**"¿Por qué trabajaste dos páginas en vez de una?"**
→ El problema real no es el contenido de una página — es que las páginas no están en conversación. El challenge menciona `/empresas` pero esa URL no existe en el sitio real. Elegí trabajar el problema arquitectónico real: ninguna de las dos páginas enlazaba a la otra.

**"¿Cómo validarías que los cambios funcionaron?"**
→ Search Console para impresiones y CTR en queries "tarjeta empresarial". GA4 para bounce rate y páginas/sesión en usuarios que entran por `/products/corporate-card`. Comparar 30 días antes vs 30 días después del deploy.

**"¿Por qué reemplazaste 'corporativa' por 'empresarial'?"**
→ Google Trends (12 meses, México) muestra "tarjeta empresarial" consistentemente por encima de "tarjeta corporativa". La estrategia es coexistencia: "empresarial" ancla los elementos de mayor peso SEO (title, H1, meta), "corporativa" permanece en body copy como señal semántica secundaria.

**"Muéstrame el FAQ schema que implementaste."**
→ Abrir `after/corporate-card.html`, buscar `application/ld+json`. O abrir el demo y ver source. 6 preguntas elegidas por ser las que un director de finanzas buscaría antes de firmar.

**"¿Qué harías diferente con más tiempo?"**
→ Construir la página "cómo funciona" que describe el ciclo completo de gasto. Es la pieza que más falta en el sitio y la de mayor impacto GEO. También escribiría `llms.txt` en español y portugués con las correcciones de precisión identificadas en el baseline (Mastercard vs Visa en la respuesta de Perplexity sobre Clara).
