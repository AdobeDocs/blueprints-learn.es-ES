---
title: Modelo de personalización de sitios web en línea/sin conexión
description: Sincronice la personalización del sitio web con la del email y otras personalizaciones de canales anónimos y conocidos.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: d30af99dc08d0bc723edc4c1c4705ebc07c3c7b7
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 100%

---

# Modelo de personalización de sitios web/móvil en línea/sin conexión

Sincronice la personalización del sitio web con la del email y otras personalizaciones de canales anónimos y conocidos.

## Casos de uso

* Optimización de la página de aterrizaje
* Segmentación de perfiles según comportamiento y sin conexión
* Personalización basada en visualizaciones de productos/contenidos anteriores, afinidad de producto/contenido, atributos del entorno, datos de audiencia de terceros y sectores demográficos, además de datos sin conexión, tales como transacciones, datos de fidelidad y CRM, y datos modelados.

## Aplicaciones

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager (opcional): añade datos de audiencia de terceros, gráficos de cooperación basados en dispositivos y la habilidad de rescatar segmentos de Platform en Adobe Analytics y viceversa.
* Adobe Analytics (opcional): añade la habilidad de generar segmentos basados en los datos de comportamiento histórico y realizar una segmentación detallada de los datos de Adobe Analytics.

## Arquitectura

<img src="assets/online_offline_personalization_with_apps.svg" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="border:1px solid #4a4a4a" />

## Guardas

[Consulte los guardas de la página de información general sobre los modelos de personalización web/móvil.](overview.md)

## Patrones de implementación

El modelo de personalización web/móvil se puede implementar mediante los siguientes enfoques, tal como se describe a continuación.

1. Con el [!UICONTROL SDK Platform Web] o [!UICONTROL SDK Platform Mobile] y [!UICONTROL Edge Network].
1. Con SDK tradicionales específicos de cada aplicación (por ejemplo, AppMeasurement.js)

### 1. Enfoque con el SDK Platform Web/Mobile y Edge

<img src="assets/web_sdk_flow.svg" alt="Arquitectura de referencia para el enfoque [!UICONTROL Platform Web SDK] o [!UICONTROL Platform Mobile SDK] y [!UICONTROL Edge Network]" style="border:1px solid #4a4a4a" />

### 2. Enfoque con el SDK específico de cada aplicación

<img src="assets/app_sdk_flow.png" alt="Arquitectura de referencia del enfoque con el SDK específico de cada aplicación" style="border:1px solid #4a4a4a" />

## Prerrequisitos de implementación

| Aplicación/servicio | Biblioteca requerida | Notas |
|---|---|---|
| Adobe Target | [!UICONTROL SDK Platform Web]*, at.js 0.9.1+ o mbox.js 61+ | Se recomienda at.js debido a que mbox.js ya no se desarrolla. |
| Adobe Audience Manager (opcional) | [!UICONTROL SDK Platform Web]* o dil.js 5.0+ |  |
| Adobe Analytics (opcional) | [!UICONTROL SDK Platform Web]* o AppMeasurement.js 1.6.4+ | El seguimiento de Adobe Analytics debe emplear la recopilación de datos regional (RDC). |
| Servicio Experience Cloud ID | [!UICONTROL SDK Platform Web]* o VisitorAPI.js 2.0+ | (Recomendación) Emplear Experience Platform Launch para implementar el servicio de ID y así garantizar que este ID se configure antes de la llamada de cualquier aplicación. |
| SDK Experience Platform Mobile (opcional) | 4.11 o superior para iOS y Android™ |  |
| SDK Experience Platform Web | 1.0, la versión actual del SDK Experience Platform, cuenta con [varios casos de uso sin compatibilidad con las aplicaciones de Experience Cloud](https://github.com/adobe/alloy/projects/5) |  |


## Pasos de implementación

1. [Implementar Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=es) para sus aplicaciones móviles o web
1. [Implementar Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=es) (opcional)
1. [Implementar Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) (opcional)
1. [Implementar Experience Platform y [!UICONTROL Real-time Customer Profile]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=es)
1. Implementar el [Servicio de identidad de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=es) o el [SDK Experience Platform Web](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es)
   >[!NOTE]
   >
   >Cada aplicación deberá emplear el Experience Cloud ID y pertenecer a la misma organización de Experience Cloud para que las aplicaciones compartan las audiencias.
1. [Solicitar suministros para compartir audiencias entre Experience Platform y Adobe Target (audiencias compartidas)](https://www.adobe.com/go/audiences)

## Documentación relacionada

* [Compartir segmentos en Experience Platform con Audience Manager y otras soluciones de Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=es)
* [Información general sobre la segmentación en Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=es)
* [Segmentación por flujo](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Información general sobre el generador de segmentos de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=es)
* [Conector de origen de Audience Manager](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=es)
* [Intercambio de segmentos de Adobe Analytics mediante Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=es)
* [Documentación del SDK Experience Platform Web](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Documentación de Experience Cloud ID Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es)
* [Documentación de Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=es)

## Entradas relacionadas en el blog

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
