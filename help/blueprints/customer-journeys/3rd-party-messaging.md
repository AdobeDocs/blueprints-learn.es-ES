---
title: 'Journey Optimizer: modelo de mensajería de terceros'
description: Muestra cómo se puede utilizar Adobe Journey Optimizer con sistemas de mensajería de terceros para organizar y enviar comunicaciones personalizadas.
solution: Experience Platform, Journey Optimizer
hidefromtoc: true
source-git-commit: a86df4a1b2de38bcb244a6afe1cea87adc7e26fa
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 35%

---

# Mensajería de terceros

Muestra cómo se puede utilizar Adobe Journey Optimizer con sistemas de mensajería de terceros para organizar y enviar comunicaciones personalizadas.

<br>

## Arquitectura

<img src="assets/3rd-party-messaging-architecture.svg" alt="Arquitectura de referencia modelo de Journey Optimizer" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Prerrequisitos

Adobe Experience Platform

* Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar las fuentes de datos de Journey Optimizer
* Para los esquemas basados en clases de eventos de experiencia, agregue el grupo de campos &quot;ID de evento de orquestación&quot; cuando desee que se active un evento que no sea un evento basado en reglas
* Para los esquemas basados en clases de Perfil individual, agregue el grupo de campos &quot;Detalles de prueba de perfil&quot; para poder cargar perfiles de prueba para utilizarlos con Journey Optimizer

Aplicación de mensajería de terceros

* Debe admitir llamadas de API de REST para enviar cargas transaccionales

<br>

## Guardas

[Vínculo del producto de Journey Optimizer Guardrade](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=es)

Protecciones adicionales de Journey Optimizer:

* El límite está disponible a través de la API para garantizar que el sistema de destino no se satura hasta el punto de error. Esto significa que los mensajes que superen el límite se perderán completamente y nunca se enviarán. No se admite la restricción.
   * Máximo de conexiones : número máximo de conexiones http/s que un destino puede gestionar
   * Recuento máximo de llamadas : número máximo de llamadas que se realizan en el parámetro periodInMs
   * periodInMs: tiempo en milisegundos
* Los recorridos iniciados por pertenencia a segmentos pueden funcionar de dos modos:
   * Segmentos por lotes (se actualizan cada 24 horas)
   * Segmentos de transmisión (calificación de &lt;5 minutos)
* Segmentos por lotes: debe conocer el volumen diario de usuarios adecuados y garantizar que el sistema de destino pueda soportar el pico de rendimiento por recorrido y durante todos los recorridos.
* Segmentos por flujo: debe asegurarse de que el pico inicial de calificaciones de perfil pueda gestionarse junto con el volumen de calificación de flujo diario por recorrido y durante todos los recorridos.
* offer decisioning no admitido
* Integraciones salientes a sistemas de terceros
   * No es compatible con una sola IP estática, ya que nuestra infraestructura es de varios inquilinos (debe realizar la lista de permitidos de todas las IP del centro de datos)
   * Solo se admiten métodos de PUT y POST para acciones personalizadas
   * Compatibilidad con autenticación: token | contraseña | OAuth2
* No es posible empaquetar y mover componentes individuales de Adobe Experience Platform o Journey Optimizer entre varios entornos limitados. Debe volver a implementarse en nuevos entornos

<br>

Sistema de mensajería de terceros

* Necesidad de comprender qué carga puede soportar el sistema para las llamadas de API transaccionales
   * Número de llamadas permitidas por segundo
   * Número de conexiones
* Necesita comprender qué autenticación se requiere para realizar llamadas de API
   * Tipo de autenticación:  token | contraseña | OAuth2 es compatible con Journey Optimizer
   * Duración de la caché de autenticación:  ¿durante cuánto tiempo es válido el token? 
* Si la ingesta por lotes solo es compatible, entonces debe transmitirse a un motor de almacenamiento en la nube como Amazon Kinesis o Azure Event Grid 1st
   * Los datos se pueden agrupar por lotes de estos motores de almacenamiento en la nube y canalizar a terceros
   * Cualquier middleware requerido sería responsabilidad del cliente o de terceros de proporcionar

<br>

## Pasos de implementación

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) según los datos ofrecidos por los clientes en Experience Platform.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) en Experience Platform para la ingesta.
1. [Añadir etiquetas de uso de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=es) al conjunto de datos de Experience Platform para la gobernanza.
1. [Crear políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=es) que refuercen la gobernanza en los destinos.

#### Perfil/identidad

1. [Crear áreas de nombres específicas para los clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Añadir identidades a los esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Configurar políticas de fusión](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=es) para diferenciar las vistas de [!UICONTROL Real-time Customer Profile] (opcional).
1. Cree segmentos para el uso del Recorrido.

#### Origen/destino

1. [Realizar la ingesta de datos en Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) mediante API de flujo y conectores de origen.

### Journey Optimizer

1. Configure la fuente de datos del Experience Platform y determine qué campos deben almacenarse en caché como parte de los datos profileStreaming utilizados para iniciar un recorrido del cliente. Primero debe configurarse en Journey Optimizer para obtener un ID de organización. Este ID de organización debe entregarse al desarrollador para usarse con la ingesta
1. Configurar orígenes externos de datos
1. Configurar acciones personalizadas para aplicaciones de terceros

### Configuración push móvil (opcional, ya que terceros pueden recopilar tokens)

1. Implemente el SDK de Experience Platform Mobile para recopilar tokens push e información de inicio de sesión con el fin de volver a perfiles de cliente conocidos
1. Aproveche las etiquetas de Adobe y cree una propiedad móvil con la siguiente extensión:
   * Adobe Journey Optimizer
   * Adobe Experience Platform Edge Network
   * Identidad para la red perimetral
   * Núcleo móvil
1. Asegúrese de tener un conjunto de datos dedicado para implementaciones de aplicaciones móviles vs. implementaciones web
1. Para obtener más información, siga la [Guía móvil de Adobe Journey Optimizer](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

<br>

## Documentación relacionada

* [documentación del Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Documentación del SDK Experience Platform Mobile](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
* [Documentación de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es)
* [Descripción del producto de Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
