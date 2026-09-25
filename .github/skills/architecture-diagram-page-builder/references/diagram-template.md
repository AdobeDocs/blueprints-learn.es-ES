---
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%
---
# Plantilla de página de diagrama de arquitectura

Esta es la plantilla de Markdown completa para una página de diagrama de arquitectura. Reemplazar cada `{placeholder}` por el valor recopilado durante la fase 1 del flujo de trabajo de aptitudes. Elimine cualquier sección opcional que no se aplique (por ejemplo, el bloque `>[!MORELIKETHIS]`): no deje marcadores de posición vacíos en el archivo generado.

&#x200B;---

```markdown
---
title: {Page title}
description: {1-2 sentence page purpose, used for search snippets and previews}
solution: {Comma-separated Adobe solutions, e.g. Experience Platform, Journey Optimizer, Customer Journey Analytics}
---
# {Page title}

{Opening paragraph -- 1-2 sentences describing what the diagrams collectively illustrate. Frame the page as a top-level architecture reference, not a use case walkthrough.}

>[!MORELIKETHIS]
>
>[{Related-content link text}]({Related-content URL}).

## {Diagram 1 section title}

{1-2 sentence explanation of what the diagram shows and why it matters.}

![{Alt text for diagram 1}](assets/{filename-1}){width="1000" zoomable="yes"}

## {Diagram 2 section title}

{1-2 sentence explanation.}

![{Alt text for diagram 2}](assets/{filename-2}){width="1000" zoomable="yes"}

## Primary data flows and integration points

- {Flow or integration 1 -- e.g., "Real-time event ingestion from [!DNL Web SDK] to [!DNL Edge Network]"}
- {Flow or integration 2 -- e.g., "Profile sync between [!DNL Experience Platform] Hub and Edge"}
- {Flow or integration 3}
- {Flow or integration 4}
- {Flow or integration 5}

## Use case patterns supported

The architecture above supports the following use case patterns:

- [{Pattern 1 name}](/help/blueprints/use-case-patterns/{category}/{pattern-1-file}.md) -- {1-line note on why this architecture enables the pattern}
- [{Pattern 2 name}](/help/blueprints/use-case-patterns/{category}/{pattern-2-file}.md) -- {1-line note}
- [{Pattern 3 name}](/help/blueprints/use-case-patterns/{category}/{pattern-3-file}.md) -- {1-line note}

## Further reading

- [{Article 1 title}]({Experience League URL 1})
- [{Article 2 title}]({Experience League URL 2})
- [{Article 3 title}]({Experience League URL 3})
```

&#x200B;---

## Reglas de Frontmatter

- **Campos obligatorios:** `title`, `description`, `solution`.
- **Campos prohibidos** (asignados automáticamente a la hora de publicación): `exl-id`, `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt`, `thumbnail`. No los incluya en los archivos que acaba de crear.

## Convenciones del cuerpo

- **Un H1**: el título de la página. Coincide exactamente con el frontmatter `title`.
- **Un H2 por diagrama.** No hay H3 dentro de las secciones del diagrama; manténgalas en una introducción de 1-2 frases más la imagen.
- **Incrustar imagen de Markdown**: proporcione texto alternativo descriptivo y use `{width="1000" zoomable="yes"}` para diagramas.
- **Ruta de la imagen** — siempre `assets/{filename}` (relativa a la carpeta de temas de la página). No utilice rutas absolutas.
- **nombres de productos Adobe** — ajuste `[!DNL ...]` en el texto del cuerpo y las viñetas. Ejemplo: `[!DNL Real-Time CDP]`, `[!DNL Journey Optimizer]`, `[!DNL Experience Platform]`.
- **Vínculos de patrones de casos de uso**: utilice siempre el formulario `/help/blueprints/use-case-patterns/{category}/{file}.md` absoluto para que el vínculo se resuelva desde cualquier página que pueda incluir este contenido.
- **vínculos de Experience League**: direcciones URL absolutas que comienzan por `https://experienceleague.adobe.com/es`. Prefiera la URL del documento canónico sobre una variante localizada.

## Ordenación de secciones

Mantenga el orden coherente en todas las páginas de arquitectura para que los lectores puedan analizar de forma predecible:

1. Frontmatter
2. H1 + párrafo de apertura
3. Llamada `>[!MORELIKETHIS]` (opcional)
4. Un H2 por diagrama (en el orden especificado por el usuario)
5. `## Use case patterns supported`
6. `## Primary data flows and integration points`
7. `## Further reading`

## Expectativas de longitud

Entre 40 y 100 líneas de markdown es típico. Si la página supera las 150 líneas, es probable que el contenido se haya desplazado al territorio de patrones de casos de uso: vuelva a comprobar `scope-guardrails.md` y considere la posibilidad de dividir.
