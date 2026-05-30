---
title: Personalization de aplicación/web de visitante conocido
description: Aprenda a ofrecer contenido, ofertas o promociones personalizadas a visitantes identificados en función del perfil en tiempo real y la pertenencia a segmentos.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 585adc0e-f528-4a09-b931-ef6b45fa8ec8
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1819'
ht-degree: 4%

---

# Personalización web/aplicación de visitante conocido

En esta guía se describe el patrón de caso de uso de personalización de aplicaciones/web de visitante conocido, que usa [!DNL Adobe Journey Optimizer] (AJO) y [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP) para entregar contenido personalizado a visitantes identificados en superficies digitales. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

La personalización de aplicaciones/web de visitante conocido es el patrón de personalización principal para experiencias digitales autenticadas. A diferencia de la personalización de visitantes anónimos, que se basa únicamente en señales de comportamiento en la sesión, este patrón aprovecha el perfil unificado completo: datos de comportamiento históricos, pertenencia a segmentos, nivel de lealtad, historial de compras, fase del ciclo vital, atributos calculados y puntuaciones de tendencia. Admite la personalización en varias páginas web (a través del canal web de AJO), mensajes móviles en la aplicación y tarjetas de contenido.

## Patrón de caso de uso

Esta sección describe el patrón principal y su plan de ejecución.

**Personalización web/aplicación de visitante conocido**

Ofrezca contenido, ofertas o promociones personalizados a un visitante identificado en función de la pertenencia a perfiles y segmentos en tiempo real en la web, aplicaciones móviles y superficies de tarjetas de contenido.

**Plan de ejecución:** Evaluación de audiencia > Personalization Decisioning > Configuración de superficie/canal > Entrega de contenido > Seguimiento de impresiones > Informes

## Resumen del caso de uso

Las organizaciones con propiedades digitales autenticadas (sitios de comercio electrónico, portales bancarios, servicios de suscripción, programas de fidelidad y aplicaciones móviles) deben ofrecer experiencias personalizadas que reflejen la relación de cada cliente con la marca. Cuando un visitante inicia sesión o se reconoce mediante la resolución de identidades, la plataforma puede acceder a su perfil unificado completo y ofrecer contenido adaptado a sus atributos, comportamientos y preferencias específicos.

Este patrón aborda el escenario en el que un visitante identificado llega a una propiedad web o abre una aplicación móvil, y el sistema debe determinar el contenido, la oferta o la promoción óptimos para mostrar en función de los datos de perfil en tiempo real y la pertenencia a audiencias. La decisión de personalización se produce en el extremo en milisegundos, lo que permite la entrega de contenido por subsegundo sin latencia perceptible.

El patrón admite la personalización determinística (donde el contenido específico se asigna a segmentos de audiencia específicos) y la toma de decisiones dinámica (donde AJO Decisioning evalúa las reglas de elegibilidad y las estrategias de clasificación para seleccionar el contenido óptimo por perfil). Abarca varias superficies digitales (páginas web, mensajes móviles en la aplicación y tarjetas de contenido) y permite una personalización coherente en todo el recorrido digital del cliente.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Ofrezca experiencias de cliente personalizadas

Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo de vida individuales. Para obtener más información, consulte [Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md).

**KPI:** participación, tasas de conversión, satisfacción del cliente (CSAT)

### Aumentar la participación en el sitio web

Mejore el tiempo en el sitio, las páginas por sesión y la interacción con el contenido web mediante experiencias relevantes. Para obtener más información, consulte [Aumentar la participación en el sitio web](../../business-objectives/acquisition-growth/increase-website-engagement.md).

**KPI:** tiempo en la página (web), participación, tasas de conversión

### Aumentar la participación en aplicaciones móviles

Impulse el uso activo diario, la adopción de funciones y las conversiones en la aplicación a través de experiencias personalizadas en la aplicación.

**KPI:** participación, retención, tasas de conversión

## Casos de uso tácticos de ejemplo

Las siguientes son implementaciones tácticas comunes de este patrón:

- Personalización de la página principal como héroe por nivel de lealtad o etapa del ciclo vital: muestre diferentes titulares a pantalla completa en función de si el cliente es nuevo, está activo, está en riesgo o es VIP
- Carrusel de recomendaciones de productos basado en el historial de compras: muestre sugerencias de productos relevantes utilizando datos de compras anteriores y puntuaciones de afinidad de productos
- Titular promocional personalizado por segmento de cliente: muestra diferentes promociones para segmentos de clientes nuevos, de alto valor y en riesgo.
- Mensaje en la aplicación para usuarios móviles basado en la adopción de funciones: guíe a los usuarios a funciones infrautilizadas según sus patrones de uso
- Tarjeta de contenido con oferta personalizada en el panel de cuentas: ofertas persistentes y descartables adaptadas al perfil del cliente
- Visualización personalizada de precios o descuentos según el nivel del cliente: mostrar precios específicos del nivel o descuentos exclusivos a los miembros del programa de fidelidad.
- Widget de recomendaciones de venta cruzada basado en productos propios: sugerir productos o servicios complementarios basados en la cartera actual
- Navegación personalizada u orden de contenido basado en intereses: vuelva a ordenar los módulos de contenido o los elementos de navegación según las preferencias demostradas.

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir la eficacia de este patrón de caso de uso.

| KPI | Método de medición | Guía de referencia |
| --- | --- | --- |
| Tasa de participación de Personalization | Clics e interacciones con elementos de contenido personalizados divididos por impresiones | El contenido personalizado debe superar el contenido predeterminado en un 20-50 % |
| Alza de tasa de conversión | Tasa de conversión para experiencias personalizadas en comparación con experiencias de control/predeterminadas | Opte a un alza del 10 al 30 % con respecto a las experiencias no personalizadas |
| Tasa de clics (CTR) | Clics en CTA, ofertas y recomendaciones personalizadas divididas por impresiones | Monitor por superficie (web, en la aplicación, tarjeta de contenido) y por segmento |
| Ingresos por visita | Ingresos atribuidos a sesiones con experiencias personalizadas | Comparación de cohortes de visitantes personalizadas y no personalizadas |
| Tasa de interacción de tarjeta de contenido | Clics y descartes en la tarjeta de contenido en relación con impresiones | Seguimiento por tipo de tarjeta y segmento de audiencia |
| Participación en mensajes en la aplicación | Interacciones de mensajes en la aplicación (clics de CTA, rechazos) relativas a impresiones | Comparar entre segmentos de audiencia y tipos de mensajes |
| Tiempo en la página | Tiempo promedio empleado en páginas con contenido personalizado en comparación con el valor predeterminado | Las páginas personalizadas deben mostrar un mayor tiempo de permanencia |
| Tasa de aceptación de ofertas | Porcentaje de ofertas seleccionadas para la toma de decisiones que resultan en un evento de conversión | Seguimiento de cada oferta, ubicación y estrategia de clasificación |

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Adobe Journey Optimizer](AJO)**: configuración del canal web, configuración del canal en la aplicación, configuración del canal de la tarjeta de contenido, toma de decisiones (selección de ofertas y clasificación), creación de mensajes (creación de contenido personalizado), ejecución de campañas, experimentación de contenido y creación de informes
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** — Evaluación de audiencias (Edge, streaming y por lotes), búsqueda de perfiles en tiempo real mediante Edge Network, enriquecimiento de perfiles con atributos calculados y puntuaciones de tendencia
- **[!DNL Adobe Experience Platform](AEP)**: almacén de perfiles, servicio de identidad, Web SDK, Mobile SDK, configuración de secuencia de datos, entrega de red perimetral

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las tecnologías y configuraciones a las que se hace referencia en esta guía.

### Personalización del canal web

- [Introducción al canal web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Creación de experiencias web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Configuración del canal web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)

### Canales de tarjeta de contenido y en la aplicación

- [Información general sobre el canal en la aplicación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [Requisitos previos del canal en la aplicación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [Creación de mensajes en la aplicación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [Canal de tarjeta de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [Configuración de tarjeta de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)
- [Crear tarjetas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/create-content-card)

### Administración de decisiones

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Personalization y contenido

- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funciones de ayuda](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Identidad y perfil

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Reglas de vinculación de gráficos de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Resumen del perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Recopilación de datos y SDK

- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Instalación de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [Información general de Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Información general sobre API de Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### Campañas y experimentación

- [Introducción a las campañas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introducción al experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### Atributos calculados y enriquecimiento

- [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Guía de IU de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Información general sobre Customer AI](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Informes y análisis

- [Informe en vivo de la campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### Gobernanza y privacidad

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Información general sobre Advanced Data Lifecycle Management](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones del servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
