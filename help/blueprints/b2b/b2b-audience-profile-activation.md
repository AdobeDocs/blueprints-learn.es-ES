---
title: Activación de audiencia y perfil B2B
description: Ofrezca audiencias basadas en cuentas y en personas con Real-Time Customer Data Platform B2B edition para su activación en todos los canales y destinos.
solution: Real-Time Customer Data Platform
source-git-commit: 7f0b624616480cf563142c08eb0598d1dd55d551
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 5%
---

# Activación de audiencia y perfil B2B

Use **Real-Time Customer Data Platform B2B edition** para reunir datos de cuentas, oportunidades y personas en perfiles B2B unificados y, a continuación, active tanto las audiencias de personas como las de cuentas en destinos como LinkedIn, Marketo Engage y almacenamiento en la nube. En este modelo se describe cómo diseñar esquemas B2B, crear audiencias de varias entidades y exportarlas para su activación en varios canales y destinos, así como para orquestación y análisis en aplicaciones como **Journey Optimizer B2B edition** y **Customer Journey Analytics B2B edition**.

## Casos de uso

- Cree audiencias de personas para la segmentación y personalización en todos los canales en función de los datos B2B, incluidas cuentas, oportunidades y posibles clientes.
- Cree audiencias de varias entidades que combinen atributos de nivel de oportunidad y cuenta con un comportamiento de nivel de persona empleando un enfoque de **segmento de segmentos** (por ejemplo, &quot;Personas que visitaron la página de precios en los últimos tres días y que toman decisiones sobre oportunidades en la fase X para cuentas del sector Y&quot;).
- Active las audiencias de personas y cuentas en destinos de Experience Platform y almacenamiento en la nube, como Marketo Engage, LinkedIn Matched Audiences, Google Customer Match, DV360, The Trade Desk, Amazon Ads, Bombora y Demandbase, para el direccionamiento, la personalización, el alcance de ventas y el análisis.

## Aplicaciones

- Real-Time Customer Data Platform B2B edition
- (Opcional) **Customer Journey Analytics B2B edition**
- (Opcional) **Journey Optimizer B2B edition**

## Patrones de integración

Los patrones de integración B2B habituales para este modelo incluyen:

- **Participación B2B y orígenes CRM → destinos de → B2B de RTCDP**

  La participación B2B y los sistemas CRM como Marketo Engage, Salesforce y Microsoft Dynamics envían posibles clientes/contactos, cuentas y oportunidades a **Real-Time CDP B2B edition** mediante los esquemas B2B estándar. A partir de ahí, las audiencias de personas y cuentas se activan en destinos que incluyen:

  - Marketo Engage
  - Audiencias coincidentes de LinkedIn/LinkedIn
  - Customer Match y DV360 de Google
  - La Oficina de Comercio
  - Amazon Ads
  - Trade Desk CRM, Criteo, Bing y otras plataformas publicitarias
  - Destinos de almacenamiento en la nube como Amazon S3, ADLS y Snowflake para uso descendente

- **Fuentes de intención y evento B2B → audiencias de → B2B → destinos de RTCDP**

  Fuentes de eventos e intención B2B como Bombora Intent, Demandbase Intent, PathFactory y RainFocus transmiten eventos de intención y participación a RTCDP B2B. Estos eventos se asignan a esquemas B2B estándar y se utilizan para crear personas y audiencias de cuenta que se pueden activar en destinos de publicidad y marketing.

Se pueden usar varias fuentes de datos B2B para asignar datos de cuenta, posible cliente, oportunidad y persona a B2B edition de Real-Time Customer Data Platform mediante los **esquemas y relaciones B2B estándar**.

## Arquitectura

<img src="assets/b2b-audience-profile-activation.png" alt="Arquitectura de referencia para el modelo de activación de audiencia y perfil B2B" style="border:1px solid #4a4a4a"  width="100%" />

## Guardas

Consulte las siguientes protecciones y documentación de idoneidad al diseñar audiencias y perfiles B2B:

- [Protecciones para Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [Casos de uso de segmentación para Real-Time CDP B2B edition](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/segmentation/b2b)
- [Protecciones de perfil y segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- [Actualización de criterios de idoneidad de segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/eligibility-criteria-update)

### Compatibilidad con varias instancias y organizaciones IMS

A continuación, se describen los patrones admitidos de asignación de instancias de Experience Platform y Marketo Engage.

#### Marketo como fuente de datos para Experience Platform

- Se admiten varias instancias de Marketo Engage a una instancia de Experience Platform.
- No se admite una instancia de Marketo Engage en varias instancias de Experience Platform.
- Se admite una instancia de Marketo Engage en una instancia de Experience Platform y varias zonas protegidas.

#### Marketo como destino para Experience Platform

- Se admite Experience Platform en muchas instancias de Marketo Engage.
- Se admiten muchas instancias de Experience Platform en una instancia de Marketo Engage.

#### Perfil de Experience Platform y protecciones de segmentación

Consulte el perfil de Experience Platform y las protecciones de segmentación aquí: [Protecciones de perfil y segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails).

Los segmentos que incluyen entidades B2B como cuentas, posibles clientes u oportunidades dependen de las relaciones entre varias entidades y se evalúan en **lote**. Por el contrario, **la segmentación por transmisión** es compatible con audiencias limitadas a personas y eventos que no incorporan entidades B2B. Para escenarios de activación B2B casi en tiempo real, considere la posibilidad de utilizar audiencias B2B evaluadas por lotes como entradas para audiencias de streaming o Edge cuando sea compatible.

#### Experience Platform - Conector de Marketo Engage Source

- Consulte la documentación [aquí](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo).

#### Experience Platform - Conector de destino de Marketo

- Consulte la documentación [aquí](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/adobe/marketo-engage-connection).

#### Guardas de destino

- Consulte la documentación de destino para obtener instrucciones específicas sobre cada destino: [Protecciones de destino](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/guardrails).
- Para destinos de publicidad como Facebook, Google Customer Match y DV360, Microsoft Bing, Trade Desk, Amazon Ads, Bombora, Demandbase y otros, asegúrese de que los identificadores que elija en su esquema y estrategia de identidad (correo electrónico, ID de publicidad móvil, campos de dirección e ID de cuenta) se alineen con las capacidades de asignación y las identidades admitidas para esos destinos.

## Pasos de implementación

Para obtener instrucciones sobre cómo implementar y configurar B2B edition de Real-Time Customer Data Platform, consulte la documentación de Real-Time CDP B2B edition: [B2B edition de Real-Time Customer Data Platform](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview).

Dos patrones de implementación son comunes:

- Ingeste datos y perfiles B2B de Marketo Engage (y su CRM conectado) en RTCDP B2B edition.
- Ingeste datos B2B directamente desde CRM u otros sistemas B2B en RTCDP B2B edition utilizando los conectores de origen correspondientes.

Como parte de las actualizaciones de la arquitectura B2B de RTCDP, algunos patrones utilizados anteriormente ya no se utilizan en las entidades B2B. Para obtener información detallada, consulte la documentación detallada [aquí](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade).

## Consideraciones sobre la implementación

Directrices sobre consideraciones y configuraciones clave del modelo.

- **Integración de CRM con y sin Marketo**

  - Si la implementación utiliza Marketo Engage como fuente y Marketo Engage está conectado a CRM, los datos de CRM sincronizados con Marketo (por ejemplo, posibles clientes/contactos, cuentas, oportunidades) fluirán a RTCDP B2B edition a través del conector de origen de Marketo.
  - Si hay tablas o atributos de CRM adicionales que no pasan a través de Marketo (por ejemplo, objetos personalizados o campos adicionales), conecte el origen de CRM directamente a Experience Platform mediante los conectores de origen de CRM y asigne esas tablas a los esquemas y relaciones B2B estándar.
  - Diseñar conjuntamente la ingesta de CRM + Marketo para evitar representaciones duplicadas o en conflicto de entidades B2B en RTCDP B2B y garantizar que todas las entidades B2B se ajusten a los esquemas estándar.

## Documentación relacionada

- [B2B edition de Real-Time Customer Data Platform](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
- [Introducción a Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial?lang=en)
- [Protecciones para Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [Esquemas en Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/schemas/b2b)
- [Actualizaciones de arquitectura a Real-Time CDP B2B edition](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade)
- [Adobe Experience Platform](https://experienceleague.adobe.com/es/docs/experience-platform)
- [Marketo Engage](https://experienceleague.adobe.com/es/docs/marketo/using/home)
- [Adobe Experience Platform - Conector de Marketo Source](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Adobe Experience Platform - Conector de destino de Marketo](https://experienceleague.adobe.com/es/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list)
- [Guardas de destino](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/guardrails)
