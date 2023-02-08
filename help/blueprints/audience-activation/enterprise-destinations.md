---
title: Modelo de activación de audiencias y perfiles en destinos de streaming empresarial y de archivos
description: Activación de audiencias y perfiles en destinos empresariales
solution: Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5
source-git-commit: 0d1bb41eb6b70be7c3c8a3196c9974a0d7807404
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 100%

---

# Modelo de activación de audiencias y perfiles en destinos de streaming empresarial y de archivos

Comparta cambios y eventos de perfil y audiencia por streaming o lotes de [!UICONTROL Real-Time Customer Data Platform] a aplicaciones y almacenes de datos empresariales. Estos eventos de perfil y audiencia se pueden utilizar para iniciar una acción de ventas o asistencia al cliente, como realizar el seguimiento de un proceso abandono de aplicación, un registro en un seminario web o actualizar aplicaciones empresariales con los últimos atributos de cliente e inteligencia de [!UICONTROL Real-Time Customer Data Platform].

## Casos de uso

* Activación de perfiles y audiencias a destinos de almacenamiento en la nube o destinos de streaming para el seguimiento, almacenamiento, análisis y activación de datos del cliente por parte de la empresa.

## Aplicaciones

* Adobe Experience Platform    Activation

## Arquitectura

<img src="assets/known_activation.svg" alt="Arquitectura de referencia para el escenario de activación empresarial" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />


## Guardas

[Consulte los guardas definidos en la página de información general sobre la activación de audiencias y perfiles.](overview.md)

## Pasos de implementación

1. [Crear esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=es) para la ingesta de datos.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) para la ingesta de datos.
1. [Configurar las identidades e identidad de áreas de nombres correctas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es) en el esquema para asegurar que los datos ingestados se puedan combinar en un perfil unificado.
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Ingesta de datos](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) a Experience Platform.
1. [Disponer el intercambio de segmentos de [!UICONTROL Real-Time Customer Data Platform]](https://www.adobe.com/go/audiences) entre Experience Platform y Audience Manager para que las audiencias definidas en Experience Platform se compartan con Audience Manager.
1. [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=es) en Experience Platform. El sistema determina automáticamente si el segmento debe ser evaluado por lotes o streaming.
1. [Configurar destinos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html?lang=es) para compartir atributos de perfil y pertenencias a audiencia a los destinos deseados.

## Documentación relacionada

* [Documentación de los destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=es)
* [Información general sobre los destinos de almacenamiento en la nube](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=es#catalog)
* [Destino HTTP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=es#overview)
* Descripción del producto [[!UICONTROL Real-Time Customer Data Platform]](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform.html)
* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Documentación de la segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)

## Vídeos y tutoriales relacionados

* Información general de [[!UICONTROL Real-Time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=es)
* [Versión de prueba de [!UICONTROL Real-Time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=es)
* [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=es)
