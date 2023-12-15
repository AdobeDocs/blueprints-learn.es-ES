---
title: Experience Platform y protecciones de aplicaciones y latencias de extremo a extremo
description: Las guardas definen las expectativas de rendimiento y el impacto para los componentes y servicios dentro de Adobe Experience Platform y las aplicaciones
solution: Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: a16d7e925b7f5e9a379214d01280e4fef56344af
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 22%

---

# Protecciones y latencias de extremo a extremo

Las protecciones son umbrales recomendados que proporcionan directrices para los datos, las latencias observadas y el uso del sistema en Adobe Experience Platform y aplicaciones. Las protecciones reflejan las restricciones del sistema y las expectativas de rendimiento para optimizar la arquitectura del cliente y el rendimiento de los casos de uso, y ayudan a evitar errores o resultados inesperados. Las protecciones no están pensadas para ser acuerdos de nivel de servicio.

Para obtener información sobre los acuerdos de nivel de servicio específicos para aplicaciones y funciones, consulte la [Descripciones de aplicaciones y funciones](#application-feature-descriptions) en la parte inferior de esta página.


## Documentación de referencia de guardas para Adobe Experience Platform y aplicaciones

Las siguientes páginas proporcionan información sobre las protecciones para las funciones, los servicios y las aplicaciones de Adobe Experience Platform:

**aplicaciones de Experience Platform**

* [Introducción a las protecciones Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [protecciones de uso compartido de audiencia de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [protecciones de ingesta de datos de Customer Journey Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [protecciones de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**servicios de Experience Platform**

* [Guardas de ingesta de datos](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [Protecciones de la API de red Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [Perfil del cliente en tiempo real y protecciones de segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Guardas de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=es)
* [Guardas del servicio de consultas](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=es)
* [Guardas de activación de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=es)

## Diagramas de latencia de extremo a extremo {#end-to-end-latency}

### Ingesta de datos {#data-ingestion}

El diagrama siguiente muestra los valores de latencia de ingesta de datos esperados a través de [ingesta por streaming](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html) y [ingesta por lotes](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=es) al introducir datos en Real-Time CDP. Haga clic en la imagen para ver una versión de alta resolución.

![Información general visual de alto nivel sobre la ingesta de datos.](/help/blueprints/experience-platform/deployment/assets/aep_data_flow_guardrails.svg "Introducción visual de alto nivel a la ingesta de datos y valores de latencia"){width="1000" zoomable="yes"}

### Segmentación {#segmentation}

El diagrama siguiente muestra los valores de latencia esperados al trabajar con audiencias en [Servicio de segmentación de Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=es). Haga clic en la imagen para ver una versión de alta resolución.

![Resumen visual de alto nivel de segmentación.](/help/blueprints/experience-platform/deployment/assets/segmentation_guardrails.svg "Información general visual de alto nivel de segmentación y valores de latencia"){width="1000" zoomable="yes"}

### Real-Time Customer Data Platform y Adobe Target {#adobe-target-latency}

El diagrama siguiente muestra los valores de latencia esperados al exportar audiencias de Real-Time CDP a [Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=es). Haga clic en la imagen para ver una versión de alta resolución.

![Información general visual de alto nivel sobre la exportación a Adobe Target.](/help/blueprints/experience-platform/deployment/assets/RTCDP_Target_guardrails.svg "Exportar audiencias a valores de latencia e información general visual de alto nivel de Adobe Target"){width="1000" zoomable="yes"}

### Customer Journey Analytics     {#customer-journey-analytics}

El diagrama siguiente muestra los valores de latencia esperados al trabajar con [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=en). Haga clic en la imagen para ver una versión de alta resolución.

![Información general sobre el trabajo con Customer Journey Analytics visual de alto nivel.](/help/blueprints/experience-platform/deployment/assets/CJA_guardrails.svg "Uso de valores de latencia e información general visual de alto nivel de Customer Journey Analytics"){width="1000" zoomable="yes"}

### Journey Optimizer   {#journey-optimizer}

El diagrama siguiente muestra los valores de latencia esperados al trabajar con [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en). Haga clic en la imagen para ver una versión de alta resolución.

![Información general visual de alto nivel sobre el uso de Adobe Journey Optimizer.](/help/blueprints/experience-platform/deployment/assets/AJO_guardrails.svg "Uso de valores de latencia e información general visual de alto nivel de Adobe Journey Optimizer"){width="1000" zoomable="yes"}

## Descripciones de aplicaciones y funciones {#application-feature-descriptions}

Para obtener información sobre los acuerdos de nivel de servicio específicos de las funciones, consulte las siguientes descripciones de productos:

* [Experience Platform Collection Enterprise](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform-collection-enterprise.html)
* [Real-Time Customer Data Platform](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform.html)
* [B2B Customer Data Platform](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform-b2b.html)
* [Experience Platform Activation](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform0.html)
* [Experience Platform Intelligence](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Servicios inteligentes](https://helpx.adobe.com/es/legal/product-descriptions/intelligent-services.html)
* [Data Distiller](https://helpx.adobe.com/es/legal/product-descriptions/data-distiller.html)
* [Customer Journey Analytics](https://helpx.adobe.com/es/legal/product-descriptions/customer-journey-analytics.html)
* [Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
* [Journey Orchestration](https://helpx.adobe.com/es/legal/product-descriptions/journey-orchestration.html)
* [Offer Decisioning](https://helpx.adobe.com/es/legal/product-descriptions/offer-decisioning-app-service.html)
