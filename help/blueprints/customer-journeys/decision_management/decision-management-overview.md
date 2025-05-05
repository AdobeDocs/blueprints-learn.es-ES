---
title: Modelos de administración de decisiones
description: Ofrezca ofertas personalizadas entre los recorridos de los clientes.
solution: Experience Platform, Journey Optimizer
exl-id: 1bc9335c-5321-4d0c-939e-4f402e2e8f51
source-git-commit: e6ac3607ea3909acf921125cc5f8fd44c0b3e0f6
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 86%

---

# Journey Optimizer: Modelos de Gestión de decisiones

Para obtener más información sobre Gestión de decisiones, consulte la [documentación del producto](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=es)

Consulte la siguiente documentación para ver las protecciones relacionadas con la gestión de decisiones. [Protecciones de administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails#decision-management)

Gestión de decisiones de Adobe es un servicio que se proporciona como parte de Adobe Journey Optimizer. Este modelo describe los casos de uso y las capacidades técnicas de la aplicación, y proporciona una explicación profunda de los diversos componentes y consideraciones sobre arquitectura que componen Gestión de decisiones.

Journey Optimizer se utiliza para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto y en el momento adecuado. Gestión de decisiones facilita la personalización con una biblioteca principal de ofertas de marketing y un motor de decisión que aplica reglas y restricciones a perfiles enriquecidos y en tiempo real creados por Adobe Experience Platform para ayudarle a enviar a sus clientes la oferta correcta en el momento adecuado.

La funcionalidad Gestión de decisiones consta de dos componentes principales:

* La biblioteca de ofertas centralizadas, que es la interfaz en la que se crean y se gestionan los distintos elementos que componen las ofertas, y donde definen sus reglas y restricciones.
* El motor de decisión de ofertas, que aprovecha los datos de Adobe Experience Platform y los perfiles del cliente en tiempo real, junto con la biblioteca de ofertas, para seleccionar el momento, los clientes y los canales adecuados a los que se enviarán las ofertas.

<img src="../assets/offers_overview.png" alt="Gestión de decisiones" style="width:100%; border:1px solid #4a4a4a" />

Gestión de decisiones se puede implementar de una de las dos maneras siguientes: en Edge o a través del hub. Cada uno de estos métodos tiene un conjunto específico de interfaces y protocolos para operar el servicio como se describe en los respectivos modelos a los que se hace referencia a continuación. También pueden obtenerse más detalles en la [documentación de Gestión de decisiones](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html?lang=es).

## Gestión de decisiones en el hub

La primera es a través del hub de Adobe Experience Platform, que es una arquitectura de centro de datos central. La arquitectura de concentrador es más adecuada para las experiencias de los clientes que no exigen una latencia baja y un rendimiento alto, pero sí requieren una vista más completa del perfil del cliente. Algunos ejemplos incluyen decisiones de oferta que se proporcionan para quioscos o experiencias asistidas por agentes, como en centros de llamadas o interacciones personales. Las ofertas que se insertan en correos electrónicos, mensajes SMS o notificaciones push y otras campañas salientes también emplean el enfoque de hub. Para obtener más información sobre Gestión de decisiones en el hub, consulte el modelo [Gestión de decisiones en el hub](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-hub.html?lang=es).

* La idoneidad de la oferta puede operar con el perfil completo del cliente en tiempo real, incluidos todos los atributos y eventos de experiencia.

### Casos de uso para Gestión de decisiones en el hub

* Ofertas personalizadas en quioscos y en experiencias de tienda.
* Ofertas personalizadas a través de la experiencia asistida por agentes, como centros de llamadas o interacciones de ventas.
* Ofertas incluidas en correos electrónicos, SMS u otras interacciones salientes.
* Ejecución de recorridos en varios canales: coherencia de ofertas en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

### Gestión de decisiones en las consideraciones técnicas del hub

* Acceso completo a Real-Time Customer Profile, lo que incluye las suscripciones a audiencias, atributos y eventos de experiencia.

## Gestión de decisiones en Edge   

El segundo método es a través de Experience [!DNL Edge Network], que es una infraestructura distribuida geográficamente a nivel global para ofrecer experiencias rápidas de segundo y milisegundo. La experiencia del consumidor final que ejecuta la infraestructura de Edge más cercana a la ubicación geográfica del consumidor para minimizar la latencia. Gestión de decisiones en Edge está diseñado para ofrecer experiencias de consumidores en tiempo real, como solicitudes de personalización entrantes web o móviles. Para obtener más información sobre Gestión de decisiones en Edge, consulte el modelo [Gestión de decisiones en Edge](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-edge.html?lang=es).

### Casos de uso para Gestión de decisiones en Edge

* Personalización en línea mediante experiencias entrantes web o móviles.
* Ejecución de recorridos en varios canales: coherencia de ofertas en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

### Gestión de decisiones en las consideraciones técnicas de Edge

* Acceso al perfil de Edge en tiempo real. Solo estarán disponibles en el perfil las audiencias y los atributos de perfil proyectados de Edge.

## Documentación relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=es)
* [Gestión de decisiones de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=es)
* [Descripción del producto Adobe Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descripción del producto de Gestión de decisiones de Adobe](https://helpx.adobe.com/es/legal/product-descriptions/offer-decisioning-app-service.html)
