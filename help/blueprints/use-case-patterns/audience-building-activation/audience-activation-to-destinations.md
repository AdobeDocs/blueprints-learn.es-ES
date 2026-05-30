---
title: Activación de audiencias en destinos
description: Obtenga información sobre cómo evaluar y publicar segmentos de audiencia en destinos externos para la segmentación o supresión mediante Adobe Real-Time CDP.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: b0b9d937-45d2-48f9-ac4c-3611c6e35f58
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 4%

---

# Activación de audiencias en destinos

En esta guía se describe el patrón de casos de uso de activación de audiencias a destinos, que evalúa los segmentos de audiencia en Adobe [!DNL Real-Time Customer Data Platform] (RT-CDP) y los publica en plataformas de publicidad, almacenamiento en la nube, sistemas CRM o socios de datos para el direccionamiento, la supresión, el modelado de similitud o el enriquecimiento de Analytics. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

Este patrón cubre el ciclo de vida completo de la activación de audiencias, desde la definición y evaluación de segmentos de audiencia hasta la configuración de conexiones de destino y audiencias de publicación, pasando por la monitorización del estado de activación y la aplicación del cumplimiento de la gobernanza.

## Patrón de caso de uso

**Audience Activation a destinos**: evalúe y publique un segmento de audiencia en destinos externos para fines de segmentación o supresión.

**Plan de ejecución:** Evaluación de audiencia > Configuración de destino > Audience Activation > Supervisión

## Resumen del caso de uso

Las organizaciones necesitan proporcionar datos de audiencia a sistemas externos para impulsar campañas de medios de pago, enriquecer registros CRM, compartir datos con socios o alimentar análisis descendentes. Audience Activation to Destinations es el patrón de activación fundamental en RT-CDP: evalúa qué perfiles cumplen los requisitos para una audiencia de destinatario, se conecta a uno o más destinos externos, asigna atributos de perfil a campos específicos de destino y publica la audiencia para consumo descendente.

Este patrón se aplica siempre que el objetivo sea obtener datos de audiencia de un sistema externo en el formato correcto y en el momento adecuado. No implica la entrega de mensajes, personalización en el sitio ni análisis. Es el punto de partida más común para implementaciones de RT-CDP y sirve como bloque de creación que otros patrones componen por encima de.

Entre las partes interesadas habituales se incluyen equipos de marketing digital que administran medios de pago, equipos de datos que enriquecen los almacenes, equipos CRM que preparan listas de contactos para campañas y equipos de privacidad que garantizan el cumplimiento de la gobernanza en los flujos de datos salientes.

>[!NOTE]
>Si su organización utiliza [!DNL Real-Time CDP] B2B edition y activa para destinos basados en cuentas, consulte [Activación de audiencia B2B](../b2b/account-audience-activation.md). Ese patrón comparte la misma mecánica de activación, pero utiliza una cuenta B2B y un modelo de datos de persona y requiere la licencia de B2B edition.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Adquisición de nuevos clientes

Amplíe la base de clientes con campañas de adquisición dirigidas, audiencias similares y optimización de medios de pago.

**KPI:** nuevos clientes, coste de adquisición del cliente, conversión de cliente potencial/posible cliente

[Más información sobre la adquisición de nuevos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Reducción del coste de adquisición del cliente

Mejore la eficacia de la segmentación, elimine a los clientes existentes de las campañas de adquisición y optimice el gasto en medios.

**KPI:** coste de adquisición del cliente, coste por posible cliente, eficiencia

[Obtenga más información sobre cómo reducir el coste de adquisición de clientes](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### Optimización del gasto y el ROI de marketing

Mejore el retorno de la inversión en marketing mediante una mejor segmentación, atribución, supresión de audiencias y asignación de presupuesto.

**KPI:** ahorros en costos, costo de adquisición de clientes, ingresos incrementales

[Más información sobre la optimización de los gastos de marketing y el ROI](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## Casos de uso tácticos de ejemplo

- **Segmentación de audiencia de plataforma de publicidad**: inserte segmentos calificados en plataformas de medios de pago para la segmentación de campañas
- **Supresión de medios de pago de clientes existentes**: excluye a clientes conocidos de las campañas de adquisición en plataformas de publicidad para eliminar el gasto desperdiciado
- **Audiencias semilla de similitud**: Envíe segmentos de clientes de alto valor a Facebook, Google Ads o The Trade Desk como audiencias semilla para la expansión de similitudes
- **Sincronización de CRM para la habilitación de ventas**: active audiencias de alta intención o de alto valor para que los equipos de ventas puedan priorizar el alcance
- **Uso compartido de audiencias de socios de datos**: comparta segmentos de audiencia calificados con socios de datos para la medición o la segmentación en cooperación
- **Exportación del almacenamiento en la nube para el enriquecimiento del almacén de datos**: exporte la pertenencia a audiencias y los atributos de perfil a Amazon S3, Azure Blob, Google Cloud Storage o SFTP para análisis descendentes.
- **Activación de audiencia de redireccionamiento**: active a los visitantes del sitio que no se convirtieron a plataformas de redireccionamiento
- **Sincronización de listas de contactos con proveedores de servicios de correo electrónico**: inserta la pertenencia a audiencias en plataformas de correo electrónico de terceros para una difusión coordinada.

## Indicadores clave de rendimiento

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Coste de adquisición de clientes (CAC) | Coste para adquirir un nuevo cliente mediante audiencias activadas | Gasto total en medios/nuevos clientes atribuido a audiencias activadas |
| Tasa de coincidencia de audiencia | Porcentaje de perfiles activados que coinciden correctamente en el destino | Perfiles coincidentes en el destino / perfiles exportados de RT-CDP |
| Ahorros por supresión | Se ha evitado el gasto en medios al eliminar los clientes existentes de las campañas de adquisición | Tamaño estimado de audiencia suprimido de CPM x |
| Tasa de entrega de activación | Porcentaje de perfiles entregados correctamente al destino | Perfiles entregados/perfiles en la audiencia de origen |
| Tiempo hasta la activación | Tiempo transcurrido desde la definición de la audiencia hasta el primer envío en el destino | Medición desde la creación del segmento hasta la primera ejecución del flujo de datos confirmada |
| Precisión de población de audiencia | Alineación entre los tamaños de audiencia esperados y reales en el destino | Recuento de público de destino/recuento de público RT-CDP |

## Aplicaciones

- **Adobe [!DNL Real-Time Customer Data Platform] (RT-CDP)**: evaluación de audiencias, administración de destinos, activación de audiencias, consentimiento y aplicación de gobernanza
- **Adobe [!DNL Experience Platform] (AEP)**: almacén de perfiles, servicio de identidad, motor de segmentación, control de datos

## Arquitectura

La siguiente arquitectura de referencia ilustra cómo los datos de audiencia y perfil fluyen desde Real-Time CDP a destinos empresariales, incluido el almacenamiento en la nube, los extremos de streaming y las aplicaciones SaaS.

![Arquitectura de referencia para la activación de perfiles y audiencias en destinos empresariales](/help/blueprints/audience-activation/assets/known_activation.png)

## Documentación relacionada

**Destinos**

- [Información general sobre los destinos](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/overview)
- [Activar audiencias en destinos de flujo continuo](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Activar audiencias para destinos de exportación de perfiles por lotes](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Activar audiencias bajo demanda en destinos por lotes](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [Protecciones de destinos](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/guardrails)
- [Información general de Destination SDK](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/destination-sdk/overview)

**Audiencias y segmentación**

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/pql/overview)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Resumen de composición de audiencia](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/audience-composition)
- [Protecciones de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)

**Identidad y perfil**

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Reglas de vinculación de gráficos de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/identity-linking-logic)
- [Resumen del perfil](https://experienceleague.adobe.com/es/docs/experience-platform/profile/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview)

**Esquemas y modelado de datos**

- [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/composition)

**Gobernanza de datos**

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Políticas de gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/policies/overview)
- [Aplicación de políticas](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/enforcement/overview)
- [Consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**Control y observabilidad**

- [Monitorización de flujos de datos para destinos](https://experienceleague.adobe.com/es/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Resumen de alertas](https://experienceleague.adobe.com/es/docs/experience-platform/observability/alerts/overview)
- [Resumen de Observability Insights](https://experienceleague.adobe.com/es/docs/experience-platform/observability/home)
- [Panel de control de uso de licencias](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**Atributos calculados**

- [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview)
- [Guía de IU de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/ui)

**Recopilación de datos y orígenes**

- [Información general de orígenes](https://experienceleague.adobe.com/es/docs/experience-platform/sources/home)
- [Información general de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure)

**Administración**

- [Información general de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home)
- [Información general de control de acceso](https://experienceleague.adobe.com/es/docs/experience-platform/access-control/home)
- [Control de acceso basado en atributos](https://experienceleague.adobe.com/es/docs/experience-platform/access-control/abac/overview)

**Protecciones**

- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- [Protecciones del servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/guardrails)
- [Protecciones de activación](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/guardrails)
- [Protecciones de ingesta](https://experienceleague.adobe.com/es/docs/experience-platform/ingestion/guardrails)
