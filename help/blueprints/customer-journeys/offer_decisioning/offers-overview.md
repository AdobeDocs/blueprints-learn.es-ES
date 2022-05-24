---
title: Información general sobre offers decisioning
description: Ofrezca ofertas personalizadas entre los recorridos de los clientes.
solution: Experience Platform, Journey Optimizer
exl-id: f6271802-faab-4ffc-92d6-4c4d7d423ed4
source-git-commit: 7dcbf86b362350312a86445bbe7a020f5ccd1752
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 48%

---

# Journey Optimizer: Información general del Offer decisioning

Para obtener más información sobre Gestión de decisiones, consulte la documentación del producto [AQUÍ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=es)

Gestión de decisiones de Adobe es un servicio que se proporciona como parte de Adobe Journey Optimizer. Este modelo describe los casos de uso y las capacidades técnicas de la aplicación, y proporciona una explicación profunda de los diversos componentes y consideraciones sobre arquitectura que componen Offer Decisioning.

Journey Optimizer se utiliza para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto y en el momento adecuado. El offer decisioning facilita la personalización con una biblioteca central de ofertas de marketing y un motor de decisión que aplica reglas y restricciones a perfiles enriquecidos y en tiempo real creados por Adobe Experience Platform para ayudarle a enviar a sus clientes la oferta correcta en el momento adecuado.

La capacidad de gestión de decisiones consta de dos componentes principales:

* Biblioteca de ofertas centralizada, que es la interfaz en la que se crean y administran los distintos elementos que componen las ofertas, y se definen sus reglas y restricciones.
* El motor de decisión de ofertas que aprovecha los datos de Adobe Experience Platform y los perfiles del cliente en tiempo real, junto con la biblioteca de ofertas, para seleccionar el momento, los clientes y los canales adecuados a los que se enviarán las ofertas.

<img src="../assets/offers_overview.png" alt="Offer Decisioning" style="width:100%; border:1px solid #4a4a4a" />

La Administración de decisiones se puede implementar de una de las dos maneras siguientes, en el perímetro o a través del concentrador. Cada uno de estos métodos tiene un conjunto específico de interfaces y protocolos para operar el servicio como se describe en los respectivos modelos a los que se hace referencia a continuación. También pueden obtenerse más detalles en la documentación de gestión de decisiones [AQUÍ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html).

## Gestión de decisiones en el centro

La primera es a través del hub de Adobe Experience Platform, que es una arquitectura de centro de datos central. En el enfoque «hub», las ofertas se ejecutan, personalizan y entregan con una latencia de más de 500 ms. Por lo tanto, la arquitectura del hub es la más adecuada para las experiencias de los clientes que no requieren latencia de subsegundo. Algunos ejemplos incluyen tomas de decisiones sobre ofertas que se proporcionan para los quioscos o experiencias asistidas por agentes, como en los centros de llamadas o en las interacciones personales. Las ofertas que se insertan en correos electrónicos, mensajes SMS o notificaciones push y otras campañas salientes también se impulsan mediante el enfoque de concentrador. Para obtener más información sobre Gestión de decisiones en el hub, consulte el modelo [Gestión de decisiones en el hub](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-hub.html?lang=es).

* La idoneidad de la oferta puede funcionar con el perfil completo del cliente en tiempo real, incluidos todos los atributos y eventos de experiencia

### Casos de uso para la gestión de decisiones en el centro

* Ofertas personalizadas en quioscos y en experiencias de tienda.
* Ofertas personalizadas a través de la experiencia asistida por agentes, como centros de llamadas o interacciones de ventas.
* Ofertas incluidas en correos electrónicos, SMS u otras interacciones salientes.
* Ejecución de recorridos en varios canales: coherencia de ofertas en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

### Gestión de decisiones sobre las consideraciones técnicas del centro

* Solicitudes por segundo = 2000.
* Latencia de respuesta &lt; 500 ms.
* Acceso a perfiles de cliente en tiempo real completos que incluyen suscripciones de audiencia, atributos y eventos de experiencia.

## Administración de decisiones en el perímetro

El segundo enfoque es a través de la red Experience Edge, que es una infraestructura distribuida globalmente y ubicada geográficamente para ofrecer experiencias rápidas de subsegundo y milisegundo. La experiencia del consumidor final que ejecuta la infraestructura de Edge más cercana a la ubicación geográfica del consumidor para minimizar la latencia. Gestión de decisiones en Edge está diseñado para ofrecer experiencias de consumidores en tiempo real, como solicitudes de personalización entrantes web o móviles. Para obtener más información sobre Gestión de decisiones en Edge, consulte el modelo [Gestión de decisiones en Edge](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-edge.html?lang=es).

### Casos de uso para la gestión de decisiones en Edge

* Personalización en línea mediante experiencias entrantes web o móviles.
* Ejecución de recorridos en varios canales: coherencia de ofertas en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

### Gestión de decisiones por consideraciones técnicas avanzadas

* Solicitudes por segundo = 5000.
* Latencia de respuesta &lt; 250 ms.
* Acceso al perfil de Edge en tiempo real. Solo estarán disponibles en el perfil las audiencias y los atributos de perfil proyectados de Edge.
* Si la personalización es necesaria en las experiencias por primera vez, hub será ideal, ya que el perfil completo está disponible. El perfil de Edge debe sincronizarse desde el hub por primera vez en la experiencia de Edge. Por lo tanto, la primera experiencia de edge no incluirá datos de perfil cargados previamente en el centro.

## Documentación relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=es)
* [Gestión de decisiones de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Descripción del producto Adobe Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descripción del producto del Offer Decisioning de Adobe](https://helpx.adobe.com/es/legal/product-descriptions/offer-decisioning-app-service.html)
