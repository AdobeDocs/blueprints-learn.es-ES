---
title: Real-Time CDP con [!DNL Campaign] v7 y patrón de integración de Campaign Standard
description: Muestra cómo Adobe Experience Platform y su herramienta de segmentación centralizada y el Perfil del cliente en tiempo real se pueden utilizar con Adobe [!DNL Campaign] para ofrecer conversaciones personalizadas.
solution: Real-Time Customer Data Platform, [!DNL Campaign]
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
source-git-commit: 258aea64f6ff2f620b1adaa0c9ba4b02b47acce9
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 42%

---

# [!DNL Real-Time Customer Data Platform] con [!DNL Campaign] patrón de integración

Muestra cómo el Adobe [!DNL Experience Platform] y su herramienta de segmentación centralizada y el Perfil del cliente en tiempo real se pueden utilizar con Adobe [!DNL Campaign] para ofrecer conversaciones personalizadas.

## Aplicaciones

* Adobe[!DNL Experience Platform Real-Time Customer Data Platform]
* Adobe [!DNL Campaign] v7 o [!DNL Campaign Standard]

## Arquitectura

<img src="assets/rtcdp-campaign-architecture.svg" alt="Arquitectura de referencia del patrón de integración de Adobe Experience Platform y mensajería por lotes" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Prerrequisitos

* EXPERIENCE PLATFORM y [!DNL Campaign] Se recomienda aprovisionar en la misma organización de IMS y utilizar Adobe Admin Console para el acceso de los usuarios. Esto también garantiza que los clientes puedan utilizar el conmutador de soluciones desde la interfaz de usuario de marketing

## Guardas

Las secciones siguientes describen las barreras para esta integración.

### Adobe[!DNL Campaign]

* Solo admite Adobe [!DNL Campaign] implementaciones de una sola unidad organizativa
* Adobe [!DNL Campaign] es la fuente fiable para todos los perfiles activos, lo que significa que los perfiles deben existir en el Adobe [!DNL Campaign] y no se deben crear nuevos perfiles basados en segmentos del Experience Platform.
* [!DNL Campaign] exportar flujos de trabajo para que se ejecuten como máximo cada 4 horas
* Esquema XDM y conjuntos de datos para Adobe [!DNL Campaign] broadLog, trackingLogs y las direcciones no permitidas no están predeterminadas y deben diseñarse y crearse

### Uso compartido de segmentos en Real-time Customer Data Platform

* Consulte RTCDP [!DNL Campaign] Conector de destino - [Conexión de campaña RTCDP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=es)

* Consulte [Protecciones predeterminadas para [!DNL Real-Time Customer Profile Data] y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)

## Pasos de implementación

Las secciones siguientes describen los pasos de las implementaciones para cada aplicación.

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=es) según los datos ofrecidos por los clientes en Experience Platform.
1. Crear Adobe [!DNL Campaign] esquemas para broadLog, trackingLog, direcciones no entregables y preferencias de perfil (opcional).
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) en Experience Platform para la ingesta.
1. [Añadir etiquetas de uso de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=es) al conjunto de datos de Experience Platform para la gobernanza.
1. [Crear políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=es) que refuercen la gobernanza en los destinos.

#### Perfil/identidad

1. [Crear áreas de nombres específicas para los clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Añadir identidades a los esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Configurar políticas de fusión](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=es) para diferenciar las vistas de [!UICONTROL Real-Time Customer Profile] (opcional).
1. Creación de segmentos para el Adobe [!DNL Campaign] uso.

#### Orígenes/destinos

1. [EXPERIENCE PLATFORM y [!DNL Campaign] Fuentes y destinos estándar](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=es)
1. [EXPERIENCE PLATFORM y [!DNL Campaign] Fuentes y destinos v7](https://experienceleague.adobe.com/docs/campaign-classic/using/integrating-with-adobe-experience-cloud/aep-sources-destinations/get-started-sources-destinations.html?lang=es)
1. [Incorporar datos en Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) mediante API de flujo y conectores de origen.
1. Configurar [!DNL Azure] destino de almacenamiento de blob para su uso con Adobe [!DNL Campaign].

#### Adobe[!DNL Campaign]

1. Configurar esquemas de perfil, datos de búsqueda y otros datos relevantes de personalización de entrega.

>[!IMPORTANT]
>
>En este punto, es fundamental comprender qué es el modelo de datos dentro del Experience Platform para los datos de perfil y evento, de modo que sepa qué datos se necesitarán en el Adobe [!DNL Campaign].

#### Importar flujos de trabajo

1. Carga e ingesta de datos de perfil simplificados en el Adobe [!DNL Campaign] sFTP.
1. Carga e ingesta de datos de personalización de mensajería y orquestación en el Adobe [!DNL Campaign] sFTP.
1. Ingesta de segmentos de Experience Platform desde los blobs de [!DNL Azure] a través de flujos de trabajo.

#### Exportar flujos de trabajo

1. Enviar Adobe [!DNL Campaign] vuelve a iniciar sesión en el Experience Platform a través de flujos de trabajo cada cuatro horas (broadLog, trackingLog, direcciones no entregables).
1. Enviar preferencias de perfil de vuelta a Experience Platform a través de flujos de trabajo generados por consulta cada 4 horas (opcional).

### Configuración push móvil

* Dos enfoques compatibles para la integración con dispositivos móviles para notificaciones push:
   * SDK móvil de Experience Platform
   * [!DNL Campaign] Mobile SDK
* Ruta del SDK móvil de Experience Platform:
   * Aproveche las etiquetas de Adobe y [!DNL Campaign Classic] extensión para configurar la integración con el SDK de Experience Platform Mobile
   * Se necesita un conocimiento práctico de las etiquetas de Adobe y la recopilación de datos
   * Se necesita experiencia de desarrollo móvil con notificaciones push en Android y iOS para implementar el SDK, integrarse con FCM (Android) y APNS (iOS) para obtener un token push, configurar la aplicación para recibir notificaciones push y gestionar interacciones push
* [!DNL Campaign] Mobile SDK
   * Consulte la [Documentación del SDK de Campaign Classic](https://developer.adobe.com/client-sdks/solution/adobe-campaign-classic/)

>[!IMPORTANT]
>
>Si implementa la variable [!DNL Campaign] Los SDK y están trabajando con otras aplicaciones de Experience Cloud; requerirán el uso del SDK de Experience Platform Mobile para la recopilación de datos. Esto creará llamadas de cliente duplicadas en el dispositivo.

## Documentación relacionada

* [Adobe [!DNL Experience Platform] documentación](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [[!DNL Campaign Classic] documentación](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=es)
* [[!DNL Campaign Standard] documentación](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=es)
* [[!DNL Experience Platform] Documentación de Launch](https://experienceleague.adobe.com/docs/launch.html?lang=es)
* [[!DNL Experience Platform] Documentación del SDK móvil](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
