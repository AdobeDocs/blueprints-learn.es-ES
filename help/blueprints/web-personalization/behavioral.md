---
title: Caso de personalización web basada en el comportamiento
description: Personalice en función del comportamiento en línea y los datos de audiencia.
solution: Experience Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7085thumb-web-personalization-scenario1.jpg
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# Caso de personalización web basada en el comportamiento

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

<img src="assets/personalization.svg" alt="Arquitectura de referencia para el escenario de personalización web basada en el comportamiento" style="border:1px solid #4a4a4a" />


## Seguridad

De forma predeterminada, el servicio de uso compartido de segmentos permite compartir un máximo de 75 audiencias para cada grupo de informes de Adobe Analytics. Si se utiliza el Audience Manager para compartir audiencias, no hay límite en el número de audiencias que se pueden compartir. 

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


## Diagramas de flujo de datos de implementación

El modelo de personalización web/móvil se puede implementar utilizando el SDK web de plataforma o el SDK móvil y la red perimetral, o bien utilizando SDK tradicionales específicos de la aplicación (por ejemplo, AppMeasurement.js).

### Platform Web/Mobile SDK y enfoque de red perimetral

<img src="assets/websdkflow.svg" alt="Arquitectura de referencia para el SDK web de plataforma/SDK móvil y el enfoque de red perimetral" style="border:1px solid #4a4a4a" />


### Enfoque de SDK específico de la aplicación

<img src="assets/appsdkflow.png" alt="Arquitectura de referencia para el Enfoque de SDK específico de la aplicación" style="border:1px solid #4a4a4a" />


## Documentación relacionada

* [Audiencias de Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Integrar el Audience Manager con Adobe Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Uso compartido de segmentos de Adobe Analytics mediante AAM](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)


## Publicaciones de blog relacionadas

* [Modelo para personalización web mediante el perfil del cliente en tiempo real de Adobe Experience Platform](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [Integración de Adobe Experience Platform Decisioning Engine con sitios web AEM](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [Cómo mejoran las experiencias personalizadas las Predictive Audiences de Adobe Experience Platform](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [SDK web de Adobe Experience Platform para la gestión de público](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Implementación del perfil del cliente en tiempo real de Adobe Experience Platform mediante nuestro programa &quot;Customer Zero&quot;](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [Cómo Adobe Experience Platform puede ayudar a los clientes a personalizar su mensajería móvil en tiempo real con el servicio de Journey Orchestration y un proveedor de mensajería móvil](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [Segmentación en segundos: Cómo Adobe Experience Platform hizo realidad los perfiles del cliente en tiempo real](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)