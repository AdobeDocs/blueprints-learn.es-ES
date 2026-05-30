---
title: Recomendación de comportamiento
description: Obtenga información sobre cómo generar recomendaciones de elementos y contenido mediante estrategias de selección y modelos de clasificación.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: db16e773-e0da-46c4-9fa5-d16f04feb46b
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 5%

---

# Recomendación de comportamiento

En esta guía se describe el patrón de casos de uso de recomendaciones de comportamiento, que usa [!DNL Adobe Journey Optimizer] (AJO) Decisioning, [!DNL Real-Time Customer Data Platform] (RT-CDP) y [!DNL Adobe Experience Platform] (AEP) para ofrecer experiencias de recomendaciones personalizadas en los canales web, de aplicaciones móviles y de correo electrónico. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

Behavioral Recommendations genera recomendaciones de nivel de elemento o de nivel de contenido mediante señales de comportamiento (vistas de producto, compras, interacciones de contenido, consultas de búsqueda) combinadas con estrategias de selección y modelos de clasificación de AJO Decisioning. A diferencia de Offer Decisioning (que rige un conjunto limitado de ofertas, promociones o incentivos mediante reglas de elegibilidad y restricciones comerciales), este patrón funciona en catálogos de artículos grandes y que cambian continuamente (productos, artículos, vídeos) donde la selección se basa en señales de afinidad de comportamiento en lugar de en la elegibilidad regida.

## Patrón de caso de uso

**Recomendación de comportamiento**

Genere recomendaciones de nivel de elemento o de nivel de contenido basadas en señales de comportamiento, utilizando estrategias de selección de AJO Decisioning y modelos de clasificación para servir contenido contextual.

**Plan de ejecución:** Ingesta de señal de comportamiento > Evaluación de estrategia de toma de decisiones > Entrega de recomendaciones > Informes

## Resumen del caso de uso

Las organizaciones con catálogos de productos, bibliotecas de contenido o bibliotecas de medios deben mostrar los elementos más relevantes para cada visitante en función de su historial de comportamiento y de la actividad de la sesión. Ya sea un carrusel &quot;recomendado para usted&quot; en una página de inicio, un widget de venta cruzada en una página de detalles del producto o las recomendaciones de productos incrustadas en una campaña de correo electrónico, el desafío subyacente es el mismo: combine el perfil de comportamiento de cada visitante con los artículos más relevantes de un catálogo y, a continuación, envíe esas recomendaciones en el canal correcto en el momento adecuado.

Este patrón aborda ese desafío mediante la ingesta de señales de comportamiento en tiempo real mediante [!DNL Web SDK] o [!DNL Mobile SDK], el procesamiento mediante estrategias de selección de AJO Decisioning que combinan atributos de elemento con contexto de comportamiento y la entrega de los elementos recomendados a través de canales web, en la aplicación o de correo electrónico. Los modelos de clasificación pueden basarse en fórmulas (por ejemplo, ordenar por puntuación de afinidad de categoría) o en una clasificación de IA (por ejemplo, modelo de recomendación personalizado). El patrón también gestiona escenarios de inicio en frío para nuevos visitantes sin historial de comportamiento configurando recomendaciones de reserva.

La audiencia a la que se dirige este patrón incluye equipos de comercialización de comercio electrónico, equipos de personalización de contenido y equipos de experiencia digital que buscan mejorar la participación, la conversión y el valor promedio de los pedidos a través de recomendaciones personalizadas impulsadas por el comportamiento real del usuario.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### [Aumentar los ingresos de ventas cruzadas y ventas adicionales](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)

Promocione productos o servicios complementarios y de primera calidad a los clientes existentes en función del comportamiento y el historial de compras.

**KPI:** porcentaje de aumento de ventas/venta cruzada, ingresos incrementales, valor de duración del cliente

### [Aumentar las tasas de conversión](../../business-objectives/revenue-monetization/increase-conversion-rates.md)

Mejore el porcentaje de visitantes y clientes potenciales que completan las acciones deseadas, como compras, suscripciones o envíos de formularios.

**KPI:** tasas de conversión, conversión de posibles clientes, costo por posible cliente

### [Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo de vida individuales.

**KPI:** participación, tasas de conversión, satisfacción del cliente (CSAT)

## Casos de uso tácticos de ejemplo

Las siguientes son implementaciones tácticas comunes de este patrón:

- Widget de venta cruzada de productos en la página de detalles del producto (&quot;los clientes también compraron&quot;)
- Carrusel &quot;Recomendado para usted&quot; en la página principal en función del historial del explorador
- Recomendaciones de contenido en sitios multimedia según el comportamiento de lectura
- Widget de &quot;Artículos vistos recientemente&quot; combinado con elementos similares
- Recomendaciones de productos complementarios posteriores a la compra
- Enviar por correo electrónico recomendaciones de productos basadas en afinidad de comportamiento
- Recomendaciones específicas por categoría basadas en el comportamiento de exploración dentro de la sesión
- Volver a clasificar los resultados de búsqueda según las señales de comportamiento

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir la eficacia de las implementaciones de recomendaciones de comportamiento.

| KPI | Método de medición |
| --- | --- |
| Tasa de clics en recomendaciones (CTR) | Clics en artículos recomendados divididos por impresiones de recomendación |
| Tasa de conversión de recomendaciones | Compras o acciones deseadas desde clics en recomendaciones divididas por el total de clics en recomendaciones |
| Ingresos influidos por Recommendations | Ingresos totales de pedidos que incluyeron al menos un producto basado en recomendaciones |
| Alza del valor de pedido promedio (AOV) | Aumento en AOV para sesiones que se comprometieron con recomendaciones en comparación con sesiones sin recomendaciones |
| Artículos por pedido | Número de artículos por pedido para las sesiones dedicadas a recomendaciones |
| Cobertura de recomendación | Porcentaje de vistas de página o sesiones aptas que recibieron recomendaciones personalizadas (no de reserva) |
| Tasa de reserva de inicio en frío | Porcentaje de solicitudes de recomendación atendidas por lógica de reserva debido a un historial de comportamiento insuficiente |

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Adobe Journey Optimizer](AJO) Decisioning**: Estrategias de selección, modelos de clasificación, catálogos de elementos y políticas de decisión que evalúan las señales de comportamiento y devuelven los elementos más relevantes para cada visitante
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)**: acumulación de datos de perfil de comportamiento, evaluación de audiencia para ámbitos de recomendación y atributos calculados para puntuación de afinidad de comportamiento
- **[!DNL Adobe Experience Platform](AEP)** — Ingesta de evento de comportamiento a través de [!DNL Web SDK] y [!DNL Mobile SDK], procesamiento de [!DNL Edge Network], administración de esquema XDM para datos de catálogo y evento

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las tecnologías y capacidades utilizadas en este patrón.

### Administración de decisiones

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear calificadores de colección](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Entrega de ofertas mediante la API de Edge Decisioning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)

### Recopilación de datos y SDK web/móvil

- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Instalación de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [Información general de Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Información general sobre API de Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### XDM y modelado de datos

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Crear un conjunto de datos](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/create)
- [Definición de una relación entre dos esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-api)

### Identidad y perfil

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Resumen del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Atributos calculados y enriquecimiento de perfiles

- [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Guía de IU de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Información general sobre Customer AI](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configuración de superficies de canal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)

### Creación y personalización de mensajes

- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### Informes y análisis

- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Resumen de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

### Gobernanza de datos y ciclo vital

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Información general sobre Advanced Data Lifecycle Management](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [Caducidad de conjuntos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration)

### Monitorización y observabilidad

- [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
- [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones de ingesta](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [Protecciones del servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)

### Tutoriales y guías

- [Información general de orígenes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Información general sobre etiquetas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
- [Grupo de campos de consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
