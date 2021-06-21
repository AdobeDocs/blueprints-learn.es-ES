---
title: 'Journey Optimizer: mensajería activada y modelo de Adobe Experience Platform'
description: Ejecute mensajes y experiencias activadas con Adobe Experience Platform como sistema centralizado de transmisión de datos, perfiles de cliente y segmentación.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: dc13a1fe9a32f70497c5c73485618e6989b7a644
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 49%

---

# Journey Optimizer

Adobe Journey Optimizer es un sistema diseñado específicamente para que los equipos de marketing reaccionen en tiempo real a los comportamientos de los clientes y los cumplan donde se encuentran. Las funcionalidades de gestión de datos se han trasladado a Adobe Experience Platform, lo que permite a los equipos de marketing centrarse en lo que hacen mejor: que está creando conversaciones personalizadas y de recorrido de clientes de nivel mundial.  Este modelo describe las capacidades técnicas de la aplicación y proporciona una explicación profunda de los distintos componentes arquitectónicos que conforman Adobe Journey Optimizer.

## Casos de uso

* Mensajería activada
* Confirmaciones de registro
* Abandonos del carro de compras y formulario de solicitud
* Mensajería activada por localización

## Arquitectura

<img src="assets/journey-optimizer.png" alt="Arquitectura de referencia para el modelo de mensajería activada y Adobe Experience Platform" style="border:1px solid #4a4a4a" />

## Patrones de integración

* Adobe Experience Platform -> Journey Optimizer

## Prerrequisitos

1. El cliente debe estar aprovisionado para el Experience Cloud con una organización IMS válida
1. Push móvil

* El cliente debe tener un desarrollador móvil disponible para crear la aplicación
* SDK de Adobe Experience Platform Mobile
* Adobe Launch
   * Propiedad móvil
      * Extensiones:
         * Extensión de Adobe Journey Optimizer
         * Adobe Experience Platform Edge Network
         * Identidad
         * Núcleo móvil
         * Perfil
   * Configuraciones de aplicaciones
   * Datastreams
      * Habilitado para Experience Platform
      * Conjunto de datos de evento : se utiliza para recopilar el comportamiento móvil general.
      * Conjunto de datos de perfil: conjunto de datos de perfil push de AJO (no puede ser diferente)

## Guardas

* Consulte el enlace para obtener más información sobre las limitaciones
* Segmentos por lotes: debe asegurarse de comprender el volumen diario de usuarios cualificados y asegurarse de que el sistema de destino pueda gestionar el rendimiento por recorrido y en todos los recorridos
* Segmentos de transmisión: es necesario asegurarse de que se pueda gestionar la explosión inicial de cualificaciones de perfil junto con el volumen de clasificación de transmisión diaria por recorrido y en todos los recorridos
* Actividad de actualización de perfil: el perfil de cliente en tiempo real se puede actualizar de forma nativa desde un recorrido.  Se produce un retraso de hasta 1 minuto al procesar la actualización en el almacén de perfiles
* Eventos comerciales: se puede activar un recorrido basado en segmentos de lectura para que comience a partir de una llamada externa al sistema JO
* De forma nativa solo admite el Offer decisioning en los mensajes. Compatibilidad futura mediante acción nativa
* Canales admitidos:
   * Correo electrónico
   * Push (FCM/APNS)
   * Puntos finales de API de Rest
* Procesa 5.000 eventos por segundo con escalado horizontal (la cartera es una limitación)
* La prueba A/B se realiza utilizando dos envíos y determinando los resultados mediante QS o CJA
* Integración de Litmus: debe tener una cuenta con Litmus para aprovechar la integración

## Pasos de implementación

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html?lang=es) según los datos ofrecidos por los clientes en Experience Platform.
1. Crear esquemas de Adobe Campaign para: broadLog, trackingLog, direcciones no entregables y preferencias de perfil (opcional).
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) en Experience Platform para la ingesta.
1. [Añadir etiquetas de uso de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=es) al conjunto de datos de Experience Platform para la gobernanza.
1. [Crear políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=es) que refuercen la gobernanza en los destinos.

#### Perfil/identidad

1. [Crear áreas de nombres específicas para los clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Añadir identidades a los esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Configurar políticas de fusión](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=es) para diferenciar las vistas de [!UICONTROL Real-time Customer Profile] (opcional).
1. Crear segmentos para el uso en campañas.

#### Origen/destino

1. [Realizar la ingesta de datos en Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) utilizando las API de flujo y conectores de origen.1. Configurar el destino de almacenamiento de los blobs de [!DNL Azure] para su uso con Adobe Campaign.

#### Implementación de aplicaciones móviles

1. Implementar el SDK de Adobe Campaign de Adobe Campaign Classic o el SDK Experience Platform de Adobe Campaign Standard. En el caso de contar con Experience Platform Launch, recomendamos utilizar la extensión de Adobe Campaign Classic o Adobe Campaign Standard con el SDK de Experience Platform.


### Journey Orchestration

1. Los datos de flujo utilizados para iniciar un recorrido de cliente deben configurarse primero en Journey Optimizer para obtener un ID de organización. Este ID de organización debe entregarse al desarrollador para usarse con la ingesta.
1. Configurar orígenes externos de datos.
1. Configurar acciones personalizadas.

## Documentación relacionada

* [Documentación de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Documentación de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=es)
* [Documentación de Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=es)
* [Documentación del SDK Experience Platform Mobile](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
