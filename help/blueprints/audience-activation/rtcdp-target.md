---
title: Personalization de cliente conocido con Target
description: Integre perfiles y públicos RTCDP con Adobe Target.
landing-page-description: Integre perfiles y públicos RTCDP con Adobe Target.
short-description: Integre perfiles y públicos RTCDP con Adobe Target.
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 88a15765c0a998d49c19d9853ad0c44d6e3bfaa1
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 31%

---


# Personalization de cliente conocido con Target

## Casos de uso

* Personalización en línea con datos de clientes conocidos
* Optimización de la página de aterrizaje
* Personalización basada en visualizaciones de productos/contenidos anteriores, afinidad de producto/contenido, atributos del entorno y datos demográficos, además de datos sin conexión, tales como datos de transacciones, fidelidad y CRM, e información modelada.
* Comparta y segmente audiencias definidas en Real-time Customer Data Platform en sitios web y aplicaciones móviles mediante Adobe Target

## Aplicaciones

* [!UICONTROL Real-Time Customer Data Platform]
* Adobe Target

### Documentación de referencia

* [Conexión de Adobe Target para Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Configuración de la secuencia de datos de Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)

## Patrones de integración

| Patrón de integración | Capacidad | Requisitos previos |
|--------------------|------------|---------------|
| **Evaluación de segmentos en tiempo real en Edge compartidos desde Real-time Customer Data Platform a Target** | : Evalúe las audiencias en tiempo real para la personalización de la misma página o de la siguiente en Edge. <br>: cualquier segmento evaluado en flujo continuo o por lotes también se proyectará a Edge Network para que se incluya en la evaluación y personalización de segmentos de Edge. | : Web/Mobile SDK debe estar implementado para la API de servidor de Edge Network. <br>: la secuencia de datos debe configurarse en Experience Edge con la extensión de Target y Experience Platform habilitada. <br>: el destino de destino debe configurarse en Destinos de Real-time Customer Data Platform. <br>- La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform. |
| **Uso compartido de streaming y audiencias por lotes desde Real-time Customer Data Platform a Target a través del enfoque de Edge** | - Comparta audiencias de flujo continuo y por lotes de Real-time Customer Data Platform en Target a través de Edge Network. <br>: las audiencias evaluadas en tiempo real requieren la implementación de Web SDK y Edge Network. | : La implementación de la API de Edge o la SDK web/móvil de Target no es necesaria para compartir audiencias de streaming y RTCDP por lotes con Target, pero se requiere para habilitar la evaluación de segmentos perimetrales en tiempo real. <br>- Si utiliza AT.js, solo se admite la integración de perfiles con el área de nombres de identidad de ECID. <br>: para las búsquedas de área de nombres de identidad personalizadas en Edge, se requiere la implementación de la API de Web SDK/Edge, y cada identidad debe establecerse como identidad en el mapa de identidad. <br>: el destino de destino debe configurarse en Destinos de Real-time Customer Data Platform; solo se admite la zona protegida de producción predeterminada en RTCDP. <br>- La integración con Target requiere la misma organización de IMS que la instancia de Experience Platform. |
| **Uso compartido de streaming y audiencias por lotes desde Real-time Customer Data Platform a Target y Audience Manager a través del enfoque del servicio de uso compartido de audiencias** | : Este patrón de integración se puede aprovechar cuando se desee un enriquecimiento adicional de datos y audiencias de terceros en Audience Manager. | : Web/Mobile SDK no es necesario para compartir audiencias de flujo continuo y por lotes con Target, pero sí para habilitar la evaluación de segmentos perimetrales en tiempo real. <br>- Si utiliza AT.js, solo se admite la integración de perfiles con el área de nombres de identidad de ECID. <br>: para las búsquedas de área de nombres de identidad personalizadas en Edge, se requiere la implementación de la API de Web SDK/Edge, y cada identidad debe establecerse como identidad en el mapa de identidad. <br>: se debe aprovisionar la proyección de audiencia mediante el servicio de uso compartido de audiencias. <br>: la integración con Target requiere la misma organización de IMS que la instancia de Experience Platform. <br>: solo las audiencias de la zona protegida de producción predeterminada admiten el servicio principal de uso compartido de audiencias. |

## Uso compartido de audiencias en tiempo real, por flujo y por lotes en Adobe Target

Arquitectura

![Arquitectura de referencia para el modelo Web Personalization en línea/sin conexión](assets/RTCDP+Target.svg)

Detalle de secuencia

![Arquitectura de referencia para el modelo Web Personalization en línea/sin conexión](assets/RTCDP+Target_flow.svg)

Vista general de la arquitectura

![Arquitectura de referencia para el modelo Web Personalization en línea/sin conexión](assets/personalization_with_apps.svg)

## Patrones de implementación

La personalización de cliente conocida se admite mediante varios enfoques de implementación.

### Patrón de implementación 1 - [!DNL Edge Network] con SDK web/móvil o API [!DNL Edge Network] (enfoque recomendado)

* Usando [!DNL Edge Network] con Web/Mobile SDK. La segmentación perimetral en tiempo real requiere el enfoque de implementación del SDK web/móvil o la API de Edge.
* [Consulte el modelo web y SDK móvil de Experience Platform](../experience-platform/deployment/websdk.md) para la implementación basada en SDK.
* Para su uso en Mobile SDK, debe estar instalada la extensión [Adobe Journey Optimizer - Decisioning](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/).
* [Consulte la [!DNL Edge Network] API de servidor](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es) para obtener una implementación basada en API de Adobe Target con perfil de Edge.

### Patrón de implementación 2: SDK específicos para aplicaciones

Con SDK tradicionales específicos de cada aplicación (por ejemplo, AT.js y AppMeasurement.js). La evaluación de segmentos en tiempo real de Edge no se admite con este enfoque de implementación. Sin embargo, el uso compartido de audiencias por flujo y por lotes desde el centro de Experience Platform se admite con este enfoque de implementación.

[Consulte la documentación del conector de Adobe Target](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection)
[Consulte el modelo de SDK específico de la aplicación](../experience-platform/deployment/appsdk.md)

## Consideraciones sobre la implementación

* Cualquier identidad principal se puede aprovechar al utilizar el patrón de implementación 1 descrito anteriormente con [!DNL Edge Network] y Web SDK.
* La primera personalización de inicio de sesión con datos de clientes conocidos introducidos anteriormente en RTCDP requiere que la solicitud de personalización tenga una identidad principal que coincida con el gráfico de identidad de clientes conocidos en Real-time Customer Data Platform. Si el ID principal se establece en ECID o en una identidad que aún no se ha vinculado con el perfil de cliente conocido, la unión de identidad tardará varios minutos en realizarse en el perímetro y que la personalización de Edge incluya datos de clientes conocidos ingeridos anteriormente.
* Actualmente, los perfiles de Edge tienen un TTL de 14 días. Por lo tanto, si un usuario no ha iniciado sesión o ha estado activo durante 14 días en el perímetro, el perfil del perímetro puede haber caducado y, por lo tanto, el perímetro debe recuperar el perfil del centro de datos para tener la vista de perfil histórica para impulsar la personalización que incluye atributos de perfil ingeridos anteriormente y segmentos, esto resultará en la personalización con la vista histórica de los perfiles que se producen en vistas de página posteriores en comparación con el primer inicio de sesión.

## Documentación relacionada

### Documentación del SDK

* [Documentación del SDK web de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
* [Documentación de Experience Cloud ID Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es)

### Documentación de la segmentación

* [Información general sobre la segmentación en Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=es)
* [Segmentación en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=es)
* [Segmentación por flujo](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es)
* [Intercambio de segmentos de Adobe Analytics mediante Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=es)
* [Configuración de políticas de combinación](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=es#create-a-merge-policy)

### Tutoriales

* [Personalización de próxima visita con Real-Time CDP y Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=es)
