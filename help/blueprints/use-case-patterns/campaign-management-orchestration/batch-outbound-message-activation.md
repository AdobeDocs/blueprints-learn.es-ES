---
title: Activación de mensaje saliente por lotes
description: Obtenga información sobre cómo evaluar una audiencia y enviar un mensaje saliente programado en una sola ejecución por lotes.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 192853ce-02ab-46e6-9092-3db5354bc19c
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 4%

---

# Activación de mensaje saliente por lotes

En esta guía se describe el patrón de caso de uso de activación de mensajes salientes por lotes, que utiliza [!DNL Adobe Journey Optimizer] (AJO) y [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP) para entregar mensajes salientes programados a segmentos de audiencia definidos. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

La activación de mensajes salientes por lotes es el patrón de campaña básico para la mensajería saliente de uno a varios. Abarca todo el ciclo de vida, desde la definición de la audiencia hasta la entrega de mensajes y el análisis de rendimiento.

## Patrón de caso de uso

**Activación de mensaje saliente en lote**

Evalúe una audiencia y luego envíe un mensaje saliente programado (correo electrónico, SMS, push) a todos los perfiles aptos en una sola ejecución por lotes.

**Plan de ejecución:** Evaluación de audiencia > Creación de mensajes > Ejecución de campaña > Informes

## Resumen del caso de uso

Con frecuencia, las organizaciones necesitan enviar un solo mensaje a un segmento de audiencia conocido en un momento específico o en respuesta a un evento del sistema. Este patrón resuelve ese requisito combinando la evaluación de audiencias en [!DNL RT-CDP] con la creación de mensajes y la ejecución de campañas en [!DNL Journey Optimizer].

El escenario empresarial es sencillo: defina quién debe recibir el mensaje, cree el contenido del mensaje con personalización, vincule la audiencia y el mensaje a una campaña o recorrido y ejecute el envío según una programación, mediante calificación de audiencia o a través de un déclencheur del sistema. El resultado es un mensaje enviado con informes completos sobre las métricas de entrega, participación y conversión.

Este patrón se aplica siempre que se puede avanzar en un objetivo empresarial enviando un solo mensaje a una audiencia conocida en una ejecución. Se diferencia de la mensajería activada por eventos, que responde a eventos de comportamiento en tiempo real, y de los recorridos organizados de varios pasos, que guían los perfiles a través de varios puntos de contacto a lo largo del tiempo. La activación por lotes es el patrón de campaña más sencillo y el punto de partida más común para los casos de uso de mensajería saliente.

## Objetivos empresariales clave

Esta sección identifica los objetivos comerciales principales que admite la activación de mensajes salientes por lotes.

### Aumentar la participación en campañas y correos electrónicos

**Descripción:** mejore las tasas de apertura, las tasas de pulsaciones y la respuesta general de la campaña mediante el contenido optimizado y el direccionamiento.

**KPI:** tasas de apertura, participación, tasas de conversión

### Aumentar ingresos y ventas

**Descripción:** Impulse el crecimiento de los ingresos de primera línea a través de canales digitales optimizados, campañas y recorridos de clientes.

**KPI:** tasas de conversión, ingresos incrementales, valor de pedido promedio

**Objetivo comercial relacionado:** [Aumentar ingresos y ventas](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

### Optimización de la ejecución de campañas

**Descripción:** Reduzca el tiempo de compilación de la campaña y simplifique la entrega de campañas multicanal a través de plantillas, automatización y procesos estandarizados.

**KPI:** velocidad de comercialización, eficiencia, tiempo de finalización %

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran aplicaciones comunes de la activación de mensajes salientes por lotes.

- **Anuncio de venta o explosión de correo electrónico promocional** — Difunde una oferta promocional a un segmento de clientes elegibles en una fecha programada
- **Notificación push de lanzamiento del producto** — Notificar a los clientes interesados sobre la disponibilidad de un nuevo producto mediante notificación push
- **Boletín o correo electrónico de resumen** — Enviar resúmenes de contenido periódicos a las audiencias de los suscriptores
- **Invitación de registro de evento** — Invite a posibles clientes calificados a seminarios web, conferencias o eventos presenciales
- **Correo electrónico de recordatorio de renovación de suscripción**: recuerde a los clientes que se acercan a las fechas de renovación que deben tomar medidas
- **Notificación de hito del programa de fidelización**: felicite a los miembros que alcanzan niveles de fidelidad o umbrales de puntos
- **Correo electrónico específico de call-to-action**: Impulse una acción de destino como completar una compra, actualizar las preferencias o registrarse en un programa
- **Campaña de SMS para venta flash u oferta por tiempo limitado** — Envíe promociones urgentes por tiempo limitado a través de SMS a audiencias de inclusión

## Indicadores clave de rendimiento

En la tabla siguiente se definen los KPI utilizados para medir la eficacia de la campaña.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de entrega | Porcentaje de mensajes enviados correctamente a los destinatarios | Entregado/enviado x 100 |
| Tasa de apertura | Porcentaje de mensajes enviados abiertos por los destinatarios | Aperturas únicas / Entregas x 100 |
| Tasa de clics (CTR) | Porcentaje de mensajes entregados en los que se hizo clic en un vínculo | Clics únicos / Entregados x 100 |
| Tasa de pulsaciones para abrir (CTOR) | Porcentaje de mensajes abiertos en los que se hizo clic en un vínculo | Clics únicos/Aperturas únicas x 100 |
| Tasa de conversión | Porcentaje de destinatarios que completaron la acción deseada | Conversiones / Entregado x 100 |
| Tasa de cancelación de suscripción | Porcentaje de destinatarios que cancelaron la suscripción después de recibir el mensaje | Cancelaciones de la suscripción/Entregas x 100 |
| Tasa de devoluciones | Porcentaje de mensajes que no se han podido entregar | Devoluciones / Enviados x 100 |
| Ingresos por correo electrónico enviado | Ingresos atribuidos a la campaña divididos por los mensajes enviados | Ingresos totales / Enviados |

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón.

- **[!DNL Adobe Journey Optimizer] (AJO)**: creación de mensajes, configuración de canal, ejecución de campañas, orquestación de recorrido, experimentación de contenido, reglas de frecuencia y generación de informes
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)**: evaluación de audiencias, cumplimiento de consentimiento y gobernanza
- **[!DNL Adobe Experience Platform] (AEP)**: almacén de perfiles, servicio de identidad, esquemas, conjuntos de datos, recopilación de datos

## Documentación relacionada

Esta sección proporciona vínculos completos a la documentación de [!DNL Experience League] organizada por temas.

### Campañas

- [Introducción a las campañas](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Campañas activadas por API](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### Recorridos

- [Introducción a los recorridos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Leer recorrido de audiencia](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Crear grupos de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [planes de calentamiento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configuración de superficie de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configuración del canal SMS](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Administrar lista de supresión](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Creación y personalización de mensajes

- [Crear un correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/create-email)
- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Uso de componentes de contenido de Email Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Importación o codificación del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/code-content)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funciones de ayuda](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### Gestión de contenido

- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Envío de pruebas de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [Procesamiento de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)

### Experimentación de contenido

- [Introducción al experimento de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Cálculos estadísticos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### Administración de frecuencia y conflictos

- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Información general sobre reglas comerciales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Introducción a la administración de conflictos y prioridades](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificación de posibles conflictos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [restricción y arbitraje de recorridos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Composición de audiencia](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/audience-composition)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/pql/overview)

### Informes

- [Informe en vivo de la campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### Gobernanza de datos y consentimiento

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Grupo de campos de consentimiento y preferencias](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/field-groups/profile/consents)
- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Modelado de datos e identidad

- [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/composition)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- [Protecciones de ingesta](https://experienceleague.adobe.com/es/docs/experience-platform/ingestion/guardrails)

### Tutoriales e introducción

- [Introducción a Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/get-started)
- [Cree su primera campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Creación de su primer recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/journey)
