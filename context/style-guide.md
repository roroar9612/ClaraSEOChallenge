# Clara — Style Guide (extraído de Webflow CDN)

Fuente: CSS vivo de `cdn.prod.website-files.com/68ffa900bd486e7d9f3183da`  
Site ID Webflow: `68ffa900bd486e7d9f3183da`

---

## Tokens de color (CSS custom properties)

```css
/* Paleta principal */
--flowblocks-component-library--color--black:        #011131;  /* navy oscuro — texto principal */
--flowblocks-component-library--color--white:        #ffffff;

/* Azules primarios */
--flowblocks-component-library--color--primary-1:    #032257;  /* navy profundo — fondos dark */
--flowblocks-component-library--color--primary-2:    #0853b6;  /* azul medio — hover */
--flowblocks-component-library--color--primary-3:    #0853b6;  /* azul medio — CTAs */

/* Teal (identidad de marca Clara) */
--flowblocks-component-library--color--primary-4:    #003f41;  /* teal oscuro */
--flowblocks-component-library--color--secondary-3:  #003f41;  /* teal oscuro (alias) */
--clara-teal-primary:                                #00adb1;  /* teal principal (de background) */
--clara-teal-medium:                                 #009497;
--clara-teal-light:                                  #0cd6dc;

/* Verde acento */
--flowblocks-component-library--color--secondary-5:  #00e66b;  /* green accent */
--clara-green-light:                                 #a3ffbf;

/* Colores de acento / soporte */
--flowblocks-component-library--color--primary-5:    #f09e99;  /* salmon */
--flowblocks-component-library--color--primary-6:    #aac2fe;  /* blue claro */
--flowblocks-component-library--color--secondary-1:  #dfe0fd;  /* lavender claro */
--_clara-palette---bold-cobalt:                      #06459c;

/* Grises UI */
--flowblocks-component-library--color--gray-1:       #f9f9f9;  /* fondo secciones claras */
--flowblocks-component-library--color--gray-2:       #787c8c;  /* texto secundario */
--flowblocks-component-library--color--light-grey:   #f5f9fc;  /* fondo muy claro */
--flowblocks-component-library--color--border-color: #e3e3e8;  /* bordes */

/* Sistema */
--flowblocks-component-library--color--transparent:  #0000;
```

---

## Tipografía

```
Headings:  Montserrat (pesos 100–900 via Google Fonts)
Body:      Inter (pesos 300, 400, 500, 600, 700 via Google Fonts)
Fallback:  Arial, "Helvetica Neue", Helvetica, sans-serif
```

WebFont loader (incluir en `<head>`):
```html
<script src="https://ajax.googleapis.com/ajax/libs/webfont/1.6.26/webfont.js"></script>
<script>
WebFont.load({
  google: {
    families: [
      "Montserrat:100,100italic,200,200italic,300,300italic,400,400italic,500,500italic,600,600italic,700,700italic,800,800italic,900,900italic",
      "Inter:300,400,500,600,700"
    ]
  }
});
</script>
```

---

## Escala tipográfica

| Nivel | Clase Webflow | Tamaño desktop | Responsive |
|---|---|---|---|
| Hero H1 | `fbl-hero-19-title` | 4.6rem | 3rem / 2.5rem / 2rem |
| H1 stats | `fbl-heading-h1-17` | 3rem, lh 1.2em | — |
| H1 base | `fbl-heading-h1` | 3rem, lh 1.2em | — |
| H2 | `fbl-heading-h2-10`, `fbl-feature-7-section-title-2` | 2.5rem | 2rem |
| H3 | `fbl-heading-h3-6`, `fbl-heading-h3-light-6` | 2.25rem | — |
| H4 | `fbl-heading-h4-11` | 1.75rem | — |
| H5 | `fbl-heading-h5-67` | 1.5rem | — |
| H6 | `fbl-heading-h6-77` | 1.25rem | — |
| Lead text | `fbl-lead-text-44`, `fbl-lead-text-26` | 1.125rem–1.25rem | — |
| Body | `fbl-text-default-103` | 1rem | — |
| FAQ title | `fbl-accordion-1-title-3` | 1.125rem | — |

---

## Border radius

```css
--flowblocks-component-library--border-radius--border-radius: 10px;   /* default */
--flowblocks-component-library--border-radius--rounded:       30px;   /* pills suaves */
--flowblocks-component-library--border-radius--round:         500px;  /* circular */
```

---

## Clases de botones y CTAs

| Uso | Clase |
|---|---|
| CTA primario (registro) | `uui-button-2` |
| CTA secundario | `uui-button-secondary-gray-2` |
| CTA con ícono | `fbl-button-icon-23` |
| Botón negro | `fbl-button-black-6` |
| Botón blanco | `fbl-button-white-11` |
| Link button | `uui-button-link-2` |

Todos los `<a>` de botón usan también `w-inline-block` de Webflow.

---

## Clases de estructura de secciones (componentes existentes)

### Hero
```
fbl-hero-19                 → sección hero principal
fbl-hero-19-content         → wrapper de contenido
fbl-hero-19-title           → H1 hero (Montserrat, 4.6rem, color: white)
fbl-hero-3-title-2          → H1 hero variante (small-business)
```

### Features
```
fbl-feature-5               → grid de features 2x2
fbl-feature-5-title         → título de feature
fbl-feature-5-button        → CTA de feature
fbl-feature-7-section-title-2 → H2 de sección de features
fbl-feature-11-*            → features con imagen lateral
fbl-bentogrid-1-*           → bento grid de features
```

### FAQ / Accordion
```
fbl-accordion-1-items-3     → contenedor de todas las preguntas
fbl-accordion-1-item-3      → ítem individual
fbl-accordion-1-heading-3   → header clickable del ítem
fbl-accordion-1-title-3     → texto de la pregunta
fbl-accordion-1-content-3   → respuesta (colapsable)
fbl-accordion-icon-plus-3   → ícono + (abierto)
fbl-accordion-icon-minus-3  → ícono − (cerrado)
```

### Spacing helpers
```
fbl-spacing-226             → separador entre sección y FAQ (~24px)
fbl-spacing-227             → separador entre copy y FAQ (~16px)
```

### Fondo de sección
```
fbl-feature-7-bg-2          → background decorativo de sección
```

---

## Colores de fondo por sección (patrón del sitio)

| Sección | Background |
|---|---|
| Hero | `#011131` (navy) o `#032257` (navy profundo) |
| Stats bar | `#00adb1` (teal) o `#003f41` (teal oscuro) |
| Features | `#f9f9f9` (gris claro) o `#fff` |
| "Lo que tu banco no puede darte" | `#f5f9fc` (light-grey) |
| FAQ | `#fff` |
| Sección interlinking | `#ecfdf3` (verde muy claro) |
| CTA final / Registro | `#011131` (navy) |

---

## CSS externo de referencia (NO incluir en Webflow — ya están cargados)

```
https://cdn.prod.website-files.com/68ffa900bd486e7d9f3183da/css/lara-test-afe7c8.shared.79e2d9b62.min.css
https://cdn.prod.website-files.com/68ffa900bd486e7d9f3183da/css/lara-test-afe7c8.69714bd40f5eea3a46cdcf96.e1c0b78d2.opt.min.css
```
