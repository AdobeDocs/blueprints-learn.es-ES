---
title: Modelo de mensajería activada y Adobe Experience Platform
description: Ejecute mensajes y experiencias activadas con Adobe Experience Platform como sistema centralizado de transmisión de datos, perfiles de cliente y segmentación.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
translation-type: ht
source-git-commit: 01f70fe432d7be38b71889ae19c0d5fe4cf0f78a
workflow-type: ht
source-wordcount: '694'
ht-degree: 100%

---

# Modelo de mensajería activada y Adobe Experience Platform

Ejecute mensajes y experiencias activadas con Adobe Experience Platform como sistema centralizado de transmisión de datos, perfiles de cliente y segmentación.

## Casos de uso

* Mensajería activada
* Confirmaciones de registro
* Abandonos del carro de compras y formulario de solicitud
* Mensajería activada por localización

## Arquitectura

<img src="assets/triggered.svg" alt="Arquitectura de referencia para el modelo de mensajería activada y Adobe Experience Platform" style="border:1px solid #4a4a4a" />

## Patrones de integración

* Adobe Experience Platform -> Journey Orchestration

## Prerrequisitos

* Adobe Experience Platform
* Journey Orchestration

## Guardas

### Journey Orchestration

* Consulte el enlace para obtener [más información sobre las limitaciones](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=es#starting-with-journeys)
* Es posible configurar la limitación a través de la API para asegurar que el sistema de destino no se sature hasta el punto que dé errores. Limitar significa que los mensajes que excedan el tope se descartarán completamente y no se enviarán jamás. Las restricciones no son compatibles aún.
   * max connections: número máximo de conexiones que admite el destino.
   * max call count: número máximo de llamadas a realizar en el parámetro periodInMs.
   * periodInMs: tiempo en milisegundos.
* Los recorridos iniciados por pertenencia a segmentos pueden funcionar de dos modos:
   * Segmentos por lotes (actualizados cada 24 horas)
   * Segmentos por flujo (calificación &lt;5 minutos)
* Segmentos por lotes: asegúrese de conocer el volumen diario de usuarios calificados para garantizar que el sistema de destino pueda soportar el pico de rendimiento por recorrido y durante todos ellos.
* Segmentos por flujo: asegúrese de que el pico inicial de calificaciones de perfil pueda manejarse juntamente con el volumen de calificación de flujo diario por recorrido y durante todos ellos.
* El destino final debe ser compatible con la carga de REST API &amp; JSON.
* Actualmente, no es compatible con Offer Decisioning.
* Consulte [los guardas de perfil e ingesta de datos de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)

### Adobe Campaign Standard

* Solo es compatible con un rendimiento de 14 tps (50 mil por hora)
* No es compatible con recorridos iniciados por pertenencia a segmento.
* Los eventos de reacción a mensajes transaccionales (abrir/clics) son compatibles con Journey Orchestration.
* En la actualidad, los registros de los mensajes transaccionales no se sincronizan nativamente con Experience Platform, por lo que requieren configuración manual. Se recomienda exportar los registros como mucho cada cuatro horas.


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
1. [Añadir identidades a los esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es).
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Configurar políticas de fusión](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=es) para diferenciar las vistas de [!UICONTROL Real-time Customer Profile] (opcional).
1. Crear segmentos para el uso en Adobe Campaign.

#### Origen/destino

1. [Realizar la ingesta de datos en Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) utilizando las API de flujo y conectores de origen.1. Configurar el destino de almacenamiento de los blobs de [!DNL Azure] para su uso con Adobe Campaign.

#### Implementación de aplicaciones móviles

1. Implementar el SDK de Adobe Campaign de Adobe Campaign Classic o el SDK Experience Platform de Adobe Campaign Standard. En el caso de contar con Experience Platform Launch, recomendamos utilizar la extensión de Adobe Campaign Classic o Adobe Campaign Standard con el SDK de Experience Platform.


### Journey Orchestration

1. El flujo de datos utilizado para iniciar el recorrido del cliente debe configurarse primero en Journey Orchestration para obtener un ID de organización. Este ID de organización debe entregarse al desarrollador para usarse con la ingesta.
1. Configurar orígenes externos de datos.
1. Configurar acciones personalizadas.

### Adobe Campaign Standard

1. Configurar plantillas de mensajería con las configuraciones de personalización adecuadas.
1. Configurar informes de exportación de flujos de trabajo y mensajes transaccionales. Recomendamos que se ejecuten como mucho cada cuatro horas.


## Documentación relacionada

* [Documentación de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Documentación de Journey Orchestration](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=es)
* [Documentación de Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=es)
* [Documentación de Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=es)
* [Documentación de Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=es)
* [Documentación del SDK Experience Platform Mobile](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
