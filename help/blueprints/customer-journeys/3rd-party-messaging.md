---
title: 'Journey Optimizer: modelo de mensajería de terceros'
description: Muestra cómo se puede utilizar Adobe Journey Optimizer con sistemas de mensajería de terceros para organizar y enviar comunicaciones personalizadas.
solution: Journey Optimizer
exl-id: 3a14fc06-6d9c-4cd8-bc5c-f38e253d53ce
source-git-commit: 75a0f2a77f39a4320dc4c4b0db918879be099dd3
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 97%

---

# Modelo de mensajería de terceros

Muestra cómo se puede utilizar Adobe Journey Optimizer con sistemas de mensajería de terceros para organizar y enviar comunicaciones personalizadas.

<br>

## Arquitectura

<img src="assets/3rd-party-messaging-architecture.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Prerrequisitos

Adobe Experience Platform

* Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar las fuentes de datos de Journey Optimizer
* Para los esquemas basados en clases de eventos de experiencia, agregue el grupo de campos &#39;ID de evento de orquestación&#39; cuando desee que se active un evento que no sea un evento basado en reglas
* Para los esquemas basados en clases de perfil individual, agregue el grupo de campos &#39;Detalles de prueba de perfil&#39; para poder cargar perfiles de prueba para utilizarlos con Journey Optimizer

Aplicación de mensajería de terceros

* Debe admitir llamadas de API de REST para enviar cargas transaccionales

<br>

## Guardas

[Vínculo del producto de guardas de Journey Optimizer](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=es)

[Protecciones y guía de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html?lang=es)


## Pasos de implementación

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=es) según los datos ofrecidos por los clientes en Experience Platform.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) en Experience Platform para la ingesta.
1. [Añadir etiquetas de uso de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=es) al conjunto de datos de Experience Platform para la gobernanza.
1. [Crear políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=es) que refuercen la gobernanza en los destinos.

#### Perfil/identidad

1. [Crear áreas de nombres específicas para los clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Añadir identidades a los esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Configurar políticas de fusión](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=es) para diferenciar las vistas de [!UICONTROL Real-Time Customer Profile] (opcional).
1. Crear segmentos para el uso de Journey.

#### Orígenes/destinos

1. [Incorporar datos en Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=es) mediante API de flujo y conectores de origen.

### Journey Optimizer

1. Configure la fuente de datos de Experience Platform y determine qué campos deben almacenarse en caché como parte de los datos profileStreaming utilizados para iniciar un recorrido del cliente. Primero debe configurarse en Journey Optimizer para obtener un ID de organización. Este ID de organización debe entregarse al desarrollador para usarse con la ingesta
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
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
* [Documentación del SDK móvil de Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
* [Documentación de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es)
* [Descripción del producto Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
