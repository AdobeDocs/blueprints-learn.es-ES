---
title: Experiencia de conversación en Brand Concierge
description: Aprenda a transformar las propiedades digitales en experiencias conversacionales seguras para la marca y con tecnología de IA que guíen el descubrimiento de clientes.
solution: Experience Platform, Real-Time Customer Data Platform
exl-id: a9545328-316d-446a-9308-18af61c58d1c
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# Experiencia conversacional en Brand Concierge

Esta guía proporciona información general para experiencias conversacionales con tecnología de IA usando [!DNL Adobe Brand Concierge], integrado con [!DNL Adobe Experience Platform] (AEP) y [!DNL Real-Time Customer Data Platform] ([!DNL RT-CDP]). Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten implementar agentes conversacionales seguros para la marca en todas las propiedades digitales.

[!DNL Brand Concierge] permite a las marcas implementar agentes conversacionales inteligentes que entienden la voz de la marca, acceden a contenido y catálogos de productos aprobados, ofrecen recomendaciones personalizadas basadas en datos de perfiles en tiempo real y capturan señales de intención y opinión en el perfil unificado del cliente. El resultado es una experiencia de conversación que se siente natural y de marca, a la vez que enriquece la comprensión de la organización de cada cliente.

## Patrón de caso de uso

**Experiencia conversacional en Brand Concierge**

Transforme las propiedades digitales en experiencias conversacionales seguras para la marca y con tecnología de IA que guíen el descubrimiento de clientes a través del diálogo natural, enriquezcan los perfiles con señales de intención y opinión y ofrezcan recomendaciones de productos personalizadas.

**Plan de ejecución:** Configuración del agente > Configuración de Brand Governance > Integración de contenido > Implementación de experiencias conversacionales > Enriquecimiento de perfiles > Analytics y optimización

## Resumen del caso de uso

Las organizaciones buscan cada vez más transformar las experiencias digitales estáticas en conversaciones dinámicas impulsadas por IA que guíen a los clientes a través del descubrimiento, la selección de productos y las decisiones de compra. [!DNL Adobe Brand Concierge] resuelve esto al proporcionar una capa de IA conversacional orquestada que se encuentra sobre las propiedades digitales existentes, con tecnología de AEP Agent Orchestrator.

Este patrón es distinto de las implementaciones de bots de chat tradicionales porque está integrado de forma nativa con el perfil unificado de AEP, utiliza protecciones de gobernanza de marca para garantizar que cada respuesta se ajuste a los estándares de marca y envía señales conversacionales de nuevo a la plataforma de datos del cliente para la personalización y activación descendentes.

La audiencia de destino incluye equipos de experiencia digital, administradores de comercio electrónico, estrategas de contenido y tecnólogos de marketing que necesitan implementar experiencias de conversación inteligentes que impulsen la participación, la conversión y el enriquecimiento de perfiles.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Ofrezca experiencias de cliente personalizadas

Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo de vida individuales.

**KPI:** participación, tasas de conversión, satisfacción del cliente (CSAT)

[Obtenga más información sobre cómo ofrecer experiencias de cliente personalizadas](/help/blueprints/business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

### Mejore la participación del cliente

Aumente la frecuencia y profundidad de interacción en todos los puntos de contacto digitales y físicos.

**KPI:** participación, tiempo de espera (página web), tasas de apertura

[Obtenga más información sobre cómo mejorar la participación de los clientes](/help/blueprints/business-objectives/qualification-sales-b2b/improve-customer-engagement.md)

### Aumentar tasas de conversión

Mejore el porcentaje de visitantes y clientes potenciales que completan las acciones deseadas, como compras, suscripciones o envíos de formularios.

**KPI:** tasas de conversión, conversión de posibles clientes, costo por posible cliente

[Más información sobre el aumento de las tasas de conversión](/help/blueprints/business-objectives/revenue-monetization/increase-conversion-rates.md)

### Adquisición de nuevos clientes

Amplíe la base de clientes con campañas de adquisición dirigidas, audiencias similares y optimización de medios de pago.

**KPI:** nuevos clientes, coste de adquisición del cliente, conversión de cliente potencial/posible cliente

[Más información sobre la adquisición de nuevos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran cómo se puede aplicar este patrón en la práctica.

- **Asistente para la detección de productos**: implemente un agente conversacional en las páginas de listas de productos que formule preguntas de calificación y reduzca las recomendaciones de productos en función de las necesidades, preferencias y presupuesto del cliente
- **Asesor de comparación guiada**: Ayude a los clientes a comparar los productos en paralelo mediante un diálogo natural, resaltando las diferencias relevantes para sus prioridades declaradas
- **Conserje de talla y ajuste** — Guía a los compradores de ropa o calzado a través de la selección de tallas usando preguntas y respuestas conversacionales, reduciendo los retornos y aumentando la confianza de compra
- **Selector de suscripción o plan**: guíe a los clientes a través de las opciones de plan de suscripción o nivel de servicio con recomendaciones personalizadas basadas en patrones de uso y necesidades declaradas
- **Asistente de navegación del sitio**: ayude a los visitantes a encontrar contenido, recursos de soporte o categorías de productos relevantes en función de su intención declarada, lo que reduce las tasas de devolución en sitios complejos
- **Consulta previa a la compra**: proporcione orientación para la compra de alta consideración (por ejemplo, productos electrónicos, financieros, seguros) mediante conversaciones de varias vueltas que se adapten a una recomendación
- **Conserje del programa de fidelización**: ayude a los miembros fieles a descubrir recompensas, comprender los beneficios del nivel y encontrar oportunidades de canje a través de la interacción conversacional
- **Conversación de renovación de participación**: inicie una conversación proactiva con los visitantes que regresan en función del historial de exploración anterior o de los elementos del carro de compras abandonados
- **Escalación de agente en vivo con contexto**: transfiera sin problemas consultas complejas a agentes de ventas o soporte en vivo y, al mismo tiempo, preserve el contexto de conversación completo y los datos de perfil del cliente
- **Soporte posterior a la compra y ampliación de venta**: involucre a los clientes después de la compra con asistencia para la configuración, sugerencias de productos complementarias y registros de satisfacción a través de canales conversacionales

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir el éxito de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de interacción de conversación | Porcentaje de visitantes que inician y mantienen una conversación | Conversaciones iniciadas/vistas de página aptas |
| Tasa de finalización de conversación | Porcentaje de conversaciones que alcanzan una resolución significativa | Conversaciones completadas/conversaciones iniciadas |
| Tasa de conversión conversacional | Porcentaje de conversaciones que conducen a una acción deseada (compra, registro, formulario de posible cliente) | Conversiones de conversación / conversaciones totales |
| Profundidad promedio de la conversación | Número de giros por conversación, lo que indica la calidad de la participación | Promedio de recuento de mensajes por sesión |
| Satisfacción del cliente (CSAT) | Puntuación de satisfacción posterior a la conversación a partir de los comentarios dentro de la experiencia | Respuestas de encuesta o clasificaciones de miniaturas arriba/abajo |
| Tasa de aceptación de recomendaciones | Porcentaje de recomendaciones de productos aceptadas o seleccionadas | Recomendaciones aplicadas/recomendaciones atendidas |
| Velocidad de transferencia del agente activo | Porcentaje de conversaciones escaladas a agentes activos | Entregas / conversaciones totales |
| Tasa de enriquecimiento de perfil | Porcentaje de conversaciones que arrojan nuevas señales de intención o preferencia | Perfiles enriquecidos/conversaciones totales |
| Ingresos influidos por la conversación | Ingresos por compras donde una conversación [!DNL Brand Concierge] precedió a la conversión | Análisis de atribución en recorridos de conversación a compra |
| Tiempo de resolución | Duración media desde el inicio de la conversación hasta la resolución o el traspaso | Análisis de marcas de tiempo en eventos de conversación |

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón de caso de uso.

- **[!DNL Brand Concierge]**: aplicación de experiencia conversacional con tecnología de IA que proporciona el agente de orquestación, Product Advisor Agent, el agente de asesoramiento de sitio, el control de marca y el análisis conversacional
- **[!DNL Adobe Experience Platform](AEP)**: base de datos unificada que proporciona esquemas XDM, resolución de identidades, perfiles de clientes en tiempo real e infraestructura de recopilación de datos para señales conversacionales
- **[!DNL Real-Time CDP]([!DNL RT-CDP])**: la plataforma de datos del cliente proporciona búsqueda de perfiles en tiempo real para conversaciones personalizadas, segmentación de audiencia a partir de señales conversacionales y enriquecimiento de perfiles con datos de intención y opinión

## Documentación relacionada

Para obtener instrucciones de implementación y más información, consulte la [descripción general de Brand Concierge](https://experienceleague.adobe.com/en/docs/brand-concierge/content/documentation/overview) en Adobe Experience League.
