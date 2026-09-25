---
source-git-commit: 2ed15399073fce5ebd1c2ba07b1cf70ec706452c
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%
---
# Estado de la migración â€&quot; modelos para patrones de casos de uso

Este documento registra el estado del esfuerzo de reorganización del modelo para que se pueda reanudar sin problemas entre sesiones.

**Última actualización:** 2026-09-24

## Donde estamos ahora mismo

La sección B2B ya no está en pausa. Su ámbito de arquitectura publicado ahora se limita a las páginas de audiencia/perfil y activación de cuentas, y las páginas retiradas se redirigen a la descripción general de la categoría.

**Estado actual:** Se ha completado la limpieza de la arquitectura B2B. Las páginas de audiencia/perfil y activación de cuenta permanecen en la categoría de diagramas de arquitectura; las demás páginas de arquitectura B2B se retiraron y se redirigieron a la descripción general de la categoría.

## Enfoque práctico

> El enfoque de trabajo que se muestra a continuación es histórico; desde entonces, la sección B2B se ha dispuesto como se ha registrado anteriormente.

El plan de trabajo actual, acordado en este período de sesiones, es el siguiente:

1. **Mantener los modelos activos** â€&quot; sin desaprobación. Cada modelo permanece en su lugar como una página centrada en la arquitectura.
2. **Agregar SUGERENCIA de vínculos cruzados** a cada modelo con un patrón de caso de uso relacionado o superpuesto, inmediatamente después de H1:

   ```
   >[!TIP]
   >This blueprint is also available as a [use case pattern](<absolute path>) under <Category>.
   ```

3. **Migrar diagramas** â€&quot; si un modelo tiene un diagrama de arquitectura del que carece el patrón relacionado, agregue una sección `## Architecture` al patrón que hace referencia al mismo SVG a través de una ruta absoluta. El recurso permanece en su ubicación original (sin copias de archivo).
4. **Recortar pasos de implementación** desde el modelo donde se trató en el patrón. Las secciones que se deben eliminar suelen incluir: `## Implementation steps`, `## Implementation patterns`, `## Implementation considerations`, a veces `## Prerequisites`. Utilice el criterio por modelo.
5. **Recorra uno a uno** â€&quot; para proponer cambios por modelo, obtener la aprobación del usuario y luego aplicar.

### Reglas universales

- El texto de la SUGERENCIA entre vínculos es coherente: `>This blueprint is also available as a [use case pattern](...) under <Category>.`
- Los nuevos archivos (patrones de casos de uso creados durante la migración) **no incluyen`exl-id`**€&quot; que la publicación de Adobe asigna.
- Las referencias de imagen en los archivos recién creados utilizan rutas de acceso absolutas (`/help/blueprints/...`), no relativas.
- Se conservan los valores de `exl-id` existentes en las páginas existentes.
- Las redirecciones en `redirects.csv` siguen el formato `source,dest` con `/en/docs/...` rutas (no `.html`).

## Fases Aâ€&quot;E (trabajo estructural inicial) â€&quot; COMPLETO

| Fase | Resultado |
| --- | --- |
| A | Se creó la categoría de patrón de caso de uso `B2B Activation & Marketing`. Se han reubicado 3 patrones existentes (`b2b-audience-activation` â†’ `b2b/account-audience-activation`, `buying-group-based-marketing` â†’ `b2b/buying-group-marketing`, `b2b-analytics` â†’ `b2b/account-analytics`). Se han añadido 3 redirecciones. |
| B | Copiados 4 modelos B2B en `use-case-patterns/b2b/` (`marketo-data-journeys`, `paid-media-orchestration`, `campaign-intake-and-creation`, `campaign-review-and-approval`). |
| C | Se han copiado 4 modelos que no son B2B (`real-time-profile-lookup`, `data-science-profile-enrichment`, `edge-profile-access`, `campaign-v8-orchestration`). |
| D | Copiados 2 modelos divididos (`audience-sharing-with-target`, `third-party-messaging`). |
| E | Se ha añadido SUGERENCIA de vínculos cruzados a 9 modelos clasificados como duplicados. |

Patrones de casos de uso totales después de Aâ€&quot;E: **26 patrones** en 6 categorías.

## Tutorial sección por sección (en curso)

El tutorial de sección aplica el enfoque de vinculación cruzada/migración de diagrama/recorte de implementación a cada modelo individualmente en la revisión del usuario.

### âoe... Activación de audiencia y perfil â€&quot; 8/8 completo

| # | Modelo | Acción realizada |
| --- | --- | --- |
| 1 | `audience-manager.md` | Sugerencia de vínculo cruzado + diagrama migrado al patrón (`anonymous-visitor-web-personalization`) + pasos de RTCDP impl eliminados |
| 2 | `enterprise-destinations.md` | Sugerencia de vínculo cruzado + diagrama migrado al patrón (`audience-activation-to-destinations`) |
| 3 | `advertising-activation.md` | Pasos de Impl eliminados (99 â†’ 35 líneas) |
| 4 | `customer-activity.md` | Pasos de Impl eliminados (51 â†’ 40 líneas) |
| 5 | `data-science.md` | Consideraciones sobre la Impl eliminadas (46 â†’ 40 líneas) |
| 6 | `real-time-lookup.md` | Requisitos previos + patrones/pasos/consideraciones de impl eliminados (156 â†’ 73 líneas) |
| 7 | `segment-match.md` | **No hay cambios** (el usuario optó por salir tal cual) |
| 8 | `rtcdp-target.md` | Patrones de Impl + consideraciones eliminadas (99 â†’ 74 líneas) |

### El B2B Activation &amp; Marketing â€&quot; 1/10 en curso

| # | Modelo | Estado |
| --- | --- | --- |
| 1 | `b2b/overview.md` | Completado: información general de la categoría B2B actualizada |
| 2 | `b2b/b2bactivation.md` | Retirado: reemplazado por la página de audiencia/perfil de los diagramas de arquitectura |
| 3 | `b2b/b2b-account-activation.md` | Retenido: se migra a la categoría B2B de diagramas de arquitectura |
| 4 | `b2b/b2b-buying-group-journeys.md` | Retirado |
| 5 | `b2b/b2b-journeys-with-marketo.md` | Retirado |
| 6 | `b2b/ajo-b2b-paid-media-controller.md` | Retirado |
| 7 | `b2b/marketo-engage-and-workfront-integration-blueprint/overview.md` | Retirado |
| 8 | `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | Retirado |
| 9 | `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | Retirado |
| 10 | `b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md` | Retirado |

### âšª Customer Journey Analytics â€&quot; 0/5 aún no comenzado

Archivos: `overview.md`, `b2b-cja.md` (Fase E duplicada, vínculo cruzado añadido), `cja-rtcdp.md` (Grupo 2 â€&quot; recomiendan el vínculo cruzado a `customer-analytics-insight-generation`), `cja-ajo.md` (Grupo 2 â€&quot; igual), `analysis.md` (Grupo 3, posiblemente reubicar en experience-platform/).

### âšª Recorridos del cliente â€&quot; limpieza de jubilación completa; migración de la página retenida pendiente

Archivos: `overview.md`; `journey-optimizer/` (4 archivos: información general, recorridos [Fase E], campañas [Fase E], mensajes de terceros [Fase D]); `campaign-v8/` (3 archivos: información general [Fase C], rtcdp-and-v8, ajo-and-v8). `decision-management/` y `campaign-v7/` están completamente retirados; sus entradas históricas permanecen en la auditoría y sus direcciones URL se redirigen a las páginas de información general aprobadas.

### âšª Experience Platform â€&quot; 0/6 aún no comenzado

Archivos: `experience-cloud.md`, `platform-applications.md`, `platform-data-flow.md`, `guardrails.md`, `deployment/websdk.md`, `deployment/appsdk.md`. Todos ellos puntuados como Sólo diagrama con 0 señales de patrón en la auditoría. **Es probable que todos &quot;sin cambio&quot;** â€&quot; sean una arquitectura fundamental con la que no se superponga ningún patrón de caso de uso.

Las decisiones de jubilación de Administración de decisiones y Campaign v7 se han completado. Sus preguntas abiertas relacionadas
son solo históricos y no deben bloquear el trabajo de migración restante.

## Archivos de referencia

| Archivo | Finalidad |
| --- | --- |
| [blueprint-audit.md](blueprint-audit.md) | Tabla de auditoría por modelo (43 filas) con recomendaciones |
| [rúbrica.md](rubric.md) | Rúbrica de puntuación utilizada para clasificar modelos |
| [migration-redirects.csv](migration-redirects.csv) | Redirecciones organizadas desde la migración |
| [redirecciones.csv](../redirects.csv) | Archivo de redirecciones canónicas (3 filas añadidas en la fase A) |

## Preguntas pendientes sin resolver (de la auditoría)

2. **`journey-optimizer-journeys.md`** â€&quot; marcados como duplicado incierto de `event-triggered-messaging`; compruebe el ámbito antes de recortar.
3. El contenido de **`customer-journey-analytics/analysis.md`** â€&quot; se refiere al servicio de consultas de Experience Platform, no a CJA; considere la posibilidad de reubicarse en `experience-platform/`.
4. **`customer-success-stories.md`** â€&quot; página solo de vínculos; confirmar clasificación de navegación.
5. Pregunta histórica de anclaje del índice reemplazada por la disposición de arquitectura B2B completada.

## Cómo reanudar

Abra una nueva sesión de Código Claude en este repositorio y diga:

> Reanudemos la migración del modelo. Lea `_evaluation/migration-status.md` para recoger lo que dejamos.

Se ha completado la limpieza de la arquitectura B2B. Continúe con la siguiente categoría de arquitectura planificada después de la validación.
