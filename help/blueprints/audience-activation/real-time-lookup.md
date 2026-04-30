---
title: Acceso al perfil de Edge en tiempo real para Personalization web y móvil
description: '[!UICONTROL Acceso al Perfil del cliente en tiempo real] en el perímetro para proporcionar contexto para la personalización móvil y web en tiempo real.'
solution: Real-Time Customer Data Platform, Data Collection
kt: 719
exl-id: 61b81d00-c4bd-41b2-8161-683814947b56
TQID: https://experienceleague.adobe.com/H59c3UBbNCQFs3H0VL5iVDKKZ5D3CFt4ri2RVwNlq7s
product_v2:
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: ba929a52-9339-4154-9487-317dc875a3c7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 631
ht-degree: 8%

---

# Acceso al perfil de Edge en tiempo real para Personalization web y móvil

>[!TIP]
>Este modelo también está disponible como [patrón de caso de uso](/help/blueprints/use-case-patterns/personalization/edge-profile-access.md) en Personalization.

El modelo de acceso a perfiles de Edge en tiempo real para Personalization web y móvil muestra cómo las aplicaciones web y móviles pueden acceder al [!UICONTROL Perfil del cliente en tiempo real] de Adobe Experience Platform en el límite para una personalización de alto rendimiento y baja latencia.

Las aplicaciones pueden acceder a los atributos y audiencias de perfil en tiempo real en el perímetro de con una latencia de milisegundos. Se puede acceder en tiempo real a los atributos, las suscripciones a audiencias y las funciones impulsadas por modelos almacenados en el perfil como atributos para la personalización de la misma página y de la siguiente página en canales web y móviles.

Con esta capacidad, puede ofrecer experiencias altamente personalizadas en sus sitios web y aplicaciones móviles en función del Perfil del cliente en tiempo real, incluidas audiencias derivadas de comportamientos en tiempo real, atributos introducidos en el Perfil del cliente en tiempo real y perspectivas calculadas.

>[!NOTE]
>
>El acceso al perfil de Edge está diseñado específicamente para casos de uso de alto rendimiento y baja latencia, como la personalización de entrada web/móvil y la toma de decisiones de oferta en tiempo real. Para escenarios de menor rendimiento, como soporte asistido por el agente o interacciones de ventas, la API de búsqueda de perfiles de concentrador es más apropiada. Consulte el [Modelo de acceso a perfiles en tiempo real para escenarios de soporte y ventas](customer-activity.md) para obtener acceso a perfiles basados en concentradores.

## Aplicaciones

* Real-Time Customer Data Platform
* Recopilación de datos de Adobe Experience Platform (SDK web/SDK móvil)
* API de servidor de Edge Network

## Casos de uso

* Personalización en tiempo real en canales web y móviles para experiencias de cliente conocidas
* Personalización de la misma página y de la siguiente página basada en atributos y audiencias de perfil en tiempo real
* Personalización de contenido y ofertas basada en perfiles de clientes, incluidos datos de comportamiento en tiempo real, atributos y perspectivas calculadas
* Integración con motores de personalización, sistemas de administración de contenido y aplicaciones externas para la toma de decisiones en tiempo real
* Pruebas y optimización de contenido con contexto de perfil en tiempo real

## Diagrama de arquitectura

<img src="assets/real-time-edge-lookup.svg" alt="Arquitectura de referencia para el acceso a perfiles de Edge para Personalization web y móvil" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## Guardas

* [Protecciones para [!UICONTROL datos del perfil del cliente en tiempo real]](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Protecciones de Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* Los perfiles de Edge tienen un tiempo de vida (TTL) de 14 días. Si un usuario no ha estado activo en el perímetro de durante 14 días, el perfil de Edge puede caducar y debe recuperarse del concentrador, lo que puede afectar a la personalización de la primera página.
* La personalización de Edge admite la evaluación de pertenencia a audiencias en tiempo real para audiencias que cumplen los criterios de segmentación de Edge. Las audiencias por lotes y de streaming desde el concentrador también están disponibles en el perímetro de con la configuración adecuada.

## Documentación relacionada

### Configuraciones de destino

* [Conexión personalizada de Personalization](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/personalization/custom-personalization) - Guía de implementación principal
* [Información general sobre destinos Personalization](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/personalization/overview)
* [Activación de audiencias en destinos de personalización de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)
* [Búsqueda de atributos de perfil en Edge en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-edge-profile-lookup)

### Documentación del SDK

* [Documentación de Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=es)
* [Documentación de Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)
* [Documentación de la API de Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es)
* [Documentación de etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
* [Respuestas de comandos en Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html?lang=es)

### Documentación de perfil y segmentación

* [Documentación de [!UICONTROL Perfil del cliente en tiempo real]](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=es)
* [Protecciones de perfil](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)

### Tutoriales

* [Personalización de próxima visita con Real-Time CDP y Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=es)
* [Configuración de flujo de datos](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=es)
