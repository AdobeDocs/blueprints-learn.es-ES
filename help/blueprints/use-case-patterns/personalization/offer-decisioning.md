---
title: Offer Decisioning
description: Aprenda a utilizar la lógica de decisión centralizada para seleccionar la mejor oferta o el contenido más próximo para un perfil en todos los canales.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 8fd511b3-0200-41bf-aff1-e3f2a00a578e
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 5%

---

# Offer Decisioning

En esta guía se describe el patrón de caso de uso de Offer Decisioning, que utiliza [!DNL Adobe Journey Optimizer] (AJO) Decisioning y [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP) para implementar una lógica de selección de ofertas centralizada que determina la mejor oferta de próxima generación para cada perfil de cliente en todos los canales. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

El patrón desvincula la decisión &quot;qué mostrar&quot; de la lógica del canal &quot;dónde mostrarlo&quot;, lo que permite una selección de ofertas coherente y optimizada en el correo electrónico, la web, la aplicación móvil y cualquier otro punto de contacto. AJO Decisioning administra todo el ciclo de vida de la oferta: creación de ofertas y administración del catálogo, reglas de elegibilidad (que pueden ver cada oferta), estrategias de clasificación (cómo seleccionar entre ofertas aptas), ubicaciones (donde aparecen las ofertas) y políticas de decisión (que unen todo).

## Patrón de caso de uso

Esta sección describe el plan de ejecución y la definición del patrón para Offer Decisioning.

**Offer Decisioning**

Utilice la lógica de decisión centralizada para seleccionar la mejor oferta o el contenido siguiente para un perfil entre canales.

**Plan de ejecución:** Evaluación de audiencia > Idoneidad de la oferta > Estrategia de clasificación > Ejecución de decisiones > Entrega > Informes

## Resumen del caso de uso

Las organizaciones suelen tener que presentar la oferta, la promoción o el incentivo más relevantes a cada cliente en el momento de la interacción. Tanto si la interacción se produce en una campaña de correo electrónico, en una página de inicio de un sitio web, en una aplicación móvil o en un punto de decisión dentro de un recorrido de varios pasos, el desafío es el mismo: seleccionar la oferta óptima de un catálogo de opciones disponibles en función de quién es el cliente, para qué cumplen los requisitos y qué oferta es la que tiene más probabilidades de impulsar el resultado deseado.

Offer Decisioning soluciona esto centralizando toda la lógica de selección de ofertas en el motor de gestión de decisiones de AJO. En lugar de codificar las asignaciones de ofertas en campañas o canales individuales, el motor de decisión evalúa los atributos de cada perfil, la pertenencia a audiencias y las señales contextuales para determinar la mejor oferta en tiempo real. Esta centralización garantiza que el mismo cliente reciba ofertas coherentes y optimizadas independientemente del canal al que acceda.

Este patrón difiere del ámbito de la personalización de aplicaciones/web de visitantes conocidos: Offer Decisioning no depende del canal y está centralizado, mientras que la personalización de visitantes conocidos se centra en la personalización de superficies digitales. Difiere de la recomendación de comportamiento en el modelo de catálogo: utilice Offer Decisioning cuando el conjunto de artículos elegibles esté regido por reglas comerciales, restricciones de elegibilidad o requisitos regulatorios (promociones, productos financieros, incentivos). Utilice recomendaciones de comportamiento cuando el conjunto de elementos sea grande, cambie continuamente y la selección esté impulsada por señales de similitud o afinidad de comportamiento (catálogos de productos, bibliotecas de contenido).

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

**[Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo de vida individuales.
**KPI:** participación, tasas de conversión, satisfacción del cliente (CSAT)

**[Aumentar los ingresos de ventas cruzadas y ventas adicionales](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
Promocione productos o servicios complementarios y de primera calidad a los clientes existentes en función del comportamiento y el historial de compras.
**KPI:** % de aumento de ventas/venta cruzada, ingresos incrementales, valor de duración del cliente

**[Aumentar la lealtad del cliente y el valor de duración](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
Profundice las relaciones con los clientes y maximice el valor a largo plazo mediante programas de fidelidad, recompensas y participación personalizada.
**KPI:** valor de duración del cliente, retención, aumento de venta/venta cruzada %

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran cómo se puede aplicar la toma de decisiones de oferta en la práctica.

- La siguiente mejor oferta en campañas de correo electrónico: seleccione la promoción más relevante por destinatario en el momento de la entrega
- Titular promocional en tiempo real en el sitio web: al tomar decisiones, se selecciona la oferta al cargar la página en función del perfil del visitante
- Tarjeta personalizada en la aplicación con el mejor incentivo para la fase de ciclo vital del usuario
- Coherencia de ofertas en canales múltiples: la misma lógica de toma de decisiones sirve para el correo electrónico, la web y la notificación push para que el cliente vea una experiencia de oferta unificada
- Selección dinámica de cupones o descuentos basada en el nivel de valor del cliente (por ejemplo, los clientes de alto valor reciben una oferta premium)
- Selección de ofertas de ampliación o actualización de productos según el nivel de suscripción actual
- Personalización de ofertas de recompensas de fidelización en función del nivel y el historial de actividades

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir la eficacia de una implementación de Offer Decisioning.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de aceptación de ofertas | Porcentaje de ofertas enviadas que resultan en un clic, canje o conversión | Clics o reembolsos de ofertas / Ofertas totales entregadas |
| Distribución de selección de oferta | Proporción de cada oferta seleccionada en todas las decisiones | Recuento por oferta/Decisiones totales procesadas |
| Tasa de reserva | Porcentaje de decisiones en las que no se cualificó ninguna oferta personalizada y se proporcionó la reserva | Impresiones de reserva/Decisiones totales |
| Tasa de conversión | Porcentaje de destinatarios de la oferta que completaron la acción deseada (compra, registro, canje) | Conversiones / Impresiones de la oferta |
| Ingresos incrementales | Ingresos atribuibles a ofertas seleccionadas para la toma de decisiones en comparación con un grupo de control o reserva | Ingresos de ofertas personalizadas: ingresos de reserva/control |
| Puntuación de coherencia entre canales | Porcentaje de perfiles que reciben la misma oferta en varios canales dentro de una ventana definida | Ofertas coherentes/Impresiones multicanal totales |
| Tasa de clics en ofertas | Porcentaje de impresiones de oferta que resultan en un clic | Clics de ofertas / Impresiones de ofertas |

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones de Adobe.

- **[!DNL Adobe Journey Optimizer] (AJO)**: motor de administración de decisiones para la creación de ofertas, reglas de elegibilidad, estrategias de clasificación, ubicaciones y políticas de decisión; configuración de canal y creación de mensajes para la entrega de ofertas; ejecución de campañas y recorridos
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Evaluación de audiencia para segmentos de elegibilidad de ofertas; datos de perfil y atributos calculados utilizados en la elegibilidad y la clasificación
- **[!DNL Adobe Experience Platform] (AEP)**: almacén de perfiles unificado, resolución de identidades y base de datos compatible con AJO y RT-CDP

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre los componentes utilizados en este patrón de caso de uso.

### Gestión de decisiones

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear calificadores de colección](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Entrega de ofertas

- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Entrega de ofertas mediante la API de Edge Decisioning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Entrega de ofertas mediante la API de decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/decisioning-api)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configuración de superficie de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Configuración del canal SMS](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### Creación y personalización de mensajes

- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Campañas y recorridos

- [Introducción a las campañas](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introducción a los recorridos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/journey)

### Experimentación de contenido

- [Introducción al experimento de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)

### Perfil e identidad

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview)
- [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview)
- [Información general sobre Customer AI](https://experienceleague.adobe.com/es/docs/experience-platform/intelligent-services/customer-ai/overview)

### Modelado y recopilación de datos

- [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home)
- [Información general de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure)

### Informes y análisis

- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Información general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/home)

### Gobernanza de datos y ciclo vital

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Información general sobre Advanced Data Lifecycle Management](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/home)
- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)

### Tutoriales

- [Introducción a la API de Gestión de decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/getting-started)
