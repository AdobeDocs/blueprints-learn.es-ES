---
title: offer decisioning en el concentrador
description: Entregue ofertas personalizadas a los consumidores en todos los canales, incluidos los quioscos, las experiencias asistidas por el agente, y en correos electrónicos y otros envíos salientes.
solution: Experience Platform, Journey Optimizer
exl-id: 5a386e18-bbac-4216-a35f-0a5016785e4a
source-git-commit: 7f566536c4ff5a6af321d60058ad67c13c28bf64
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 28%

---

# Journey Optimizer: Offer decisioning en el concentrador

Para obtener más información sobre la gestión de decisiones, consulte la documentación del producto [AQUÍ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html) y el Offer decisioning [AQUÍ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-overview.html)

Administración de decisiones de Adobe es un servicio que se proporciona como parte de Adobe Journey Optimizer. Este modelo describe los casos de uso y las capacidades técnicas de la aplicación y proporciona una explicación profunda de los diversos componentes y consideraciones arquitectónicos que componen el Offer decisioning.

Journey Optimizer se utiliza para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto y en el momento adecuado. El offer decisioning facilita la personalización con una biblioteca central de ofertas de marketing y un motor de decisión que aplica reglas y restricciones a perfiles enriquecidos y en tiempo real creados por Adobe Experience Platform para ayudarle a enviar a sus clientes la oferta correcta en el momento adecuado.

La Administración de decisiones se puede implementar de una de las dos maneras siguientes. La primera es a través del concentrador de Adobe Experience Platform, que es una arquitectura de centro de datos central. En el enfoque &quot;hub&quot;, las ofertas se ejecutan, personalizan y entregan en >500 ms de latencia. Por lo tanto, la arquitectura de concentrador es la más adecuada para las experiencias de los clientes que no requieren latencia de subsegundo, los ejemplos incluyen decisiones de oferta que se proporcionan para los quioscos o experiencias asistidas por el agente, como en los centros de llamadas o en las interacciones personales. Las ofertas que se insertan en correos electrónicos y en campañas salientes también utilizan el método de concentrador.

El segundo método es a través de la red Experience Edge, que es una infraestructura distribuida globalmente y ubicada geográficamente para ofrecer experiencias rápidas de subsegundo y milisegundo. La experiencia del consumidor final que ejecuta la infraestructura perimetral más cercana a la ubicación geográfica del consumidor para minimizar la latencia. La administración de decisiones en Edge está diseñada para ofrecer experiencias de consumidores en tiempo real, como solicitudes de personalización entrantes web o móviles.

Este modelo abarcará los aspectos específicos de la gestión de decisiones en el centro.

Para obtener más información sobre la administración de decisiones en Edge, consulte la [Administración de decisiones en el perímetro](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-edge.html) modelo.

## Casos de uso para la gestión de decisiones en el centro

* Ofertas personalizadas en quioscos y en experiencias de tienda.
* Ofertas personalizadas a través de la experiencia asistida por el agente, como centros de llamadas o interacciones de ventas.
* Ofertas incluidas en correos electrónicos, SMS u otras interacciones salientes.
* Ejecución de recorridos en varios canales : ofrece coherencia en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

<br>

## Arquitectura

<img src="../assets/offers_hub.svg" alt="Offer decisioning de arquitectura de referencia en el modelo de borde" style="width:100%; border:1px solid #4a4a4a" />

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

* Para obtener más información sobre las protecciones de Journey Optimizer, consulte lo siguiente [Journey Optimizer Guardrade](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html).
* Para las protecciones de Offer decisioning, consulte lo siguiente [Descripción del producto offer decisioning](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html).


### Guardas de ingesta de datos

<img src="../assets/aep-data-ingestion-details-latency.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:80%; border:1px solid #4a4a4a" />

<br>

### Guardas de activación

<img src="../assets/ajo-activation-details-latency.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:80%; border:1px solid #4a4a4a" />

<br>

## Patrones de implementación

* Implementado en canales de correo electrónico, SMS y de salida mediante integración directa con [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/offers-e2e.html).
* Para la implementación basada en API de servidor de Offer decisioning, aproveche la variable [API de decisiones](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/decisioning-vs-edge-apis.html).
* Para la implementación de la toma de decisiones por lotes para entregar ofertas de forma masiva a una aplicación de entrega de mensajes, utilice el [API de decisiones por lotes](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/batch-decisioning-api.html).
* Para experiencias en tiempo real basadas en Edge, utilice el SDK web/móvil o la API de Edge Decisioning como se describe en la sección [offer decisioning en el modelo de Edge](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-edge.html).
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
* [Descripción del producto de Adobe Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descripción del producto del Offer decisioning de Adobe](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
