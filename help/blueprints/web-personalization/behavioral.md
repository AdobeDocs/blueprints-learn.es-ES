---
title: Modelo de personalización web basada en el comportamiento
description: Personalice en función del comportamiento en línea y los datos de audiencia.
solution: Experience Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7085thumb-web-personalization-scenario1.jpg
exl-id: b9882c2c-cb45-4efa-a85c-8fe48f641a12
translation-type: tm+mt
source-git-commit: 009a55715b832c3167e9a3413ccf89e0493227df
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Modelo de personalización web basada en el comportamiento

Personalice en función del comportamiento en línea y los datos de audiencia.

## Casos de uso

* Optimización de la página de aterrizaje
* Segmentación basada en el comportamiento
* Personalización basada en vistas de producto/contenido anteriores, afinidad de producto/contenido, atributos ambientales, datos de audiencia de terceros y datos demográficos

## Aplicaciones

* Adobe Target
* Adobe Analytics (opcional)
* Adobe Audience Manager (opcional)

## Arquitectura

<img src="assets/personalization.svg" alt="Arquitectura de referencia para el modelo de personalización web basada en el comportamiento" style="border:1px solid #4a4a4a" />


## Seguridad

De forma predeterminada, el servicio de uso compartido de segmentos permite compartir un máximo de 75 audiencias para cada grupo de informes de Adobe Analytics. Si se utiliza el Audience Manager para compartir audiencias, no hay límite en el número de audiencias que se pueden compartir. 

## Patrones de implementación

El modelo de personalización web/móvil se puede implementar mediante los siguientes enfoques, tal como se describe a continuación.

1. Uso del SDK web de plataforma/SDK móvil y la red perimetral.
1. Uso de SDK tradicionales específicos de la aplicación (por ejemplo, AppMeasurement.js)

### 1. SDK web/móvil de plataforma y enfoque perimetral

<img src="assets/websdkflow.svg" alt="Arquitectura de referencia para el SDK web de plataforma/SDK móvil y el enfoque de red perimetral" style="border:1px solid #4a4a4a" />

### 2. Enfoque de SDK específico de la aplicación

<img src="assets/appsdkflow.png" alt="Arquitectura de referencia para el Enfoque de SDK específico de la aplicación" style="border:1px solid #4a4a4a" />




## Requisitos previos de implementación

| Aplicación/servicio | Biblioteca requerida | Notas |
|---|---|---|
| Adobe Target | SDK web de plataforma*, at.js 0.9.1 o posterior, o mbox.js 61 o posterior | Se prefiere at.js porque mbox.js ya no se está desarrollando. |
| Adobe Audience Manager (opcional) | Platform Web SDK* o dil.js 5.0+ |  |
| Adobe Analytics (opcional) | SDK web de plataforma* o AppMeasurement.js 1.6.4+ |  |
| Servicio de identidad de Experience Cloud | Platform Web SDK* o VisitorAPI.js 2.0+ |  |
| SDK móvil de Experience Platform (opcional) | 4.11 o superior para iOS y Android™ |  |
| SDK web de Experience Platform | 1.0, la versión actual del SDK de Experience Platform tiene [varios casos de uso aún no compatibles con las aplicaciones de Experience Cloud](https://github.com/adobe/alloy/projects/5) |  |

## Pasos de la implementación

1. [Implemente Adobe ](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) Target para sus aplicaciones web o móviles.

   Si utiliza Audience Manager o Analytics:

1. [Implementación de Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html)
1. [Implementación de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
1. [Implementación del servicio de identidad de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html)

   >[!NOTE]
   >
   >Cada aplicación debe utilizar el ID de Experience Cloud y formar parte de la misma organización de Experience Cloud para permitir el uso compartido de audiencias entre aplicaciones.

1. [Solicitar aprovisionamiento para los servicios de uso compartido de personas y audiencias (audiencias compartidas)](https://www.adobe.com/go/audiences)
1. Genere segmentos en [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html) o [Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html) y [configure esas audiencias para compartirlas con el Experience Cloud](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html) (si usa el Audience Manager o Adobe Analytics)
1. Una vez que las audiencias están disponibles en Adobe Target, pueden utilizarse para [experiencias de segmentación con Adobe Target](https://experienceleague.adobe.com/docs/target/using/audiences/target.html)

## Documentación relacionada

* [Audiencias de Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Integrar el Audience Manager con Adobe Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Uso compartido de segmentos de Adobe Analytics mediante Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)


## Publicaciones de blog relacionadas

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
