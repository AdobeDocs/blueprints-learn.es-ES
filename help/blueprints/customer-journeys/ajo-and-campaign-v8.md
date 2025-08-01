---
title: Modelo de Journey Optimizer con Adobe Campaign v8
description: Muestra cómo se puede utilizar Adobe Journey Optimizer con Adobe Campaign para enviar mensajes de forma nativa utilizando el servidor de mensajería en tiempo real en Campaign
solution: Journey Optimizer, Campaign, Campaign v8, Campaign v8 Client Console
version: Campaign v8, Campaign v8 Client Console
exl-id: 447a1b60-f217-4295-a0df-32292c4742b0
source-git-commit: 75a0f2a77f39a4320dc4c4b0db918879be099dd3
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 63%

---

# Modelo de Journey Optimizer con Adobe Campaign v8

Muestra cómo se puede usar Adobe [!DNL Journey Optimizer] con Adobe [!DNL Campaign] para enviar mensajes de forma nativa mediante el servidor de mensajería en tiempo real de [!DNL Campaign].

## Arquitectura

<img src="assets/ajo-campaign-architecture.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

>[!IMPORTANT]
>El uso de Journey Optimizer y Campaign para enviar mensajes de forma independiente entre sí es posible, pero tiene algunas consideraciones técnicas que se deben tener en cuenta. Si desea seguir esta ruta, póngase en contacto con su arquitecto empresarial de preventa para asegurarse de que comprende lo que se necesitará para admitir la implementación.

## Prerrequisitos

Revise los siguientes requisitos previos para cada aplicación.

### Adobe Experience Platform     

* Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar las fuentes de datos de Journey Optimizer
* Para los esquemas basados en clases de eventos de experiencia, agregue el grupo de campos &#39;ID de evento de orquestación&#39; cuando desee que se active un evento que no sea un evento basado en reglas
* Para los esquemas basados en clases de perfil individual, agregue el grupo de campos &#39;Detalles de prueba de perfil&#39; para poder cargar perfiles de prueba para utilizarlos con Journey Optimizer
* Journey Optimizer y Campaign se aprovisionan en la misma organización de IMS

### Campaign v8

* La instancia de ejecución del servicio de mensajería en tiempo real (es decir, el Centro de mensajes) debe estar alojada por Adobe Managed Cloud Services
* Toda la creación de mensajes se realiza dentro de la propia instancia de Campaign

## Guardas

* [Limitaciones de productos de la protección de Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)

* [Protecciones e instrucciones de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html)

## Pasos de implementación

Siga las implementaciones para cada aplicación que se describen a continuación.

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=es) según los datos ofrecidos por los clientes en Experience Platform.
1. (Opcional) Cree esquemas basados en clases de Experience Event para las tablas broadLog, trackingLog y direcciones no entregables de Adobe Campaign.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) en Experience Platform para la ingesta.
1. [Añadir etiquetas de uso de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=es) al conjunto de datos de Experience Platform para la gobernanza.
1. [Crear políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=es) que refuercen la gobernanza en los destinos.

#### Perfil/identidad

1. [Crear áreas de nombres específicas para los clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Añadir identidades a los esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Configurar políticas de fusión](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=es) para diferenciar las vistas de [!UICONTROL Real-Time Customer Profile] (opcional).
1. Crear segmentos para el uso de Journey.

#### Orígenes/destinos

1. [Ingesta de datos en [!DNL Experience Platform]](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=es) mediante la transmisión de API y conectores de origen.

### Journey Optimizer  

1. Configure su origen de datos [!DNL Experience Platform] y determine qué campos deben almacenarse en caché como parte del perfil. Los datos de streaming utilizados para iniciar un recorrido de cliente deben configurarse primero en Journey Optimizer para obtener un ID de orquestación. Este ID de organización debe entregarse al desarrollador para usarse con la ingesta.
1. Configurar orígenes externos de datos.
1. Configure acciones personalizadas para la instancia de Campaign.

### Campaign v8

* Las plantillas de mensajería deben configurarse con el contexto de personalización adecuado.
* Para el estándar [!DNL Campaign]: es necesario configurar los flujos de trabajo de exportación para exportar los registros de mensajería transaccional de nuevo a Experience Platform. La recomendación es que se ejecute como máximo cada cuatro horas.
* Para [!DNL Campaign] v8.4 es posible aprovechar el conector Adobe [!DNL Campaign] Managed Services Source en Experience Platform para sincronizar los eventos de envío y seguimiento de Campaign en Experience Platform. Consulte la documentación de [Source Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=es) para obtener detalles.

### Configuración push móvil (opcional)

1. Implemente [!DNL Experience Platform] Mobile SDK para recopilar tokens push e información de inicio de sesión con el fin de vincularlos a perfiles de clientes conocidos.
1. Aproveche las etiquetas de Adobe y cree una propiedad móvil con la siguiente extensión:
   * Adobe [!DNL Journey Optimizer] | Adobe [!DNL Campaign Classic] | Adobe [!DNL Campaign Standard]
   * Adobe [!DNL Experience Platform] [!DNL Edge Network]
   * Identidad de [!DNL Edge Network]
   * Núcleo móvil
1. Asegúrese de tener un flujo de datos dedicado para implementaciones de aplicaciones móviles en lugar de implementaciones web.
1. Para obtener más información, consulte la [Guía de Adobe Journey Optimizer Mobile](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer/push-notification/).

   >[!IMPORTANT]
   >Puede que sea necesario recopilar los tokens móviles tanto en Journey Optimizer como en Campaign si se desea enviar comunicaciones en tiempo real a través de Journey Optimizer y notificaciones push por lotes a través de Campaign. Campaign v8 requiere el uso exclusivo del SDK de Campaign para capturar tokens push.

## Documentación relacionada

* [Documentación de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es)
* [Descripción del producto Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
* [Documentación de Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=es)
