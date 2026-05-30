---
title: Personalization web de visitante anónimo
description: Aprenda a ofrecer contenido web personalizado a visitantes no identificados en función de las señales de comportamiento durante la sesión.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: e2446801-ffce-40e6-bfe9-abec623c9201
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 4%

---

# Personalización web de visitante anónimo

En esta guía se describe el patrón de caso de uso de personalización web de visitante anónimo, que utiliza [!DNL Adobe Journey Optimizer] (AJO), [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP) y [!DNL Adobe Experience Platform] (AEP) para entregar contenido web personalizado a visitantes anónimos (no identificados) en función de las señales de comportamiento en la sesión. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

El patrón funciona con datos limitados, solo lo que se puede observar en la sesión actual y cualquier perfil de Edge anónimo acumulado de visitas anteriores con el mismo dispositivo o cookie. Esto lo convierte en una herramienta adecuada para la personalización de la parte superior de funnel, en la que el visitante no tiene cuenta o no se ha autenticado.

## Patrón de caso de uso

A continuación se describe el patrón principal y el plan de ejecución para este caso de uso.

**Personalization web de visitante anónimo**

Ofrezca contenido personalizado basado en señales de comportamiento en la sesión para visitantes no identificados a través del canal web de AJO.

**Plan de ejecución:** Configuración de superficie web > Evaluación de regla de comportamiento > Entrega de contenido > Seguimiento de impresión > Informes

## Resumen del caso de uso

La Personalization web de visitantes anónimos aborda la necesidad empresarial de ofrecer contenido relevante y personalizado a los visitantes del sitio web que aún no se han identificado: no han iniciado sesión, no tienen identidad conocida y no se pueden resolver en un perfil unificado de cliente. A pesar de esta limitación, se puede lograr una personalización significativa mediante señales de comportamiento en la sesión: páginas vistas, tiempo en el sitio, profundidad de desplazamiento, fuente de referencia, ubicación geográfica, tipo de dispositivo y parámetros de campaña de UTM.

Este patrón utiliza las superficies de canal web de AJO y las experiencias basadas en código para modificar el contenido de la página en tiempo real. La segmentación de Edge es el método de evaluación principal, ya que las decisiones deben tomarse con latencia de subsegundos a medida que el visitante navega por el sitio. [!DNL Web SDK] recopila señales de comportamiento y las envía a [!DNL AEP Edge Network], donde las reglas de audiencia evaluadas por el perímetro determinan qué variante de contenido se va a enviar.

A diferencia de la personalización de aplicaciones/web de visitantes conocidos, que aprovecha el perfil unificado completo y la pertenencia a segmentos, este patrón se limita a los datos observables en la sesión actual y a cualquier perfil Edge anónimo asociado al ECID del visitante ([!DNL Experience Cloud ID]). Esta distinción es crítica para la planificación de la implementación: las señales de comportamiento disponibles para la personalización se limitan a lo que captura [!DNL Web SDK] y a lo que persiste en el almacén de perfiles de Edge entre sesiones a través del ECID basado en cookies.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

**[Aumentar la participación en el sitio web](../../business-objectives/acquisition-growth/increase-website-engagement.md)**

Mejore el tiempo en el sitio, las páginas por sesión y la interacción con el contenido web mediante experiencias relevantes adaptadas a las señales de visitantes anónimos.

| KPI |
| --- |
| Página de tiempo de activación (web) |
| Participación |
| Tasas de conversión |

**[Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo vital individuales, incluso para los visitantes que aún no se han identificado.

| KPI |
| --- |
| Participación |
| Tasas de conversión |
| Satisfacción del cliente (CSAT) |

**[Aumentar las tasas de conversión](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

Mejore el porcentaje de visitantes y clientes potenciales que completan las acciones deseadas, como compras, suscripciones o envíos de formularios, presentando el contenido más relevante en función del contexto de comportamiento.

| KPI |
| --- |
| Tasas de conversión |
| Conversión de cliente potencial |
| Coste por posible cliente |

## Casos de uso tácticos de ejemplo

Los siguientes ejemplos ilustran escenarios específicos en los que se puede aplicar este patrón.

- **Prueba A/B de titular de página de aterrizaje basada en la fuente de referencia**: pruebe diferentes titulares para visitantes que llegan desde Google, medios sociales o tráfico directo para optimizar la participación por canal de adquisición
- **Recomendaciones de afinidad de la categoría basadas en el comportamiento del explorador** — Muestra recomendaciones de productos o contenido basadas en páginas vistas en la sesión actual para aumentar el descubrimiento y la conversión
- **Oferta de intención de salida para visitantes que están a punto de irse**: presenta una oferta promocional o un formulario de captura de posibles clientes cuando las señales de comportamiento indican que el visitante está a punto de abandonar el sitio
- **Banner promocional con destino geográfico**: muestra promociones específicas de la ubicación, contenido de localizadores de tiendas u ofertas regionales basadas en la ubicación geográfica del visitante
- **Optimización del diseño de contenido específico del dispositivo**: adapte el diseño del contenido, los tamaños de las imágenes y la ubicación de CTA en función de si el visitante está en un equipo de escritorio, una tableta o un dispositivo móvil
- **Mensajes de bienvenida de visitantes nuevos y recurrentes**: diferencie la experiencia de los visitantes nuevos de la de los anónimos que regresan mediante la persistencia de ECID en todas las sesiones
- **Recomendaciones de contenido basadas en páginas vistas en la sesión actual**: muestra de forma dinámica artículos, productos o recursos relacionados basados en las páginas que el visitante ya ha visto
- **Banner a pantalla completa dinámico basado en parámetros de campaña de UTM** — Personalice el banner a pantalla completa para que coincida con los mensajes o el elemento creativo de la campaña de referencia

## Indicadores clave de rendimiento

Utilice los siguientes KPI para medir la eficacia de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de impresiones de Personalization | Porcentaje de vistas de página aptas en las que se entregó contenido personalizado | informe AJO campaign: impresiones / vistas totales de página |
| Tasa de clics (CTR) | Porcentaje de impresiones de contenido personalizadas que resultan en un clic | informe AJO campaign: clics/impresiones |
| Alza de participación | Aumento del tiempo en la página, las páginas por sesión o la profundidad de desplazamiento para el contenido personalizado frente al predeterminado | Comparación de CJA Workspace: cohorte personalizada frente a control |
| Tasa de conversión | Porcentaje de visitantes expuestos a contenido personalizado que completan una acción deseada | análisis de CJA funnel: impresión > interacción > conversión |
| Reducción de tasa de devolución | Disminución en las sesiones de una sola página para los visitantes que reciben contenido personalizado | análisis de sesión de CJA: delta de tasa de devolución para personalizado frente a predeterminado |
| Tasa de victorias del experimento | Porcentaje de pruebas A/B que producen un ganador estadísticamente significativo | Informe de experimento de AJO: experimentos que alcanzan el umbral de confianza |

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Adobe Journey Optimizer] (AJO)**: configuración de superficie de canal web, creación de contenido (experiencias web y basadas en código), ejecución de campañas, experimentación de contenido (pruebas A/B), toma de decisiones (selección dinámica de contenido) y sistema de informes.
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Segmentación de Edge para la evaluación de audiencias en tiempo real basada en señales de comportamiento en la sesión; administración anónima de perfiles de Edge
- **[!DNL Adobe Experience Platform] (AEP)** — [!DNL Web SDK] para la recopilación de señales de comportamiento, [!DNL Edge Network] para el enrutamiento de datos en tiempo real y la entrega de personalización, configuración de secuencia de datos

## Arquitectura

La siguiente arquitectura de referencia ilustra cómo se recopilan las señales de visitantes anónimos en el perímetro, se evalúan en relación con las reglas de audiencia y se utilizan para ofrecer contenido personalizado.

![Arquitectura de referencia para la personalización y activación anónima de audiencias](/help/blueprints/audience-activation/assets/anonymous_activation.png)

## Documentación relacionada

Los siguientes recursos de Experience League proporcionan detalles adicionales sobre las funciones utilizadas en este patrón de caso de uso.

**Canal web y experiencias basadas en código**

- [Introducción al canal web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Creación de experiencias web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Canal de experiencia basado en código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [Configuración de experiencias basadas en código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/code-based-configuration)

**Audiencias y segmentación**

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

**Personalization y contenido**

- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

**Experimentación de contenido**

- [Introducción al experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Cálculos estadísticos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

**Administración de decisiones**

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

**Campañas**

- [Introducción a las campañas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

**[!DNL Web SDK]y recopilación de datos**

- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Instalación de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Información general sobre etiquetas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

**Identidad y perfil**

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Resumen del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

**Modelado de datos**

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

**Informes y análisis**

- [Informe en vivo de la campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)

**Gobernanza de datos y privacidad**

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Información general sobre Advanced Data Lifecycle Management](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [Grupo de campos de consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)

**Protecciones**

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones del servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
