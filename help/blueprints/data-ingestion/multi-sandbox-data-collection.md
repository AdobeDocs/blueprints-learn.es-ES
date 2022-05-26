---
title: Modelo de recopilación de datos de reenvío de eventos de Simulador para pruebas múltiples
description: Transmitir datos recopilados por SDK de Experience Platform a varios entornos limitados mediante el reenvío de eventos
solution: Data Collection
kt: 7202
source-git-commit: 8ea7041103f86f034740f00a607ae36ca0b358cf
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 18%

---

# Modelo de recopilación de datos de reenvío de eventos de Simulador para pruebas múltiples

El modelo de recopilación de datos de reenvío de eventos de entornos limitados muestra cómo se pueden configurar los datos recopilados con los SDK móviles y web de Adobe Experience Platform para recopilar un solo evento y reenviar a varios entornos limitados de AEP. Este modelo es un caso de uso específico que utiliza la función Reenvío de eventos de las etiquetas de Adobe.

Además de replicar el evento, con las funciones de Reenvío de eventos, puede agregar, filtrar o manipular los datos recopilados originales que cumplan los requisitos de otros entornos limitados. Por ejemplo, el Simulador para pruebas A debe recibir todos los elementos de datos de evento y el Simulador para pruebas B solo debe recibir datos que no sean PII.

El reenvío de eventos utiliza una propiedad Tag independiente que contiene los elementos de datos, las reglas y las extensiones necesarias para los requisitos de datos. Con un evento entrante, la propiedad Event Forwarding puede recopilar los datos y administrar según sea necesario antes del reenvío.

El sadnbox de destino necesitaría un punto final de flujo HTTP configurado que utilizaría la extensión HTTPS de reenvío de eventos.



## Casos de uso

* Informes de datos globales : al usar varios entornos limitados para aislar los entornos operativos y la necesidad de consolidar la recopilación de datos en un entorno limitado para la creación de informes en varios entornos limitados. Event Forward to a reporting sandbox permite que cada entorno operativo del simulador de pruebas envíe datos a medida que se recopilan en tiempo real a un simulador de pruebas de informes
* Administre la recopilación de datos en entornos limitados en función de distintas reglas de datos para cada entorno operativo de entorno limitado. Entornos operativos que requieren el filtrado de datos confidenciales, como los Servicios de salud y financieros

## Aplicaciones

* Colección de Adobe Experience Platform

## Arquitectura

<img src="assets/multi-Sandbox-Data-Collection.svg" alt="Arquitectura de referencia para el reenvío de eventos de entornos limitados" style="width:90%; border:1px solid #4a4a4a" />

1. Los autores de etiquetas definen tanto una propiedad de etiqueta como una propiedad de reenvío de eventos. Aquí, los autores definirán los elementos de datos, las reglas y las acciones que administran la recopilación de datos. Tenga en cuenta que el código de propiedad de etiqueta se ejecuta en el cliente y se distribuye mediante un host CDN. El código de propiedad Event Forwarding se ejecuta en el servidor de Adobe Edge.

1. Los datos recopilados en el cliente se envían al servidor perimetral. Los clientes también tienen la opción de enviar datos primero a su propio servidor como método de recopilación en el servidor.
El WebSDK puede proporcionar una capacidad de recopilación de servidor a servidor. Sin embargo, esto requiere un modelo de programación diferente para implementarlo. Consulte la documentación **Información general sobre la API del servidor de red perimetral** below

1. Platform Edge Server recibe cargas de recopilación de datos y organiza el flujo de datos a los sistemas necesarios, como Target y Analytics.

1. Propiedad de reenvío de eventos Los elementos de datos se utilizan para acceder a los datos de evento que llegan en la carga útil. Las reglas también pueden utilizarse para manipular los datos de Evento según sea necesario antes del reenvío. Por ejemplo, formatear los datos en el XDM necesario para la transmisión de datos

1. El reenvío de eventos proporciona la extensión HTTPS que proporciona la capacidad de reenviar los datos de evento a un punto final HTTPS.

1. El Simulador para pruebas 2 está configurado con un Punto Final de Transmisión que recibe el evento reenviado.

## Documentación relacionada

* [Documentación del reenvío de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=es)
* [Vídeos de reenvío de eventos](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=es)
* [Lección sobre el reenvío de eventos](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=es) del tutorial del SDK web
* [Información general del Experience Platform WebSDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es)
* [Información general sobre la API del servidor de red perimetral](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es)

## Entradas relacionadas en el blog

* [[!DNL Boosting Website Performance with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [[!DNL Solving Implementation Pain Points with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Adobe Experience Platform Web SDK — Adobe Target]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [[!DNL Adobe Experience Platform Web SDK Migration Scenarios for Adobe Analytics]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [[!DNL Unify Your Adobe Experience Platform Services with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [[!DNL Accelerate Your Mobile Application Development with Adobe Experience Platform Mobile SDK and Launch]](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [[!DNL Simplifying Customer Workflows with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
