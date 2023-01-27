---
title: Modelo de recopilación de datos de reenvío de eventos de Simulador para pruebas múltiples
description: Transmitir datos recopilados por los SDK de Experience Platform a múltiples zonas protegidas mediante el reenvío de eventos
solution: Data Collection
kt: 7202
exl-id: c24a47fe-b3da-4170-9416-74d2b6a18f32
source-git-commit: b18d491fdefc57762932d1570401b5437bf97c76
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Modelo de recopilación de datos de reenvío de eventos de Simulador para pruebas múltiples

El modelo de recopilación de datos de reenvío de eventos de múltiples zonas protegidas muestra cómo se pueden configurar los datos recopilados con los SDK móviles y web de Adobe Experience Platform con el fin de recopilar un solo evento y reenviarlo a múltiples zonas protegidas de AEP. Este modelo es un caso de uso específico que utiliza la función de reenvío de eventos de las etiquetas de Adobe.

Además de replicar el evento, con las funciones de reenvío de eventos, puede agregar, filtrar o manipular los datos recopilados originales que cumplan los requisitos de otras zonas protegidas. Por ejemplo, la zona protegida A debe recibir todos los elementos de datos de evento y la zona protegida B solo debe recibir datos que no sean de identificación personal.

El reenvío de eventos utiliza una propiedad de etiqueta independiente que contiene los elementos de datos, las reglas y las extensiones necesarias para sus requisitos de datos. Con un evento entrante, la propiedad Reenvío de eventos puede recopilar los datos y gestionarlos según sea necesario antes del reenvío.

La zona protegida de destino debería tener configurado un punto final de flujo HTTP para su uso por parte de la extensión HTTPS de reenvío de eventos.



## Casos de uso

* Informes de datos globales: cuando se utilizan varias zonas protegidas con el fin de aislar los entornos operativos y es necesario consolidar la recopilación de datos en una zona protegida para la creación de informes de varias zonas. El reenvío de eventos a una zona protegida de creación de informes permite que cada entorno operativo de zona protegida envíe datos a medida que se recopilan en tiempo real.
* Administre la recopilación de datos en zonas protegidas en función de distintas reglas de datos para cada entorno operativo de zona protegida. Entornos operativos que requieren el filtrado de datos confidenciales, como los servicios de salud y financieros

## Aplicaciones

* Recopilación de datos de Adobe Experience Platform

## Arquitectura

<img src="assets/multi-Sandbox-Data-Collection.svg" alt="Arquitectura de referencia para el reenvío de eventos de múltiples zonas protegidas" style="width:90%; border:1px solid #4a4a4a" />

1. Los autores de etiquetas definen tanto una propiedad de etiqueta como una propiedad de reenvío de eventos. Aquí, los autores definirán los elementos de datos, las reglas y las acciones que administran la recopilación de datos. Tenga en cuenta que el código de propiedad tag se ejecuta en el cliente y se distribuye mediante un host CDN. El código de propiedad Reenvío de eventos se ejecuta en el servidor de Adobe Edge.

1. Los datos recopilados en el cliente se envían a la red perimetral. Los clientes también tienen la opción de enviar datos primero a su propio servidor como método de recopilación del lado del servidor.  El SDK web puede proporcionar una capacidad de recopilación de servidor a servidor. Sin embargo, su implementación requiere un modelo de programación diferente. Consulte la documentación **Información general sobre la API del servidor de red de Edge**, a continuación.

1. Platform Edge Network recibe cargas de recopilación de datos y organiza el flujo de datos a los sistemas necesarios, como Target y Analytics.

1. Los elementos de datos de la propiedad de reenvío de eventos se utilizan para acceder a los datos de evento que llegan a la carga útil. Las reglas también permiten manipular los datos de evento antes del reenvío, de ser necesario. Por ejemplo, puede dar a los datos de transmisión el formato XDM necesario para su ingesta.

1. El reenvío de eventos proporciona la extensión HTTPS que permite reenviar los datos de evento a un punto final HTTPS.

1. El Simulador para pruebas 2 está configurado con un punto final de flujo continuo que recibe el evento reenviado.

## Documentación relacionada

* [Documentación del reenvío de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=es)
* [Vídeos de reenvío de eventos](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=es)
* [Lección sobre el reenvío de eventos](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=es) del tutorial del SDK web
* [Información general sobre el SDK web de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es)
* [Información general sobre la API del servidor de red de Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es)

## Publicaciones de blog relacionadas

* [[!DNL Boosting Website Performance with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [[!DNL Solving Implementation Pain Points with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Adobe Experience Platform Web SDK — Adobe Target]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [[!DNL Adobe Experience Platform Web SDK Migration Scenarios for Adobe Analytics]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [[!DNL Unify Your Adobe Experience Platform Services with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [[!DNL Accelerate Your Mobile Application Development with Adobe Experience Platform Mobile SDK and Launch]](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [[!DNL Simplifying Customer Workflows with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
