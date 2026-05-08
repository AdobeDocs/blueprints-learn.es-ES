---
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '234'
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

<img src="assets/{filename-1}" alt="{Alt text for diagram 1}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## {Diagram 2 section title}

{1-2 sentence explanation.}

<img src="assets/{filename-2}" alt="{Alt text for diagram 2}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

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
- **`<img>`incrustado**: se requieren el estilo en línea y `class="modal-image"`. Impulsan la interacción modal-zoom de Experience League.
- **Ruta de la imagen** — siempre `assets/{filename}` (relativa a la carpeta de temas de la página). No utilice rutas absolutas.
- **nombres de productos Adobe** — ajuste `[!DNL ...]` en el texto del cuerpo y las viñetas. Ejemplo: `[!DNL Real-Time CDP]`, `[!DNL Journey Optimizer]`, `[!DNL Experience Platform]`.
- **Vínculos de patrones de casos de uso**: utilice siempre el formulario `/help/blueprints/use-case-patterns/{category}/{file}.md` absoluto para que el vínculo se resuelva desde cualquier página que pueda incluir este contenido.
- **vínculos de Experience League**: direcciones URL absolutas que comienzan por `https://experienceleague.adobe.com/`. Prefiera la URL del documento canónico sobre una variante localizada.

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
