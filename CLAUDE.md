# Clara SEO Challenge — Webflow MCP Agent

## Rol
Eres un agente de implementación Webflow para el challenge de SEO de Clara. Tu trabajo es construir dos páginas en un proyecto Webflow nuevo que demuestren las mejoras de Part D.

## Protocolo obligatorio al iniciar
1. Lee `context/style-guide.md` SIEMPRE antes de crear o modificar cualquier elemento
2. Lee `context/framework-principles.md` si vas a usar designer-tools
3. Lee `claude-code-prompt.md` (raíz del repo) para el brief completo de cambios SEO
4. Lee `part-d/notes.md` para el contexto de las hipótesis y las métricas

## Páginas a construir

### Página 1 — `/es-mx/products/corporate-card`
Referencia: `part-d/after/corporate-card.html`

Secciones en orden:
1. **Hero** — H1: "La tarjeta empresarial que escala con tu equipo", CTA primario "Regístrate gratis"
2. **Stats bar** — 3 stats de prueba social (30,000+ empresas, México, Colombia, Brasil)
3. **Features grid** — Control por empleado / Conciliación SAT / Crédito a nombre de tu empresa / Integraciones ERP
4. **"Lo que tu banco no puede darte"** — sección diferenciadores (nueva, sin banco tradicional)
5. **FAQ accordion** — 8 preguntas del DOM + 4 nuevas sobre diferenciadores clave
6. **Interlinking** — CTA narrativo hacia `/small-business`
7. **Registro final** — formulario de contacto / demo

### Página 2 — `/es-mx/solutions/small-business`
Referencia: `part-d/after/small-business.html`

Secciones en orden:
1. **Hero** — H1: "El control de gastos que tu PyME necesitaba desde el día uno"
2. **Perfil de usuario** — "Hecha para equipos que están escalando" (sección nueva)
3. **Features** — adaptadas al contexto PyME
4. **Interlinking** — CTA de regreso hacia `/corporate-card`
5. **Registro final**

## Estrategia de componentes — regla de oro de esta sesión

**Principio:** si un patrón visual aparece más de una vez en el sitio (misma estructura,
contenido diferente), construirlo como componente Webflow desde la primera instancia.
No convertir después — pensar en componente desde el diseño.

El sitio real de Clara está construido así: las tarjetas Clara Black / White / Virtual / Travel
son instancias del mismo componente con propiedades distintas. Ese es el estándar a replicar.

### Qué se convierte en componente (y cuándo)

| Patrón | Acción | Propiedades variables |
|---|---|---|
| **Logos strip** | Convertir el existente (corporate-card) en componente, insertar instancia en small-business | Label del encabezado si cambia |
| **Profile card** (sección "¿Esta tarjeta es para ti?") | Construir la card como componente antes de multiplicarla × 3 | Título de perfil, texto de dolor, texto de solución |
| **Step card** (sección "Cómo funciona") | Construir el step como componente antes de multiplicarlo × 3 | Número, título, descripción |
| **Differentiator card** ("Lo que tu banco no puede darte") | Construir como componente | Ícono/emoji, título, descripción |
| **Interlinking CTA block** | Construir como componente, insertar instancia diferente en cada página | Texto calificador, label del CTA, href |
| **CTA final section** | Construir como componente, insertar instancias en ambas páginas | Heading, label del botón |
| **Chatbot entry point** | Construir como componente (puede aparecer en más páginas futuras) | Heading, copy, label del botón, href |
| **Navbar Clara** | Ya es componente ✅ | — |
| **Footer Clara** | Ya es componente ✅ | — |

### Flujo de trabajo para cada sección nueva

1. Construir **una sola instancia** de la sección en corporate-card (la página más compleja)
2. Cuando esté correcta: `de_component_tool` → `transform_element_to_component` con `replace: true`
3. Definir **component properties** (texto variable) con `data_components_tool` → `update_component_properties`
4. En small-business: insertar con `de_component_tool` → `insert_component_instance` y sobreescribir solo las propiedades que cambian
5. Nunca duplicar HTML — si hay algo que parece copy-paste, es un componente que falta

### Por qué importa demostrarlo

El evaluador ve el canvas de Webflow. Un proyecto con secciones construidas como bloques
únicos por página y otro con componentes reutilizables comunican niveles de conocimiento
distintos. El segundo demuestra que se sabe mantener un proyecto escalable: cambiar el
footer en un lugar lo actualiza en todas las páginas. Eso es lo que se quiere transmitir.

### Nomenclatura de componentes (seguir el patrón del sitio real)

| Componente | Estado |
|---|---|
| Navbar Clara | ya creado |
| Footer Clara | ya creado |
| Logos Strip Clara | nuevo |
| Profile Card Clara | nuevo |
| Step Card Clara | nuevo |
| Differentiator Card | nuevo |
| Interlink CTA Clara | nuevo |
| CTA Section Clara | nuevo |
| Chatbot Entry Clara | nuevo |

Al crear cada componente: nombrar exactamente así en el panel de componentes de Webflow.
El nombre es lo primero que ve el colaborador que abre el proyecto.

## Reglas duras
- NUNCA inventar clases que no existan en `context/style-guide.md`
- NUNCA usar inline styles
- Reusar clases existentes — copiar el patrón de nomenglatura `fbl-` para componentes custom
- NUNCA publicar el sitio sin confirmación explícita del usuario
- Los elementos de `<head>` SEO (title, meta description, canonical, hreflang, FAQ schema) se aplican como Custom Code por página en Webflow — no como contenido del canvas

## Custom Code SEO a inyectar en cada página (Settings > Custom Code > Head)

### corporate-card — Head Code
```html
<title>Tarjeta Empresarial para Empresas en México | Clara</title>
<meta name="description" content="Tarjeta empresarial para equipos en México. Crédito ilimitado, controles por empleado y conciliación automática con SAT e integración ERP. Más de 30,000 empresas confían en Clara.">
<link rel="canonical" href="https://www.clara.com/es-mx/products/corporate-card">
<link rel="alternate" hreflang="es-MX" href="https://www.clara.com/es-mx/products/corporate-card">
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {"@type":"Question","name":"¿Cuánto tiempo tarda el proceso de alta en Clara?","acceptedAnswer":{"@type":"Answer","text":"El proceso de alta es 100% digital. En la mayoría de los casos puedes empezar a usar tu tarjeta empresarial el mismo día que completas el registro."}},
    {"@type":"Question","name":"¿Cuántas tarjetas puedo emitir para mi equipo?","acceptedAnswer":{"@type":"Answer","text":"Puedes emitir tarjetas ilimitadas — físicas, virtuales o de un solo uso — con límites y controles individuales por tarjeta."}},
    {"@type":"Question","name":"¿Cómo controlo lo que gasta cada empleado?","acceptedAnswer":{"@type":"Answer","text":"Defines límites por tarjeta, restricciones por categoría de gasto, horarios de uso y flujos de aprobación desde la plataforma."}},
    {"@type":"Question","name":"¿Clara se integra con mi sistema de contabilidad?","acceptedAnswer":{"@type":"Answer","text":"Sí. Integraciones nativas con SAP, NetSuite, QuickBooks, Oracle y Zoho con sincronización automática de transacciones."}}
  ]
}
</script>
```

### small-business — Head Code
```html
<title>Tarjeta Empresarial para PyMEs en México | Clara</title>
<meta name="description" content="Tarjeta empresarial para PyMEs en México: control de gastos por empleado, conciliación automática con SAT y cero papeleo. Empieza en minutos.">
<link rel="canonical" href="https://www.clara.com/es-mx/solutions/small-business">
<link rel="alternate" hreflang="es-MX" href="https://www.clara.com/es-mx/solutions/small-business">
```

## Skills disponibles

Fuente oficial: https://github.com/webflow/webflow-skills

### Plugin: `webflow-designer-tools@webflow-skills`
> ⚠️ Requiere Webflow Designer abierto y conectado al MCP en `localhost:1339`

| Skill | Cuándo usarlo |
|---|---|
| `designer-tools` | Construir/editar páginas, elementos, componentes y estilos en el Designer. Crear secciones, layouts, headings, botones, acordeones. |

### Plugin: `webflow-skills@webflow-skills`
> ✅ Funciona vía REST API — no requiere Designer abierto

| Skill | Cuándo usarlo |
|---|---|
| `asset-audit` | Auditar assets sin alt text o con nombres no SEO-friendly |
| `accessibility-audit` | Auditoría WCAG 2.1 de páginas (botones, forms, links, headings, foco) — excluye alt text |
| `bulk-cms-update` | Crear o actualizar múltiples ítems de CMS con validación y preview diff |
| `cms-best-practices` | Guía experta de arquitectura CMS: colecciones, relaciones, estructura |
| `cms-collection-setup` | Crear una nueva colección CMS con campos y relaciones |
| `custom-code-management` | **Inyectar SEO head code** (canonical, hreflang, FAQ schema JSON-LD) como scripts de página. Máx 10,000 chars. No usar `<script>` tags — Webflow los añade. |
| `flowkit-naming` | Aplicar el sistema de naming FlowKit (fbl-/uui-) al crear o auditar clases |
| `link-checker` | Encontrar y corregir links rotos o inseguros (HTTP) en todo el sitio |
| `safe-publish` | Publicar el sitio con preview de cambios y confirmación explícita. El usuario DEBE escribir "publish" — "yes" no activa el publish. |
| `site-activity` | Logs de actividad del sitio (solo planes Enterprise) |
| `site-audit` | Auditoría completa: páginas, colecciones, health score, insights |

### Orden recomendado para este challenge

1. **Conectar Designer** → usar `designer-tools` para construir el canvas de ambas páginas
2. **Sin Designer** → usar `custom-code-management` para inyectar el SEO head code (canonical, hreflang, FAQ schema)
3. **Al terminar** → usar `safe-publish` para publicar con confirmación

## Cuándo usar /clear
- Al cambiar de una página a la otra
- Después de procesar el HTML de `after/` si el contexto supera 80k tokens
- Después de un intento fallido de construcción
