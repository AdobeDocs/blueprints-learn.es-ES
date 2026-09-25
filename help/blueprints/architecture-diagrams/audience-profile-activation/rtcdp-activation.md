---
title: Activación de Adobe Real-Time CDP
description: Referencia de arquitectura para activar audiencias y datos de perfil de Adobe Real-Time CDP en destinos publicitarios, sociales, de almacenamiento en la nube y empresariales.
solution: Real-Time Customer Data Platform, Experience Platform
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%
---
# Activación de Adobe Real-Time CDP

Esta arquitectura muestra cómo Adobe [!DNL Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) activa las audiencias y los datos de perfil en destinos publicitarios, sociales, de almacenamiento en la nube y empresariales a través de flujos de datos de flujo continuo y por lotes.

## Activación de audiencia y perfil

La arquitectura ilustra la ruta de activación compartida desde las audiencias y perfiles de [!DNL Real-Time CDP] hasta las aplicaciones de destino. Incluye la activación de destino para plataformas publicitarias y sociales, así como destinos empresariales utilizados para flujos de trabajo de aplicaciones de almacenamiento, análisis y flujo descendente.

![Arquitectura de activación de perfiles y audiencias de Adobe Real-Time CDP](assets/real_time_cdp_activation.png){width="1000" zoomable="yes"}

## Patrones de casos de uso admitidos

La arquitectura anterior admite los siguientes patrones de casos de uso:

- [Activación de audiencias en destinos](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md): active audiencias evaluadas en publicidad, medios sociales, almacenamiento en la nube, CRM y otros destinos empresariales.
- [Personalización web anónima de visitantes](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md): admite la activación de audiencias y la personalización basada en perfiles en canales digitales.

## Flujos de datos principales y puntos de integración

- Ingresar datos de clientes de varios orígenes en [!DNL Real-Time CDP].
- Unificar la identidad y los atributos de perfil en [!DNL Real-Time Customer Profile].
- Evaluar perfiles en audiencias para su activación.
- Transmita o procese cambios de audiencia y perfil a destinos publicitarios, sociales, de almacenamiento en la nube y empresariales.
- Utilice perfiles y datos de audiencia activados en flujos de trabajo de marketing, ventas, asistencia, análisis y personalización descendentes.

## Lectura adicional

- [Destinos de Adobe Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Activar audiencias en destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [protecciones de Adobe Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview)
