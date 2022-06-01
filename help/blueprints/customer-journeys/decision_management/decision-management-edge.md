---
title: Administración de decisiones en el perímetro
description: Ofrezca ofertas personalizadas a los consumidores en todos los canales, incluidas las experiencias web y móviles en tiempo real.
solution: Experience Platform, Journey Optimizer
exl-id: 31e5f624-5578-49e1-ab92-5cabd596a632
source-git-commit: 5b2f7531cc05178127fb08d3fdafcbce70192ecd
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 69%

---

# Journey Optimizer: Administración de decisiones en Edge

Para obtener más información sobre la gestión de decisiones, consulte la documentación del producto [AQUÍ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=es) y la información general sobre la gestión de decisiones [AQUÍ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/decision-management-overview.html)

Gestión de decisiones de Adobe es un servicio que se proporciona como parte de Adobe Journey Optimizer. Este modelo describe los casos de uso y las capacidades técnicas de la aplicación y proporciona una profunda explicación de los diversos componentes y consideraciones arquitectónicos que componen la gestión de decisiones.

Gestión de decisiones se puede implementar de una de las dos maneras siguientes. La primera es a través de Adobe Experience Platform Hub, que es una arquitectura de centro de datos único. En el método «hub», las ofertas se ejecutan, personalizan y entregan con una latencia de un segundo. Por lo tanto, la arquitectura del hub es la más adecuada para la experiencia del cliente que no requiere latencia de subsegundo. Algunos ejemplos incluyen tomas de decisiones sobre ofertas que se proporcionan para los quioscos o experiencias asistidas por agentes, como en los centros de llamadas o en las interacciones personales.

El segundo enfoque es a través de la red Experience Edge, que es una infraestructura distribuida globalmente y ubicada geográficamente para ofrecer experiencias rápidas de subsegundo y milisegundo. La experiencia del consumidor final que ejecuta la infraestructura de Edge más cercana a la ubicación geográfica del consumidor para minimizar la latencia. Gestión de decisiones en Edge está diseñado para ofrecer experiencias de consumo en tiempo real. Estas incluyen experiencias como solicitudes de personalización de entrada web o móvil.

Este modelo abarcará los aspectos específicos de Gestión de decisiones en Edge.

Para obtener más información sobre Gestión de decisiones en el hub, consulte el modelo [Gestión de decisiones en el hub](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/decision-management-hub.html).

## Casos de uso para la gestión de decisiones en Edge

* Personalización en línea mediante experiencias entrantes web o móviles.
* Ejecución de recorridos en varios canales: coherencia de ofertas en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

<br>

## Arquitectura

<img src="../assets/offers_edge.svg" alt="Arquitectura de referencia Administración de decisiones en el modelo edge" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Patrones de integración

| Integración | Descripción |
| :-- | :--- |
| [Administración de decisiones con Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html?lang=es) | La Administración de decisiones se puede integrar con Adobe Target, de modo que las ofertas se puedan probar y entregar como experiencias de Target. |

## Prerrequisitos

Adobe Experience Platform

* Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar las fuentes de datos de Journey Optimizer
* Para los esquemas basados en clases de eventos de experiencia, agregue el grupo de campos &#39;ID de evento de orquestación&#39; cuando desee que se active un evento que no sea un evento basado en reglas
* Para los esquemas basados en clases de perfil individual, agregue el grupo de campos &#39;Detalles de prueba de perfil&#39; para poder cargar perfiles de prueba para utilizarlos con Journey Optimizer

<br>

## Guardas

* Para obtener más información sobre las protecciones de Journey Optimizer, consulte las [Protecciones de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=es).
* Para las protecciones de la gestión de decisiones, consulte lo siguiente [Descripción del producto de Administración de decisiones](https://helpx.adobe.com/es/legal/product-descriptions/offer-decisioning-app-service.html).
* Solicitudes por segundo = 5000.
* Latencia de respuesta &lt; 250 ms.
* Acceso al perfil de Edge en tiempo real. Solo estarán disponibles en el perfil las audiencias y los atributos de perfil proyectados de Edge.
* Si la personalización es necesaria en las experiencias por primera vez, hub será ideal, ya que el perfil completo está disponible. El perfil de Edge debe sincronizarse desde el hub por primera vez en la experiencia de Edge. Por lo tanto, la primera experiencia de edge no incluirá datos de perfil cargados previamente en el centro.

### Guardas de ingesta de datos

<img src="../assets/aep-data-ingestion-details-latency.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:80%; border:1px solid #4a4a4a" />

<br>

### Guardas de activación

<img src="../assets/ajo-activation-details-latency.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:80%; border:1px solid #4a4a4a" />

<br>

## Patrones de implementación

* Utilice el SDK web o móvil para la implementación en sitios web y aplicaciones móviles a fin de implementar la Administración de decisiones donde se haya implementado el SDK.
   * [Modelo de SDK web/móvil](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/data-ingestion/websdk.html?lang=es)
   * [WebSDK](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/offer-decisioning/offer-decisioning-overview.html?lang=es)
   * [MobileSDK](https://aep-sdks.gitbook.io/docs/)

O

* Para una implementación basada en servidor y servidor de API, utilice la API de servicio de red perimetral para la implementación de servidor a servidor directa de la Administración de decisiones.
   * [API del servidor de red de Edge](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/deliver-offers.html?lang=es)

<br>

## Pasos de implementación

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) según los datos ofrecidos por los clientes en Experience Platform.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) en Experience Platform para la ingesta.
1. [Añadir etiquetas de uso de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=es) al conjunto de datos de Experience Platform para la gobernanza.
1. [Crear políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=es) que refuercen la gobernanza en los destinos.

#### Perfil/identidad

1. [Crear áreas de nombres específicas para los clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Añadir identidades a los esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Configurar políticas de fusión](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=es) para diferenciar las vistas de [!UICONTROL Real-time Customer Profile] (opcional).
1. Crear segmentos para el uso de Journey.

#### Origen/destino

1. [Incorporar datos en Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) mediante API de flujo y conectores de origen.

## Documentación relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=es)
* [Gestión de decisiones de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Descripción del producto Adobe Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descripción del producto de Administración de decisiones de Adobe](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
