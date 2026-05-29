---
title: Personalization de cliente conocido con Target
description: Integre perfiles y públicos RTCDP con Adobe Target.
landing-page-description: Integre perfiles y públicos RTCDP con Adobe Target.
short-description: Integre perfiles y públicos RTCDP con Adobe Target.
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
TQID: https://experienceleague.adobe.com/1ti2SqfAFOgnKbaJ70xwGI-xHDE1WXJ7-oTStcJJy1E
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: ba929a52-9339-4154-9487-317dc875a3c7
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
  - id: cdd3e38b-fec2-4f39-8b10-83ddaab1ac16
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
  - id: ee602049-8a18-43df-9299-a689a025a371
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 213e2d7d73d91fa7b487289dfe62685bc32d5029
workflow-type: tm+mt
source-wordcount: 735
ht-degree: 37%

---

# Personalization de cliente conocido con Target

>[!TIP]
>Este modelo también está disponible como [patrón de caso de uso](/help/blueprints/use-case-patterns/personalization/audience-sharing-with-target.md) en Personalization.

## Casos de uso

* Personalización en línea con datos de clientes conocidos
* Optimización de la página de aterrizaje
* Personalización basada en visualizaciones de productos/contenidos anteriores, afinidad de producto/contenido, atributos del entorno y datos demográficos, además de datos sin conexión, tales como datos de transacciones, fidelidad y CRM, e información modelada.
* Comparta y segmente audiencias definidas en Real-time Customer Data Platform en sitios web y aplicaciones móviles mediante Adobe Target

## Aplicaciones

* [!UICONTROL Real-Time Customer Data Platform]
* Adobe Target

### Documentación de referencia

* [Adobe Target Connection para Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=es)
* [Configuración de flujo de datos Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)

## Patrones de integración

| Patrón de integración | Capacidad | Requisitos previos |
|--------------------|------------|---------------|
| **Evaluación de segmentos en tiempo real en Edge compartidos desde Real-time Customer Data Platform a Target** | : Evalúe las audiencias en tiempo real para la personalización de la misma página o de la siguiente en Edge. <br>: cualquier segmento evaluado en flujo continuo o por lotes también se proyectará a Edge Network para que se incluya en la evaluación y personalización de segmentos de Edge. | : Web/Mobile SDK debe estar implementado para la API de servidor de Edge Network. <br>: la secuencia de datos debe configurarse en Experience Edge con la extensión de Target y Experience Platform habilitada. <br>: el destino de destino debe configurarse en Destinos de Real-time Customer Data Platform. <br>- La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform. |
| **Uso compartido de streaming y audiencias por lotes desde Real-time Customer Data Platform a Target a través del enfoque de Edge** | - Comparta audiencias de flujo continuo y por lotes de Real-time Customer Data Platform en Target a través de Edge Network. <br>: las audiencias evaluadas en tiempo real requieren la implementación de Web SDK y Edge Network. | : La implementación de la API de Edge o la SDK web/móvil de Target no es necesaria para compartir audiencias de streaming y RTCDP por lotes con Target, pero se requiere para habilitar la evaluación de segmentos perimetrales en tiempo real. <br>- Si utiliza AT.js, solo se admite la integración de perfiles con el área de nombres de identidad de ECID. <br>: para las búsquedas de área de nombres de identidad personalizadas en Edge, se requiere la implementación de la API de Web SDK/Edge, y cada identidad debe establecerse como identidad en el mapa de identidad. <br>: el destino de destino debe configurarse en Destinos de Real-time Customer Data Platform; solo se admite la zona protegida de producción predeterminada en RTCDP. <br>- La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform. |
| **Uso compartido de streaming y audiencias por lotes desde Real-time Customer Data Platform a Target y Audience Manager a través del enfoque del servicio de uso compartido de audiencias** | : Este patrón de integración se puede aprovechar cuando se desee un enriquecimiento adicional de datos y audiencias de terceros en Audience Manager. | : Web/Mobile SDK no es necesario para compartir audiencias de flujo continuo y por lotes con Target, pero sí para habilitar la evaluación de segmentos perimetrales en tiempo real. <br>- Si utiliza AT.js, solo se admite la integración de perfiles con el área de nombres de identidad de ECID. <br>: para las búsquedas de área de nombres de identidad personalizadas en Edge, se requiere la implementación de la API de Web SDK/Edge, y cada identidad debe establecerse como identidad en el mapa de identidad. <br>: se debe aprovisionar la proyección de audiencia mediante el servicio de uso compartido de audiencias. <br>- La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform. <br>: solo las audiencias de la zona protegida de producción predeterminada admiten el servicio principal de uso compartido de audiencias. |

## Uso compartido de audiencias en tiempo real, por flujo y por lotes en Adobe Target

Arquitectura

![Arquitectura de referencia para el modelo Web Personalization en línea/sin conexión](assets/RTCDP+Target.png)

Detalle de secuencia

![Arquitectura de referencia para el modelo Web Personalization en línea/sin conexión](assets/RTCDP+Target_flow.png)

Vista general de la arquitectura

![Arquitectura de referencia para el modelo Web Personalization en línea/sin conexión](assets/personalization_with_apps.png)

## Documentación relacionada

### Documentación del SDK

* [Documentación de Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es)
* [Documentación de etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
* [Documentación del servicio de Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es)

### Documentación de la segmentación

* [Resumen de segmentación de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=es)
* [Segmentación en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=es)
* [Segmentación de streaming](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Uso compartido de segmentos de Adobe Analytics mediante Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=es)
* [Configuración de política de combinación](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=es#create-a-merge-policy)

### Tutoriales

* [Personalización de próxima visita con Real-Time CDP y Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=es)
