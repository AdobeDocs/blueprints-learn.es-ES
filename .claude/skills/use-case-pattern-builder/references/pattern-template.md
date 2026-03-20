---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

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

This guide provides a comprehensive implementation blueprint for {{pattern name}} using {{solutions with [!DNL ...] formatting}}. It is designed for solution architects, marketing technologists, and implementation engineers who need to {{primary capability description}}.

Use this guide to understand what to configure, where implementation choices exist, and what trade-offs drive each decision.

{{Optional: 1-2 additional introductory sentences about what the guide covers.}}

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

## Use case pattern

**{{Pattern Name}}**

{{One-sentence description of what the pattern does.}}

**Function Chain:** {{Step 1}} > {{Step 2}} > {{Step 3}} > {{Step 4}} > {{Step 5}}

## Applications

The following Adobe applications are used in this use case pattern.

- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}
- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}
- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}

## Foundational functions

The following foundational capabilities must be configured before implementing this pattern. Each function represents a prerequisite or assumed platform capability.

| Foundational Function | Status | What Must Be in Place | Experience League Reference |
| --- | --- | --- | --- |
| {{Function name}} | {{Required / Assumed in Place / Not Applicable}} | {{Description of what must be configured or available}} | [{{Link text}}]({{URL}}) |
| {{Function name}} | {{Required / Assumed in Place / Not Applicable}} | {{Description}} | [{{Link text}}]({{URL}}) |
| {{Function name}} | {{Required / Assumed in Place / Not Applicable}} | {{Description}} | [{{Link text}}]({{URL}}) |
| {{Function name}} | {{Required / Assumed in Place / Not Applicable}} | {{Description}} | [{{Link text}}]({{URL}}) |

## Supporting functions

The following supporting capabilities enhance or extend the pattern but are not strictly required for a basic implementation.

| Supporting Function | Status | Why It Matters | Experience League Reference |
| --- | --- | --- | --- |
| {{Function name}} | {{Recommended / Included / Not Applicable}} | {{Description of why this function matters for this pattern}} | [{{Link text}}]({{URL}}) |
| {{Function name}} | {{Recommended / Included / Not Applicable}} | {{Description}} | [{{Link text}}]({{URL}}) |
| {{Function name}} | {{Recommended / Included / Not Applicable}} | {{Description}} | [{{Link text}}]({{URL}}) |

## Application functions

### [!DNL {{Application Name}}] ({{Abbreviation}})

| Function | Implementation Phase | Description |
| --- | --- | --- |
| {{Function name}} | {{Phase name (e.g., Setup, Configuration, Activation, Optimization)}} | {{Description of what this function does in context}} |
| {{Function name}} | {{Phase name}} | {{Description}} |
| {{Function name}} | {{Phase name}} | {{Description}} |

### [!DNL {{Application Name}}] ({{Abbreviation}})

| Function | Implementation Phase | Description |
| --- | --- | --- |
| {{Function name}} | {{Phase name}} | {{Description}} |
| {{Function name}} | {{Phase name}} | {{Description}} |
| {{Function name}} | {{Phase name}} | {{Description}} |

{{Repeat for each application listed in the Applications section.}}

## Prerequisites

Complete the following before beginning the implementation.

- [ ] {{Prerequisite item -- e.g., "XDM schemas for behavioral and profile data are defined and deployed"}}
- [ ] {{Prerequisite item -- e.g., "Datastreams are configured for web and/or mobile properties"}}
- [ ] {{Prerequisite item -- e.g., "Identity namespaces are defined and identity resolution rules are configured"}}
- [ ] {{Prerequisite item -- e.g., "Merge policies are configured for the target profile dataset"}}
- [ ] {{Prerequisite item -- e.g., "Required Adobe product licenses are provisioned and sandbox access is granted"}}
- [ ] {{Prerequisite item}}

## Implementation options

### Option A: {{Option name}}

**Best for:** {{One-sentence description of when to use this option}}

**How it works:**

{{Paragraph 1: Describe the overall approach and architecture of this option.}}

{{Paragraph 2: Describe the key configuration steps or workflow.}}

{{Paragraph 3 (optional): Describe any runtime behavior or execution model.}}

{{Paragraph 4 (optional): Describe monitoring, reporting, or optimization considerations.}}

**Key considerations:**

- {{Consideration about timing, latency, or throughput}}
- {{Consideration about data requirements or dependencies}}
- {{Consideration about channel support or limitations}}
- {{Consideration about governance or compliance}}

**Advantages:**

- {{Advantage of this approach}}
- {{Advantage of this approach}}
- {{Advantage of this approach}}

**Limitations:**

- {{Limitation or trade-off}}
- {{Limitation or trade-off}}
- {{Limitation or trade-off}}

**Experience League:**

- [{{Link text}}]({{URL}})
- [{{Link text}}]({{URL}})

### Option B: {{Option name}}

**Best for:** {{One-sentence description of when to use this option}}

**How it works:**

{{Paragraph 1: Describe the overall approach and architecture of this option.}}

{{Paragraph 2: Describe the key configuration steps or workflow.}}

**Key considerations:**

- {{Consideration}}
- {{Consideration}}

**Advantages:**

- {{Advantage}}
- {{Advantage}}

**Limitations:**

- {{Limitation}}
- {{Limitation}}

**Experience League:**

- [{{Link text}}]({{URL}})

{{Repeat for Options C, D as needed. Include 2-4 options total.}}

### Option comparison

| Criteria | Option A | Option B | Option C |
| --- | --- | --- | --- |
| Best for | {{description}} | {{description}} | {{description}} |
| Complexity | {{Low / Medium / High}} | {{Low / Medium / High}} | {{Low / Medium / High}} |
| Time to value | {{Fast / Moderate / Slow}} | {{Fast / Moderate / Slow}} | {{Fast / Moderate / Slow}} |
| Channel support | {{description}} | {{description}} | {{description}} |
| Personalization depth | {{description}} | {{description}} | {{description}} |
| Scalability | {{description}} | {{description}} | {{description}} |
````

---

## Notas sobre el uso de esta plantilla

- **Frontmatter de YAML:** `exl-id` debe ser un UUID de marcador de posición (por ejemplo: `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`). La canalización de publicación asigna el valor real.
- **Nombres de productos de Adobe:** Utilice siempre la sintaxis `[!DNL ...]` para los nombres de productos de Adobe en texto independiente y tablas (por ejemplo, `[!DNL Journey Optimizer]`). Esta es una convención de Experience League que impide la traducción de nombres de productos.
- **Vínculos de objetivos empresariales:** Use rutas relativas del archivo de patrones al directorio de objetivos empresariales: `../../business-objectives/{{category}}/{{filename}}.md`.
- **Nombres de archivo en mayúsculas y minúsculas:** El nombre de archivo del patrón debe ser en mayúsculas y minúsculas derivado del título del patrón. Ejemplo: &quot;Mensajería activada por eventos&quot; se convierte en `event-triggered-messaging.md`.
- **Cadena de funciones:** Utilice ` > ` (espacio, mayor que, espacio) como separador entre pasos.
- **Valores de estado:** Uso de funciones básicas: Necesario, Supuesto en contexto, No aplicable. Uso de funciones de soporte: Recomendado, Incluido, No aplicable.
- **Fases de implementación:** Los nombres de fase comunes incluyen: Configuración, Activación, Optimización y Monitorización.
- **Requisitos previos:** Use la sintaxis de la casilla de verificación `- [ ]` para cada elemento.
