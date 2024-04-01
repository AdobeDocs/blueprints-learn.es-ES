---
title: Experience Platform y guardas de aplicaciones
description: Las guardas definen las expectativas de rendimiento y el impacto para los componentes y servicios dentro de Adobe Experience Platform y las aplicaciones
solution: Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 15%

---

# Guardas

Las protecciones son umbrales recomendados que proporcionan directrices para los datos, las latencias observadas y el uso del sistema en Adobe Experience Platform y aplicaciones. Las protecciones reflejan las restricciones del sistema y las expectativas de rendimiento para optimizar la arquitectura del cliente y el rendimiento de los casos de uso, y ayudan a evitar errores o resultados inesperados. Las protecciones no están pensadas para ser acuerdos de nivel de servicio, los acuerdos de nivel de servicio se documentan en las descripciones de productos vinculadas a continuación y en los acuerdos de licencia de cliente. Las protecciones están pensadas para proporcionar orientación en la arquitectura de soluciones para casos de uso específicos de clientes a fin de garantizar la estabilidad y la ejecución.

Para obtener información sobre los acuerdos de nivel de servicio específicos para aplicaciones y funciones, consulte la [Descripciones de aplicaciones y funciones](#application-feature-descriptions) en la parte inferior de esta página.

Tenga en cuenta que, para cualquier caso de uso de cliente que tenga requisitos estrictos de latencia o volumen, Adobe recomienda revisar en detalle el caso de uso con el equipo de la cuenta de Adobe y el socio de implementación. En algunos casos, es aconsejable probar y observar la implementación de un caso de uso determinado antes del lanzamiento de producción del caso de uso para observar y comprender el comportamiento esperado, ya que cada implementación de cliente tiene varios factores en juego, incluida la naturaleza y cadencia de la ingesta de datos, los detalles específicos de las reglas de segmentos que se están creando y los distintos canales de activación y cargas útiles. Cada implementación de caso de uso tendrá un rendimiento observado variable. Como tal, es mejor establecer y probar el rendimiento esperado por adelantado para garantizar una arquitectura e implementación adecuadas de acuerdo con los requisitos de latencia y rendimiento del caso de uso.


## Documentación de referencia de guardas para Adobe Experience Platform y aplicaciones

Las siguientes páginas proporcionan información sobre las protecciones para las funciones, los servicios y las aplicaciones de Adobe Experience Platform:

**aplicaciones de Experience Platform**

* [Introducción a las protecciones Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [protecciones de uso compartido de audiencia de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
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

### Latencias observadas principales de Experience Platform Edge Network y Hub {#edge-hub-latencies}

En el diagrama siguiente se muestran las latencias observadas en el eje y la arista principales que deben tenerse en cuenta al crear casos de uso en el Experience Platform y las aplicaciones.

![Experience Platform [!DNL Edge Network] latencias observadas principales de y hub.](/help/blueprints/experience-platform/deployment/assets/aep_edge_hub_latency.svg "Latencias observadas principales de Experience Platform Edge Network y hub"){width="1000" zoomable="yes"}

### Ingesta de datos {#data-ingestion}

El diagrama siguiente muestra los valores de latencia de ingesta de datos esperados a través de [ingesta por streaming](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html) y [ingesta por lotes](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=es) al introducir datos en Real-Time CDP. Haga clic en la imagen para ver una versión de alta resolución.

![Información general visual de alto nivel sobre la ingesta de datos.](/help/blueprints/experience-platform/deployment/assets/aep_data_flow_guardrails.svg "Introducción visual de alto nivel a la ingesta de datos y valores de latencia"){width="1000" zoomable="yes"}

### Segmentación {#segmentation}

El diagrama siguiente muestra los valores de latencia esperados al trabajar con audiencias en [Servicio de segmentación de Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=es). Haga clic en la imagen para ver una versión de alta resolución.

![Resumen visual de alto nivel de segmentación.](/help/blueprints/experience-platform/deployment/assets/segmentation_guardrails.svg "Información general visual de alto nivel de segmentación y valores de latencia"){width="1000" zoomable="yes"}

### REAL-TIME CUSTOMER DATA PLATFORM y [!DNL Edge Network] {#adobe-edge-latency}

El diagrama siguiente muestra los valores de latencia esperados al aprovechar el [!DNL Edge Network] : por ejemplo, para aprovechar las audiencias de RTCDP en [Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=es). Haga clic en la imagen para ver una versión de alta resolución.

![Información general visual de alto nivel sobre Adobe Edge Network y Experience Platform.](/help/blueprints/experience-platform/deployment/assets/RTCDP_Edge_guardrails.svg "Información general y latencia visual de alto nivel sobre la exportación de audiencias a Adobe Target"){width="1000" zoomable="yes"}

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
