---
title: Recopilación de datos de reenvío de eventos de varias zonas protegidas
description: Descubra cómo se pueden configurar los datos recopilados con los SDK web y móvil de Experience Platform para recopilar un único evento y reenviarlos a varios entornos limitados de Experience Platform.
solution: Data Collection
kt: 7202
source-git-commit: e9a9abeaa722bb2f9a232f4e861b1b5eae86edd1
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 20%

---


# Recopilación de datos de reenvío de eventos de varias zonas protegidas

Este modelo muestra cómo se pueden configurar los datos recopilados con los SDK web y móvil de Experience Platform para recopilar un único evento y reenviarlos a varios entornos limitados de AEP. Este modelo es específico para la recopilación de datos de varias zonas protegidas que utiliza [!UICONTROL Reenvío de eventos] para lograr este objetivo.

Además de replicar el evento con [!UICONTROL Reenvío de eventos] Con estas funciones, puede agregar, filtrar o manipular los datos recopilados originales que cumplan los requisitos de otras zonas protegidas.

[!UICONTROL Reenvío de eventos] utiliza una propiedad independiente que contiene [!UICONTROL Elementos de datos], [!UICONTROL Reglas], y [!UICONTROL Extensiones] necesario para sus requisitos de datos. Con un evento entrante, su [!UICONTROL Reenvío de eventos] La propiedad puede recopilar los datos y administrarlos según sea necesario antes del reenvío.

Su zona protegida de destino requiere un punto final de flujo HTTP configurado que utilice el Adobe [!UICONTROL Conector de nube] extensión.

## Casos de uso

* Creación de informes de datos globales: Cuando se utilizan varios entornos limitados para aislar los entornos operativos y la necesidad de consolidar la recopilación de datos en un entorno limitado para la creación de informes entre entornos limitados. Enrutamiento de un evento de Experience Edge mediante [!UICONTROL Reenvío de eventos] La migración a una zona protegida de informes permite que cada entorno operativo de la zona protegida envíe datos a medida que se recopilen en tiempo real a una zona protegida de informes.

* Administre la recopilación de datos en zonas protegidas en función de distintas reglas de datos para cada entorno operativo de zona protegida.

## Aplicaciones

* [!DNL Experience Platform] Recopilación de datos
* [!UICONTROL Reenvío de eventos]
* AEP [!UICONTROL Extensión]
* [!UICONTROL Extensión de Cloud Connector]

## Consideraciones

Con [!UICONTROL Reenvío de eventos] como método para enviar datos a varios entornos limitados, hay consideraciones que deben tenerse en cuenta con la arquitectura de la solución.

### Sin datos de la HIPAA

[!UICONTROL No se considera que el reenvío de eventos esté preparado para cumplir con los requisitos de la HIPAA y no debe usarse en casos de uso de la HIPAA en los que se recopilen datos de la HIPAA. ] Sin embargo, la infraestructura utilizada para [!UICONTROL Reenvío de eventos] se considera que HIPAA está listo y es únicamente a discreción del cliente. Mientras que su [!UICONTROL Reenvío de eventos] La propiedad de etiqueta reside en [!UICONTROL Reenvío de eventos] sistema, toda la carga útil de datos recopilada se envía a [!UICONTROL Reenvío de eventos] sistema para procesamiento. Es este proceso el que hace que [!UICONTROL Reenvío de eventos] sobre los casos de uso de HIPAA. Con toda la carga útil enviada a [!UICONTROL Reenvío de eventos] , esto incluiría cualquier valor HIPAA. Aunque el [!UICONTROL Reenvío de eventos] Las reglas filtrarán esos datos antes de enviarlos a su destino, y esos datos HIPAA se seguirán enviando a una infraestructura no preparada para HIPAA. Sin embargo, los datos de carga útil nunca se almacenan y simplemente se transmiten sin ser retenidos.

### Diferentes flujos de datos y puntos finales de flujo

A medida que los datos fluyen por flujos de datos desde [!UICONTROL Red perimetral de plataforma], al utilizar [!UICONTROL Reenvío de eventos] En otra zona protegida de AEP, un requisito es no utilizar nunca el mismo conjunto de datos o punto final de flujo que el conjunto de datos que hace la colección original. Esto puede resultar perjudicial para la instancia de AEP y posiblemente provocar una situación de DoS.

### Volúmenes de tráfico estimados

Es necesario revisar los volúmenes de tráfico en cada caso de uso. Esto es importante, ya que los volúmenes altos podrían provocar una situación de restricción y, si esto ocurre, se notifica a los clientes.

## Arquitectura

![Zona protegida múltiple [!UICONTROL Reenvío de eventos]](assets/multi-sandbox-data-collection.png)

1. Recopilación y envío de datos de evento a [!UICONTROL Red perimetral de plataforma] es necesario para utilizar [!UICONTROL Reenvío de eventos]. Los clientes pueden utilizar etiquetas de Adobe para el lado del cliente o el [!UICONTROL API del servidor de red perimetral de Platform] para la recopilación de datos de servidor a servidor. El [!UICONTROL API de red de Platform Edge] puede proporcionar una capacidad de recopilación de servidor a servidor. Sin embargo, esto requiere un modelo de programación diferente para implementar. Consulte [Información general sobre la API del servidor de red perimetral](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es).

1. Las cargas útiles recopiladas se envían desde la implementación de etiquetas a [!UICONTROL Red perimetral de plataforma] a la [!UICONTROL Reenvío de eventos] servicio y procesado por su propia cuenta [!UICONTROL Elementos de datos], [!UICONTROL Reglas] y [!UICONTROL Acciones]. Puede obtener más información sobre las diferencias entre [[!UICONTROL las etiquetas y el reenvío de eventos]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=es#differences-from-tags).

1. Un [!UICONTROL Reenvío de eventos] también es necesaria para recibir los datos de evento recopilados del [!UICONTROL Red perimetral de plataforma]. Si los datos de evento se enviaron a Platform Edge Network mediante una implementación de etiquetas implementada o una colección de servidor a servidor. Los autores definen los elementos de datos, las reglas y las acciones que se utilizan para mejorar los datos de evento antes del reenvío a la segunda zona protegida. Considere utilizar el código personalizado [!DNL JavaScript] elemento de datos para ayudar a estructurar los datos para la ingesta en zonas protegidas. En combinación con las capacidades de preparación de datos de Platform, tiene varias opciones para administrar la estructura de datos.

1. Actualmente, el uso del Adobe [!UICONTROL Extensión de conector de nube] es necesario dentro de [!UICONTROL Reenvío de eventos] Propiedad. Una vez que las reglas procesan o enriquecen los datos de evento, Cloud Connector se utiliza dentro de una llamada de captura configurada para un POST que envía la carga útil a la segunda zona protegida

1. Se requiere un punto final de flujo continuo para la ingesta de datos en la segunda zona protegida. También puede considerar las funcionalidades de preparación de datos en AEP para ayudar con la ingesta y asignación de [!UICONTROL Reenvío de eventos] cargas útiles a XDM. Consulte la documentación de AEP [Creación de una conexión por streaming de API de HTTP mediante la IU](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=es)
