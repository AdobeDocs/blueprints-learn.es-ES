---
title: Modelo de activación de audiencias y perfiles en destinos empresariales
description: Activación de audiencias y perfiles en destinos empresariales
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: a63da7d5da3038cf66b5f2c99e117d4aa5b21cc1
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Modelo de activación de audiencias y perfiles en destinos empresariales

Replicación y actualización de los cambios de perfil y audiencia en los almacenes de datos empresariales para casos de uso de activación y generación de informes. <!-- This sentence is difficult to mentally process because there's no verb. Describe what the customer can do with this feature. The first paragraph on a page should not be an abstract description.-->

Inicie una acción de ventas o asistencia al cliente mediante la notificación de una acción del cliente desde la [!UICONTROL Plataforma de datos del cliente en tiempo real] a sistemas y aplicaciones empresariales. <!-- What kinds of sales or support actions? You might add a "For example...." The content in these blueprints should be more simple and friendly.-->

## Casos de uso

* Activación de perfiles y audiencias en destinos de almacenamiento en la nube o destinos de flujo continuo para el seguimiento, almacenamiento, análisis y activación de datos y perspectivas de clientes por parte de la empresa.

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
Una vez al día, o iniciados manualmente, ad hoc mediante API.

* Aproximadamente 1 hora por trabajo para un tamaño de almacén de perfiles de hasta 10 TB
* Aproximadamente 2 horas por trabajo para un tamaño de almacén de perfiles de 10 TB a 100 TB

## Pasos de la implementación

1. Cree esquemas para introducir los datos. <!-- Cross-references to these topics would be helpful -->
1. Cree conjuntos de datos para incorporar datos.
1. Configure las identidades y los espacios de nombres de identidad correctos en el esquema para asegurarse de que los datos introducidos se puedan unir en un perfil unificado.
1. Habilite los esquemas y conjuntos de datos para el procesamiento de perfiles.
1. Configure cualquier fuente para el consumo de datos.
1. Segmentos de autor en Experience Platform, que se evaluarán en lote o flujo continuo. El sistema determina automáticamente si el segmento se evalúa como lote o flujo continuo.
1. Configure destinos para compartir atributos de perfil y pertenencias de audiencia en destinos deseados.

## Consideraciones sobre la implementación

Activación de atributos e identidades

* [!UICONTROL La ] plataforma de datos del cliente en tiempo real puede activar las suscripciones de audiencia, así como los cambios de atributos e identidad que se producen en los perfiles que son miembros de segmentos seleccionados para la activación. Si su objetivo es activar atributos o identidades, debe definir un segmento global que incluya todos los perfiles a los que se envían las actualizaciones de atributos e identidades. En este punto, puede seleccionar el segmento y los atributos deseados para activarlos como parte de la configuración de destino.
* Tenga en cuenta que los destinos de lote no admiten la activación de eventos de cambio de solo atributo. Se pueden enviar suscripciones de audiencia completas o incrementales junto con los atributos seleccionados para la activación, pero no se pueden activar eventos de cambio de solo atributos mediante destinos por lotes.

Activación de segmentos por lotes en destinos de flujo continuo

* Se admite la activación de segmentos por lotes a destinos de flujo continuo. Los trabajos de segmentos por lotes colocan mensajes en la canalización una vez que se haya completado el trabajo del segmento para la activación de flujo continuo

Activación de segmentos de flujo continuo en destinos por lotes

* Se admite la activación de segmentos de transmisión a destino por lotes. La programación de destino de lote exporta las suscripciones a segmentos de perfil en función de la programación de destino de lote. Esto incluye tanto las suscripciones a segmentos determinadas mediante métodos de flujo continuo como por lotes.

Activación de eventos de experiencia

* No se admite la activación de eventos de experiencia sin procesar. Para activarse con eventos de experiencia, se debe crear un segmento con las reglas necesarias que incluyan o excluyan la lógica de eventos de experiencia. Esto crea un segmento que se define para los eventos de experiencia y la pertenencia a un segmento se puede activar como proxy para activar los eventos de experiencia sin procesar. Considere también la posibilidad de utilizar [!UICONTROL Launch Server Side] para activar eventos de experiencia sin procesar recopilados mediante SDK.

## Documentación relacionada

* [Documentación de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)
* [Información general sobre los destinos de almacenamiento en la nube](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [Destino HTTP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [[!UICONTROL Descripción del producto de la ] plataforma de datos del cliente en tiempo real](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Documentación de segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)

## Vídeos y Tutorials relacionados

* [[!UICONTROL Resumen de la plataforma de datos del cliente en ] tiempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demostración de la plataforma de datos del cliente en tiempo  [!UICONTROL real]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
