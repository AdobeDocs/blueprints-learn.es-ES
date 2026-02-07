---
name: blueprint-document-reference
description: Referencia para crear y editar documentos de modelo de experiencia digital de Adobe. Se utiliza al crear nuevos modelos, agregar páginas de modelo o cuando el usuario pregunte sobre la estructura del modelo, secciones, plantillas o referencias a Adobe Experience League.
source-git-commit: dfa21942ecf2a1db06df6f6cc945f5572811ca93
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---


# Referencia de documento de modelo

Utilice esta habilidad al crear o editar documentos de modelo en este repositorio. Los modelos son implementaciones repetibles que abordan problemas empresariales establecidos, e incluyen diagramas de arquitectura, consideraciones técnicas y vínculos a la documentación de Adobe Experience League.

## Cuándo se aplica

- Creación de un nuevo documento de modelo o página de información general de modelo
- Adición o reestructuración de secciones en un modelo existente
- Vinculación o referencia a la documentación de Adobe Experience League
- Alineación del nuevo contenido con las convenciones del modelo (contenido previo, encabezados y diagramas)

## Referencia rápida

1. **Propósito del documento**: los modelos proporcionan la arquitectura del sistema y del flujo de datos para mostrar cómo se integran Adobe Experience Platform y las aplicaciones. Son visuales y técnicos, no de marketing.
2. **Secciones**: utilice las secciones estándar de la plantilla; omita solo cuando no corresponda (consulte [reference.md](reference.md)).
3. **Experience League**: prefiere vincular Experience League para documentos de productos, API, protecciones y tutoriales. Use direcciones URL completas; consulte [reference.md](reference.md) para ver patrones y formato de direcciones URL.
4. **Estructura del repositorio**: Los modelos están activos bajo `help/blueprints/`. Actualizar `help/blueprints/TOC.md` al agregar o mover páginas de modelo.

## Plantilla de documento

Cada página de modelo debe seguir esta estructura. Incluya solo las secciones que correspondan.

```markdown
---
title: [Short descriptive title]
description: "[One sentence: what this blueprint shows and why it matters.]"
solution: [Product name, e.g. Real-Time Customer Data Platform, Journey Optimizer]
exl-id: [UUID - leave blank if new, this will be auto-generated as part of the Experience League publishing flow]
---
# [H1 - same as title or expanded]

[1–3 paragraphs: what the blueprint covers, key capabilities, and who it’s for.]

## Applications

* [Product 1]
* [Product 2]

## Use cases

* [Use case 1]
* [Use case 2]

## Prerequisites

[Bullets or short paragraphs: required products, config, or setup.]

## Architecture Diagram

<img src="[path to SVG/image]" alt="[Descriptive alt]" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Guardrails

[Link to Experience League guardrails and any blueprint-specific limits.]

## Implementation patterns

[Optional: named patterns with bullets.]

## Implementation steps

1. [Step with link to Experience League where relevant]
2. ...

## Implementation considerations

[Optional: identity, performance, security, etc.]

## Related documentation

[Grouped links to Experience League: product docs, APIs, tutorials.]
```

Para las páginas de información general o de concentrador, utilice una estructura más corta: introducción, casos de uso (o pestañas), imagen de arquitectura, tabla de escenario/patrón, requisitos previos, protecciones y documentación relacionada. Vea las descripciones generales existentes en `help/blueprints/` para ver ejemplos.

## Frontmatter

| Campo | Requerido | Notas |
|-------|----------|--------|
| `title` | Sí | Corto; usar `[!DNL Product Name]` para nombres de productos por estilo de Adobe |
| `description` | Sí | Una frase; se usa en búsquedas y tarjetas |
| `solution` | Sí | Producto principal (por ejemplo, Real-Time Customer Data Platform, Journey Optimizer) |
| `exl-id` | Sí | UUID; dejar en blanco para las páginas nuevas |
| `doc-type` | Para obtener información general | Usar `overview-page` para las páginas principales de información general de modelo |
| `kt` | Opcional | ID de artículo de la base de conocimiento si está vinculado |

## Referencia a Adobe Experience League

- **Cuándo vincular**: vincule a Experience League para obtener documentación del producto, referencias de API, protecciones, tutoriales y pasos de configuración. No duplique los procedimientos largos; resuma y vincule.
- **Formato de dirección URL**: Use direcciones URL completas. Preferir `https://experienceleague.adobe.com/docs/...` o `https://experienceleague.adobe.com/en/docs/...`. Para documentos de desarrolladores, `https://developer.adobe.com/...` también es válido.
- **Texto del vínculo**: Use texto descriptivo (por ejemplo, &quot;[Crear esquemas](url)&quot; no &quot;Haga clic aquí&quot;). Para los nombres de productos en el texto del vínculo, use `[!DNL Product Name]` cuando corresponda.
- **Sección de documentación relacionada**: finalice modelos con una sección &quot;Documentación relacionada&quot; que agrupe vínculos por categoría (por ejemplo, configuraciones de destino, documentación de SDK, perfil y segmentación, tutoriales).

Para ver patrones de URL detallados, agrupación de vínculos y ejemplos, consulte [reference.md](reference.md).

## Lista de comprobación antes de enviar

- [ ] La materia frontal tiene `title`, `description`, `solution`, `exl-id`
- [ ] H1 coincide o amplía correctamente el título
- [ ] diagrama de arquitectura presente y texto alternativo descriptivo
- [ ] pasos de implementación vinculan a Experience League donde se ejecutan los procedimientos
- [ ] vínculos de la sección de protecciones a documentos oficiales de la protección de Experience League
- [ ] La sección de documentación relacionada incluye enlaces relevantes de Experience League
- [ ] Las páginas nuevas o movidas se reflejan en `help/blueprints/TOC.md`

## Recursos adicionales

- Plantilla completa y notas de sección: [reference.md](reference.md)
- Modelos existentes: `help/blueprints/` (por ejemplo: `audience-activation/real-time-lookup.md`, `customer-journeys/journey-optimizer/journey-optimizer-overview.md`)
- TDC y navegación: `help/blueprints/TOC.md`
