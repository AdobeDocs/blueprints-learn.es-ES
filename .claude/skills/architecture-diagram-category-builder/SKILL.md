---
name: architecture-diagram-category-builder
description: 'Creación de guías de una nueva categoría de nivel superior (subsección) en Diagramas de arquitectura y modelos en el repositorio de modelos de Adobe Experience Platform. Utilice esta aptitud cuando un diagrama de arquitectura propuesto no se ajuste a ninguna de las categorías existentes (descripciones generales de arquitectura, activación de audiencia y perfil, activación y marketing B2B, perspectivas del cliente, recorridos del cliente) y se necesite uno nuevo. Gestiona el flujo de trabajo completo: confirmar una nueva categoría está realmente justificado, aplicar las convenciones de nomenclatura de carpetas/anclajes, crear la estructura de carpetas y la página de aterrizaje overview.md, agregar la subsección TOC.md y actualizar la cuadrícula de la tarjeta de la página de aterrizaje de los diagramas de arquitectura. Para añadir una página a una categoría *existente*, utilice Architecture-Diagram-Page-Builder en su lugar.'
source-git-commit: c766cd3153efce4635089d008daf3eb426eb7a24
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%
---

# Generador de categorías de diagrama de arquitectura

Esta aptitud guía la creación de una nueva categoría de nivel superior bajo `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` en `/help/blueprints/TOC.md`. Una categoría es una carpeta como `customer-insights/` o `b2b-activation-marketing/`: un grupo de páginas de diagrama de arquitectura relacionadas con su propia página de aterrizaje `overview.md` y su propia subsección de índice.

**Es una operación poco frecuente.** Hay cinco categorías hoy. La adición de un sexto solo debería producirse cuando un dominio de contenido de arquitectura genuinamente nuevo no se ajusta a ninguno existente, no como método abreviado para evitar organizar una página en una categoría existente.

## Lectura requerida antes de comenzar

- `./references/naming-conventions.md`: la regla de nomenclatura de carpeta/anclaje/etiqueta y por qué importa. Lea esto a fondo; es la única fuente fiable sobre cómo se deben nombrar las categorías.
- `./references/category-overview-template.md`: la estructura exacta necesaria para `overview.md` de la nueva categoría.
- Si aún no lo ha hecho, también elimine `../architecture-diagram-page-builder/SKILL.md` — una vez que existe la categoría, las páginas individuales dentro de ella se agregan usando esa habilidad, no esta.

## Fase 1: Confirmar que se necesita una nueva categoría

Antes de hacer nada más, enumere las cinco categorías existentes y su ámbito para el usuario:

| Categoría | Carpeta | Ámbito |
| --- | --- | --- |
| Información general de arquitectura | `architecture-overviews/` | Arquitectura de Experience Cloud/Experience Platform de nivel superior, protecciones, SDK de implementación |
| Activación de audiencias y perfiles | `audience-profile-activation/` | Creación y activación de audiencias y perfiles mediante Real-Time CDP, Audience Manager |
| Activación y marketing B2B | `b2b-activation-marketing/` | Activación basada en cuenta, recorridos de grupo de compra, Marketo/Workfront |
| Customer Insights | `customer-insights/` | Customer Journey Analytics y sus integraciones |
| Recorridos del cliente | `customer-journeys/` | Journey Optimizer, Gestión de decisiones, Campaign v7/v8 |

Pida al usuario que confirme que el contenido propuesto no se ajusta a ninguno de estos elementos. Si encaja perfectamente (p. ej., un nuevo diagrama B2B, un nuevo diagrama de personalización), redirija a `architecture-diagram-page-builder` para esa categoría existente en lugar de crear una nueva. Solo continúe con la Fase 2 si el usuario confirma que se garantiza una categoría realmente nueva.

## Fase 2: Recopilar información de categoría

Utilice un formulario de preguntas para recopilar, en una ronda:

1. **Etiqueta de categoría**: la etiqueta de índice legible en lenguaje natural (p. ej. &quot;Arquitectura de Commerce&quot;, no una abreviatura). Presente 2-3 frases sugeridas más &quot;Otro&quot;.
2. **Descripción de una frase**: lo que cubre esta categoría, para el contenido principal de `overview.md` y la tarjeta de la página de aterrizaje.
3. **Solución(s) Adobe principal(es)** — para el campo de `solution` de frontmatter.
4. **Páginas iniciales**: ¿el usuario ya tiene más de una página lista para colocarla en esta categoría o solo está andamiando la categoría para que las páginas sigan más tarde?

Derive el nombre de la carpeta y el anclaje de la etiqueta de categoría mediante la regla de slug en `./references/naming-conventions.md` (en minúsculas, soltar `&`, guiones, sin abreviatura). Muestre al usuario la carpeta o anclaje derivado y confirme antes de continuar: este es el único detalle que resulta costoso de corregir más adelante.

## Fase 3: Crear la estructura de carpetas

```
help/blueprints/architecture-diagrams/{new-folder}/
help/blueprints/architecture-diagrams/{new-folder}/assets/
help/blueprints/architecture-diagrams/{new-folder}/overview.md
```

Generar `overview.md` mediante `./references/category-overview-template.md`. Si el usuario tiene las páginas iniciales listas, muéstrelas ahora en la tabla (con `architecture-diagram-page-builder` para generar esos archivos de página por sí mismo; esta habilidad solo crea el andamio de categorías y su página de información general, no páginas de diagramas individuales). Si no existe ninguna página todavía, la tabla puede estar vacía o omitirse hasta que se agregue la primera página: tenga en cuenta esto al usuario en lugar de inventar filas de marcador de posición.

La carpeta `assets/` puede estar vacía en el momento de la creación; existe por lo que la primera página de diagrama agregada a la categoría tiene un lugar donde colocar sus imágenes.

## Fase 4: Agregar la subsección TOC.md

Inserte la nueva categoría como una entrada de nivel superior bajo `+ Architecture Diagrams and Blueprints{#architecture-diagrams}`, colocada después de la última categoría existente a menos que el usuario especifique lo contrario:

```
  + {Category Label}{#{folder-slug}}
    + [Overview](/help/blueprints/architecture-diagrams/{new-folder}/overview.md)
    + [{Page title}](/help/blueprints/architecture-diagrams/{new-folder}/{filename}.md)
```

Reglas:

- Sangría de 2 espacios para el encabezado de la categoría, que coincide con los otros cinco.
- El anclaje `{#{folder-slug}}` debe coincidir exactamente con el nombre de la carpeta (consulte nomenclatura-convenciones.md).
- `+ [Overview]` es siempre la primera entrada, con una sangría de 4 espacios, antes de cualquier página de contenido.
- Conservar el orden y el contenido existentes de todas las demás entradas de TOC.md: insertar, no reordenar ni volver a escribir sólo secciones no relacionadas.

## Fase 5: Actualizar la página de aterrizaje de Diagramas de arquitectura y modelos

Agregue una tarjeta nueva a `help/blueprints/architecture-diagrams/overview.md`, en la misma cuadrícula de `<table style="table-layout:fixed; width:100%;">` utilizada por las otras cinco tarjetas. La nueva tarjeta:

- Vínculos a `{new-folder}/overview.md`.
- Utiliza una miniatura de diagrama representativa de `{new-folder}/assets/` (o una nota de marcador de posición neutro si todavía no existe ningún diagrama; márquela para el usuario en lugar de inventar una ruta de acceso a la imagen).
- Utiliza el mismo bloque de estilo en línea que las tarjetas existentes (`width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;` en la imagen, `min-height:100px;` en el div de texto).

**Volver a calcular el diseño de cuadrícula.** Las cinco tarjetas existentes rellenan una cuadrícula de tres columnas (dos filas, una celda vacía final). Si agrega una sexta tarjeta, se rellena exactamente esa celda vacía, no es necesario cambiar el diseño. Si esta es la categoría 7.ª, 8.ª, etc., agregue un nuevo(a) `<tr>` con las nuevas tarjetas y rellene las celdas vacías restantes de esa fila con los elementos `<td style="width:33%; ...;"></td>` en blanco para que la fila no se muestre irregular.

## Fase 6: Validación

Confirmar e informar al usuario:

1. **Uniformidad de nombres**: el nombre de carpeta, el anclaje del índice y el slug de etiqueta de categoría son idénticos (por convención de nomenclatura.md).
2. **overview.md structure** — coincide con `category-overview-template.md` (tabla de introducción + `Diagram | Description` de dos columnas, sin imágenes incrustadas ni listas anidadas en la tabla).
3. **Ubicación de TOC.md**: la nueva subsección se encuentra en Diagramas y modelos de arquitectura, `+ [Overview]` es la primera, la sangría es correcta y no se modificaron otras entradas.
4. **Tarjeta de página de aterrizaje**: se agregó en la posición de cuadrícula correcta, usa el estilo de tarjeta estándar y vincula al nuevo `overview.md`.
5. **Redirecciones**: si esta categoría consolida o cambia el nombre del contenido que antes vivía en otra parte (poco frecuente para una categoría completamente nueva, pero marca), agregue entradas a `redirects.csv` siguiendo el formato de `source,dest` existente que se usaba para los cambios de nombre de diagramas de arquitectura anteriores.

Corrija los problemas de validación antes de considerar que la tarea se ha completado.

## Notas

- Si el usuario cambia posteriormente el nombre de una categoría (etiqueta, carpeta o anclaje), se trata de una operación de cambio de nombre, no de una operación de nueva categoría (siga la regla namespace-convenciones.md para el nuevo nombre, actualice todos los vínculos internos (TOC.md, tanto las páginas de información general como los vínculos relativos del mismo nivel y los documentos de aptitudes) y añada entradas de redirección. Trátelo del mismo modo en que se han gestionado anteriormente los cambios de nombre de categoría en este repositorio: `git mv` la carpeta y, a continuación, una búsqueda y sustitución de toda la repo de los antiguos formularios de ruta de acceso, nunca una sustitución de cadena global ciega que pudiera chocar con direcciones URL externas no relacionadas (por ejemplo, `experienceleague.adobe.com/docs/experience-platform/...` vínculos de documentación de producto).
- Mantenga esta aptitud y `architecture-diagram-page-builder` sincronizados: si la tabla de asignación de subsecciones de `references/toc-placement.md` de `architecture-diagram-page-builder` aún no enumera la nueva categoría, agréguela allí también.
