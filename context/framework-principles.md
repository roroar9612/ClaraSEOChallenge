# Clara — Framework Principles (Webflow)

Convenciones de nomenclatura y estructura extraídas del HTML vivo de clara.com.

---

## Sistema de clases: Flowblocks (fbl-) + UUI (uui-)

Clara usa dos librerías de componentes Webflow:

### Flowblocks (`fbl-`)
Componentes de página: heroes, features, acordeones, grids, textos.

**Patrón de nomenclatura:**
```
fbl-{tipo-componente}-{variante-número}
fbl-{tipo-componente}-{sub-elemento}-{variante-número}
```

Ejemplos:
```
fbl-hero-19              → sección hero, variante 19
fbl-hero-19-title        → título dentro del hero 19
fbl-feature-11-item-2    → ítem dentro de feature 11, variante 2
fbl-heading-h2-10        → heading H2, variante 10
fbl-lead-text-26         → párrafo lead, variante 26
fbl-accordion-1-item-3   → ítem de acordeón 1, variante 3
```

### UUI (`uui-`)
Componentes de UI global: navbar, botones, formularios.

```
uui-navbar02_*           → navbar componentes
uui-button-2             → botón primario
uui-button-secondary-*   → botón secundario
```

---

## Clases custom nuevas (para secciones añadidas)

Para las secciones nuevas del `after/` que no existen en el sitio original, seguir el mismo patrón fbl- con sufijo descriptivo:

```
fbl-section-banco-vs-clara    → sección "Lo que tu banco no puede darte"
fbl-section-interlink         → sección de interlinking hacia small-business
fbl-section-interlink-back    → sección de interlinking hacia corporate-card
fbl-section-profile           → sección perfil de usuario (small-business)
```

---

## Estructura de página (orden canónico)

```
<nav>            → navbar (uui-navbar02_*)
<main>
  <section>      → hero (fbl-hero-19 o fbl-hero-3)
  <div>          → stats bar / prueba social
  <section>      → features principales (fbl-feature-*)
  <section>      → sección diferenciadores (nueva)
  <section>      → FAQ accordion (fbl-accordion-1-*)
  <section>      → interlinking
  <section>      → CTA final / registro (fbl-hero-12)
</main>
<footer>         → footer estándar
```

---

## Jerarquía de headings (1 H1 por página)

```
H1  →  fbl-hero-19-title          (hero, único, 4.6rem)
H2  →  fbl-feature-7-section-title-2  (secciones)
H2  →  fbl-heading-h2-10
H2  →  fbl-heading-h3-6           (usar h3 o h2 según contexto, clase visual independiente)
H3  →  fbl-heading-h5-67          (cards de features)
H3  →  fbl-accordion-1-title-3    (FAQ questions)
```

**Regla crítica:** Solo un `<h1>` por página. Si Webflow genera un segundo `<h1>` (como `fbl-heading-h1-17`), cambiarlo a `<h2>` conservando la clase.

---

## Tono del copy (consistencia)

- Tuteo: "tu empresa", "tu equipo", "tu gasto"
- Beneficios > features: "da autonomía a tu equipo" ≠ "emite tarjetas virtuales"
- CTAs con verbos de acción: "Regístrate gratis", "Ver cómo funciona", "Empieza ahora"
- Sin superlativos vacíos: no "la mejor", no "líder en"
- "sin aval" siempre en minúsculas
- "PyMEs" con mayúsculas (acrónimo)
- "empresarial" > "corporativa" como keyword principal

---

## Webflow: reglas de implementación

1. **Clases**: solo usar clases del style-guide o del patrón fbl-/uui-. Nunca inline styles.
2. **Imágenes**: URLs del CDN de Clara — no descargar ni re-hostear.
   Patrón: `https://cdn.prod.website-files.com/68ffa900bd486e7d9f3183da/`
3. **Scripts externos**: no añadir scripts que no estén en el before/ original.
4. **Breakpoints Webflow** (Desktop → Tablet → Mobile landscape → Mobile portrait):
   - Desktop: base (≥992px)
   - Tablet: 768px–991px
   - Mobile L: 480px–767px
   - Mobile P: <480px
5. **SEO settings**: se aplican en Page Settings > SEO (title, description) y Custom Code > Head (canonical, hreflang, JSON-LD).
6. **Publicación**: NUNCA publicar sin confirmación explícita del usuario.

---

## Componentes reutilizables identificados en el sitio

| Componente | Clase principal | Descripción |
|---|---|---|
| Navbar | `uui-navbar02_*` | Navegación global con dropdowns |
| Hero dark | `fbl-hero-19` | Fondo navy, H1 blanco, CTA |
| Hero light | `fbl-hero-3` | Fondo claro (small-business) |
| Stats bar | `fbl-feature-36` | Números grandes + labels |
| Feature grid | `fbl-feature-5` | 2x2 con icono + título + copy |
| Feature lateral | `fbl-feature-11-*` | Imagen derecha/izquierda + copy |
| Bento grid | `fbl-bentogrid-1-*` | Layout asimétrico tipo bento |
| FAQ | `fbl-accordion-1-*` | Acordeón colapsable |
| CTA final | `fbl-hero-12` | Sección oscura + formulario |
| Footer | Estándar | No modificar |
