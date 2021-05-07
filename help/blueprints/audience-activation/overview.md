---
title: Activación de audiencias y perfiles
description: Ofrezca experiencias de cliente activadas por la audiencia y centradas en el perfil a través de Real-time Customer Data Platform.
solution: Experience Platform, Real-time Customer Data Platform
kt: null
thumbnail: null
exl-id: eeeb4325-d0e8-4fd8-86ab-0b8afdd0b69f
translation-type: tm+mt
source-git-commit: 5471d9c0f6fdef6fbac72d5d35f32353ea5a5ee8
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 91%

---


# Activación de audiencias y perfiles

La activación de audiencias y perfiles es la clave del éxito en el mundo del marketing basado en datos. Sin embargo, muchas marcas aún centran sus esfuerzos en la activación por canal en primer lugar, lo que suele producir un alcance y una personalización incoherentes.

Abordando el canal en primer lugar, cada canal actúa como un depósito donde los esfuerzos de personalización se dirigen solo a los clientes que interactúan con la marca en ese preciso canal. Este enfoque no refleja la realidad de la interacción del cliente con las marcas por diferentes puntos de contacto. La activación de audiencias y perfiles permite que las marcas conecten la interacción del cliente a través de los diferentes canales, con el fin de conseguir una audiencia centralizada que se puede activar en todos los canales.

| Modelo | Descripción | Aplicaciones de Experience Cloud |
|---|---|---|
| **[Activación de audiencia anónima](anonymous.md)** | <ul><li>Segmentación de la audiencia a través del sitio web y otros canales de publicidad para conseguir datos anónimos de comportamiento del cliente.</li><li>Integración con datos de audiencia de terceros para una personalización mejorada.</li></ul> | <ul><li>Adobe Audience Manager</li></ul> |
| **[Activación de audiencia en línea / sin conexión](online-offline.md)** | <ul><li>Activación de destinos conocidos basados en perfiles, tales como proveedores de email, redes sociales y destinos de publicidad. </li><li>Utilización de atributos y eventos sin conexión, tales como pedidos sin conexión, transacciones, CRM o datos de fidelidad y comportamiento en línea para la segmentación y personalización en línea.</li></ul> | <ul><li>Adobe Experience Platform</li><li> [!UICONTROL Real-time Customer Data Platform]</li><li>Adobe Audience Manager (opcional)</li></ul> |
| **[Activación de audiencias y perfiles en destinos empresariales](enterprise-destinations.md)** | <ul><li>Replicación y actualización de los cambios de perfil y audiencia en los almacenes de datos empresariales para casos de uso de activación y generación de informes. </li></ul><ul><li>Inicio de una acción de ventas o asistencia al cliente mediante la notificación de una acción del cliente desde [!UICONTROL Real-time Customer Data Platform] a los sistemas y las aplicaciones empresariales.</li></ul> | <ul><li>Adobe Experience Platform</li><li>[!UICONTROL Plataforma de datos de clientes en tiempo real]</li><li>Activación de Experience Platform</li><li>Adobe Audience Manager (opcional)</li></ul> |
| **[Activación de audiencias y perfiles con aplicaciones de Experience Cloud](platform-and-applications.md)** | </ul><li>Administrar perfiles y audiencias en Experience Platform y compartirlos con aplicaciones Experience Cloud</li><li>Cree y comparta segmentos y perspectivas de clientes enriquecidos en Experience Platform y compártalos con aplicaciones Experience Cloud</li></ul> | <ul><li>Adobe Experience Platform</li><li>[!UICONTROL Plataforma de datos de clientes en tiempo real]</li><li>Activación de Experience Platform</li><li>Aplicaciones de Experience Cloud</li></ul> |
| **[Centro de actividad del cliente](customer-activity.md)** | <ul><li>Ofrecer un contexto más rico sobre el cliente a las interacciones realizadas por agentes, como las experiencias de asistencia y ventas. Utilizando la búsqueda de perfil en Experience Platform, los agentes pueden recibir más contexto sobre el cliente, tal como compras recientes, interacciones con campañas, tendencias, pertenencia a audiencia y otros atributos y datos que se almacenan en tiempo real en el perfil del cliente.</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |



## Protecciones para los esquemas de activación de audiencias y perfiles

* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)


### Activación de atributos e identidades

* [!UICONTROL Real-time Customer Data Platform] puede activar las pertenencias a audiencia, así como los cambios de atributos e identidad que se producen en los perfiles que pertenecen a los segmentos seleccionados para la activación. Si su objetivo es activar atributos o identidades, debe definir un segmento global que incluya todos los perfiles a los que se envían las actualizaciones de atributos e identidades. En ese momento, puede seleccionar el segmento y los atributos deseados para activarlos como parte de la configuración de destino.
* Tenga en cuenta que los destinos por lotes no son compatibles con la activación de eventos de cambio solo por atributo. Se pueden enviar las pertenencias a audiencia completas o incrementales junto con los atributos seleccionados para la activación, pero no se pueden activar eventos de cambio solo de atributos mediante destinos por lotes.

### Activación de segmentos por lotes en destinos de flujo

* Es posible activar segmentos por lotes en destinos de flujo. Los trabajos de segmentos por lotes colocan mensajes en el proceso cuando se ha completado el trabajo del segmento de la activación por flujo.

### Activación de segmentos por flujo en destinos por lotes

* Se admite la activación de segmentos de transmisión a destinos por lotes. La programación del destino por lotes exporta las pertenencias a segmentos de perfil en función de la programación de destino por lotes. Esto incluye tanto las pertenencias a segmentos determinadas por métodos de flujo como por lotes.

### Activación de eventos de experiencia

* No es compatible con la activación de eventos brutos de experiencia. Para la activación con eventos de experiencia, se debe crear un segmento con las reglas necesarias que incluyan o excluyan la lógica de eventos de experiencia. Esto crea un segmento que se define para los eventos de experiencia, y la pertenencia a segmento se puede activar como proxy para activar los eventos brutos de experiencia. Considere también la posibilidad de utilizar [!UICONTROL Launch Server Side] para activar eventos brutos de experiencia recopilados mediante SDK.


## Entradas relacionadas en el blog

* [[!DNL Blueprints for Audience Activation in Adobe Experience Platform]](https://medium.com/adobetech/a-blueprint-for-audience-activation-in-adobe-experience-platform-b2b30fae90fd)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
