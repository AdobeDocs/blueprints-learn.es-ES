---
title: Perfil y Audience Activation a destinos empresariales
description: Perfil y Audience Activation a destinos empresariales
solution: Experience Platform,Real-time Customer Data Platform,Target,Audience Manager,Analytics,Experience Cloud Services,Data Collection
kt: 7086
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5
translation-type: tm+mt
source-git-commit: 98d44067a1640dc8b695cb0d25f69ec26be647e1
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Escenario de perfiles y Audience Activation a destinos empresariales

Replicación y actualización de cambios de perfil en almacenes de datos empresariales para casos de uso de activación y generación de informes.

Inicie una acción de ventas o asistencia al cliente mediante la notificación de una acción del cliente desde la plataforma de datos del cliente en tiempo real a sistemas y aplicaciones empresariales.

## Casos de uso

* Activación de perfiles y audiencias en destinos de almacenamiento en la nube o de flujo continuo para el seguimiento, almacenamiento, análisis y activación de datos y perspectivas de clientes por parte de la empresa.

## Aplicaciones

* Activación de Adobe Experience Platform

## Arquitectura

<img src="assets/enterprise_destination.svg" alt="Arquitectura de referencia para el escenario de activación empresarial" style="border:1px solid #4a4a4a" />

## Seguridad

[Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

Umbrales de latencia y rendimiento:

Segmentación por transmisión:

* Hasta 5 minutos para la segmentación de flujo continuo, con hasta 1500 eventos por segundo
* Hasta 11 minutos para activación de flujo continuo

Segmentación por lotes:
Una vez al día o iniciada manualmente ad hoc mediante API

* Aproximadamente 1 hora por trabajo para un tamaño de almacén de perfiles de hasta 10 TB
* Aproximadamente 2 horas por trabajo para un tamaño de almacén de perfiles de 10 TB a 100 TB

## Pasos de la implementación

1. Crear esquemas para los datos que se van a introducir
1. Crear conjuntos de datos para los datos que se van a ingerir
1. Configure las identidades y los espacios de nombres de identidad correctos en el esquema para asegurarse de que los datos introducidos se puedan unir en un perfil unificado.
1. Habilite los esquemas y conjuntos de datos para el procesamiento de perfiles.
1. Configurar las fuentes para la ingesta de datos
1. Segmentos de autor en el Experience Platform, que se evaluarán en lote o flujo continuo. El sistema determina automáticamente si el segmento se evalúa como lote o flujo continuo.
1. Configure destinos para compartir atributos de perfil y pertenencias de audiencia en destinos deseados.

## Consideraciones sobre la implementación

Activación de atributos e identidades

* La plataforma de datos del cliente en tiempo real puede activar tanto las suscripciones de audiencia como los cambios de atributos e identidad que se producen en los perfiles que son miembros de segmentos que se han seleccionado para la activación. Como tal, si el caso de uso es para activar atributos o identidades, se debe definir un segmento global que incluya todos los perfiles para los que se enviarán las actualizaciones de atributos o identidades. Una vez colocado este valor, el segmento y los atributos deseados que se activan se pueden seleccionar como parte de la configuración de destino.
* Tenga en cuenta que los destinos de lote no admiten la activación de solo eventos de cambio de atributo. La pertenencia a audiencias completa o incremental se puede enviar junto con los atributos seleccionados para la activación, pero los eventos de cambio de atributos solo se pueden activar mediante destinos por lotes.

Activación de segmentos por lotes a destinos de flujo continuo

* Se admite la activación de segmentos por lotes a destinos de flujo continuo. Los trabajos de segmentos por lotes colocan mensajes en la canalización una vez que se haya completado el trabajo del segmento para la activación de flujo continuo

Activación de segmentos de flujo continuo a destinos por lotes

* Se admite la activación de segmentos de transmisión a destino por lotes. La programación de destino de lote exportará las suscripciones de segmentos de los perfiles según la programación de destino de lote. Esto incluye tanto las suscripciones a segmentos determinadas mediante métodos de flujo continuo como por lotes.

Activación de eventos de experiencias

* Actualmente no se admite la activación de eventos de experiencia sin procesar. Para activarse con eventos de experiencia, se debe crear un segmento con las reglas necesarias que incluyan o excluyan la lógica de evento de experiencia con la que se activará. Esto crea un segmento que se define para los eventos de experiencia y la pertenencia a un segmento se puede activar como proxy para activar los eventos de experiencia sin procesar. Considere también la posibilidad de aprovechar el servidor de Launch para activar los eventos de experiencia sin procesar recopilados mediante SDK.

## Documentación relacionada

* [Descripción del producto de la plataforma de datos del cliente en tiempo real](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Documentación de segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Documentación de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Vídeos y Tutorials relacionados

* [Información general sobre la plataforma de datos del cliente en tiempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demostración de la plataforma de datos del cliente en tiempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
