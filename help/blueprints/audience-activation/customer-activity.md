---
title: Modelo de centro de actividad del cliente
description: '[!UICONTROL Busque perfiles de cliente en tiempo real para ofrecer contexto a los agentes de atención al cliente y ventas.]'
solution: Experience Platform,Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c,4f15aa5d-9ee3-4d92-8012-3e2f0c0d615f
translation-type: tm+mt
source-git-commit: da21d1796eb9a2c9c0f087d82606874ca55bd4ea
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 90%

---

# Modelo de centro de actividad del cliente

El modelo de centro de actividad del cliente muestra cómo ciertas aplicaciones externas pueden acceder a [!UICONTROL Real-time Customer Profile] de Adobe Experience Platform.

Las aplicaciones externas pueden acceder a perfiles con una solicitud de GET de API. Los atributos, eventos, pertenencia a segmento y todos los recursos por modelo almacenados en el perfil se podrán utilizar posteriormente en las aplicaciones externas que no pertenezcan a Adobe.

Con esta capacidad, es posible hacer aflorar contenido de interés cuando el cliente contacta con el centro de llamadas. El agente de asistencia podrá visualizar el valor de duración del cliente y su tendencia a cancelar o exponerse a campañas de marketing, por ejemplo. Los agentes de ventas también pueden beneficiarse del contexto extra que brinda información sobre el cliente.

>[!NOTE]
>
>La latencia actual admitida por la API de búsqueda de perfiles es de aproximadamente 500 milisegundos, lo que hace que este enfoque no sea adecuado para la integración del perfil con motores de decisión en tiempo real, como la personalización móvil o web en la misma página.

## Casos de uso

* Ofrecer un contexto más rico sobre el cliente a las interacciones realizadas por agentes, como las experiencias de asistencia y ventas. Utilizando la búsqueda de perfil en Experience Platform, los agentes pueden recibir más contexto sobre el cliente, tal como compras recientes, interacciones con campañas, tendencias, pertenencia a audiencia y otros atributos y datos que se almacenan en tiempo real en el perfil del cliente.

## Arquitectura

<img src="assets/customer_activity_hub.svg" alt="Arquitectura de referencia para el modelo de centro de actividad del cliente" style="border:1px solid #4a4a4a" />


## Guardas

* [Guardas de los datos de Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)

## Pasos de implementación

1. Configurar conjunto de datos y esquemas.
1. Configurar [!UICONTROL Perfil del cliente en tiempo real]: configure el esquema y el conjunto de datos para [!UICONTROL Perfil del cliente en tiempo real] y una política de combinación y las identidades.
1. Realizar la ingesta de datos en Platform y procesarla en [!UICONTROL Real-time Customer Profile].
1. Utilizar la API de la entidad para buscar un atributo de perfil, tanto de la entidad de registro como de la de evento de experiencia.

## Documentación relacionada

* [Descripción del producto Adobe Experience Platform Activation](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform0.html)
* [Documentación de Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=es)
* [Guardas de perfil](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [API de búsqueda de perfiles](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
