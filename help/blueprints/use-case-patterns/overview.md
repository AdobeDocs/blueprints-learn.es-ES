---
title: Patrones de casos de uso
description: Conozca los patrones de casos de uso para implementar Adobe Experience Platform y aplicaciones con el fin de lograr objetivos comerciales clave.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
doc-type: overview-page
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Patrones de casos de uso

Los patrones de casos de uso definen enfoques de implementación repetibles para Adobe Experience Platform y sus aplicaciones. Cada patrón describe una capacidad específica, la cadena de funciones que la ofrece, las aplicaciones involucradas y los [objetivos clave para la empresa](/help/blueprints/business-objectives/overview.md) que admite.

Utilice las tablas siguientes para encontrar el patrón que coincida con sus necesidades de implementación y, a continuación, siga el vínculo a la referencia de implementación completa que incluye opciones, fases, orientación para la toma de decisiones y documentación de Experience League.

## Creación y activación de audiencias

Los siguientes patrones le ayudan a crear, evaluar y activar segmentos de audiencia en canales y destinos.

| Patrón | Funcionalidad principal | Soluciones principales |
| --- | --- | --- |
| [Audience Activation a destinos](audience-building-activation/audience-activation-to-destinations.md) | Evaluar y publicar segmentos de audiencia en destinos externos para la segmentación o supresión | [!DNL Real-Time CDP] |
| [Audience Collaboration con coincidencia de segmento](audience-building-activation/audience-collaboration-segment-match.md) | Comparta y haga coincidir segmentos de audiencia en entornos limitados u organizaciones mediante Coincidencia de segmentos | [!DNL Real-Time CDP], [!DNL Experience Platform] |
| [Reenvío de eventos](audience-building-activation/event-forwarding.md) | Reenviar datos de eventos en tiempo real recopilados mediante Edge Network a destinos que no sean de Adobe | [!DNL Experience Platform] (Edge Network, reenvío de eventos) |
| [Activación de audiencia B2B](audience-building-activation/b2b-audience-activation.md) | Activar audiencias B2B basadas en cuentas en canales web, de correo electrónico y de publicidad | [!DNL Real-Time CDP] B2B edition |

## Personalización

Los siguientes patrones ofrecen experiencias adaptadas a visitantes conocidos y desconocidos en todas las superficies web y de aplicaciones.

| Patrón | Funcionalidad principal | Soluciones principales |
| --- | --- | --- |
| [Personalization web de visitante anónimo](personalization/anonymous-visitor-web-personalization.md) | Ofrezca contenido personalizado basado en señales de comportamiento en la sesión para visitantes no identificados | [!DNL Journey Optimizer] (canal web), [!DNL Real-Time CDP] |
| [Personalization de aplicación/web de visitante conocido](personalization/known-visitor-web-app-personalization.md) | Ofrezca contenido, ofertas o promociones personalizados a visitantes identificados en función de perfiles en tiempo real y abonos a segmentos | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Offer Decisioning](personalization/offer-decisioning.md) | Utilice la lógica de decisión centralizada para seleccionar la mejor oferta o el contenido siguiente para un perfil entre canales | [!DNL Journey Optimizer] (Toma de decisiones), [!DNL Real-Time CDP] |
| [Recomendación de comportamiento](personalization/behavioral-recommendation.md) | Generar recomendaciones de elementos y contenido mediante estrategias de selección y modelos de clasificación | [!DNL Journey Optimizer] (Toma de decisiones), [!DNL Real-Time CDP] |

## Administración y orquestación de campañas

Los siguientes patrones abarcan la entrega de mensajes programados, activados y de varios pasos a través de los canales.

| Patrón | Funcionalidad principal | Soluciones principales |
| --- | --- | --- |
| [Activación de mensaje saliente por lotes](campaign-management-orchestration/batch-outbound-message-activation.md) | Evalúe una audiencia y envíe un mensaje saliente programado en una sola ejecución por lotes | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Mensajería activada por eventos](campaign-management-orchestration/event-triggered-messaging.md) | Escuche un evento del sistema o de comportamiento en tiempo real y, a continuación, envíe un mensaje contextual al perfil de activación | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Recorrido orquestado de varios pasos](campaign-management-orchestration/multi-step-orchestrated-journey.md) | Guía de un perfil a través de un recorrido ramificado y multitáctil con esperas, condiciones y varias acciones de mensaje | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Recorrido en canales múltiples con toma de decisiones](campaign-management-orchestration/cross-channel-journey-with-decisioning.md) | Orquestación de un recorrido de varios pasos que incorpore la toma de decisiones en tiempo real para seleccionar un canal, contenido u oferta óptimos | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Administración de Recorridos y marketing basado en grupos de compras](campaign-management-orchestration/buying-group-based-marketing.md) | Desarrolle recorridos de nivel de cuenta que califiquen clientes potenciales en grupos de compra para mejorar la eficacia del marketing B2B | [!DNL Journey Optimizer] B2B edition, [!DNL Real-Time CDP] B2B edition |

## Análisis

Los siguientes patrones admiten el análisis del comportamiento y el rendimiento en canales múltiples.

| Patrón | Funcionalidad principal | Soluciones principales |
| --- | --- | --- |
| [Generación de Customer Analytics y Insight](analysis/customer-analytics-insight-generation.md) | Cree espacios de trabajo de análisis en canales múltiples, métricas calculadas y paneles para el análisis de comportamiento y rendimiento | [!DNL Customer Journey Analytics], [!DNL Experience Platform] |
| [Análisis B2B](analysis/b2b-analytics.md) | Incluir información de nivel de cuenta B2B en el análisis de recorrido de clientes en canales múltiples | [!DNL Customer Journey Analytics] B2B edition, [!DNL Real-Time CDP] B2B edition |

## Experiencia de conversación

Los siguientes patrones habilitan interacciones conversacionales seguras para la marca y con tecnología de IA en propiedades digitales.

| Patrón | Funcionalidad principal | Soluciones principales |
| --- | --- | --- |
| [Experiencia de conversación en Brand Concierge](conversational-experience/brand-concierge-conversational-experience.md) | Transforme las propiedades digitales en experiencias conversacionales seguras para la marca y con tecnología de IA que guíen el descubrimiento de clientes | [!DNL Brand Concierge], [!DNL Experience Platform], [!DNL Real-Time CDP] |
