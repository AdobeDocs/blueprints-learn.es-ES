---
title: Mensajería activada por eventos
description: Aprenda a entregar mensajes contextuales en tiempo real en respuesta a eventos de comportamiento o del sistema.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 75137990-9848-40c0-abf3-adbd21d2de52
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1955'
ht-degree: 5%

---

# Mensajería activada por eventos

En esta guía se describe el patrón de caso de uso de mensajería activada por eventos, que utiliza [!DNL Adobe Journey Optimizer] (AJO), [!DNL Real-Time Customer Data Platform] (RT-CDP) y [!DNL Adobe Experience Platform] (AEP) para entregar mensajes contextuales en tiempo real en respuesta a eventos de comportamiento o del sistema. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

Este patrón cubre el ciclo de vida completo, desde la ingesta de eventos y la creación de recorridos hasta la entrega de mensajes y la creación de informes de rendimiento.

## Patrón de caso de uso

En esta sección se describe el patrón principal y el plan de ejecución que impulsa la mensajería activada por eventos.

**Mensajería activada por eventos**

Escuche un evento del sistema o de comportamiento en tiempo real y, a continuación, envíe un mensaje contextual al perfil de activación.

**Plan de ejecución:** Ingesta de eventos > Entrada de Recorrido > Evaluación de condiciones > Entrega de mensajes > Informes

## Resumen del caso de uso

La mensajería activada por eventos ofrece un mensaje contextual en respuesta a un evento del sistema o de comportamiento en tiempo real. A diferencia de la activación de mensajes salientes por lotes, que envía a una audiencia preevaluada según una programación, este patrón escucha un evento correspondiente (como el abandono del carro de compras, una sesión de exploración, un envío de formulario o un cambio de estado del sistema) e introduce inmediatamente el perfil de activación en un recorrido que evalúa las condiciones y envía un mensaje.

El patrón se basa en la transmisión de eventos en tiempo real a AEP (a través de Web SDK, Mobile SDK o API del lado del servidor), un recorrido con una entrada de evento unitario en AJO y una lógica de evaluación de condiciones que determina si se debe enviar y qué. El mensaje se envía normalmente pocos minutos después del evento de activación, lo que hace que este patrón sea ideal para comunicaciones contextualmente relevantes y con distinción de tiempo.

Las organizaciones utilizan este patrón para responder a las acciones de los clientes en tiempo real, lo que aumenta la relevancia e impulsa tasas de participación y conversión más altas en comparación con las comunicaciones por lotes programadas. Entre los escenarios comunes se incluyen la recuperación del carro de compras abandonado, el seguimiento posterior a la compra, los mensajes de bienvenida después del registro y las notificaciones con distinción de tiempo, como errores de pago o alertas de caída de precios.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

**[Recuperar carros y recorridos abandonados](../../business-objectives/customer-experience/recover-abandoned-carts-journeys.md)**

Vuelva a atraer a los usuarios que abandonaron durante los flujos de compra, solicitud o inscripción con seguimientos personalizados y oportunos.

| KPI |
| --- |
| Tasas de conversión, ingresos incrementales, participación |

**[Aumentar las tasas de conversión](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

Mejore el porcentaje de visitantes y clientes potenciales que completan las acciones deseadas, como compras, suscripciones o envíos de formularios.

| KPI |
| --- |
| Tasas de conversión, Conversión de cliente potencial, Coste por cliente potencial |

**[Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo de vida individuales.

| KPI |
| --- |
| Participación, tasas de conversión, satisfacción del cliente (CSAT) |

**[Mejorar la incorporación de los clientes](../../business-objectives/customer-experience/improve-customer-onboarding.md)**

Acelere el tiempo de respuesta al valor para los nuevos clientes con experiencias de bienvenida y recorridos de activación optimizados y personalizados.

| KPI |
| --- |
| Participación, Retención, Tasas de conversión |

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran cómo se puede aplicar la mensajería activada por eventos a distintos contextos comerciales.

- **Correo electrónico o SMS de abandono del carro de compras**: envía un mensaje recordatorio cuando un cliente agrega artículos al carro de compras, pero no completa la compra en un plazo definido
- **Seguimiento del abandono del examen**: vuelva a atraer visitantes que vieron productos o contenido pero no realizaron una acción de conversión
- **Agradecimiento o venta cruzada posterior a la compra**: envíe una confirmación y una recomendación de venta cruzada inmediatamente después de un evento de compra
- **Recordatorio de caducidad de prueba**: notifique a los usuarios que se aproximen al final de una prueba gratuita con mensajes de renovación o conversión
- **Mensaje de bienvenida después del registro**: envíe un mensaje de incorporación inmediato cuando un nuevo usuario se registre o cree una cuenta
- **Confirmación de envío de formulario**: reconozca los envíos de formularios (solicitudes de contacto, solicitudes e inscripciones) con una confirmación contextual
- **Notificación de error de pago**: avisa a los clientes cuando un pago recurrente falla y les solicita que actualicen la información de pago
- **Notificación push de recuperación tras la desinstalación de la aplicación**: Déclencheur de un mensaje de recuperación cuando un usuario desinstala una aplicación móvil
- **Confirmación de reserva o cita** — Enviar confirmación inmediata después de que se programe una reserva, reserva o cita
- **Alerta de bajada de precios para artículos en la lista de deseos** — Notificar a los clientes cuando un producto en su lista de deseos baje de precio

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir la eficacia de las implementaciones de mensajería activadas por eventos.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de conversión | Porcentaje de destinatarios de mensajes activados que completan la acción deseada (compra, registro, renovación) | Conversiones / Mensajes entregados * 100 |
| Ingresos incrementales | Ingresos adicionales atribuibles a mensajes activados por eventos en comparación con los grupos de control sin envío | Ingresos de envíos activados: línea base del grupo de control |
| Tasa de apertura | Porcentaje de mensajes enviados que abren los destinatarios | Aperturas / Entregas * 100 |
| Tasa de clics (CTR) | Porcentaje de mensajes enviados que generan al menos un clic | Clics/Entregados * 100 |
| Tiempo de conversión | Tiempo promedio transcurrido entre el envío del mensaje y el evento de conversión | Avg(marca de tiempo de conversión - marca de tiempo de entrega) |
| Tasa de finalización de recorridos | Porcentaje de perfiles que entran en el recorrido y llegan al paso de entrega de mensajes (no perdidos por condiciones o salidas) | Perfiles que llegan a la entrega / Perfiles que entran en el recorrido * 100 |
| Tasa de supresión de mensajes | Porcentaje de perfiles calificados suprimidos debido a límites de frecuencia, consentimiento o evaluación de condición | Perfiles suprimidos / Perfiles cualificados totales * 100 |
| Tasa de devoluciones | Porcentaje de mensajes que no se pudieron enviar debido a mensajes devueltos no entregados o rechazados | Devoluciones / Enviados * 100 |

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones de Adobe.

- **[!DNL Adobe Journey Optimizer](AJO)**: orquestación de Recorrido con entrada de evento unitario, evaluación de condición, pasos de espera, creación de mensajes, configuración de canal, control de frecuencia e informes de envío
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)**: evaluación de audiencias para filtrado basado en condiciones dentro de los recorridos, aplicación del consentimiento y del control, enriquecimiento de perfiles
- **[!DNL Adobe Experience Platform](AEP)**: ingesta de eventos en tiempo real mediante Web SDK, Mobile SDK o API del lado del servidor; modelado de datos; resolución de identidades; Edge Network

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las capacidades utilizadas en esta implementación.

### orquestación de recorrido

- [Introducción a los recorridos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Crear un recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propiedades del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Eventos generales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de calificación de público](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Actividad de condición](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Actividad Esperar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Añadir un mensaje en un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Criterios de salida](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [administración de entradas de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Prueba del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicación del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Crear grupos de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [planes de calentamiento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configuración de superficie de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Administrar lista de supresión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Creación y personalización de mensajes

- [Crear un correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funciones de ayuda](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Creación de un mensaje SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Diseño de una notificación push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### Frecuencia y reglas empresariales

- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Información general sobre reglas comerciales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [API de límite](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/channel-surfaces/capping)

### Administración de conflictos y prioridades

- [Introducción a la administración de conflictos y prioridades](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Identificación de posibles conflictos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [restricción y arbitraje de recorridos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### Creación de informes y rendimiento

- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### Recopilación e ingesta de datos

- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Información general de Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Información general sobre API de Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Resumen de ingesta de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview)

### Modelado de datos y esquemas

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### Identidad y perfil

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Reglas de vinculación de gráficos de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Resumen del perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Segmentación y audiencias

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)

### Gobernanza de datos y consentimiento

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Grupo de campos de consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Atributos calculados

- [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Guía de IU de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)

### Monitorización y observabilidad

- [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones de ingesta](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### Tutoriales y guías

- [Tutorial sobre Creación de un recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Instalación de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
