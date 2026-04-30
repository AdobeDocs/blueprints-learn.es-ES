---
source-git-commit: 7511cc0e5c099d5d3ee1275a374cd9ffdc972335
workflow-type: tm+mt
source-wordcount: '3505'
ht-degree: 6%

---
# Auditoría de modelos y recomendaciones

Esta auditoría aplica el [encabezamiento de evaluación](rubric.md) a todos los documentos que se encuentran bajo el
Sección &quot;Diagramas de arquitectura y modelos&quot; de [TOC.md](../help/blueprints/TOC.md) (líneas 76-133), y
recomienda si cada modelo debe convertirse en un caso de uso **Pattern**, una arquitectura
**Diagrama**, ambos (**Dividido**), o se marcarán como **Duplicado** de un patrón existente.

Esto es solo una auditoría; no se ha movido ningún contenido. El registro de pendientes de migración (acciones A-D por lotes)
se redactará como un plan de seguimiento independiente una vez que se hayan revisado las recomendaciones.

## Resumen

**Total de documentos auditados:** 43

| Recomendación | Recuento | Acción |
| --- | --- | --- |
| Patrón | 8 | Cree un nuevo patrón de caso de uso; recorte el original a un diagrama. |
| Duplicar | 9 | El patrón existente cubre el ámbito; simplifique el modelo a un diagrama y vincule. |
| División | 2 | Extraer contenido del patrón; reducir original a diagrama; vincular ambos. |
| Diagrama | 16 | Mantener como diagrama de arquitectura; recortar narrativa si es necesario. |
| Navegación | 8 | Página de aterrizaje de la sección (overview.md o links únicamente); volver a visitar después del aterrizaje de las migraciones. |

### Calibración del grupo de control

Los 6 archivos de `experience-platform/` tuvieron una puntuación de Pattern=0, Diagram=3 → unánimemente **Diagram**.
La rúbrica está calibrada; los resultados de las otras subáreas se pueden confiar como puntuados.

### Nueva categoría de patrones de casos de uso: Activación y marketing B2B

Una nueva categoría `use-case-patterns/b2b/` (etiqueta de visualización **Activación y marketing B2B**, delimitador de TDC
`{#b2b-patterns}` propuesto) alojará todos los patrones específicos de B2B. La etiqueta refleja la etiqueta existente
subsección &quot;Activación y marketing B2B&quot; en el área de diagramas de arquitectura de [TOC.md](../help/blueprints/TOC.md),
dando a los lectores simetría visual entre las dos secciones.

Una vez completada, la categoría contendrá **7 patrones**:

| Origen | Acción | Ruta de destino |
| --- | --- | --- |
| `use-case-patterns/audience-building-activation/b2b-audience-activation.md` | **Reubicar** patrón existente | `use-case-patterns/b2b/account-audience-activation.md` |
| `use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md` | **Reubicar** patrón existente | `use-case-patterns/b2b/buying-group-marketing.md` |
| `use-case-patterns/analysis/b2b-analytics.md` | **Reubicar** patrón existente | `use-case-patterns/b2b/account-analytics.md` |
| `b2b/b2b-journeys-with-marketo.md` | **Crear nuevo** (fila del patrón de auditoría) | `use-case-patterns/b2b/marketo-data-journeys.md` |
| `b2b/ajo-b2b-paid-media-controller.md` | **Crear nuevo** (fila del patrón de auditoría) | `use-case-patterns/b2b/paid-media-orchestration.md` |
| `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | **Autor nuevo** | `use-case-patterns/b2b/campaign-intake-and-creation.md` |
| `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | **Autor nuevo** | `use-case-patterns/b2b/campaign-review-and-approval.md` |

> **Estado de transición inicial — puerta de coordinación de escritura.** El existente &quot;Activación y marketing B2B&quot;> la subsección del área de diagramas de arquitectura de [TOC.md](../help/blueprints/TOC.md) (líneas 95-106) **permanece intacta> durante la transición**. Cada conversión de modelo y reubicación de patrones existentes requiere lo siguiente> cierre la sesión del escritor propietario antes de migrar el contenido. El nuevo patrón de caso de uso `b2b/`> coexiste con la sección de modelo existente mientras las migraciones se producen página por página, con> vínculos cruzados entre ellos.

Cuando las reubicaciones y los nuevos patrones hayan aterrizado:

- La sección [TOC.md](../help/blueprints/TOC.md) `Use Case Patterns` obtendrá un `B2B Activation & Marketing{#b2b-patterns}`
subsección (ubicación por determinar con el escritor).
- [use-case-patterns/overview.md](../help/blueprints/use-case-patterns/overview.md) obtendrá una tabla de categoría B2B.
- Los patrones reubicados se eliminarán de `audience-building-activation`,
  `campaign-management-orchestration` y `analysis` tablas de información general; se conservan sus direcciones URL antiguas
activo mediante redirecciones en [migration-redirects.csv](migration-redirects.csv).

### Duplicados identificados (9)

El ámbito del modelo ya está cubierto por un patrón de caso de uso existente. La acción de migración es
**simplificar al diagrama de arquitectura + vínculo cruzado**.

| Modelo | Patrón existente |
| --- | --- |
| `audience-activation/advertising-activation.md` | `use-case-patterns/audience-building-activation/audience-activation-to-destinations.md` |
| `audience-activation/segment-match.md` | `use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md` |
| `b2b/b2bactivation.md` | `use-case-patterns/audience-building-activation/b2b-audience-activation.md` |
| `b2b/b2b-buying-group-journeys.md` | `use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md` |
| `customer-journey-analytics/b2b-cja.md` | `use-case-patterns/analysis/b2b-analytics.md` |
| `customer-journeys/journey-optimizer/journey-optimizer-journeys.md` | `use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md` |
| `customer-journeys/journey-optimizer/journey-optimizer-campaigns.md` | `use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md` |
| `customer-journeys/decision-management/decision-management-edge.md` | `use-case-patterns/personalization/offer-decisioning.md` |
| `customer-journeys/decision-management/decision-management-hub.md` | `use-case-patterns/personalization/offer-decisioning.md` |

> Nota: `decision-management-edge.md` y `decision-management-hub.md` se asignan al mismo> patrón `offer-decisioning.md` existente. Considere la posibilidad de consolidar ambos modelos en uno solo> diagrama de opciones de implementación o aumento del patrón existente con la implementación edge-vs-hub> variantes. Indicador para revisión de escritor.

### Patrones de creación (8 nuevos + 2 de Divisiones = 10 en total)

| Modelo de Source | Categoría propuesta | Título de patrón propuesto |
| --- | --- | --- |
| `audience-activation/customer-activity.md` | audience-building-activation | Búsqueda de perfil en tiempo real para soporte y ventas |
| `audience-activation/data-science.md` | audience-building-activation | Ingesta de modelos de ciencia de datos para enriquecimiento de perfiles |
| `audience-activation/real-time-lookup.md` | personalización | Acceso al perfil de Edge para Personalization web/móvil |
| `b2b/b2b-journeys-with-marketo.md` | **b2b** (nuevo) | Recorridos de cuenta B2B con integración de datos de Marketo |
| `b2b/ajo-b2b-paid-media-controller.md` | **b2b** (nuevo) | Orquestación de medios de pago B2B mediante lógica de ruta dividida de cascada |
| `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | **b2b** (nuevo) | Admisión de solicitudes de campaña y creación automatizada de programas |
| `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | **b2b** (nuevo) | Flujo de trabajo de revisión y aprobación de recursos Campaign |
| `customer-journeys/campaign-v8/campaign-v8-overview.md` | campaign-management-orchestration | Orquestación por lotes y mensajería transaccional de Campaign v8 |
| `audience-activation/rtcdp-target.md` *(División)* | personalización | Uso compartido de audiencias en tiempo real con Adobe Target |
| `customer-journeys/journey-optimizer/3rd-party-messaging.md` *(División)* | campaign-management-orchestration | Integración de mensajería de terceros con Journey Optimizer |

### Nueva categoría de patrón propuesta

- **`b2b/`** (etiqueta de visualización **Activación y marketing B2B**): consulte la sección dedicada anterior. El
Los patrones Marketo + Workfront (`intake-and-create`, `review-and-approve-blueprint`) se enrutan
aquí, en lugar de en una categoría `marketing-resource-management` independiente, ya que representan
Operaciones de marketing B2B en la práctica. La nueva categoría suma 7 patrones en total: 3 reubicados
de las categorías existentes y 4 recién creadas a partir de modelos.

### Redirecciones de migración

Cada cambio de URL introducido por esta migración agrega una fila a la canónica
[`redirects.csv`](../redirects.csv) en la raíz del repositorio (formato: `source,dest`). Confirmado
las redirecciones se almacenan en [migration-redirects.csv](migration-redirects.csv) y se combinan en
archivo canónico a medida que se produce cada movimiento correspondiente.

**Confirmado (3 entradas, en fase):** Reubicaciones de patrones existentes en `b2b/`. Consulte
[migration-redirects.csv](migration-redirects.csv).

**Pendiente — agregado cuando se *elimina* un modelo (no cuando se reduce a un diagrama local):** si
El modelo de Patrón, División o Duplicado de fila se eliminará por completo más adelante. Añada una redirección desde el
URL de modelo a la URL del patrón canónico. Enfoque de migración predeterminado (simplificar a diagrama)
mantiene activa la dirección URL del modelo y **no requiere** estas redirecciones. Enumerado a continuación para
integridad si algún modelo está completamente retirado:

```
# Pattern blueprints — if deleted, redirect to the new pattern URL
# (slugs are placeholders; finalize when each pattern is authored)
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/customer-activity → use-case-patterns/audience-building-activation/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/data-science → use-case-patterns/audience-building-activation/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/real-time-lookup → use-case-patterns/personalization-patterns/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2b-journeys-with-marketo → use-case-patterns/b2b-patterns/marketo-data-journeys
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/ajo-b2b-paid-media-controller → use-case-patterns/b2b-patterns/paid-media-orchestration
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/marketo-engage-and-workfront-integration-blueprint/intake-and-create → use-case-patterns/b2b-patterns/campaign-intake-and-creation
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint → use-case-patterns/b2b-patterns/campaign-review-and-approval
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/campaign-v8/campaign-v8-overview → use-case-patterns/campaign-orchestration-patterns/<new-pattern-slug>

# Duplicate blueprints — if deleted, redirect to the existing pattern URL
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/advertising-activation → use-case-patterns/audience-building-activation/audience-activation-to-destinations
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/segment-match → use-case-patterns/audience-building-activation/audience-collaboration-segment-match
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2bactivation → use-case-patterns/b2b-patterns/account-audience-activation  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2b-buying-group-journeys → use-case-patterns/b2b-patterns/buying-group-marketing  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journey-analytics/b2b-cja → use-case-patterns/b2b-patterns/account-analytics  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/journey-optimizer/journey-optimizer-journeys → use-case-patterns/campaign-orchestration-patterns/event-triggered-messaging
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/journey-optimizer/journey-optimizer-campaigns → use-case-patterns/campaign-orchestration-patterns/batch-outbound-message-activation
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/decision-management/decision-management-edge → use-case-patterns/personalization-patterns/offer-decisioning
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/decision-management/decision-management-hub → use-case-patterns/personalization-patterns/offer-decisioning

# Optional one-off — if customer-journey-analytics/analysis.md is relocated to experience-platform/
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journey-analytics/analysis → architecture-diagrams/architecture-overview/analysis
```

Al convertir cualquiera de los elementos anteriores en filas de redireccionamiento activas, aplique el formato separado por comas `source,dest`
con rutas `/en/docs/...` completas (sin sufijo `.html`), que coinciden con el patrón existente en
[`redirects.csv`](../redirects.csv).

### Política de creación de redireccionamiento (regla duradera)

Para cada paso de migración, siga estas reglas:

1. **Archivo movido o renombrado** → agregar redireccionamiento de la URL antigua a la nueva URL.
2. **Archivo eliminado** (modelo reemplazado; no se retiene ningún diagrama) → agregar la redirección de la URL eliminada a
URL de reemplazo canónico.
3. **Archivo simplificado** (URL sin modificar) no → redireccionamiento.
4. **Se cambió el nombre del anclaje de la tabla de contenido** (por ejemplo, cambio en el encabezado de la sección) → agregar redirecciones para cada página en
dicho anclaje, ya que la dirección URL cambia.

### Preguntas abiertas para el escritor

1. **Gestión de decisiones edge vs. hub** — ambos se asignan al mismo existente `offer-decisioning.md`
patrón. Consolidar en un solo diagrama con variantes de implementación o tratarlo como independiente
¿qué diagramas se cruzan con el mismo patrón?
2. **recorridos de Journey Optimizer frente a mensajes activados por eventos** — el agente marcó este duplicado
clasificación como incierto. Compruebe la alineación del ámbito antes de reducir el modelo.
3. **`customer-journey-analytics/analysis.md`** — el contenido es sobre Experience Platform
Servicio de consultas, no CJA. Considere la posibilidad de reubicarse en la carpeta `experience-platform/`. (Una redirección
se agregaría si es así: consulte [migration-redirects.csv](migration-redirects.csv).)
4. **Campaign v7 (obsoleto)**: tres archivos v7 obsoletos se clasificaron como Diagrama /
Navegación. Confirme si desea migrar, salir tal cual o eliminar de la TDC por completo.
5. **`customer-success-stories.md`** — página de referencia solo de vínculos (no es `overview.md`).
Clasificado como Navegación. Confirme o vuelva a clasificar.
6. **Anclaje de TDC de sección B2B** — `{#b2b-patterns}` propuesto. Otros patrones que utilizan las subsecciones
   `-patterns` sufijo (`{#personalization-patterns}`, `{#analysis-patterns}`,
   `{#campaign-orchestration-patterns}`). Confirme o elija otro anclaje antes de crear las redirecciones.
7. **Colocación de sección B2B en el índice** — propuesta en `+ Use Case Patterns{#use-case-patterns}`.
Pedido entre hermanos (Generación y activación de audiencias, Personalization, Administración de campañas)
&amp; Orchestration, Analysis, B2B Activation &amp; Marketing, Conversational Experience) es la
la llamada del escritor.
8. **Coordinación de propietario-escritor**: cada conversión de modelo y reubicación de patrones existentes
necesita la firma del escritor antes de mover el contenido. La tabla de auditoría es el estado objetivo, no un
plan de secuenciación; la secuenciación se produce en un plan de migración de seguimiento después de la coordinación.

## Tabla de auditoría

| ruta | title | resumen | dominante_type | recomendación | posed_pattern_category | posed_pattern_title | título_diagrama_propuesto | duplicate_of | pattern_score | score_diagrama | apuntes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| help/blueprints/experience-platform/experience-cloud.md | Diagramas de la arquitectura de Adobe Experience Cloud | Arquitectura empresarial que muestra cómo se integran las aplicaciones y los servicios de Experience Cloud en AEP. | Diagrama | Diagrama |  |  | Descripción general de arquitectura de Experience Cloud |  | 0 | 3 | Anular 3 (sin objetivo empresarial). Tres diagramas complementarios (arquitectura, integración, entorno empresarial). Grupo de control: según lo esperado. |
| help/blueprints/experience-platform/platform-applications.md | Diagramas de arquitectura de aplicaciones y Adobe Experience Platform | Diagramas de arquitectura que muestran cómo se relaciona Experience Platform con otras aplicaciones de Experience Cloud. | Diagrama | Diagrama |  |  | Arquitectura de aplicaciones y AEP |  | 0 | 3 | Anular 3. Dos diagramas generales/detallados; sin directrices de implementación. Vínculos cruzados a integraciones, documentos de aprendizaje. Grupo de control: según lo esperado. |
| help/blueprints/experience-platform/platform-data-flow.md | Diagramas de arquitectura del flujo de datos de Adobe Experience Platform | Diagrama de la arquitectura del flujo de datos que muestra las rutas de ingesta y salida de Experience Platform. | Diagrama | Diagrama |  |  | Arquitectura de flujo de datos de AEP |  | 0 | 3 | Anular 3. Diagrama de flujo de datos único con referencia a documentos de recopilación de datos. Puro artefacto de arquitectura. Grupo de control: según lo esperado. |
| help/blueprints/experience-platform/guardrails.md | Experience Platform y guardas de aplicaciones | Restricciones del sistema, expectativas de rendimiento y protecciones de latencia para AEP y aplicaciones. | Diagrama | Diagrama |  |  | Protecciones y latencias de AEP y aplicaciones |  | 0 | 3 | Anular 3. Diagrama de latencia más tablas de referencia. Orientado a arquitectos (edge/hub). Documentación de restricciones, no de procedimientos. Grupo de control: según lo esperado. |
| help/blueprints/experience-platform/deployment/websdk.md | Diagrama de la arquitectura de Experience Platform Web SDK y Edge Network | Arquitectura de implementación de Web SDK y Edge Network que muestra flujos de recopilación de datos. | Diagrama | Diagrama |  |  | Implementación de Web SDK y Edge Network |  | 0 | 3 | Anular 3. Dos diagramas (flujo y secuencia). Hace referencia a tutoriales, pero no a procedimientos en documentos. Centrado en el arquitecto. Grupo de control: según lo esperado. |
| help/blueprints/experience-platform/deployment/appsdk.md | Diagrama de la arquitectura de implementación de SDK específico de la aplicación | Diagrama de arquitectura de recopilación de datos y rutas de integración de SDK específicas de la aplicación. | Diagrama | Diagrama |  |  | Implementación de SDK específica de la aplicación |  | 0 | 3 | Anular 3. Diagrama de implementación único con una narrativa mínima. Puro artefacto de arquitectura. Grupo de control: según lo esperado. |
| help/blueprints/audience-activation/advertising-activation.md | Destinos de Audience Activation a Social y Advertising | Activar audiencias en redes de anuncios de Facebook y Google a través de RTCDP con la configuración de identidad y el destino configurados. | Patrón | Duplicar |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md | 4 | 1 | El patrón existente abarca este ámbito. Anulación duplicada. Acción: simplificar para obtener un diagrama puro y establecer vínculos cruzados. |
| help/blueprints/audience-activation/audience-manager.md | Basado en dispositivo: segmentación de audiencias anónimas con Audience Manager | Activación anónima de audiencias mediante Audience Manager o RTCDP para la segmentación basada en dispositivos en todos los canales. | Diagrama | Diagrama |  |  | Segmentación de audiencias anónima basada en dispositivo |  | 1 | 2 | Una narrativa mínima. Diagrama de arquitectura presente, topología del sistema mostrada. Sin marco de objetivos empresariales; SDK de implementación y conceptos de concentrador/perímetro. |
| help/blueprints/audience-activation/customer-activity.md | Acceso a perfiles en tiempo real para escenarios de soporte y ventas | Habilite el contexto de cliente en tiempo real de agentes de ventas y asistencia mediante la API de búsqueda de perfiles. | Patrón | Patrón | audience-building-activation | Búsqueda de perfil en tiempo real para soporte y ventas |  |  | 3 | 1 | Enmarca el resultado empresarial (contexto del agente). Tiene una lista de comprobación de requisitos previos; pasos de implementación > 30 líneas. Caso de uso único: acceso al perfil de concentrador (no personalización de Edge). Distinto de los patrones de personalización existentes. |
| help/blueprints/audience-activation/data-science.md | Modelo de ciencia de datos personalizada para el enriquecimiento de perfiles | Introduzca puntuaciones del modelo de aprendizaje automático en RTCDP para enriquecer los perfiles de personalización y segmentación. | Patrón | Patrón | audience-building-activation | Ingesta de modelos de ciencia de datos para enriquecimiento de perfiles |  |  | 3 | 1 | Resultado empresarial de los marcos (enriquecimiento para la personalización). Tiene casos de uso y consideraciones; consideraciones de implementación >30 líneas. Céntrese en los flujos de trabajo de ciencia de datos, no en la mensajería/activación. |
| help/blueprints/audience-activation/enterprise-destinations.md | Activación de audiencias y perfiles en destinos empresariales | Transmita o procese cambios de perfil y audiencia en el almacenamiento en la nube y las aplicaciones empresariales para ventas, soporte técnico y análisis. | Diagrama | Diagrama |  |  | Activación de audiencia y perfil de Enterprise |  | 1 | 2 | No tiene objetivos empresariales. Directrices de implementación dispersas. Diagrama de arquitectura + topología del sistema para aplicaciones empresariales/almacenamiento en la nube. Visual-dominante. |
| help/blueprints/audience-activation/real-time-lookup.md | Acceso al perfil de Edge en tiempo real para Personalization web y móvil | Acceda al perfil unificado en el borde en milisegundos para la personalización móvil y web en tiempo real. | Patrón | Patrón | personalización | Acceso al perfil de Edge para Personalization web/móvil |  |  | 5 | 2 | Marco empresarial sólido (personalización de baja latencia). Dos patrones de implementación (Web SDK frente a la API de Edge). Amplios requisitos previos y pasos (más de 30 líneas). KPI implícitos (latencia, rendimiento). |
| help/blueprints/audience-activation/rtcdp-target.md | Personalization de cliente conocido con Target | Comparta audiencias y perfiles de RTCDP con Adobe Target para la personalización móvil y web de visitantes conocidos. | Mixto | División | personalización | Uso compartido de audiencias en tiempo real con Adobe Target | Arquitectura de integración de Target | help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md | 3 | 2 | Se superpone con el patrón de visitante conocido existente, pero con un ámbito más limitado (solo Target). Tres patrones de integración. Se han tenido en cuenta los diagramas de arquitectura + implementación de Edge. Contenido del patrón + diagrama sustanciales → Dividir. |
| help/blueprints/audience-activation/segment-match.md | Audience Collaboration con coincidencia de segmentos | Habilite la colaboración segura con la audiencia de los socios mediante Coincidencia de segmentos con controles de privacidad. | Patrón | Duplicar |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md | 4 | 1 | El patrón existente cubre esto exactamente. Anulación duplicada. Contenido único que conservar en el diagrama: configuración detallada de RBAC/consentimiento/gobernanza y flujo de trabajo de publicidad programática. |
| help/blueprints/b2b/overview.md | Modelos de análisis, activación y marketing B2B | Página de navegación que enumera análisis B2B, activación de audiencia, grupo de compra, Marketo y modelos de Workfront. | Navegación | Navegación |  |  |  |  |  |  | Anular 1: archivo llamado overview.md. Excluido de la migración. |
| help/blueprints/b2b/b2bactivation.md | Modelo de activación de audiencias y perfiles B2B | Active audiencias B2B basadas en cuentas en canales web, de correo electrónico y de publicidad mediante datos de cuenta y perfil. | Patrón | Duplicar |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md | 3 | 1 | Anular 2: existe un patrón equivalente. El modelo es un subconjunto más limitado centrado en la arquitectura. |
| help/blueprints/b2b/b2b-account-activation.md | Activación de cuentas B2B en destinos de Advertising y destinos de archivos | Segmente cuentas B2B a través de LinkedIn y destinos de almacenamiento en la nube mediante la creación y activación de audiencias de cuenta. | Diagrama | Diagrama |  |  | Audience Activation de cuenta B2B |  | 1 | 2 | Marco empresarial mínimo, sin KPI, narrativa mínima. Diagrama de arquitectura presente; topología de LinkedIn/almacenamiento en la nube descrita. Mantener como diagrama. |
| help/blueprints/b2b/b2b-buying-group-journeys.md | Modelo de gestión de Recorridos y marketing basado en grupos de compra | Diseñe recorridos de cuenta que califiquen clientes potenciales en grupos de compra con funciones definidas e intereses de solución. | Patrón | Duplicar |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md | 5 | 2 | Anular 2: existe un patrón equivalente. El modelo tiene contenido de patrón enriquecido, pero el patrón existente es más completo. |
| help/blueprints/b2b/b2b-journeys-with-marketo.md | Recorridos B2B con el modelo de datos de Marketo | Implemente Journey Optimizer B2B edition con datos de Marketo para organizar los recorridos de grupo de compra y la participación de la cuenta. | Patrón | Patrón | b2b | Recorridos de cuenta B2B con integración de datos de Marketo |  |  | 4 | 1 | Marco de negocios fuerte. KPI enumerados; varias opciones de implementación; consideraciones detalladas (>30 líneas). Se diferencia del patrón existente por la profundidad de integración de datos de Marketo (configuración XDM, vinculación de identidad, bloqueo de campos). Rutas a la nueva categoría b2b/. |
| help/blueprints/b2b/ajo-b2b-paid-media-controller.md | AJO B2B - Journey Orchestration de cuenta - Controlador de medios de pago | Orqueste campañas de medios pagados B2B con la lógica de cascada para asignar cuentas a campañas y activarlas en destinos. | Patrón | Patrón | b2b | Orquestación de medios de pago B2B mediante lógica de ruta dividida de cascada |  |  | 4 | 2 | Marco de negocios fuerte. KPI explícitos; varias opciones de implementación; requisitos previos; narrativa de >30 líneas. Distinto del patrón de grupo de compra existente (se centra en la priorización de medios de pago, no en nutrir). Rutas a la nueva categoría b2b/. |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md | Información general sobre Marketo Engage y el modelo de integración de Workfront | Información general sobre la planificación de campañas para la automatización de la ejecución mediante Marketo Engage y Workfront con Fusion. | Navegación | Navegación |  |  |  |  |  |  | Anular 1: archivo llamado overview.md. Excluido de la migración. |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md | Modelo de ingesta y creación | Automatice la admisión de solicitudes de campañas de marketing B2B en la creación mediante formularios Workfront y plantillas de programas de Marketo Engage. | Patrón | Patrón | b2b | Admisión de solicitudes de campaña y creación automatizada de programas |  |  | 4 | 1 | Marco de negocios fuerte en la velocidad de la campaña. KPI implícitos (errores/reducción de reprocesamiento); pasos del flujo de trabajo > 30 líneas; lista de comprobación de preparación. Rutas a la nueva categoría b2b/ (las operaciones Marketo+Workfront son predominantemente B2B). |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md | Revisar y aprobar el modelo | Integre los flujos de trabajo de revisión y aprobación de Workfront con los recursos de correo electrónico de Marketo Engage mediante la automatización de Fusion. | Patrón | Patrón | b2b | Flujo de trabajo de revisión y aprobación de recursos Campaign |  |  | 3 | 2 | Marco empresarial sólido en cuanto a conformidad y precisión; KPI implícitos (velocidad de aprobación); narrativa > 30 líneas; sección de planificación del flujo de trabajo. Rutas a la nueva categoría b2b/. |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md | Historias de éxito de clientes | Vínculos a casos prácticos de clientes y seminarios web que muestran los resultados de la integración de Marketo y Workfront. | Navegación | Navegación |  |  |  |  |  |  | Contenido mínimo (6 hipervínculos). Sin marcos empresariales, KPI, arquitectura ni narrativa. Se trata como navegación. El escritor debería confirmar. |
| help/blueprints/customer-journey-analytics/overview.md | modelos de Customer Journey Analytics | Unificar y analizar los datos y el comportamiento de los clientes desde varios canales para crear vistas basadas en el recorrido. | Navegación | Navegación |  |  |  |  |  |  | Anulación 1: overview.md. Página de aterrizaje de estilo TDC. Excluido de la migración. |
| help/blueprints/customer-journey-analytics/b2b-cja.md | Modelo de Customer Journey Analytics B2B | Informes y análisis CJA basados en cuentas para organizaciones B2B que utilizan la cuenta como modelo de datos principal. | Patrón | Duplicar |  |  |  | help/blueprints/use-case-patterns/analysis/b2b-analytics.md | 4 | 2 | Anulación 2: un patrón equivalente abarca el análisis de nivel de cuenta B2B con CJA B2B edition. Acción: simplificar en diagrama, vínculo cruzado. |
| help/blueprints/customer-journey-analytics/cja-rtcdp.md | Modelo de Customer Journey Analytics con Real-time Customer Data Platform | Cree y publique audiencias de CJA en RTCDP para fines de segmentación y personalización. | Diagrama | Diagrama |  |  | Integración de publicación de audiencias de CJA a RTCDP |  | 1 | 3 | Enfoque de arquitectura sólido (integración de sistema a sistema, forma de implementación). Una narrativa mínima. Contenido único: protecciones de latencia de publicación de audiencias de CJA. |
| help/blueprints/customer-journey-analytics/cja-ajo.md | Modelo de Customer Journey Analytics con Journey Optimizer | Analizar datos de interacción y envío de AJO en CJA; publicar audiencias de CJA en AJO. | Diagrama | Diagrama |  |  | Integración y análisis de CJA con AJO |  | 1 | 3 | Fuerte enfoque en la arquitectura. Una narrativa mínima. Contenido único: patrón bidireccional de uso compartido de datos CJA-AJO. |
| help/blueprints/customer-journey-analytics/analysis.md | Modelo de análisis de datos e inteligencia | Utilice Experience Platform Query Service para el análisis exploratorio de datos del lago de datos. | Diagrama | Diagrama |  |  | Integración de Experience Platform Query Service y la herramienta BI |  | 1 | 3 | Cubre el servicio de consultas, NO específico de CJA. Puede colocarse incorrectamente en la carpeta CJA; considere la posibilidad de reubicarse en experience-platform/. Audiencia de arquitectos sólida (herramientas PostgreSQL, BI). |
| help/blueprints/customer-journeys/overview.md | Modelos de recorrido del cliente | Plataformas de marketing modernas que admiten recorridos impulsados por eventos y campañas iniciadas por la marca en todos los canales. | Navegación | Navegación |  |  |  |  |  |  | Anulación 1: overview.md. TDC para subcategorías de recorrido; describe el posicionamiento de Journey Optimizer y Campaign. |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md | Modelos de Journey Optimizer | Organización de perfiles 1:1 impulsada por eventos y comunicaciones de marca basadas en audiencias entre canales. | Navegación | Navegación |  |  |  |  |  |  | Anulación 1: overview.md. Página de aterrizaje con pestañas de casos de uso y patrones de integración. |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-journeys.md | Journey Optimizer: Mensajería activada y modelo Adobe Experience Platform | Flujos de trabajo impulsados por eventos en tiempo real que ofrecen experiencias personalizadas de varios pasos basadas en los comportamientos de los clientes. | Patrón | Duplicar |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md | 4 | 2 | Anular 2 con advertencia: el agente se ha marcado como probablemente duplicado pero incierto. Compruebe la alineación del ámbito antes de reducir. Las consideraciones de arquitectura pueden ser únicas (actualización del perfil, tiempo de calificación del segmento) y vale la pena preservarlas en el diagrama. |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-campaigns.md | Journey Optimizer: Campaign Orchestration | Comunicaciones programadas de varios pasos y basadas en audiencias en canales salientes: correo electrónico, SMS, push, correo postal. | Patrón | Duplicar |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md | 3 | 2 | Anular 2: patrón equivalente. Varios diagramas de arquitectura; conservar como diagrama. Contenido único: detalles de arquitectura de base de datos relacional/portal de audiencia/perfil delgado. |
| help/blueprints/customer-journeys/journey-optimizer/3rd-party-messaging.md | Journey Optimizer: modelo de mensajería de terceros | Muestra la integración de Journey Optimizer con sistemas de mensajería de terceros para comunicaciones organizadas. | Mixto | División | campaign-management-orchestration | Integración de mensajería de terceros con Journey Optimizer | Arquitectura de mensajería de terceros |  | 2 | 2 | Puntuaciones vinculadas → Split. Diagrama (topología de sistema a sistema) más contenido de patrón (pasos de implementación, restricciones de integración: autenticación de portador, sin IP estáticas, límites de velocidad). Vale la pena preservar ambas. |
| help/blueprints/customer-journeys/decision-management/decision-management-overview.md | Modelos de administración de decisiones | Ofrezca ofertas personalizadas en todos los recorridos del cliente a través de una biblioteca de ofertas y un motor de decisión centralizados. | Navegación | Navegación |  |  |  |  |  |  | Anulación 1: overview.md. Describe los componentes de Administración de decisiones y los enfoques de implementación de Edge vs. Hub. |
| help/blueprints/customer-journeys/decision-management/decision-management-edge.md | Modelo de Gestión de decisiones en Edge | Ofrezca ofertas personalizadas en experiencias web y móviles en tiempo real con latencia de menos de un segundo en la red perimetral. | Mixto | Duplicar |  |  |  | help/blueprints/use-case-patterns/personalization/offer-decisioning.md | 2 | 3 | Anulación 2: asigna a offer-decisioning. Variante de implementación de Edge: considere la posibilidad de consolidar con modelo de concentrador en un único diagrama de opciones de implementación. |
| help/blueprints/customer-journeys/decision-management/decision-management-hub.md | Modelo de Gestión de decisiones en el centro | Ofrezca ofertas personalizadas en varios canales, incluidos quioscos, experiencias asistidas por agentes y envíos salientes. | Mixto | Duplicar |  |  |  | help/blueprints/use-case-patterns/personalization/offer-decisioning.md | 2 | 3 | Anulación 2: asigna a offer-decisioning. Variante de implementación Hub: considere la posibilidad de consolidar con modelo Edge en un único diagrama de opciones de implementación. |
| help/blueprints/customer-journeys/campaign-v8/campaign-v8-overview.md | Modelo, Campaign y plataforma de Campaign v8 | Plataforma de administración de campañas por lotes de próxima generación con funciones de ETL, segmentación y mensajería transaccional. | Patrón | Patrón | campaign-management-orchestration | Orquestación por lotes y mensajería transaccional de Campaign v8 | Modelos de implementación de arquitectura de Campaign v8 |  | 4 | 3 | Enfoque técnico distinto (Campaign v8 nativo, no AJO). Múltiples diagramas de arquitectura; marcos de negocios; KPI implícitos en protecciones (20 millones de msg/h por lotes, 1 millón/h en tiempo real). No hay equivalente en el catálogo de patrones existente. Nota: las puntuaciones también se clasifican como División: el patrón propuesto, pero el escritor puede querer retener el diagrama. |
| help/blueprints/customer-journeys/campaign-v8/rtcdp-and-campaign-v8.md | Patrón de integración de Real-Time CDP con Adobe Campaign v8 | Muestra la integración de audiencias y perfiles de RTCDP con Campaign v8 para mantener conversaciones personalizadas. | Diagrama | Diagrama |  |  | RTCDP: intercambio de audiencia y perfil en la versión 8 de Campaign |  | 1 | 2 | Modelo del conector de integración, no caso de uso independiente. Diagrama + breves requisitos previos/protecciones. Orientado a arquitectos. |
| help/blueprints/customer-journeys/campaign-v8/ajo-and-campaign-v8.md | Modelo de Journey Optimizer con Adobe Campaign v8 | Muestra la orquestación de AJO con mensajes transaccionales de Campaign v8 para experiencias 1:1. | Diagrama | Diagrama |  |  | Integración de mensajería transaccional de Journey Optimizer - Campaign v8 |  | 1 | 2 | Conector de integración. Diagrama + pasos de implementación + restricciones técnicas (acelerador de 4000 msg/5 minutos, solo iniciado por evento). Vínculo cruzado a los patrones de AJO y Campaign v8. |
| help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md | Modelo de Campaign v7 | Obsoleto: mensajería basada en lotes, incorporación, remarketing, correo directo, mensajería transaccional simple. | Navegación | Navegación |  |  |  |  |  |  | PRODUCTO OBSOLETO (vínculos de frontmatter a la versión 8). Contenido mínimo (solo diagrama de arquitectura). No migrar. |
| help/blueprints/customer-journeys/campaign-v7/rtcdp-and-campaign-v7.md | Real-Time CDP con Campaign v7 y patrón de integración de Campaign Standard | Muestra la integración de RTCDP y el Perfil del cliente en tiempo real con Campaign v7/Standard para mantener conversaciones personalizadas. | Diagrama | Diagrama |  |  | RTCDP: intercambio de audiencia y perfil en Campaign v7/Standard |  | 1 | 2 | OBSOLETO. Conector de integración. Diagrama + pasos completos de implementación. No migrar a un patrón nuevo; dejar tal cual. |
| help/blueprints/customer-journeys/campaign-v7/ajo-and-campaign-v7.md | Modelo de Journey Optimizer con Adobe Campaign v7 | Muestra la orquestación de AJO con mensajes transaccionales de Campaign v7 para experiencias 1:1. | Diagrama | Diagrama |  |  | Journey Optimizer: Integración de mensajería transaccional de Campaign v7 |  | 1 | 2 | OBSOLETO. Conector de integración. Diagrama + pasos de implementación + restricciones. No migrar; dejar tal cual. |
