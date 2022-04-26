---
title: Modelo de personalización web basada en comportamiento
description: Descubra cómo personalizar el contenido en función del comportamiento en línea y los datos de audiencia.
landing-page-description: Descubra cómo personalizar según el comportamiento en línea y los datos de audiencia.
solution: Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection, Experience Platform
kt: 7085thumb-web-personalization-scenario1.jpg
exl-id: b9882c2c-cb45-4efa-a85c-8fe48f641a12
source-git-commit: 24d5ec498d09f6dac443561bd530d58a33dae7af
workflow-type: ht
source-wordcount: '617'
ht-degree: 100%

---

# Modelo de personalización web/móvil basada en comportamiento

Personalización basada en el comportamiento en línea y datos de audiencia.

## Casos de uso

* Optimización de la página de aterrizaje
* Segmentación basada en el comportamiento
* Personalización basada en visualizaciones de productos/contenidos anteriores, afinidad de producto/contenido, atributos del entorno, datos de audiencia de terceros y sectores demográficos

## Aplicaciones

* Adobe Target
* Adobe Analytics (opcional)
* Adobe Audience Manager (opcional)
* Adobe Real-time Customer Data Platform (opcional)

## Arquitectura

<img src="assets/behavioral_personalization.svg" alt="Arquitectura de referencia del modelo de personalización web basada en comportamiento" style="width:90%; border:1px solid #4a4a4a" />


## Patrones de implementación

El modelo de personalización web/móvil se puede implementar mediante los siguientes enfoques, tal como se describe a continuación.

1. Con el [!UICONTROL SDK web de Platform] o [!UICONTROL SDK móvil de Platform] y [!UICONTROL Edge Network]. [Consulte el modelo del SDK móvil y web de Experience Platform](../data-ingestion/websdk.md)
1. Con SDK tradicionales específicos de cada aplicación (por ejemplo, AppMeasurement.js). [Consulte el modelo de SDK específico para aplicaciones](../data-ingestion/appsdk.md)

## Pasos de implementación

1. [Implementar Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=es) para las aplicaciones móviles o web.

### Pasos de implementación: Audience Manager o Adobe Analytics

1. [Implementar Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=es).
1. [Implementar Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es).
1. [Implementar el Servicio de identidad de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=es).

   >[!NOTE]
   >
   >Cada aplicación deberá emplear el Experience Cloud ID y pertenecer a la misma organización de Experience Cloud para que las aplicaciones compartan las audiencias.

1. [Solicitar suministros para los servicios que comparten personas y audiencia (audiencias compartidas)](https://www.adobe.com/go/audiences).
1. Generar segmentos en [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html?lang=es) o [Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=es) y [configurar las audiencias de modo que se compartan con Experience Cloud](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=es) (si se emplea Audience Manager o Adobe Analytics).
1. Cuando las audiencias estén disponibles en Adobe Target, se podrán utilizar [para la segmentación de experiencias en Adobe Target](https://experienceleague.adobe.com/docs/target/using/audiences/target.html?lang=es).

### Pasos de implementación de Real-time Customer Data Platform

1. [Crear esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) para la ingesta de datos.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) para la ingesta de datos.
1. [Configurar las identidades e identidad de áreas de nombres correctas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es) en el esquema para asegurar que los datos ingestados se puedan combinar en un perfil unificado.
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Ingesta de datos](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) a Experience Platform.
1. [Disponer el intercambio de segmentos de [!UICONTROL Real-time Customer Data Platform]](https://www.adobe.com/go/audiences) entre Experience Platform y Audience Manager para que las audiencias definidas en Experience Platform se compartan con Audience Manager.
1. [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=es) en Experience Platform. El sistema determina automáticamente si el segmento debe ser evaluado por lotes o streaming.
1. [Configurar destinos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html?lang=es) para compartir atributos de perfil y pertenencias a audiencia a los destinos deseados.


## Documentación relacionada

* [Audiencias de Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=es)
* [Integrar Audience Manager con Adobe Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html?lang=es)
* [Intercambio de segmentos de Adobe Analytics mediante Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=es)
* Información general de [[!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=es)
* Descripción del producto [[!UICONTROL Real-time Customer Data Platform]](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform.html)
* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Documentación de la segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Documentación de los destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=es)

## Entradas relacionadas en el blog

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
