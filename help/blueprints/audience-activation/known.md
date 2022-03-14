---
title: Activación de cliente conocida
description: Activación de audiencia en línea/sin conexión.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
source-git-commit: 20dd657a85ffeb8ae2f160855369643c2f2743bb
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Modelo conocido de activación del cliente

Emplee atributos y eventos sin conexión, tales como pedidos sin conexión, transacciones, CRM o datos de fidelidad y comportamiento en línea para la segmentación y personalización en línea.

Los identificadores ampliados con controles de control integrados ofrecen más oportunidades de comunicarse con clientes conocidos. Active audiencias de destinos conocidos basados en perfiles, tales como proveedores de email, redes sociales y destinos de publicidad.

La información adicional ofrecida en el [modelo de activación de audiencias y perfiles con las aplicaciones de Experience Cloud](platform-and-applications.md) es específica de la integración entre Experience Platform y las aplicaciones de Experience Cloud.

## Casos de uso

* Segmentación de audiencia para audiencias conocidas en destinos sociales y de publicidad.
* Personalización en línea con atributos en línea y sin conexión.
* Activación de audiencias de canales conocidos, como email y SMS.

## Aplicaciones

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]

## Arquitectura

### Activación con datos en línea y sin conexión con destinos

<img src="assets/online_offline_activation.svg" alt="Arquitectura de referencia para el modelo de activación de audiencia en línea/sin conexión" style="width:80%; border:1px solid #4a4a4a" />
<br>

## Guardas

[Consulte los guardas definidos en la página de información general sobre la activación de audiencias y perfiles](overview.md).

## Pasos de implementación

1. [Crear esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) para la ingesta de datos.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) para la ingesta de datos.
1. [Configurar las identidades e identidad de áreas de nombres correctas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es) en el esquema para asegurar que los datos ingestados se puedan combinar en un perfil unificado.
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Ingesta de datos](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) a Experience Platform.
1. [Disponer el intercambio de segmentos de [!UICONTROL Real-time Customer Data Platform]](https://www.adobe.com/go/audiences) entre Experience Platform y Audience Manager para que las audiencias definidas en Experience Platform se compartan con Audience Manager.
1. [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=es) en Experience Platform. El sistema determina automáticamente si el segmento debe ser evaluado por lotes o streaming.
1. [Configurar destinos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html?lang=es) para compartir atributos de perfil y pertenencias a audiencia a los destinos deseados.

## Consideraciones sobre la implementación

* Compartir datos de perfil con los destinos requiere incluir un valor de identidad específico utilizado por el destino en su carga. Cualquier identidad que requiera el destino específico debe ingerirse en Platform y configurarse como identidad en [!UICONTROL Real-time Customer Profile].

* Consulte la [Modelo de activación de audiencias y perfiles con aplicaciones Experience Cloud](platform-and-applications.md) para obtener más información sobre cómo compartir audiencias de Real-time Customer Data Platform con Audience Manager, Analytics, Target, Campaign y Journey Optimizer.

## Documentación relacionada

* Descripción del producto [[!UICONTROL Real-time Customer Data Platform]](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform.html)
* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Documentación de la segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Documentación de los destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=es)

## Vídeos y tutoriales relacionados

* Información general de [[!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=es)
* [Versión de prueba de [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=es)
* [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)