---
title: Recorrido en canales múltiples con toma de decisiones
description: Aprenda a organizar un recorrido de varios pasos que incorpore decisiones en tiempo real para seleccionar un canal, contenido u oferta óptimos.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: eabdd91f-bb7d-4de3-adb5-5940d3ca4a78
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1983'
ht-degree: 5%

---

# Recorrido en canales múltiples con toma de decisiones

En esta guía se describe el recorrido en canales múltiples con el patrón de casos de uso de decisiones, que usa [!DNL Adobe Journey Optimizer] y [!DNL Adobe Real-Time Customer Data Platform] para orquestar recorridos multicanal de varios pasos que incorporan la toma de decisiones en tiempo real en uno o más nodos de recorrido. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

El recorrido en canales múltiples con toma de decisiones es el patrón de orquestación de campaña más sofisticado en el ecosistema [!DNL Adobe Experience Platform]. Amplía los recorridos organizados en varios pasos al incorporar la toma de decisiones en tiempo real (mediante [!DNL AJO] Decisioning) para evaluar el contexto actual de un perfil y seleccionar dinámicamente el canal, el contenido o la oferta óptimos en uno o más puntos de decisión dentro del lienzo de recorrido.

## Patrón de caso de uso

**recorrido en canales múltiples con toma de decisiones**

Orqueste un recorrido de varios pasos y canales que incorpore la toma de decisiones en tiempo real en uno o más nodos para seleccionar el canal, el contenido o la oferta óptimos.

**Plan de ejecución:** Evaluación de audiencia > Ejecución de Recorrido > Nodo de decisión > Selección de canal > Entrega de mensaje > Informes

## Resumen del caso de uso

Las organizaciones necesitan cada vez más ofrecer recorridos de cliente adaptables y personalizados que respondan dinámicamente al contexto en tiempo real de cada individuo en lugar de seguir una secuencia fija y predeterminada. El canal preferido de un cliente, su historial de participación, su nivel de lealtad, su valor de duración predicho y sus intereses actuales de productos dependen de cuál debe ser la mejor acción siguiente en cada punto de contacto.

El recorrido en canales múltiples con toma de decisiones aborda esta necesidad combinando dos potentes capacidades de [!DNL AJO]: orquestación de recorrido (que administra el flujo de varios pasos, el tiempo, las condiciones y la entrega de canal) y toma de decisiones (que evalúa las reglas de elegibilidad, aplica estrategias de clasificación y selecciona la oferta óptima o la variante de contenido en cada punto de decisión).

Este patrón es adecuado cuando:

- El recorrido debe adaptarse dinámicamente al estado en tiempo real de cada perfil en lugar de seguir un canal fijo o una secuencia de contenido
- Varias ofertas, variantes de contenido o canales son candidatos en uno o más nodos de recorrido y la mejor opción debe seleccionarse en función del contexto del perfil
- Se necesita una clasificación asistida por IA o basada en fórmulas para optimizar la selección de ofertas en todo el recorrido
- La organización desea consolidar la lógica de selección de canales y la administración de ofertas en un marco de decisión centralizado, en lugar de mantener una lógica de ramificación compleja

La audiencia de destino incluye a los especialistas en marketing que administran programas del ciclo vital, recorridos de lealtad, secuencias de recuperación e flujos de incorporación en los que la personalización a escala requiere la toma de decisiones automatizada en cada punto de contacto.

>[!NOTE]
>Si el recorrido no requiere la toma de decisiones dinámica en nodos individuales (por ejemplo, un programa de nutrición o de incorporación de secuencia fija), consulte [recorrido orquestado de varios pasos](multi-step-orchestrated-journey.md). Ese patrón es más sencillo de configurar y no requiere AJO Decisioning.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

**[Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo de vida individuales.
**KPI:** participación, tasas de conversión, satisfacción del cliente (CSAT)

**[Aumentar la lealtad del cliente y el valor de duración](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
Profundice las relaciones con los clientes y maximice el valor a largo plazo mediante programas de fidelidad, recompensas y participación personalizada.
**KPI:** valor de duración del cliente, retención, aumento de venta/venta cruzada %

**[Mejorar la retención de clientes](../../business-objectives/customer-experience/improve-customer-retention.md)**
Mantenga el compromiso de los clientes existentes y renuévelos mediante experiencias basadas en valores y una nutrición continua de las relaciones.
**KPI:** retención, valor de duración del cliente, participación

**[Aumentar los ingresos de ventas cruzadas y ventas adicionales](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
Promocione productos o servicios complementarios y de primera calidad a los clientes existentes en función del comportamiento y el historial de compras.
**KPI:** % de aumento de ventas/venta cruzada, ingresos incrementales, valor de duración del cliente

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran cómo se puede aplicar en la práctica el recorrido entre canales con la toma de decisiones.

- **recorrido adaptable de recuperación**: un recorrido de varios pasos donde la toma de decisiones selecciona el canal (correo electrónico, push o SMS) en función del historial de participación de cada perfil y selecciona dinámicamente la mejor oferta de incentivos en función del valor de duración predicho
- **recorrido del ciclo de vida de la siguiente mejor acción**: la toma de decisiones determina qué comunicar en cada fase del ciclo de vida del cliente, seleccionando entre contenido de incorporación, ofertas de venta cruzada, recompensas por fidelidad o incentivos de retención
- **Incorporación personalizada con selección de contenido dinámico**: nuevo recorrido de incorporación del cliente en el que cada punto de contacto utiliza la toma de decisiones para seleccionar el contenido de educación del producto, las sugerencias o las ofertas de activación más relevantes
- **recorrido de programas de fidelización en canales múltiples con recompensas personalizadas**: los miembros de fidelidad progresan a través de un recorrido en el que la toma de decisiones selecciona ofertas de recompensas personalizadas basadas en el nivel, el historial de compras y la afinidad de la categoría
- **Reparticipación dinámica con la optimización de canales e incentivos**: reparticipación inactiva de clientes donde tanto el canal de alcance como el incentivo se seleccionan dinámicamente para maximizar la probabilidad de respuesta
- **Nutrición del ciclo de vida del cliente con recomendaciones de contenido clasificado por IA**: recorrido de nutrición continua en el que la toma de decisiones clasificadas por IA selecciona las recomendaciones de contenido o producto más relevantes en cada punto de contacto

## Indicadores clave de rendimiento

Utilice los siguientes KPI para medir la eficacia de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de finalización de recorridos | Porcentaje de perfiles que completan el recorrido completo | Informe de recorrido: completado/introducido |
| Tasa de aceptación de ofertas | Porcentaje de ofertas seleccionadas para la toma de decisiones que participan en (se hace clic y se canjea) | Informe de decisiones: clics en ofertas / impresiones de ofertas |
| Tasa de participación en canal | Tasas de apertura y clics en cada canal utilizado en el recorrido | Métricas de envío por canal en el informe de recorrido |
| Tasa de conversión | Porcentaje de participantes en el recorrido que completan la acción de conversión de destino | Seguimiento de eventos de salida de recorrido para análisis de CJA funnel |
| Tasa de ofertas de reserva | Porcentaje de solicitudes de decisión que devuelven la oferta de reserva en lugar de una oferta personalizada | Informe de decisiones: selecciones de reserva/selecciones totales |
| Impacto en valor de duración de cliente | Cambio en CLV para los participantes del recorrido frente al grupo de control | Análisis de cohorte de CJA con comparación de exclusión |
| Ingresos de venta cruzada/aumento de ventas | Ingresos incrementales atribuidos a ofertas seleccionadas para la toma de decisiones | Análisis de atribución de CJA en conversiones impulsadas por ofertas |
| Eficacia de clasificación de decisiones | Diferencia de rendimiento entre ofertas clasificadas por IA y selección aleatoria/basada en prioridad | Experimento A/B que compara estrategias de clasificación |

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón de caso de uso.

- **[!DNL Adobe Journey Optimizer] ([!DNL AJO])**: orquestación de Recorrido (diseño de lienzo de varios pasos, condiciones de entrada, esperas, condiciones, criterios de salida), creación de mensajes en todos los canales, configuración de superficie de canal, administración de conflictos y prioridades
- **[!DNL Adobe Journey Optimizer]decisión**: administración de ofertas y elementos de contenido, reglas de elegibilidad, estrategias de clasificación (prioridad, fórmula, IA), políticas de decisión, ubicaciones, ofertas de reserva
- **[!DNL Adobe Real-Time Customer Data Platform] ([!DNL RT-CDP])**: evaluación de audiencia para segmentos de idoneidad de entrada de recorrido y oferta, enriquecimiento de perfil con atributos calculados y puntuaciones de tendencia, aplicación de consentimiento y gobernanza
- **[!DNL Adobe Experience Platform] ([!DNL AEP])**: almacén de perfiles de cliente en tiempo real, servicio de identidad para resolución en canales múltiples, modelado de datos e infraestructura de ingesta

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las capacidades utilizadas en este patrón de caso de uso.

### orquestación de recorrido

- [Introducción a los recorridos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Crear un recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propiedades del recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Leer actividad de audiencia](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Eventos generales](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de calificación de público](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Actividad de condición](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Actividad Esperar](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Añadir un mensaje en un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Criterios de salida](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [administración de entradas de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Prueba del recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicación del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### Administración de decisiones

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear calificadores de colección](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Crear grupos de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [planes de calentamiento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configuración de superficie de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configuración del canal SMS](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Creación y personalización de mensajes

- [Crear un correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/create-email)
- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Administración de conflictos, prioridades y frecuencias

- [Resumen de administración de conflictos y prioridades](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificación de posibles conflictos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [restricción y arbitraje de recorridos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Composición de audiencia](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/audience-composition)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/pql/overview)

### Informes y análisis

- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Información general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/home)

### Perfil e identidad

- [Resumen del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/home)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview)
- [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview)
- [Información general sobre Customer AI](https://experienceleague.adobe.com/es/docs/experience-platform/intelligent-services/customer-ai/overview)

### Gobernanza de datos y consentimiento

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Administrar lista de supresión](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- [Protecciones del servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/guardrails)
