# Plantilla NoExpertise · Reformas de baños y cocinas

Web luminosa para quien reforma baños y cocinas: packs con precio, obras hechas, financiación y WhatsApp.

- Sectores: reformas, baños, cocinas, reformas integrales, interiorismo y reformas. Estilo: limpio. Plan mínimo: gratis.
- Secciones: hero, packs, trabajos, proceso, materiales, financiacion, zonas, opiniones, preguntas, presupuesto, contacto (+ `texto` para apartados nuevos).
- Campos propios: `hero.destacado` (nota de quién hace la obra) y `hero.items` (garantías); `packs.packs[]` (`nombre, texto, precio, incluye` con «;», `duracion, destacado`) + `packs.etiqueta_destacado` y `boton_pack` opcional; `trabajos.trabajos[]` (`titulo, tipo, lugar, texto, imagen`, `imagen_antes` opcional) + `etiqueta_antes`; `materiales.items[]` (`titulo, texto, imagen`); `financiacion.items[]` + `financiacion.nota`; `presupuesto.nota` y `presupuesto.boton_formulario`.
- Para autónomos: textos en primera persona, botón de WhatsApp en la cabecera y en la portada, barra fija «Llamar / WhatsApp» en móvil y formulario de presupuesto corto (nombre, teléfono, qué necesitas).
- Ejemplo: Rubén Carrasco Reformas, reformas de baños y cocinas en Móstoles y el sur de Madrid (negocio ficticio).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (con `areaServed` desde `zonas`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) dibujadas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.packs.packs` con `detalle` tiene su página en `/reformas/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Cada zona de `secciones.zonas.items` con `texto` tiene su página en `/zonas/<slug>/` (`src/pages/zonas/[slug].astro`); en la sección, `titulo_pagina` y `texto_pagina` con {zona} y {negocio}.
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
