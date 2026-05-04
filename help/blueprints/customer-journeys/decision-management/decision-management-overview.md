---
title: Modelos de administración de decisiones
description: Ofrezca ofertas personalizadas entre los recorridos de los clientes.
solution: Experience Platform, Journey Optimizer
exl-id: 1bc9335c-5321-4d0c-939e-4f402e2e8f51
TQID: https://experienceleague.adobe.com/FWKq0QzEzCXp8TrfECmhY4E3ocA4zZkTGyHrrKQCOBw
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: df64005d-8f9a-422e-ba4d-c6f6dc3454b4
  - id: fe338112-e2ce-4876-8989-fc4d497613f1
subfeature_v2:
  - id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
  - id: fa683eda-48de-4558-af32-2673edcd44fe
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d00e9f03-e50b-4162-b143-0c0817c937c2
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: a99add31cc9f485db119ca00426798545e6a7316
workflow-type: tm+mt
source-wordcount: 731
ht-degree: 76%

---

# Journey Optimizer: modelos de gestión de decisiones

Consulte la siguiente documentación para [Administración de decisiones](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=es)

Consulte la siguiente documentación para ver las protecciones relacionadas con la gestión de decisiones. [Protecciones de administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails#decision-management.html)

Gestión de decisiones de Adobe es un servicio que se proporciona como parte de Adobe Journey Optimizer. Este modelo describe los casos de uso y las capacidades técnicas de la aplicación, y proporciona una explicación profunda de los diversos componentes y consideraciones sobre arquitectura que componen Gestión de decisiones.

Journey Optimizer se utiliza para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto y en el momento adecuado. Administración de decisiones facilita la personalización con una biblioteca central de ofertas de marketing y un motor de decisión que aplica reglas y restricciones a perfiles en tiempo real creados por Adobe Experience Platform. Esto le permite enviar fácilmente a sus clientes la oferta correcta en el momento adecuado.

La funcionalidad Gestión de decisiones consta de dos componentes principales:

* La biblioteca de ofertas centralizadas, que es la interfaz en la que se crean y se gestionan los distintos elementos que componen las ofertas, y donde definen sus reglas y restricciones.
* El motor de decisión de ofertas, que aprovecha los datos de Adobe Experience Platform y los perfiles del cliente en tiempo real, junto con la biblioteca de ofertas, para seleccionar el momento, los clientes y los canales adecuados a los que se enviarán las ofertas.

<img src="images/offers_overview.png" alt="Gestión de decisiones" style="width:100%; border:1px solid #4a4a4a" />

Gestión de decisiones se puede implementar de una de las dos maneras siguientes: en Edge o a través del hub. Cada uno de estos métodos tiene un conjunto específico de interfaces y protocolos para operar el servicio como se describe en los respectivos modelos a los que se hace referencia a continuación. También pueden obtenerse más detalles en la [documentación de Gestión de decisiones](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html?lang=es).

## Gestión de decisiones en el hub

La primera es a través del hub de Adobe Experience Platform, que es una arquitectura de centro de datos central. La arquitectura de concentrador es más adecuada para las experiencias de los clientes que no exigen una latencia baja y un rendimiento alto, pero sí requieren una vista más completa del perfil del cliente. Algunos ejemplos incluyen decisiones de oferta que se proporcionan para quioscos o experiencias asistidas por agentes, como en centros de llamadas o interacciones personales. Las ofertas que se insertan en correos electrónicos, mensajes SMS o notificaciones push y otras campañas salientes también emplean el enfoque de hub. Para obtener más información sobre Gestión de decisiones en el hub, consulte el modelo [Gestión de decisiones en el hub](decision-management-hub.md).

* La idoneidad de la oferta puede operar con el perfil completo del cliente en tiempo real, incluidos todos los atributos y eventos de experiencia.

### Casos de uso para Gestión de decisiones en el hub

* Ofertas personalizadas en quioscos y en experiencias de tienda.
* Ofertas personalizadas a través de la experiencia asistida por agentes, como centros de llamadas o interacciones de ventas.
* Ofertas incluidas en correos electrónicos, SMS u otras interacciones salientes.
* Ejecución de recorridos en varios canales: coherencia de ofertas en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

### Gestión de decisiones en las consideraciones técnicas del hub

* Acceso completo a Real-Time Customer Profile, lo que incluye las suscripciones a audiencias, atributos y eventos de experiencia.

## Gestión de decisiones en Edge

El segundo método es a través de Experience [!DNL Edge Network], que es una infraestructura distribuida geográficamente a nivel global para ofrecer experiencias rápidas de segundo y milisegundo. La experiencia del consumidor final que ejecuta la infraestructura de Edge más cercana a la ubicación geográfica del consumidor para minimizar la latencia. Gestión de decisiones en Edge está diseñado para ofrecer experiencias de consumidores en tiempo real, como solicitudes de personalización entrantes web o móviles. Para obtener más información sobre Gestión de decisiones en Edge, consulte el modelo [Gestión de decisiones en Edge](decision-management-edge.md).

### Casos de uso para Gestión de decisiones en Edge

* Personalización en línea mediante experiencias entrantes web o móviles.
* Ejecución de recorridos en varios canales: coherencia de ofertas en todos los canales de interacción web, móvil, correo electrónico y otros a través de Adobe Journey Optimizer.

### Gestión de decisiones en las consideraciones técnicas de Edge

* Acceso al perfil de Edge en tiempo real. Solo estarán disponibles en el perfil las audiencias y los atributos de perfil proyectados de Edge.

## Documentación relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=es)
* [Gestión de decisiones de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=es)
* [Descripción del producto de Adobe Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descripción del producto de Adobe Decision Management](https://helpx.adobe.com/es/legal/product-descriptions/offer-decisioning-app-service.html)
