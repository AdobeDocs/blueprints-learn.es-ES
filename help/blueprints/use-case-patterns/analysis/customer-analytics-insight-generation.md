---
title: Generación de Customer Analytics y Insight
description: Learn how to build cross-channel analysis workspaces, computed metrics, and dashboards for behavior and performance analysis.
solution: Customer Journey Analytics, Experience Platform
exl-id: 235a4eb0-91ae-4030-b90e-7eda08c67ae1
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8947'
ht-degree: 1%

---

# Customer analytics &amp; insight generation

This guide provides a complete implementation reference for customer analytics and insight generation. It covers how to connect [!DNL Adobe Experience Platform] datasets to [!DNL Customer Journey Analytics], configure data views, build freeform analysis workspaces, create computed metrics, publish dashboards and mobile scorecards, and optionally publish CJA-defined audiences back to [!DNL Adobe Experience Platform] for activation.

It is designed for solution architects, marketing technologists, and implementation engineers who need to understand all viable implementation paths, the trade-offs between them, and the configuration decisions required at each phase.

Unlike the other patterns in the taxonomy which focus on activation and engagement (sending messages, personalizing content, activating audiences), this pattern focuses on understanding -- analyzing customer behavior, measuring campaign performance, identifying trends, and generating insights that inform strategy and optimization decisions. It is the most commonly composed pattern and pairs with nearly every activation or personalization pattern.

## Use case overview

Organizations need to understand how customers behave across channels, how campaigns perform, where customers drop off in their journeys, which content resonates, and how different segments retain over time. Customer analytics and insight generation addresses this need by connecting the rich cross-channel data in [!DNL Adobe Experience Platform] to [!DNL Customer Journey Analytics], where analysts can build freeform workspaces, create custom metrics, configure attribution models, and publish dashboards for stakeholder consumption.

The pattern serves multiple audiences: marketing analysts who need deep exploratory analysis, campaign managers who need performance dashboards, product managers who need engagement and retention insights, and executives who need at-a-glance KPI scorecards. The implementation approach varies based on the primary analytical focus -- campaign performance measurement, cross-channel journey analysis, analysis-driven audience activation, or guided product insights.

## Key business objectives

The following business objectives are supported by this use case pattern.

**Mejorar análisis e informes**

Mejore las capacidades de creación de informes para obtener perspectivas de marketing más rápidas y procesables mediante paneles unificados y herramientas de autoservicio.

- **KPI:** eficiencia, productividad

Consulte [Mejorar análisis e informes](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md) para obtener más información sobre este objetivo comercial.

**Habilitar la toma de decisiones basada en datos**

Habilite a los equipos con análisis de autoservicio, perspectivas de clientes en tiempo real y predicciones impulsadas por IA para guiar la estrategia.

- **KPI:** eficiencia, productividad

Consulte [Habilitar la toma de decisiones basada en datos](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md) para obtener más información sobre este objetivo empresarial.

**Mejorar la atribución de marketing**

Mida con precisión el impacto de los puntos de contacto de marketing, canales y campañas en los resultados de conversión e ingresos.

- **KPI:** eficiencia, ingresos incrementales

Consulte [Mejorar la atribución de mercadotecnia](/help/blueprints/business-objectives/analytics-insights/improve-marketing-attribution.md) para obtener más información sobre este objetivo comercial.

**Optimizar el gasto y el retorno de la inversión del marketing**

Optimice la asignación del presupuesto de marketing teniendo en cuenta qué canales y campañas ofrecen la mayor rentabilidad.

- **KPI:** eficiencia, ingresos incrementales

Consulte [Optimizar el gasto y el retorno de la inversión del marketing](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md) para obtener más información sobre este objetivo comercial.

## Casos de uso tácticos de ejemplo

A continuación se muestran ejemplos de casos de uso tácticos que se pueden implementar con este patrón.

- Panel de rendimiento de la campaña: métricas de entrega, tasas de participación, conversión y atribución de ingresos en campañas de correo electrónico, SMS, push y de medios de pago
- Análisis de abandonos del recorrido del cliente: identifique dónde abandonan los clientes en los canales de compra, registro o incorporación
- Análisis de retención de cohortes: mida la retención de diferentes cohortes de adquisición en semanas, meses y trimestres
- Modelado de atribución de canal: compare la atribución de primer contacto, último contacto, lineal y de decadencia de tiempo para comprender qué canales generan conversiones
- Análisis del rendimiento del contenido: identifique qué contenido resuena más por segmento, canal y fase del ciclo vital
- Análisis de uso y adopción de productos: efectúe el seguimiento de la adopción de funciones, la frecuencia de la participación y las tendencias de crecimiento del usuario
- Análisis de la fase del ciclo vital del cliente: segmente y analice clientes por fase del ciclo vital (nuevos, activos, en riesgo, caducados).
- Marketing mix optimization dashboard -- compare channel investment against revenue contribution
- Cross-channel engagement scoring and reporting -- build composite engagement scores from web, app, email, and campaign interactions

## Indicadores clave de rendimiento

The following KPIs help measure the success of this use case pattern.

| KPI | Descripción | Measurement approach |
| --- | --- | --- |
| Efficiency | Reduction in time-to-insight and manual reporting effort | Track analyst time spent building reports before and after CJA implementation |
| Productivity | Number of self-service analyses created by business users | Monitor Workspace project creation and dashboard usage |
| Incremental Revenue | Revenue attributed to insights-driven optimization decisions | Measure revenue lift from campaigns optimized based on CJA analysis |
| Conversion Rates | Funnel completion rates across key customer journeys | Track fallout rates at each journey step using CJA fallout visualization |
| Participación | Depth and frequency of customer interaction across channels | Build computed metrics for engagement scoring in CJA |
| Retención | Customer return rates over defined time periods | Use CJA cohort analysis to measure retention curves |

## Use case pattern

**Customer analytics &amp; insight generation**

Build cross-channel analysis workspaces, computed metrics, and dashboards to understand customer behavior and campaign performance.

**Function chain:** Data Connection > Data View Configuration > Workspace Analysis > Computed Metric Creation > Dashboard Publishing

Consulte la sección [Opciones de implementación](#implementation-options) para obtener instrucciones de composición.

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Customer Journey Analytics](CJA)**: conexiones, vistas de datos, análisis del espacio de trabajo, análisis guiado, métricas calculadas, paneles, publicación de audiencias y análisis de contenido
- **[!DNL Adobe Experience Platform](AEP)**: conjunto de datos, esquemas XDM, datos de perfil y evento que alimentan las conexiones de CJA

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Se asume en contexto | perfil de producto de CJA aprovisionado con permisos de creación de espacio de trabajo y acceso de vista de datos. Conjuntos de datos de AEP accesibles para la conexión de CJA. Usuarios asignados a funciones de CJA apropiadas. | [Resumen de control de acceso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | Los esquemas XDM y los conjuntos de datos que se van a conectar a CJA deben existir en AEP. El diseño del esquema influye directamente en las dimensiones y métricas disponibles en las vistas de datos de CJA. Los esquemas de evento necesitan campos con marca de hora; los esquemas de búsqueda necesitan campos clave. | [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home) |
| Fuentes de datos y recopilación | Requerido | Los datos deben fluir a conjuntos de datos de AEP: eventos web a través de Web SDK, eventos de aplicación a través de Mobile SDK, eventos de campaña de AJO, datos CRM a través de conectores de origen. La riqueza del análisis depende de la amplitud de los datos recopilados. | [Resumen de orígenes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| Configuración de identidad y perfil | Requerido | La configuración del ID de persona en la conexión de CJA determina cómo se vinculan los eventos entre conjuntos de datos. La vinculación de identidad entre dispositivos en AEP mejora la capacidad de CJA para crear recorridos de cliente completos. El área de nombres de identidad debe configurarse para el campo ID de persona. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) |
| Definición de audiencia y segmentación | No aplicable | CJA crea sus propios filtros y audiencias dentro del contexto de análisis. Las audiencias de RT-CDP no son un requisito previo, aunque CJA puede volver a publicar audiencias en AEP mediante la publicación de audiencias (Opción C). | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Los atributos calculados de AEP pueden enriquecer los conjuntos de datos conectados a CJA, proporcionando dimensiones y métricas adicionales para el análisis (por ejemplo, recuento de compras de por vida, días transcurridos desde la última actividad). Estas agregaciones de nivel de perfil están disponibles como dimensiones en las vistas de datos de CJA. | [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Administración del ciclo de datos | Recomendado | Las políticas de retención de conjuntos de datos afectan a qué datos históricos están disponibles en CJA. Normalmente, se desea una retención larga para que los análisis permitan comparaciones año tras año y análisis de tendencias a largo plazo. Configure los TTL del conjunto de datos para garantizar una profundidad histórica adecuada. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Etiquetado y aplicación del uso de datos | Recomendado | Las etiquetas de gobernanza de los campos confidenciales pueden restringir lo que aparece en las vistas de datos de CJA. Si se incluyen PII o datos confidenciales en la conexión de CJA, las etiquetas de control de datos garantizan el acceso compatible y evitan la exposición no autorizada en los paneles compartidos. | [Resumen de control de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Monitorización y observabilidad | Recomendado | Se debe supervisar el estado de la conexión de CJA y la actualización de los datos. Configure alertas para los errores y problemas de ingesta del flujo de datos de origen para garantizar que la fuente de datos de CJA sea fiable y esté actualizada. | [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Informes y análisis | Incluido | Esta es la implementación de informes y análisis. Cuando un plan de referencia para otro patrón incluya S5, utilice este plan de generación de insight y análisis de clientes para la implementación de Analytics. | [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Customer Journey Analytics] (CJA)

En la tabla siguiente se enumeran las funciones de aplicación de CJA utilizadas en este patrón.

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Conexión de datos | Fase 1: Conexión de datos | Enlace los conjuntos de datos de AEP a una conexión de CJA para el análisis en canales múltiples, configuración de tipos de conjuntos de datos e ID de persona para la vinculación de conjuntos de datos cruzados |
| Configuración de vista de datos | Fase 2: Configuración de vista de datos | Defina dimensiones, métricas, modelos de atribución, configuración de persistencia, parámetros de sesión y campos derivados que dan forma a la perspectiva analítica |
| Análisis de Workspace | Fase 3: Análisis y creación de métricas | Cree proyectos de análisis de forma libre con tablas, visualizaciones, filtros, anotaciones y desgloses de dimensión (Opciones A, B, C) |
| Análisis guiado | Fase 3: Análisis y creación de métricas | Utilice flujos de trabajo guiados estructurados para funnel, tendencias, retención, crecimiento del usuario y análisis de frecuencia de participación (Opción D) |
| Creación de métricas calculadas | Fase 3: Análisis y creación de métricas | Defina métricas calculadas mediante fórmulas, filtros y funciones para KPI reutilizables como tasa de conversión, puntuación de participación e ingresos por visita |
| Publicación de paneles y cuadros de resultados | Fase 4: Publicación del panel | Cree y comparta paneles interactivos y cuadros de resultados móviles para la creación de informes para las partes interesadas |
| Publicación de audiencias | Fase 5: Publicación de audiencias (solo opción C) | Volver a publicar audiencias definidas por CJA en el Perfil del cliente en tiempo real de AEP para la activación descendente |
| Análisis de contenido | Fase 3: Análisis y creación de métricas | Analizar las tendencias, las anomalías y la fatiga del rendimiento de contenido en las propiedades digitales (cuando el análisis de contenido es el objetivo) |

### [!DNL Adobe Experience Platform] (AEP)

En la tabla siguiente se enumeran las funciones de aplicación de AEP utilizadas en este patrón.

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Lago de datos y conjuntos de datos | Requisito previo (F2, F3) | Proporcione los conjuntos de datos de evento, perfil y búsqueda de origen que alimentan la conexión de CJA |
| Servicio de identidad | Requisito previo (F4) | Proporcione la configuración del área de nombres de identidad para la vinculación de ID de persona entre conjuntos de datos en la conexión de CJA |

## Prerrequisitos

Los siguientes requisitos previos deben cumplirse antes de implementar este patrón de caso de uso.

- [ Se ha proporcionado el derecho de producto de CJA ] para la organización
- [ ] perfiles de producto de CJA están configurados con acceso de usuario apropiado (creación de área de trabajo, acceso a vista de datos)
- [ ]: la zona protegida de AEP contiene los conjuntos de datos de destino con flujo de datos (eventos web, eventos de aplicación, datos de campaña, registros CRM).
- [ ] esquemas XDM se definen para todos los conjuntos de datos de origen con los grupos de campos adecuados
- [ El campo de ID de persona ] se ha identificado y está disponible de forma consistente en todos los conjuntos de datos que se conectarán
- [ ] Las áreas de nombres de identidad están configuradas en AEP para el ID de persona utilizado en la vinculación de conexión de CJA
- [ Se han documentado ] requisitos de las partes interesadas: qué KPI, qué audiencias consumirán los paneles, qué nivel de detalle
- [ ] para cuadros de resultados móviles: las partes interesadas tienen instalada la aplicación móvil de paneles [!DNL Adobe Analytics]
- [ ] para la opción C (Publicación de audiencias): el perfil del cliente en tiempo real de AEP está habilitado en la zona protegida de destino
- [ ] para la opción D (análisis guiado): el SKU de CJA incluye funciones de análisis guiado

## Opciones de implementación

En esta sección se describen las opciones de implementación disponibles para este patrón de caso de uso.

### Opción A: Análisis del rendimiento de la campaña

**Lo mejor para:** Medir y optimizar la efectividad de campañas y recorridos: paneles de campañas de correo electrónico, análisis de funnel de recorrido, comparación de rendimiento de canal e informes de ROI de marketing.

**Cómo funciona:**

Esta opción conecta los conjuntos de datos de recorrido y campaña de AJO con CJA, configura las vistas de datos con métricas de entrega y participación (envíos, envíos, aperturas, clics, devoluciones, cancelaciones de suscripciones), crea paneles de rendimiento de la campaña y publica cuadros de resultados para las partes interesadas del marketing. El objetivo es comprender el rendimiento de las campañas de marketing en los distintos canales y a lo largo del tiempo.

La vista de datos se configura con dimensiones específicas de la campaña (nombre de la campaña, nombre del recorrido, tipo de canal, variante del mensaje) y métricas de envío. Las métricas calculadas se crean para medidas derivadas como la tasa de apertura, la tasa de pulsaciones, la tasa de conversión y los ingresos por mensaje. Los paneles presentan estos KPI con periodos de comparación para el análisis de tendencias.

**Consideraciones clave:**

- Requiere AJO campaign y conjuntos de datos de evento de recorrido en AEP
- Los modelos de atribución deben alinearse con la filosofía de medición de campañas de la organización
- Considere la posibilidad de incluir informes nativos de AJO (para métricas de envío operacionales) y CJA (para el impacto comercial en canales múltiples)

**Ventajas:**

- Creación específica para la medición y optimización de campañas
- Habilita la comparación entre campañas y el análisis de canales combinados
- Las métricas calculadas proporcionan definiciones de KPI estandarizadas en todas las campañas
- Los cuadros de resultados móviles proporcionan un rendimiento rápido para los líderes de marketing

**Limitaciones:**

- Limitado a los datos de campaña y recorrido; no proporciona un contexto de recorrido completo del cliente
- No incluye rutas de recorrido, visitas en el orden previsto ni análisis de cohorte
- La atribución se dirige a puntos de contacto de campaña en lugar del recorrido completo del cliente

**Experience League:**

- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Información general de Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### Opción B: Análisis del recorrido del cliente

**Ideal para:** comprender los recorridos de clientes en canales múltiples: análisis de abandonos, análisis de rutas, retención de cohortes, modelado de atribuciones y análisis de etapas del ciclo vital en puntos de contacto web, aplicaciones, correo electrónico, CRM y sin conexión.

**Cómo funciona:**

Esta opción conecta varios conjuntos de datos de AEP (eventos web, eventos de aplicación, datos CRM, interacciones de campañas, registros transaccionales) para crear una vista unificada multicanal del recorrido del cliente. La vista de datos se configura con dimensiones y métricas que abarcan todos los canales. Las visualizaciones de flujo, visitas en el orden previsto, cohorte y atribución de CJA se utilizan para analizar cómo se mueven los clientes por los recorridos, dónde caen, cómo se retienen los distintos segmentos y qué canales merecen crédito por las conversiones.

Esta es la opción analítica más completa, que proporciona una insight profunda en la experiencia del cliente de extremo a extremo. También es la implementación más compleja, ya que requiere una cuidadosa configuración de ID de persona para la vinculación de conjuntos de datos cruzados y un cuidadoso diseño de vista de datos para exponer las dimensiones y métricas correctas.

**Consideraciones clave:**

- Requiere un ID de persona coherente en todos los conjuntos de datos conectados para un análisis preciso entre canales
- El diseño de esquemas en AEP afecta directamente a la calidad y la profundidad del análisis de CJA
- Más conjuntos de datos en la conexión significa un análisis más completo, pero tiempos de relleno más largos
- El modelado de atribución requiere definiciones de eventos de conversión claras

**Ventajas:**

- Visibilidad completa del recorrido del cliente en canales múltiples
- Conjunto completo de visualizaciones de CJA: flujo, visita en orden previsto, cohorte, atribución, tablas de forma libre
- Permite el descubrimiento de perspectivas invisibles en la creación de informes de un solo canal
- Admite preguntas analíticas complejas sobre el comportamiento de los clientes y el ciclo vital

**Limitaciones:**

- Mayor complejidad de la implementación debido a las conexiones de conjuntos de datos múltiples y la vinculación multicanal
- Requiere una planificación más inicial para la configuración de la vista de datos y los campos derivados
- El relleno para conexiones grandes de varios conjuntos de datos puede llevar días
- La calidad del análisis depende de la integridad y la coherencia de los datos subyacentes

**Experience League:**

- [Información general sobre Conexiones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Visualización de flujo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualización de abandonos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabla de cohortes](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Panel de atribución](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)

### Opción C: Analytics con publicación de audiencias

**Mejor opción para:** Activación basada en análisis: descubra segmentos interesantes mediante el análisis de CJA y, a continuación, vuelva a publicarlos en AEP para su activación mediante destinos RT-CDP, campañas de AJO o recorridos de AJO.

**Cómo funciona:**

Esta opción amplía la opción A o la opción B con la publicación de audiencias desde CJA. Los analistas crean segmentos en CJA utilizando datos de comportamiento en canales múltiples y toda la potencia analítica de los filtros de CJA, y luego publican esas audiencias en el Perfil del cliente en tiempo real de AEP para la activación descendente. Esto reduce la brecha entre insight y la acción: los segmentos descubiertos durante el análisis exploratorio se convierten en audiencias procesables sin necesidad de recreación manual en el Generador de segmentos de AEP.

Las audiencias publicadas aparecen en el portal de audiencias de AEP con el origen &quot;CJA&quot; y se pueden activar en cualquier destino de RT-CDP, utilizarse como objetivos de campaña en AJO o como condiciones de entrada de recorrido.

**Consideraciones clave:**

- Requiere que el perfil del cliente en tiempo real de AEP esté habilitado en la zona protegida de Target
- La conexión de CJA debe tener un ID de persona válido que se resuelva en un área de nombres de identidad de AEP
- Las audiencias publicadas se contabilizan en los derechos de audiencia de AEP de la organización
- La cadencia de actualización debe configurarse en función de los requisitos de activación (una vez, cada 4 horas, diario, semanal)

**Ventajas:**

- Cierra el bucle entre análisis y activación
- Permite el descubrimiento de segmentos de alto valor mediante los datos de comportamiento en canales múltiples de CJA
- Las audiencias definidas en CJA pueden aprovechar dimensiones y filtros que no están disponibles en el Generador de segmentos de AEP
- Admite el refinamiento iterativo de criterios de audiencia basados en perspectivas analíticas

**Limitaciones:**

- Máximo de 75 audiencias publicadas por cliente de CJA
- La evaluación inicial de la audiencia puede tardar hasta 24 horas en conjuntos de datos grandes
- Las audiencias publicadas en CJA no se pueden editar en AEP; los cambios se deben realizar en CJA
- Requiere un área de nombres de identidad y una configuración de perfil adicionales más allá del análisis básico

**Experience League:**

- [Resumen de audiencias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Crear y publicar públicos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)

### Opción D: análisis guiado para equipos de productos

**Lo mejor para:** Información sobre la experiencia del producto: adopción de funciones, tendencias de participación del usuario, análisis de retención, conversión de funnel y análisis de impacto de versiones con los flujos de trabajo de análisis guiados de CJA sin requerir una configuración compleja del proyecto de Workspace de forma libre.

**Cómo funciona:**

Esta opción utiliza el análisis guiado de CJA para la generación estructurada y con plantillas de insight. El análisis guiado proporciona tipos de análisis creados previamente (funnel, tendencias, retención, crecimiento del usuario, frecuencia de participación, impacto de la versión, primer uso y cronología) que guían a los analistas por un flujo de trabajo estructurado para responder preguntas específicas sobre productos y experiencias. Es ideal para los gestores de productos y analistas que necesitan perspectivas rápidas y centradas sin crear proyectos de forma libre desde cero.

La implementación conecta los conjuntos de datos de AEP con CJA, configura una vista de datos con dimensiones y métricas de nivel de evento y, a continuación, utiliza flujos de trabajo de análisis guiados para generar perspectivas. Los resultados se pueden guardar como paneles dentro de proyectos de Workspace para una mayor personalización.

**Consideraciones clave:**

- El análisis guiado requiere la asignación de derechos de producto de CJA que incluye capacidades de análisis guiado
- Es más adecuado para análisis de productos y experiencias que para la medición de rendimiento de campañas
- Proporciona flujos de trabajo estructurados que son más accesibles para los usuarios no analistas
- Se puede combinar con el análisis de Workspace de forma libre para una exploración más profunda

**Ventajas:**

- Menos barreras de entrada: los flujos de trabajo estructurados guían a los usuarios a través del análisis
- Diseñado específicamente para preguntas sobre experiencia del producto (funnel, retención, crecimiento, impacto)
- Obtención de un tiempo de respuesta a insight más rápido para preguntas analíticas comunes
- Los análisis guardados se pueden incrustar en proyectos de Workspace junto con el análisis de forma libre

**Limitaciones:**

- Menos flexible que el análisis de Workspace de forma libre
- Limitado a los tipos de análisis creados previamente (funnel, tendencias, retención, crecimiento, frecuencia, impacto, cronología)
- Las comparaciones de segmentos admiten hasta 3 segmentos simultáneamente
- El análisis de funnel admite un máximo de 15 pasos

**Experience League:**

- [Resumen del análisis guiado](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Vista de funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Vista Retención](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

### Comparación de opciones

La siguiente tabla compara las opciones de implementación disponibles.

| Criterios | Opción A: Rendimiento de la campaña | Opción B: recorrido del cliente | Opción C: Analytics + activación | Opción D: análisis guiado |
| --- | --- | --- | --- | --- |
| Mejor para | Medición y optimización de campañas | Comprensión del recorrido en canales múltiples | Activación de audiencias impulsada por insight | Perspectivas de experiencia del producto |
| Complejidad | Low-Medium | Alta | Alta | Baja |
| Conjuntos de datos obligatorios | Eventos de recorrido/campaña de AJO | Varios conjuntos de datos de canales cruzados | Igual que A o B, más identidad de perfil | Conjuntos de datos de evento con interacciones de producto |
| Visualizaciones clave | Tablas improvisadas, números de resumen, líneas de tendencia | Flujo, visita en orden previsto, cohorte, atribución | Igual que A o B, más publicación de audiencia | Funnel, tendencias, retención, crecimiento |
| Capacidad de activación | No (solo informes) | No (solo informes) | Sí (publica audiencias en AEP) | No (solo informes) |
| Audiencia requerida | Analistas de marketing, administradores de campañas | Analistas de datos, arquitectos de recorridos | Analistas + equipos de activación | Gestores de productos, analistas de crecimiento |
| Funciones de CJA utilizadas | Conexión, Vista de datos, Workspace, Métricas calculadas, Tablero | Conexión, Vista de datos, Workspace, Métricas calculadas, Tablero | Igual que A o B, más Publicación de audiencias | Conexión, Vista de datos, Análisis guiado, Tablero |
| Tiempo hasta el primer insight | Días | Semanas | Semanas | Horas-días |

### Elija la opción correcta

Siga estas directrices para seleccionar la opción de implementación que mejor se adapte a sus necesidades.

- **Si su objetivo principal es medir la efectividad de las campañas** y tiene datos de AJO campaign fluyendo a AEP, comience con **Opción A**. Proporciona la relación tiempo-valor más rápida para la creación de informes de rendimiento de marketing.

- **Si necesita comprender el recorrido completo del cliente** en puntos de contacto web, de aplicación, de correo electrónico y sin conexión, y tiene varios conjuntos de datos con un ID de persona coherente, elija **Opción B**. Proporciona las capacidades analíticas más profundas, pero requiere una inversión inicial mayor en la configuración de vistas de datos.

- **Si desea actuar según las perspectivas** publicando los segmentos descubiertos por CJA en AEP para su activación en RT-CDP o AJO, elija **Opción C**. Esto amplía la opción A o B con publicación de audiencias y requiere la configuración del perfil del cliente en tiempo real de AEP.

- **Si tu equipo necesita información de productos estructurada y rápida** sin la complejidad de los proyectos de Workspace de forma libre, y tu SKU de CJA incluye análisis guiado, elige **Opción D**. Es la forma más rápida de responder a preguntas específicas sobre la experiencia del producto.

- **Muchas organizaciones implementan varias opciones**: la opción A para los paneles de campañas de equipo de marketing, la opción B para el análisis en canales múltiples del equipo de Analytics y la opción D para las perspectivas de autoservicio del equipo de productos. Estas opciones comparten la misma conexión de CJA y la misma infraestructura de vista de datos.

## Fases de implementación

Esta sección detalla las fases de implementación paso a paso para este patrón de caso de uso.

### Fase 1: Conexión de datos

**Función de aplicación:** CJA: Data Connection

Esta fase configura una conexión de CJA que enlaza uno o más conjuntos de datos de AEP a CJA para su análisis. La conexión define qué conjuntos de datos fluyen a CJA, cómo se vinculan los eventos entre conjuntos de datos a través del ID de persona y cómo se incorporan los datos históricos y de flujo continuo. Este es el vínculo fundamental entre el lago de datos de AEP y CJA.

#### Puntos de decisión

Durante esta fase deben tomarse las siguientes decisiones.

>[!NOTE]
>**Decisión: selección de zona protegida de AEP**
>
>¿Qué zona protegida de AEP contiene los conjuntos de datos de origen?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Zona protegida de producción | Datos de clientes activos para informes de producción | Se utiliza para paneles de producción e informes a las partes interesadas |
>| Zona protegida de desarrollo | Pruebas e iteraciones antes de la implementación de producción | Se utiliza para la configuración y validación iniciales antes de pasar a producción |

>[!NOTE]
>**Decisión: selección de conjunto de datos y designación de tipo**
>
>¿Qué conjuntos de datos de AEP se deben incluir en la conexión y qué tipo se debe asignar a cada uno?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Conjuntos de datos de evento | Datos de comportamiento con marca de hora (interacciones web, eventos de aplicación, interacciones de campaña, transacciones) | Requerir un campo de marca de hora; forma el núcleo de la mayoría de los análisis |
>| Buscar conjuntos de datos | Datos de referencia de clave-valor (catálogo de productos, metadatos de campañas, ubicaciones de tiendas) | Unido a los datos de evento mediante una clave compartida; solo se utiliza el estado más reciente |
>| Conjuntos de datos de perfil | Atributos de nivel de persona (nivel de lealtad, valor de duración, atributos CRM) | Proporcionar enriquecimiento en el nivel de la persona; solo se utiliza el estado más reciente |

>[!NOTE]
>**Decisión: configuración de ID de persona**
>
>¿Qué campo sirve como ID de persona para la vinculación de conjuntos de datos cruzados?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| ID de CRM | La organización tiene un identificador CRM coherente en todos los canales | Proporciona la vinculación entre canales más precisa para los clientes conocidos |
>| ECID (Experience Cloud ID) | Análisis principal del comportamiento anónimo en la web/aplicación | Con ámbito de dispositivo; no se vincula entre dispositivos sin resolución de identidad |
>| Correo electrónico (con hash) | El correo electrónico es el identificador común entre conjuntos de datos | Funciona bien cuando el correo electrónico se captura de forma consistente en puntos de contacto |
>| Área de nombres personalizada | La organización utiliza un identificador propio | Debe coincidir con un área de nombres de identidad de AEP para la publicación de audiencias (Opción C) |

>[!NOTE]
>**Decisión: intervalo de relleno**
>
>¿Cuántos datos históricos deben importarse en la conexión?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Todos los datos existentes | Profundidad histórica máxima necesaria para las comparaciones anuales y las tendencias a largo plazo | El relleno para conjuntos de datos grandes (miles de millones de registros) puede tardar días en completarse |
>| Intervalo de fechas personalizado | Solo el historial reciente es relevante o la optimización del almacenamiento es motivo de preocupación | Limita la profundidad histórica disponible para el análisis |
>| Sin relleno | Solo se necesita un análisis orientado al futuro | Configuración de conexión más rápida; no hay datos históricos disponibles hasta que lleguen nuevos datos |

>[!NOTE]
>**Decisión: habilitación de transmisión**
>
>¿Deben entrar nuevos datos en CJA en tiempo casi real?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Habilitar flujo | Se necesitan informes casi en tiempo real (datos disponibles en ~90 minutos tras la ingesta de AEP) | Más común para conexiones de producción; permite el análisis oportuno |
>| Solo lote | La actualización periódica es suficiente y no se necesita flujo continuo | Configuración más sencilla; datos disponibles después del procesamiento por lotes |

#### Configuración de la conexión de datos

**Navegación de la interfaz de usuario:** CJA > Conexiones > Crear nueva conexión

Detalles de configuración clave:

- El nombre y la descripción de la conexión deben seguir las convenciones de nomenclatura organizativa
- Se utiliza el número promedio de eventos diarios para la planificación de la capacidad de CJA
- Todos los conjuntos de datos de una sola conexión deben proceder de la misma zona protegida de AEP
- Los campos de ID de persona deben ser coherentes en todos los conjuntos de datos para lograr una vinculación precisa entre conjuntos de datos
- Compruebe que el campo ID de persona existe y se rellena en cada conjunto de datos antes de agregarlo a la conexión

**Documentación de Experience League:**

- [Información general sobre Conexiones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Crear o editar una conexión](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Administrar conexiones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)
- [protecciones de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)

### Fase 2: Configuración de vista de datos

**Función de aplicación:** CJA: Configuración de vista de datos

Esta fase configura una vista de datos que define cómo aparecen los datos de conexión en el análisis. La vista de datos determina qué campos de esquema se exponen como dimensiones y métricas, cómo se atribuyen y persisten los valores, cómo se definen las sesiones y qué campos derivados transforman los datos sin procesar en componentes listos para el análisis. Se pueden crear varias vistas de datos a partir de una sola conexión para diferentes perspectivas analíticas.

#### Puntos de decisión

Durante esta fase deben tomarse las siguientes decisiones.

>[!NOTE]
>**Decisión: nomenclatura de contenedor**
>
>¿Qué terminología deben utilizar los contenedores para que coincida con el dominio empresarial?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Predeterminado (persona/sesión/evento) | El equipo comprende la terminología estándar de Analytics | Funciona en la mayoría de las implementaciones |
>| Nombres personalizados (por ejemplo, Comprador/Visita/Interacción) | La terminología específica del dominio empresarial mejora la adopción del usuario | Ayuda a las partes interesadas no técnicas a comprender el ámbito del análisis |
>| Nombres B2B (por ejemplo, Cuenta/Participación/Punto de contacto) | Análisis B2B en el que el análisis a nivel de cuenta es el objetivo | Alinea el ámbito del contenedor con los conceptos empresariales B2B |

>[!NOTE]
>**Decisión: tiempo de espera de sesión**
>
>¿Cuánto tiempo de inactividad define un límite de sesión?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| 30 minutos (predeterminado) | Definición de sesión de análisis web estándar | Estándar del sector; se adhiere a la mayoría de los análisis de referencia |
>| 15 minutos | Contenido de formato corto o sitios transaccionales en los que los usuarios completan tareas rápidamente | Crea más sesiones; puede capturar mejor las distintas intenciones del usuario |
>| 60 minutos o más | Contenido de formato largo, interacciones B2B complejas o recorridos con gran volumen de investigación | Menos sesiones; captura la investigación extendida como sesiones únicas |
>| Personalizado con nuevos eventos de sesión | Ciertos eventos (por ejemplo, inicio de aplicación, clics en campañas) siempre deben iniciar una nueva sesión | Proporciona límites de sesión impulsados por lógica empresarial |

>[!NOTE]
>**Decisión: valores predeterminados del modelo de atribución**
>
>¿Qué modelo de atribución predeterminado debe aplicarse a las métricas de conversión?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Último contacto (predeterminado) | El crédito debe ir al punto de contacto más reciente antes de la conversión | Sencillo e intuitivo; puede infravalorar los canales de sensibilización |
>| Primer contacto | Comprender qué canales impulsan la sensibilización y la adquisición iniciales | Útil para el análisis de adquisición; ignora los puntos de contacto de nutrición |
>| Lineal | Todos los puntos de contacto deben compartir el mismo crédito | Distribución equitativa; puede diluir el impacto de los puntos de contacto clave |
>| Deterioro de tiempo | Los puntos de contacto recientes deben recibir más crédito que los distantes | Equilibra la actualización con la contribución histórica |
>| en forma de U | Los puntos de primer y último contacto son los que merecen más crédito | Ideal para comprender los canales de adquisición y cierre |
>| Algorítmico | Atribución impulsada por datos mediante modelos de IA de CJA | El más preciso, pero requiere un volumen de datos de conversión suficiente |

>[!NOTE]
>**Decisión: lógica de campo derivada**
>
>¿Se necesitan reglas empresariales personalizadas para transformar los datos sin procesar en dimensiones preparadas para el análisis?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Clasificación del canal de marketing (caso cuando) | Los códigos de seguimiento sin procesar deben clasificarse en grupos de canales | Caso de uso de campo derivado más común; crítico para el análisis de canal |
>| Clasificación de valor | Los valores continuos deben agruparse en rangos (por ejemplo, niveles de valor de pedido) | Simplifica el análisis de las métricas continuas |
>| Combinación de campos | Los campos de varios orígenes deben combinarse en una sola dimensión | Resulta útil cuando el mismo concepto existe en diferentes rutas de esquema entre conjuntos de datos |
>| Extracción basada en regex | Es necesario analizar los valores estructurados (por ejemplo, extraer el tipo de campaña del código de campaña) | Potente, pero requiere un diseño cuidadoso de patrones regex |

#### Configuración de vista de datos

**Navegación de la interfaz de usuario:** CJA > Vistas de datos > Crear nueva vista de datos

Detalles de configuración clave:

- Seleccione la conexión principal creada en la fase 1
- Configure la zona horaria y el tipo de calendario para que coincidan con los requisitos de informes
- Asignar campos de esquema XDM a dimensiones con la configuración de persistencia (asignación y caducidad) adecuada
- Asigne campos de esquema XDM a métricas con formato (decimal, entero, moneda, porcentaje, tiempo) y configuración de atribución
- Configure reglas de inclusión/exclusión en dimensiones para filtrar valores irrelevantes
- Habilitar la anulación de deduplicación de métricas donde sea necesario para evitar el recuento doble
- Cree campos derivados para la clasificación del canal de marketing, la agrupación de valores o la combinación de campos
- Máximo de 5000 dimensiones y 5000 métricas por vista de datos
- Máximo de 100 campos derivados por vista de datos

#### Dónde divergen las opciones

**Para la opción A (análisis de rendimiento de la campaña):**

Asigne dimensiones específicas de la campaña: nombre de la campaña, nombre del recorrido, tipo de canal, variante del mensaje, línea de asunto. Asignar métricas de entrega: envíos, envíos, aperturas, clics, devoluciones, cancelaciones de suscripción. Configure la atribución en métricas de conversión basadas en la filosofía de medición de campañas.

**Para la opción B (Análisis de recorrido del cliente):**

Asigne dimensiones multicanal: nombre de página, pantalla de aplicación, canal, campaña, producto, tipo de contenido. Asigne métricas de participación y conversión en todos los canales. Configure varios modelos de atribución para el análisis de comparación. Cree campos derivados para la clasificación de canales y la identificación de la fase de recorrido.

**Para la opción D (análisis guiado):**

Asigne dimensiones y métricas de nivel de evento relevantes para el análisis de experiencia del producto: nombre de la función, acción del usuario, tipo de participación. Céntrese en eventos que definen los pasos de funnel, los criterios de retención y las señales de crecimiento.

**Documentación de Experience League:**

- [Resumen de vistas de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [Creación o edición de una vista de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Resumen de configuración de componentes](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configuración de persistencia](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configuración de atribución](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Configuración de formato](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Anulación de duplicación métrica](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication)
- [Incluir/excluir valores](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/include-exclude-values)
- [Configuración de sesión](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)
- [Campos derivados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)

### Fase 3: análisis y creación de métricas

**Función de aplicación:** CJA: Workspace Analysis, CJA: Análisis guiado, CJA: Creación de métricas calculadas

Esta fase crea los espacios de trabajo de análisis (proyectos de forma libre o análisis guiado), las métricas calculadas para KPI derivados, los filtros para análisis segmentados y las anotaciones para eventos clave. Aquí es donde se realiza el valor analítico: creando las tablas, las visualizaciones y las métricas que responden a las preguntas comerciales.

#### Puntos de decisión

Durante esta fase deben tomarse las siguientes decisiones.

>[!NOTE]
>**Decisión: enfoque de análisis**
>
>¿Debe este análisis utilizar proyectos de Workspace de forma libre o flujos de trabajo de análisis guiados?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Workspace de forma libre (opciones A, B y C) | Análisis exploratorio profundo, diseños personalizados, desgloses complejos y visualizaciones avanzadas | Máxima flexibilidad; requiere habilidad de analista; admite todos los tipos de visualización |
>| Análisis guiado (opción D) | Perspectivas del producto estructuradas, respuestas rápidas a preguntas específicas, usuarios menos técnicos | Tiempo de ejecución de insight más rápido; limitado a tipos de análisis creados previamente; guarda en Workspace para una mayor personalización |
>| Ambos | La organización necesita un análisis profundo y perspectivas estructuradas rápidas | Utilice el análisis guiado para preguntas comunes; Workspace para la exploración profunda |

>[!NOTE]
>**Decisión: tipos de visualización**
>
>¿Qué visualizaciones comunican mejor las perspectivas para este caso de uso?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Tabla de forma libre | Exploración de datos detallada con desgloses de dimensión | Base de la mayoría de los análisis; admite hasta 10 niveles de desglose |
>| Visualización de flujo | Explicación del comportamiento de las rutas (flujo de página, transiciones de canal) | Excelente para la detección de rutas de recorrido; puede ser complejo con alta cardinalidad |
>| Visualización de abandonos | Medición de la conversión mediante una secuencia definida de puntos de contacto | Ideal para análisis de funnel; muestra claramente la lista desplegable en cada paso |
>| Tabla de cohortes | Análisis de retención a lo largo del tiempo por cohorte de adquisición | Muestra la eficacia con la que se conservan los distintos grupos; fundamental para el análisis del ciclo vital |
>| Panel de atribución | Comparación de modelos de atribución para métricas de conversión | Comparación de modelos en paralelo; requiere una definición clara del evento de conversión |
>| Número/cambio de resumen | Visualización del KPI ejecutivo con comparación período tras período | Visualización de métricas limpia y rápida; ideal para encabezados de panel |

>[!NOTE]
>**Decisión: fórmulas de métricas calculadas**
>
>¿Qué KPI empresariales requieren métricas calculadas más allá de las métricas de vista de datos base?
>
>| Patrón de métrica | Ejemplo de fórmula | Cuándo usar |
>| --- | --- | --- |
>| Proporción/tasa | Pedidos / Visitas | Tasa de conversión, tasa de pulsaciones, tasa de salida hacia otro sitio |
>| Métrica filtrada | Ingresos (donde canal = &quot;correo electrónico&quot;) | Medidas específicas del canal o del segmento |
>| Promedio por elemento | Ingresos / Pedidos | Valor de pedido promedio, ingresos por visita |
>| Fórmula compuesta | (Ingresos - Coste) / Ingresos | Porcentaje de margen, cálculos de ROI |
>| Puntuación de participación | Suma ponderada de interacciones | Puntuación de participación compuesta en varios canales |

#### Configuración de análisis y métricas

**Navegación por la interfaz de usuario:**

- Workspace: CJA > Workspace > Proyectos > Crear proyecto > Proyecto en blanco
- Análisis guiado: CJA > Inicio > Análisis guiado (o Workspace > Crear > Análisis guiado)
- Métricas calculadas: CJA > Componentes > Métricas calculadas > Crear
- Filtros: CJA > Componentes > Filtros > Crear filtro

Detalles de configuración clave:

- Seleccione la vista de datos creada en la fase 2 como vista de datos del proyecto
- Establezca intervalos de fechas y periodos de comparación adecuados para el análisis
- Cree tablas improvisadas arrastrando dimensiones a filas y métricas a columnas
- Añada desgloses de dimensión para explorar datos en niveles más profundos (por ejemplo, canal por campaña, página por producto)
- Crear filtros reutilizables (segmentos) para análisis específicos de la audiencia (ámbito de nivel de persona, de sesión o de nivel de evento).
- Añada anotaciones para marcar eventos comerciales clave (lanzamientos de productos, campañas, incidentes)
- Establezca el formato de la métrica calculada (decimal, porcentaje, moneda, tiempo) y la polaridad (la subida es buena / la subida es mala)
- Compartir proyectos de Workspace con usuarios de CJA en permisos de visualización o edición

#### Dónde divergen las opciones

**Para la opción A (análisis de rendimiento de la campaña):**

Cree tablas de forma libre con dimensiones de campaña desglosadas por métricas de entrega y participación. Cree métricas calculadas para la tasa de apertura, la tasa de pulsaciones, la tasa de conversión, los ingresos por mensaje y el ROI de la campaña. Añada visualizaciones de tendencias para rastrear el rendimiento de la campaña a lo largo del tiempo. Comparar variantes de campaña con la comparación de segmentos.

**Para la opción B (Análisis de recorrido del cliente):**

Cree visualizaciones de visitas en el orden previsto para identificar los puntos de entrega de recorrido. Cree visualizaciones de flujo para descubrir patrones de navegación entre canales. Genere tablas de cohorte para medir la retención por cohorte de adquisición. Configure el panel de atribución para comparar los modelos de atribución para las métricas de conversión. Cree métricas calculadas para la tasa de finalización de recorridos, la puntuación de participación en canales múltiples y la conversión de la fase del ciclo vital.

**Para la opción C (Analytics con publicación de audiencias):**

Cree los espacios de trabajo de análisis a partir de la opción A o B e identifique los segmentos de alto valor o de bajo rendimiento durante el análisis. Cree filtros CJA que capturen estos segmentos para publicarlos en la fase 5.

**Para la opción D (análisis guiado):**

Seleccione el tipo de análisis guiado adecuado en función de la pregunta comercial. Configure eventos clave, intervalos de fechas, métodos de recuento y comparaciones de segmentos. Guarde los análisis completados como paneles en proyectos de Workspace para una mayor personalización.

**Documentación de Experience League:**

- [Información general de Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Crear un proyecto](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabla de forma libre](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Visualización de flujo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualización de abandonos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabla de cohortes](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Panel de atribución](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Dimensiones de desglose](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)
- [Resumen de filtros](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Creación de filtros](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Resumen de anotaciones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [Resumen de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Creación de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Funciones de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-functions)
- [Resumen del análisis guiado](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Vista de funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Vista de tendencias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Vista Retención](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/retention/retention-rates)
- [Vista de crecimiento activo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/user-growth/active)
- [Vista de frecuencia de participación](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/frequency)
- [Vista de impacto de versión](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/impact/release)
- [Análisis de contenido](https://experienceleague.adobe.com/es/docs/analytics-platform/using/content-analytics/content-analytics)

### Fase 4: Publicación del panel

**Función de la aplicación:** CJA: Publicación de tableros y cuadros de resultados

Esta fase crea paneles interactivos (proyectos de Workspace) y cuadros de resultados móviles que ofrecen visibilidad de KPI a las partes interesadas. Los paneles proporcionan visibilidad ejecutiva y operativa a través de números de resumen, líneas de tendencia, desgloses y anotaciones. Los cuadros de resultados móviles proporcionan datos de rendimiento de un vistazo a través de la aplicación móvil de paneles de [!DNL Adobe Analytics].

#### Puntos de decisión

Durante esta fase deben tomarse las siguientes decisiones.

>[!NOTE]
>**Decisión: tipo de panel**
>
>¿Se trata de un tablero de Workspace de escritorio, un cuadro de resultados móvil o ambos?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Proyecto de Workspace (escritorio) | Paneles interactivos detallados para analistas y especialistas en marketing | Funciones de visualización completas; admite paneles, tablas y diseños complejos |
>| Cuadro de resultados móvil | KPI de un vistazo para ejecutivos e interesados en dispositivos móviles | Limitado a 16 mosaicos; números de resumen con minigráficos de tendencia; requiere aplicación móvil |
>| Ambos | La organización necesita análisis detallados e informes móviles de nivel ejecutivo | Separe los artefactos, pero puede compartir la misma vista de datos y las mismas métricas calculadas |

>[!NOTE]
>**Decisión: compartiendo modelo**
>
>¿Quién debe recibir el tablero y cómo?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Compartir con usuarios específicos | Audiencia limitada con necesidades de acceso específicas | Control más granular; requiere administración de usuarios individuales |
>| Compartir con el grupo de perfiles del producto | Acceso de nivel de equipo alineado con las funciones organizativas | Eficiente para la distribución en todo el equipo; administrado mediante perfiles de producto de CJA |
>| Programar envío de correo electrónico | Informes PDF/CSV recurrentes para las partes interesadas que no inician sesión en CJA | Envío automatizado; la frecuencia máxima es por hora; formatos PDF y CSV |

>[!NOTE]
>**Decisión: visibilidad de anotación**
>
>¿Deben anotarse los eventos clave en las líneas de tendencia del panel?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Sí — crear anotaciones | Las principales campañas, lanzamientos de productos, incidentes del sitio o eventos de temporada pueden explicar las tendencias de los datos | Las anotaciones aparecen como marcadores en gráficos de líneas y tendencias del cuadro de resultados; proporcionan contexto para picos o caídas de datos |
>| No | La audiencia del panel está familiarizada con el contexto empresarial y las anotaciones añadirían desorden | Presentación visual más sencilla |

#### Configuración de paneles

**Navegación por la interfaz de usuario:**

- Paneles de Workspace: CJA > Workspace > Crear proyecto
- Cuadros de resultados móviles: CJA > Proyectos > Crear > Cuadro de resultados móvil
- Uso compartido: CJA > Workspace > Compartir > Compartir con usuarios de Workspace
- Envío programado: CJA > Workspace > Compartir > Programar proyecto

Detalles de configuración clave:

- En los cuadros de resultados móviles, cree mosaicos que muestren una sola métrica con un número de resumen y una tendencia del minigráfico
- Configure intervalos de fechas y períodos de comparación predeterminados (por ejemplo, últimos 30 días frente a período anterior o mes tras mes).
- Añadir filtros de ámbito de audiencia que los ejecutivos puedan activar en los cuadros de resultados móviles
- Configuración del envío de correo electrónico programado para informes recurrentes de PDF o CSV
- Máximo de 16 mosaicos por cuadro de resultados móvil; máximo de 15 paneles por proyecto de Workspace
- Las anotaciones están limitadas a 100 por vista de datos

**Documentación de Experience League:**

- [Creación de un cuadro de resultados móvil](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Configurar y depurar informes de valoración](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Paneles de Adobe Analytics: guía ejecutiva](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [Uso compartido de proyectos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Programar proyectos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Visualización de número de resumen](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/summary-number-change)
- [Intervalos de fechas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

### Fase 5: Publicación de audiencias (solo opción C)

**Función de aplicación:** CJA: Publicación de audiencias

Esta fase configura la publicación de audiencias de CJA para devolver los segmentos descubiertos por el análisis al Perfil del cliente en tiempo real de AEP para su activación descendente en destinos RT-CDP, campañas de AJO o recorridos de AJO.

#### Puntos de decisión

Durante esta fase deben tomarse las siguientes decisiones.

>[!NOTE]
>**Decisión: Actualizar cadencia**
>
>¿Con qué frecuencia se debe actualizar la pertenencia a la audiencia?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Única vez (instantánea) | Audiencia específica de la campaña que no necesita una actualización continua | No hay procesamiento en curso; debe volver a publicar las actualizaciones |
>| Cada 4 horas | Requisitos de activación en tiempo casi real | Mayor coste de procesamiento; la mejor opción para audiencias con tiempos limitados |
>| Diario | Cadencia de activación de marketing estándar | Actualización y coste equilibrados; opción más habitual |
>| Semanalmente | Audiencias estables y de cambio lento | Procesamiento mínimo; adecuado para segmentos a largo plazo |

>[!NOTE]
>**Decisión: área de nombres de identidad**
>
>¿Qué área de nombres de identidad debe utilizar CJA para la resolución de miembros de audiencia?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| ID de CRM | Identificador de cliente principal de la organización | La mejor precisión para la coincidencia de clientes conocida |
>| ECID | Principalmente audiencias basadas en aplicaciones/web | Con ámbito de dispositivo; puede que no se resuelva en todos los registros de perfil |
>| Correo electrónico (con hash) | El correo electrónico es el identificador común de la activación | Debe coincidir con el área de nombres utilizada en la configuración de identidad de AEP |
>| Área de nombres personalizada | Identificador de propietario utilizado en la organización | Debe configurarse en el servicio de identidad de AEP |

#### Configurar publicación de audiencias

**Navegación de la interfaz de usuario:** CJA > Componentes > Audiencias > Publicar audiencia

Detalles de configuración clave:

- Defina criterios de audiencia mediante los filtros de CJA (ámbito de persona, sesión o contenedor de evento)
- Seleccione la vista de datos y el filtro que desea publicar
- Configuración del área de nombres de identidad para la resolución de perfiles de AEP
- Establezca la cadencia de actualización en función de las necesidades de activación
- Monitorizar el estado de publicación en la lista Audiencias de CJA (columna Componentes > Audiencias > Estado)
- Compruebe que la audiencia aparece en AEP Audience Portal (Audiencias > Examinar > Filtrar por origen &quot;CJA&quot;)
- Máximo de 75 audiencias publicadas por cliente de CJA (en todos los entornos limitados)
- La evaluación inicial de la audiencia puede tardar hasta 24 horas en conjuntos de datos grandes

**Documentación de Experience League:**

- [Resumen de audiencias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Crear y publicar públicos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
- [Administrar audiencias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/manage)
- [Información general de Audience Portal](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-portal)

## Consideraciones sobre la implementación

Esta sección abarca protecciones, escollos comunes, prácticas recomendadas y decisiones de compensación para este patrón de caso de uso.

### Protecciones y límites

Esta implementación se rige por las siguientes limitaciones y limitaciones.

- **Límites de conexión:** El número máximo de conexiones por organización está limitado por el SKU de CJA. Una sola conexión solo puede incluir conjuntos de datos de una zona protegida de AEP. — [protecciones de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)
- **Límites de vista de datos:** Máximo de 5000 dimensiones y 5000 métricas por vista de datos. Máximo de 100 campos derivados por vista de datos con hasta 5 niveles de funciones anidadas.
- **Límites de Workspace:** Máximo de 40 paneles por proyecto. Las tablas de forma libre admiten hasta 10 desgloses de dimensión. Máximo de 50 000 filas por solicitud de informe.
- **Límites del cuadro de resultados:** Máximo de 16 mosaicos por cuadro de resultados móvil.
- **Latencia de streaming:** Los datos de streaming suelen estar disponibles en CJA en los 90 minutos posteriores a la ingesta de AEP.
- **Límites de publicación de audiencias:** Máximo de 75 audiencias publicadas por cliente de CJA. La cadencia mínima de actualización es cada 4 horas.
- **Límites del análisis guiado:** El análisis de Funnel admite un máximo de 15 pasos. Las comparaciones de segmentos admiten hasta 3 segmentos a la vez.

### Peligros comunes

Tenga en cuenta los siguientes problemas comunes al implementar este patrón.

- **El ID de persona no coincide en todos los conjuntos de datos:** Todos los conjuntos de datos de una conexión deben utilizar un campo de ID de persona coherente para el análisis de conjuntos de datos cruzados. Los ID de persona no coincidentes resultan en vistas de cliente fragmentadas en las que la misma persona aparece como varias personas. Compruebe la coherencia del ID de persona antes de crear la conexión.

- **El relleno tarda mucho tiempo de forma inesperada:** Los conjuntos de datos grandes con miles de millones de registros pueden tardar días en rellenarse. Planifique esto durante los plazos de implementación e inicie el relleno antes de tiempo. Monitorice el progreso en la vista de detalles de la conexión.

- **Vista de datos que muestra &quot;No especificado&quot; para la mayoría de los valores de dimensión:** El campo de esquema asignado puede estar escasamente relleno en los datos de origen. Compruebe la calidad de los datos del conjunto de datos de origen antes de asumir un error de configuración. Considere utilizar un campo derivado para controlar valores nulos.

- **Los recuentos de sesiones parecen incorrectos:** La configuración del tiempo de espera de la sesión afecta drásticamente a las métricas de ámbito de sesión. Un tiempo de espera muy corto crea más sesiones; un tiempo de espera muy largo crea menos. Los nuevos eventos de inicio de sesión también pueden fragmentar sesiones inesperadamente. Revise y pruebe la configuración de la sesión con los patrones de comportamiento conocidos del usuario.

- **El modelo de atribución no se aplica como se esperaba:** Los modelos de atribución solo se aplican a métricas, no a dimensiones. Compruebe que la ventana retrospectiva está configurada correctamente para el ciclo empresarial. Las ventanas retrospectivas cortas pueden perder los puntos de contacto iniciales de funnel.

- **Métricas calculadas que devuelven ceros o valores inesperados:** Compruebe que las métricas base a las que se hace referencia en la fórmula tienen datos en la vista de datos de destino para el intervalo de fechas seleccionado. Compruebe la división por cero en las métricas de proporción. Recupere la definición de la métrica y verifique la estructura de la fórmula.

- **Error en la publicación de audiencias (Opción C):** La conexión de CJA debe tener un Id. de persona válido que se resuelva en un área de nombres de identidad de AEP. Compruebe la configuración del área de nombres de identidad y que el Perfil del cliente en tiempo real de AEP esté habilitado en la zona protegida de Target.

### Prácticas recomendadas

Siga estas prácticas recomendadas para una implementación exitosa.

- **Comience con una sola conexión completa:** Cree una conexión que incluya todos los conjuntos de datos relevantes y, a continuación, cree varias vistas de datos para diferentes perspectivas analíticas. Esto evita la proliferación de conexiones y simplifica la administración.

- **Utilice campos derivados para la clasificación de canales de marketing:** En lugar de depender de los códigos de seguimiento sin procesar, cree campos derivados con la lógica Case When para clasificar el tráfico en los canales de marketing. Esto garantiza unos informes de canal coherentes en todos los análisis.

- **Crear un diccionario de métricas:** Documente todas las métricas calculadas con sus fórmulas, uso previsto e intervalos de valores esperados. Comparta este diccionario con el equipo de análisis para garantizar un uso coherente de las métricas en todos los proyectos.

- **Diseñe vistas de datos para su audiencia:** Cree vistas de datos independientes para diferentes grupos de partes interesadas: una vista de datos de marketing con dimensiones y métricas centradas en la campaña y una vista de datos de producto con dimensiones de características y participación. Esto simplifica las listas de componentes para cada grupo de usuarios.

- **Anotar todo:** Cree anotaciones para lanzamientos de campañas, cambios de sitio, incidentes técnicos, temporadas y cualquier evento que pueda explicar las tendencias de datos. Las anotaciones proporcionan un contexto crítico al revisar los paneles meses después.

- **Probar métricas calculadas con cálculos manuales:** Antes de confiar en una métrica calculada para paneles, ejecute un informe con la métrica calculada y sus componentes base uno al lado del otro. Compruebe que los valores calculados coinciden con un cálculo manual.

- **Use los filtros estratégicamente:** Cree filtros reutilizables para patrones de segmentación comunes (nuevos o recurrentes, móviles o de escritorio, por ubicación geográfica). Aplíquelos como filtros de nivel de panel en lugar de incrustarlos en cada tabla de forma libre.

- **Supervise regularmente el estado de la conexión:** Compruebe la vista de detalles de conexión para ver si hay registros omitidos, lotes con errores y retrasos de flujo continuo. Los problemas de calidad de los datos en el nivel de conexión afectan a todos los análisis descendentes.

### Decisiones de compensación

Tenga en cuenta los siguientes aspectos clave al planificar la implementación.

>[!NOTE]
>**Compensación: Profundidad del análisis frente al tiempo de espera de insight**
>
>La opción B (Análisis del recorrido del cliente) proporciona la información más profunda entre canales, pero requiere una inversión inicial significativa en la configuración de la conexión, el diseño de la vista de datos y la creación de campos derivados. La opción D (Análisis guiado) ofrece un tiempo de respuesta de insight más rápido con flujos de trabajo estructurados, pero ofrece menos flexibilidad analítica.
>
>- **La opción B favorece:** comprensión completa, análisis multicanal complejo, modelado de atribución, desarrollo de KPI personalizado
>- **Favoritos de la opción D:** Velocidad, accesibilidad para usuarios que no son analistas, preguntas estructuradas sobre la experiencia del producto
>- **Recomendación:** Comience con la opción D para obtener información inmediata del producto mientras crea la infraestructura de la opción B en paralelo. Muchas organizaciones ejecutan ambas simultáneamente para equipos diferentes.

>[!NOTE]
>**Compensación: integridad del relleno frente a preparación de la conexión**
>
>La importación de todos los datos históricos proporciona la máxima profundidad analítica para comparaciones año tras año y análisis de tendencias a largo plazo, pero el relleno para conjuntos de datos grandes puede tardar días. Al limitar el relleno a un período reciente, la conexión se prepara más rápido, pero el análisis histórico se ve limitado.
>
>- **Todos los datos favorecen:** Análisis de tendencias a largo plazo, comparaciones año tras año, análisis de cohorte con historial extendido
>- **Favoritos de relleno limitados:** Preparación de conexión más rápida, tiempo más rápido para el primer tablero, optimización del almacenamiento
>- **Recomendación:** Rellene todos los datos de las conexiones de producción que admitan el análisis estratégico. Utilice un relleno limitado para conexiones de desarrollo e implementaciones de prueba de concepto.

>[!NOTE]
>**Compensación: vista de datos integral única vs. múltiples vistas de datos enfocadas**
>
>Una sola vista de datos con todas las dimensiones y métricas proporciona un espacio de trabajo analítico unificado, pero puede saturar a los usuarios con listas de componentes. Varias vistas de datos centradas (una por equipo o caso de uso) simplifican la experiencia del componente, pero requieren mantener varias configuraciones.
>
>- **Favoritos de vista de datos única:** Análisis unificado, desgloses entre dominios, administración más sencilla
>- **Varias vistas de datos favorecen:** listas de componentes más limpias, terminología específica del equipo, diferentes definiciones de sesión por caso de uso
>- **Recomendación:** Comience con una vista de datos principal y, a continuación, cree vistas de datos enfocadas adicionales si la complejidad de la lista de componentes se convierte en una barrera para la adopción. Todas las vistas de datos pueden hacer referencia a la misma conexión.

>[!NOTE]
>**Compensación: flujo en tiempo real vs. ingesta por lotes**
>
>Al habilitar la transmisión en la conexión de CJA, se proporcionan datos casi en tiempo real (en ~90 minutos tras la ingesta de AEP), pero se procesan más datos de forma continua. La ingesta solo por lotes procesa los datos periódicamente y puede introducir retrasos.
>
>- **Favoritos de streaming:** Informes oportunos, monitorización de campañas activas y paneles casi en tiempo real
>- **Favoritos solo por lotes:** Configuración más sencilla, ventanas de procesamiento predecibles, suficiente para generar informes semanales o mensuales
>- **Recomendación:** Habilitar la transmisión por secuencias para las conexiones de producción. El coste de procesamiento incremental es mínimo en comparación con el valor de los datos oportunos para la monitorización de campañas activas y los paneles operativos.

## Documentación relacionada

Los siguientes recursos proporcionan información adicional para este patrón de caso de uso.

### [!DNL Customer Journey Analytics]: Introducción

- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [protecciones de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)

### Conexiones

- [Información general sobre Conexiones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Crear o editar una conexión](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Administrar conexiones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)

### Vistas de datos

- [Resumen de vistas de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [Creación o edición de una vista de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Resumen de configuración de componentes](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configuración de persistencia](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configuración de atribución](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Configuración de formato](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Anulación de duplicación métrica](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication)
- [Incluir/excluir valores](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/include-exclude-values)
- [Configuración de sesión](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)
- [Campos derivados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)

### Workspace y análisis

- [Información general de Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Crear un proyecto](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabla de forma libre](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Visualización de flujo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualización de abandonos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabla de cohortes](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Panel de atribución](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Dimensiones de desglose](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)
- [Uso compartido de proyectos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Programar proyectos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Información general de exportación](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/export/export-cloud)

### Análisis guiado

- [Resumen del análisis guiado](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Vista de funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Vista de tendencias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Vista de frecuencia de participación](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/frequency)
- [Vista Retención](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/retention/retention-rates)
- [Vista de crecimiento activo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/user-growth/active)
- [Vista de impacto de versión](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/impact/release)
- [Primera vista de impacto de uso](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/impact/first-use)
- [Vista Cronología](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/streams/timeline)

### Componentes

- [Resumen de filtros](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Creación de filtros](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Resumen de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Creación de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Funciones de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-functions)
- [Resumen de anotaciones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [Intervalos de fechas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)
- [Componente Métricas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/apply-create-metrics)

### Publicación de audiencias

- [Resumen de audiencias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Crear y publicar públicos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
- [Administrar audiencias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/manage)

### Análisis de contenido

- [Análisis de contenido](https://experienceleague.adobe.com/es/docs/analytics-platform/using/content-analytics/content-analytics)
- [Configuración de Content Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/config/configuration)

### Paneles y cuadros de resultados

- [Creación de un cuadro de resultados móvil](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Configurar y depurar informes de valoración](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Paneles de Adobe Analytics: guía ejecutiva](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [Visualización de número de resumen](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/summary-number-change)

### Fundamentos de AEP

- [Información general sobre conjuntos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/overview)
- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Resumen de orígenes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general de Audience Portal](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-portal)

### Integración de informes de AJO

- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Informe de correo electrónico de Campaign](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/campaign-global-report-cja-email)
- [informe de correo electrónico de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/journey-global-report-cja-email)

### Tutoriales y guías

- [Conceptos básicos de composición](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
