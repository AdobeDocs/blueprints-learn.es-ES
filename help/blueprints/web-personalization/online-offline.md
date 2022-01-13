---
title: Personalización web/móvil con datos en línea y sin conexión
description: Sincronice la personalización del sitio web con la del email y otras personalizaciones de canales anónimos y conocidos.
landing-page-description: Sincronice la personalización del sitio web con la del email y otras personalizaciones de canales anónimos y conocidos.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 070c78ee3cf32e70af90c6cbcdd77d5258a32fb7
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 63%

---

# Personalización web/móvil con datos en línea y sin conexión

Sincronice la personalización del sitio web con la del email y otras personalizaciones de canales anónimos y conocidos.

## Casos de uso

* Optimización de la página de aterrizaje
* Segmentación de perfiles según comportamiento y sin conexión
* Personalización basada en visualizaciones de productos/contenidos anteriores, afinidad de producto/contenido, atributos del entorno, datos de audiencia de terceros y sectores demográficos, además de datos sin conexión, tales como transacciones, datos de fidelidad y CRM, y datos modelados.
* Comparta y dirija audiencias definidas en Real-time Customer Data Platform en sitios web y aplicaciones móviles mediante Adobe Target.

## Aplicaciones

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager (opcional): añade datos de audiencia de terceros, gráficos de cooperación basados en dispositivos y la habilidad de rescatar segmentos de Platform en Adobe Analytics y viceversa.
* Adobe Analytics (opcional): añade la habilidad de generar segmentos basados en los datos de comportamiento histórico y realizar una segmentación detallada de los datos de Adobe Analytics.

## Patrones de integración

<table class="tg" style="undefined;table-layout: fixed; width: 790px">
<colgroup>
<col style="width: 20px">
<col style="width: 276px">
<col style="width: 229px">
<col style="width: 265px">
</colgroup>
<thead>
  <tr>
    <th class="tg-y6fn">#</th>
    <th class="tg-f7v4">Patrón de integración</th>
    <th class="tg-y6fn">Capacidad</th>
    <th class="tg-f7v4">Requisitos previos</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">1</td>
    <td class="tg-73oq"><span style="font-weight:400;font-style:normal">Flujo continuo RTCDP y uso compartido de audiencias en lote en Target y Audience Manager mediante el enfoque del servicio de uso compartido de audiencias</span></td>
    <td class="tg-0lax"><span style="font-weight:400;font-style:normal">: comparta audiencias de flujo continuo y por lotes de RTCDP a Target y Audience Manager a través del servicio de uso compartido de audiencias. Las audiencias evaluadas en tiempo real requieren el uso de WebSDK y la evaluación de audiencias en tiempo real que se describen en el patrón de integración 3.</span></td>
    <td class="tg-73oq">: se debe aprovisionar la proyección de audiencias mediante el servicio de uso compartido de audiencias.<br>: la integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.<br>: la identidad debe resolverse en ECID para compartirla en el perímetro para que Target actúe al respecto. AAM tiene una lista separada de identidades aprobadas con la que hacer coincidir<br>: La implementación de WebSDK no es necesaria para esta integración.</td>
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-73oq">Flujo continuo RTCDP y uso compartido de audiencias en lote en Target mediante el enfoque de Edge</td>
    <td class="tg-0lax">: comparta audiencias de flujo continuo y por lotes de RTCDP a Target a través de la red perimetral. Las audiencias evaluadas en tiempo real requieren el uso de WebSDK y la evaluación de audiencias en tiempo real que se describen en el patrón de integración 3.</td>
    <td class="tg-73oq"><span style="text-decoration:none">- Actualmente en versión beta</span><br>- El destino de destino debe configurarse en Destinos RTCDP.<br>: la integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.<br>WebSDK no es obligatorio. Se admiten WebSDk y AT.js. <br>- Si se utiliza AT.js, solo se admite la búsqueda de perfiles con el ECID. <br>: Para las búsquedas de espacio de nombres de id personalizadas en Edge, la implementación de WebSDK es necesaria y cada identidad debe establecerse como identidad en el mapa de identidad.</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-73oq">Evaluación de segmentos en tiempo real de RTCDP en Edge compartido con Target a través de la red perimetral mediante WebSDK.</td>
    <td class="tg-0lax">: Evalúe las audiencias en tiempo real para la personalización de la misma página o de la siguiente en Edge.</td>
    <td class="tg-73oq"><span style="text-decoration:none">- Actualmente en versión beta</span><br>- El destino de destino debe configurarse en Destinos RTCDP.<br>: la integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.<br>- Se debe implementar WebSDK.<br>: También se admite mediante API.</td>
  </tr>
</tbody>
</table>


## Arquitectura

Arquitectura general

<img src="assets/RTCDP+Target.png" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a" />

Arquitectura de flujo de proceso

<img src="assets/RTCDP+Target_flow.png" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a" />

Arquitectura detallada

<img src="assets/personalization_with_apps.png" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a"/>

## Guardas

[Consulte los guardas de la página de información general sobre los modelos de personalización web/móvil.](overview.md)

## Patrones de implementación

El modelo de personalización web/móvil se puede implementar mediante los siguientes enfoques, tal como se describe a continuación.

1. Con el [!UICONTROL SDK Platform Web] o [!UICONTROL SDK Platform Mobile] y [!UICONTROL Edge Network].
1. Con SDK tradicionales específicos de cada aplicación (por ejemplo, AppMeasurement.js)

### 1. Enfoque con el SDK Platform Web/Mobile y Edge

[Consulte el modelo del SDK móvil y web de Experience Platform](../data-ingestion/websdk.md)

### 2. Enfoque con el SDK específico de cada aplicación

<img src="assets/app_sdk_flow.png" alt="Arquitectura de referencia del enfoque con el SDK específico de cada aplicación" style="width:80%; border:1px solid #4a4a4a" />

## Prerrequisitos de implementación

Requisitos previos de identidad

* El uso compartido de audiencias de Adobe Experience Platform con Adobe Target requiere el uso de ECID como identidad.
* También se pueden usar identidades alternativas para compartir audiencias de Experience Platform a Adobe Target a través de Audience Manager. Experience Platform activa las audiencias en Audience Manager mediante las siguientes áreas de nombres admitidas: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Tenga en cuenta que Audience Manager y Target resuelven las suscripciones de audiencia a través de la identidad de ECID, por lo que ECID sigue siendo necesario para que la audiencia final se comparta en Adobe Target.

| Aplicación/servicio | Biblioteca requerida | Notas |
|---|---|---|
| Adobe Target | [!UICONTROL SDK Platform Web]*, at.js 0.9.1+ o mbox.js 61+ | Se recomienda at.js debido a que mbox.js ya no se desarrolla. |
| Adobe Audience Manager (opcional) | [!UICONTROL SDK Platform Web]* o dil.js 5.0+ |  |
| Adobe Analytics (opcional) | [!UICONTROL SDK Platform Web]* o AppMeasurement.js 1.6.4+ | El seguimiento de Adobe Analytics debe emplear la recopilación de datos regional (RDC). |
| Servicio Experience Cloud ID | [!UICONTROL SDK Platform Web]* o VisitorAPI.js 2.0+ | (Recomendación) Emplear Experience Platform Launch para implementar el servicio de ID y así garantizar que este ID se configure antes de la llamada de cualquier aplicación. |
| SDK Experience Platform Mobile (opcional) | 4.11 o superior para iOS y Android™ |  |
| SDK web de Experience Platform | 1.0, la versión actual del SDK Experience Platform, cuenta con [varios casos de uso sin compatibilidad con las aplicaciones de Experience Cloud](https://github.com/adobe/alloy/projects/5) |  |




## Pasos de implementación

1. [Implementar Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=es) para sus aplicaciones móviles o web
1. [Implementar Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=es) (opcional)
1. [Implementar Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) (opcional)
1. [Implementar Experience Platform y [!UICONTROL Real-time Customer Profile]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=es)
1. Implementar el [Servicio de identidad de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=es) o el [SDK web de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es)
1. [Habilitar Adobe Target como destino en Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en) o para el enfoque de uso compartido de audiencias [Solicitar aprovisionamiento para el uso compartido de audiencias entre Experience Platform y Adobe Target (audiencias compartidas)](https://www.adobe.com/go/audiences) para compartir audiencias de Experience Platform a Target.
   >[!NOTE]
   >
   >Al utilizar el servicio de uso compartido de audiencias entre RTCDP y Adobe Target, las audiencias deben compartirse con el ID de Experience Cloud y formar parte de la misma organización de Experience Cloud. La compatibilidad con identidades distintas de ECID requiere el uso de WebSDK y Experience Edge Network.


## Documentación relacionada

* [Compartir segmentos en Experience Platform con Audience Manager y otras soluciones de Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=es)
* [Información general sobre la segmentación en Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=es)
* [Segmentación por streaming](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Conexión de Adobe Target para Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
* [Información general sobre el generador de segmentos de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=es)
* [Conector de origen de Audience Manager](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=es)
* [Intercambio de segmentos de Adobe Analytics mediante Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=es)
* [Documentación del SDK web de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Documentación de Experience Cloud ID Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)

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
