---
title: Generación de Customer Analytics y Insight
description: Aprenda a crear espacios de trabajo de análisis en canales múltiples, métricas calculadas y paneles para el análisis de comportamiento y rendimiento.
solution: Customer Journey Analytics, Experience Platform
exl-id: 235a4eb0-91ae-4030-b90e-7eda08c67ae1
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 3%

---

# Generación de Customer Analytics y insight

En esta guía se describe el patrón de casos de uso de generación de insight y Customer Analytics, que conecta conjuntos de datos de [!DNL Adobe Experience Platform] a [!DNL Customer Journey Analytics] para generar vistas de datos, espacios de trabajo de análisis de forma libre, métricas calculadas, paneles y cuadros de resultados móviles, y para publicar de forma opcional audiencias definidas por CJA de nuevo en [!DNL Adobe Experience Platform] para su activación.

Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

A diferencia de los otros patrones de la taxonomía que se centran en la activación y la participación (envío de mensajes, personalización de contenido, activación de audiencias), este patrón se centra en la comprensión, análisis del comportamiento del cliente, medición del rendimiento de la campaña, identificación de tendencias y generación de perspectivas que informan las decisiones de estrategia y optimización.

## Patrón de caso de uso

**Generación de Customer Analytics y insight**

Cree espacios de trabajo de análisis en canales múltiples, métricas calculadas y paneles para comprender el comportamiento de los clientes y el rendimiento de las campañas.

**Plan de ejecución:** Conexión de datos > Configuración de vista de datos > Workspace Analysis > Publicación de panel

## Resumen del caso de uso

Las organizaciones necesitan comprender cómo se comportan los clientes en los distintos canales, cómo funcionan las campañas, dónde abandonan los clientes en sus recorridos, qué contenido resuena y cómo se conservan los distintos segmentos a lo largo del tiempo. La generación de insight y Customer Analytics resuelve esta necesidad conectando los datos enriquecidos de canales cruzados de [!DNL Adobe Experience Platform] a [!DNL Customer Journey Analytics], donde los analistas pueden crear espacios de trabajo improvisados, crear métricas personalizadas, configurar modelos de atribución y publicar paneles para el consumo de las partes interesadas.

El patrón sirve para varias audiencias: analistas de marketing que necesitan un análisis exploratorio profundo, administradores de campañas que necesitan paneles de rendimiento, administradores de productos que necesitan perspectivas de participación y retención, y ejecutivos que necesitan cuadros de resultados de KPI de un vistazo. El enfoque de implementación varía en función del enfoque analítico principal: medición del rendimiento de la campaña, análisis de recorrido en canales múltiples, activación de audiencia basada en análisis o perspectivas de producto guiadas.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

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
- Panel de optimización de la combinación de marketing: compare la inversión en el canal con la contribución de ingresos
- Informes y puntuación de participación en canales múltiples: cree puntuaciones de participación compuestas a partir de interacciones web, de aplicaciones, de correo electrónico y de campañas

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir el éxito de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Eficiencia | Reducción del tiempo de respuesta a insight y del esfuerzo manual de creación de informes | Rastree el tiempo invertido por el analista en la creación de informes antes y después de la implementación de CJA |
| Productividad | Número de análisis de autoservicio creados por usuarios empresariales | Monitorizar la creación de proyectos y el uso de tableros de Workspace |
| Ingresos incrementales | Ingresos atribuidos a decisiones de optimización basadas en las perspectivas | Mida el aumento de ingresos de las campañas optimizadas en función del análisis de CJA |
| Tasas de conversión | Tasas de finalización de funnel en recorridos clave del cliente | Rastrear tasas de abandonos en cada paso del recorrido mediante la visualización de abandonos de CJA |
| Participación | Profundidad y frecuencia de la interacción del cliente entre canales | Cree métricas calculadas para la puntuación de participación en CJA |
| Retención | Tasas de retorno del cliente en períodos de tiempo definidos | Uso del análisis de cohorte de CJA para medir curvas de retención |

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Customer Journey Analytics] (CJA)**: conexiones, vistas de datos, análisis del espacio de trabajo, análisis guiado, métricas calculadas, paneles, publicación de audiencias y análisis de contenido
- **[!DNL Adobe Experience Platform] (AEP)**: conjunto de datos, esquemas XDM, datos de perfil y evento que alimentan las conexiones de CJA

## Documentación relacionada

Los siguientes recursos proporcionan información adicional para este patrón de caso de uso.

### [!DNL Customer Journey Analytics]: Introducción

- [Información general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview)
- [protecciones de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-admin/guardrails)

### Conexiones

- [Información general sobre Conexiones](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-connections/overview)
- [Crear o editar una conexión](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-connections/create-connection)
- [Administrar conexiones](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-connections/manage-connections)

### Vistas de datos

- [Resumen de vistas de datos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/data-views)
- [Creación o edición de una vista de datos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Resumen de configuración de componentes](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configuración de persistencia](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configuración de atribución](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Configuración de formato](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Anulación de duplicación métrica](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication)
- [Incluir/excluir valores](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/include-exclude-values)
- [Configuración de sesión](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/session-settings)
- [Campos derivados](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/derived-fields)

### Workspace y análisis

- [Información general de Workspace](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/home)
- [Crear un proyecto](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabla de forma libre](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Visualización de flujo](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualización de abandonos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabla de cohortes](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Panel de atribución](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Dimensiones de desglose](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)
- [Uso compartido de proyectos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Programar proyectos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Información general de exportación](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/export/export-cloud)

### Análisis guiado

- [Resumen del análisis guiado](https://experienceleague.adobe.com/es/docs/analytics-platform/using/guided-analysis/overview)
- [Vista de funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Vista de tendencias](https://experienceleague.adobe.com/es/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Vista de frecuencia de participación](https://experienceleague.adobe.com/es/docs/analytics-platform/using/guided-analysis/trends/frequency)
- [Vista Retención](https://experienceleague.adobe.com/es/docs/analytics-platform/using/guided-analysis/retention/retention-rates)
- [Vista de crecimiento activo](https://experienceleague.adobe.com/es/docs/analytics-platform/using/guided-analysis/user-growth/active)
- [Vista de impacto de versión](https://experienceleague.adobe.com/es/docs/analytics-platform/using/guided-analysis/impact/release)
- [Primera vista de impacto de uso](https://experienceleague.adobe.com/es/docs/analytics-platform/using/guided-analysis/impact/first-use)
- [Vista Cronología](https://experienceleague.adobe.com/es/docs/analytics-platform/using/guided-analysis/streams/timeline)

### Componentes

- [Resumen de filtros](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Creación de filtros](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Resumen de métricas calculadas](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Creación de métricas calculadas](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Funciones de métricas calculadas](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-functions)
- [Resumen de anotaciones](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/annotations/overview)
- [Intervalos de fechas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)
- [Componente Métricas](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/apply-create-metrics)

### Publicación de audiencias

- [Resumen de audiencias](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Crear y publicar públicos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/audiences/publish)
- [Administrar audiencias](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/audiences/manage)

### Análisis de contenido

- [Análisis de contenido](https://experienceleague.adobe.com/es/docs/analytics-platform/using/content-analytics/content-analytics)
- [Configuración de Content Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/config/configuration)

### Paneles y cuadros de resultados

- [Creación de un cuadro de resultados móvil](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Configurar y depurar informes de valoración](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Paneles de Adobe Analytics: guía ejecutiva](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [Visualización de número de resumen](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/visualizations/summary-number-change)

### Fundamentos de AEP

- [Información general sobre conjuntos de datos](https://experienceleague.adobe.com/es/docs/experience-platform/catalog/datasets/overview)
- [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home)
- [Información general de orígenes](https://experienceleague.adobe.com/es/docs/experience-platform/sources/home)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Información general de Audience Portal](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/audience-portal)

### Integración de informes de AJO

- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Informe de correo electrónico de Campaign](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/campaign-global-report-cja-email)
- [informe de correo electrónico de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/journey-global-report-cja-email)

### Tutoriales y guías

- [Conceptos básicos de composición](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/composition)
- [Información general de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure)
