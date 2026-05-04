---
title: Experience Platform y guardas de aplicaciones
description: Las guardas definen las expectativas de rendimiento y el impacto para los componentes y servicios dentro de Adobe Experience Platform y las aplicaciones
solution: Experience Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
TQID: https://experienceleague.adobe.com/ZSHbFR3sEy4C-876IU3yN8U5vOUVvDWIP-O3l-wKm78
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2: id: d1823595-9241-4128-8a33-e4ac3bf08773id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74id: ee602049-8a18-43df-9299-a689a025a371
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a99add31cc9f485db119ca00426798545e6a7316
workflow-type: tm+mt
source-wordcount: 486
ht-degree: 14%

---

# Guardas

Las protecciones reflejan las restricciones del sistema, las latencias esperadas y las expectativas de rendimiento para optimizar la arquitectura del cliente y el rendimiento de los casos de uso y ayudan a garantizar la estabilidad, evitar errores o resultados inesperados.

## Tipos de protecciones

| Tipo de protección | Descripción |
|---|---|
| Protección de rendimiento (límite suave) | Las protecciones de rendimiento son límites de uso relacionados con el ámbito de los casos de uso y el esquema del rendimiento esperado en condiciones normales. Cuando se supera, puede experimentar una degradación y latencia del rendimiento. Las protecciones de rendimiento se documentan en los documentos de Experience League en las secciones de protección para cada solución, como se describe a continuación. |
| Límite estático (límite estricto) | Estos son límites impuestos por el sistema que no se pueden superar. Los límites estáticos suelen estar vinculados y descritos contractualmente en el contrato de cliente y en las [descripciones de productos](https://helpx.adobe.com/legal/product-descriptions.html). |

>[!NOTE]
>
> Las protecciones no están pensadas para ser acuerdos de nivel de servicio, sino más bien como orientación para configuraciones óptimas y comportamiento esperado del sistema. Cualquier protección que sea límites del sistema o contractuales o acuerdos de nivel de servicio se documentará específicamente en los contratos de cliente y las descripciones de productos. Si le interesa conocer los límites personalizados, póngase en contacto con su representante del servicio de atención al cliente.

>[!NOTE]
>
> En el caso de casos de uso con estrictas necesidades de latencia o rendimiento, Adobe sugiere hablar sobre los detalles con su equipo de cuenta de Adobe y su socio de implementación. La configuración de cada cliente puede variar según los patrones de ingesta de datos, los recuentos y la riqueza de perfiles, las reglas de segmentos y los canales de activación. Por lo tanto, es importante crear y probar el caso de uso para optimizar su rendimiento y comprender plenamente las características de rendimiento esperadas.

## Documentación de referencia de guardas para Adobe Experience Platform y aplicaciones

Las siguientes páginas proporcionan información sobre las protecciones para las funciones, los servicios y las aplicaciones de Adobe Experience Platform:

**aplicaciones de Experience Platform**

* [Introducción a las protecciones Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [Protecciones de uso compartido de audiencias Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [Protecciones de ingesta de datos Customer Journey Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [protecciones de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**Servicios de Experience Platform**

* [Protecciones de ingesta de datos](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [[!DNL Edge Network] protecciones de API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [Perfil del cliente en tiempo real y protecciones de segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Protecciones de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=es)
* [Protecciones del servicio de consultas](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=es)
* [Protecciones de activación de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=es)

## Diagramas de latencia de extremo a extremo {#end-to-end-latency}

### Latencias observadas principales de Experience Platform Edge Network y Hub {#edge-hub-latencies}

El diagrama siguiente muestra las latencias observadas en el concentrador y la arista principales que deben tenerse en cuenta al crear casos de uso en Experience Platform y aplicaciones.

![Latencias observadas principales de Experience Platform [!DNL Edge Network] y hub.](/help/blueprints/experience-platform/assets/aep_edge_hub_latency_v1.svg "Latencias observadas principales de Edge Network y hub de Experience Platform"){width="1000" zoomable="yes"}