---
title: Offer Decisioning
description: Ofrecer ofertas personalizadas a los consumidores a través de canales, incluidos quioscos y experiencias asistidas por agentes.
solution: Experience Platform, Journey Optimizer
source-git-commit: 5309a5ce986ebf238884df2aac38eb175f3dda11
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 39%

---

# Journey Optimizer: Offer decisioning en el borde

Administración de decisiones de Adobe es un servicio que se proporciona como parte de Adobe Journey Optimizer. Este modelo describe los casos de uso y las capacidades técnicas de la aplicación y proporciona una explicación profunda de los diversos componentes y consideraciones arquitectónicos que componen el Offer decisioning.

La Administración de decisiones se puede implementar de una de las dos maneras siguientes. La primera es a través de Adobe Experience Platform Hub, que es una arquitectura de centro de datos única. En el método &quot;hub&quot;, las ofertas se ejecutan, personalizan y entregan en segunda latencia. Por lo tanto, la arquitectura de concentrador es la más adecuada para la experiencia del cliente que no requiere latencia de subsegundo, los ejemplos incluyen decisiones de oferta que se proporcionan para quioscos o experiencias asistidas por el agente, como en centros de llamadas o en interacciones personales.

El segundo método es a través de la red Experience Edge, que es una infraestructura distribuida globalmente y ubicada geográficamente para ofrecer experiencias rápidas de subsegundo y milisegundo. La experiencia del consumidor final que ejecuta la infraestructura perimetral más cercana a la ubicación geográfica del consumidor para minimizar la latencia. La administración de decisiones en Edge está diseñada para ofrecer experiencias de consumo en tiempo real. Estas incluyen experiencias como solicitudes de personalización de entrada web o móvil.

Este modelo cubrirá los aspectos específicos de Administración de decisiones en Edge.

Para obtener más información sobre la gestión de decisiones, consulte la documentación del producto [AQUÍ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)

## Casos de uso

* Personalización en línea mediante web o móvil.
* Offer decisioning entrante y propuestas de oferta.
* Ejecución de recorridos en varios canales : ofrece coherencia en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

<br>

## Arquitectura

<img src="../assets/offers_edge.svg" alt="Offer decisioning de arquitectura de referencia en el modelo de borde" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Patrones de integración

| Integración | Descripción |
| :-- | :--- |
| [offer decisioning con Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | El offer decisioning se puede integrar con Adobe Target de modo que las ofertas se puedan probar y entregar como experiencias de Target. |

## Prerrequisitos

Adobe Experience Platform

* Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar las fuentes de datos de Journey Optimizer
* Para los esquemas basados en clases de eventos de experiencia, agregue el grupo de campos &#39;ID de evento de orquestación&#39; cuando desee que se active un evento que no sea un evento basado en reglas
* Para los esquemas basados en clases de perfil individual, agregue el grupo de campos &#39;Detalles de prueba de perfil&#39; para poder cargar perfiles de prueba para utilizarlos con Journey Optimizer

<br>

## Guardas

[Vínculo del producto de guardas de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html)


### Guardas de ingesta de datos

<img src="../assets/aep-data-ingestion-details-latency.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:80%; border:1px solid #4a4a4a" />

<br>

### Guardas de activación

<img src="../assets/ajo-activation-details-latency.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:80%; border:1px solid #4a4a4a" />

<br>

## Patrones de implementación

* Utilice el SDK web o móvil para la implementación en sitios web y aplicaciones móviles a fin de implementar el Offer decisioning en el que se implementó el SDK.
   * [WebSDK](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/web-sdk.html)
   * [MobileSDK](https://aep-sdks.gitbook.io/docs/)

O

* Para que un servidor de API e implementación basada en servidor utilice la API de servidor de red perimetral para la implementación de Offer decisioning de servidor a servidor directo. [Vínculo](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/deliver-offers.html)

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

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html)
* [Administración de decisiones de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Descripción del producto de Adobe Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descripción del producto del Offer decisioning de Adobe](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
