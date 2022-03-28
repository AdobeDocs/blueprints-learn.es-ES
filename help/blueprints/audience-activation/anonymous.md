---
title: Modelo de activación de audiencia anónima
description: Descubra cómo segmentar audiencias de sitios web y otros canales de publicidad basándose en los datos anónimos de comportamiento de los clientes. Con esto, se puede crear una experiencia del cliente coherente y personalizada en diversos dispositivos.
landing-page-description: Descubra cómo segmentar audiencias de sitios web y otros canales de publicidad basándose en los datos anónimos de comportamiento de los clientes.
solution: Experience Platform, Audience Manager
kt: 7211
thumbnail: null
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
source-git-commit: 4a46b7a4c278107c806d3ddd14591c7abe1a13d3
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 34%

---

# Modelo de activación de audiencia anónima

La activación de audiencias anónimas es la capacidad de dirigir y personalizar audiencias a través de canales web, móviles y publicitarios en función de datos de comportamiento y dispositivos anónimos.

## Casos de uso

* Realice segmentación y personalización de audiencias digitales anónimas en el sitio web, la aplicación móvil o en canales publicitarios admitidos.
* Optimice las experiencias de página de aterrizaje y de autenticación previa en función de las características conocidas de dispositivo y comportamiento.
* Aproveche la red de datos de terceros de Audience Manager para refinar y expandir aún más las audiencias para el direccionamiento.


## Aplicaciones

* Audience Manager
* Real-time Customer Data Platform

Tanto el Audience Manager como Real-time Customer Data Platform se pueden aprovechar para impulsar el Audience Activation anónimo para destinos en el sitio y publicitarios. Tenga en cuenta que Real-time Customer Data Platform solo admite un subconjunto de destinos publicitarios con identificadores de dispositivo anónimos, tal como se catalogan en la variable [documentación de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=en).

Microsoft Bing, Google DV360 y TradeDesk son los principales destinos publicitarios de Real-time Customer Data Platform admitidos para la segmentación anónima basada en dispositivos. Además de esto, Real-time Customer Data Platform admite numerosos destinos conocidos basados en clientes, tal y como se catalogan en la variable [documentación de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=en) y tal como se describe en la sección [modelo conocido de activación de clientes](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).

## Arquitectura

<img src="assets/anonymous_activation.svg" alt="Arquitectura de referencia para el modelo de activación de audiencia anónima" style="width:80%; border:1px solid #4a4a4a" />

<br>

## Pasos de implementación para el Audience Manager

* Para obtener más información sobre la implementación del Audience Manager, consulte lo siguiente [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=es).

## Pasos de implementación de Real-time Customer Data Platform

* Para ver los pasos de implementación de Real-time Customer Data Platform, consulte lo siguiente [documentación](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).

## Documentación relacionada

* [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html?lang=es)
* [[!UICONTROL Audiencias] de Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=es)
* [Integrar Audience Manager con Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html?lang=es)
* [Compartir segmentos de Adobe Analytics a través de Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=es)
* [Modelo conocido de activación de cliente](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).
* [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html)
