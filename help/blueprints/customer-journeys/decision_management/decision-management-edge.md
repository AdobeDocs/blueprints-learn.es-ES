---
title: Modelo de Gestión de decisiones en Edge
description: Ofrezca ofertas personalizadas a los consumidores en todos los canales, incluidas las experiencias web y móviles en tiempo real.
solution: Experience Platform, Journey Optimizer
exl-id: 31e5f624-5578-49e1-ab92-5cabd596a632
source-git-commit: 2960cc95b9b83a3efea7fa247e1adabf310f3ee1
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 95%

---

# Journey Optimizer: Modelo de Gestión de decisiones en Edge

Para obtener más información sobre Gestión de decisiones, consulte la documentación del producto [AQUÍ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=es) y la Información general sobre Gestión de decisiones [AQUÍ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview.html?lang=es)

Gestión de decisiones de Adobe es un servicio que se proporciona como parte de Adobe Journey Optimizer. Este modelo describe los casos de uso y las capacidades técnicas de la aplicación, y proporciona una explicación profunda de los diversos componentes y consideraciones sobre arquitectura que componen Gestión de decisiones.

Gestión de decisiones se puede implementar de una de las dos maneras siguientes. La primera es a través de Adobe Experience Platform Hub, que es una arquitectura de centro de datos único. En el método &quot;hub&quot;, las ofertas se ejecutan, personalizan y entregan con una latencia de un segundo. Por lo tanto, la arquitectura del hub es la más adecuada para la experiencia del cliente que no requiere latencia de subsegundo. Algunos ejemplos incluyen tomas de decisiones sobre ofertas que se proporcionan para los quioscos o experiencias asistidas por agentes, como en los centros de llamadas o en las interacciones personales.

El segundo enfoque es a través de la red Experience Edge, que es una infraestructura distribuida globalmente y ubicada geográficamente para ofrecer experiencias rápidas de subsegundo y milisegundo. La experiencia del consumidor final que ejecuta la infraestructura de Edge más cercana a la ubicación geográfica del consumidor para minimizar la latencia. Gestión de decisiones en Edge está diseñado para ofrecer experiencias de consumo en tiempo real. Estas incluyen experiencias como solicitudes de personalización de entrada web o móvil.

Este modelo abarcará los aspectos específicos de Gestión de decisiones en Edge.

Para obtener más información sobre Gestión de decisiones en el hub, consulte el modelo [Gestión de decisiones en el hub](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-hub.html?lang=es).

## Casos de uso para Gestión de decisiones en Edge

* Casos de uso de streaming en los que la latencia de contexto de perfil es estricta por debajo de los 15 minutos de latencia y la ejecución de la administración de decisiones es de subsegundo.
* Personalización en línea mediante experiencias entrantes web o móviles.
* Ejecución de recorridos en varios canales: coherencia de ofertas en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

<br>

## Arquitectura

<img src="../assets/offers_edge.svg" alt="Arquitectura de referencia Gestión de decisiones en el modelo de Edge" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Patrones de integración

| Integración | Descripción |
| :-- | :--- |
| [Gestión de decisiones con Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html?lang=es) | Gestión de decisiones se puede integrar con Adobe Target de modo que las ofertas se puedan probar y entregar como experiencias de Target. |

## Prerrequisitos

Adobe Experience Platform

* Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar las fuentes de datos de Journey Optimizer
* Para los esquemas basados en clases de eventos de experiencia, agregue el grupo de campos &#39;ID de evento de orquestación&#39; cuando desee que se active un evento que no sea un evento basado en reglas
* Para los esquemas basados en clases de perfil individual, agregue el grupo de campos &#39;Detalles de prueba de perfil&#39; para poder cargar perfiles de prueba para utilizarlos con Journey Optimizer

<br>

## Guardas

* Para obtener más información sobre las guardas de Journey Optimizer, consulte las [Guardas de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=es).

* Si quiere información sobre las guardas de Gestión de decisiones, consulte la siguiente [Descripción del producto de Gestión de decisiones](https://helpx.adobe.com/es/legal/product-descriptions/offer-decisioning-app-service.html).

[Protecciones y guía de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)


## Patrones de implementación

* Utilice el SDK web o móvil para la implementación en sitios web y aplicaciones móviles a fin de implementar Gestión de decisiones donde se implementó el SDK.
   * [Modelo de SDK web/móvil](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/websdk.html?lang=es)
   * [SDK web](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/offer-decisioning/offer-decisioning-overview.html?lang=es)
   * [SDK móvil](https://aep-sdks.gitbook.io/docs/)

O

* Para que un servidor de API e implementación basada en servidor utilicen la API de servicio de Edge Network para la implementación de Gestión de decisiones de servidor a servidor directo.
   * [API del servidor de Edge Network](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/deliver-offers.html?lang=es)

<br>

## Pasos de implementación

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=es) según los datos ofrecidos por los clientes en Experience Platform.
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

1. [Incorporar datos en Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) mediante API de flujo y conectores de origen.

## Documentación relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=es)
* [Gestión de decisiones de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=es)
* [Descripción del producto Adobe Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descripción del producto de Gestión de decisiones de Adobe](https://helpx.adobe.com/es/legal/product-descriptions/offer-decisioning-app-service.html)
