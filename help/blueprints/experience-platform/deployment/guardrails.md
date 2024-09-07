---
title: Experience Platform y guardas de aplicaciones
description: Las guardas definen las expectativas de rendimiento y el impacto para los componentes y servicios dentro de Adobe Experience Platform y las aplicaciones
solution: Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 64d5e2514d54b3879b09a1dc49d37a2867e21deb
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 10%

---


# Guardas
Las protecciones reflejan las restricciones del sistema, las latencias esperadas y las expectativas de rendimiento para optimizar la arquitectura del cliente y el rendimiento de los casos de uso y ayudan a garantizar la estabilidad, evitar errores o resultados inesperados.

## Tipos de protecciones

| Tipo de protección | Descripción |
|---|---|
| Protección de rendimiento (límite suave) | Las protecciones de rendimiento son límites de uso relacionados con el ámbito de los casos de uso y el esquema del rendimiento esperado en condiciones normales. Cuando se supera, puede experimentar una degradación y latencia del rendimiento. Las protecciones de rendimiento se documentan en los documentos del Experience League en las secciones de protección para cada solución, como se describe a continuación. |
| Límite estático (límite estricto) | Estos son límites impuestos por el sistema que no se pueden superar. Los límites estáticos suelen estar vinculados y descritos contractualmente en el contrato de cliente y en las [descripciones de productos](https://helpx.adobe.com/legal/product-descriptions.html). |

>[!NOTE]
>
> Las protecciones no están pensadas para ser acuerdos de nivel de servicio, sino más bien como orientación para configuraciones óptimas y comportamiento esperado del sistema. Cualquier protección que sea límites del sistema o contractuales o acuerdos de nivel de servicio se documentará específicamente en los contratos de cliente y las descripciones de productos. Si le interesa conocer los límites personalizados, póngase en contacto con su representante del servicio de atención al cliente.

>[!NOTE]
>
> En el caso de casos de uso con estrictas necesidades de latencia o rendimiento, el Adobe sugiere discutir los detalles con el equipo de cuenta de Adobe y el socio de implementación. La configuración de cada cliente puede variar según los patrones de ingesta de datos, las reglas de segmentos y los canales de activación. Es importante probar y revisar su caso de uso antes de lanzarlo, para comprender cómo se comportará.

## Documentación de referencia de guardas para Adobe Experience Platform y aplicaciones

Las siguientes páginas proporcionan información sobre las protecciones para las funciones, los servicios y las aplicaciones de Adobe Experience Platform:

**aplicaciones de Experience Platform**

* [descripción general de las protecciones de Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [protecciones para compartir audiencias de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [protecciones de ingesta de datos de Customer Journey Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [protecciones de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**servicios de Experience Platform**

* [Guardas de ingesta de datos](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [[!DNL Edge Network] Protecciones de API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [Perfil del cliente en tiempo real y protecciones de segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Guardas de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=es)
* [Guardas del servicio de consultas](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=es)
* [Guardas de activación de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=es)

## Diagramas de latencia de extremo a extremo {#end-to-end-latency}

### Latencias observadas principales del Edge Network Experience Platform y del concentrador {#edge-hub-latencies}

En el diagrama siguiente se muestran las latencias observadas en el eje y la arista principales que deben tenerse en cuenta al crear casos de uso en el Experience Platform y las aplicaciones.

![Latencias observadas principales del Experience Platform [!DNL Edge Network] y del concentrador.](/help/blueprints/experience-platform/deployment/assets/aep_edge_hub_latency_v1.svg "Latencias observadas principales del Edge Network Experience Platform y el concentrador"){width="1000" zoomable="yes"}

### Ingesta de datos {#data-ingestion}

El diagrama siguiente muestra los valores de latencia de ingesta de datos esperados mediante [ingesta de transmisión](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html) e [ingesta por lotes](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=es) al introducir datos en Real-Time CDP. Haga clic en la imagen para ver una versión de alta resolución.

![Resumen visual de alto nivel de ingesta de datos.](/help/blueprints/experience-platform/deployment/assets/aep_data_flow_guardrails.svg "Valores de latencia e información general visual de alto nivel de ingesta de datos"){width="1000" zoomable="yes"}

### Segmentación {#segmentation}

El diagrama siguiente muestra los valores de latencia esperados al trabajar con audiencias en el [servicio de segmentación de Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=es). Haga clic en la imagen para ver una versión de alta resolución.

![Resumen visual de alto nivel de segmentación.](/help/blueprints/experience-platform/deployment/assets/segmentation_guardrails.svg "Valores de latencia e información general visual de alto nivel de segmentación"){width="1000" zoomable="yes"}

### Real-time Customer Data Platform y [!DNL Edge Network] {#adobe-edge-latency}

El diagrama siguiente muestra los valores de latencia esperados al aprovechar [!DNL Edge Network]; por ejemplo, para aprovechar las audiencias de RTCDP en [Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=es). Haga clic en la imagen para ver una versión de alta resolución.

![Información general visual de alto nivel sobre Adobe Edge Network y Experience Platform.](/help/blueprints/experience-platform/deployment/assets/RTCDP_Edge_guardrails.svg "Información general y latencia visual de alto nivel sobre la exportación de audiencias a Adobe Target"){width="1000" zoomable="yes"}

### Customer Journey Analytics     {#customer-journey-analytics}

El diagrama siguiente muestra los valores de latencia esperados al trabajar con [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=en). Haga clic en la imagen para ver una versión de alta resolución.

![Información general sobre el trabajo con Customer Journey Analytics de alto nivel visual.](/help/blueprints/experience-platform/deployment/assets/CJA_guardrails.svg "Trabajar con valores de latencia y descripción general visual de alto nivel de Customer Journey Analytics"){width="1000" zoomable="yes"}

### Journey Optimizer   {#journey-optimizer}

El diagrama siguiente muestra los valores de latencia esperados al trabajar con [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en). Haga clic en la imagen para ver una versión de alta resolución.

![Información general visual de alto nivel sobre el trabajo con Adobe Journey Optimizer.](/help/blueprints/experience-platform/deployment/assets/AJO_guardrails.svg "Trabajar con valores de latencia y descripción general visual de alto nivel de Adobe Journey Optimizer"){width="1000" zoomable="yes"}