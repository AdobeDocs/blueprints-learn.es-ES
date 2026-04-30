---
source-git-commit: 7511cc0e5c099d5d3ee1275a374cd9ffdc972335
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---
# Módulo de evaluación de modelo

Esta rúbrica se aplica a cada documento en la sección &quot;Diagramas de arquitectura y modelos&quot;
de [TOC.md](../help/blueprints/TOC.md) (líneas 76-133) para recomendar si cada modelo debe convertirse en un
**Patrón de caso de uso**, un **Diagrama de arquitectura**, ambos (**Split**) o se marcarán como
**Duplicado** de un patrón existente.

El resultado de aplicar este encabezamiento es [blueprint-audit.md](blueprint-audit.md).

## Definiciones

- **Patrón de caso de uso**: un documento que describe un objetivo comercial o técnico específico y
esbozar posibles enfoques y consideraciones para la aplicación a fin de lograr ese objetivo.
Forma canónica: `.claude/skills/use-case-pattern-builder/references/pattern-template.md`.
- **Diagrama de arquitectura**: un diagrama visual que representa la funcionalidad de un sistema, el
integraciones y flujos de datos. Narración mínima; el diagrama es el artefacto.
Ejemplo canónico: [platform-data-flow.md](../help/blueprints/experience-platform/platform-data-flow.md).

## Puntuación

Cada modelo se lee de extremo a extremo y se clasifica con ocho señales binarias. Cada señal contribuye
+1 a la puntuación del patrón o a la puntuación del diagrama.

### Señales de patrón (cada una = +1 patrón)

1. **Marco de objetivos empresariales**: fotogramas de ingresos, retención, adquisición, generación de posibles clientes, costo
reducción, experiencia del cliente o resultado comercial similar.
2. **KPI o métricas de éxito**: nombra explícitamente métricas, tasas de conversión, tasas de coincidencia, ROI o
medidas de resultado similares.
3. **Múltiples opciones de implementación o niveles de vencimiento** — presenta la Opción A / Opción B, básica vs.
alternativas avanzadas o comparables que el lector elija entre ellas.
4. **Lista de comprobación de requisitos previos o preparación**: enumera los requisitos que deben cumplirse antes de implementar.
5. **Pasos de implementación narrativa > ~30 líneas** — Guía de implementación sustantiva, no
sólo una breve descripción general.

### Señales del diagrama (cada una = +1 Diagrama)

6. **Imagen de flujo de datos/arquitectura presente** — `.svg`, `.png` o `.jpg` que muestra la topología del sistema,
flujo de datos o flechas de integración.
7. **Topología de integración entre sistemas, forma de implementación o protecciones**: describe cómo
los componentes se conectan, donde residen los datos, los modelos de implementación (edge o hub) o los límites de capacidad.
8. **La audiencia es arquitectos de soluciones**: la creación de marcos usa la implementación, SDK, edge, hub o similar
terminología orientada al arquitecto en lugar de marcos orientados al experto en marketing (campañas, recorridos,
audiencias).

## Lógica de recomendación

Aplique primero las reglas de anulación. Si no se activa ninguna anulación, derive la recomendación de las puntuaciones.

### Ignorar reglas (prioridad más alta)

1. **El nombre del archivo es`overview.md`** → recomendación = `Navigation`. Excluido de la migración; el
Una página de aterrizaje es una página de aterrizaje de estilo TDC que se revisará después de que se establezcan los archivos secundarios.
2. **Ya existe un patrón equivalente en`help/blueprints/use-case-patterns/`** →
recomendación = `Duplicate`. La acción de migración consiste en simplificar el modelo para convertirlo en un
y añada un vínculo cruzado &quot;Ver patrón de caso de uso&quot; al patrón existente.
Registre la ruta de acceso del patrón existente en la columna `duplicate_of`.
3. **El archivo se encuentra en `experience-platform/` y no tiene ninguna señal de objetivo empresarial (#1)** → forma predeterminada
   `Diagram` independientemente de otras puntuaciones. Esta carpeta es el nivel de descripción general de arquitectura.

### Recomendación basada en la puntuación (cuando no se activa ninguna anulación)

| Puntuación de patrón | Puntuación de diagrama | Recomendación | Razonar |
| --- | --- | --- | --- |
| ≥ 3 | ≤ 1 | `Pattern` | Señales de patrón fuertes, señales de diagrama débiles → migrar al patrón. |
| ≤ 1 | ≥ 2 | `Diagram` | Señales de patrón débil, el enfoque visual/topológico dominante → mantener como diagrama. |
| ≥ 3 | ≥ 2 | `Split` | Tanto el contenido de patrón enriquecido como un diagrama significativo → extraer el patrón, reducir el original al diagrama y establecer vínculos cruzados. |
| 2 | 2 | `Split` | Amarre con fuerza moderada → partir. |
| 2 | ≤ 1 | `Pattern` | Inclinación del patrón, sin valor significativo en el diagrama. |
| ≤ 1 | ≤ 1 | `Diagram` | Fino en general, probablemente una página de arquitectura mínima existente. |

## Cómo aplicar la rúbrica

Para cada archivo de marcado de modelo en el ámbito:

1. Lea el archivo completo de extremo a extremo.
2. Marque cada una de las ocho señales presentes/ausentes.
3. Aplique reglas de anulación en orden. Si uno se dispara, esa es la recomendación.
4. De lo contrario, calcule la puntuación del patrón y la puntuación del diagrama y busque la recomendación.
5. Para las recomendaciones `Pattern` y `Split`, proponga:
   - `proposed_pattern_category` — uno de:
     `audience-building-activation`, `personalization`, `campaign-management-orchestration`,
     `analysis`, `conversational-experience` o una nueva categoría denominada `(new) <name>`.
   - `proposed_pattern_title`: un título corto orientado a la acción que sigue el patrón existente
estilo de nomenclatura.
6. Para las recomendaciones `Diagram` y `Split`, proponga:
   - `proposed_diagram_title`: normalmente el título existente recortado de la trama empresarial.
7. Capture los duplicados que se encuentren comparando el ámbito del modelo con el catálogo de patrones existente
en `duplicate_of`.
8. Registre las preguntas abiertas, el contenido técnico único que vale la pena conservar o el riesgo de migración en `notes`.

## Catálogo de patrones de casos de uso existentes (para la detección de duplicados)

| Categoría | Patrones |
| --- | --- |
| audience-building-activation | audience-activation-to-destinations, audience-collaborative-segment-match, b2b-audience-activation, reenvío de eventos |
| personalización | anonymous-visitor-web-personalization, known-visitor-web-app-personalization, offer-decisioning, behavior-recommendation |
| campaign-management-orchestration | activación de mensajes salientes por lotes, mensajería activada por eventos, recorrido orquestado por varios pasos, recorrido en canales múltiples con toma de decisiones, marketing basado en grupos de compra |
| análisis | customer-analytics-insight-generation, b2b-analytics |
| conversación-experiencia | brand-concierge-conversational-experience |
