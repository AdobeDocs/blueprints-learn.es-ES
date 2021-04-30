---
title: Modelo de Audience Activation en línea/sin conexión
description: Audience Activation en línea / sin conexión.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: 76fe52d8e83e075f9e7ce6e8596880181b01a7fd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 79%

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

<img src="assets/online_offline_activation.svg" alt="Arquitectura de referencia para el modelo de Audience Activation en línea/sin conexión" style="border:1px solid #4a4a4a" />

## Guardas

Consulte las protecciones como se describe en la página Información general sobre la activación de perfiles y audiencias: [LINK](overview.md)

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
* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Documentación de la segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Documentación de los destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=es)

## Vídeos y tutoriales relacionados

* [Información general de Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=es)
* [[!UICONTROL Versión de prueba de Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=es)
* [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=es)
