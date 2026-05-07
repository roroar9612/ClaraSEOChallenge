# Part A — SEO Audit: clara.com

**Scope:** Technical SEO issues, on-page review of the homepage, and content opportunities for MX and BR.  
**Tools used:** Stackoptic (automated technical audit), Browser DevTools, manual site review, Google Trends (12-month export by country), Sitemap analysis, SEMrush (traffic data).  
**Date:** April 2026

---

## Assumption Log

**Assumption 1 — La `/empresas` page es hipotética.** No existe esa URL en el sitemap. Para la Parte D se trabaja sobre dos páginas reales que sirven el mismo propósito: `/es-mx/products/corporate-card` y `/es-mx/solutions/small-business`. Ambas comparten componentes y copy casi idénticos — lo cual es en sí mismo un hallazgo.

**Assumption 2 — La estrategia de vocabulario requiere coexistencia, no sustitución.** Clara usa "tarjeta corporativa" como nombre de producto. Google Trends muestra que "tarjeta empresarial" supera a "tarjeta corporativa" en volumen de búsqueda en MX y CO de forma consistente — en Colombia, "corporativa" tiene volumen cercano a cero. El enfoque correcto no es abandonar "corporativa" sino trabajar con los dos términos en capas distintas: "empresarial" como ancla en los elementos de mayor peso SEO (title, H1, meta description), y "corporativa" como señal semántica secundaria en subtítulos y cuerpo de texto. Brasil es la excepción — "cartão corporativo" lidera y el sitio ya lo usa correctamente.

Esta estrategia resuelve la tensión entre lo que la marca llama al producto y lo que los usuarios buscan, sin crear inconsistencia de marca.

**Assumption 3 — Los slugs de URL en inglés afectan la señal de localización.** Páginas como `/products/corporate-card` y `/cards/black-card` dentro de rutas en español generan una señal de localización inconsistente. El impacto del slug por sí solo es modesto, pero la inconsistencia amplifica los problemas de hreflang y contenido duplicado que ya existen. Cualquier migración de slugs debe acompañarse de 301 redirects y validación en Google Search Console antes y después del cambio.

---

## 1. Top 3 Critical Technical SEO Issues

### Issue 1 — Hreflang incompleto en páginas internas

Clara opera en tres mercados (MX, CO, BR) con contenido en español y portugués. Stackoptic confirma que la homepage global (`clara.com`) tiene hreflang implementado correctamente — con pares por idioma-país y `x-default` apuntando a la versión global (score 10/10). El problema está en las páginas internas: los atributos `hreflang` y `canonical` usan URLs relativas en lugar de absolutas, lo que hace que Google no pueda resolver a qué versión pertenece cada página ni servir la correcta a cada mercado.

**Por qué es prioritario:** No es un bug aislado — es la causa raíz que amplifica todos los demás problemas de localización. Un CFO en Colombia buscando "tarjeta empresarial" puede recibir la versión mexicana, o la homepage global en inglés, según lo que Google decida. La caída del 11% en tráfico orgánico observada en SEMrush (235,528 visitas, abril 2026) tiene explicación estructural aquí: el sitio canibaliza sus propias versiones.

**Impacto esperado al corregirlo:** Hreflang con URLs absolutas permite a Google indexar y servir la versión correcta a cada mercado. Detiene la canibalización entre `/es-mx/`, `/es-co/` y `/pt-br/` y recupera impresiones orgánicas perdidas por confusión de versión.

**Nota de implementación:** Una tag hreflang por página por par idioma-país, con `x-default` apuntando a la versión global. Debe ser consistente tanto en el `<head>` HTML como en el sitemap. En Webflow, esto se gestiona desde Custom Code > Head en Page Settings.

---

### Issue 2 — Structured data ausente (score 0/100)

Stackoptic detectó ausencia completa de structured data en las páginas de producto. No hay schema de tipo `Organization`, `FAQPage`, `BreadcrumbList`, ni `LocalBusiness`. El score en esta dimensión es 0/100.

**Por qué importa:** El structured data es la forma en que el sitio le comunica a Google — y a los motores de AI search — qué tipo de entidad es cada página, qué preguntas responde, y cómo se relaciona con el resto del sitio. Sin él, Google no puede mostrar rich results (accordions de FAQ en SERP, breadcrumbs visuales, datos de empresa). Para GEO, la ausencia de schema estructurado reduce la probabilidad de que los modelos de AI citen correctamente la información del sitio — los modelos priorizan contenido estructurado y atribuible.

`FAQPage` schema en la página de tarjeta corporativa es la intervención de mayor retorno inmediato: habilita rich results en la SERP para las preguntas que los prospectos ya están haciendo.

**Impacto esperado al corregirlo:** Rich results en SERP para páginas de producto, mejor señal de entidad para Google Knowledge Graph, y contenido más citable por motores de AI search. El FAQ schema se implementa como JSON-LD en el `<head>` — sin tocar el HTML visible ni requerir cambios de diseño.

---

### Issue 3 — Señales de localización inconsistentes

Este issue tiene múltiples expresiones que apuntan al mismo problema subyacente: el sitio creció rápido en mercados sin un proceso centralizado de localización.

Las manifestaciones concretas identificadas en el audit incluyen:

- El atributo `html lang` está fijado como `"en-US"` en todas las versiones del sitio, incluyendo las páginas en español (`/es-mx/`, `/es-co/`) y portugués (`/pt-br/`). Esto envía una señal de idioma incorrecta a Google y a los lectores de pantalla — es una falla simultánea de SEO y accesibilidad (WCAG 3.1.1).
- Páginas de error 404 aparecen en inglés dentro de rutas `/es-mx/`, exponiendo texto de CMS: "0 results found for this URL".
- Nombres de producto en inglés dentro de páginas en portugués en `/pt-br/`.
- El selector de país en la homepage global mezcla países con idiomas (中文 listado junto a nombres de países), con la mayoría de selecciones redirigiendo a una versión en español diseñada para otro mercado.
- No hay detección por IP para sugerir la versión correcta del mercado a un visitante nuevo.

**Por qué importa:** Cada inconsistencia envía una señal contradictoria sobre el idioma y mercado al que sirve cada página. Esto refuerza el problema de hreflang y genera confusión adicional sobre qué versión debería rankear para qué query. El `html lang="en-US"` en páginas en español también falla WCAG 3.1.1, lo que impide que lectores de pantalla pronuncien el contenido correctamente.

**Impacto esperado al corregirlo:** Corregir `html lang` por ruta (`es-MX`, `es-CO`, `pt-BR`), añadir páginas de error localizadas, corregir el selector de país, e implementar sugerencia de versión por IP reduciría la fricción en cada etapa del journey y fortalecería la señal de localización por mercado.

---

## 2. On-Page SEO Review — Homepage

Se revisaron dos versiones: `clara.com` (global) y `clara.com/es-mx` (México).

### Homepage global — `clara.com`

| Elemento | Estado actual | Evaluación |
|---|---|---|
| Title tag | `Clara \| Spend Management for LatAm` | En inglés. "LatAm" es una abreviatura del sector, no un término de búsqueda que usen usuarios hispanohablantes o lusohablantes. |
| Meta description | `The financial operating system for Latin America. Corporate cards, expense automation, AP, and banking — built for companies in MX, BR, and CO.` | En inglés. Formato de lista de features. Menciona MX, BR, CO (señal geográfica positiva), pero no está escrita para responder ninguna búsqueda orgánica real. |
| H1 | `The partner to Latin America's leading finance teams` | En inglés. Statement de posicionamiento, no una frase orientada a búsqueda. "Leading finance teams" señala aspiración enterprise pero no corresponde a ninguna query real. |

**El problema no es que la homepage global esté en inglés.** Es una decisión de marca defendible — la homepage global sirve a inversores, socios y prensa, audiencias para quienes el inglés funciona como idioma compartido en el mundo fintech. El problema es estructural: `clara.com` es la URL de mayor autoridad del dominio, y está completamente desconectada de cualquier intención de búsqueda orgánica en los mercados que generan el tráfico real. Su interlinking no distribuye autoridad eficientemente hacia las páginas en español y portugués que compiten por queries reales. La homepage está optimizada para una audiencia que no descubre Clara a través de búsqueda orgánica, y al mismo tiempo falla en apoyar las páginas que sí dependen de ella.

### Homepage México — `clara.com/es-mx`

| Elemento | Estado actual | Evaluación |
|---|---|---|
| Title tag | `Clara \| Gestión Financiera Inteligente para LatAm` | En español. "Gestión Financiera Inteligente" es un tagline de marca, no una búsqueda. No hay keyword target presente. |
| Meta description | `Tarjetas corporativas, gestión de gastos y banking en una sola plataforma. Clara ayuda a empresas en Latinoamérica a controlar gastos y escalar con confianza.` | En español. Más descriptivo que la versión global. Sigue sin estar escrita alrededor de una intención de búsqueda específica. |
| H1 | `Gestión de gastos para equipos financieros exigentes` | En español. Describe la plataforma con precisión pero funciona como tagline. "Equipos financieros exigentes" no es una frase que ningún usuario escriba en Google. |

**Qué cambiaría y por qué:**

El title tag y el H1 deben incorporar el término de búsqueda primario del mercado, preservar el nombre de la marca, y mantener el tono de tuteo característico de Clara. Una propuesta de title: `Clara — Tarjeta corporativa y gestión de gastos para tu empresa en México`. Esto mantiene la marca, usa "tarjeta corporativa" como nombre oficial del producto con señal geográfica, y evita pleonasmos como "tarjeta empresarial para empresas" donde el sustantivo y el adjetivo repiten la misma idea.

El H1 debe reflejar intención de búsqueda sin sonar genérico. Una dirección que respeta el tono de Clara: `El control de gastos que tu empresa necesitaba desde el primer día`. Habla en segunda persona (tuteo, consistente con la guía de estilo), ancla la página en la categoría real del producto, y comunica el diferenciador de valor sin superlativos vacíos.

La meta description debe funcionar como un activo de conversión en la SERP, respondiendo la pregunta implícita del comprador potencial: ¿por qué Clara sobre una tarjeta de banco tradicional? Propuesta: `Emite tarjetas para tu equipo, automatiza reembolsos y cierra el mes sin caos. Sin aval, sin historial crediticio. Más de 30,000 empresas ya lo hacen con Clara.`

El **interlinking interno** de la homepage de México está orientado principalmente al registro. La sección hero enlaza a `/es-mx/registration` y a un demo de plataforma. No hay links prominentes hacia páginas de producto (`/products/corporate-card`), páginas de solución (`/solutions/small-business`, `/solutions/enterprise`), ni contenido que ayude a un prospecto a entender el producto antes de comprometerse con el flujo de registro. Esto limita la capacidad de la homepage de distribuir autoridad hacia el sitio y acorta el journey de descubrimiento para usuarios que aún no están listos para registrarse.

---

## 3. Hallazgos adicionales de Stackoptic

Stackoptic identificó tres problemas adicionales que no son críticos para rankings pero sí para la experiencia del usuario y para señales indirectas de SEO:

**Flesch Reading Ease: 18/100.** El texto del sitio tiene un nivel de complejidad extremadamente alto — equivalente a un paper académico. Para una plataforma dirigida a directores financieros de PyMEs y startups, este nivel crea fricción innecesaria. El tono de Clara en su guía de estilo apunta a lo contrario: beneficios concretos sobre features, tuteo, sin superlativos. "Tu equipo gasta, tú apruebas, el sistema reconcilia" — no "la solución optimiza los flujos de gestión del gasto empresarial". El Flesch score es también una señal indirecta de SEO: el tiempo en página y el scroll depth caen cuando el texto es difícil de leer.

**Font sizes en `vw` puro.** Unidades de tamaño de fuente definidas exclusivamente en `vw` sin `clamp()` ni fallback en `rem` rompen el zoom del navegador. Falla WCAG 1.4.4 (Resize Text). La corrección es técnica y no afecta el diseño visual.

**Madurez del marketing tech stack: 32/100.** Stackoptic solo detectó Google Analytics y GTM activos en el sitio. No hay herramientas de heatmaps, A/B testing ni CRO (Hotjar, VWO, Optimizely o equivalentes). Para un equipo de growth que toma decisiones sobre cambios en el sitio, la ausencia de datos de comportamiento del usuario limita la capacidad de validar hipótesis — incluyendo las planteadas en este challenge.

---

## 4. Two Content Opportunities in MX and BR

### Opportunity 1 — Capturar demanda de "tarjeta empresarial" en MX y CO

Google Trends de los últimos 12 meses muestra una brecha consistente y significativa entre el volumen de búsqueda de "tarjeta empresarial" y "tarjeta corporativa" en México y Colombia. "Tarjeta empresarial" supera a "tarjeta corporativa" en todos los meses del período. En Colombia, "tarjeta corporativa" registra volumen cercano a cero. Brasil es la excepción — "cartão corporativo" lidera y el sitio ya lo usa correctamente.

El sitio usa "Tarjeta Corporativa" como nombre de producto oficial en todos los mercados hispanohablantes. Esto genera una brecha de vocabulario: la marca habla de una manera y el mercado busca de otra. La solución no es renombrar el producto — es trabajar los dos términos en capas distintas: "empresarial" en elementos de mayor peso SEO (title, H1, meta description) y "corporativa" como refuerzo semántico en subtítulos y cuerpo de texto, donde refuerza la identidad de marca. La URL `/es-mx/landing/tarjeta-de-credito-empresarial` ya existe y señala que la oportunidad fue identificada parcialmente, pero existe como landing page aislada sin arquitectura de contenido coherente detrás.

Términos de alto intent sin trabajar actualmente: "tarjeta empresarial sin aval", "tarjeta corporativa sin historial crediticio", "tarjeta de gastos para empleados México". Estos describen los diferenciadores específicos de Clara frente a los bancos tradicionales y tienen baja competencia orgánica.

### Opportunity 2 — Contenido mid-funnel sobre procesos de gestión de gastos

Un comprador potencial que tiene el problema que Clara resuelve pero aún no conoce Clara no busca "Clara tarjeta empresarial". Busca respuestas a problemas operativos: "cómo reembolsar gastos a empleados en México", "proceso de reembolso de viáticos empresas", "cómo controlar gastos de equipo en campo", "política de gastos corporativos PyME".

Ninguna de estas queries tiene respuesta en ninguna página del sitio hoy. El blog de product releases contiene descripciones detalladas y precisas de exactamente los features que responden estas preguntas — el módulo de reembolsos, los controles de tarjeta, la reconciliación Smart Match — pero ese contenido está escrito como anuncios internos de producto, no como respuestas a búsquedas de usuarios. Llega a clientes existentes, no a prospectos.

La oportunidad es construir una capa de contenido entre el blog y las páginas de producto: artículos o landing pages escritas alrededor de problemas operativos específicos que Clara resuelve, usando el vocabulario de la búsqueda, y enlazando a la página de producto relevante como solución. Este tipo de contenido es particularmente valioso para GEO porque los motores de AI search priorizan respuestas desde contenido estructurado, específico y claramente atribuible — exactamente lo que esta capa proveería.

Brasil es un foco adicional. El sitio `/pt-br/` tiene el vocabulario correcto ("cartão corporativo") pero la misma ausencia de contenido mid-funnel. Búsquedas como "como reembolsar despesas de funcionários" o "controle de gastos empresariais Brasil" representan demanda real que ninguna página captura actualmente.
