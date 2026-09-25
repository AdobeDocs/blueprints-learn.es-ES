---
source-git-commit: c766cd3153efce4635089d008daf3eb426eb7a24
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%
---
# Referencia de ubicación de TOC.md

Cuando la aptitud genera una nueva página de diagrama de arquitectura, debe agregar una entrada a `/help/blueprints/TOC.md` para que la página se pueda detectar en la navegación del sitio. Este documento define exactamente dónde y cómo va esa entrada.

## Sección principal

Todas las páginas del diagrama de arquitectura se encuentran en la sección `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` de nivel superior de TOC.md. Dentro de esa sección, varias subsecciones agrupan las páginas por temas.

Los nombres de carpeta, los delimitadores de tabla de contenido y las etiquetas de tabla de contenido de estas subsecciones deben seguir la regla de nomenclatura de `../../architecture-diagram-category-builder/references/naming-conventions.md`; vea ese archivo si alguna vez se necesita una nueva categoría (use la habilidad `architecture-diagram-category-builder` para eso, no esta).

## Asignación de subsecciones

Elija la subsección que coincida con la carpeta de temas de la nueva página:

| Carpeta de temas | Encabezado de subsección del índice |
| --- | --- |
| `architecture-diagrams/architecture-overviews/` | `+ Architecture overviews{#architecture-overviews}` |
| `architecture-diagrams/audience-profile-activation/` | `+ Audience & Profile Activation{#audience-profile-activation}` |
| `architecture-diagrams/b2b-activation-marketing/` | `+ B2B activation & marketing{#b2b-activation-marketing}` |
| `architecture-diagrams/customer-insights/` | `+ Customer Insights{#customer-insights}` |
| `architecture-diagrams/customer-journeys/` | `+ Customer journeys{#customer-journeys}` |

Si el usuario propone una carpeta de temas que no está en esta tabla, trátela como una nueva subsección de nivel superior y pause (pídale al usuario que confirme si desea crearla). No invente silenciosamente una nueva subsección.

## Formato de entrada

```
    + [{Page title}](/help/blueprints/{topic-folder}/{filename}.md)
```

Reglas:

- **Sangría:** exactamente cuatro espacios, luego `+ `. El analizador del índice depende de esto; las tabulaciones o el espaciado diferente interrumpirán la navegación.
- **Texto del vínculo:** el título de la página, que coincide exactamente con el frontmatter de `title`. Use `[!DNL ...]` solo si los elementos del mismo nivel de la misma subsección lo usan (coincide con la convención local).
- **Destino del vínculo:** ruta absoluta que comienza por `/help/blueprints/`. Incluya siempre la extensión `.md`.
- **Posición:** anexar como la última entrada en la subsección coincidente a menos que el usuario especifique una posición diferente. Conservar el orden existente de todas las entradas del mismo nivel.

## Subsecciones anidadas

`+ Architecture overviews{#architecture-overviews}` no tiene agrupaciones anidadas: todas las páginas de `architecture-diagrams/architecture-overviews/` (incluidas las páginas de implementación de SDK, como `websdk.md`, `appsdk.md`) se sientan en el mismo nivel de sangría de cuatro espacios. Otras subsecciones (`Audience & Profile Activation`, `B2B activation & marketing`, etc.) puede contener agrupaciones anidadas: revise la sección antes de colocar la entrada. Si hay una agrupación anidada y la nueva página pertenece a ella, aplique sangría a dos espacios adicionales; de lo contrario, coloque la entrada en el nivel superior de la subsección.

## Ejemplos trabajados

### Ejemplo 1 — página de AEP de nivel superior

- Carpeta de temas: `architecture-diagrams/architecture-overviews/`
- Nombre de archivo: `mix-modeler-integration.md`
- Título de página: `Adobe Mix Modeler integration with Experience Platform`

Entrada:

```
    + [Adobe Mix Modeler integration with Experience Platform](/help/blueprints/architecture-diagrams/architecture-overviews/mix-modeler-integration.md)
```

Colocado en `+ Architecture overviews{#architecture-overviews}`.

### Ejemplo 2 — Arquitectura de recorrido de AJO

- Carpeta de temas: `architecture-diagrams/customer-journeys/`
- Nombre de archivo: `cross-channel-journey-architecture.md`
- Título de página: `Cross-channel journey architecture`

Entrada:

```
    + [Cross-channel journey architecture](/help/blueprints/architecture-diagrams/customer-journeys/cross-channel-journey-architecture.md)
```

Colocado en `+ Customer journeys{#customer-journeys}`.

### Ejemplo 3: página de implementación de SDK

- Carpeta de temas: `architecture-diagrams/architecture-overviews/`
- Nombre de archivo: `mobile-sdk-architecture.md`
- Título de página: `Mobile SDK deployment architecture`

Entrada (la misma sangría de cuatro espacios que en otras páginas de descripción general de arquitectura):

```
    + [Mobile SDK deployment architecture](/help/blueprints/architecture-diagrams/architecture-overviews/mobile-sdk-architecture.md)
```

Colocado en `+ Architecture overviews{#architecture-overviews}`.

## Verificación

Después de editar TOC.md, vuelva a leer la subsección afectada y confirme lo siguiente:

1. La nueva entrada utiliza exactamente cuatro espacios de sangría (o seis si están anidados en una agrupación específica de subsección, por ejemplo, la agrupación RTCDP de `Audience & Profile Activation`).
2. El destino del vínculo coincide con la ruta de acceso del archivo en el disco, incluida la extensión `.md`.
3. La entrada se agrupa dentro de la subsección correcta, no flotando entre subsecciones.
4. No se reordenó ni modificó ninguna entrada existente.
