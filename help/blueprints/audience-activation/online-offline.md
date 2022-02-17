---
title: Activación con modelo de datos en línea y sin conexión
description: Activación de audiencia en línea/sin conexión.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
source-git-commit: 53ef83cbaa9dde0793e379c0044f449cfca078ab
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 79%

---

# Activación con modelo de datos en línea y sin conexión

Emplee atributos y eventos sin conexión, tales como pedidos sin conexión, transacciones, CRM o datos de fidelidad y comportamiento en línea para la segmentación y personalización en línea.

Active audiencias de destinos conocidos basados en perfiles, tales como proveedores de email, redes sociales y destinos de publicidad.

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

<img src="assets/online_offline_activation.svg" alt="Arquitectura de referencia para el modelo de activación de audiencia en línea / sin conexión" style="width:80%; border:1px solid #4a4a4a" />
<br>

## Guardas

[Consulte los guardas definidos en la página de información general sobre la activación de audiencias y perfiles.](overview.md)

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

### Uso compartido de audiencias de Real-time Customer Data Platform con Audience Manager

* La pertenencia a audiencias de RT-CDP se comparte con Audience Manager de forma continua en cuanto se completa la evaluación de segmentos y se escribe en el perfil del cliente en tiempo real, independientemente de si la evaluación de segmentos se produce en lote o en flujo continuo. Si el perfil cualificado contiene la información de enrutamiento regional para dispositivos de perfil relacionados, la pertenencia a audiencias de RT-CDP se clasifica en modo de flujo continuo en Audience Manager Edge asociado. Si la información de enrutamiento regional se aplicó a un perfil con una marca de tiempo en los últimos 14 días, se evaluará en el borde del Audience Manager en streaming. Si los perfiles de RTCDP no contienen información de enrutamiento regional o si la información de enrutamiento regional tiene buenos 14 días, las pertenencias de perfil se envían a la ubicación de concentrador de Audience Manager para la evaluación y activación basadas en lotes. Los perfiles aptos para la activación de Edge se activarán en cuestión de minutos después de la calificación del segmento de RTCDP, los perfiles que no cumplen los requisitos para la activación de Edge se clasificarán en el centro de Audience Manager y pueden tener un intervalo de tiempo de 12 a 24 horas para el procesamiento.

* La información de enrutamiento regional en la que se almacena el perfil de Audience Manager de Edge se puede recopilar al Experience Platform desde el Audience Manager, el servicio de ID de visitante, Analytics, Launch o directamente desde el SDK web como un conjunto de datos de clase de registro de perfil independiente mediante el grupo de campos XDM &quot;información de región de captura de datos&quot;.

* En los casos de activación en los que las audiencias se comparten de Experience Platform a Audience Manager, las siguientes identidades se comparten automáticamente: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Actualmente, las áreas de nombres de los clientes no se comparten.

Las audiencias de Experience Platform se pueden compartir a través de los destinos de Audience Manager cuando las identidades de destino necesarias se incluyan en [!UICONTROL Real-time Customer Profile] o cuando las identidades de [!UICONTROL Real-time Customer Profile] se relacionen con las identidades requeridas en destino, si están vinculadas en Audience Manager.

## Documentación relacionada

* Descripción del producto [[!UICONTROL Real-time Customer Data Platform]](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform.html)
* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Documentación de la segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Documentación de los destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=es)

## Vídeos y tutoriales relacionados

* Información general de [[!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=es)
* [Versión de prueba de [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=es)
* [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
