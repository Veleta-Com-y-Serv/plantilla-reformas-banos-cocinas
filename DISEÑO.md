# Reformas de baños y cocinas: brief de diseño

Plantilla `reformas-banos-cocinas` creada el 02/11/2026 a partir de `energia-solar` con `php artisan plantillas:nueva`
y rediseñada entera (fila 3 del brief de la tanda 4, «5 plantillas para autónomos»). Este fichero se queda en el
repo: es lo que lee quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: autónomos y equipos muy pequeños que reforman baños y cocinas, cambian bañeras por duchas y hacen
  reformas integrales pequeñas (`sectores`: reformas, banos, cocinas, reformas-integrales, interiorismo-reformas).
  Su cliente es un particular con un baño o una cocina viejos: quiere ver obras terminadas, saber por dónde va el
  precio, cuánto tiempo estará sin baño y que quien entra en su casa es serio, limpio y de la zona.
- **Qué tiene que conseguir la web**: que llamen, escriban por WhatsApp o pidan presupuesto. WhatsApp en la cabecera
  (icono hasta 1280 px), en la portada, en preguntas, presupuesto y contacto; teléfono grande en preguntas,
  presupuesto, contacto y pie; barra fija «Llamar / WhatsApp» en móvil; formulario corto (nombre, teléfono, qué
  necesitas). Los textos en primera persona del singular («Soy Rubén…»): nada de «nuestra empresa».
- **Tono y estilo** (`estilo: limpio`): luminoso, ordenado y cercano. Referencia que sí: losmartesnohayluna.com por
  las bandas a sangre y la tipografía grande; un baño bien alicatado (juntas finas, madera clara, verde agua). Que
  no: la caja centrada con tarjetas blancas; el verde + amarillo sol, los discos y los horizontes curvos de
  `energia-solar` (de la que parte); la sans fina y gris de `arquitectura-interiorismo`; el beige + terracota con
  círculos de `yoga-pilates`; el amarillo obra con diagonales de `reformas-oficios`.
- **Paleta de ejemplo**: primario `#1f7a70` (verde agua), acento `#d2ad84` (madera clara), fondo `#ffffff`, texto
  `#1b2928`. Derivados en `global.css` con `color-mix`: `--hondo` (36 % primario + texto: bandas oscuras),
  `--hondo-2` (velos), `--agua` (9 % primario sobre fondo), `--madera-suave` (20 % acento sobre fondo), `--linea`.
  La letra sobre cada color (`--sobre-primario`, `--sobre-acento`, `--sobre-hondo`) se calcula con oklch; cada
  banda fija su color de botón (`--boton`) y de raya (`--raya`), así el diseño aguanta los cuatro colores del cliente.
- **Tipografía**: del sistema. Títulos en serif fina de alto contraste ("Didot", "Bodoni 72", "Bodoni MT",
  "Hoefler Text", Cambria, Georgia) a 400, interletrado −0,015 em; el del hero llega a 6,4 rem en escritorio
  (2,6 en móvil); cursiva para números de pasos, el 404 y una de cada tres localidades. Antetítulos de 0,78 rem en
  mayúsculas espaciadas (0,2 em) con una **cota** delante (línea de medida con dos topes). Texto en system-ui.
- **Formas y motivos**: botones rectangulares con esquina de azulejo (0,35 rem); **azulejo metro** (juntas finas en
  hilada trabada, máscara SVG pintada con el color de la banda: `.azulejo`) en packs, presupuesto, 404, aviso legal y
  huecos sin foto; **listón de madera** (franja de 6 px con veta: `.liston`) encima del panel del hero, bajo la
  cabecera sólida, en la nota del hero y sobre el pie; **cinta métrica** de borde a borde en el proceso; **arco de
  hornacina** en las fotos de materiales; **juntas blancas** de 6 px entre las fotos de trabajos; iconos dentro de
  una **pieza** (azulejo cuadrado con junta). Marca: inicial en un azulejo verde agua con canto de madera.
- **Ritmo de bandas** (todas de borde a borde; contenido hasta 90 rem, 16 px de margen en móvil):
  1. `hero` — foto del baño a sangre a pantalla completa; panel blanco abajo a la izquierda que toca los bordes
     izquierdo e inferior, con listón de madera; nota «Soy Rubén…» en placa oscura arriba a la derecha. En móvil,
     foto (50 svh) con la nota encima y panel a todo el ancho debajo.
  2. `packs` — agua con juntas; titular partido; tres columnas separadas por juntas, el destacado en verde agua
     pleno con la etiqueta de madera colgando; precio «desde» en serif grande, opcional.
  3. `trabajos` — blanco; titular partido y rejilla de fotos 4:3 de borde a borde (3/2/1) con juntas blancas,
     pieza de tipo arriba, miniatura «Antes» opcional y placa de texto debajo.
  4. `proceso` — verde agua pleno; cinta métrica a todo el ancho y cuatro pasos con número en cursiva.
  5. `materiales` — madera suave; titular centrado y cuatro hornacinas (2 en móvil).
  6. `financiacion` — partida: foto a sangre a la izquierda, hondo a la derecha con filas numeradas y aviso.
  7. `zonas` — blanco; titular a la izquierda y pueblos en serif grande con rombos de madera a la derecha.
  8. `opiniones` — madera plena; cita enorme y dos opiniones en columnas con filetes.
  9. `preguntas` — blanco; titular fijo con teléfono y WhatsApp, acordeón con «+» en pieza de azulejo.
  10. `presupuesto` — partida en dos colores: hondo con juntas (pasos, teléfono, nota) y agua con el formulario corto.
  11. `contacto` — partida: teléfono enorme, WhatsApp y datos a la izquierda; foto de la furgoneta a sangre.
  Pie: hondo con listón arriba y cuatro columnas (marca y teléfono, contacto, web, zonas). Cabecera fija:
  transparente sobre la foto del hero y blanca con listón al bajar (o al abrir el menú). Barra fija de móvil: dos
  azulejos, «Llamar» verde agua y «WhatsApp» hondo.
- **Apartados y listas propias**: `packs.packs` (`nombre, texto, precio, incluye, duracion, destacado`) +
  `etiqueta_destacado`, `boton_pack`; `trabajos.trabajos` (`titulo, tipo, lugar, texto, imagen`, `imagen_antes`) +
  `etiqueta_antes`; `materiales.items` (`titulo, texto, imagen`); `financiacion.items` (`titulo, texto`) + `nota`;
  `hero.destacado` y `hero.items`. Las que salen vacías pintan solo su titular (packs, trabajos, materiales,
  opiniones) o no se pintan (preguntas).
- **Fotos** (`fotos.json`, 14): baño reformado con ducha de obra y madera clara (hero, 21:9), seis trabajos (baño
  de los setenta y su «antes», cocina abierta, ducha en un día, cocina en U verde agua, aseo pequeño, cocina lineal),
  cuatro materiales en vertical (porcelánico, plato extraplano, encimera de cuarzo, madera), mesa con plano y
  muestras (financiación) y furgoneta sin rotular (contacto). Sin texto legible, sin logotipos, sin matrículas ni
  personas. De respaldo, `public/placeholders/` (hero, cocina, material, persona).
- **Qué no hacer**: tarjetas blancas flotando en una caja estrecha; discos, soles y bordes curvos (son de
  `energia-solar`); sans pesada en los títulos; precios, plazos o cifras fijos en los componentes (van en
  `site.yaml`); hablar en plural de empresa; fotos de personas.
