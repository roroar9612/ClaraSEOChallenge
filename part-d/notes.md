# Part D — SEO Quick Win: Tarjeta Corporativa + PyMEs Clara

## Decisión de alcance

El challenge pedía `/empresas`. Esa URL no existe en el sitio real. La decisión fue trabajar el problema real de arquitectura entre dos páginas que sí existen y que deberían estar en conversación:

- `/es-mx/products/corporate-card` → responde "¿qué es el producto?"
- `/es-mx/solutions/small-business` → responde "¿es para una empresa como la mía?"

Ninguna llevaba a la otra. El `before/` documenta ese estado. El `after/` implementa el journey completo.

---

## Cambios implementados — corporate-card.html

### 1. hreflang `es-MX` y canonical — corrección de URL relativa
**Antes:** `href="corporate-card.html"`
**Después:** `href="https://www.clara.com/es-mx/products/corporate-card"`
**Por qué:** Google no puede resolver URLs relativas en hreflang. Esta configuración hace que la versión mexicana de la página no reciba la señal de localización correcta, lo que afecta el ranking en búsquedas desde México. El canonical relativo tiene el mismo problema: sin URL absoluta, Google no puede consolidar señales de link equity hacia la URL canónica.

### 2. Title tag — keyword primaria
**Antes:** "Tarjeta Corporativa: Emisión Inmediata | Clara"
**Después:** "Tarjeta Empresarial para Empresas en México | Clara"
**Por qué:** Google Trends (últimos 12 meses, México) muestra que "tarjeta empresarial" supera consistentemente a "tarjeta corporativa" en volumen de búsqueda. "Emisión Inmediata" es copy de conversión, no un modificador con demanda de búsqueda real. El nuevo title incorpora el modificador geográfico "en México", que captura búsquedas transaccionales de alta intención.

### 3. Meta description — orientada a diferenciadores
**Antes:** Lista de features (emisión al instante, conciliación, SAT)
**Después:** Incluye "sin aval", beneficio por empleado, prueba social ("30,000 empresas")
**Por qué:** La descripción anterior no diferenciaba Clara de un banco tradicional. "Sin aval" es el diferenciador más poderoso de Clara y ningún banco puede ofrecer eso. Incluirlo en el snippet aumenta el CTR de usuarios en evaluación activa.

### 4. og:title + twitter:title — consistencia
Actualizados para coincidir con el nuevo `<title>`. El copy compartido en redes tiene que reflejar el mismo posicionamiento.

### 5. H1 hero — keyword + diferenciador de equipo
**Antes:** "Tarjeta de crédito empresarial para crecer con control"
**Después:** "La tarjeta empresarial que escala con tu equipo"
**Por qué:** Mantiene el keyword primario "empresarial", elimina el tagline genérico "para crecer con control", e introduce "equipo" — término que aparece en queries transaccionales como "tarjeta empresarial para empleados".

### 6. Segundo H1 → H2 — corrección semántica
**Antes:** `<h1 class="fbl-heading-h1-17">Acelera tu crecimiento con Clara</h1>`
**Después:** `<h2 class="fbl-heading-h1-17">Acelera tu crecimiento con Clara</h2>`
**Por qué:** Una página no debe tener dos H1. La clase Webflow `fbl-heading-h1-17` controla el estilo visual, no la semántica — el cambio de tag es cero riesgo visual.

### 7. FAQ schema — JSON-LD
**Antes:** 8 preguntas en el DOM (ya existentes) sin marcado estructurado
**Después:** Bloque `FAQPage` en JSON-LD con las 8 preguntas del accordion + 4 preguntas adicionales sobre diferenciadores clave (aval, integraciones, control de gastos)
**Por qué:** El schema FAQPage habilita rich results en SERP (preguntas expandibles debajo del snippet), lo que aumenta el CTR orgánico sin modificar el contenido visible. Las preguntas adicionales sobre "sin aval" e integraciones capturan búsquedas informacionales que preceden a la intención de compra.

### 8. Sección "Lo que tu banco no puede darte"
Nueva sección de contenido insertada antes del FAQ accordion.
**Por qué:** Captura búsquedas de alta intención como "tarjeta corporativa sin aval" y "tarjeta empresarial sin historial crediticio" — términos que describen el diferenciador principal de Clara y que ninguna página del sitio trabajaba explícitamente.

### 9. Interlinking hacia small-business
Nueva sección con CTA antes del formulario de registro final.
**Por qué:** Un usuario que llegó a `/corporate-card` por búsqueda orgánica no tiene señal de que existe una página diseñada específicamente para su tamaño de empresa. El interlinking narrativo ("¿Es Clara para una empresa como la tuya?") guía al usuario al siguiente paso del journey sin interrumpir la conversión.

---

## Cambios implementados — small-business.html

### 1. hreflang `es-MX` y canonical — mismo bug que corporate-card
Corregidos a URLs absolutas.

### 2. Title tag
**Antes:** "Soluciones para PyMEs | Clara"
**Después:** "Tarjeta Empresarial para PyMEs en México | Clara"
**Por qué:** El title anterior no tenía keyword de búsqueda. "PyMEs" sola no captura intención de compra. El nuevo title conecta con queries como "tarjeta empresarial para pymes México".

### 3. H1 — orientado a dolor, no a categoría
**Antes:** "Gestión financiera simple para PyMEs en crecimiento"
**Después:** "El control de gastos que tu PyME necesitaba desde el día uno"
**Por qué:** El H1 anterior describe una categoría de producto. El nuevo describe el estado deseado del usuario y crea urgencia narrativa.

### 4. Sección "Hecha para equipos que están escalando"
Perfil del usuario real insertado después del H1.
**Por qué:** La página no tenía un párrafo que le dijera al visitante "esto es para ti". La sección de perfil reduce el bounce rate de usuarios que necesitan confirmación de fit antes de explorar features.

### 5. Interlinking de regreso hacia corporate-card
**Por qué:** Cierra el loop del journey. Un usuario que exploró `/small-business` y aún no está convencido puede profundizar en los detalles del producto desde `/corporate-card` sin salir del sitio.

---

## Hipótesis SEO principal

La ausencia de interlinking entre páginas de producto y páginas de solución crea journeys incompletos que aumentan el bounce rate y reducen el tiempo en el sitio — señales negativas para rankings. Conectar las dos páginas narrativamente debería reducir el bounce rate y aumentar páginas por sesión en usuarios que entran por búsqueda orgánica.

---

## Métricas de validación

| Métrica | Fuente | Ventana |
|---|---|---|
| Impresiones y posición media para "tarjeta empresarial" | Search Console > Rendimiento > Consultas | 30–60 días post-despliegue |
| Errores de hreflang es-MX | Search Console > Internacional | 2–4 semanas |
| Rich results FAQ activos | Search Console > Mejoras > Preguntas frecuentes | 2–4 semanas |
| Bounce rate de ambas páginas | Google Analytics | 30 días |
| Páginas por sesión (entrada por /corporate-card) | Google Analytics > Rutas de exploración | 30 días |
| CTR orgánico para queries "tarjeta empresarial PyME" | Search Console | 30–60 días |

---

## Limitación técnica — Webflow

Estos cambios viven en el repo. En producción, deben implementarse directamente en el editor de Webflow (Custom Code en página) o vía Webflow Data API para que una republicación desde el CMS no sobreescriba las modificaciones. Los cambios de contenido (H1, nuevas secciones) requieren edición en el canvas de Webflow — no se pueden inyectar solo con custom code.

---

## Implementación en Webflow — Iteración 1 (mayo 2026)

**Sitio:** `clara-seo-challenge.webflow.io`
**Site ID:** `69f57ff4021a4f2250a9fbd4`

### Páginas construidas

**Corporate Card** (`/corporate-card`, page ID `69f592e365ffb17eb53e7488`)
7 secciones: hero navy → stats bar teal → features grid 2×2 → "Lo que tu banco no puede darte" → FAQ accordion 8 preguntas → interlinking → CTA final navy.

**Small Business** (`/small-business`, page ID `69fc967c3d0867342deac6eb`)
5 secciones: hero navy → perfil de usuario → features grid PyME → interlinking hacia corporate-card → CTA final navy.

### Scripts aplicados (Webflow Scripts API)

| Script ID | Versión | Página | Contenido |
|---|---|---|---|
| `claraccfaqschema` | 1.0.1 | corporate-card | FAQ JSON-LD (4 preguntas sobre aval, tarjetas, control de gastos, integraciones) |
| `claraccseolinks` | 1.0.0 | corporate-card | canonical + hreflang es-MX inyectados via JS |
| `clarasbseolinks` | 1.0.0 | small-business | canonical + hreflang es-MX inyectados via JS |

### Limitaciones encontradas en la API

- **Scripts API no acepta HTML arbitrario:** Canonical y hreflang son `<link>` tags — no se pueden inyectar como HTML estático vía la API. Se inyectan via JS (`document.createElement('link')`). Para producción real: Page Settings → Custom Code → Head.
- **Atributos de script requieren prefijo `data-`:** No se puede pasar `type="application/ld+json"` como atributo nativo. El FAQ schema se crea dinámicamente con JS (`s.type = 'application/ld+json'`).
- **`whtml_builder` no acepta Body como parent directo:** Se necesita una Section intermedia creada con `element_builder`. Descubierto en la primera iteración.

### Lo que falta (iteración 2+)

- [ ] Navbar y footer — las páginas no tienen navegación global
- [ ] Formulario de registro funcional (Webflow Form con integración CRM)
- [ ] Imágenes y assets visuales (hero image, feature icons)
- [ ] Responsive refinement — tipografía y grid en mobile/tablet
- [ ] Open Graph images por página (`og:image`)
- [ ] Sitemap.xml y robots.txt
- [ ] Variables CSS del sistema de diseño Clara (tokens de color y tipografía)
- [ ] Canonical/hreflang como HTML estático (no JS) vía Page Settings
- [ ] A/B testing setup para validar hipótesis de H1
