---
title: Modelos de administración de decisiones
description: Ofrezca ofertas personalizadas entre los recorridos de los clientes.
solution: Experience Platform, Journey Optimizer
exl-id: 1bc9335c-5321-4d0c-939e-4f402e2e8f51
source-git-commit: b18d491fdefc57762932d1570401b5437bf97c76
workflow-type: ht
source-wordcount: '757'
ht-degree: 100%

---

# Journey Optimizer: Modelos de Gestión de decisiones

Para obtener más información sobre Gestión de decisiones, consulte la [documentación del producto](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=es)

Gestión de decisiones de Adobe es un servicio que se proporciona como parte de Adobe Journey Optimizer. Este modelo describe los casos de uso y las capacidades técnicas de la aplicación, y proporciona una explicación profunda de los diversos componentes y consideraciones sobre arquitectura que componen Gestión de decisiones.

Journey Optimizer se utiliza para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto y en el momento adecuado. Gestión de decisiones facilita la personalización con una biblioteca principal de ofertas de marketing y un motor de decisión que aplica reglas y restricciones a perfiles enriquecidos y en tiempo real creados por Adobe Experience Platform para ayudarle a enviar a sus clientes la oferta correcta en el momento adecuado.

La funcionalidad Gestión de decisiones consta de dos componentes principales:

* La biblioteca de ofertas centralizadas, que es la interfaz en la que se crean y se gestionan los distintos elementos que componen las ofertas, y donde definen sus reglas y restricciones.
* El motor de decisión de ofertas, que aprovecha los datos de Adobe Experience Platform y los perfiles del cliente en tiempo real, junto con la biblioteca de ofertas, para seleccionar el momento, los clientes y los canales adecuados a los que se enviarán las ofertas.

<img src="../assets/offers_overview.png" alt="Gestión de decisiones" style="width:100%; border:1px solid #4a4a4a" />

Gestión de decisiones se puede implementar de una de las dos maneras siguientes: en Edge o a través del hub. Cada uno de estos métodos tiene un conjunto específico de interfaces y protocolos para operar el servicio como se describe en los respectivos modelos a los que se hace referencia a continuación. También pueden obtenerse más detalles en la [documentación de Gestión de decisiones](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html?lang=es).

## Gestión de decisiones en el hub

La primera es a través del hub de Adobe Experience Platform, que es una arquitectura de centro de datos central. En el enfoque «hub», las ofertas se ejecutan, personalizan y entregan con una latencia de más de 500 ms. Por lo tanto, la arquitectura del hub es la más adecuada para las experiencias de los clientes que no requieren latencia de subsegundo. Algunos ejemplos incluyen tomas de decisiones sobre ofertas que se proporcionan para los quioscos o experiencias asistidas por agentes, como en los centros de llamadas o en las interacciones personales. Las ofertas que se insertan en correos electrónicos, mensajes SMS o notificaciones push y otras campañas salientes también emplean el enfoque de hub. Para obtener más información sobre Gestión de decisiones en el hub, consulte el modelo [Gestión de decisiones en el hub](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-hub.html?lang=es).

* La idoneidad de la oferta puede operar con el perfil completo del cliente en tiempo real, incluidos todos los atributos y eventos de experiencia.

### Casos de uso para Gestión de decisiones en el hub

* Ofertas personalizadas en quioscos y en experiencias de tienda.
* Ofertas personalizadas a través de la experiencia asistida por agentes, como centros de llamadas o interacciones de ventas.
* Ofertas incluidas en correos electrónicos, SMS u otras interacciones salientes.
* Ejecución de recorridos en varios canales: coherencia de ofertas en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

### Gestión de decisiones en las consideraciones técnicas del hub

* Solicitudes por segundo =2000.
* Latencia de respuesta &lt;500ms.
* Acceso completo a Real-Time Customer Profile, lo que incluye las suscripciones a audiencias, atributos y eventos de experiencia.

## Gestión de decisiones en Edge

El segundo enfoque es a través de la red Experience Edge, que es una infraestructura distribuida globalmente y ubicada geográficamente para ofrecer experiencias rápidas de subsegundo y milisegundo. La experiencia del consumidor final que ejecuta la infraestructura de Edge más cercana a la ubicación geográfica del consumidor para minimizar la latencia. Gestión de decisiones en Edge está diseñado para ofrecer experiencias de consumidores en tiempo real, como solicitudes de personalización entrantes web o móviles. Para obtener más información sobre Gestión de decisiones en Edge, consulte el modelo [Gestión de decisiones en Edge](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-edge.html?lang=es).

### Casos de uso para Gestión de decisiones en Edge

* Personalización en línea mediante experiencias entrantes web o móviles.
* Ejecución de recorridos en varios canales: coherencia de ofertas en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

### Gestión de decisiones en las consideraciones técnicas de Edge

* Solicitudes por segundo =5000.
* Latencia de respuesta &lt;250 ms.
* Acceso al perfil de Edge en tiempo real. Solo estarán disponibles en el perfil las audiencias y los atributos de perfil proyectados de Edge.
* Si se requiere personalización para la primera experiencia, hub es ideal, ya que el perfil completo está disponible. El perfil de Edge debe sincronizarse desde el hub para la primera experiencia en Edge. Por lo tanto, la primera experiencia en Edge no incluirá datos de perfil cargados previamente en el hub.

## Documentación relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=es)
* [Gestión de decisiones de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=es)
* [Descripción del producto Adobe Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descripción del producto de Gestión de decisiones de Adobe](https://helpx.adobe.com/es/legal/product-descriptions/offer-decisioning-app-service.html)
