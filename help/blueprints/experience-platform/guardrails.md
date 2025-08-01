---
title: Experience Platform y guardas de aplicaciones
description: Las guardas definen las expectativas de rendimiento y el impacto para los componentes y servicios dentro de Adobe Experience Platform y las aplicaciones
solution: Experience Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 75a0f2a77f39a4320dc4c4b0db918879be099dd3
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 13%

---


# Guardas

Las protecciones reflejan las restricciones del sistema, las latencias esperadas y las expectativas de rendimiento para optimizar la arquitectura del cliente y el rendimiento de los casos de uso y ayudan a garantizar la estabilidad, evitar errores o resultados inesperados.

## Tipos de protecciones

| Tipo de protección | Descripción |
|---|---|
| Protección de rendimiento (límite suave) | Las protecciones de rendimiento son límites de uso relacionados con el ámbito de los casos de uso y el esquema del rendimiento esperado en condiciones normales. Cuando se supera, puede experimentar una degradación y latencia del rendimiento. Las protecciones de rendimiento se documentan en los documentos de Experience League en las secciones de protección para cada solución, como se describe a continuación. |
| Límite estático (límite estricto) | Estos son límites impuestos por el sistema que no se pueden superar. Los límites estáticos suelen estar vinculados y descritos contractualmente en el contrato de cliente y en las [descripciones de productos](https://helpx.adobe.com/es/legal/product-descriptions.html). |

>[!NOTE]
>
> Las protecciones no están pensadas para ser acuerdos de nivel de servicio, sino más bien como orientación para configuraciones óptimas y comportamiento esperado del sistema. Cualquier protección que sea límites del sistema o contractuales o acuerdos de nivel de servicio se documentará específicamente en los contratos de cliente y las descripciones de productos. Si le interesa conocer los límites personalizados, póngase en contacto con su representante del servicio de atención al cliente.

>[!NOTE]
>
> En el caso de casos de uso con estrictas necesidades de latencia o rendimiento, Adobe sugiere hablar sobre los detalles con su equipo de cuenta de Adobe y su socio de implementación. La configuración de cada cliente puede variar según los patrones de ingesta de datos, los recuentos y la riqueza de perfiles, las reglas de segmentos y los canales de activación. Por lo tanto, es importante crear y probar el caso de uso para optimizar su rendimiento y comprender plenamente las características de rendimiento esperadas.

## Documentación de referencia de guardas para Adobe Experience Platform y aplicaciones

Las siguientes páginas proporcionan información sobre las protecciones para las funciones, los servicios y las aplicaciones de Adobe Experience Platform:

**aplicaciones de Experience Platform**

* [descripción general de las protecciones de Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html?lang=es)
* [Protecciones para compartir audiencias de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=es#latency)
* [protecciones de ingesta de datos de Customer Journey Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=es#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [protecciones de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=es)

**Servicios de Experience Platform**

* [Guardas de ingesta de datos](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html?lang=es)
* [[!DNL Edge Network] Protecciones de API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html?lang=es)
* [Perfil del cliente en tiempo real y protecciones de segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Guardas de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=es)
* [Guardas del servicio de consultas](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=es)
* [Guardas de activación de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=es)

## Diagramas de latencia de extremo a extremo {#end-to-end-latency}

### Latencias observadas principales de Experience Platform Edge Network y Hub {#edge-hub-latencies}

El diagrama siguiente muestra las latencias observadas en el concentrador y la arista principales que deben tenerse en cuenta al crear casos de uso en Experience Platform y aplicaciones.

![Latencias observadas principales de Experience Platform [!DNL Edge Network] y hub.](/help/blueprints/experience-platform/assets/aep_edge_hub_latency_v1.svg "Latencias observadas principales de Edge Network y hub de Experience Platform"){width="1000" zoomable="yes"}