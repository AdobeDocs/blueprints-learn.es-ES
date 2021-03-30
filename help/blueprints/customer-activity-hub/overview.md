---
title: Modelo de Centro de actividades del cliente
description: Búsquedas de Perfil del cliente en tiempo real para proporcionar contexto para la asistencia y las ventas asistidas por el agente.
solution: Experience Platform, Data Collection
kt: 7195
translation-type: tm+mt
source-git-commit: c4bd4bbd40f2ae6b9ab980c5274a6e2007d976d3
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Modelo de Centro de actividades del cliente

El modelo de Centro de actividades del cliente muestra cómo las aplicaciones externas pueden acceder al [!UICONTROL Perfil del cliente en tiempo real] de Adobe Experience Platform.

Las aplicaciones externas pueden acceder a R[!UICONTROL Perfiles del cliente en tiempo real] mediante una solicitud de GET de API. A continuación, en estas aplicaciones externas que no son de Adobe se pueden usar atributos, eventos, suscripciones a segmentos y funciones controladas por modelos almacenadas en el perfil.

Con esta capacidad, podría mostrar un contexto enriquecido cuando un cliente llame a su centro de llamadas. Los agentes de asistencia técnica podrían tener visibilidad sobre el valor de duración del cliente, la propensión a producir o la exposición a las campañas de marketing, por ejemplo. Los agentes de ventas también pueden beneficiarse de un mayor contexto o conocimiento de sus clientes.

>[!NOTE]
>
>La latencia actual admitida por la API de búsqueda de perfiles es de aproximadamente 500 milisegundos, por lo que este método no es adecuado para la integración del perfil con motores de decisión en tiempo real, como la personalización móvil o web de la misma página.

## Casos de uso

* Proporcione un contexto de cliente más profundo a las interacciones compatibles con el agente, como experiencias de asistencia y ventas. Con la búsqueda de perfiles en Experience Platform, los agentes pueden recibir más contexto sobre el consumidor, como compras recientes, interacciones de campañas, tendencias, pertenencia a audiencias y otros atributos y perspectivas que se almacenan en el perfil del cliente en tiempo real.

## Arquitectura

<img src="assets/cah.svg" alt="Arquitectura de referencia para el modelo de Centro de actividades del cliente" style="border:1px solid #4a4a4a" />

## Seguridad

* [Protecciones para datos de perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Pasos de la implementación

1. Configure conjuntos de datos y esquemas.
1. Configure [!UICONTROL Perfiles del cliente en tiempo real]: configure el esquema y el conjunto de datos para [!UICONTROL Perfil del cliente en tiempo real] y una política de combinación y las identidades.
1. Ingeste datos en Platform y procese en [!UICONTROL Perfil del cliente en tiempo real].
1. Utilice la API de entidad para buscar un atributo de perfil, ya sea desde la entidad de registro o la entidad de evento de experiencia.

## Documentación relacionada

* [Descripción del producto Adobe Experience Platform Activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)
* [Documentación del perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en)
* [Protección de perfiles](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [API de búsqueda de perfil](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
