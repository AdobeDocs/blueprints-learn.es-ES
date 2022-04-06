---
title: Patrón de integración de Real-Time CDP con Adobe Campaign
description: Muestra cómo se puede utilizar el perfil del cliente en tiempo real de Adobe Experience Platform y su herramienta de segmentación centralizada con Adobe Campaign para ofrecer conversaciones personalizadas.
solution: Real-time Customer Data Platform, Campaign
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
source-git-commit: 24d5ec498d09f6dac443561bd530d58a33dae7af
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 100%

---

# Patrón de integración de Real-Time CDP con Adobe Campaign

Muestra cómo se puede utilizar el perfil del cliente en tiempo real de Adobe Experience Platform y su herramienta de segmentación centralizada con Adobe Campaign para ofrecer conversaciones personalizadas.

<br>

## Aplicaciones

* Adobe Experience Platform Real-Time CDP
* Adobe Campaign v7 o Campaign Standard

<br>

## Arquitectura

<img src="assets/rtcdp-campaign-architecture.svg" alt="Arquitectura de referencia del patrón de integración de Adobe Experience Platform y mensajería por lotes" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Prerrequisitos

* Se recomienda que Experience Platform y Campaign estén aprovisionados en la misma organización de IMS y que utilicen Adobe Admin Console para el acceso de los usuarios. Esto también garantiza que los clientes puedan utilizar el conmutador de soluciones desde la interfaz de usuario de marketing

<br>

## Guardas

### Adobe Campaign

* Solamente compatible con la implementación de entidades organizativas únicas de Adobe Campaign
* Adobe Campaign es la fuente de información verídica de todos los perfiles activos, esto es, que los perfiles deben existir en Adobe Campaign y los nuevos no deben crearse según los segmentos de Experience Platform.
* Los flujos de trabajo de exportación de Campaign se ejecutan como máximo cada 4 horas.
* El esquema XDM y los conjuntos de datos para broadLog, trackingLogs y direcciones que no se pueden enviar de Adobe Campaign no están listos para usar y deben diseñarse y crearse

### Uso compartido de segmentos de CDP de Experience Platform

* Recomendación: máximo de 20 segmentos.
* La activación se limita a cada 24 horas.
* Solo los atributos de esquemas de unión están disponibles para la activación (no es compatible con eventos array/maps/experience)
* Recomendación: máximo de 20 atributos por segmento.
* Un archivo por segmento de todos los perfiles con la pertenencia a segmento “realized” O si la pertenencia a segmento se añade como atributo en el archivo como perfiles “realized” y “exited” a la vez.
* Compatible con la exportación de segmentos incrementales y completos.
* No es compatible con la criptografía de archivos.

<br>

## Pasos de implementación

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) según los datos ofrecidos por los clientes en Experience Platform.
1. Crear esquemas de Adobe Campaign para broadLog, trackingLog, direcciones que no se pueden enviar y preferencias de perfil (opcional).
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) en Experience Platform para la ingesta.
1. [Añadir etiquetas de uso de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=es) al conjunto de datos de Experience Platform para la gobernanza.
1. [Crear políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=es) que refuercen la gobernanza en los destinos.

#### Perfil/identidad

1. [Crear áreas de nombres específicas para los clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Añadir identidades a los esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Configurar políticas de fusión](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=es) para diferenciar las vistas de [!UICONTROL Real-time Customer Profile] (opcional).
1. Crear segmentos para el uso en Adobe Campaign.

#### Origen/destino

1. [Incorporar datos en Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) mediante API de flujo y conectores de origen.
1. Configurar el destino de almacenamiento de los blobs de [!DNL Azure] para su uso con Adobe Campaign.

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

1. Enviar registros de Adobe Campaign de vuelta a Experience Platform a través de flujos de trabajo cada 4 horas (broadLog, trackingLog y direcciones que no se pueden enviar).
1. Enviar preferencias de perfil de vuelta a Experience Platform a través de flujos de trabajo generados por consulta cada 4 horas (opcional).


### Configuración push móvil

* Dos enfoques compatibles para la integración con dispositivos móviles para notificaciones push:
   * SDK móvil de Experience Platform
   * SDK móvil de Campaign
* Ruta del SDK móvil de Experience Platform:
   * Aproveche las etiquetas de Adobe y la extensión de Campaign Classic para configurar la integración con el SDK móvil de Experience Platform
   * Se necesita un conocimiento práctico de las etiquetas de Adobe y la recopilación de datos
   * Se necesita experiencia de desarrollo móvil con notificaciones push en Android y iOS para implementar el SDK, integrarse con FCM (Android) y APNS (iOS) para obtener un token push, configurar la aplicación para recibir notificaciones push y gestionar interacciones push
* SDK móvil de Campaign
   * Siga la [Documentación del SDK de Campaign] (SDK móvil de Campaign Siga la documentación de implementación aquí descrita)

   >[!IMPORTANT]
   >Si implementa el SDK de Campaign y trabaja con otras aplicaciones de Experience Cloud, será necesario utilizar el SDK móvil de Experience Platform para la recopilación de datos. Esto creará llamadas de cliente duplicadas en el dispositivo.

## Documentación relacionada

* [Documentación de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Documentación de Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=es)
* [Documentación de Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=es)
* [Documentación de Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=es)
* [Documentación del SDK móvil de Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
