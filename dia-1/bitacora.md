# Bitácora · Semana 2 · Día 1 — Rueda Libre v1.5

## MiniReto 1 — Encabezado, menú y pie con Flexbox

**¿A qué ancho aprox. el menú empezó a bajar de línea?**
Más o menos a los **570 px**. Con menos ancho, el logo (240 px) y los 3 enlaces ya no caben juntos.

**¿Qué pasó con logo y menú?**
En pantalla ancha el logo queda a la izquierda y el menú a la derecha, centrados entre sí. Al estrechar, primero se acercan (el `gap` evita que se peguen) y a los 570 px el menú baja debajo del logo gracias a `flex-wrap: wrap`. Los enlaces no se salen de la pantalla.

**¿Qué pasó con los 3 bloques del pie?**
Van en fila (Marca, Contacto, Horario) y quedan alineados por arriba. Cuando el ancho baja de unos **680 px** el bloque de Horario baja a una segunda fila, y más abajo (unos 450 px) cada bloque queda en su propia línea.

Lo que cambié: `header` y `footer` con `display: flex`; el menú con `gap` y sin `margin` ni `inline-block` en los `li`; y el pie ahora tiene 3 bloques en las 3 páginas.

## MiniReto 2 — La flota con Grid

Usé `grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr))` y `gap: var(--esp-m)`, sin ninguna media query. Dentro de cada tarjeta usé Flexbox en columna y `margin-top: auto` en el botón para que "Reservar" quede siempre abajo.

| Ancho de pantalla | Columnas que veo |
|---|---|
| 1280 px | 3 |
| 900 px | 3 |
| 500 px | 1 |

El Tándem (7.º modelo) entró solo, sin tocar el CSS.

## MiniReto 3 — Layout en dos dimensiones

| Parte | ¿Flexbox o Grid? | Por qué |
|---|---|---|
| Portada (texto + foto) | Grid | Son 2 columnas con proporción `1fr 1fr` y el texto centrado en vertical: columnas y filas a la vez. |
| Galería de rutas | Grid | 3 tarjetas iguales en columnas `repeat(3, 1fr)`. Quiero control del ancho de cada columna. |
| Reservas (formulario + aside) | Grid | La proporción 2:1 se define con `2fr 1fr`; es una cuadrícula de columnas. |
| Fila documento + celular | Grid | Dos campos de igual ancho (`1fr 1fr`). Se podría con Flexbox, pero Grid me da el ancho igual sin `flex: 1`. |
| Encabezado | Flexbox | Solo hay una dimensión (una fila): logo a un lado, menú al otro. |
| Pie de página | Flexbox | Tres bloques en una sola fila que se reparten el espacio y bajan de línea si no caben. |

Regla que usé: si solo reparto elementos en **una fila o una columna**, Flexbox. Si necesito **columnas con proporciones definidas** (o filas y columnas), Grid. Todas las columnas están en `fr`, sin `%` ni `px`.

## MiniReto 4 — Mobile-first (v1.5)

Reescribí el CSS para que lo base sea el celular (una columna) y puse las media queries al final, siempre con `min-width`: **768 px** (tablet) y **1200 px** (escritorio). Solo las usé en portada, galería de rutas, reservas, encabezado, pie, fila de campos y tablas. La flota no necesitó ninguna.

Revisé las 3 páginas a 360, 768 y 1280 px y no hay scroll horizontal en ninguna.

### Problemas que encontré y cómo los resolví

1. **Tablas de tarifas más anchas que la pantalla en 360 px.** La de recorridos tiene 5 columnas. Bajé el `padding` de `th, td` y el tamaño de letra de la tabla en móvil, y los recupero desde 768 px.
2. **Pie con huecos enormes entre bloques en el celular.** Al pasar el pie a columna, el `flex: 1 1 12rem` de cada bloque se aplicaba a la altura y los estiraba. Dejé `flex: none` en móvil y el `flex: 1 1 12rem` solo desde 768 px.
3. **Encabezado amontonado en móvil.** Logo y menú peleaban por la misma línea. En móvil puse `flex-direction: column` y `align-items: center` (logo arriba, menú centrado debajo) y desde 768 px vuelve a fila con `space-between`.
4. **Portada con el texto apretado junto a la imagen.** En móvil la portada es de una sola columna (texto arriba, foto abajo) y las 2 columnas solo empiezan en 768 px.
5. **Fieldset del formulario que puede ensanchar la página.** Por defecto un `fieldset` no se encoge más que su contenido, y los radios en fila lo empujan. Le puse `min-width: 0` para que los radios bajen de línea en vez de salirse.
6. **Botón fijo de WhatsApp tapando contenido.** Por eso el `body` tiene `padding-bottom` grande: al llegar al final, el pie queda libre del botón.

### Publicación

URL de GitHub Pages: https://samintone2106.github.io/html-semana-2/dia-1/reto-4-mobile-first/
