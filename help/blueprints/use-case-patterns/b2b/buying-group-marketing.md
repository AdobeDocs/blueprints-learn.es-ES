---
title: Adquisición de gestión de Recorridos y marketing basada en grupos
description: Aprenda a desarrollar recorridos de nivel de cuenta que califiquen clientes potenciales en grupos de compra para mejorar la eficacia del marketing B2B.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 2bf57f67-80c8-4368-98d2-05706427772d
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 1%

---

# Compra de gestión de recorridos y marketing basada en grupos

En esta guía se describe el patrón de casos de uso de administración de recorridos y marketing basado en grupos de compras, que usa [!DNL Adobe Journey Optimizer B2B Edition] y [!DNL Real-Time CDP B2B Edition] para implementar la orquestación de recorridos a nivel de cuenta con la administración de grupos de compras. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

A diferencia de los patrones de recorrido a nivel de persona, este patrón funciona a nivel de cuenta, calificando a los posibles clientes individuales en grupos de compra asociados con intereses de soluciones, puntuando la participación a nivel de grupo de compra y orquestando recorridos de cuenta de varios pasos que llevan las cuentas a través de las fases de canalización hasta la preparación de las ventas.

## Patrón de caso de uso

**Comprar administración de recorridos y marketing basada en grupos**

Desarrolle recorridos de nivel de cuenta que califiquen clientes potenciales en grupos de compra para mejorar la eficacia del marketing B2B.

**Plan de ejecución:** Identificación de cuenta > Definición de grupo de compra > Calificación de posibles clientes > Ejecución de Recorridos de cuenta > Puntuación de participación > Informes

## Resumen del caso de uso

Las organizaciones B2B se enfrentan a un desafío fundamental: las decisiones de compra rara vez las toma una sola persona. Las compras complejas de B2B implican múltiples partes interesadas (responsables de la toma de decisiones, influyentes, defensores, tenedores de presupuesto y evaluadores técnicos) que, colectivamente, forman un &quot;grupo de compra&quot;. El marketing tradicional basado en el posible cliente trata a cada persona de forma independiente, sin tener en cuenta la señal crítica de si la combinación correcta de funciones dentro de una cuenta está comprometida y lista para comprar.

La compra de gestión de recorridos y marketing basada en grupos soluciona este problema cambiando la unidad de orquestación de posibles clientes individuales a cuentas y grupos de compra. El patrón permite a los especialistas en marketing B2B definir los intereses de la solución (los productos o servicios que se venden), crear plantillas de grupo de compra que especifican qué funciones se necesitan para una decisión de compra, calificar los posibles clientes entrantes respecto a esas funciones, puntuar la participación en el nivel de grupo de compra y orquestar recorridos de cuenta que responden a las señales de integridad y preparación del grupo de compra.

El resultado deseado es mejorar la calidad y la velocidad de la canalización: el marketing envía cuentas a las ventas solo cuando se involucra a las personas adecuadas dentro de la cuenta y el grupo de compra es lo suficientemente completo, lo que reduce el esfuerzo de ventas desperdiciado y acelera la progresión del acuerdo.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Mejore la calificación y conversión de posibles clientes

Aumente la calidad del posible cliente y acelere la progresión de la canalización mediante la puntuación, la nutrición y el seguimiento personalizado.

**KPI:** conversión de posibles clientes, conversión de posibles clientes/posibles clientes, eficiencia

[Obtenga más información sobre cómo mejorar la calificación y conversión de posibles clientes](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### Aumentar la generación de posibles clientes

Genere posibles clientes más cualificados para el canal de ventas a través de formularios, eventos, contenido y participación multicanal.

**KPI:** clientes potenciales, coste por cliente potencial, conversión de cliente potencial

[Más información sobre cómo aumentar la generación de posibles clientes](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### Aumentar ingresos y ventas

Impulse el crecimiento de los ingresos de primera línea a través de canales digitales optimizados, campañas y recorridos con los clientes.

**KPI:** crecimiento de ingresos, velocidad de canalización, tasa de cierre de acuerdo

[Más información sobre el aumento de ingresos y ventas](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

## Casos de uso tácticos de ejemplo

Los siguientes son escenarios específicos en los que se puede aplicar este patrón.

- **Calificación del grupo de compra específica de la solución**: defina grupos de compra para cada línea de producto (por ejemplo, &quot;Enterprise CRM&quot;, &quot;Data Platform&quot;, &quot;Security Suite&quot;) con plantillas de roles que especifiquen las personas requeridas (Comprador económico, Evaluador técnico, Campeón, Usuario final) y califique a los posibles clientes del sistema de automatización de marketing y CRM con esas funciones.
- **recorrido de cuenta para la aceleración de canalizaciones**: organice un recorrido de cuenta de varios pasos que envíe correos electrónicos de nutrición dirigidos a roles que no participan suficientemente dentro de un grupo de compras, genere déclencheur de ventas cuando se alcancen los umbrales de participación y pase la cuenta a una fase lista para las ventas.
- **Campañas de integridad de grupos de compra**: identifique las cuentas en las que faltan roles en los grupos de compra (por ejemplo, no se ha identificado ningún comprador económico) e inicie campañas de adquisición dirigidas para atraer a las personas adecuadas dentro de esas cuentas.
- **recorridos de cuentas de venta cruzada**: después de que se cierre un acuerdo inicial, cree nuevos grupos de compras para intereses de soluciones complementarias y organice recorridos de cuentas que nutren al comité de compras ampliado.
- **Reparticipación para ofertas estancadas**: detecta cuentas en las que las puntuaciones de participación del grupo comprador han declinado y déclencheur recorridos de renovación de participación con contenido nuevo, alcance ejecutivo o invitaciones a eventos.
- **Alineación de ventas y marketing mediante perspectivas de CRM**: el estado del grupo de compras superficiales, los datos de participación y el progreso del recorrido de la cuenta directamente dentro de [!DNL Salesforce] o [!DNL Dynamics 365], de modo que los representantes de ventas tengan visibilidad en tiempo real de las cuentas calificadas para marketing.
- **Actualizaciones de grupos de compra impulsadas por eventos**: actualice automáticamente las puntuaciones de participación y pertenencia a grupos de compra cuando los posibles clientes asistan a seminarios web, descarguen documentos técnicos, visiten páginas de precios o soliciten demostraciones.
- **Coordinación de cuentas de varias regiones**: administre grupos de compras en cuentas globales donde los distintos contactos regionales tienen diferentes roles, unificando la puntuación de participación en todas las regiones.

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir la eficacia de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Índice de integridad del grupo de compra | Porcentaje de grupos compradores con todos los roles obligatorios ocupados | [!DNL AJO B2B] paneles de Analytics: rastrear la cobertura de funciones por grupo de compra |
| Puntuación de participación del grupo de compra | Puntuación de participación agregada en todos los miembros de un grupo comprador | Puntuación de participación de [!DNL AJO B2B]: puntuaciones a nivel de persona acumuladas en el grupo de compra |
| Tasa de cuenta calificada de marketing (MQA) | Porcentaje de cuentas que alcanzan el umbral de cualificación de marketing | Criterios de salida del recorrido de cuentas: cuentas en transición a la fase de ventas preparadas |
| Velocidad de canalización | Tiempo promedio desde la creación del grupo de compra hasta la oportunidad calificada para ventas | Integración de CRM: rastrear transiciones de fase de [!DNL AJO B2B] a la canalización de CRM |
| Tasa de calificación del grupo de clientes potenciales a compradores | Porcentaje de posibles clientes cualificados correctamente para comprar roles de grupo | [!DNL AJO B2B] Administración de grupos de compra: relación de clientes potenciales cualificados frente a no cualificados |
| Tasa de respuesta de alertas de ventas | Porcentaje de alertas de ventas que resultan en una actividad de seguimiento de ventas | Perspectivas de ventas de CRM: rastrear la conversión de alerta a actividad |
| Tasa de finalización de Recorridos de cuenta | Porcentaje de cuentas que completan la ruta de recorrido deseada | [!DNL AJO B2B] paneles de Analytics: métricas de finalización de recorridos |
| Tasa de participación en el correo electrónico (B2B) | Tasas de apertura y clics para correos electrónicos de B2B nutre | Informes de [!DNL AJO B2B]: envío de correo electrónico y métricas de participación |

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones de Adobe.

- **[!DNL Journey Optimizer B2B Edition]([!DNL AJO B2B])**: Orquesta recorridos de nivel de cuenta, administra grupos de compras con plantillas de roles e intereses de soluciones, puntúa la participación a nivel de persona y grupo de compras, crea contenido de correo electrónico B2B, envía mensajes SMS, configura alertas de ventas y proporciona paneles de análisis B2B.
- **[!DNL Real-Time CDP B2B Edition]([!DNL RT-CDP B2B])**: unifica perfiles de cuenta a partir de datos B2B de origen cruzado, resuelve relaciones persona a cuenta, evalúa audiencias a nivel de cuenta, configura destinos específicos B2B ([!DNL Marketo Engage], [!DNL LinkedIn], CRM) y aplica el control de datos en los datos B2B.

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las aplicaciones y capacidades a las que se hace referencia en esta guía.

### [!DNL AJO B2B Edition]

- [Inicio de la documentación de AJO B2B edition](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [Resumen de grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [Intereses de solución](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [Plantillas de roles](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [Creación de grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)
- [Fases del grupo de compras](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Resumen de recorridos de cuenta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [Nodos del recorrido de cuentas](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [Correos electrónicos de alerta de ventas](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sales-alert-email)
- [Perspectivas de ventas de CRM](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/crm-sales-insights)

### Correo electrónico y contenido B2B

- [Creación de correo electrónico B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/email-authoring)
- [Creación de SMS en AJO B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sms-authoring)
- [Asistente de IA para la creación de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/ai-assistant-emails)

### Análisis y paneles B2B

- [Panel de grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/buying-groups-dashboard)
- [Tablero de participación](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/engagement-dashboard)
- [Panel inteligente](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/intelligent-dashboard)
- [Información general sobre CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### [!DNL RT-CDP B2B Edition]

- [Información general sobre RT-CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)
- [Esquemas B2B en Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Audiencias de cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [Conector de origen de Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)

### Base de datos

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general de orígenes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### Gobernanza de datos y privacidad

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

### Destinos

- [Información general sobre los destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Destino de audiencias coincidentes de LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)

### Guardas

- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [Protecciones de ingesta](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)

### Tutoriales y introducción

- [Introducción a AJO B2B edition](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [Tutorial de B2B edition de RT-CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-tutorial)
