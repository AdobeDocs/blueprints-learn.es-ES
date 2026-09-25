---
source-git-commit: c766cd3153efce4635089d008daf3eb426eb7a24
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%
---
# Convenciones de nomenclatura: Diagramas y modelos de arquitectura

Este documento es la fuente fiable sobre cómo se asignan los nombres a las categorías de `+ Architecture Diagrams and Blueprints{#architecture-diagrams}`. Tanto la aptitud `architecture-diagram-category-builder` (nuevas categorías) como la aptitud `architecture-diagram-page-builder` (nuevas páginas dentro de categorías existentes) deben seguir estas reglas.

## La regla

**Nombre de carpeta = slug de anclaje de TDC = kebab-case de la etiqueta de TDC completa.** Los tres deben coincidir exactamente, sin abreviaturas ni truncaciones.

| Etiqueta de TDC | Anclaje | Carpeta |
| --- | --- | --- |
| Información general de arquitectura | `#architecture-overviews` | `architecture-overviews/` |
| Activación de audiencias y perfiles | `#audience-profile-activation` | `audience-profile-activation/` |
| Activación y marketing B2B | `#b2b-activation-marketing` | `b2b-activation-marketing/` |
| Customer Insights | `#customer-insights` | `customer-insights/` |
| Recorridos del cliente | `#customer-journeys` | `customer-journeys/` |

Este es el estado actual y corregido de las cinco categorías (a partir del 16 de septiembre de 2026). Anteriormente en el historial de este repositorio, algunos de estos elementos se abreviaban (`architecture-overview`, `audience-activation`, `b2b-activation`); esa incoherencia se ha corregido. No vuelva a introducir nombres abreviados de carpeta/anclaje para categorías nuevas o existentes.

## Por qué esto importa

- **Previsibilidad.** Un colaborador (humano o agente) debe poder adivinar la ruta de la carpeta desde la etiqueta del índice y viceversa, sin abrir TOC.md.
- **Automatización segura.** Las habilidades y los scripts que generan rutas a partir de etiquetas (o etiquetas a partir de rutas) solo funcionan de forma fiable cuando la asignación es exacta y mecánica (caso de uso de kebab, sin abreviatura).
- **Redirigir higiene.** Cada cambio de nombre requiere nuevas entradas en `redirects.csv`. Mantener los nombres estables y totalmente descriptivos desde el principio evita la pérdida repetida de nombres.

## Cómo derivar un slug de una etiqueta

1. Ponga la etiqueta en minúsculas.
2. Suelte `&` por completo y una las palabras que lo rodean con un guión (por ejemplo, `Audience & Profile Activation` -> `audience-profile-activation`).
3. Reemplace los espacios por guiones.
4. Puntuación de franja distinta a los guiones.
5. No abrevie, trunque ni suelte palabras de la etiqueta (no `b2b-activation` para &quot;Activación y marketing B2B&quot; — use `b2b-activation-marketing`).

## Recursos necesarios por categoría

Cada carpeta de categoría directamente debajo de `help/blueprints/architecture-diagrams/` debe contener:

1. **`overview.md`**: una página de aterrizaje para la categoría. Consulte `./category-overview-template.md` para obtener la estructura requerida. Cada página de información general de categoría debe tener el mismo aspecto: párrafo(s) de introducción, luego una sola tabla `| Diagram | Description |` que enumere todas las páginas de la categoría (en orden de tabla de contenido). No utilice celdas `<ul><li>` anidadas, imágenes de diagrama incrustadas o una tercera columna, para que coincidan exactamente con las cinco categorías existentes.
2. **`assets/`** — carpeta para imágenes de diagrama, incluso si está vacía en el momento de la creación (créela una vez que se haya agregado el primer diagrama).

## Requisitos de TOC.md

- La entrada `+ [Overview](/help/blueprints/architecture-diagrams/{folder}/overview.md)` de la categoría siempre es la entrada **first** bajo el encabezado de categoría, antes de cualquier página de contenido.
- El encabezado de categoría y su anclaje se encuentran inmediatamente debajo de `+ Architecture Diagrams and Blueprints{#architecture-diagrams}`, en el mismo nivel de sangría de 2 espacios que las otras cinco categorías.
- Las páginas de contenido tienen una sangría de 4 espacios (`+` con el prefijo cuatro espacios iniciales). A las subagrupaciones anidadas (por ejemplo, la agrupación de RTCDP en Activación de audiencia y perfil) se les aplica una sangría de 6 espacios.

## Requisitos de página de aterrizaje

`help/blueprints/architecture-diagrams/overview.md` (la página de aterrizaje Diagramas de arquitectura y modelos de nivel superior) debe tener exactamente una tarjeta por categoría, en orden de TDC. Cada tarjeta:

- Vínculos a `overview.md` de la categoría (no una página de contenido).
- Utiliza una imagen de diagrama representativa de la carpeta `assets/` de esa categoría como miniatura, con el estilo CSS de tarjeta estándar (`background-color:#ffffff; border:1px solid #d3d3d3;` más las reglas de relleno o tamaño compartidas que ya se encuentran en el archivo).
- Incluye el nombre de la categoría (negrita/strong) y una descripción de una frase que coincide con la introducción de la descripción general de la categoría.

Cuando el número de categorías es múltiplo de 3, la tabla se procesa como filas completas limpias (3 columnas, `table-layout:fixed`, `width:33%` por celda). Si no es un múltiplo de 3, agregue un(a) `<td>` vacío por cada ranura que falte en la última fila (no deje la tabla fragmentada/sin estilo).
