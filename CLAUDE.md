# Plantilla «Reformas de baños y cocinas» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **limpio**
(blanco + verde agua + madera clara, bandas a todo el ancho, titulares en serif fina de sistema, botones
rectangulares con esquina de azulejo, juntas de azulejo «metro» en las bandas de agua y oscuras, cota de obra en
los antetítulos, listón de madera en portada, cabecera y pie, fotos de materiales en arco de hornacina). Es la web
de un **autónomo**: habla en primera persona («Soy Rubén…», «te doy un precio cerrado»), y el teléfono y WhatsApp
mandan. Todo en castellano de España, frases cortas, sin jerga. El brief de diseño completo está en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…); `src/styles/global.css` deriva el resto con `color-mix`:
  - `primario` = verde agua: botones en bandas claras, banda del proceso, pack destacado, teléfono grande, barra de móvil.
  - `acento` = madera clara: listones, botones en bandas oscuras, banda de opiniones, etiquetas, números en cursiva.
  - `--hondo` (primario + texto): bandas oscuras (financiación, presupuesto, pie). `--agua` (primario muy claro): packs, formulario. `--madera-suave`: materiales.
  - La letra encima de cada color se calcula sola (`--sobre-primario`, `--sobre-acento`, `--sobre-hondo`: negra si el color es claro, blanca si es oscuro).
- **Tipografías y aspecto general**: `src/styles/global.css` (pilas del sistema: `--fuente-titulos` = "Didot", "Bodoni 72", "Bodoni MT", Cambria… a 400; bandas `.banda-clara/.banda-agua/.banda-madera-suave/.banda-hondo/.banda-primario/.banda-madera`, `.azulejo` (juntas), `.liston`, `.antetitulo` con cota, `.titular-partido`, `.btn`/`.btn-sec`/`.enlace-subrayado`, `.pieza` (icono en azulejo), filas partidas a sangre `.partida`/`.partida-foto`/`.partida-texto`, cabecera `.cabecera-agua`, pie `.pie-agua` y barra fija de móvil). No añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (lista y descripción en `fotos.json`); las de relleno, en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`).
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en un azulejo verde agua con canto de madera + nombre en serif.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Todas son bandas a todo el ancho y pintan bien con listas y campos vacíos.
- `hero` → `hero.astro`: foto a sangre a pantalla completa y panel blanco abajo a la izquierda (toca el borde) con listón de madera: `antetitulo`, `titulo` enorme, `texto`, `cta`, botón de WhatsApp automático (si hay `contacto.whatsapp`) y `cta_secundario` como enlace; `items: [{titulo, icono}]` como garantías; `destacado: {titulo, texto}` = nota de quién hace la obra en una placa oscura sobre la foto. En móvil, foto arriba y panel debajo. La cabecera va transparente encima.
- `packs` → `packs.astro`: banda de agua con juntas; `packs: [{nombre, texto, precio, incluye, duracion, destacado}]` en columnas (3/2/1). `precio` opcional («desde 6.900 €»; vacío no se pinta), `incluye` separado por «;», `destacado: true` en verde agua pleno con `etiqueta_destacado` («El más pedido»). Botón de cada pack: `boton_pack` o el texto del `cta`, hacia `cta.url` (o #presupuesto).
- `trabajos` → `trabajos.astro`: titular y rejilla de fotos de borde a borde con juntas blancas (3/2/1); `trabajos: [{titulo, tipo, lugar, texto, imagen, imagen_antes}]`. `tipo` («Baño», «Cocina») en una pieza de color; `imagen_antes` opcional: miniatura con `etiqueta_antes` («Antes»).
- `proceso` → `proceso.astro`: banda verde agua plena con la cinta métrica de borde a borde; `items: [{titulo, texto, icono}]` numerados en cursiva (en móvil, regla vertical).
- `materiales` → `materiales.astro`: banda de madera suave; `items: [{titulo, texto, imagen}]` como hornacinas (foto en arco), 4/2 columnas.
- `financiacion` → `financiacion.astro`: fila partida con `imagen` a sangre a la izquierda y banda hondo; `items: [{titulo, texto}]` numerados, `nota` (aviso de la entidad) y `cta`. **No pongas plazos ni intereses** que no dé el cliente.
- `zonas` → `zonas.astro`: banda clara; titular a la izquierda y localidades (`items: [{titulo}]`) en serif grande separadas por rombos de madera. `imagen` opcional: franja panorámica a sangre debajo. Las primeras 8 salen también en el pie.
- `opiniones` → `opiniones.astro`: banda de madera; la primera opinión como cita enorme y el resto en dos columnas; `testimonios: [{texto, autor, nota}]`. No inventes opiniones.
- `preguntas` → `preguntas.astro`: titular fijo a la izquierda con teléfono y WhatsApp y acordeón `details/summary` a la derecha. Sin preguntas no se pinta.
- `presupuesto` → `presupuesto.astro`: fila partida: hondo con juntas (titular, `items` como pasos, teléfono grande y `nota`) y agua con el formulario corto (nombre, teléfono, qué necesitas) y el botón de WhatsApp. `boton_formulario` opcional.
- `contacto` → `contacto.astro`: fila partida: titular, teléfono enorme, botón de WhatsApp y datos de `contacto`; `imagen` a sangre a la derecha. Si `presupuesto` no está activa, a la derecha va el formulario corto.
- `texto` → `texto.astro`: apartado genérico (párrafos, `imagen` a sangre a la derecha o banda de agua con juntas, `items`, `cta`). Para apartados nuevos: `tipo: texto`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`. Procura alternar bandas claras y de color (proceso es verde agua, financiación y presupuesto son oscuras, opiniones es madera) y no poner seguidas dos filas partidas con la foto del mismo lado.
3. **Cambiar textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas. Mantén la primera persona (es un autónomo).
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Precios y cifras siempre como texto entre comillas (`"desde 6.900 €"`, `"2 años de garantía"`). `incluye` de los packs: una cadena con «;». Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`. En páginas que no son la portada la cabecera es sólida y deja su hueco sola.
6. **Sección nueva**: mejor un apartado con `tipo:` (`tipo: texto`, `tipo: packs`, `tipo: trabajos`…) y su propio id. Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)` y `Titular`, como una banda a todo el ancho (`seccion banda-…` + `contenedor`, o `partida`). `src/pages/index.astro` la recoge sola: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Los ids `hero` y `contacto` son obligatorios. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (solo hay el de la cabecera), 16 px de margen lateral del texto en móvil (`.contenedor`, `.partida-texto`) con las fotos y fondos tocando el borde, sin scroll horizontal, botones de 44 px o más, barra inferior fija de móvil («Llamar» / «WhatsApp»: sale sola si hay teléfono o WhatsApp). Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
9. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml`. El de presupuesto es corto a propósito (nombre, teléfono, qué necesitas; solo texto). Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. Iconos disponibles: ver `src/components/ui/Icono.astro` (del oficio: `regla, plano, martillo, llave, azulejo, ducha, grifo, cocina, herramienta, documento, escudo, mensaje, casa, euro`…).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento y páginas por zona)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.packs.packs` → `/reformas/<slug>/` (reforma).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Zonas: cada elemento de `secciones.zonas.items` **con `texto`** (60-150 palabras: qué trabajos se hacen allí, pueblos cercanos)
  tiene su página en `/zonas/<slug>/`. En la sección: `titulo_pagina` («Reformas en {zona}») y `texto_pagina` (entrada, con {zona} y {negocio}).
- Una orden «añade una página para X» = escribir su `detalle` (o el `texto` de la zona) en site.yaml. Nunca crees a mano páginas en
  `src/pages/reformas/` ni en `src/pages/zonas/`: salen solas de `src/pages/[coleccion]/[slug].astro` y `src/pages/zonas/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay; zonas con `areaServed`).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "servicios; planes" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella la web pasa a Inicio (hero + lo que no esté en ninguna página) y una página por entrada (`/servicios/`…); el menú se hace solo con las páginas (las entradas `/#…` de `menu` no salen) y los enlaces `/#id` del site.yaml se cambian solos por la dirección de su sección. Sin ella, una sola página larga. Una orden «haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso.
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro` (comunes a todas las plantillas). En un componente, un enlace fijo a una sección va con `enlace('/#contacto')` (de `src/lib/multipagina.ts`).
