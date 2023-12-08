---
title: Recopilación de datos de reenvío de eventos de múltiples zonas protegidas
description: Descubra cómo se pueden configurar los datos recopilados con los SDK móviles y web de Experience Platform con el fin de recopilar un solo evento y reenviarlo a múltiples zonas protegidas de Experience Platform.
solution: Data Collection
kt: 7202
exl-id: ecc94fc8-9fad-4b88-a153-3d0fc00d8d58
source-git-commit: 3d6a2416cdb9956e59be4b2918ba19f88cd2150b
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 100%

---

# Recopilación de datos de reenvío de eventos de múltiples zonas protegidas

Este modelo muestra cómo se pueden configurar los datos recopilados con los SDK móviles y web de Experience Platform con el fin de recopilar un solo evento y reenviarlo a múltiples zonas protegidas de AEP. Este modelo es específico para la recopilación de datos de varias zonas protegidas que usan el [!UICONTROL reenvío de eventos] para lograr este objetivo.

Además de replicar el evento, con las funciones de [!UICONTROL reenvío de eventos], puede agregar, filtrar o manipular los datos recopilados originales que cumplan los requisitos de otras zonas protegidas.

El [!UICONTROL reenvío de eventos] utiliza una propiedad independiente que contiene los [!UICONTROL elementos de datos], las [!UICONTROL reglas] y las [!UICONTROL extensiones] necesarias para sus requisitos de datos. Con un evento entrante, la propiedad de [!UICONTROL reenvío de eventos] puede recopilar los datos y gestionarlos según sea necesario antes del reenvío.

Es necesario que se configure un punto de conexión de streaming por HTTP en la zona protegida de destino para que lo utilice la extensión de Adobe [!UICONTROL Cloud Connector].

## Casos de uso

* Informes de datos globales: cuando se utilizan varias zonas protegidas con el fin de aislar los entornos operativos y es necesario consolidar la recopilación de datos en una zona protegida para la creación de informes de varias zonas. El enrutamiento de un evento de Experience Edge a través del [!UICONTROL reenvío de eventos] a una zona protegida de creación de informes permite que cada entorno operativo de zona protegida envíe datos a medida que se recopilan en tiempo real.

* Administre la recopilación de datos en zonas protegidas en función de distintas reglas de datos para cada entorno operativo de zona protegida.

## Aplicaciones

* [!DNL Experience Platform] Recopilación de datos
* [!UICONTROL Reenvío de eventos]
* [!UICONTROL Extensión] de AEP
* [!UICONTROL Extensión de Cloud Connector]

## Consideraciones

Con el [!UICONTROL reenvío de eventos] como enfoque para enviar datos a múltiples zonas protegidas, hay consideraciones que deben tenerse en cuenta con la arquitectura de la solución.

### Sin datos de la HIPAA

No se considera que el [!UICONTROL reenvío de eventos] esté preparado para cumplir con los requisitos de la HIPAA y no debe usarse en casos de uso de la HIPAA en los que se recopilen datos de la HIPAA. Sin embargo, se considera que la infraestructura que se utiliza para el [!UICONTROL reenvío de eventos] está preparada para cumplir con los requisitos de la HIPAA y tomar la decisión de utilizarla es responsabilidad exclusiva del cliente. Aunque la propiedad Etiqueta del [!UICONTROL reenvío de eventos] se encuentre en el sistema de [!UICONTROL reenvío de eventos], toda la carga útil de datos recopilada se envía al sistema de [!UICONTROL reenvío de eventos] para su procesamiento. Este proceso es el que hace que el [!UICONTROL reenvío de eventos] sea preocupante para los casos de uso de la HIPAA. El envío de toda la carga útil al sistema de [!UICONTROL reenvío de eventos] incluirá cualquier valor de la HIPAA. Aunque las reglas de [!UICONTROL reenvío de eventos] filtren esos datos antes de enviarlos a su destino, esos datos de la HIPAA se seguirán enviando a una infraestructura que no está preparada para cumplir con los requisitos de la HIPAA. Sin embargo, los datos de carga útil nunca se almacenan y simplemente se transmiten sin ser retenidos.

### Secuencias de datos y puntos de conexión de streaming distintos

A medida que los datos se transmiten a través de secuencias de datos desde [!UICONTROL Platform Edge Network], al utilizar el [!UICONTROL reenvío de eventos] a otra zona protegida de AEP, un requisito que se debe cumplir es no utilizar nunca la misma secuencia de datos o punto de conexión de streaming que la secuencia de datos que realiza la recopilación original. Esto puede resultar perjudicial para la instancia de AEP y posiblemente provocar una situación de DoS.

### Volúmenes de tráfico estimados

Es necesario revisar los volúmenes de tráfico en cada caso de uso. Esto es importante, ya que un gran volumen puede provocar una situación de restricción y, si esto ocurre, los clientes reciben una notificación.

## Arquitectura

![Zona protegida múltiple [!UICONTROL Reenvío de eventos]](assets/multi-sandbox-data-collection.png)

1. Es necesario recopilar y enviar datos de evento a [!UICONTROL Platform Edge Network] para utilizar el [!UICONTROL reenvío de eventos]. Los clientes pueden utilizar las etiquetas de Adobe para el lado del cliente o la API del servidor de [!UICONTROL Platform Edge Network] para la recopilación de datos de servidor a servidor. La API de [!UICONTROL Platform Edge Network] puede ofrecer una funcionalidad de recopilación de servidor a servidor. Sin embargo, su implementación requiere un modelo de programación diferente. Consulte la [información general sobre la API del servidor de Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es).

1. Las cargas útiles recopiladas se envían desde la implementación de etiquetas a [!UICONTROL Platform Edge Network] y luego al servicio de [!UICONTROL reenvío de eventos], y se procesan mediante sus propios [!UICONTROL elementos de datos], [!UICONTROL reglas] y [!UICONTROL acciones]. Puede obtener más información sobre las diferencias entre las [etiquetas y el [!UICONTROL reenvío de eventos]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=es#differences-from-tags).

1. También es necesaria una propiedad de [!UICONTROL reenvío de eventos] para recibir los datos de evento recopilados de [!UICONTROL Platform Edge Network]. independientemente de si los datos de evento se enviaron a Platform Edge Network mediante una implementación de etiquetas implementada o una recopilación de servidor a servidor. Los autores definen los elementos de datos, las reglas y las acciones que se utilizan para mejorar los datos de evento antes del reenvío a la segunda zona protegida. Considere la posibilidad de utilizar el elemento de datos de código personalizado [!DNL JavaScript] para estructurar los datos para la ingesta en zonas protegidas. En combinación con las funcionalidades de preparación de datos de Platform, tiene varias opciones para administrar la estructura de datos.

1. Actualmente, es necesario el uso de la extensión de Adobe [!UICONTROL Cloud Connector] en la propiedad de [!UICONTROL reenvío de eventos]. Una vez que las reglas procesan o mejoran los datos de evento, Cloud Connector se utiliza en una llamada de recuperación configurada para realizar una solicitud POST que envía la carga útil a la segunda zona protegida.

1. Se requiere un punto de conexión de streaming para la ingesta de datos para la segunda zona protegida. También puede tener en cuenta las funcionalidades de preparación de datos de AEP para la ingesta y asignación de cargas útiles de [!UICONTROL reenvío de eventos] a XDM. Consulte la documentación de AEP [Creación de una conexión por streaming de API de HTTP mediante la IU](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=es)
