---
source-git-commit: 7511cc0e5c099d5d3ee1275a374cd9ffdc972335
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 2%

---
# Estado de la migración: modelos para patrones de casos de uso

Este documento registra el estado del esfuerzo de reorganización del modelo para que se pueda reanudar sin problemas entre sesiones.

**Última actualización:** 2026-04-29

## Donde estamos ahora mismo

**Actualmente en pausa el:** `b2b/overview.md` (#1 de modelo de sección B2B de 10) — a la espera de una decisión sobre si se debe dejar tal cual, agregar una referencia cruzada a la nueva sección de patrones de Activación y marketing B2B, o actualizar la tabla para enumerar todos los modelos + agregar referencia cruzada.

**Para reanudar:** responda con **A** (dejar tal cual, recomendado), **B** (agregar referencia cruzada) o **C** (actualizar tabla + agregar referencia cruzada). A continuación, continúe con la #2 de modelo (`b2b/b2bactivation.md`).

## Enfoque práctico

El plan de trabajo actual, acordado en este período de sesiones, es el siguiente:

1. **Mantener los modelos activos** — sin desaprobación. Cada modelo permanece en su lugar como una página centrada en la arquitectura.
2. **Agregar SUGERENCIA de vínculos cruzados** a cada modelo con un patrón de caso de uso relacionado o superpuesto, inmediatamente después de H1:

   ```
   >[!TIP]
   >This blueprint is also available as a [use case pattern](<absolute path>) under <Category>.
   ```

3. **Migrar diagramas**: si un modelo tiene un diagrama de arquitectura del que carece el patrón relacionado, agregue una sección `## Architecture` al patrón que haga referencia al mismo SVG a través de una ruta de acceso absoluta. El recurso permanece en su ubicación original (sin copias de archivo).
4. **Recortar pasos de implementación** desde el modelo donde se trató en el patrón. Las secciones que se deben eliminar suelen incluir: `## Implementation steps`, `## Implementation patterns`, `## Implementation considerations`, a veces `## Prerequisites`. Utilice el criterio por modelo.
5. **Recorrer uno a uno**: proponer cambios por modelo, obtener la aprobación del usuario y aplicar.

### Reglas universales

- El texto de la SUGERENCIA entre vínculos es coherente: `>This blueprint is also available as a [use case pattern](...) under <Category>.`
- Los nuevos archivos (patrones de casos de uso creados durante la migración) **no incluyen`exl-id`**: la publicación de Adobe los asigna.
- Las referencias de imagen en los archivos recién creados utilizan rutas de acceso absolutas (`/help/blueprints/...`), no relativas.
- Se conservan los valores de `exl-id` existentes en las páginas existentes.
- Las redirecciones en `redirects.csv` siguen el formato `source,dest` con `/en/docs/...` rutas (no `.html`).

## Fases A-E (trabajo estructural inicial) — COMPLETA

| Fase | Resultado |
| --- | --- |
| A | Se creó la categoría de patrón de caso de uso `B2B Activation & Marketing`. Se reubicaron 3 patrones existentes (`b2b-audience-activation` → `b2b/account-audience-activation`, `buying-group-based-marketing` → `b2b/buying-group-marketing`, `b2b-analytics` → `b2b/account-analytics`). Se han añadido 3 redirecciones. |
| B | Copiados 4 modelos B2B en `use-case-patterns/b2b/` (`marketo-data-journeys`, `paid-media-orchestration`, `campaign-intake-and-creation`, `campaign-review-and-approval`). |
| C | Se han copiado 4 modelos que no son B2B (`real-time-profile-lookup`, `data-science-profile-enrichment`, `edge-profile-access`, `campaign-v8-orchestration`). |
| D | Copiados 2 modelos divididos (`audience-sharing-with-target`, `third-party-messaging`). |
| E | Se ha añadido SUGERENCIA de vínculos cruzados a 9 modelos clasificados como duplicados. |

Patrones de casos de uso totales después de A-E: **26 patrones** en 6 categorías.

## Tutorial sección por sección (en curso)

El tutorial de sección aplica el enfoque de vinculación cruzada/migración de diagrama/recorte de implementación a cada modelo individualmente en la revisión del usuario.

### Activación de audiencia y perfil de ✅: 8/8 completa

| # | Modelo | Acción realizada |
| --- | --- | --- |
| 1 | `audience-manager.md` | Sugerencia de vínculo cruzado + diagrama migrado al patrón (`anonymous-visitor-web-personalization`) + pasos de RTCDP impl eliminados |
| 2 | `enterprise-destinations.md` | Sugerencia de vínculo cruzado + diagrama migrado al patrón (`audience-activation-to-destinations`) |
| 3 | `advertising-activation.md` | Pasos de Impl eliminados (99 → 35 líneas) |
| 4 | `customer-activity.md` | Pasos de Impl eliminados (51 → 40 líneas) |
| 5 | `data-science.md` | Consideraciones sobre la Impl eliminadas (46 → 40 líneas) |
| 6 | `real-time-lookup.md` | Se han eliminado los requisitos previos + los patrones/pasos/consideraciones de impl (156 → 73 líneas) |
| 7 | `segment-match.md` | **No hay cambios** (el usuario optó por salir tal cual) |
| 8 | `rtcdp-target.md` | Patrones de Impl + consideraciones eliminadas (99 → 74 líneas) |

### 🟡 Activación y marketing B2B: 1/10 en curso

| # | Modelo | Estado |
| --- | --- | --- |
| 1 | `b2b/overview.md` | **PAUSADO** — a la espera de la decisión A/B/C (vea &quot;Donde estamos ahora&quot; más arriba) |
| 2 | `b2b/b2bactivation.md` | Pendiente: Duplicado de fase E; se ha agregado un vínculo cruzado; es necesario revisar el diagrama + recorte de impl |
| 3 | `b2b/b2b-account-activation.md` | Pendiente — Clasificado según el diagrama; necesita un vínculo cruzado a `b2b/account-audience-activation.md` + consideración de la migración al diagrama |
| 4 | `b2b/b2b-buying-group-journeys.md` | Pendiente: Duplicado de fase E; se ha añadido un vínculo cruzado; es necesario revisarlo |
| 5 | `b2b/b2b-journeys-with-marketo.md` | Pendiente: copia de fase B; el patrón es una copia; necesita recorte de impl-step |
| 6 | `b2b/ajo-b2b-paid-media-controller.md` | Pendiente: copia de fase B; necesita recorte de impl-step |
| 7 | `b2b/marketo-engage-and-workfront-integration-blueprint/overview.md` | Pendiente: página de aterrizaje de sección |
| 8 | `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | Pendiente: copia de fase B; necesita recorte de impl-step |
| 9 | `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | Pendiente: copia de fase B; necesita recorte de impl-step |
| 10 | `b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md` | Pendiente: página solo de vínculos (auditoría marcada como Navegación) |

### ⚪ Customer Journey Analytics — 0/5 aún no iniciado

Archivos: `overview.md`, `b2b-cja.md` (Fase E duplicada, vínculo cruzado agregado), `cja-rtcdp.md` (Grupo 2 — recomendar vínculo cruzado a `customer-analytics-insight-generation`), `cja-ajo.md` (Grupo 2 — mismo), `analysis.md` (Grupo 3, posiblemente reubicar en experience-platform/).

### ⚪ Recorridos del cliente: 0/14 sin iniciar

Archivos: `overview.md`; `journey-optimizer/` (4 archivos: información general, recorridos [Fase E], campañas [Fase E], mensajería de terceros [Fase D]); `decision-management/` (3 archivos: información general, perímetro [Fase E], concentrador [Fase E]); `campaign-v8/` (3 archivos: información general [Fase C], rtcdp-and-v8, ajo-and-v8); `campaign-v7/` (3 obsoleto) archivos).

### ⚪ Experience Platform — 0/6 aún no iniciado

Archivos: `experience-cloud.md`, `platform-applications.md`, `platform-data-flow.md`, `guardrails.md`, `deployment/websdk.md`, `deployment/appsdk.md`. Todos ellos puntuados como Sólo diagrama con 0 señales de patrón en la auditoría. **Probablemente todos &quot;sin cambio&quot;**, son una arquitectura fundamental con la que no se superpone ningún patrón de caso de uso.

## Archivos de referencia

| Archivo | Finalidad |
| --- | --- |
| [blueprint-audit.md](blueprint-audit.md) | Tabla de auditoría por modelo (43 filas) con recomendaciones |
| [rúbrica.md](rubric.md) | Rúbrica de puntuación utilizada para clasificar modelos |
| [migration-redirects.csv](migration-redirects.csv) | Redirecciones organizadas desde la migración |
| [redirecciones.csv](../redirects.csv) | Archivo de redirecciones canónicas (3 filas añadidas en la fase A) |

## Preguntas pendientes sin resolver (de la auditoría)

1. **Edge + hub de Administración de decisiones**: ambos actualmente se vinculan a `offer-decisioning`. Considere la posibilidad de consolidarla en un único diagrama de opciones de implementación.
2. **`journey-optimizer-journeys.md`** — marcado como duplicado incierto de `event-triggered-messaging`; compruebe el ámbito antes de recortar.
3. **`customer-journey-analytics/analysis.md`** — el contenido es sobre Experience Platform Query Service, no sobre CJA; considere la posibilidad de reubicarse en `experience-platform/`.
4. **Campaign v7 (3 archivos obsoletos)**: ¿migrar, salir o eliminar de la tabla de contenido?
5. **`customer-success-stories.md`** — página solo de vínculos; confirmar clasificación de navegación.
6. **El anclaje de TDC** para la nueva sección B2B es `{#b2b-patterns}`; confirmar antes de cualquier creación de redirección de producción.

## Cómo reanudar

Abra una nueva sesión de Código Claude en este repositorio y diga:

> Reanudemos la migración del modelo. Lea `_evaluation/migration-status.md` para recoger lo que dejamos.

El siguiente paso concreto: responder a la decisión `b2b/overview.md` (A/B/C). A continuación, continúe con la #2 del modelo (`b2b/b2bactivation.md`) y continúe por la sección B2B, luego Customer Journey Analytics, Recorridos del cliente y Experience Platform.
