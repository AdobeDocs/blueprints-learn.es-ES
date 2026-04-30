---
title: Acceso a perfiles en tiempo real para escenarios de soporte y ventas
description: Búsquedas en [!UICONTROL Real-time Customer Profile] para ofrecer contexto a los agentes de atención al cliente y ventas.
solution: Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c
TQID: https://experienceleague.adobe.com/Ci9pUbGCLQ9uhlQ9l1na7A2NiI9CpCRMLrUSN6lSOnU
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
  - id: b12f6872-9271-4369-85e5-86969a0b99a2
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
  - id: ba929a52-9339-4154-9487-317dc875a3c7
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
  - id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
  - id: ee602049-8a18-43df-9299-a689a025a371
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 368
ht-degree: 54%

---

# Acceso a perfiles en tiempo real para escenarios de soporte y ventas

>[!TIP]
>Este modelo también está disponible como [patrón de caso de uso](/help/blueprints/use-case-patterns/audience-building-activation/real-time-profile-lookup.md) en Generación de audiencias y activación.

El modelo de acceso a perfiles en tiempo real para escenarios de soporte y ventas muestra cómo las aplicaciones externas pueden acceder al [!UICONTROL Perfil del cliente en tiempo real] de Adobe Experience Platform.

Las aplicaciones externas pueden acceder a los perfiles con una solicitud API GET. Los atributos, los eventos, las pertenencias a segmento y todos los recursos por modelo almacenados en el perfil se podrán utilizar posteriormente en las aplicaciones externas que no pertenezcan a Adobe.

Con esta capacidad, es posible hacer aflorar contenido de interés cuando el cliente contacta con el centro de llamadas. El agente de asistencia podrá visualizar el valor de duración del cliente y su tendencia a cancelar o exponerse a campañas de marketing, por ejemplo. Los agentes de ventas también pueden beneficiarse del contexto extra que brinda la información sobre el cliente.

>[!NOTE]
>
>La búsqueda de perfiles en el concentrador no está diseñada para casos de uso de alto rendimiento y baja latencia, como la personalización de entrada web/móvil. La búsqueda de perfiles en el concentrador está diseñada para escenarios de latencia más baja, como soporte asistido por agentes o interacciones de ventas. Para escenarios de baja latencia y alto rendimiento, como personalización web/móvil o Offer Decisioning en tiempo real, se debe aprovechar el perfil de Edge. El perfil de Edge habilita el acceso en tiempo real mediante la [conexión personalizada de Personalization](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/personalization/custom-personalization) de Real-time Customer Data Platform.

## Casos de uso

* Ofrecer un contexto más rico sobre el cliente a las interacciones realizadas por agentes, como las experiencias de asistencia y ventas. Utilizando la búsqueda de perfil en Experience Platform, los agentes pueden recibir más contexto sobre el cliente, tal como compras recientes, interacciones con campañas, tendencias, pertenencia a audiencia y otros atributos y datos que se almacenan en Real-Time Customer Profile.

## Arquitectura

<img src="assets/customer_activity_hub.svg" alt="Arquitectura de referencia para el modelo de centro de actividad del cliente" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## Guardas

* [Protecciones para [!UICONTROL datos del perfil del cliente en tiempo real]](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)

## Documentación relacionada

* [Descripción del producto de Adobe Experience Platform Activation](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform0.html)
* [Documentación de [!UICONTROL Perfil del cliente en tiempo real]](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=es)
* [Protecciones de perfil](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [API de búsqueda de perfil](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
