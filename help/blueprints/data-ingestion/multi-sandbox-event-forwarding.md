---
title: Recopilación de datos de reenvío de eventos de múltiples zonas protegidas
description: Descubra cómo se pueden configurar los datos recopilados con los SDK móviles y web de Experience Platform con el fin de recopilar un solo evento y reenviarlo a múltiples zonas protegidas de Experience Platform.
solution: Data Collection
kt: 7202
exl-id: ecc94fc8-9fad-4b88-a153-3d0fc00d8d58
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 55%

---

# Recopilación de datos de reenvío de eventos de múltiples zonas protegidas

Este modelo muestra cómo se recopilan los datos con [!DNL Experience Platform] Los SDK web y móvil se pueden configurar para recopilar un único evento y reenviarlo a varios entornos limitados de AEP. Este modelo es específico para la recopilación de datos de varias zonas protegidas que usan el [!UICONTROL reenvío de eventos] para lograr este objetivo.

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

[!UICONTROL Reenvío de eventos] no se considera HIPAA Ready y no debe usarse en ningún caso de uso de HIPAA donde se recopilen datos de HIPAA.

Sin embargo, la infraestructura utilizada para [!UICONTROL Reenvío de eventos] se considera compatible con HIPAA y queda a discreción del cliente. Aunque la propiedad Etiqueta del [!UICONTROL reenvío de eventos] se encuentre en el sistema de [!UICONTROL reenvío de eventos], toda la carga útil de datos recopilada se envía al sistema de [!UICONTROL reenvío de eventos] para su procesamiento. Este proceso hace que [!UICONTROL Reenvío de eventos] sobre los casos de uso de HIPAA. Con toda la carga útil enviada a [!UICONTROL Reenvío de eventos] , este proceso incluiría cualquier valor HIPAA. Aunque el [!UICONTROL Reenvío de eventos] Las reglas de filtran esos datos antes de enviarlos a su destino, de modo que los datos HIPAA se siguen enviando a una infraestructura no compatible con HIPAA. Sin embargo, los datos de carga útil nunca se almacenan y son simplemente un paso a través.

### Secuencias de datos y puntos de conexión de streaming distintos

A medida que los datos fluyen por flujos de datos desde [!DNL Platform Edge Network], al utilizar [!UICONTROL Reenvío de eventos] En otra zona protegida de AEP, un requisito es no utilizar nunca el mismo conjunto de datos o punto final de flujo que el conjunto de datos que hace la colección original. Esto puede resultar perjudicial para la instancia de AEP y posiblemente provocar una situación de DoS.

### Volúmenes de tráfico estimados

Es necesario revisar los volúmenes de tráfico en cada caso de uso. Esto es importante, ya que un gran volumen puede provocar una situación de restricción y, si esto ocurre, los clientes reciben una notificación.

## Arquitectura

![Zona protegida múltiple [!UICONTROL Reenvío de eventos]](assets/multi-sandbox-data-collection.png)

1. Recopilación y envío de datos de evento a [!DNL Platform Edge Network] es necesario para utilizar [!UICONTROL Reenvío de eventos]. Puede utilizar etiquetas de Adobe para el lado del cliente o el [!DNL Platform Edge Network Server API] para la recopilación de datos de servidor a servidor.

   El [!DNL Platform Edge Network API] puede proporcionar una capacidad de recopilación de servidor a servidor. Sin embargo, esto requiere un modelo de programación diferente para implementar. Consulte la [información general sobre la API del servidor de Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es).

1. Las cargas útiles recopiladas se envían desde la implementación de etiquetas a [!DNL Platform Edge Network] a la [!UICONTROL Reenvío de eventos] servicio y procesado por su propia cuenta [!UICONTROL Elementos de datos], [!UICONTROL Reglas], y [!UICONTROL Acciones]. Para obtener más información sobre las diferencias, consulte [Etiquetas y [!UICONTROL Reenvío de eventos]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=es#differences-from-tags).

1. Un [!UICONTROL Reenvío de eventos] también es necesaria para recibir los datos de evento recopilados del [!DNL Platform Edge Network], si los datos de evento se enviaron a [!DNL Platform Edge Network] mediante una implementación de Etiquetas implementada o una colección de servidor a servidor.

   Los autores definen los elementos de datos, las reglas y las acciones que se utilizan para mejorar los datos de evento antes del reenvío a la segunda zona protegida. Considere la posibilidad de utilizar el elemento de datos de código personalizado [!DNL JavaScript] para estructurar los datos para la ingesta en zonas protegidas. En combinación con las funcionalidades de preparación de datos de Platform, tiene varias opciones para administrar la estructura de datos.

1. Actualmente, es necesario el uso de la extensión de Adobe [!UICONTROL Cloud Connector] en la propiedad de [!UICONTROL reenvío de eventos]. Después de que las reglas procesen o enriquezcan los datos de evento, la variable [!UICONTROL Conector de nube] se utiliza en una llamada de captura configurada para un POST, que envía la carga útil a la segunda zona protegida.

1. Se requiere un extremo de flujo continuo para la ingesta de datos en la segunda zona protegida. También puede tener en cuenta [!UICONTROL Preparación de datos] funciones en AEP para ayudar con la ingesta y asignación de [!UICONTROL Reenvío de eventos] cargas útiles a XDM. Consulte la documentación de AEP [Creación de una conexión por streaming de API de HTTP mediante la IU](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=es)
