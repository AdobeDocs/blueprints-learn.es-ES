---
source-git-commit: e0ecfa4d74b8fcc0bbaf35d44c33c725a1b1a539
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%
---
# Plantilla de category.overview.md

Cada carpeta de categoría bajo `help/blueprints/architecture-diagrams/` necesita un(a) `overview.md` que se parezca a los otros cinco. Utilice esta estructura exacta.

## Frontmatter

```yaml
---
title: {Category Label}
description: {One-sentence summary of what this category covers.}
solution: {Primary Adobe solution(s), comma-separated}
doc-type: overview-page
---
```

No incluya `exl-id`, `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt` o `thumbnail` en una nueva página: la canalización de publicación los rellena automáticamente.

## Cuerpo

```markdown
# {Category Label}

{1-3 paragraph intro describing what this category of diagrams covers and why it matters.}

| Diagram | Description |
| --- | --- |
| [{Page title}]({filename}.md) | {One-sentence description of the page} |
| [{Page title}]({filename}.md) | {One-sentence description of the page} |
```

Reglas:

- Enumere todas las páginas de la categoría, en el mismo orden en que aparecen en TOC.md.
- Los destinos de vínculo son nombres de archivo relativos (sin prefijo `/help/blueprints/...`), ya que la descripción general se encuentra junto a las páginas del mismo nivel.
- Las descripciones son una frase, no se requiere un punto final si se lee como una etiqueta.
- Si una categoría tiene una subagrupación natural (por ejemplo, &quot;Diagramas obsoletos&quot; en recorridos del cliente), agregue un encabezado `## {Sub-group name}` seguido de su propia tabla de dos columnas en el mismo formato; no mezcle miniaturas de diagrama ni columnas adicionales en la tabla.
- No incruste miniaturas de diagrama `<img>` en esta tabla. Manténgalo en dos columnas: `Diagram` (vínculo) y `Description` (texto). Las miniaturas pertenecen a páginas de contenido individuales, no a la descripción general de la categoría.
- No utilice HTML `<ul><li>` anidado dentro de celdas de tabla. Solo texto sin formato.

## Ejemplo (Customer Insights)

```markdown
---
title: Customer Insights
description: Unify and analyze data and customer behaviors from across the customer journey
solution: Customer Journey Analytics
doc-type: overview-page
---
# Customer Insights

Customer Journey Analytics shows how brands can unify customer data and behavior from various interaction channels and sources to create a journey-based view of all customer interactions.

| Diagram | Description |
| --- | --- |
| [Adobe Customer Journey Analytics](cja.md) | Core Customer Journey Analytics architecture, including B2B and audience-sharing derivations |
| [Adobe Customer Journey Analytics & Adobe Journey Optimizer integration](cja-ajo-integration.md) | Campaign and journey insights integration between Customer Journey Analytics and Journey Optimizer |
```
