# SKILL — Clara SEO Challenge: Part D
## Contexto para Claude Code

Lee este documento completo antes de ejecutar cualquier cambio en el repo.

---

## Qué estamos construyendo y por qué

La Part D del challenge pide un "quick win" sobre una página hipotética `/empresas`. La decisión tomada es más ambiciosa y más honesta: en lugar de simular una página que no existe, demostramos el problema real de arquitectura entre dos páginas que sí existen.

**El argumento central:** El sitio de Clara tiene dos páginas que deberían estar en conversación y no lo están. `/products/corporate-card` responde "qué es el producto" y `/solutions/small-business` responde "es para una empresa como la mía" — pero ninguna lleva a la otra. El usuario que llega por búsqueda orgánica aterriza en una de las dos, no recibe dirección hacia el siguiente paso de su journey, y sale sin convertir.

El `before/` documenta ese estado. El `after/` implementa el journey completo: interlinking narrativo, SEO on-page corregido, y una estructura que guía al usuario desde el descubrimiento del producto hasta la evaluación de fit y el registro.

---

## Estructura del repo

```
clara-seo-challenge/
├── README.md
├── part-a/
│   └── audit.md
├── part-b/
│   └── keyword-strategy.md
├── part-c/
│   └── geo-ai-search.md
└── part-d/
    ├── before/
    │   ├── corporate-card.html      ← wget de /es-mx/products/corporate-card
    │   └── small-business.html     ← wget de /es-mx/solutions/small-business
    ├── after/
    │   ├── corporate-card.html     ← versión mejorada con SEO + interlinking
    │   └── small-business.html    ← versión mejorada con narrativa + interlinking
    └── notes.md                    ← hipótesis SEO y métricas de validación
```

---

## Paso 1 — Clonar las páginas (before/)

Ejecutar desde la raíz del repo:

```bash
wget --mirror \
     --convert-links \
     --adjust-extension \
     --no-parent \
     --page-requisites \
     -P part-d/before/ \
     https://www.clara.com/es-mx/products/corporate-card

wget --mirror \
     --convert-links \
     --adjust-extension \
     --no-parent \
     --page-requisites \
     -P part-d/before/ \
     https://www.clara.com/es-mx/solutions/small-business
```

Renombrar los archivos resultantes a `corporate-card.html` y `small-business.html` dentro de `before/`.

---

## Paso 2 — Leer y extraer la guía de estilos

Antes de modificar nada en `after/`, leer el HTML de `before/corporate-card.html` y extraer:

**Clases de Webflow a preservar:**
```
fbl-hero-7-title-3     → H1 principal
fbl-heading-h3-6       → H2 de sección
fbl-heading-h5-14      → H3 de componente
fbl-lead-text-26       → Párrafo de cuerpo
fbl-button-2           → CTA primario
uui-button-2           → Botón de registro navbar
fbl-button-icon-23     → CTA secundario con ícono
```

**Tono del copy a mantener:**
- Tuteo consistente: "tu empresa", "tu equipo", "tu gasto"
- Orientado a beneficios, no a features: no "emite tarjetas virtuales" sino "da autonomía a tu equipo sin perder control"
- CTAs con verbos de acción: "Empieza ahora", "Regístrate gratis", "Ver cómo funciona"
- Sin superlativos vacíos

---

## Paso 3 — Cambios SEO on-page en after/corporate-card.html

### Title tag
```html
<!-- BEFORE -->
<title>Tarjeta Corporativa: Emisión Inmediata | Clara</title>

<!-- AFTER -->
<title>Tarjeta Empresarial para Empresas en México | Clara</title>
```
**Por qué:** "Tarjeta empresarial" supera consistentemente a "tarjeta corporativa" en búsquedas en México y Colombia según Google Trends. El cambio alinea el title con el vocabulario real del mercado.

---

### Meta description
```html
<!-- BEFORE -->
<meta name="description" content="Tarjeta Corporativa de crédito empresarial con emisión inmediata...">

<!-- AFTER -->
<meta name="description" content="Tarjeta empresarial para equipos en México. Crédito ilimitado, controles por empleado y conciliación automática. Regístrate en minutos.">
```
**Por qué:** La descripción actual lista features. La nueva responde la pregunta implícita del prospecto ("¿por qué Clara y no mi banco?") y destaca los diferenciadores principales — controles por empleado y conciliación automática — que ninguna tarjeta bancaria tradicional ofrece de forma integrada.

---

### H1
```html
<!-- BEFORE -->
<h1 class="fbl-hero-7-title-3">
  Tarjeta de crédito empresarial para crecer con control
</h1>

<!-- AFTER -->
<h1 class="fbl-hero-7-title-3">
  La tarjeta empresarial que escala con tu equipo
</h1>
```
**Por qué:** Mantiene el keyword primario "empresarial", elimina el tagline genérico "para crecer con control", e introduce "equipo" — término que aparece en queries de intención transaccional como "tarjeta empresarial para empleados".

---

### H2 de sección — añadir sección de diferenciadores vs banco tradicional

Añadir antes del bloque de FAQ existente:

```html
<h2 class="fbl-heading-h3-6">
  Lo que tu banco no puede darte
</h2>
<p class="fbl-lead-text-26">
  A diferencia de una tarjeta bancaria tradicional, puedes emitir 
  tarjetas ilimitadas para tu equipo en minutos, con límites y 
  controles individuales por colaborador. El crédito se otorga 
  a la empresa, no al dueño.
</p>
```
**Por qué:** Esta es la oportunidad de capturar búsquedas de alta intención como "tarjeta corporativa para empresas" y "tarjeta empresarial con control de gastos" — términos que describen los diferenciadores de Clara frente a bancos tradicionales y que ninguna página del sitio trabaja explícitamente hoy.

---

### FAQ schema markup — añadir en <head>

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "¿Cuánto tiempo tarda el proceso de alta en Clara?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "El proceso de alta es 100% digital. En la mayoría de los casos puedes empezar a usar tu tarjeta empresarial el mismo día que completas el registro."
      }
    },
    {
      "@type": "Question",
      "name": "¿Cuántas tarjetas puedo emitir para mi equipo?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Puedes emitir tarjetas ilimitadas — físicas, virtuales o de un solo uso — para todos tus colaboradores, con límites y controles individuales por tarjeta."
      }
    },
    {
      "@type": "Question",
      "name": "¿Cómo controlo lo que gasta cada empleado?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Desde la plataforma Clara defines límites por tarjeta, restricciones por categoría de gasto, horarios de uso y flujos de aprobación. Puedes congelar o cancelar una tarjeta en tiempo real desde la app."
      }
    },
    {
      "@type": "Question",
      "name": "¿Clara se integra con mi sistema de contabilidad?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Sí. Clara tiene integraciones nativas con SAP, NetSuite, QuickBooks, Oracle y Zoho, con sincronización automática de transacciones para cierre mensual sin entradas manuales."
      }
    }
  ]
}
</script>
```

---

### Interlinking hacia small-business — añadir sección antes del CTA final

```html
<div class="fbl-section-interlink">
  <h2 class="fbl-heading-h3-6">
    ¿Es Clara para una empresa como la tuya?
  </h2>
  <p class="fbl-lead-text-26">
    Clara funciona para startups de 5 personas y para empresas 
    de 500. Si tu equipo está creciendo y los gastos se están 
    volviendo difíciles de rastrear, la solución es la misma: 
    control desde el primer peso, sin fricción operativa.
  </p>
  <a href="/es-mx/solutions/small-business" class="fbl-button-icon-23 w-inline-block">
    <div>Ver cómo funciona para PyMEs</div>
  </a>
</div>
```

---

## Paso 4 — Cambios en after/small-business.html

### Title tag
```html
<!-- BEFORE -->
<title>Soluciones para PyMEs | Clara</title>

<!-- AFTER -->
<title>Tarjeta Empresarial para PyMEs en México | Clara</title>
```

### H1
```html
<!-- BEFORE -->
<h1 class="fbl-hero-7-title-3">
  Gestión financiera simple para PyMEs en crecimiento
</h1>

<!-- AFTER -->
<h1 class="fbl-hero-7-title-3">
  El control de gastos que tu PyME necesitaba desde el día uno
</h1>
```

### Añadir perfil de usuario real — después del hero

```html
<div class="fbl-section-profile">
  <h2 class="fbl-heading-h3-6">
    Hecha para equipos que están escalando
  </h2>
  <p class="fbl-lead-text-26">
    Tienes entre 5 y 100 colaboradores. Algunos viajan, otros 
    compran materiales, otros gestionan suscripciones digitales. 
    Hoy todos gastan de su bolsillo y tú reconcilias tickets a 
    fin de mes. Clara elimina ese ciclo: cada colaborador tiene 
    su tarjeta, cada gasto tiene su límite, y tú ves todo en 
    tiempo real sin perseguir a nadie.
  </p>
</div>
```

### Interlinking de regreso hacia corporate-card

```html
<div class="fbl-section-interlink">
  <p class="fbl-lead-text-26">
    ¿Quieres entender primero cómo funciona la tarjeta?
  </p>
  <a href="/es-mx/products/corporate-card" class="fbl-button-icon-23 w-inline-block">
    <div>Ver todas las opciones de tarjeta empresarial</div>
  </a>
</div>
```

---

## Paso 5 — notes.md

Documentar en `part-d/notes.md`:

1. **Assumption:** `/empresas` no existe en el sitio real. La intervención trabaja sobre las dos páginas reales equivalentes.
2. **Hipótesis SEO principal:** La ausencia de interlinking entre páginas de producto y páginas de solución crea journeys incompletos que aumentan el bounce rate y reducen el tiempo en el sitio — señales negativas para rankings. Conectar las dos páginas narrativamente debería reducir el bounce rate y aumentar páginas por sesión.
3. **Hipótesis de vocabulario:** Cambiar "corporativa" por "empresarial" en title tags y H1 de MX debería aumentar impresiones para queries con ese término en 30-60 días.
4. **Métricas de validación:**
   - Bounce rate de ambas páginas (Google Analytics)
   - Páginas por sesión para usuarios que entran por `/products/corporate-card`
   - Impresiones y CTR para queries "tarjeta empresarial" (Search Console)
   - Posición promedio para "tarjeta empresarial México" (Search Console)
5. **Limitación técnica:** Los cambios implementados en el `after/` viven en el repo. En producción, deben aplicarse directamente en Webflow o vía Webflow API para que una republicación no los sobreescriba.

---

## Lo que NO tocar

- Las clases de Webflow existentes — no renombrar ni eliminar
- La estructura de navegación — no modificar el navbar ni el footer
- Los assets externos — imágenes, fuentes y scripts vienen del CDN de Clara y no deben reemplazarse
- El formulario de registro — su funcionalidad depende de scripts de Webflow que no están en el HTML estático
