---
title: Modelo de Journey Optimizer con Adobe Campaign v8
description: Muestra cómo se puede utilizar Adobe Journey Optimizer con Adobe Campaign para enviar mensajes de forma nativa utilizando el servidor de mensajería en tiempo real en Campaign
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: 447a1b60-f217-4295-a0df-32292c4742b0
source-git-commit: 5110ee2a7a079945475055cbcfdabf7cdcaa0ab5
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 100%

---

# Journey Optimizer con Adobe Campaign    v8  modelo

Muestra cómo se puede utilizar Adobe Journey Optimizer con Adobe Campaign para enviar mensajes de forma nativa utilizando el servidor de mensajería en tiempo real en Campaign.

<br>

## Arquitectura

<img src="assets/ajo-campaign-architecture.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

>[!IMPORTANT]
>El uso de Journey Optimizer y Campaign para enviar mensajes de forma independiente entre sí es posible, pero tiene algunas consideraciones técnicas que se deben tener en cuenta. Si desea seguir esta ruta, póngase en contacto con su arquitecto empresarial de preventa para asegurarse de que comprende lo que se necesitará para admitir la implementación.

<br>

## Prerrequisitos

### Adobe Experience Platform

* Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar las fuentes de datos de Journey Optimizer
* Para los esquemas basados en clases de eventos de experiencia, agregue el grupo de campos &#39;ID de evento de orquestación&#39; cuando desee que se active un evento que no sea un evento basado en reglas
* Para los esquemas basados en clases de perfil individual, agregue el grupo de campos &#39;Detalles de prueba de perfil&#39; para poder cargar perfiles de prueba para utilizarlos con Journey Optimizer
* Journey Optimizer y Campaign se aprovisionan en la misma organización de IMS

### Campaign v8

* La instancia de ejecución del servicio de mensajería en tiempo real (es decir, el Centro de mensajes) debe estar alojada por Adobe Managed Cloud Services
* Toda la creación de mensajes se realiza dentro de la propia instancia de Campaign

<br>

## Guardas

[Vínculo del producto de guardas de Journey Optimizer](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=es)

### Guardas adicionales de Journey Optimizer

* Es posible configurar la limitación a través de la API para asegurar que el sistema de destino no se sature hasta el punto que dé errores. Esto significa que los mensajes que excedan el tope se descartarán completamente y no se enviarán jamás. No se admite establecer limitaciones.
   * Número máximo de conexiones: número máximo de conexiones de http/s que admite el destino.
   * Recuento máximo de llamadas: número máximo de llamadas que se pueden realizar en el parámetro periodInMs.
   * periodInMs: tiempo en milisegundos.
* Los recorridos iniciados por pertenencia a segmentos pueden funcionar de dos modos:
   * Segmentos por lotes (actualizados cada 24 horas)
   * Segmentos por flujo (calificación &lt;5 minutos)
* Segmentos por lotes: debe conocer el volumen diario de usuarios adecuados y garantizar que el sistema de destino pueda soportar el pico de rendimiento por recorrido y durante todos los recorridos.
* Segmentos por flujo: debe asegurarse de que el pico inicial de calificaciones de perfil pueda gestionarse junto con el volumen de calificación de flujo diario por recorrido y durante todos los recorridos.
* Gestión de decisiones no es compatible
* No se admiten los eventos comerciales
* Integraciones salientes a sistemas de terceros
   * No es compatible con una sola IP estática, ya que nuestra infraestructura es de varios inquilinos (debe realizar la lista de permitidos de todas las IP del centro de datos)
   * Solo se admiten métodos de PUT y POST para acciones personalizadas
   * Compatibilidad con autenticación: token | contraseña | OAuth2
* No es posible empaquetar y mover componentes individuales de Adobe Experience Platform o Journey Optimizer entre varias zonas protegidas. Debe volver a implementarse en nuevos entornos

<br>

### Campaign (v8)

* La instancia de ejecución del Centro de mensajes debe estar alojada por Adobe Managed Cloud Services
* Rendimiento de mensajería
   * AC (v8) hasta 1 millón por hora basado en el paquete
* AC (v8) no es compatible con la gestión de decisiones en los mensajes
* No se restringen las llamadas de API salientes realizadas a Campaign
* Con Campaign v8.4, es posible sacar provecho del conector de origen (Source Connector) de Adobe Campaign Managed Services en Experience Platform para sincronizar los eventos de envío y seguimiento de Campaign a Experience Platform. Consulte la documentación del conector de origen para obtener más información. [Vínculo](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=es)

<br>

## Pasos de implementación

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=es) según los datos ofrecidos por los clientes en Experience Platform.
1. Crear esquemas basados en clases de eventos de experiencias para las tablas broadLog, trackingLog y direcciones que no se pueden enviar de Adobe Campaign (opcional).
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

1. [Incorporar datos en Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) mediante API de flujo y conectores de origen.

### Journey Optimizer

1. Configure la fuente de datos de Experience Platform y determine qué campos deben almacenarse en caché como parte de los datos profileStreaming utilizados para iniciar un recorrido del cliente. Primero debe configurarse en Journey Optimizer para obtener un ID de organización. Este ID de organización debe entregarse al desarrollador para usarse con la ingesta
1. Configure orígenes externos de datos
1. Configure acciones personalizadas para una instancia de Campaign

### Campaign v8

* Las plantillas de mensajería deben configurarse con el contexto de personalización adecuado
* Para Campaign Standard: los flujos de trabajo de exportación deben configurarse para exportar de nuevo los registros de mensajería transaccional a Experience Platform. Se recomienda que se ejecuten como mucho cada cuatro horas.
* Para Campaign v8.4, es posible sacar provecho del conector de origen (Source Connector) de Adobe Campaign Managed Services en Experience Platform para sincronizar los eventos de envío y seguimiento de Campaign a Experience Platform. Consulte la documentación del conector de origen para obtener más información. [Vínculo](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=es)

### Configuración push móvil (opcional)

1. Implemente el SDK móvil de Experience Platform para recopilar tokens push e información de inicio de sesión con el fin de volver a perfiles de cliente conocidos
1. Aproveche las etiquetas de Adobe y cree una propiedad móvil con la siguiente extensión:
   * Adobe Journey Optimizer | Adobe Campaign Classic | Adobe Campaign Standard
   * Adobe Experience Platform Edge Network
   * Identidad      para Edge Network
   * Núcleo móvil
1. Asegúrese de tener un conjunto de datos dedicado para implementaciones de aplicaciones móviles vs. implementaciones web
1. Para obtener más información, siga la [Guía móvil de Adobe Journey Optimizer](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

   >[!IMPORTANT]
   >Puede que sea necesario recopilar los tokens móviles tanto en Journey Optimizer como en Campaign si se desea enviar comunicaciones en tiempo real a través de Journey Optimizer y notificaciones push por lotes a través de Campaign. Campaign v8 requiere el uso exclusivo del SDK de Campaign para capturar tokens push.

<br>

## Documentación relacionada

* [Documentación de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es)
* [Descripción del producto Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
* [Documentación de Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=es)
