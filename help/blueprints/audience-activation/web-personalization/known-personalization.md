---
title: 'Información general sobre Web/Mobile Personalization: Adobe Target y RTCDP'
description: Sincronice la personalización web con el correo electrónico y otras personalizaciones de canales anónimos y conocidos.
landing-page-description: Sincronice la personalización web con el correo electrónico y otras personalizaciones de canales anónimos y conocidos.
short-description: Sincronice la personalización web con el correo electrónico y otras personalizaciones de canales anónimos y conocidos.
solution: Real-Time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 845655a275cdb6d4a9cd397ec7c3515cbf02d321
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 79%

---


# Personalization web/móvil con modelo de datos de clientes conocidos

## Casos de uso

* Personalización en línea con datos de clientes conocidos
* Optimización de la página de aterrizaje
* Personalización basada en visualizaciones de productos/contenidos anteriores, afinidad de producto/contenido, atributos del entorno y datos demográficos, además de datos sin conexión, tales como datos de transacciones, fidelidad y CRM, e información modelada.
* Comparta y dirija audiencias definidas en Real-Time Customer Data Platform en sitios web y aplicaciones móviles mediante Adobe Target.

## Aplicaciones

* [!UICONTROL Real-Time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager (opcional): añade datos de audiencia de terceros
* Adobe Analytics o Customer Journey Analytics (opcional): añade la capacidad de generar segmentos basados en datos históricos de comportamiento y clientes con segmentación detallada

### Documentación de referencia

* [Conexión de Adobe Target para Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Configuración de la secuencia de datos de Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)
* [Compartir segmentos en Experience Platform con Audience Manager y otras soluciones de Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=es)


## Patrones de integración

| Patrón de integración | Capacidad | Requisitos previos |
|---|---|---|
| Evaluación de segmentos en tiempo real en Edge compartida desde Real-Time Customer Data Platform en Target | <ul><li>Evalúe las audiencias en tiempo real para la personalización de la misma página o de la siguiente en Edge.</li><li>Además, cualquier segmento evaluado en flujo continuo o en lote también se proyectará a [!DNL Edge Network] para que se incluya en la evaluación y personalización de segmentos de Edge.</li></ul> | <ul><li>El SDK web/móvil debe estar implementado para la API de servidor [!DNL Edge Network]</li><li>La secuencia de datos debe estar configurada en Experience Edge con Target y la extensión de Experience Platform habilitadas.</li><li>El destino de Target debe configurarse en los destinos de Real-Time Customer Data Platform.</li><li>La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.</li></ul> |
| Uso compartido de audiencias por flujo y por lotes desde Real-Time Customer Data Platform en Target con el enfoque de Edge | <ul><li>Comparta audiencias de flujo continuo y por lotes de Real-time Customer Data Platform a Target a través de [!DNL Edge Network]. Las audiencias evaluadas en tiempo real requieren el SDK web y la implementación de [!DNL Edge Network].</li></ul> | <ul><li>No se requiere el SDK web/móvil o la implementación de la API de Edge de Target para compartir audiencias RTCDP de flujo y por lotes a Target, aunque se requiere para permitir la evaluación de segmentos perimetrales en tiempo real descrita anteriormente.</li><li>Si utiliza AT.js, solo se admite la integración de perfiles con el área de nombres de identidad de ECID.</li><li>Para las búsquedas del área de nombres de identidad personalizadas en Edge, se necesita la implementación del SDK web o la API de Edge y cada identidad debe establecerse como tal en el mapa de identidades.</li><li>El destino de Target debe configurarse en los destinos de Real-Time Customer Data Platform. Solo se admite la zona protegida de producción por defecto en RTCDP.</li><li>La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.</li></ul> |
| Uso compartido de audiencias de streaming y lotes de Real-Time Customer Data Platform en Target y Audience Manager con el enfoque del servicio de uso compartido de audiencias | <ul><li>Este patrón de integración se puede aprovechar cuando se desea un enriquecimiento adicional de datos y audiencias de terceros en Audience Manager.</li></ul> | <ul><li>El SDK web/móvil no es necesario para compartir audiencias de flujo y por lotes en Target, aunque es necesario para habilitar la evaluación de segmentos de Edge en tiempo real.</li><li>Si utiliza AT.js, solo se admite la integración de perfiles con el área de nombres de identidad de ECID.</li><li>Para las búsquedas del área de nombres de identidad personalizadas en Edge, se necesita la implementación del SDK web o la API de Edge y cada identidad debe establecerse como tal en el mapa de identidades.</li><li>Se debe aprovisionar la proyección de audiencias mediante el servicio de uso compartido de audiencias.</li><li>La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.</li><li>Solo las audiencias de la zona protegida del producto por defecto admiten el servicio principal de uso compartido de audiencias.</li></ul> |

## Uso compartido de audiencias en tiempo real, por flujo y por lotes en Adobe Target

Arquitectura

<img src="assets/RTCDP+Target.svg" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Detalle de secuencia

<img src="assets/RTCDP+Target_flow.svg" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Vista general de la arquitectura

<img src="assets/personalization_with_apps.svg" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Patrones de implementación

La personalización de cliente conocida se admite mediante varios enfoques de implementación.

### Patrón de implementación 1 - [!DNL Edge Network] con SDK web/móvil o API [!DNL Edge Network] (enfoque recomendado)

* Usando [!DNL Edge Network] con el SDK web/móvil. La segmentación perimetral en tiempo real requiere el enfoque de implementación del SDK web/móvil o la API de Edge.
* [Consulte el modelo del SDK móvil y web de Experience Platform](../../experience-platform/deployment/websdk.md) para la implementación basada en SDK.
* Para su uso en el SDK móvil, la [extensión Adobe Journey Optimizer - Decisioning](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer-decisioning) debe estar instalada en el SDK móvil.
* [Consulte la [!DNL Edge Network] API de servidor](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es) para obtener una implementación basada en API de Adobe Target con perfil de Edge.

### Patrón de implementación 2: SDK específicos para aplicaciones

Con SDK tradicionales específicos de cada aplicación (por ejemplo, AT.js y AppMeasurement.js). La evaluación de segmentos en tiempo real de Edge no se admite con este enfoque de implementación. Sin embargo, el uso compartido de audiencias por flujo y por lotes desde el centro de Experience Platform se admite con este enfoque de implementación.

[Consulte la documentación del conector de Adobe Target](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection)
[Consulte el modelo de SDK específico de la aplicación](../../experience-platform/deployment/appsdk.md)

## Consideraciones sobre la implementación

Requisitos previos de identidad

* Cualquier identidad principal se puede aprovechar al utilizar el patrón de implementación 1 descrito anteriormente con [!DNL Edge Network] y el SDK web. La personalización del primer inicio de sesión requiere que la identidad principal del conjunto de solicitudes de personalización coincida con la identidad principal del perfil de Real-time Customer Data Platform.

## Documentación relacionada

### Documentación del SDK

* [Documentación del SDK web de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
* [Documentación de Experience Cloud ID Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es)

### Documentación de la segmentación

* [Información general sobre la segmentación en Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=es)
* [Segmentación en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=es)
* [Segmentación por flujo](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Intercambio de segmentos de Adobe Analytics mediante Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=es)
* [Configuración de políticas de combinación](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=es#create-a-merge-policy)

### Tutoriales

* [Personalización de próxima visita con Real-Time CDP y Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=es)

### Entradas relacionadas en el blog

* [Adobe lanza la personalización mejorada de la misma página con Adobe Target y Real-Time Customer Data Platform](https://blog.adobe.com/en/publish/2021/10/05/adobe-announces-same-page-enhanced-personalization-with-adobe-target-real-time-customer-data-platform)
* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Adobe Experience Platform's Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our "Customer Zero" Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
