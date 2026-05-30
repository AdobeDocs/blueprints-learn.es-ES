---
title: Reenvío de eventos
description: Aprenda a reenviar datos de evento en tiempo real recopilados mediante Edge Network a destinos que no sean de Adobe para análisis, almacenamiento o publicidad.
solution: Experience Platform
exl-id: 24964d27-db56-4fa4-a79f-1b6750564b34
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# Reenvío de eventos

En esta guía se describe el patrón de casos de uso del reenvío de eventos, que utiliza el procesamiento del lado del servidor en [!DNL Adobe Experience Platform] Edge Network para distribuir datos de eventos en tiempo real a destinos que no son de Adobe, como plataformas de análisis de terceros, extremos de almacenamiento en la nube, redes de publicidad o ganchos web personalizados. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

## Patrón de caso de uso

En esta sección se describe el patrón y el plan de ejecución utilizados para implementar el reenvío de eventos.

**Reenvío de eventos**: reenvía datos de eventos en tiempo real recopilados mediante Edge Network a destinos que no sean de Adobe para análisis, almacenamiento o publicidad.

**Plan de ejecución:** Configuración de secuencia de datos > Definición de regla de evento > Asignación de destino > Ejecución de reenvío > Supervisión

## Resumen del caso de uso

Las organizaciones que recopilan datos de comportamiento a través de la API de servidor, SDK móvil o Web SDK [!DNL Adobe Experience Platform] suelen tener que compartir el mismo flujo de eventos con sistemas que no sean de Adobe (plataformas de análisis como [!DNL Google Analytics] o [!DNL Snowflake], redes de publicidad para el seguimiento de conversiones, almacenes de datos para almacenamiento a largo plazo o servicios internos personalizados). Tradicionalmente, esto requería la proliferación de etiquetas del lado del cliente, que aumenta el peso de la página, introduce latencia y crea riesgos de privacidad y gobernanza.

El reenvío de eventos resuelve esto al operar en el lado del servidor en Edge Network. Cuando la interacción de un visitante déclencheur un evento a través de la API del servidor o Web SDK, ese evento se enruta a través de un conjunto de datos a Edge Network. Reglas de reenvío de eventos (configuradas en una propiedad de reenvío de eventos específica) evalúan los datos de evento entrantes y los reenvían de forma selectiva a uno o varios destinos configurados. Este método del lado del servidor reduce la sobrecarga de etiquetas del lado del cliente, mejora el rendimiento de la página, centraliza la gobernanza de datos y proporciona a la organización control sobre los datos que salen del ecosistema de Adobe.

La audiencia de destino de este patrón incluye organizaciones que ya han implementado (o planean implementar) la API de servidor o Web SDK [!DNL Adobe Experience Platform] para la recopilación de datos y desean ampliar esa inversión distribuyendo datos de evento a extremos que no sean de Adobe sin agregar etiquetas de JavaScript del lado del cliente.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Mejore la calidad y la gobernanza de los datos

Garantice datos limpios, completos y compatibles para un direccionamiento preciso, una reducción de residuos y análisis fiables. El reenvío de eventos centraliza la distribución de datos en el servidor, lo que proporciona a la organización un único punto de control sobre los datos que se comparten con sistemas externos, reduce el riesgo de fuga de datos y garantiza que las políticas de gobernanza se apliquen antes de que los datos salgan de la Edge Network [!DNL Adobe].

**KPI:** eficiencia, ahorros en costos

Para obtener más información, consulte [Mejorar la calidad y el control de los datos](../../business-objectives/cost-efficiency/improve-data-quality-governance.md).

### Consolidar y modernizar la tecnología de marketing

Reduzca la fragmentación de herramientas y la deuda técnica migrando a plataformas unificadas y escalables. El reenvío de eventos permite a las organizaciones reemplazar varias etiquetas de proveedor del lado del cliente con un único mecanismo de distribución de datos del lado del servidor, lo que reduce la sobrecarga de carga de página y simplifica la pila de tecnología.

**KPI:** Ahorro en costos, eficiencia y velocidad de comercialización

Para obtener más información, vea [Consolidar y modernizar la tecnología de marketing](../../business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md).

## Casos de uso tácticos de ejemplo

Los siguientes son escenarios tácticos comunes en los que se aplica este patrón de caso de uso.

- **Enriquecimiento de análisis de terceros**: reenvía eventos de visualización de página, clics y conversión a [!DNL Google Analytics], [!DNL Snowflake] u otras plataformas de análisis en tiempo real sin agregar etiquetas del lado del cliente
- **Seguimiento de conversión de Advertising**: envíe eventos de compra y de generación de posibles clientes a la API de conversiones [!DNL Meta], [!DNL Google Ads], [!DNL TikTok] o [!DNL Snap] para la medición y optimización de conversiones en el servidor
- **Flujo de Data Warehouse**: enrute los datos de evento sin procesar a un almacén de datos en la nube ([!DNL Google BigQuery], [!DNL Amazon S3], [!DNL Azure Event Hubs]) para el almacenamiento a largo plazo y el análisis sin conexión
- **Integración de ganchos web personalizados**: reenvíe datos de evento filtrados o transformados a microservicios internos, sistemas CRM o plataformas asociadas a través de extremos HTTP
- **Reducción de etiquetas y mejora del rendimiento de la página**: reemplace varias etiquetas JavaScript de proveedor del lado del cliente con una sola implementación de Web SDK más reglas de reenvío de eventos del lado del servidor, reduciendo el peso de la página y mejorando Core Web Vitals
- **Uso compartido de datos compatible con la privacidad**: aplique reglas de filtrado de datos y de redacción en el nivel de campo en el servidor antes de compartir datos de evento con terceros, asegurándose de que la PII se elimine o se utilice como hash antes de que llegue a los sistemas externos
- **Distribución de eventos en varias nubes**: reenvía simultáneamente el mismo flujo de eventos a varios destinos (por ejemplo, análisis, publicidad y Data Warehouse) desde un único conjunto de reglas del lado del servidor
- **Reenvío de señales de fraude en tiempo real**: reenvíe eventos de transacciones de alto valor a sistemas de detección de fraude para la puntuación y las alertas de riesgos en tiempo real

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir el éxito de este patrón de caso de uso.

- **Reducción del tiempo de carga de la página**: se ha medido la mejora en la velocidad de carga de la página y en Core Web Vitals después de migrar las etiquetas del lado del cliente al reenvío de eventos del lado del servidor
- **Tasa de éxito de entrega de datos**: porcentaje de eventos reenviados correctamente a extremos de destino sin errores ni tiempos de espera
- **Reducción de recuento de etiquetas**: número de etiquetas de proveedor del lado del cliente eliminadas después de implementar equivalentes del lado del servidor
- **Actualización/latencia de datos**: tiempo entre la ocurrencia del evento en el cliente y la llegada del evento en el extremo de destino (destino: de subsegundo a segundos)
- **Tasa de cumplimiento de control**: porcentaje de recursos compartidos de datos salientes que pasan por las reglas de filtrado del lado del servidor, lo que garantiza que ningún PII o datos restringidos llegue a destinos no autorizados
- **Eficiencia operativa**: reducción en las horas de desarrollador que invierten en administrar implementaciones de etiquetas del lado del cliente y en solucionar conflictos de etiquetas

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Adobe Experience Platform](Edge Network)**: recibe y enruta datos de evento en tiempo real desde Web SDK, Mobile SDK o la API de servidor a través de flujos de datos configurados
- **[!DNL Adobe Experience Platform](Reenvío de eventos)**: proporciona el motor de reglas del lado del servidor para evaluar, filtrar, transformar y reenviar datos de eventos a destinos externos
- **[!DNL Adobe Experience Platform](Etiquetas / Recopilación de datos)**: administra el ciclo de vida de la propiedad de reenvío de eventos, las extensiones, las reglas y el flujo de trabajo de publicación

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre los temas tratados en esta guía.

**Reenvío de eventos**

- [Resumen del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [Introducción al reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)
- [Supervisión del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring)
- [Secretos del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)

**Extensiones de reenvío de eventos**

- [Catálogo de extensiones del lado del servidor](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Extensión de conector de Adobe Cloud](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [Extensión de API de conversiones de Meta](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/meta/overview)
- [Extensión de Google Cloud Platform](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [Extensión de AWS](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/aws/overview)
- [Extensión de Snowflake](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/snowflake/overview)
- [Extensión de conversiones mejoradas de Google Ads](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-ads-enhanced-conversions/overview)
- [Extensión de Mailchimp](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/mailchimp/overview)

**Recopilación de datos y Edge Network**

- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Resumen de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)
- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Información general sobre API de Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Información general sobre etiquetas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
