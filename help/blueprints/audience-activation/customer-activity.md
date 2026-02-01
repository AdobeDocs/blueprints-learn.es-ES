---
title: Acceso a perfiles en tiempo real para escenarios de soporte y ventas
description: Búsquedas en [!UICONTROL Real-time Customer Profile] para ofrecer contexto a los agentes de atención al cliente y ventas.
solution: Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c
source-git-commit: 88a15765c0a998d49c19d9853ad0c44d6e3bfaa1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 65%

---

# Acceso a perfiles en tiempo real para escenarios de soporte y ventas

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

* [Guardas de los datos de [!UICONTROL Real-Time Customer Profile]](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)

## Pasos de implementación

1. [Crear esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=es) para la ingesta de datos.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) para la ingesta de datos.
1. [Configurar las identidades e identidad de áreas de nombres correctas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es) en el esquema para asegurar que los datos ingestados se puedan combinar en un perfil unificado.
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Ingesta de datos](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=es) a Experience Platform.
1. [Configurar políticas de fusión](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=es).
1. Use la API [Entidades para buscar un atributo de perfil](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=es).

## Documentación relacionada

* [Descripción del producto Adobe Experience Platform Activation](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform0.html)
* Documentación de [[!UICONTROL Real-Time Customer Profile]](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=es)
* [Guardas de perfil](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [API de búsqueda de perfiles](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
