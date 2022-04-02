---
title: Información general de Web/Mobile Personalization
description: Sincronice la personalización del sitio web con la del email y otras personalizaciones de canales anónimos y conocidos.
landing-page-description: Sincronice la personalización del sitio web con la del email y otras personalizaciones de canales anónimos y conocidos.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: b050017505b8d77fcf507e4dec147b66c561779a
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 81%

---


# Web/Mobile Personalization con datos de clientes conocidos

## Casos de uso

* Personalización en línea con datos de clientes conocidos
* Optimización de la página de aterrizaje
* Personalización basada en visualizaciones de productos/contenidos anteriores, afinidad de producto/contenido, atributos del entorno y datos demográficos, además de datos sin conexión, tales como datos de transacciones, fidelidad y CRM, e información modelada.
* Comparta y dirija audiencias definidas en Real-time Customer Data Platform en sitios web y aplicaciones móviles mediante Adobe Target.

## Aplicaciones

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager (opcional): Agrega datos de audiencia de terceros, gráfico de dispositivos basado en cooperación
* Adobe Analytics (opcional): añade la habilidad de generar segmentos basados en los datos de comportamiento histórico y realizar una segmentación detallada de los datos de Adobe Analytics.

## Patrones de integración

| # | Patrón de integración | Capacidad | Requisitos previos |
|---|---|---|---|
| 1 | Evaluación de segmentos en tiempo real en Edge compartida desde Real-time Customer Data Platform en Target | <ul><li>Evalúe las audiencias en tiempo real para la personalización de la misma página o de la siguiente en Edge.</li><li>Además, cualquier segmento evaluado en streaming o por lotes también se proyectará en la red de Edge para que se incluya en la evaluación y personalización de segmentos de Edge.</li></ul> | <ul><li>El SDK web/móvil debe implementarse.</li><li>El conjunto de datos debe configurarse en Experience Edge con la extensión Target y el Experience Platform habilitada</li><li>El Target específico debe configurarse en destinos de Real-time Customer Data Platform.</li><li>La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.</li></ul> |
| 2 | Uso compartido de audiencias por streaming y por lotes desde Real-time Customer Data Platform en Target con el enfoque de Edge | <ul><li>Comparta audiencias de flujo continuo y por lotes de Real-time Customer Data Platform en Target a través de Edge Network. Las audiencias evaluadas en tiempo real requieren la implementación de WebSDK y Edge Network.</li></ul> | <ul><li>El SDK web/Mobile no es necesario para compartir audiencias de flujo continuo y por lotes con Target, aunque es necesario para habilitar la evaluación de segmentos perimetrales en tiempo real.</li><li>Si utiliza AT.js, solo se admite la integración de perfiles con el área de nombres de identidad de ECID.</li><li>Para las búsquedas del área de nombres de identidad personalizadas en Edge, la implementación de WebSDK es necesaria y cada identidad debe establecerse como identidad en el mapa de identidades.</li><li>El Target específico debe configurarse en destinos de Real-time Customer Data Platform.</li><li>La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.</li></ul> |
| 3 | Uso compartido de audiencias de streaming y lotes de Real-time Customer Data Platform en Target y Audience Manager con el enfoque del servicio de uso compartido de audiencias | <ul><li>Este patrón de integración se puede aprovechar cuando se desea un enriquecimiento adicional de datos y audiencias de terceros en Audience Manager.</li></ul> | <ul><li>El SDK web/Mobile no es necesario para compartir audiencias de flujo continuo y por lotes con Target, aunque es necesario para habilitar la evaluación de segmentos perimetrales en tiempo real.</li><li>Si utiliza AT.js, solo se admite la integración de perfiles con el área de nombres de identidad de ECID.</li><li>Para las búsquedas del área de nombres de identidad personalizadas en Edge, la implementación de WebSDK es necesaria y cada identidad debe establecerse como identidad en el mapa de identidades.</li><li>Se debe aprovisionar la proyección de audiencias mediante el servicio de uso compartido de audiencias.</li><li>El Target específico debe configurarse en destinos de Real-time Customer Data Platform.</li><li>La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.</li></ul> |

## Uso compartido de audiencias en tiempo real, por transmisión y por lotes en Adobe Target

Arquitectura

<img src="assets/RTCDP+Target.png" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a" />

Detalle de secuencia

<img src="assets/RTCDP+Target_flow.png" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a" />

Vista general de la arquitectura

<img src="assets/personalization_with_apps.png" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a"/>

## Patrones de implementación

El conocido Personalization del cliente se admite mediante varios enfoques de implementación.

### Patrón de implementación 1: red perimetral con SDK web/Mobile (enfoque recomendado)

Uso de Edge Network con el SDK web/móvil. La segmentación perimetral en tiempo real requiere el enfoque de implementación del SDK web/Mobile o de la API perimetral.

[Consulte el modelo del SDK móvil y web de Experience Platform](../data-ingestion/websdk.md)

### Patrón de implementación 2: SDK específicos de la aplicación

Con SDK tradicionales específicos de cada aplicación (por ejemplo, AT.js y AppMeasurement.js). La evaluación de segmentos en tiempo real de Edge no es compatible con este método de implementación. Sin embargo, el uso compartido de audiencias por flujo continuo y por lotes desde el centro de Experience Platform es compatible con este método de implementación.

[Consulte el modelo de SDK específico de la aplicación](../data-ingestion/appsdk.md)

### Pasos de implementación

1. [Implemente Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=es) para sus aplicaciones móviles o web
1. [Implemente Experience Platform y [!UICONTROL Real-time Customer Profile]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=es), y asegúrese de que las audiencias creadas se activen en Edge configurando las [políticas de combinación](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=es#create-a-merge-policy) como activas en Edge.
1. Implemente [el SDK web de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es). El SDK web de Experience Platform es necesario para la segmentación en tiempo real de Edge, pero no es necesario para compartir audiencias de flujo continuo y por lotes de Real-time Customer Data Platform en Target. Tenga en cuenta que actualmente no está disponible la compatibilidad con la segmentación en tiempo real mediante el SDK móvil y la API.
1. [Configuración de Edge Network con una secuencia de datos de Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)
1. [Activación de Adobe Target como destino en Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=es)
1. (Opcional) [Implementación de Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=es) (opcional)
1. (Opcional) [Solicitar aprovisionamiento para el uso compartido de audiencias entre Experience Platform y Adobe Target (audiencias compartidas)](https://www.adobe.com/go/audiences) para compartir audiencias de Experience Platform a Target.

## Guardas

[Consulte los guardas de la página de información general sobre los modelos de personalización web/móvil.](overview.md)

## Consideraciones sobre la implementación

Requisitos previos de identidad

* Cualquier identidad principal se puede aprovechar al utilizar el patrón de implementación 1 descrito anteriormente con Edge Network y WebSDK. La personalización del primer inicio de sesión requiere que la identidad principal del conjunto de solicitudes de personalización coincida con la identidad principal del perfil de Real-time Customer Data Platform. La vinculación de identidad entre dispositivos anónimos y clientes conocidos se procesa en el centro y, posteriormente, se proyecta al extremo.
* El uso compartido de audiencias de Adobe Experience Platform en Adobe Target requiere el uso de ECID como identidad al utilizar el servicio de uso compartido de audiencias, tal como se describe en el escenario de caso de uso 3 anterior.
* También se pueden usar identidades alternativas para compartir audiencias de Experience Platform en Adobe Target a través de Audience Manager. Experience Platform activa las audiencias en Audience Manager mediante las siguientes áreas de nombres admitidas: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Tenga en cuenta que Audience Manager y Target resuelven las pertenencias a audiencias a través de la identidad de ECID, por lo que ECID sigue siendo necesario para que la audiencia final se comparta en Adobe Target.

## Documentación relacionada

### Documentación del SDK

* [Documentación del SDK web de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
* [Documentación de Experience Cloud ID Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es)

### Documentación de la conexión

* [Conexión de Adobe Target para Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
* [Configuración de la secuencia de datos de Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)
* [Compartir segmentos en Experience Platform con Audience Manager y otras soluciones de Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=es)

### Documentación de la segmentación

* [Información general sobre la segmentación en Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=es)
* [Segmentación en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=es)
* [Segmentación por flujo](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Intercambio de segmentos de Adobe Analytics mediante Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=es)
* [Configuración de políticas de combinación](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=en#create-a-merge-policy)

### Tutoriales

* [Personalización de próxima visita con Real-Time CDP y Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=es)

### Entradas relacionadas en el blog

* [Adobe lanza la personalización mejorada de la misma página con Adobe Target y Real-time Customer Data Platform](https://blog.adobe.com/en/publish/2021/10/05/adobe-announces-same-page-enhanced-personalization-with-adobe-target-real-time-customer-data-platform)
* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
