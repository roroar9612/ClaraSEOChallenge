# Claude Code — Prompt de producción: SEO Quick Win Clara (Part D)

Este archivo contiene el contexto completo y las instrucciones para implementar las mejoras SEO sobre la página de Tarjeta Corporativa de Clara. Léelo completo antes de modificar cualquier archivo.

---

## Contexto del proyecto

Tienes acceso al archivo `before/corporate-card.html`, descargado con wget desde `https://www.clara.com/es-mx/products/corporate-card` el 30 de abril de 2026. Es una página de Webflow con assets hosteados en el CDN de Clara — no los descargues ni copies, mantén todas las URLs absolutas intactas.

La tarea es producir `after/corporate-card.html` con las mejoras SEO implementadas, sin alterar la estructura visual ni las clases de Webflow. El diff entre `before/` y `after/` es el entregable principal.

---

## Sistema de diseño extraído del archivo (no modificar)

**Tipografías:** Montserrat (headings, todos los pesos de 100 a 900) e Inter (body, pesos 300–700). Cargadas via WebFont.load desde Google Fonts.

**Clases de heading por jerarquía:**
- H1 hero: `fbl-hero-19-title`
- H1 stats section: `fbl-heading-h1-17`
- H2 principal: `fbl-heading-h2-10`, `fbl-feature-5-title`, `fbl-feature-7-section-title-2`, `fbl-heading-h3-6`
- H3 cards: `fbl-heading-h5-67`
- H3 FAQ: `fbl-accordion-1-title-3`

**CSS externo (no tocar):**
```
https://cdn.prod.website-files.com/68ffa900bd486e7d9f3183da/css/lara-test-afe7c8.shared.79e2d9b62.min.css
https://cdn.prod.website-files.com/68ffa900bd486e7d9f3183da/css/lara-test-afe7c8.69714bd40f5eea3a46cdcf96.e1c0b78d2.opt.min.css
```

**Site ID de Webflow:** `68ffa900bd486e7d9f3183da`  
**Page ID de Webflow:** `69714bd40f5eea3a46cdcf96`

---

## Estado actual del `before/` — bugs y oportunidades confirmados

### Bug 1 — hreflang `es-MX` con URL relativa (error de implementación)

```html
<!-- ANTES — URL relativa, inválida para hreflang -->
<link rel="alternate" hrefLang="es-MX" href="corporate-card.html"/>

<!-- También el canonical apunta relativo -->
<link href="corporate-card.html" rel="canonical"/>
```

Esto rompe la señal de localización para México. Google no puede resolver URLs relativas en hreflang.

### Bug 2 — `<title>` con keyword débil

```html
<!-- ANTES -->
<title>Tarjeta Corporativa: Emisión Inmediata | Clara</title>
```

"Tarjeta corporativa" tiene menor volumen de búsqueda en México que "tarjeta empresarial" según Google Trends (últimos 12 meses). "Emisión Inmediata" es copy de marketing, no un modificador de búsqueda.

### Bug 3 — Meta description duplicada en og:description y twitter:description

El mismo texto aparece en `name="description"`, `property="og:description"` y `property="twitter:title"`. No es un error técnico grave, pero es una oportunidad para diferenciar el snippet social del orgánico.

### Bug 4 — FAQ sin schema estructurado

La página tiene una sección FAQ funcional con 8 preguntas (clase `fbl-accordion-1-items-3`) pero sin el bloque `application/ld+json` de tipo `FAQPage`. Google no puede leer esas preguntas como rich results.

### Oportunidad — H1 mejorable en la sección de stats

Hay un segundo `<h1>` en la sección de estadísticas (`fbl-heading-h1-17`) con el texto "Acelera tu crecimiento con Clara". Semánticamente debería ser un `<h2>` — una página no debe tener dos H1.

---

## Instrucciones de implementación — cambios exactos a realizar

### Cambio 1 — Corregir hreflang `es-MX` y canonical

Localiza estas dos líneas en el `<head>`:

```html
<link rel="alternate" hrefLang="es-MX" href="corporate-card.html"/>
```
```html
<link href="corporate-card.html" rel="canonical"/>
```

Reemplázalas por:

```html
<link rel="alternate" hrefLang="es-MX" href="https://www.clara.com/es-mx/products/corporate-card"/>
```
```html
<link href="https://www.clara.com/es-mx/products/corporate-card" rel="canonical"/>
```

### Cambio 2 — Actualizar `<title>` y meta description

Localiza:

```html
<title>Tarjeta Corporativa: Emisión Inmediata | Clara</title>
```

Reemplaza por:

```html
<title>Tarjeta Empresarial para Empresas en México | Clara</title>
```

Localiza `name="description"`:

```html
<meta content="Tarjetas corporativas con emisión al instante y controles en tiempo real. Conciliación en 5 segundos, sincronización con SAT y políticas de gasto automatizadas." name="description"/>
```

Reemplaza por:

```html
<meta content="Tarjeta empresarial con emisión al instante, controles por equipo y conciliación automática. Sincronización con SAT, integración ERP y políticas de gasto automatizadas. Más de 30,000 empresas en México." name="description"/>
```

Actualiza también `og:title` y `twitter:title` para que coincidan con el nuevo `<title>`:

```html
<meta content="Tarjeta Empresarial para Empresas en México | Clara" property="og:title"/>
<meta content="Tarjeta Empresarial para Empresas en México | Clara" property="twitter:title"/>
```

### Cambio 3 — Corregir el segundo H1 a H2

Localiza el elemento con clase `fbl-heading-h1-17`:

```html
<h1 class="fbl-heading-h1-17">Acelera tu crecimiento con Clara</h1>
```

Reemplaza por:

```html
<h2 class="fbl-heading-h1-17">Acelera tu crecimiento con Clara</h2>
```

> Nota: la clase `fbl-heading-h1-17` controla el estilo visual, no la semántica. Puedes conservarla en un `<h2>` sin que cambie el diseño.

### Cambio 4 — Agregar FAQ schema en JSON-LD

Las 8 preguntas del FAQ ya existen en el HTML. Agrega el siguiente bloque `<script>` inmediatamente **antes del cierre del `</head>`**, usando las preguntas y respuestas tal como aparecen en el DOM:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "¿Qué significa que una tarjeta esté en estado 'Restringido'?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Indica que tu tarjeta sigue reglas de control de tiempo definidas por tu admin — está esperando el inicio de su ventana de uso permitida."
      }
    },
    {
      "@type": "Question",
      "name": "¿Existe una política de cancelación para las tarjetas?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Clara cancela automáticamente tarjetas Virtuales y White sin uso prolongado. No aplica para Black. Te avisan con 1 mes de anticipación."
      }
    },
    {
      "@type": "Question",
      "name": "¿Puedo usar mi tarjeta Clara en billeteras digitales?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Sí. Compatible con Apple Pay (iPhone/Watch), Google Pay (Android) y Garmin Pay (relojes Garmin)."
      }
    },
    {
      "@type": "Question",
      "name": "¿Cómo modificar el límite de una tarjeta?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "En Tarjetas > selecciona tarjeta > Editar > cambia límite de crédito. La solicitud sigue el flujo de aprobación configurado."
      }
    },
    {
      "@type": "Question",
      "name": "¿Qué hago en caso de robo o clonación de mi tarjeta?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Bloquea tu tarjeta inmediatamente desde la plataforma o app. Informa a tu administrador y reporta el incidente a soporte."
      }
    },
    {
      "@type": "Question",
      "name": "¿Cuánto tarda en llegar mi tarjeta Clara?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Aproximadamente 4 días hábiles. Puedes monitorear el envío en tiempo real desde la plataforma Clara."
      }
    },
    {
      "@type": "Question",
      "name": "¿Cómo activo mi tarjeta Clara?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Las tarjetas Clara White y Black se activan desde la app. Las virtuales se activan automáticamente al crearlas."
      }
    },
    {
      "@type": "Question",
      "name": "¿Cómo crear tarjetas en Clara?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Accede a Tarjetas > Nueva tarjeta, llena formulario con tipo (Virtual, White, Black), límite y configuraciones. No hay límite de tarjetas adicionales."
      }
    }
  ]
}
</script>
```

---

## Output esperado

Al terminar, el repo debe tener esta estructura:

```
part-d/
├── before/
│   └── corporate-card.html        ← archivo original sin modificar
├── after/
│   └── corporate-card.html        ← archivo con los 4 cambios implementados
└── notes.md                       ← justificación de cada cambio (ver abajo)
```

---

## Contenido del `notes.md` a generar

Genera `part-d/notes.md` con esta estructura:

```markdown
# Part D — SEO Quick Win: Tarjeta Corporativa Clara

## Hipótesis
Cuatro cambios técnicos de bajo riesgo y alto impacto sobre la página 
/es-mx/products/corporate-card, ejecutables sin rediseño.

## Cambios implementados

### 1. hreflang es-MX y canonical — corrección de URL relativa
**Antes:** `href="corporate-card.html"`  
**Después:** `href="https://www.clara.com/es-mx/products/corporate-card"`  
**Por qué:** Google no puede resolver URLs relativas en hreflang. Esta configuración 
hace que la versión mexicana de la página no reciba la señal de localización correcta, 
lo que afecta el ranking en búsquedas desde México.

### 2. Title tag — keyword primaria
**Antes:** "Tarjeta Corporativa: Emisión Inmediata | Clara"  
**Después:** "Tarjeta Empresarial para Empresas en México | Clara"  
**Por qué:** Google Trends (últimos 12 meses, México) muestra que "tarjeta empresarial" 
supera consistentemente a "tarjeta corporativa" en volumen. "Emisión Inmediata" es copy 
de conversión, no un modificador de búsqueda con demanda real.

### 3. H1 duplicado — corrección semántica
**Antes:** Dos elementos `<h1>` en la misma página  
**Después:** El segundo H1 se convierte en `<h2>` (conservando la clase visual)  
**Por qué:** Una página con dos H1 envía señales contradictorias sobre el tema principal. 
Google recomienda una jerarquía clara; el cambio es de una sola línea y cero riesgo visual.

### 4. FAQ schema — JSON-LD
**Antes:** 8 preguntas en el DOM sin marcado estructurado  
**Después:** Bloque FAQPage en JSON-LD con las mismas 8 preguntas  
**Por qué:** El schema FAQPage habilita rich results en SERP (preguntas expandibles), 
lo que aumenta el CTR sin modificar el contenido visible. Las preguntas ya existen; 
el costo de implementación es agregar ~40 líneas al `<head>`.

## Métricas de validación
- **hreflang:** Google Search Console > Internacional > Errores de hreflang. 
  El error de URL relativa para es-MX debe desaparecer en 2–4 semanas.
- **Title/keyword:** Search Console > Rendimiento > Consultas. 
  Monitorear impresiones y posición media para "tarjeta empresarial" vs "tarjeta corporativa" 
  a 30 días del despliegue.
- **FAQ schema:** Google Rich Results Test aplicado al `after/`. 
  En producción: Search Console > Mejoras > Preguntas frecuentes.

## Assumption crítica
Estos cambios viven en el repo. En producción, deben implementarse directamente 
en el editor de Webflow o vía Webflow API para evitar que una republicación 
desde el CMS sobreescriba las modificaciones.
```

---

## Verificación final antes de hacer commit

Corre estos checks sobre `after/corporate-card.html`:

```bash
# 1. Confirmar que el hreflang es-MX ya es absoluto
grep 'hrefLang="es-MX"' after/corporate-card.html

# 2. Confirmar que el title cambió
grep '<title>' after/corporate-card.html

# 3. Confirmar que no hay dos <h1> (debe devolver 1 resultado)
grep -c '<h1' after/corporate-card.html

# 4. Confirmar que el schema está presente
grep 'FAQPage' after/corporate-card.html
```

Los cuatro checks deben pasar antes de hacer commit.
