---
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 48%

---
# Plantilla de patrón de caso de uso

Este archivo contiene la plantilla Markdown completa para una página de patrones de casos de uso. Reemplazar todos los `{{placeholder}}` valores con contenido real al generar un nuevo patrón.

---

## Plantilla

````markdown
---
title: {{Pattern Title}}
description: {{One-sentence description of what this pattern teaches}}
solution: {{Comma-separated Adobe solutions}}
exl-id: {{generate-uuid-placeholder}}
---
# {{Pattern title}}

This guide provides an overview of {{pattern name}} using {{solutions with [!DNL ...] formatting}}. It is designed for solution architects, marketing technologists, and implementation engineers who need to {{primary capability description}}.

## Use case pattern

**{{Pattern Name}}**

{{One-two sentence description of what the pattern does and enables.}}

**Execution plan:** {{Step 1}} > {{Step 2}} > {{Step 3}} > {{Step 4}} > {{Step 5}}

## Use case overview

{{Paragraph 1: Define the pattern. What does it do? How does it differ from related patterns? Provide a clear, specific definition.}}

{{Paragraph 2: Describe the typical trigger or starting condition. When does this pattern apply? What event, schedule, or condition initiates it?}}

{{Paragraph 3: Describe what the pattern delivers. What is the end result for the customer or business? What channels or touchpoints does it affect?}}

{{Paragraph 4: Clarify scope boundaries. What does this pattern NOT cover? What adjacent patterns handle those needs? Reference other patterns by name if relevant.}}

{{Paragraph 5 (optional): Identify typical stakeholders and teams involved in implementation. Who owns what?}}

## Key business objectives

The following business objectives are supported by this use case pattern.

**[{{Objective Name}}](../../business-objectives/{{category}}/{{objective-file}}.md)**

{{Brief description of how this pattern supports the objective -- 1-2 sentences.}}

| KPIs |
| --- |
| {{KPI1}}, {{KPI2}}, {{KPI3}} |

{{Repeat the above block for each supported business objective.}}

## Example tactical use cases

The following scenarios illustrate how {{pattern name}} can be applied across different business contexts.

- **{{Scenario name}}** -- {{Description of the scenario and how it uses this pattern}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
{{Include 6-10 scenarios total}}

## Key performance indicators

| KPI | Description | Measurement |
| --- | --- | --- |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |

## Applications

The following Adobe applications are used in this use case pattern.

- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}
- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}
- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}

## Related documentation

The following resources provide additional detail on the capabilities used in this pattern. Group the reference links to primary Experience League documents under descriptive subheadings.

### {{Topic group}}

- [{{Link text}}]({{URL}})
- [{{Link text}}]({{URL}})

### {{Topic group}}

- [{{Link text}}]({{URL}})
- [{{Link text}}]({{URL}})
````

---

## Notas sobre el uso de esta plantilla

- **Frontmatter de YAML:** `exl-id` debe ser un UUID de marcador de posición (por ejemplo: `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`). La canalización de publicación asigna el valor real.
- **Orden de sección:** La sección `Use case pattern` se produce inmediatamente después de la introducción de apertura, antes de `Use case overview`. Ofrece a los lectores una definición nítida y de una línea y el plan de ejecución de alto nivel por adelantado.
- **Nombres de productos de Adobe:** Utilice siempre la sintaxis `[!DNL ...]` para los nombres de productos de Adobe en texto independiente y tablas (por ejemplo, `[!DNL Journey Optimizer]`). Esta es una convención de Experience League que impide la traducción de nombres de productos.
- **Vínculos de objetivos empresariales:** Use rutas relativas del archivo de patrones al directorio de objetivos empresariales: `../../business-objectives/{{category}}/{{filename}}.md`.
- **Nombres de archivo en mayúsculas y minúsculas:** El nombre de archivo del patrón debe ser en mayúsculas y minúsculas derivado del título del patrón. Ejemplo: &quot;Mensajería activada por eventos&quot; se convierte en `event-triggered-messaging.md`.
- **Plan de ejecución:** Use ` > ` (espacio, mayor que, espacio) como separador entre pasos. Mantenga la etiqueta exactamente `**Execution plan:**`.
- **Documentación relacionada:** Vínculos de referencia de grupo en subtítulos descriptivos de `###` (por ejemplo, por aplicación o área de capacidad). Estas son las referencias de Experience League para las aplicaciones y funcionalidades utilizadas en el patrón.
- **Arquitectura (opcional):** Si un patrón se beneficia de un diagrama de arquitectura de referencia, se puede colocar una sección `## Architecture` opcional entre `Applications` y `Related documentation`.
- **Ámbito:** Esta plantilla excluye intencionalmente secciones de implementación detalladas (funcionalidades básicas/de soporte/de aplicación, requisitos previos, opciones de implementación y pasos de implementación por fases). Estos detalles se encuentran en la documentación de Experience League vinculada desde `Related documentation`.