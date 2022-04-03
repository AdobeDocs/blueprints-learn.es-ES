---
title: Modelo de activación de audiencias y perfiles con las aplicaciones de Experience Cloud
description: Administrar perfiles y audiencias en Experience Platform y compartirlas con las aplicaciones de Experience Cloud.
solution: Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services
kt: 7722
exl-id: f36014e8-170d-47e1-b4ec-10c0ea70612d
source-git-commit: 3425495df36ff8da0f2fd737b35d294ccafe31bd
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 100%

---

# Modelo de activación de audiencias y perfiles con las aplicaciones de Experience Cloud

Administrar perfiles y audiencias en Experience Platform y compartirlas con las aplicaciones de Experience Cloud. Generar y compartir segmentos y datos enriquecidos de clientes en Experience Platform y compartirlos con las aplicaciones de Experience Cloud.

La activación con las aplicaciones de Experience Cloud se alinea estrechamente con el [Modelo de activación de cliente conocida](known.md).

## Casos de uso

* Personalización y segmentación a través de los canales de interacción del cliente con Experience Cloud.
* Intercambio de datos de audiencias y perfiles entre Experience Platform y las aplicaciones de Experience Cloud.

## Aplicaciones

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]
* Experience Platform Activation
* Aplicaciones de Experience Cloud
   * Adobe Audience Manager
   * Adobe Target
   * Adobe Campaign
   * Journey Optimizer

## Arquitectura

Consulte la sección [Arquitectura de Experience Platform y otras aplicaciones](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=es) para ver más diagramas de arquitectura relacionados con las integraciones de Experience Platform con aplicaciones de Experience Cloud.

### Activación de audiencias y perfiles con las aplicaciones de Experience Cloud

<img src="../experience-platform/assets/aep+apps_horizontal.svg" alt="Arquitectura de referencia de la activación de audiencias y perfiles con las aplicaciones de Experience Cloud" style="width:90%; border:1px solid #4a4a4a" />
<br>

## Guardas

Consulte los [guardas de la página de información general sobre la activación de audiencias y perfiles.](overview.md)

## Consideraciones sobre la implementación

* Compartir datos de perfil con los destinos requiere incluir un valor de identidad específico utilizado por el destino en su carga. Cualquier identidad que requiera el destino específico debe ingerirse en Platform y configurarse como identidad en [!UICONTROL Real-time Customer Profile].

### Uso compartido de audiencias de Real-time Customer Data Platform con Audience Manager

* Consulte la siguiente documentación para obtener más información. [Compartir segmentos en Experience Platform con Audience Manager y otras soluciones de Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=es).

* La pertenencia a audiencias de RT-CDP se comparte con Audience Manager de forma continua en cuanto se completa la evaluación de segmentos y se escribe en el perfil del cliente en tiempo real, independientemente de si la evaluación de segmentos se produce en lote o en flujo continuo. Si el perfil cualificado contiene la información de enrutamiento regional para dispositivos de perfil relacionados, la pertenencia a audiencias de RT-CDP se clasifica en modo de flujo continuo en Audience Manager Edge asociado. Si la información de enrutamiento regional se aplicó a un perfil con una marca de tiempo en los últimos 14 días, se evaluará en Audience Manager Edge en modo de flujo continuo. Si los perfiles de RTCDP no contienen información de enrutamiento regional o si la información de enrutamiento regional tiene más de 14 días, las pertenencias a perfiles se envían a la ubicación del centro de Audience Manager para la evaluación y activación basadas en lotes. Los perfiles aptos para la activación de Edge se activarán en cuestión de minutos después de la calificación de segmentos de RT-CDP, los perfiles que no cumplen los requisitos para la activación de Edge se clasificarán en el centro de Audience Manager y pueden tener un intervalo de tiempo de 12 a 24 horas para el procesamiento.

* La información de enrutamiento regional en la que se almacena el perfil de Audience Manager de Edge se puede recopilar en Experience Platform desde Audience Manager, el servicio de ID de visitante, Analytics, Launch o directamente desde el SDK web como un conjunto de datos de clase de registro de perfil independiente mediante el grupo de campos XDM &quot;información de región de captura de datos&quot;.

* En los casos de activación en los que las audiencias se comparten de Experience Platform a Audience Manager, las siguientes identidades se comparten automáticamente: ECID, IDFA, GAID, direcciones de correo electrónico con hash (EMAIL_LC_SHA256), AdCloud ID. Actualmente, las áreas de nombres de los clientes no se comparten.

* Las audiencias de Experience Platform se pueden compartir a través de los destinos de Audience Manager cuando las identidades de destino necesarias se incluyan en [!UICONTROL Real-time Customer Profile] o cuando las identidades de [!UICONTROL Real-time Customer Profile] se relacionen con las identidades requeridas en destino, si están vinculadas en Audience Manager.

### Uso compartido de audiencias de Real-time Customer Data Platform con Target

* Consulte la [Personalización web/móvil con modelos de datos en línea y sin conexión](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/web-personalization/online-offline.html?lang=es) para obtener más información sobre cómo compartir perfiles y audiencias de Real-time Customer Data Platform en Target.

### Uso compartido de audiencias de Real-time Customer Data Platform con Campaign y Journey Optimizer

* Consulte los [modelos de recorridos del cliente](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/overview.html?lang=es) para obtener más información sobre el uso compartido de perfiles y audiencias de Real-time Customer Data Platform en Campaign y Journey Optimizer.

## Documentación relacionada

* Descripción del producto [[!UICONTROL Real-time Customer Data Platform]](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform.html)
* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Documentación de la segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Documentación de los destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=es)

## Vídeos y tutoriales relacionados

* Información general de [[!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=es)
* [Versión de prueba de [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=es)
* [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=es)
