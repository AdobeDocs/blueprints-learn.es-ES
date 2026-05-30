---
title: Recorrido orquestado de varios pasos
description: Aprenda a guiar un perfil a través de un recorrido ramificado y multitáctil con esperas, condiciones y varias acciones de mensaje a lo largo del tiempo.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 5667b188-1b20-4a85-aebb-74efd5f771a1
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1798'
ht-degree: 5%

---

# Recorrido orquestado de varios pasos

En esta guía se describe el patrón de caso de uso de recorrido orquestado de varios pasos, que usa [!DNL Adobe Journey Optimizer] (AJO) y [!DNL Real-Time Customer Data Platform] (RT-CDP) para orquestar recorridos de clientes multitáctiles y ramificados que envían varios mensajes a lo largo del tiempo. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

## Patrón de caso de uso

**Recorrido orquestado de varios pasos**

Guía de un perfil a través de un recorrido ramificado y multitáctil con esperas, condiciones y varias acciones de mensaje a lo largo del tiempo.

**Plan de ejecución:** Evaluación de audiencia > Ejecución de Recorrido (varios nodos) > Bifurcación de condiciones > Entrega de mensajes (xN) > Criterios de salida > Informes

## Resumen del caso de uso

Los recorridos organizados en varios pasos se dirigen a escenarios comerciales en los que un solo mensaje es insuficiente para lograr el resultado deseado del cliente. En lugar de un envío único, el recorrido guía a cada perfil a través de una secuencia de puntos de contacto (correos electrónicos, mensajes SMS, notificaciones push o mensajes en la aplicación) espaciados entre días o semanas, con una lógica de ramificación que adapta la ruta en función de atributos de perfil, señales de comportamiento o datos de evento.

Estos recorridos son el patrón de campaña más complejo de AJO. Combinan entradas basadas en audiencias o en eventos con un lienzo de nodos de acción (mensajes), nodos de condición (lógica de ramificación), nodos de espera (retrasos de tiempo) y criterios de salida (eventos de conversión o tiempos de espera). Cada perfil progresa a través del recorrido de forma independiente, a su propio ritmo, recibiendo contenido relevante contextualmente en cada paso.

Este patrón subsume los patrones más simples: activación de mensajes salientes por lotes para campañas de un solo envío y mensajería activada por eventos para respuestas de un solo evento. Utilice este patrón cuando el caso de uso requiera alimentar un perfil a través de varias interacciones a lo largo del tiempo.

>[!NOTE]
>Si su recorrido requiere una selección dinámica de la oferta, el contenido o el canal óptimos en puntos de decisión individuales, consulte [recorrido en canales múltiples con toma de decisiones](cross-channel-journey-with-decisioning.md). Ese patrón amplía este con la integración de AJO Decisioning.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Mejorar la retención de clientes

Mantenga el compromiso de los clientes existentes y renuévelos mediante experiencias basadas en valores y una nutrición continua de las relaciones.

**KPI:** retención, valor de duración del cliente, participación

[Más información sobre la mejora de la retención de clientes](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### Mejore la incorporación del cliente

Acelere el tiempo de respuesta al valor para los nuevos clientes con experiencias de bienvenida y recorridos de activación optimizados y personalizados.

**KPI:** participación, retención, tasas de conversión

[Más información sobre la mejora de la incorporación del cliente](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)

### Reactivar clientes inactivos

Recupere clientes inactivos o caducados con campañas de reactivación dirigidas basadas en señales de comportamiento.

**KPI:** participación, retención, tasas de conversión

[Más información sobre la mejora de la retención de clientes](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### Recuperar carros y recorridos abandonados

Vuelva a atraer a los usuarios que abandonaron durante los flujos de compra, solicitud o inscripción con seguimientos personalizados y oportunos.

**KPI:** tasas de conversión, ingresos incrementales, participación

[Más información sobre la recuperación de carros de compras y recorridos abandonados](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran aplicaciones comunes del patrón de recorrido orquestado de varios pasos.

- **Serie de incorporación del cliente**: correo electrónico de bienvenida, seguido de educación sobre las funciones y un mensaje de activación durante los primeros 14 días posteriores al registro
- **Campaña de goteo de renovación de participación**: un correo electrónico recordatorio, una oferta de incentivo y un aviso final para los clientes caducados durante 3 semanas.
- **recorrido de hito de fidelización**: notificación de actualización de nivel, seguida de una oferta exclusiva y, a continuación, un recordatorio de renovación conforme se acerca el aniversario de la pertenencia
- **Secuencia de recuperación**: correo electrónico de &quot;Te echamos de menos&quot;, después una oferta de descuento por correo electrónico y, por último, un recordatorio SMS para los compradores que hayan caducado
- **recorrido de adopción de productos**: bienvenida de prueba, sugerencias de uso y solicitud de actualización a medida que avance el período de prueba
- **Secuencia de renovación de suscripción**: aviso con 30 días de antelación, recordatorio de 7 días y un mensaje de día de caducidad para próximas renovaciones de suscripción
- **Servicio poscompra**: correo electrónico de agradecimiento, guía de uso, recomendación de venta cruzada y solicitud de revisión más de 30 días después de la compra

## Indicadores clave de rendimiento

Utilice los siguientes KPI para medir la eficacia de la implementación de recorridos organizados en varios pasos.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de finalización de recorridos | Porcentaje de perfiles que completan el recorrido completo sin una salida anticipada | Informe de recorrido: Salido (completado) / Ingresado |
| Tasa de conversión de etapas | Porcentaje de perfiles que progresan de un paso al siguiente | Métricas por nodo en el informe de recorrido |
| Tasa de participación en canal | Tasas de apertura, tasas de pulsaciones y tasas de respuesta en cada punto de contacto | Métricas de envío y participación por mensaje |
| Tasa de conversión de criterios de salida | Porcentaje de perfiles que almacenan en déclencheur el evento de salida (por ejemplo, compra, registro) antes del tiempo de espera de recorrido | Recuento de visitas de criterios de salida/Total introducido |
| Tiempo de conversión | Duración media desde la entrada de recorrido hasta el evento de criterios de salida | Recorrido analytics: marca de tiempo de entrada a la marca de tiempo del evento de conversión |
| Tasa de entrega de recorridos | Porcentaje de perfiles que dejan de interactuar en cada paso (análisis de abandonos) | Visualización de abandonos de CJA en varios pasos del recorrido |
| Tasa de retención/renovación de la participación | Porcentaje de perfiles objetivo que vuelven al estado activo | Análisis de comportamiento posterior al recorrido en CJA |

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón de caso de uso.

- **[!DNL Adobe Journey Optimizer] (AJO)**: motor de orquestación de Recorrido, creación de mensajes, configuración de canal, experimentación de contenido, administración de frecuencia y conflictos y sistema de informes
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)**: evaluación y definición de audiencias para audiencias de entrada de recorrido, datos de perfil para personalización y bifurcación de condiciones
- **[!DNL Adobe Experience Platform] (AEP)**: almacén de perfiles, servicio de identidad, ingesta de datos de evento e infraestructura de datos básica

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las capacidades utilizadas en esta implementación.

### Recorridos

- [Introducción a los recorridos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Crear un recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propiedades del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Publicación del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)
- [Prueba del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)

### actividades de recorrido

- [Leer actividad de audiencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Eventos generales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de calificación de público](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Actividad de condición](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Actividad Esperar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Añadir un mensaje en un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Actividad Finalizar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/end-activity)
- [Configuración de una acción personalizada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions)

### Administración de entrada y salida

- [administración de entradas de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Criterios de salida](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configuración de superficies de canal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Crear grupos de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [planes de calentamiento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Creación y personalización de mensajes

- [Crear un correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Uso de componentes de contenido de Email Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funciones de ayuda](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Experimentación de contenido

- [Introducción al experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Cálculos estadísticos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### Frecuencia, conflicto y prioridad

- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Información general sobre reglas comerciales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Introducción a la administración de conflictos y prioridades](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [restricción y arbitraje de recorridos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Identificación de posibles conflictos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/edge-segmentation)

### Informes y análisis

- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)

### Consentimiento y control

- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Administrar lista de supresión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Base de datos

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Resumen del perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
