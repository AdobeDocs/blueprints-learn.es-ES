---
title: Modelo de activación de audiencia en línea / sin conexión
description: Activación de audiencia en línea / sin conexión.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
source-git-commit: f527b23587e4ec893532997c3c99270946d7fa31
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 77%

---

# Modelo de activación de audiencia en línea / sin conexión

Emplee atributos y eventos sin conexión, tales como pedidos sin conexión, transacciones, CRM o datos de fidelidad y comportamiento en línea para la segmentación y personalización en línea.

Active audiencias de destinos conocidos basados en perfiles, tales como proveedores de email, redes sociales y destinos de publicidad.

El modelo de Audience Activation en línea/sin conexión se alinea estrechamente con el modelo [Audiencia y Activación de perfil con aplicaciones de Experience Cloud](platform-and-applications.md). Se proporcionan detalles adicionales en [Audience and Profile Activation with Experience Cloud Applications Blueprint](platform-and-applications.md)   específico para integraciones entre aplicaciones de Experience Platform y de Experience Cloud.

## Casos de uso

* Segmentación de audiencia para audiencias conocidas en destinos sociales y de publicidad.
* Personalización en línea con atributos en línea y sin conexión.
* Activación de audiencias de canales conocidos, como email y SMS.

## Aplicaciones

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]

## Arquitectura

### Audience Activation en línea/sin conexión con destinos

<img src="assets/online_offline_activation.svg" alt="Arquitectura de referencia para el modelo de activación de audiencia en línea / sin conexión" style="border:1px solid #4a4a4a" />
<br>

## Guardas

[Consulte las protecciones tal como se describe en la página Información general sobre la activación de perfiles y audiencias .](overview.md)

## Pasos de implementación

1. [Crear esquemas para la ingesta de datos.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html)
1. [Crear conjuntos de datos para la ingesta de datos.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
1. [Configurar las identidades e identidad de áreas de nombres correctas en el esquema para asegurar que los datos ingeridos se puedan combinar en un perfil unificado.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)
1. [Habilite los esquemas y conjuntos de datos para el perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ingesta de datos a Experience Platform.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)
1. [Disponer el intercambio de segmentos de [!UICONTROL Real-time Customer Data Platform] entre Experience Platform y Audience Manager para que las audiencias definidas en Experience Platform se compartan con Audience Manager.](https://www.adobe.com/go/audiences)
1. [Cree ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=es) segmentos en el Experience Platform. El sistema determina automáticamente si el segmento debe ser evaluado por lotes o flujo.
1. [Configurar destinos para compartir atributos de perfil y pertenencias a audiencia a los destinos deseados.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html)

## Consideraciones sobre la implementación

* Compartir datos de perfil con los destinos requiere incluir un valor de identidad específico utilizado por el destino en su carga. Cualquier identidad requerida por el destino específico debe ingerirse en Platform y configurarse como identidad en [!UICONTROL Real-time Customer Profile].

* Para escenarios de activación donde las audiencias se comparten de Experience Platform a Audience Manager, todas las identidades incluidas en [!UICONTROL Real-time Customer Profile] se comparten con Audience Manager. Las audiencias de Experience Platform se pueden compartir a través de los destinos de Audience Manager cuando las identidades de destino necesarias se incluyan en [!UICONTROL Real-time Customer Profile] o cuando las identidades de [!UICONTROL Real-time Customer Profile] se relacionen con las identidades requeridas en destino, si están vinculadas en Audience Manager.

## Documentación relacionada

* Descripción del producto [[!UICONTROL Real-time Customer Data Platform]](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform.html)
* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Documentación de la segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Documentación de los destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=es)

## Vídeos y tutoriales relacionados

* Información general de [[!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=es)
* [Versión de prueba de [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=es)
* [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
