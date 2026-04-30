---
title: 'Journey Optimizer: modelo de mensajería de terceros'
description: Muestra cómo se puede utilizar Adobe Journey Optimizer con sistemas de mensajería de terceros para enviar comunicaciones personalizadas.
solution: Journey Optimizer
exl-id: 3a14fc06-6d9c-4cd8-bc5c-f38e253d53ce
TQID: https://experienceleague.adobe.com/dlCwgPnHuoU0IGois2Yy3e9wPELIQsLkStzTBVl5M1M
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
feature_v2:
  - id: a653cc2e-bc85-4353-a306-399e5b247978
  - id: d556b755-390a-43f0-be32-a08cf6236126
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
subfeature_v2:
  - id: af7571a6-3ddb-4c1c-abdf-4d4dde592140
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 577
ht-degree: 61%

---

# Modelo de mensajería de terceros

>[!TIP]
>Este modelo también está disponible como [patrón de caso de uso](/help/blueprints/use-case-patterns/campaign-management-orchestration/third-party-messaging.md) en Administración y orquestación de campañas.

Muestra cómo se puede utilizar Adobe Journey Optimizer con sistemas de mensajería de terceros para enviar comunicaciones personalizadas.

<br>

## Arquitectura

<img src="images/3rd-party-messaging-architecture.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Prerrequisitos

**Adobe Experience Platform**

* Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar las fuentes de datos de Journey Optimizer
* Para los esquemas basados en clases de Experience Event, agregue el grupo de campos ID de evento de orquestación cuando desee tener un evento activado que no sea un evento basado en reglas
* Para esquemas basados en clases de Perfil individual, agregue el grupo de campos Detalles de la prueba de perfil para poder cargar perfiles de prueba para utilizarlos con Journey Optimizer

**Aplicación de mensajería de terceros**

* Debe admitir llamadas de API de REST para enviar cargas transaccionales

<br>

## Guardas

[Vínculo del producto de protecciones Journey Optimizer](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=es)

[Protecciones y guía de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html?lang=es)

<br>

## Pasos de implementación

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=es) en Experience Platform, según los datos proporcionados por el cliente.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) en Experience Platform para la ingesta.
1. [Añadir etiquetas de uso de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=es) al conjunto de datos de Experience Platform para la gobernanza.
1. [Crear políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=es) que refuercen la gobernanza en los destinos.

#### Perfil/identidad

1. [Crear áreas de nombres específicas para los clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Añadir identidades a los esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile).
1. [Configurar políticas de fusión](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=es) para diferenciar las vistas de [!UICONTROL Real-Time Customer Profile] (opcional).
1. Crear segmentos para el uso de Journey.

#### Orígenes/destinos

1. [Incorporar datos en Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=es) mediante API de flujo y conectores de origen.

### Journey Optimizer

1. Configure la fuente de datos de Experience Platform y determine qué campos deben almacenarse en caché como parte de la recorrido
1. Los datos de flujo, utilizados para iniciar un recorrido de cliente, deben configurarse primero para obtener un ID de orquestación. Este ID de orquestación se proporciona al desarrollador para que lo utilice durante la ingesta
1. Configure orígenes externos de datos
1. Configure acciones personalizadas para aplicaciones de terceros

### Configuración push móvil (opcional, ya que terceros pueden recopilar tokens)

1. Implemente el SDK móvil de Experience Platform para recopilar tokens push e información de inicio de sesión con el fin de volver a perfiles de cliente conocidos
1. Aproveche las etiquetas de Adobe y cree una propiedad móvil con la siguiente extensión:
   * Adobe Journey Optimizer
   * Adobe Experience Platform Edge Network
   * Identidad de [!DNL Edge Network]
   * Núcleo móvil
1. Asegúrese de tener un conjunto de datos dedicado para implementaciones de aplicaciones móviles vs. implementaciones web
1. Para obtener más información, siga la [Guía móvil de Adobe Journey Optimizer](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer/)

<br>

## Documentación relacionada

* [Documentación de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Documentación de etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
* [Documentación de Experience Platform Mobile SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
* [Documentación de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es)
* [Descripción del producto de Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
