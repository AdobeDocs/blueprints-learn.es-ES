---
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---
# Referencia de ubicación de TOC.md

Cuando la aptitud genera una nueva página de diagrama de arquitectura, debe agregar una entrada a `/help/blueprints/TOC.md` para que la página se pueda detectar en la navegación del sitio. Este documento define exactamente dónde y cómo va esa entrada.

## Sección principal

Todas las páginas del diagrama de arquitectura se encuentran en la sección `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` de nivel superior de TOC.md. Dentro de esa sección, varias subsecciones agrupan las páginas por temas.

## Asignación de subsecciones

Elija la subsección que coincida con la carpeta de temas de la nueva página:

| Carpeta de temas | Encabezado de subsección del índice |
| --- | --- |
| `experience-platform/` | `+ Architecture overviews{#architecture-overview}` |
| `experience-platform/deployment/` | `+ Deployment{#deployment}` (una subsección anidada dentro de `Architecture overviews`) |
| `audience-activation/` | `+ Audience & Profile Activation{#audience-activation}` |
| `b2b/` | `+ B2B activation & marketing{#b2b-activation}` |
| `customer-journey-analytics/` | `+ Customer Journey Analytics{#customer-journey-analytics}` |
| `customer-journeys/` | `+ Customer journeys{#customer-journeys}` |

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

`+ Architecture overviews{#architecture-overview}` contiene un bloque `+ Deployment{#deployment}` anidado para páginas SDK. Si la nueva página se encuentra en `experience-platform/deployment/`, coloque la entrada dentro de `Deployment` con **seis** espacios de sangría:

```
      + [{Page title}](/help/blueprints/experience-platform/deployment/{filename}.md)
```

Otras subsecciones (`Audience & Profile Activation`, `B2B activation & marketing`, etc.) también puede contener agrupaciones anidadas: revise la sección antes de colocar la entrada. Si hay una agrupación anidada y la nueva página pertenece a ella, aplique sangría a dos espacios adicionales; de lo contrario, coloque la entrada en el nivel superior de la subsección.

## Ejemplos trabajados

### Ejemplo 1 — página de AEP de nivel superior

- Carpeta de temas: `experience-platform/`
- Nombre de archivo: `mix-modeler-integration.md`
- Título de página: `Adobe Mix Modeler integration with Experience Platform`

Entrada:

```
    + [Adobe Mix Modeler integration with Experience Platform](/help/blueprints/experience-platform/mix-modeler-integration.md)
```

Colocado en `+ Architecture overviews{#architecture-overview}`.

### Ejemplo 2 — Arquitectura de recorrido de AJO

- Carpeta de temas: `customer-journeys/`
- Nombre de archivo: `cross-channel-journey-architecture.md`
- Título de página: `Cross-channel journey architecture`

Entrada:

```
    + [Cross-channel journey architecture](/help/blueprints/customer-journeys/cross-channel-journey-architecture.md)
```

Colocado en `+ Customer journeys{#customer-journeys}`.

### Ejemplo 3 — Página de SDK de implementación

- Carpeta de temas: `experience-platform/deployment/`
- Nombre de archivo: `mobile-sdk-architecture.md`
- Título de página: `Mobile SDK deployment architecture`

Entrada (observe la sangría de seis espacios):

```
      + [Mobile SDK deployment architecture](/help/blueprints/experience-platform/deployment/mobile-sdk-architecture.md)
```

Colocado bajo `+ Deployment{#deployment}` dentro de `+ Architecture overviews{#architecture-overview}`.

## Verificación

Después de editar TOC.md, vuelva a leer la subsección afectada y confirme lo siguiente:

1. La nueva entrada utiliza exactamente cuatro espacios de sangría (o seis si están anidados en `Deployment`).
2. El destino del vínculo coincide con la ruta de acceso del archivo en el disco, incluida la extensión `.md`.
3. La entrada se agrupa dentro de la subsección correcta, no flotando entre subsecciones.
4. No se reordenó ni modificó ninguna entrada existente.
