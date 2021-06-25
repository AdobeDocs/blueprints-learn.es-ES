---
title: Activación de audiencias y perfiles
description: Ofrezca experiencias de cliente activadas por la audiencia y centradas en el perfil a través de Real-time Customer Data Platform.
solution: Experience Platform, Real-time Customer Data Platform
kt: null
thumbnail: null
exl-id: eeeb4325-d0e8-4fd8-86ab-0b8afdd0b69f
source-git-commit: 8cdb08ae29b766adf16877919af82d0691768576
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 100%

---


# Activación de audiencias y perfiles

La activación de audiencias y perfiles es la clave del éxito en el mundo del marketing basado en datos. Sin embargo, muchas marcas aún centran sus esfuerzos en la activación por canal en primer lugar, lo que suele producir un alcance y una personalización incoherentes.

Abordando el canal en primer lugar, cada canal actúa como un depósito donde los esfuerzos de personalización se dirigen solo a los clientes que interactúan con la marca en ese preciso canal. Este enfoque no refleja la realidad de la interacción del cliente con las marcas por diferentes puntos de contacto. La activación de audiencias y perfiles permite que las marcas conecten la interacción del cliente a través de los diferentes canales, con el fin de conseguir una audiencia centralizada que se puede activar en todos los canales.

| Modelo | Descripción | Aplicaciones de Experience Cloud |
|---|---|---|
| **[Activación de audiencia anónima](anonymous.md)** | <ul><li>Segmentación de la audiencia a través del sitio web y otros canales de publicidad para conseguir datos anónimos de comportamiento del cliente.</li><li>Integración con datos de audiencia de terceros para una personalización mejorada.</li></ul> | <ul><li>Adobe Audience Manager</li></ul> |
| **[Activación de audiencia en línea/sin conexión](online-offline.md)** | <ul><li>Activación de destinos conocidos basados en perfiles, tales como proveedores de email, redes sociales y destinos de publicidad. </li><li>Utilización de atributos y eventos sin conexión, tales como pedidos sin conexión, transacciones, CRM o datos de fidelidad y comportamiento en línea para la segmentación y personalización en línea.</li></ul> | <ul><li>Adobe Experience Platform</li><li> [!UICONTROL Real-time Customer Data Platform]</li><li>Adobe Audience Manager (opcional)</li></ul> |
| **[Activación de audiencias y perfiles en destinos empresariales](enterprise-destinations.md)** | <ul><li>Replicación y actualización de los cambios de perfil y audiencia en los almacenes de datos empresariales para casos de uso de activación y generación de informes. </li></ul><ul><li>Inicio de una acción de ventas o asistencia al cliente mediante la notificación de una acción del cliente desde [!UICONTROL Real-time Customer Data Platform] a los sistemas y las aplicaciones empresariales.</li></ul> | <ul><li>Adobe Experience Platform</li><li>[!UICONTROL Plataforma de datos de clientes en tiempo real]</li><li>Activación de Experience Platform</li><li>Adobe Audience Manager (opcional)</li></ul> |
| **[Activación de audiencias y perfiles con las aplicaciones de Experience Cloud](platform-and-applications.md)** | <ul><li>Administrar perfiles y audiencias en Experience Platform y compartirlas con las aplicaciones de Experience Cloud</li><li>Generar y compartir segmentos ricos y datos de clientes en Experience Platform y compartirlos con las aplicaciones de Experience Cloud</li></ul> | <ul><li>Adobe Experience Platform</li><li>[!UICONTROL Plataforma de datos de clientes en tiempo real]</li><li>Activación de Experience Platform</li><li>Aplicaciones de Experience Cloud</li></ul> |
| **[Centro de actividad del cliente](customer-activity.md)** | <ul><li>Ofrecer un contexto más rico sobre el cliente a las interacciones realizadas por agentes, como las experiencias de asistencia y ventas. Utilizando la búsqueda de perfil en Experience Platform, los agentes pueden recibir más contexto sobre el cliente, tal como compras recientes, interacciones con campañas, tendencias, pertenencia a audiencia y otros atributos y datos que se almacenan en tiempo real en el perfil del cliente.</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |

## Arquitectura de Real-time Customer Profile

La siguiente ilustración describe los componentes principales de Real-time Customer Profile de Experience Platform.

Las primeras fuentes de datos se ingieren en Experience Platform. Si la fuente de datos está configurada para el procesamiento de perfiles, se incluirá en Real-time Customer Profile. Se crea un único fragmento o documento de perfil para cada fuente de datos y para cada registro de ID principal configurado para cada fuente de datos. Además, a medida que los datos se ingieren en el perfil, también los procesa el servicio de identidad. Cualquier registro de la fuente de datos que tenga más de una identidad marcada en el esquema y con los valores correspondientes rellenados en el registro se procesará como una relación de identidad dentro del servicio de identidad.

El servicio de identidad no procesa los registros que solo tienen una identidad, ya que no tienen vínculos de identidad para rellenar el gráfico con más detalle. Tenga en cuenta, asimismo, que el servicio de identidad no distingue entre identidades principales y secundarias. Simplemente procesa las relaciones de identidad entre las propias identidades.

La fusión de fragmentos de perfil se produce cuando el gráfico de identidad proporciona las relaciones entre los distintos fragmentos de perfil de origen que se han relacionado. La política de fusión determina qué fragmentos de origen y qué gráfico de identidad se utilizarán cuando se combinen los fragmentos. Cada vez que se accede al perfil, se produce la fusión de los fragmentos de perfil para garantizar la vista combinada más actualizada del mismo. Las reglas de política y gobernanza garantizan que solo se puedan activar los segmentos y los atributos autorizados en los destinos especificados.

<img src="assets/profile_architecture.jpg" alt="Arquitectura de referencia de Real-time Customer Profile" style="border:1px solid #4a4a4a" />


## Guardas para los modelos de activación de audiencias y perfiles

* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)


### Activación de atributos e identidades

* [!UICONTROL Real-time Customer Data Platform] puede activar las pertenencias a audiencia, así como los cambios de atributos e identidad que se producen en los perfiles que pertenecen a los segmentos seleccionados para la activación. Si su objetivo es activar atributos o identidades, debe definir un segmento global que incluya todos los perfiles a los que se envían las actualizaciones de atributos e identidades. En ese momento, puede seleccionar el segmento y los atributos deseados para activarlos como parte de la configuración de destino.
* Tenga en cuenta que los destinos por lotes no son compatibles con la activación de eventos de cambio solo por atributo. Se pueden enviar las pertenencias a audiencia completas o incrementales junto con los atributos seleccionados para la activación, pero no se pueden activar eventos de cambio solo por atributo mediante destinos por lotes.

### Activación de segmentos por lotes en destinos de flujo

* Es posible activar segmentos por lotes en destinos de flujo. Los trabajos de segmentos por lotes colocan mensajes en el proceso cuando se ha completado el trabajo del segmento de la activación por flujo.

### Activación de segmentos por flujo en destinos por lotes

* Es posible activar segmentos por flujo en destinos por lotes. La programación del destino por lotes exporta las pertenencias a segmentos de perfil en función de la programación de destino por lotes. Esto incluye tanto las pertenencias a segmentos determinadas por métodos de flujo como por lotes.

### Activación de eventos de experiencia

* No es compatible con la activación de eventos brutos de experiencia. Para la activación con eventos de experiencia, se debe crear un segmento con las reglas necesarias que incluyan o excluyan la lógica de eventos de experiencia. Esto crea un segmento que se define para los eventos de experiencia, y la pertenencia a segmento se puede activar como proxy para activar los eventos brutos de experiencia. Considere también la posibilidad de utilizar [!UICONTROL Launch Server Side] para activar eventos brutos de experiencia recopilados mediante SDK.


## Entradas relacionadas en el blog

* [[!DNL Blueprints for Audience Activation in Adobe Experience Platform]](https://medium.com/adobetech/a-blueprint-for-audience-activation-in-adobe-experience-platform-b2b30fae90fd)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
