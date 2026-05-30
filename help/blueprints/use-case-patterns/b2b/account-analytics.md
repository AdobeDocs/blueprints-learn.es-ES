---
title: Análisis B2B
description: Aprenda a incluir información de nivel de cuenta B2B en el análisis de recorrido de clientes en canales múltiples.
solution: Customer Journey Analytics, Real-Time Customer Data Platform
exl-id: 9d576e5c-cbd2-4c60-a6b0-88f8b8b963b4
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 2%

---

# Análisis B2B

En esta guía se describe el patrón de casos de uso de análisis B2B, que usa [!DNL Customer Journey Analytics] ([!DNL CJA]) B2B edition y [!DNL Real-Time Customer Data Platform] ([!DNL RT-CDP]) B2B edition para incorporar información de nivel de cuenta B2B en el análisis de recorrido de clientes en canales múltiples. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

B2B Analytics amplía las capacidades estándar de [!DNL CJA] con conexiones basadas en cuentas, contenedores específicos de B2B (cuenta, cuenta global, oportunidad, grupo de compra) e informes de nivel de cuenta. Esta capacidad permite a las organizaciones analizar la participación de ventas y marketing a nivel de cuenta, rastrear la progresión de las oportunidades, medir la integridad del grupo de compra y atribuir ingresos a puntos de contacto de marketing en ciclos de ventas B2B ampliados.

## Patrón de caso de uso

**Análisis B2B**

Incluya información de nivel de cuenta B2B en el análisis de recorrido de clientes en canales múltiples.

**Plan de ejecución:** Conexión de datos B2B > Configuración de vista de datos de cuenta > Workspace Analysis > Publicación de paneles

## Resumen del caso de uso

Las organizaciones B2B se enfrentan a un desafío de análisis fundamental: sus clientes no son personas individuales, sino cuentas compuestas por múltiples partes interesadas, grupos de compra y oportunidades. Los análisis estándar basados en personas no pueden responder preguntas como &quot;¿Qué cuentas son las más comprometidas?&quot;, &quot;¿Cuán completos son nuestros grupos de compra?&quot; o &quot;¿Qué puntos de contacto de marketing impulsan la progresión de la oportunidad?&quot;.

B2B Analytics resuelve esto aprovechando [!DNL CJA] B2B edition para crear vistas analíticas centradas en las cuentas que combinan datos de comportamiento a nivel de persona con dimensiones de cuenta, oportunidad y grupo de compra. [!DNL RT-CDP] B2B edition proporciona la unificación del perfil de cuenta subyacente y la resolución de identidad B2B que alimenta la capa de análisis. En conjunto, estas soluciones permiten a las organizaciones crear análisis de recorrido en canales múltiples a nivel de cuenta, correlacionar la participación de marketing con la progresión de la canalización y ofrecer perspectivas procesables a los equipos de marketing y ventas.

La audiencia de destino incluye equipos de operaciones de marketing B2B, líderes de generación de demanda, analistas de operaciones de ingresos y líderes de ventas que necesitan visibilidad sobre la participación a nivel de cuenta y el estado de la canalización.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Mejore los análisis y los informes

Mejore las capacidades de creación de informes para obtener perspectivas de marketing más rápidas y procesables mediante paneles unificados y herramientas de autoservicio. B2B Analytics permite a las organizaciones consolidar datos de participación a nivel de cuenta de múltiples fuentes en un único entorno analítico, lo que proporciona visibilidad en canales múltiples sobre cómo los programas de marketing influyen en la canalización y los ingresos.

**KPI:** eficiencia, productividad

[Más información sobre la mejora de los análisis y los informes](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)

### Habilitar la toma de decisiones basada en datos

Habilite a los equipos con análisis de autoservicio, perspectivas de clientes en tiempo real y predicciones impulsadas por IA para guiar la estrategia. Los análisis a nivel de cuenta equipan a los equipos de marketing y ventas con los datos necesarios para priorizar las cuentas, optimizar las estrategias de participación y alinearse en las oportunidades de canalización.

**KPI:** eficiencia, productividad

[Obtenga más información sobre cómo habilitar la toma de decisiones basada en datos](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)

### Mejore la calificación y conversión de posibles clientes

Aumente la calidad del posible cliente y acelere la progresión de la canalización mediante la puntuación, la nutrición y el seguimiento personalizado. CJA B2B edition proporciona ventanas retrospectivas de cuenta de 13 meses ampliadas diseñadas específicamente para ciclos de ventas B2B, lo que permite una atribución exacta de múltiples contactos en todo el recorrido de la cuenta.

**KPI:** eficiencia, ingresos incrementales

[Obtenga más información sobre cómo mejorar la calificación y conversión de posibles clientes](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran cómo se puede aplicar este patrón en la práctica.

- **Análisis de puntuación de participación de cuenta**: mida y clasifique cuentas según su participación agregada en la web, el correo electrónico, los eventos y las interacciones de contenido para identificar cuentas de alta intención para el seguimiento de ventas
- **Seguimiento de la integridad del grupo de compra** — Analice la composición del grupo de compra en todas las cuentas para identificar lagunas en la cobertura de roles y priorizar la adquisición de posibles clientes para los grupos de compra incompletos
- **Correlación de canalización de oportunidad**: correlacione los datos de participación de marketing con la progresión de la fase de oportunidad para comprender qué campañas y puntos de contacto impulsan el avance de la canalización
- **Atribución B2B multitáctil**: aplique modelos de atribución con ventanas retrospectivas de 13 meses a puntos de contacto de marketing de crédito en todo el recorrido de compra B2B desde el primer contacto hasta el cerrado ganado
- **Asignación de recorridos de cuenta**: visualice el recorrido de cuentas en canales múltiples desde la percepción inicial hasta la creación y el cierre de oportunidades, identificando rutas comunes y puntos de fricción
- **Influencia de la campaña en la canalización**: mida cómo influyen las campañas específicas en la creación de la canalización de la cuenta, el avance de la oportunidad y la generación de ingresos
- **Progresión de la participación del grupo de compra**: efectúe el seguimiento de la evolución de las puntuaciones de participación del grupo de compra a lo largo del tiempo y correlacione los umbrales de participación con los resultados de la oportunidad
- **Rendimiento del contenido basado en cuentas**: Analice qué recursos y temas de contenido resuenan en segmentos de cuenta específicos, industrias o roles de grupo de compra
- **Paneles de alineación de ventas y marketing**: cree paneles compartidos que proporcionen a los equipos de ventas y marketing una vista unificada de la participación de la cuenta, el estado de la canalización y la atribución de ingresos
- **Segmentación de cuentas para activación**: cree segmentos B2B basados en análisis de nivel de cuenta (por ejemplo, &quot;cuentas con un alto nivel de participación sin oportunidades abiertas&quot;) y publíquelos para su activación descendente

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir el éxito de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Puntuación de participación de cuenta | Métrica de participación agregada en todos los contactos de una cuenta | Métrica calculada que combina visitas web, interacciones por correo electrónico, asistencia a eventos y descargas de contenido a nivel de cuenta |
| Integridad del grupo de compra | Porcentaje de funciones requeridas dentro de un grupo de compra | Proporción de puestos ocupados respecto al total de puestos necesarios por grupo de compra, con seguimiento en el tiempo |
| Canalización influenciada por el marketing | Ingresos en canalización que se han visto afectados por las actividades de marketing | Valor de oportunidad donde los contactos de cuenta asociados tienen puntos de contacto de marketing dentro de la ventana de atribución |
| Tasa de conversión de cuenta a oportunidad | Porcentaje de cuentas comprometidas que generan oportunidades cualificadas | Cuentas con oportunidades divididas por el total de cuentas comprometidas durante un periodo definido |
| Duración media del ciclo de oferta | Tiempo desde el primer contacto de marketing hasta el cerrado ganado | Duración media desde el primer punto de contacto atribuido hasta la fecha de cierre de la oportunidad |
| Ingresos de atribución de marketing | Ingresos atribuidos a puntos de contacto de marketing | Ingresos de oportunidades ganadas a puerta cerrada con toques de marketing, distribuidos por modelo de atribución |
| Alcance y penetración de la cuenta | Número de contactos contratados por cuenta de destinatario | Contactos únicos con interacciones de marketing por cuenta, en comparación con el total de contactos conocidos |
| Participación en el contenido por rol de compra | Métricas de participación segmentadas mediante la compra de un rol de grupo | Vistas de página, descargas y tiempo empleado desglosados por persona o función dentro de los grupos compradores |

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón de caso de uso.

- **[!DNL Customer Journey Analytics]B2B edition**: proporciona conexiones basadas en cuentas, contenedores de vista de datos específicos de B2B, análisis del espacio de trabajo a nivel de cuenta, análisis de grupos de compras, análisis de oportunidades, segmentación B2B y atribución B2B con ventanas retrospectivas extendidas
- **[!DNL Real-Time CDP]B2B edition**: proporciona la base de datos B2B, incluida la unificación del perfil de cuenta, la resolución de identidades B2B, las clases de esquema B2B (cuenta, oportunidad, grupo de compra) y la integración de [!DNL Marketo Engage] para la ingesta de datos de participación B2B

## Documentación relacionada

Los siguientes recursos proporcionan información adicional para implementar este patrón de caso de uso.

**[!DNL CJA]B2B edition**

- [Información general sobre CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [Información general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview)
- [protecciones de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-admin/guardrails)

**Conexiones**

- [Información general sobre Conexiones](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-connections/overview)
- [Crear o editar una conexión](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-connections/create-connection)
- [Administrar conexiones](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-connections/manage-connections)

**Vistas de datos**

- [Resumen de vistas de datos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/data-views)
- [Creación o edición de una vista de datos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Resumen de configuración de componentes](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configuración de persistencia](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configuración de atribución](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Configuración de formato](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Campos derivados](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [Configuración de sesión](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/session-settings)

**Workspace y análisis**

- [Información general de Workspace](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/home)
- [Crear un proyecto](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabla de forma libre](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Visualización de flujo](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualización de abandonos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabla de cohortes](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Panel de atribución](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Uso compartido de proyectos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Programar proyectos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Dimensiones de desglose](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

**Componentes**

- [Resumen de filtros](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Creación de filtros](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Resumen de métricas calculadas](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Creación de métricas calculadas](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Resumen de anotaciones](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/annotations/overview)
- [Intervalos de fechas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

**Audiencias**

- [Resumen de audiencias](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Crear y publicar públicos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/audiences/publish)
- [Administrar audiencias](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/audiences/manage)

**Paneles y cuadros de resultados**

- [Creación de un cuadro de resultados móvil](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Configurar y depurar informes de valoración](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Paneles de Adobe Analytics: guía ejecutiva](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dashboards/set-up-execs)

**Análisis guiado**

- [Resumen del análisis guiado](https://experienceleague.adobe.com/es/docs/analytics-platform/using/guided-analysis/overview)
- [Vista de funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Vista de tendencias](https://experienceleague.adobe.com/es/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Vista Retención](https://experienceleague.adobe.com/es/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

**[!DNL RT-CDP]B2B edition**

- [Información general sobre RT-CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#702702)
- [Esquemas de B2B edition](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/schemas/b2b)
- [Resumen de fuentes B2B](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/sources/b2b)

**AEP data foundation**

- [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home)
- [Información general de orígenes](https://experienceleague.adobe.com/es/docs/experience-platform/sources/home)
- [Conector de Marketo Engage](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Información general de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home)

**Gobernanza de datos y ciclo vital**

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/home)

**Tutoriales y guías**

- [Conceptos básicos de composición](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/composition)
- [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview)
- [Resumen de Observability Insights](https://experienceleague.adobe.com/es/docs/experience-platform/observability/home)
