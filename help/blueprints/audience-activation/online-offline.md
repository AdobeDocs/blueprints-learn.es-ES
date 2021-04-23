---
title: Modelo de Audience Activation en línea/sin conexión
description: Audience Activation en línea / sin conexión.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: 009a55715b832c3167e9a3413ccf89e0493227df
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 81%

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
* Las tareas de segmentación por lotes se ejecutan una vez al día según la programación predeterminada. Las tareas de exportación de segmentos se ejecutan antes de la entrega programada en el destino. Observe que las tareas de segmentación por lotes y entrega en destino se ejecutan separadamente. El rendimiento de las tareas de segmentación por lotes y exportación depende de la cantidad de perfiles, su tamaño y número de segmentos que están siendo evaluados.
* Las tareas de segmentación por flujo se evalúan en minutos, lo que tarda el flujo de datos en llegar al perfil, y escriben las pertenencias a segmento en el perfil inmediatamente, además de enviar un evento para que las aplicaciones se suscriban.
* El abono de segmentos por flujo se lleva a cabo inmediatamente hacia los destinos de flujo y se entrega bien en eventos de pertenencia a segmento o en un microlote de eventos de perfil múltiple que depende de los patrones de ingesta del destino. Los destinos programados iniciarán la tarea de exportación de segmentos desde el perfil, antes de la entrega, para todos los segmentos evaluados en flujo que se entreguen por lotes de segmentos programados.
* Para compartir [!UICONTROL la pertenencia de la Plataforma de datos del cliente en tiempo real] al Audience Manager, esto sucede en cuestión de minutos para los segmentos de flujo continuo y en cuestión de minutos tras la finalización de la evaluación de segmentos por lotes para la segmentación por lotes.
* Los segmentos se comparten de Experience Platform a Audience Manager a los pocos minutos de la generación del segmento, tanto si se hace por el método de evaluación por flujo como por lotes. Existe una sincronización inicial de la configuración de segmentos entre Experience Platform y Audience Manager una vez que el segmento se ha creado inicialmente, después de ~4 horas, las suscripciones de segmentos de Experience Platform pueden empezar a realizarse en perfiles de Audience Manager. La pertenencia a audiencia realizada antes de la configuración del intercambio de audiencia de Experience Platform y Audience Manager, o antes de que los metadatos de audiencia se sincronicen desde Experience Platform hacia Audience Manager, no se generarán en Audience Manager hasta que no se comparta la próxima tarea de segmentación donde las pertenencias a segmento se marquen como “existing” (existente).
* Las tareas de destino por lotes o flujo de las tareas de segmentación por lote pueden compartir actualizaciones de atributos de perfil, así como pertenencias a segmentos.
* Las tareas de segmentación por flujo a destinos por flujo solo comparten actualizaciones de pertenencia a segmento.

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
* [Documentación de la segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Documentación de los destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=es)

## Vídeos y tutoriales relacionados

* [Información general de Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=es)
* [[!UICONTROL Versión de prueba de Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=es)
* [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=es)
