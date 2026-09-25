---
title: Customer Journey Analytics con Real-time Customer Data Platform
description: Unifique y analice los datos y los comportamientos de los clientes desde todo el recorrido del cliente en Customer Journey Analytics y publique la audiencia de CJA a RTCDP
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
TQID: https://experienceleague.adobe.com/gbNXsco0cQIcn5O83ofB-rb0PF65v7kaTZ7mTngqHks
product_v2:
  - id: e98b7246-966c-4318-9e95-cad2f7a17dc7
    internal-label: Customer Journey Analytics
feature_v2:
  - id: ce577701-5b9e-4fe4-8fa3-4eedea976da4
    internal-label: Components
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 8%
---

# Adobe Customer Journey Analytics

Adobe Customer Journey Analytics unifica los datos de interacción del cliente de Adobe Experience Platform y otras fuentes en un servicio de análisis basado en el recorrido. Esta arquitectura proporciona la referencia principal para el análisis entre canales, las derivaciones de CJA B2B y la publicación de audiencias de CJA en Real-Time CDP.

## Arquitectura de Customer Journey Analytics

Este diagrama muestra el flujo principal de datos de interacción del cliente en Customer Journey Analytics para conexiones, vistas de datos, análisis y creación de audiencias.

![Arquitectura principal de Adobe Customer Journey Analytics](assets/cja.png){width="1000" zoomable="yes"}

## Derivaciones de arquitectura

- B2B Customer Journey Analytics amplía la arquitectura principal con dimensiones de cuenta, oportunidad, grupo de compra y persona para el análisis basado en cuentas.
- El uso compartido de audiencias de CJA publica audiencias creadas de Customer Journey Analytics a Real-Time CDP para su activación y ejecución posterior del recorrido.

## Flujos de datos principales y puntos de integración

- Los datos de interacción del cliente se recopilan de fuentes web, móviles, comerciales, CRM y de otro tipo en Adobe Experience Platform.
- Los conjuntos de datos de Experience Platform se seleccionan en una conexión de Customer Journey Analytics.
- Las vistas de datos exponen métricas, dimensiones y campos calculados para el análisis en canales múltiples.
- Las audiencias de Customer Journey Analytics se pueden publicar en Real-Time CDP para su activación.
- Las perspectivas de Customer Journey Analytics se pueden utilizar con Journey Optimizer a través de la arquitectura de integración dedicada.

## Patrones de casos de uso admitidos

- [Análisis B2B](/help/blueprints/use-case-patterns/b2b/account-analytics.md): Analice los recorridos de cuenta, oportunidad y nivel de persona con dimensiones B2B.
- [Generación de Customer Analytics y insight](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md): Analice el comportamiento en canales múltiples y genere perspectivas de recorrido.

## Lectura adicional

- [Información general de Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview)
- [Conexiones de Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-connections/create-connection)
- [Publicación de audiencias de Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/audiences/publish)
