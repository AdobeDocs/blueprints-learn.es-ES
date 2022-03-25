---
title: Personalización web/móvil con datos en línea y sin conexión
description: Sincronice la personalización del sitio web con la del email y otras personalizaciones de canales anónimos y conocidos.
landing-page-description: Sincronice la personalización del sitio web con la del email y otras personalizaciones de canales anónimos y conocidos.
solution: Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 17faffdd972f2485951ac1e870b578e9b1a011a5
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 100%

---


# Personalización web/móvil con datos en línea y sin conexión

## Casos de uso

* Personalización en línea con datos en línea y sin conexión, y perfiles conocidos
* Optimización de la página de aterrizaje
* Personalización basada en visualizaciones de productos/contenidos anteriores, afinidad de producto/contenido, atributos del entorno y datos demográficos, además de datos sin conexión, tales como datos de transacciones, fidelidad y CRM, e información modelada.
* Comparta y dirija audiencias definidas en Real-time Customer Data Platform en sitios web y aplicaciones móviles mediante Adobe Target.

## Aplicaciones

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager (opcional): añade datos de audiencia de terceros, gráficos de cooperación basados en dispositivos y la habilidad de rescatar audiencias de Real-time Customer Data Platform en Adobe Analytics y viceversa.
* Adobe Analytics (opcional): añade la habilidad de generar segmentos basados en los datos de comportamiento histórico y realizar una segmentación detallada de los datos de Adobe Analytics.

## Escenarios de casos de uso

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
    <th class="tg-f7v4">Escenarios de casos de uso</th>
    <th class="tg-y6fn">Capacidad</th>
    <th class="tg-f7v4">Requisitos previos</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">1</td>
<td class="tg-73oq">Evaluación de segmentos en tiempo real en Edge compartida desde Real-time Customer Data Platform en Target</td>
    <td class="tg-0lax">- Evalúe las audiencias en tiempo real para la personalización de la misma página o de la siguiente en Edge.<br>- Además, cualquier segmento evaluado en streaming o por lotes también se proyectará en la red de Edge para que se incluya en la evaluación y personalización de segmentos de Edge.</td>
    <td class="tg-73oq">- El patrón de implementación 1 se describe a continuación.<br>- El SDK web/móvil debe implementarse.<br>- Tenga en cuenta que el SDK móvil y la compatibilidad basada en API para la segmentación en tiempo real no están disponibles actualmente.<br>- La secuencia de datos debe configurarse en Experience Edge con la extensión de Target y Experience Platform habilitada, el ID de la secuencia de datos se proporcionará en la configuración de destino de Target.<br>- El Target específico debe configurarse en destinos de Real-time Customer Data Platform.<br>- La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.</td> 
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-73oq">Uso compartido de audiencias por streaming y por lotes desde Real-time Customer Data Platform en Target con el enfoque de Edge</td>
    <td class="tg-0lax">- Comparta audiencias de flujo continuo y por lotes de Real-time Customer Data Platform en Target a través de Edge Network. Las audiencias evaluadas en tiempo real requieren el uso de WebSDK y la evaluación de audiencias en tiempo real que se describen en el patrón de integración 1.<br>- Esta integración suele aprovecharse para compartir audiencias de streaming y lotes mediante SDK tradicionales en lugar de migrar a la recopilación de Edge y a SDK web, que alimenta las audiencias en tiempo real, así como las de streaming y lotes, tal como se describe en el patrón de integración 1.</td>
    <td class="tg-73oq">- El patrón de implementación 1 o 2 se describe a continuación.<br>- El SDK web/móvil no es necesario para compartir audiencias de streaming y lotes en Target, aunque es necesario para habilitar la evaluación de segmentos de Edge en tiempo real como se describe en el patrón de integración 1. <br>- Si utiliza AT.js, solo se admite la integración de perfiles con el área de nombres de identidad de ECID. <br>- Para las búsquedas del área de nombres de identidad personalizadas en Edge, la implementación de WebSDK es necesaria y cada identidad debe establecerse como identidad en el mapa de identidades.<br>- La secuencia de datos debe configurarse en Experience Edge. El ID de la secuencia de datos se proporcionará en la configuración de destino de Target.<br>- El Target específico debe configurarse en destinos de Real-time Customer Data Platform.<br>- La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-73oq"><span style="font-weight:400;font-style:normal">Uso compartido de audiencias de streaming y lotes de Real-time Customer Data Platform en Target y Audience Manager con el enfoque del servicio de uso compartido de audiencias</span></td>
    <td class="tg-0lax"><span style="font-weight:400;font-style:normal">- Comparta audiencias de flujo continuo y por lotes de Real-time Customer Data Platform en Target y Audience Manager con el enfoque del servicio de uso compartido de audiencias.<br>- Este patrón de integración se puede aprovechar cuando se desea un enriquecimiento adicional de datos y audiencias de terceros en Audience Manager. De lo contrario, se prefieren los patrones de integración 1 y 2. Las audiencias evaluadas en tiempo real requieren el uso de WebSDK y la evaluación de audiencias en tiempo real que se describen en el patrón de integración 1.</span></td>
    <td class="tg-73oq">- El patrón de implementación 1 o 2 se describe a continuación.<br>- La implementación del SDK web/móvil no es necesaria para esta integración.<br>- Se debe aprovisionar la proyección de audiencias mediante el servicio de uso compartido de audiencias.<br>- La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform.<br>- La identidad debe resolverse en ECID para compartirla en el extremo para que Target actúe al respecto.</td>
  </tr>
</tbody>
</table>

## Escenario 1 y 2: - Uso compartido de audiencias en tiempo real, por streaming y por lotes en Adobe Target

Arquitectura

<img src="assets/RTCDP+Target.png" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a" />

Detalle de secuencia

<img src="assets/RTCDP+Target_flow.png" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a" />

Arquitectura de información general para los casos de uso 1 y 2

<img src="assets/personalization_with_apps.png" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a"/>

### Pasos de implementación para el Escenario de caso de uso 1, que también admite el Caso de uso 2

1. [Implemente Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=es) para sus aplicaciones móviles o web
1. [Implemente Experience Platform y [!UICONTROL Real-time Customer Profile]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=es), y asegúrese de que las audiencias creadas se activen en Edge configurando las [políticas de combinación](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=es#create-a-merge-policy) como activas en Edge.
1. Implemente [el SDK web de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es). El SDK web de Experience Platform es necesario para la segmentación en tiempo real de Edge, pero no es necesario para compartir audiencias de flujo continuo y por lotes de Real-time Customer Data Platform en Target. Tenga en cuenta que actualmente no está disponible la compatibilidad con la segmentación en tiempo real mediante el SDK móvil y la API.
1. [Configuración de Edge Network con una secuencia de datos de Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)
1. [Activación de Adobe Target como destino en Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=es)

<br>

## Escenario 3: Uso compartido de audiencias de streaming y lotes a través del servicio de uso compartido de audiencias con Adobe Target y Audience Manager

Arquitectura

<img src="assets/audience_share_architecture.png" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a" />

### Pasos de implementación para el escenario 3, que también se admiten en el escenario 2

1. [Implemente Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) para sus aplicaciones móviles o web
1. [Implemente Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=es) (opcional)
1. [Implemente Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) (opcional)
1. [Implemente Experience Platform y [!UICONTROL Real-time Customer Profile]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html)
1. Implemente [el Servicio de identidad de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=es).
1. [Solicite aprovisionamiento para el uso compartido de audiencias entre Experience Platform y Adobe Target (audiencias compartidas)](https://www.adobe.com/go/audiences) para compartir audiencias de Experience Platform en Target.
1. (Opcional) [Configure Edge Network con una secuencia de datos de Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html). (Esto solo es necesario en el caso del patrón de integración 2, en el que las audiencias no necesitan compartirse con Audience Manager ni enriquecirse con audiencias o datos de Audience Manager).
1. (Opcional) [Habilite Adobe Target como destino en Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en) para compartir audiencias de streaming y lotes desde Real-time Customer Data Platform directamente en Edge, en lugar de a través del servicio de uso compartido de audiencias y Audience Manager.

<br>

## Patrones de implementación

La personalización en línea y sin conexión es compatible mediante varios enfoques de implementación.

### Patrón de implementación 1, que admite los casos de uso 1 y 2. Edge Network con SDK web/móvil (enfoque recomendado)

Uso de Edge Network con el SDK web/móvil
<img src="assets/web_sdk_flow.png" alt="Arquitectura de referencia del enfoque con el SDK específico de cada aplicación" style="width:80%; border:1px solid #4a4a4a" />

Diagrama de secuencia

<img src="assets/RTCDP+Target_sequence.png" alt="Arquitectura de referencia del modelo de personalización del sitio web en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a" />

<br>

### Patrón de implementación 2, que admite los casos de uso 2 y 3. SDK específicos de la aplicación

Con SDK tradicionales específicos de cada aplicación (por ejemplo, AT.js y AppMeasurement.js)
<img src="assets/app_sdk_flow.png" alt="Arquitectura de referencia del enfoque con el SDK específico de cada aplicación" style="width:80%; border:1px solid #4a4a4a" />

<br>

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
