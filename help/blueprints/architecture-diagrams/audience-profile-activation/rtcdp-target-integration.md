---
title: Integración de Adobe Real-Time CDP y Adobe Target
description: Comprenda cómo las audiencias de Real-Time Customer Data Platform y el contexto de perfil se integran con Adobe Target a través de Edge Network.
landing-page-description: Comprenda cómo las audiencias de Real-Time Customer Data Platform y el contexto de perfil se integran con Adobe Target a través de Edge Network.
short-description: Comprenda cómo las audiencias de Real-Time Customer Data Platform y el contexto de perfil se integran con Adobe Target a través de Edge Network.
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
TQID: https://experienceleague.adobe.com/1ti2SqfAFOgnKbaJ70xwGI-xHDE1WXJ7-oTStcJJy1E
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
    internal-label: Real-Time Customer Data Platform
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
    internal-label: Segmentation
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: ba929a52-9339-4154-9487-317dc875a3c7
    internal-label: Use cases
  - id: c132d929-fa62-4271-803e-b823be07b914
    internal-label: Profile
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
    internal-label: Implementation
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
    internal-label: Segments
  - id: cdd3e38b-fec2-4f39-8b10-83ddaab1ac16
    internal-label: B2B
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
    internal-label: Audiences
  - id: ee602049-8a18-43df-9299-a689a025a371
    internal-label: Use cases
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
    internal-label: Measurement
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 17%
---
# Integración de Adobe Real-Time CDP y Adobe Target

Esta arquitectura muestra cómo se integran [!DNL Real-Time Customer Data Platform] y [!DNL Adobe Target] a través de Edge Network. Le ayuda a seleccionar entre la evaluación de audiencias en tiempo real en el perímetro de y el uso compartido de audiencias de streaming o por lotes con Target.

## Aplicaciones

* [!DNL Real-Time Customer Data Platform]
* [!DNL Adobe Target]
* [!DNL Experience Platform] Edge Network
* API de servidor de Experience Platform Web SDK o Edge Network

## Elija un enfoque de integración

### Evaluación de audiencias en tiempo real en Edge

Utilice este método cuando [!DNL Adobe Target] necesite audiencias evaluadas por Edge y atributos de perfil para la personalización de la misma página o de la página siguiente. Implemente la API de Web SDK o Edge Network Server y configure un conjunto de datos con los servicios [!DNL Adobe Target] y [!DNL Experience Platform] habilitados.

### Streaming y uso compartido de audiencias por lotes a Target

Utilice este método cuando las audiencias evaluadas en [!DNL Real-Time Customer Data Platform] deban estar disponibles en [!DNL Adobe Target] sin evaluación de Edge en tiempo real. Configure el destino [!DNL Adobe Target] en la zona protegida de producción predeterminada. La implementación de la API de servidor de Edge Network o Web SDK solo es necesaria para la evaluación de Edge en tiempo real o las búsquedas del área de nombres de identidad personalizadas.

## Diagrama de arquitectura

Este diagrama muestra los puntos de integración principales entre la recopilación de datos, Edge Network, [!DNL Real-Time Customer Data Platform] y [!DNL Adobe Target].

![Arquitectura para la integración de Real-Time Customer Data Platform y Adobe Target](assets/real_time_cdp_target.png){zoomable="yes"}

## Diagrama de flujo de datos

Esta secuencia muestra cómo una solicitud de cliente llega a Edge Network, evalúa las audiencias y el contexto del perfil, envía una solicitud de personalización a [!DNL Adobe Target] y devuelve la experiencia resultante al cliente.

![Flujo de datos para la integración de Real-Time Customer Data Platform y Adobe Target](assets/real_time_cdp_target_data_flow_detail.png){zoomable="yes"}

## Consideraciones sobre la implementación

* [!DNL Adobe Target] y [!DNL Real-Time Customer Data Platform] deben usar la misma organización de IMS.
* El destino [!DNL Adobe Target] admite la zona protegida de producción predeterminada en [!DNL Real-Time Customer Data Platform].
* Para realizar búsquedas personalizadas de área de nombres de identidad en el perímetro, utilice Web SDK o la API de servidor de Edge Network e incluya cada identidad en el mapa de identidad.
* Si utiliza at.js, la integración de perfiles solo admite el área de nombres de identidad de ECID.

## Documentación relacionada

### Configuración de la integración

* [Adobe Target Connection para Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Configuración de flujo de datos Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)

### Implementación en el perímetro de

* [Documentación de Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es)
* [Documentación de etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
* [Documentación del servicio de Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es)

### Evaluar públicos

* [Resumen de segmentación de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=es)
* [Segmentación en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=es)
* [Segmentación de streaming](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Configuración de política de combinación](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=es#create-a-merge-policy)
