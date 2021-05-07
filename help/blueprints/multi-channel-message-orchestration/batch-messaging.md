---
title: Modelo de mensajería por lotes y Adobe Experience Platform
description: Ejecute campañas de mensajería programadas por lotes con Adobe Experience Platform como repositorio central de los perfiles de clientes y segmentación.
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
translation-type: tm+mt
source-git-commit: 01f70fe432d7be38b71889ae19c0d5fe4cf0f78a
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 84%

---

# Modelo de mensajería por lotes y Adobe Experience Platform

Ejecute campañas de mensajería programadas por lotes con Adobe Experience Platform como repositorio central de los perfiles de clientes y segmentación.

## Casos de uso

* Campañas programadas de email
* Campañas de incorporación y remarketing

## Aplicaciones

* Adobe Experience Platform
* Adobe Campaign Classic o Standard

## Patrones de integración

* Adobe Experience Platform → Adobe Campaign Classic
* Adobe Experience Platform → Adobe Campaign Standard

## Arquitectura

<img src="assets/aepbatch.svg" alt="Arquitectura de referencia del modelo de mensajería por lotes y Adobe Experience Platform" style="border:1px solid #4a4a4a" />

## Guardas

* Solamente compatible con la implementación de entidades organizativas únicas de Adobe Campaign
* Adobe Campaign es la fuente de información verídica de todos los perfiles activos, esto es, que los perfiles deben existir en Adobe Campaign y los nuevos no deben crearse según los segmentos de Experience Platform.
* La generación de pertenencia a segmento desde Experience Platform está implícita tanto en lotes (1 al día) como flujo (~5 minutos).

Compartir segmentos de **[!UICONTROL Real-time Customer Data Platform] con Adobe Campaign:**

* Recomendación: máximo de 20 segmentos.
* La activación se limita a cada 24 horas.
* Solo los atributos de esquemas de unión están disponibles para la activación (no es compatible con eventos array/maps/experience).
* Recomendación: máximo de 20 atributos por segmento.
* Un archivo por segmento de todos los perfiles con la pertenencia a segmento “realized” O si la pertenencia a segmento se añade como atributo en el archivo como perfiles “realized” y “exited” a la vez.
* Compatible con la exportación de segmentos incrementales o completos.
* No es compatible con la criptografía de archivos.
* Los flujos de trabajo de exportación de Adobe Campaign se ejecutan como máximo cada 4 horas.
* Consulte [los guardas de perfil e ingesta de datos de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)

## Pasos de implementación

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple según los datos ofrecidos por los clientes en Experience Platform.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html)
1. Crear esquemas de Adobe Campaign para: broadLog, trackingLog, direcciones no entregables y preferencias de perfil (opcional).
1. [Cree ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) conjuntos de datos en el Experience Platform para que se incorporen los datos.
1. [Agregue ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) etiquetas de uso de datos en el Experience Platform al conjunto de datos para su administración.
1. [Crear políticas que refuercen la gobernanza en los destinos.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html)

#### Perfil/identidad

1. [Crear áreas de nombres específicas para los clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Añadir identidades a los esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Habilite los esquemas y conjuntos de datos para Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Configure ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) directivas de combinación para diferentes vistas del Perfil del cliente en tiempo  [!UICONTROL real]  (opcional).
1. Crear segmentos para el uso en Adobe Campaign.

#### Origen/destino

1. [Realizar la ingesta de datos en Experience Platform mediante API de flujo y conectores de origen.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)
1. Configurar el destino de almacenamiento de los blobs de [!DNL Azure] para su uso con Adobe Campaign.

#### Implementación de aplicaciones móviles

1. Implementar el SDK de Adobe Campaign de Adobe Campaign Classic o el SDK Experience Platform de Adobe Campaign Standard. En el caso de contar con Experience Platform Launch, recomendamos utilizar la extensión de Adobe Campaign Classic o Adobe Campaign Standard con el SDK de Experience Platform.

#### Adobe Campaign

1. Configurar esquemas de perfil, datos de búsqueda y otros datos relevantes de personalización de entrega.

>[!IMPORTANT]
>
>Llegados a este punto, es esencial comprender qué es el modelo de datos de perfil y datos de evento en Experience Platform, para que pueda saber qué datos serán necesarios en Adobe Campaign.

#### Importar flujos de trabajo

1. Carga e ingesta de datos de perfiles simplificados al sFTP de Adobe Campaign.
1. Carga e ingesta de datos de organización y personalización de mensajería al sFTP de Adobe Campaign.
1. Ingesta de segmentos de Experience Platform desde los blobs de [!DNL Azure] a través de flujos de trabajo.

#### Exportar flujos de trabajo

1. Enviar registros de Adobe Campaign de vuelta a Experience Platform a través de flujos de trabajo a cada 4 horas (broadLog, trackingLog y direcciones no entregables).
1. Enviar preferencias de perfil de vuelta a Experience Platform a través de flujos de trabajo generados por consulta a cada 4 horas (opcional).


## Documentación relacionada

* [Documentación de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Documentación de Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=es)
* [Documentación de Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=es)
* [Documentación de Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=es)
* [Documentación del SDK Experience Platform Mobile](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
