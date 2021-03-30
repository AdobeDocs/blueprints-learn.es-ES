---
title: Situación de Audience Activation en línea/sin conexión
description: Audience Activation en línea/sin conexión.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
translation-type: tm+mt
source-git-commit: c4bd4bbd40f2ae6b9ab980c5274a6e2007d976d3
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---


# Situación de Audience Activation en línea/sin conexión

Utilice atributos y eventos sin conexión, como pedidos sin conexión, transacciones, CRM o datos de fidelidad, junto con el comportamiento en línea para la segmentación y personalización en línea.

Active audiencias en destinos basados en perfiles conocidos, como proveedores de correo electrónico, redes sociales y destinos publicitarios.

## Casos de uso

* Segmentación de audiencias para audiencias conocidas en destinos sociales y publicitarios.
* Personalización en línea con atributos en línea y sin conexión.
* Active audiencias en canales conocidos, como correo electrónico y SMS.

## Aplicaciones

* Adobe Experience Platform
* Plataforma de datos de clientes en tiempo real

## Arquitectura

<img src="assets/onoff.svg" alt="Arquitectura de referencia para el escenario de Audience Activation en línea/sin conexión" style="border:1px solid #4a4a4a" />

## Seguridad

* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* Los trabajos de segmentos por lotes se ejecutan una vez al día en función de la programación predeterminada. Los trabajos de exportación de segmentos se ejecutan antes de la entrega de destino programada. Tenga en cuenta que los trabajos de segmento por lotes y los trabajos de entrega de destino se ejecutan por separado. Los trabajos de segmentos por lotes y el rendimiento de los trabajos de exportación dependen del número de perfiles, el tamaño de los perfiles y el número de segmentos que se evalúen.
* Los trabajos de los segmentos de transmisión se evalúan minutos después de que los datos de flujo lleguen al perfil, escriban inmediatamente la pertenencia al segmento en el perfil y envíen un evento para que las aplicaciones se suscriban.
* La pertenencia a segmentos de transmisión se toma en cuenta inmediatamente para los destinos de flujo continuo y se entrega en eventos de pertenencia a un solo segmento o en un microlote de eventos de perfil múltiples que dependen de los patrones de ingesta del destino. Los destinos programados iniciarán un trabajo de exportación de segmentos desde el perfil antes de la entrega para cualquier segmento evaluado en la transmisión que se entregue mediante la entrega programada de segmentos por lotes.
* Para compartir la pertenencia a segmentos RTCDP con Audience Manager, esto sucede en minutos para segmentos de flujo continuo y en minutos después de la finalización de la evaluación de segmentos por lotes para la segmentación por lotes.
* Los segmentos compartidos de Experience Platform a Audience Manager se comparten pocos minutos después de la realización del segmento, ya sea a través del método de evaluación por lotes o de flujo continuo. Existe una sincronización inicial de la configuración de segmentos entre AEP y AAM una vez que el segmento se ha creado inicialmente, después de ~4 horas, las suscripciones de segmentos a AEP pueden empezar a realizarse en perfiles AAM. La pertenencia a audiencias realizada antes de la configuración del uso compartido de audiencias de Experience Platform y Audience Manager o antes de que los metadatos de audiencia se sincronicen de Experience Platform a Audience Manager no se realizará en Audience Manager hasta que se compartan las suscripciones de segmentos &quot;existentes&quot;.
* Los trabajos de destino por lotes o de flujo continuo de los trabajos de segmentos por lotes pueden compartir actualizaciones de atributos de perfil, así como suscripciones a segmentos.
* Los trabajos de segmentación por transmisión a destinos de flujo continuo solo comparten actualizaciones de pertenencia a segmentos.

## Pasos de la implementación

1. Configure esquemas y conjuntos de datos en Experience Platform.
1. Configure las identidades y los espacios de nombres de identidad correctos en el esquema para asegurarse de que los datos introducidos se puedan unir en un perfil unificado.
1. Habilite el esquema y los conjuntos de datos para Perfil.
1. Ingeste datos en Platform.
1. Aprovisionar el uso compartido de segmentos en tiempo real de la Plataforma de datos del cliente entre el Experience Platform y el Audience Manager para que las audiencias definidas en el Experience Platform se compartan con el Audience Manager.
1. Segmentos de autor en el Experience Platform, que se evaluarán en lote o flujo continuo. El sistema determina automáticamente si el segmento se evalúa como lote o flujo continuo.
1. Configure destinos para compartir atributos de perfil y pertenencias de audiencia en destinos deseados.

## Consideraciones sobre la implementación

* Para compartir datos de perfil con destinos es necesario incluir el valor de identidad específico que utiliza el destino en la carga útil de destino. Cualquier identidad necesaria para un destino de destino debe ingerirse en Platform y configurarse como identidad para el perfil del cliente en tiempo real.

* En los casos de activación en los que las audiencias se comparten de Experience Platform a Audience Manager, todas las identidades incluidas en el [!UICONTROL Perfil del cliente en tiempo real] se comparten con el Audience Manager. Las audiencias del Experience Platform se pueden compartir a través de destinos de Audience Manager cuando las identidades de destino requeridas se incluyen en el [!UICONTROL Perfil del cliente en tiempo real] o donde las identidades del [!UICONTROL Perfil del cliente en tiempo real] se pueden relacionar con las identidades de destino requeridas que están vinculadas en Audience Manager.

## Documentación relacionada

* [Descripción del producto de la plataforma de datos del cliente en tiempo real](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Directrices de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Documentación de segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Documentación de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Vídeos y Tutorials relacionados

* [Información general sobre la plataforma de datos del cliente en tiempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demostración de la plataforma de datos del cliente en tiempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Crear segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)