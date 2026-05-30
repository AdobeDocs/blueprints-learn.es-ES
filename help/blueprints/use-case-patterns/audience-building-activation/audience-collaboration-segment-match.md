---
title: Audience Collaboration
description: Aprenda a compartir y hacer coincidir segmentos de audiencia en entornos limitados u organizaciones mediante Coincidencia de segmentos.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: 7014849c-5e32-4ec3-a531-c0e8ce896f44
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 3%

---

# Audience Collaboration

Esta guía describe el patrón de casos de uso de colaboración de audiencias, que usa [!DNL Segment Match] en [!DNL Real-Time CDP] y [!DNL Adobe Experience Platform] para compartir y hacer coincidir segmentos de audiencia en entornos limitados u organizaciones de una manera segura para la privacidad. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender qué hace este patrón, los objetivos comerciales que admite, los casos de uso tácticos que habilita y las aplicaciones de Adobe implicadas.

[!DNL Segment Match] permite que dos o más organizaciones de [!DNL Experience Platform] (o zonas protegidas dentro de una organización) colaboren en los datos de audiencia compartiendo información de pertenencia a segmentos sin exponer la PII subyacente. Los participantes pueden estimar la superposición, compartir audiencias y activar perfiles coincidentes en destinos descendentes.

## Patrón de caso de uso

Este caso de uso sigue el patrón de Audience Collaboration.

Comparta y combine segmentos de audiencia en zonas protegidas u organizaciones mediante [!DNL Segment Match].

**Plan de ejecución:** Selección de segmentos > Configuración de coincidencias > Estimación de superposición > Uso compartido de audiencias > Activación

## Resumen del caso de uso

Las organizaciones necesitan cada vez más colaborar en los datos de audiencia con socios, filiales o entre unidades de negocio, al tiempo que mantienen estrictos controles de privacidad. La colaboración entre audiencias resuelve esta necesidad habilitando el uso compartido seguro de segmentos a través de [!DNL Segment Match], una característica de [!DNL Real-Time CDP] que permite a dos o más organizaciones de [!DNL Experience Platform] (o zonas protegidas) intercambiar información de pertenencia a audiencias mediante identificadores hash seguros para la privacidad.

El escenario empresarial suele incluir una organización (el remitente) que ha creado un segmento de audiencia valioso y desea compartirlo con una organización asociada (el receptor) para la segmentación, supresión o enriquecimiento conjuntos. Antes de compartir, ambas partes pueden estimar la superposición de audiencias para evaluar el valor. Una vez compartida, la organización receptora puede activar la audiencia coincidente a través de sus propios destinos.

Este patrón es distinto de la activación de audiencia estándar porque funciona entre organizaciones o zonas protegidas en lugar de con destinos de marketing o publicidad externos. También es distinto de las salas limpias de datos o las plataformas de colaboración de terceros, ya que funciona de forma nativa dentro del ecosistema de Adobe mediante la infraestructura de identidad [!DNL Experience Platform].

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Adquisición de nuevos clientes

Amplíe la base de clientes con campañas de adquisición dirigidas, audiencias similares y optimización de medios de pago. La colaboración de audiencias permite a las organizaciones descubrir nuevos grupos de clientes potenciales comparando sus segmentos con las audiencias de los socios, identificando superposiciones de alto valor y llegando a clientes nuevos mediante la activación conjunta.

- **KPI:** nuevos clientes, coste de adquisición del cliente, conversión de cliente potencial/posible cliente
- [Adquisición de nuevos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Reducción del coste de adquisición del cliente

Mejore la eficacia de la segmentación, elimine a los clientes existentes de las campañas de adquisición y optimice el gasto en medios. Al compartir segmentos de supresión entre organizaciones o unidades de negocio, los equipos pueden evitar el gasto desperdiciado en clientes ya convertidos y centrar los presupuestos en perspectivas realmente nuevas.

- **KPI:** coste de adquisición del cliente, coste por posible cliente, eficiencia
- [Reducción del coste de adquisición del cliente](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### Optimización del gasto y el ROI de marketing

Mejore el retorno de la inversión en marketing mediante una mejor segmentación, atribución, supresión de audiencias y asignación de presupuesto. [!DNL Segment Match] habilita la supresión de audiencias entre organizaciones y la segmentación conjunta que reduce la duplicación y mejora la precisión.

- **KPI:** ahorros en costos, costo de adquisición de clientes, ingresos incrementales
- [Optimización del gasto y el ROI de marketing](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## Casos de uso tácticos de ejemplo

- **Coincidencia de audiencia de publicador-anunciante**: una marca comparte su segmento de cliente de alto valor con un publicador de medios para estimar la superposición y dirigirse a los usuarios coincidentes con anuncios personalizados, lo que mejora la relevancia de la campaña sin exponer la PII.
- **Supresión entre marcas dentro de una compañía matriz**: varias marcas bajo una organización principal comparten segmentos de clientes para suprimir a los clientes existentes de marcas hermanas de las campañas de adquisición, lo que reduce el gasto desperdiciado en publicidad.
- **Enriquecimiento de la audiencia de la red de medios comerciales**: Un retailer comparte segmentos basados en compras con socios de marcas CPG, lo que permite que las marcas se dirijan a compradores probados en la red de medios de retailer con tasas de conversión más altas.
- **Descubrimiento de audiencias de socios de marketing conjunto**: dos marcas que no compiten evalúan la superposición de audiencias para evaluar el potencial de asociación antes de lanzar una campaña conjunta, utilizando una estimación de superposición para validar la alineación de audiencia.
- **Uso compartido de segmentos de la cooperativa de datos**: las organizaciones en una cooperativa de datos comparten segmentos de audiencia con hash para expandir el alcance de segmentación mientras mantienen el cumplimiento de la privacidad y los controles de gobernanza de datos.
- **Federación de audiencias de zonas protegidas múltiples**: una empresa global comparte segmentos de audiencia en zonas protegidas regionales para permitir una segmentación de clientes coherente en todos los mercados, respetando al mismo tiempo los requisitos de residencia de datos regionales.
- **Activación de socios cruzados del programa de fidelización**: una coalición de fidelidad comparte segmentos de nivel de fidelidad con comerciantes participantes para que cada socio pueda ofrecer promociones apropiadas para el nivel a la base de clientes compartidos.
- **Colaboración de medición y atribución**: Un anunciante comparte un segmento de conversión con un socio de medios para que pueda medir la eficacia de la campaña comparando usuarios expuestos con convertidores.

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir el éxito de las implementaciones de colaboración de audiencia.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de superposición de audiencia | Porcentaje de perfiles en el segmento compartido que coinciden entre remitente y destinatario | [!DNL Segment Match] informe de estimación de superposición |
| Tamaño de audiencia coincidente | Número de perfiles coincidentes correctamente y disponibles para la activación | [!DNL Segment Match] estado de uso compartido y recuento de población de audiencia |
| Nueva adquisición de cliente de audiencias coincidentes | Nuevos clientes netos adquiridos mediante campañas dirigidas a segmentos coincidentes | Seguimiento de conversión en campañas que utilizan audiencias coincidentes |
| Reducción de costes de adquisición de clientes | Disminución del coste por adquisición al usar audiencias coincidentes frente a una segmentación amplia | Análisis de costes de Campaign comparando el rendimiento de audiencia coincidente con el incomparable |
| Ahorros por supresión | Gasto en medios ahorrado al eliminar clientes conocidos de las campañas de adquisición | Comparación del gasto en medios antes y después de la supresión |
| Alza de rendimiento de Campaign | Mejora en la tasa de conversión, la tasa de pulsaciones o la participación para campañas que utilizan audiencias coincidentes | Prueba A/B que compara campañas de audiencia coincidentes con control |
| Tiempo para Collaboration | Tiempo transcurrido desde el inicio del uso compartido de segmentos hasta la preparación para la activación | [!DNL Segment Match] marcas de tiempo de flujo |

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Real-Time CDP]**: proporciona la capacidad [!DNL Segment Match] para el uso compartido de audiencias con seguridad de privacidad, la evaluación de audiencias para la creación de segmentos y la activación de destino para el uso posterior de audiencias coincidentes.
- **[!DNL Adobe Experience Platform]**: proporciona la infraestructura de datos básica, incluida la resolución de identidades, la unificación de perfiles, el control de datos y la aplicación del consentimiento de la que depende [!DNL Segment Match].

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las capacidades utilizadas en este patrón de caso de uso.

### [!DNL Segment Match]

- [Resumen de coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Solución de problemas de Coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### Segmentación y audiencias

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Resumen de composición de audiencia](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Identidad y perfil

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Resumen del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### Gobernanza de datos y consentimiento

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Aplicación de políticas](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview)
- [Consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [Grupo de campos de consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)

### Destinos y activación

- [Información general sobre los destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Monitorización de flujos de datos para destinos](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)

### Modelado y esquema de datos

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### Administración y control de acceso

- [Información general de control de acceso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home)
- [Información general de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home)

### Monitorización y observabilidad

- [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)

### Guardas

- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [Protecciones de activación](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

### Tutoriales

- [Creación de un esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [Habilitar un conjunto de datos para el perfil](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/enable-for-profile)
