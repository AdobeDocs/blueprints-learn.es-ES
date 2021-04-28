---
title: Modelo de Audience Activation en línea/sin conexión
description: Audience Activation en línea / sin conexión.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: 24b6ffe3021389d33e84688a8f1a90711ca4b772
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 35%

---

# Modelo de Audience Activation en línea/sin conexión

Emplee atributos y eventos sin conexión, tales como pedidos sin conexión, transacciones, CRM o datos de fidelidad y comportamiento en línea para la segmentación y personalización en línea.

Active audiencias de destinos conocidos basados en perfiles, tales como proveedores de email, redes sociales y destinos de publicidad.

## Casos de uso

* Segmentación de audiencia para audiencias conocidas en destinos sociales y de publicidad.
* Personalización en línea con atributos en línea y sin conexión.
* Activación de audiencias de canales conocidos, como email y SMS.

## Aplicaciones

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]

## Arquitectura

<img src="assets/onoff.svg" alt="Arquitectura de referencia para el modelo de Audience Activation en línea/sin conexión" style="border:1px solid #4a4a4a" />

## Guardas

* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)

### Protecciones para la evaluación y activación de segmentos

| Tipo de segmentación | Frecuencia | Rendimiento | Latencia (Evaluación de segmentos) | Latencia (Activación de segmentos) | Carga útil de activación |
|---|---|---|---|---|---|
| Segmentación de Edge | La segmentación de Edge está actualmente en fase beta y permite evaluar una segmentación válida en tiempo real en la red perimetral del Experience Platform para la toma de decisiones en la misma página en tiempo real mediante Adobe Target y Journey Optimizer de Adobe. |  | ~100 ms | Disponible inmediatamente para su personalización en Adobe Target, para búsquedas de perfiles en el perfil de Edge y para su activación mediante destinos basados en cookies. | Pertenencia a audiencias disponibles en Edge para búsquedas de perfiles y destinos basados en cookies.<br>Los atributos Pertenencia a audiencias y Perfil están disponibles para Adobe Target y Journey Optimizer. |
| Segmentación por flujo | Cada vez que se incorpora un nuevo evento o registro de flujo continuo en el perfil del cliente en tiempo real y la definición del segmento es un segmento de flujo continuo válido. <br>Consulte la documentación de  [segmentación ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es) para obtener instrucciones sobre los criterios de los segmentos de flujo continuo | Hasta 1500 eventos por segundo. | ~ p95 &lt;5 min | Destinos de transmisión: Las pertenencias a audiencias de transmisión se activan en aproximadamente 10 minutos o se agrupan por lotes en función de los requisitos del destino.<br>Destinos programados: Las pertenencias a audiencias de flujo continuo se activan en lote según la hora de envío de destino programada. | Destinos de transmisión: Cambios en la pertenencia a audiencias, valores de identidad y atributos de perfil.<br>Destinos programados: Cambios en la pertenencia a audiencias, valores de identidad y atributos de perfil. |
| Segmentación incremental | Una vez por hora para los nuevos datos que se han incorporado en el perfil del cliente en tiempo real desde la última evaluación de segmentos por lotes o incrementales. |  |  | Destinos de transmisión: Las suscripciones de audiencia incrementales se activan en aproximadamente 10 minutos o por lotes según los requisitos del destino.<br>Destinos programados: Las suscripciones de audiencia incrementales se activan en lote según la hora de entrega de destino programada. | Destinos de transmisión: Los cambios en la pertenencia a la audiencia y solo los valores de identidad.<br>Destinos programados: Cambios en la pertenencia a audiencias, valores de identidad y atributos de perfil. |
| Segmentación por lotes | Una vez al día en función de una programación predeterminada del sistema o iniciada manualmente mediante API. |  | Aproximadamente una hora por trabajo para un tamaño de almacén de perfiles de hasta 10 TB, 2 horas por trabajo para un tamaño de almacén de perfiles de entre 10 TB y 100 TB. El rendimiento del trabajo del segmento por lotes depende del número de perfiles, el tamaño de los perfiles y el número de segmentos que se evalúen. | Destinos de transmisión: Las pertenencias a audiencias por lotes se activan aproximadamente dentro de los 10 días posteriores a la finalización de la evaluación de segmentación o del microagrupamiento, según los requisitos del destino.<br>Destinos programados: Las suscripciones a audiencias por lotes se activan según la hora de envío de destino programada. | Destinos de transmisión: Los cambios en la pertenencia a la audiencia y solo los valores de identidad.<br>Destinos programados: Cambios en la pertenencia a audiencias, valores de identidad y atributos de perfil. |

### Protecciones para el uso compartido de audiencias entre aplicaciones

| Integraciones de aplicaciones de audiencia | Frecuencia | Rendimiento/volumen | Latencia (Evaluación de segmentos) | Latencia (Activación de segmentos) |
|---|---|---|---|---|
| Audience Manager de la plataforma de datos del cliente en tiempo real | Depender del tipo de segmentación : consulte la tabla de protecciones de segmentación anterior. | Depender del tipo de segmentación : consulte la tabla de protecciones de segmentación anterior. | Depender del tipo de segmentación : consulte la tabla de protecciones de segmentación anterior. | Minutos después de la finalización de la evaluación del segmento.<br>La sincronización inicial de la configuración de audiencia entre la plataforma de datos del cliente en tiempo real y el Audience Manager tarda aproximadamente 4 horas.<br>Cualquier pertenencia a una audiencia realizada durante el periodo de 4 horas se escribirá en el Audience Manager del trabajo de segmentación por lotes subsiguiente como pertenencia a una audiencia &quot;existente&quot;. |
| Adobe Analytics al Audience Manager |  | De forma predeterminada, se puede compartir un máximo de 75 audiencias para cada grupo de informes de Adobe Analytics. Si se utiliza una licencia de Audience Manager, no hay límite en el número de audiencias que se pueden compartir entre Adobe Analytics y Adobe Target o Adobe Audience Manager y Adobe Target. |  |  |
| Adobe Analytics a la plataforma de datos del cliente en tiempo real | No disponible actualmente | No disponible actualmente | No disponible actualmente | No disponible actualmente |





## Pasos de implementación

1. Configurar esquemas y conjuntos de datos en Experience Platform.
1. Configurar las identidades e identidad de áreas de nombres correctas en el esquema para asegurar que los datos ingeridos se puedan combinar en un perfil unificado.
1. Activar el esquema y los conjuntos de datos del perfil.
1. Ingerir datos en Platform.
1. Aprovisionar el uso compartido de segmentos [!UICONTROL Plataforma de datos del cliente en tiempo real] entre el Experience Platform y el Audience Manager para que las audiencias definidas en el Experience Platform se compartan con el Audience Manager.
1. Generar segmentos en Experience Platform para que se evalúen por lotes o flujo. El sistema determina automáticamente si el segmento debe ser evaluado por lotes o flujo.
1. Configurar destinos para compartir atributos de perfil y pertenencias a audiencia a los destinos deseados.

## Consideraciones sobre la implementación

* Compartir datos de perfil con los destinos requiere incluir un valor de identidad específico utilizado por el destino en su carga. Cualquier identidad necesaria para un destino de destino debe ingerirse en Platform y configurarse como identidad para el [!UICONTROL Perfil del cliente en tiempo real].

* Para escenarios de activación donde las audiencias se comparten de Experience Platform a Audience Manager, todas las identidades incluidas en el [!UICONTROL perfil del cliente en tiempo real] se comparten con Audience Manager. Las audiencias de Experience Platform se pueden compartir a través de los destinos de Audience Manager cuando las identidades de destino necesarias se incluyan en el [!UICONTROL perfil del cliente en tiempo real] o cuando las identidades del [!UICONTROL perfil del cliente en tiempo real] se relacionen con las identidades requeridas en destino, si están vinculadas en Audience Manager.

## Documentación relacionada

* [Descripción del producto Real-time Customer Data Platform](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform.html)
* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Documentación de la segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Documentación de los destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=es)

## Vídeos y tutoriales relacionados

* [Información general de Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=es)
* [[!UICONTROL Versión de prueba de Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=es)
* [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=es)
