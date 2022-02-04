---
title: Journey Optimizer con Adobe Campaign Blueprint
description: Muestra cómo se puede utilizar Adobe Journey Optimizer con Adobe Campaign para enviar mensajes de forma nativa utilizando el servidor de mensajería en tiempo real en Campaign
solution: Experience Platform, Journey Optimizer, Campaign v8, Campaign Classic v7, Campaign Standard
hidefromtoc: true
source-git-commit: a86df4a1b2de38bcb244a6afe1cea87adc7e26fa
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 26%

---

# Journey Optimizer con Adobe Campaign

Muestra cómo se puede utilizar Adobe Journey Optimizer con Adobe Campaign para enviar mensajes de forma nativa utilizando el servidor de mensajería en tiempo real en Campaign.

<br>

## Arquitectura

<img src="assets/ajo-campaign-architecture.svg" alt="Arquitectura de referencia modelo de Journey Optimizer" style="width:100%; border:1px solid #4a4a4a" />

>[!IMPORTANT]
>El uso de Journey Optimizer y Campaign para enviar mensajes de forma independiente entre sí es posible, pero tiene algunas consideraciones técnicas que se deben tener en cuenta. Si desea seguir esta ruta, póngase en contacto con su arquitecto empresarial de preventa para asegurarse de que comprende lo que se necesitará para admitir la implementación.

<br>

## Prerrequisitos

### Adobe Experience Platform

* Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar las fuentes de datos de Journey Optimizer
* Para los esquemas basados en clases de eventos de experiencia, agregue el grupo de campos &quot;ID de evento de orquestación&quot; cuando desee que se active un evento que no sea un evento basado en reglas
* Para los esquemas basados en clases de Perfil individual, agregue el grupo de campos &quot;Detalles de prueba de perfil&quot; para poder cargar perfiles de prueba para utilizarlos con Journey Optimizer
* Journey Optimizer y Campaign se aprovisionan en la misma organización de IMS

### Campaign v7/v8 o Campaign Standard

* La instancia de ejecución del servicio de mensajería en tiempo real (es decir, el Centro de mensajes) debe estar alojada por los Cloud Services administrados de Adobe
* Toda la creación de mensajes se realiza dentro de la propia instancia de Campaign

<br>

## Guardas

[Vínculo del producto de Journey Optimizer Guardrade](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=es)

### Protecciones adicionales de Journey Optimizer

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
* No se admiten eventos comerciales
* Integraciones salientes a sistemas de terceros
   * No es compatible con una sola IP estática, ya que nuestra infraestructura es de varios inquilinos (debe realizar la lista de permitidos de todas las IP del centro de datos)
   * Solo se admiten métodos de PUT y POST para acciones personalizadas
   * Compatibilidad con autenticación: token | contraseña | OAuth2
* No es posible empaquetar y mover componentes individuales de Adobe Experience Platform o Journey Optimizer entre varios entornos limitados. Debe volver a implementarse en nuevos entornos

<br>

### Campaign (v7/v8)

* La instancia de ejecución del Centro de mensajes debe estar alojada por Cloud Services administrados de Adobe
* Debe estar en la versión 7 > 21.1 o v8
* Rendimiento de mensajería
   * AC (v7) 50 k por hora
   * AC (v8) hasta 1M por hora basado en el paquete
* AC (v7) solo admite el recorrido iniciado por evento
   * No se ha iniciado ningún segmento o pertenencia a segmento, Recorrido
   * La lectura de los recorridos basados en eventos de audiencia y de negocio no es compatible debido al volumen que puede enviar a las instancias de ejecución
* Ni AC (v7) ni AC (v8) admiten Offer decisioning en los mensajes
* No se restringen las llamadas de API salientes realizadas a Campaign
* Los registros de mensajería transaccional no se sincronizan de forma nativa con AEP. Requiere un esfuerzo de consultoría. Recomendación para exportar registros como máximo cada 4 horas

<br>

### Campaign Standard

* Soporta 14 tps (50 k por hora) en rendimiento
* Solo admite recorridos iniciados por eventos
   * No se ha iniciado ningún segmento o pertenencia a segmento, Recorrido
   * La lectura de los recorridos basados en eventos de audiencia y de negocio no es compatible debido al volumen que puede enviar a las instancias de ejecución
* Las actividades de aperturas y clics de mensajes transaccionales enviados al Campaign Standard se exponen de forma nativa como &quot;eventos de reacción&quot; dentro del lienzo de recorrido de Journey Optimizer
* Los registros de mensajería transaccional no se sincronizan de forma nativa con el Experience Platform. Requiere un esfuerzo de consultoría. Recomendación para exportar registros como máximo cada 4 horas

<br>

## Pasos de implementación

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. [Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) según los datos ofrecidos por los clientes en Experience Platform.
1. Cree esquemas basados en clases de Experience Event para las tablas broadLog, trackingLog y direcciones no entregables de Adobe Campaign (opcional).
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
1. Configurar acciones personalizadas para una instancia de Campaign

### Campaign v7/v8 o Campaign Standard

* Las plantillas de mensajería deben configurarse con el contexto de personalización adecuado
* Los flujos de trabajo de exportación deben configurarse para exportar de nuevo los registros de mensajería transaccional al Experience Platform. La recomendación es que se ejecute como máximo cada 4 horas

### Configuración push móvil (opcional)

1. Implemente el SDK de Experience Platform Mobile para recopilar tokens push e información de inicio de sesión con el fin de volver a perfiles de cliente conocidos
1. Aproveche las etiquetas de Adobe y cree una propiedad móvil con la siguiente extensión:
   * Adobe Journey Optimizer | Adobe Campaign Classic | Adobe Campaign Standard
   * Adobe Experience Platform Edge Network
   * Identidad para la red perimetral
   * Núcleo móvil
1. Asegúrese de tener un conjunto de datos dedicado para implementaciones de aplicaciones móviles vs. implementaciones web
1. Para obtener más información, siga la [Guía móvil de Adobe Journey Optimizer](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

   >[!IMPORTANT]
   >Puede que sea necesario recopilar los tokens móviles tanto en Journey Optimizer como en Campaign si se desea enviar comunicaciones en tiempo real a través de Journey Optimizer y notificaciones push por lotes a través de Campaign. Campaign v8 requiere el uso exclusivo del SDK de Campaign para capturar tokens push.

<br>

## Documentación relacionada

* [documentación del Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Documentación del SDK Experience Platform Mobile](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
* [Documentación de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es)
* [Descripción del producto de Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Documentación de Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=en)
* [Documentación de Campaign v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=es)
* [Documentación de Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=es)