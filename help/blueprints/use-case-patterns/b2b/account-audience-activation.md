---
title: Audience Activation B2B
description: Obtenga información sobre cómo activar audiencias B2B basadas en cuentas en canales web, de correo electrónico y de publicidad.
solution: Real-Time Customer Data Platform
exl-id: 2b979159-37aa-41d4-a6b4-1105538f6546
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 2%

---

# Activación de audiencia B2B

En esta guía se describe el patrón de caso de uso de activación de audiencia B2B, que utiliza [!DNL Adobe Real-Time Customer Data Platform] ([!DNL RT-CDP]) B2B edition para generar, evaluar y activar audiencias de nivel de cuenta en los canales web, de correo electrónico, de publicidad y CRM. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

Este patrón cubre el ciclo de vida completo, desde la unificación del perfil de cuenta hasta la evaluación y activación de audiencias, pasando por destinos específicos de B2B como [!DNL Marketo Engage], [!DNL LinkedIn] y sistemas CRM.

## Patrón de caso de uso

**Activación de audiencia B2B**

Active audiencias B2B basadas en cuentas en los canales web, de correo electrónico y de publicidad.

**Plan de ejecución:** Enriquecimiento del perfil de cuenta > Evaluación de audiencia de cuenta > Configuración de destino > Audience Activation > Supervisión

## Resumen del caso de uso

Los equipos de marketing B2B necesitan segmentar y activar audiencias en el nivel de la cuenta en lugar de en el nivel de persona individual. A diferencia de la activación de audiencia B2C, en la que la unidad de segmentación es un perfil de consumidor único, la activación de audiencia B2B requiere comprender la relación entre las personas y las cuentas a las que pertenecen, evaluar la pertenencia a la audiencia en función de atributos de nivel de cuenta combinados con señales de participación de nivel de persona y enviar esas audiencias a destinos que admitan la segmentación basada en cuentas.

[!DNL RT-CDP] B2B edition amplía el estándar [!DNL Real-Time Customer Data Platform] con clases XDM especializadas para cuentas, oportunidades y campañas, junto con la resolución de identidad B2B que asigna relaciones persona a cuenta. Esto permite a los especialistas en marketing crear audiencias de cuenta que combinen datos firmográficos (industria, ingresos, recuento de empleados), datos tecnográficos (pila de tecnología, uso de productos) y datos de comportamiento (visitas web, participación por correo electrónico, asistencia a eventos) de las personas asociadas con esas cuentas.

Las audiencias de cuentas activadas alimentan los casos de uso en toda la funnel de generación de demanda: campañas de sensibilización de funnel en [!DNL LinkedIn] y publicidad de visualización, programas de nutrición de funnel en [!DNL Marketo Engage] y activación de ventas de funnel de nivel inferior mediante la integración de CRM. Las audiencias de supresión de cuentas evitan el gasto desperdiciado al excluir a los clientes existentes, las cuentas cerradas y perdidas o las cuentas que ya están en ciclos de ventas activos.

>[!NOTE]
>Si su caso de uso implica la activación de audiencias a nivel de persona (B2C) en lugar de a nivel de cuenta, consulte [Activación de audiencias a destinos](../audience-building-activation/audience-activation-to-destinations.md). Ese patrón utiliza el modelo de datos estándar RT-CDP y no requiere B2B edition.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Aumentar la generación de posibles clientes

Genere posibles clientes más cualificados para el canal de ventas a través de formularios, eventos, contenido y participación multicanal.

**KPI:** clientes potenciales, coste por cliente potencial, conversión de cliente potencial

[Más información sobre cómo aumentar la generación de posibles clientes](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### Mejore la calificación y conversión de posibles clientes

Aumente la calidad del posible cliente y acelere la progresión de la canalización mediante la puntuación, la nutrición y el seguimiento personalizado.

**KPI:** conversión de posibles clientes, conversión de posibles clientes/posibles clientes, eficiencia

[Obtenga más información sobre cómo mejorar la calificación y conversión de posibles clientes](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### Adquisición de nuevos clientes

Amplíe la base de clientes con campañas de adquisición dirigidas, audiencias similares y optimización de medios de pago.

**KPI:** nuevos clientes, coste de adquisición del cliente, conversión de cliente potencial/posible cliente

[Más información sobre la adquisición de nuevos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Optimización del gasto y el ROI de marketing

Mejore el retorno de la inversión en marketing mediante una mejor segmentación, atribución, supresión de audiencias y asignación de presupuesto.

**KPI:** ahorros en costos, costo de adquisición de clientes, ingresos incrementales

[Obtenga más información sobre cómo optimizar el gasto y el ROI de marketing](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran cómo se puede aplicar este patrón en la práctica.

- **Publicidad basada en cuentas en[!DNL LinkedIn]**: cuentas de Target que coinciden con su perfil de cliente (ICP) ideal con contenido patrocinado y campañas de InMail en [!DNL LinkedIn], mediante listas de cuentas activadas desde [!DNL RT-CDP] B2B edition
- **[!DNL Marketo Engage]segmentación de programas de Nutrición** — Activar audiencias de cuenta para [!DNL Marketo Engage] para inscribir posibles clientes y contactos asociados en flujos de Nutrición segmentados según criterios de calificación de nivel de cuenta
- **Sincronización de lista de cuentas de CRM**: inserte listas de cuentas calificadas en [!DNL Salesforce] o [!DNL Microsoft Dynamics] para la visibilidad del equipo de ventas, la asignación de territorios y los flujos de trabajo de prospección de salida
- **Supresión de cuentas para medios pagados**: elimine clientes existentes, cuentas ganadas cerradas o cuentas en ciclos de ventas activos de campañas de adquisición pagada para reducir el gasto desperdiciado
- **Segmentación de cuentas basada en intención**: combine señales de intención de terceros con datos de participación de origen a nivel de cuenta para identificar y activar audiencias de cuentas en el mercado
- **Venta cruzada de productos a cuentas existentes**: cree audiencias de cuentas con una línea de productos pero no con otra y, a continuación, actívela en canales de correo electrónico y publicidad para campañas de venta cruzada
- **Segmentación de eventos y seminarios web**: active las audiencias de cuenta en los canales de publicidad y correo electrónico para impulsar el registro de eventos desde las cuentas de destino
- **Campañas de desplazamiento competitivo** — Cuentas de Target que utilizan productos de la competencia con mensajes personalizados activados a través de canales de publicidad y correo electrónico
- **Participación de cuenta por niveles**: Segmente las cuentas en niveles de participación (alta, media, baja) según la actividad agregada a nivel de persona y active campañas diferenciadas para cada nivel
- **Audiencias de marketing conjunto de socios**: comparta segmentos de audiencia de cuenta con socios de canal o programas de marketing conjunto a través de destinos de almacenamiento en la nube

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir el éxito de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Alcance de cuenta | Número de cuentas de destinatario contactadas a través de canales de activación | Seguimiento de cuentas únicas activadas por destino |
| Tasa de participación de cuenta | Porcentaje de cuentas activadas que muestran señales de participación | Medir la participación a nivel de persona agregada a la cuenta |
| Influencia de canalización | Canalización de ingresos atribuida a campañas de activación basadas en cuentas | Rastrear oportunidades creadas a partir de audiencias de cuentas activadas |
| Costo por cuenta comprometida | Gasto en marketing dividido por el número de cuentas que muestran participación | Cálculo entre los costes de canal de correo electrónico y publicidad |
| Tasa de conversión de posibles clientes | Porcentaje de posibles clientes de cuentas activadas que se convierten en oportunidades | Rastrear conversión de posible cliente a oportunidad para audiencias activadas |
| Ahorro de supresión de audiencia | Coste evitado al suprimir cuentas no aptas de campañas pagadas | Mida la reducción de gasto de las audiencias de supresión |
| Cobertura de cuenta | Porcentaje del mercado total accesible (TAM) cubierto por audiencias activadas | Comparar cuentas activadas con el universo ICP total |

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón de caso de uso.

- **[!DNL Real-Time CDP]B2B edition**: plataforma principal para la unificación de perfiles de cuenta, resolución de identidades B2B, evaluación de audiencias de cuenta, configuración de destino específica B2B y activación de audiencias de cuenta
- **[!DNL Adobe Experience Platform](AEP)**: infraestructura básica para el modelado de datos XDM B2B, la ingesta de datos desde CRM y fuentes de automatización de marketing, servicio de identidad y administración
- **[!DNL Marketo Engage]**: destino principal de automatización de marketing B2B para programas de nutrición de posibles clientes, puntuación y ejecución de campañas alimentadas por audiencias de cuenta activadas

## Documentación relacionada

Los siguientes recursos proporcionan contexto adicional e instrucciones detalladas para las capacidades utilizadas en este patrón de caso de uso.

**[!DNL RT-CDP]B2B edition**

- [Información general sobre Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b)
- [Esquemas B2B en Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Audiencias de cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [Descripción del producto de RT-CDP B2B edition](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

**Evaluación y segmentación de audiencias**

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Composición de audiencia](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

**Destinos y activación**

- [Información general sobre los destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Marketo Engage destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [Destino de audiencias coincidentes de LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
- [Destino de Salesforce CRM](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Microsoft Dynamics 365 destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/microsoft-dynamics-365)
- [Amazon S3 destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)
- [Activar audiencias en destinos de flujo continuo](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Activar audiencias en destinos por lotes](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Protecciones de activación](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

**Fuentes de datos y conectores**

- [Información general de orígenes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Conector de Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Conector de Salesforce](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/crm/salesforce)

**Modelado e identidad de datos**

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Resumen del perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

**Gobernanza de datos y privacidad**

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**Monitoreo y observabilidad**

- [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Monitorización de flujos de datos de destino](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Monitorización de flujos de datos de origen](https://experienceleague.adobe.com/en/docs/experience-platform/sources/api-tutorials/monitor)
- [Panel de control de uso de licencias](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**Informes y análisis**

- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Información general sobre Conexiones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Resumen de vistas de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)

**Tutoriales y guías**

- [Introducción a Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro)
- [Creación de un esquema para fuentes B2B](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Herramientas de zona protegida](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/overview)
