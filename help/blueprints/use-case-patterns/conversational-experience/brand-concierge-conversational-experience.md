---
title: Experiencia de conversación en Brand Concierge
description: Aprenda a transformar las propiedades digitales en experiencias conversacionales seguras para la marca y con tecnología de IA que guíen el descubrimiento de clientes.
solution: Experience Platform, Real-Time Customer Data Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '7239'
ht-degree: 0%

---


# Experiencia conversacional en Brand Concierge

Esta guía proporciona una referencia de implementación completa para experiencias conversacionales con tecnología de IA que usan [!DNL Adobe Brand Concierge], integradas con [!DNL Adobe Experience Platform] (AEP) y [!DNL Real-Time Customer Data Platform] ([!DNL RT-CDP]). Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten implementar agentes conversacionales seguros para la marca en todas las propiedades digitales.

Abarca todos los enfoques viables para implementar experiencias conversacionales, desde bots de chat de asesoramiento de productos hasta asistentes de navegación de sitio completos, con instrucciones sobre cuándo elegir cada opción. El plan aborda la configuración del agente, el gobierno de marca, la integración de contenido, las estrategias de implementación, el enriquecimiento de perfiles a partir de señales de conversación y la optimización de análisis.

[!DNL Brand Concierge] permite a las marcas implementar agentes conversacionales inteligentes que entienden la voz de la marca, acceden a contenido y catálogos de productos aprobados, ofrecen recomendaciones personalizadas basadas en datos de perfiles en tiempo real y capturan señales de intención y opinión en el perfil unificado del cliente. El resultado es una experiencia de conversación que se siente natural y de marca, a la vez que enriquece la comprensión de la organización de cada cliente.

## Resumen del caso de uso

Las organizaciones buscan cada vez más transformar las experiencias digitales estáticas en conversaciones dinámicas impulsadas por IA que guíen a los clientes a través del descubrimiento, la selección de productos y las decisiones de compra. [!DNL Adobe Brand Concierge] Para solucionarlo, proporciona una capa de IA conversacional orquestada que se encuentra sobre las propiedades digitales existentes, con tecnología de AEP Agent Orchestrator.

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

**KPI:** porcentaje de aumento de ventas/venta cruzada, ingresos incrementales, valor de duración del cliente

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

## Patrón de caso de uso

**Experiencia conversacional en Brand Concierge**

Transforme las propiedades digitales en experiencias conversacionales seguras para la marca y con tecnología de IA que guíen el descubrimiento de clientes a través del diálogo natural, enriquezcan los perfiles con señales de intención y opinión y ofrezcan recomendaciones de productos personalizadas.

**Cadena de funciones:** Configuración del agente > Configuración de Brand Governance > Integración de contenido > Implementación de experiencias conversacionales > Enriquecimiento de perfiles > Analytics y optimización

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón de caso de uso.

- **[!DNL Brand Concierge]**: aplicación de experiencia conversacional con tecnología de IA que proporciona el agente de orquestación, Product Advisor Agent, el agente de asesoramiento de sitio, el control de marca y el análisis conversacional
- **[!DNL Adobe Experience Platform] (AEP)**: base de datos unificada que proporciona esquemas XDM, resolución de identidades, perfiles de clientes en tiempo real e infraestructura de recopilación de datos para señales conversacionales
- **[!DNL Real-Time CDP] ([!DNL RT-CDP])**: la plataforma de datos del cliente proporciona búsqueda de perfiles en tiempo real para conversaciones personalizadas, segmentación de audiencia a partir de señales conversacionales y enriquecimiento de perfiles con datos de intención y opinión

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Requerido | Zona protegida aprovisionada con el derecho de [!DNL Brand Concierge] habilitado; funciones configuradas para administradores de experiencias conversacionales, administradores de contenido y usuarios de Analytics; políticas ABAC establecidas para datos conversacionales que contienen PII o señales confidenciales del cliente | [Resumen de control de acceso](https://experienceleague.adobe.com/es/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | Esquemas XDM para eventos conversacionales (clase ExperienceEvent con grupos de campos específicos de la conversación que capturan la intención, la opinión, las interacciones de productos y los eventos de transferencia); esquema de perfil ampliado con preferencias conversacionales y atributos de intención; esquema de búsqueda del catálogo de productos para recomendaciones básicas | [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home) |
| Fuentes de datos y recopilación | Requerido | [!DNL Web SDK] o [!DNL Mobile SDK] configurados con flujos de datos que enrutan datos de evento conversacional a conjuntos de datos de AEP; integración de [!DNL Edge Network] para la captura de eventos en tiempo real durante las conversaciones; datos del catálogo de productos ingeridos mediante conectores de origen o la ingesta por lotes | [Información general del SDK web](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home) |
| Configuración de identidad y perfil | Requerido | Áreas de nombres de identidad configuradas para la identificación de visitantes (ECID para anónimo, CRM ID o correo electrónico para autenticado); política de combinación configurada con activación de Edge para la búsqueda de perfiles en tiempo real durante las conversaciones; reglas de vinculación de identidad para la continuidad de la conversación entre dispositivos | [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home) |
| Definición de audiencia y segmentación | Se asume en contexto | Audiencias no necesarias para la implementación conversacional principal, pero necesarias para estrategias de conversación personalizadas (por ejemplo, segmentos de clientes de alto valor reciben diferentes flujos de conversación); evaluación de streaming o Edge recomendada para la personalización de conversaciones en tiempo real | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Agregar señales de conversación en atributos de nivel de perfil (por ejemplo, conversaciones totales, intereses dominantes de productos, puntuación de opinión promedio) para su uso en la segmentación y personalización descendentes | [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview) |
| Administración del ciclo de datos | Recomendado | Configure políticas de retención para datos de eventos conversacionales, administre el consentimiento para la grabación y generación de perfiles de conversaciones y admita solicitudes de eliminación de privacidad para transcripciones de conversaciones | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/home) |
| Etiquetado y aplicación del uso de datos | Recomendado | Etiquetar campos de datos de conversación que contengan PII, opinión o señales de intención; aplicar políticas de gobernanza que impidan que los datos de conversación confidenciales lleguen a destinos no autorizados | [Resumen de control de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home) |
| Monitorización y observabilidad | Recomendado | Monitorice las canalizaciones de ingesta de eventos conversacionales, rastree las tasas de éxito de enriquecimiento del perfil y avise sobre los errores del flujo de datos que podrían afectar la calidad de la personalización de la conversación | [Resumen de Observability Insights](https://experienceleague.adobe.com/es/docs/experience-platform/observability/home) |
| Informes y análisis | Incluido | Analice el rendimiento de las conversaciones, los comentarios de los clientes, la atribución de conversión y la eficacia del agente con [!DNL Brand Concierge] análisis integrados y [!DNL CJA] para el análisis de impacto de las conversaciones en canales múltiples | [Información general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del Catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Brand Concierge]

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Configuración del agente | Fase 1: Configuración del agente | Configure [!DNL Brand Concierge] agent orchestrator con especializaciones de agente (Asesor de productos, Asesor de sitios) y configuración de comportamiento base |
| Configuración de Brand Governance | Fase 2: Configuración de Brand Governance | Defina la voz de la marca, el tono, las protecciones de mensajería, los límites del contenido aprobado y los temas prohibidos que dan forma a todas las interacciones conversacionales |
| Integración de contenido | Fase 3: Integración de contenido | Conecte fuentes de contenido aprobadas por la marca, incluido contenido de AEM, catálogos de productos, bases de conocimiento y otros datos de confianza, para fundamentar las respuestas |
| Configuración del Asesor de productos | Fase 3: Integración de contenido | Configure Product Advisor Agent para obtener recomendaciones de productos personalizadas, comparaciones guiadas y entregas de respuestas alineadas con la marca. |
| Configuración de Site Advisory | Fase 3: Integración de contenido | Configure el Agente de asesoramiento del sitio para mejorar la navegación adaptando las interacciones en función del comportamiento del visitante y las señales de intención |
| Implementación de experiencia de conversación | Fase 4: Implementación de la experiencia de conversación | Implemente experiencias conversacionales en todos los canales admitidos (web, aplicación móvil, SDK personalizado) con compatibilidad para la interacción de texto y voz |
| Administración de flujo de código bajo | Fase 4: Implementación de la experiencia de conversación | Permita que los equipos de marketing actualicen el tono, los flujos y el contenido conversacional mediante herramientas de configuración de código bajo |
| Enriquecimiento de perfil de conversación | Fase 5: enriquecimiento de perfiles | Enriquezca los perfiles de los clientes de AEP con las señales de intención, opinión, afinidad del producto y comportamiento capturadas durante las conversaciones |
| Análisis de conversación | Fase 6: Analytics y optimización | Monitorice las métricas de participación, los comentarios de los clientes, los datos de conversión y la calidad de la conversación a través de paneles de análisis integrados |
| Entrega del agente activo | Fase 4: Implementación de la experiencia de conversación | Configure el envío sin problemas a los agentes de soporte o ventas en directo, preservando al mismo tiempo el contexto de conversación completo |

### [!DNL Real-Time CDP]

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Búsqueda de perfiles en tiempo real | Fase 4: Implementación de la experiencia de conversación | Acceda a atributos de perfil del cliente en tiempo real y suscripciones a segmentos para personalizar las respuestas conversacionales en función de los datos de clientes conocidos |
| Enriquecimiento de perfiles | Fase 5: enriquecimiento de perfiles | Enriquezca los perfiles con atributos calculados derivados de eventos de comportamiento conversacional (puntuaciones por intención, tendencias de opinión, afinidad del producto) |
| Evaluación de audiencia | Fase 5: enriquecimiento de perfiles | Evalúe la pertenencia a audiencias en función de las señales conversacionales para permitir la segmentación descendente de segmentos conversacionales comprometidos |

## Prerrequisitos

Los siguientes elementos deben estar implementados antes de que comience la implementación.

- El derecho de [!DNL Adobe Brand Concierge] está activo para la organización
- Las licencias de AEP y [!DNL RT-CDP] se han aprovisionado con suficientes derechos de perfil y volumen de evento
- Documento de directrices de marca disponible que define temas de voz, tono, mensajería aprobada y prohibidos
- Catálogo de productos o repositorio de contenido preparado para la integración (recursos de AEM, datos de PIM o fuente de productos estructurada)
- Propiedades web identificadas para la implementación de experiencias conversacionales con acceso técnico para la integración con SDK
- Infraestructura de agente activa disponible si se requiere el traspaso (plataforma del centro de contacto, integración CRM)
- Marco de administración de consentimiento para la captura y generación de perfiles de datos conversacionales
- [!DNL Web SDK] o [!DNL Mobile SDK] ya se implementaron en las propiedades de destino (o se planearon para la implementación simultánea)
- Alineación de partes interesadas en el ámbito de la conversación (solo asesoramiento de productos, navegación del sitio o ambos)
- Se completó la revisión legal y de privacidad para la captura y el uso de datos conversacionales con tecnología de IA

## Opciones de implementación

Las secciones siguientes describen diferentes enfoques para implementar este patrón de caso de uso.

### Opción A: implementación del Asesor de productos

**Ideal para:** organizaciones de comercio electrónico y minoristas que se centran en experiencias guiadas de descubrimiento, comparación y recomendación de productos que impulsan la conversión y el valor de pedido promedio.

**Cómo funciona:**

El Product Advisor Agent se configura como la especialización conversacional principal. Se conecta al catálogo de productos, comprende los atributos y las relaciones del producto y guía a los clientes a través del diálogo natural para llegar a recomendaciones personalizadas. El agente utiliza protecciones de gobernanza de marca para garantizar que las recomendaciones se alineen con las prioridades comerciales (por ejemplo, promocionando artículos en stock, destacando productos con márgenes favorables).

El Asesor de productos se integra con el perfil del cliente en tiempo real para acceder al historial de compras, el comportamiento del explorador y los datos de preferencias, lo que permite realizar recomendaciones que tienen en cuenta lo que el cliente ya posee, ha considerado anteriormente o es probable que necesite en función de su perfil. Las conversaciones se capturan a medida que los eventos de experiencia y las señales de intención regresan al perfil para su uso posterior.

**Consideraciones clave:**

- Requiere un catálogo de productos bien estructurado con datos de atributos enriquecidos para lograr recomendaciones eficaces
- Los datos del producto deben mantenerse actualizados para evitar que se recomienden productos agotados o que se interrumpan
- El control de marca debe definir cómo gestiona el agente las menciones de productos competitivos y las comparaciones de precios

**Ventajas:**

- Impulsa directamente un impacto medible en los ingresos mediante la conversión guiada de compras
- Reduce las tasas de devolución de productos mediante decisiones de compra mejor informadas
- Captura señales de intención y afinidad de producto de alto valor para la personalización descendente
- Extensión natural de las experiencias de comercio electrónico existentes

**Limitaciones:**

- Requiere mantenimiento y sincronización continuos del catálogo de productos
- Limitado a conversaciones centradas en el producto; es posible que no se respondan las preguntas de navegación del sitio
- La eficacia depende de la calidad y la integridad de los datos del catálogo

**Experience League:**

- [Información general de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [asesor de producto de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)

### Opción B: despliegue de Site Advisory

**Ideal para:** organizaciones con propiedades digitales complejas (medios de comunicación, servicios financieros, atención médica, tecnología) en las que los visitantes necesitan asistencia de navegación para encontrar contenido, recursos o herramientas de autoservicio relevantes.

**Cómo funciona:**

El Agente de asesoramiento del sitio está configurado como la especialización conversacional principal. Indexa la estructura de contenido del sitio, comprende las relaciones entre páginas y las categorías de contenido y adapta su guía en función de las señales de comportamiento del visitante y la intención declarada. Cuando un visitante se involucra, el agente interpreta sus necesidades y las dirige al contenido, las herramientas o los recursos más relevantes.

El asesoramiento del sitio utiliza señales de comportamiento en tiempo real (página actual, fuente de referencia, ruta de navegación) combinadas con datos de perfil (visitas anteriores, preferencias de contenido, nivel de cliente) para proporcionar asistencia de navegación relevante para el contexto. Esto resulta especialmente útil en sitios con jerarquías de contenido profundas, varias líneas de productos o flujos de trabajo de autoservicio complejos.

**Consideraciones clave:**

- Requiere una indexación de contenido completa y una rastrea regular a medida que cambia el contenido del sitio
- Más eficaz en sitios con una amplitud de contenido significativa donde los visitantes suelen tener dificultades para encontrar lo que necesitan
- El control de marca debe definir los límites del ámbito (a qué áreas de sitio puede navegar el agente)

**Ventajas:**

- Reduce las tasas de devolución y mejora la capacidad de detección de contenido en sitios complejos
- Captura señales de intención de navegación que revelan lagunas de contenido y problemas de experiencia del usuario
- Complejidad de implementación menor que la del asesor de productos (no se requiere integración del catálogo de productos)
- Proporciona perspectivas de análisis de lo que los visitantes buscan pero no encuentran

**Limitaciones:**

- Menos directamente relacionado con la conversión de ingresos que las conversaciones centradas en el producto
- Requiere que el contenido esté bien estructurado y se actualice regularmente para obtener una orientación precisa
- Puede necesitar un reciclaje frecuente a medida que evoluciona la estructura del sitio

**Experience League:**

- [Información general de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [asesor del sitio de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)

### Opción C: implementación combinada de Asesor de productos + Asesor de sitios

**Ideal para:** organizaciones que desean una experiencia de conversación completa que abarque la detección de productos y la navegación por el sitio, normalmente grandes marcas comerciales o B2C con amplias propiedades digitales y diversos propósitos para los visitantes.

**Cómo funciona:**

Tanto Product Advisor Agent como Site Advisory Agent están configurados en el orquestador [!DNL Brand Concierge]. El agente de orquestación utiliza la detección de intención para dirigir las conversaciones a la especialización adecuada: las consultas relacionadas con el producto se dirigen al Asesor de productos mientras que las consultas de navegación y búsqueda de contenido se dirigen al Asesor de sitios. El orquestador gestiona transiciones sin problemas entre especializaciones dentro de una sola conversación.

Este enfoque proporciona la experiencia de conversación más completa, y gestiona toda la gama de necesidades de los visitantes, desde &quot;Ayúdeme a encontrar un producto&quot; hasta &quot;¿Dónde puedo comprobar el estado de mi pedido?&quot; Las protecciones de gobernanza de marca se aplican uniformemente en ambas especializaciones, lo que garantiza una voz de marca coherente independientemente del tema de conversación.

**Consideraciones clave:**

- Mayor complejidad de la implementación que requiere integración de contenido y catálogo de productos
- El enrutamiento por intención entre especializaciones debe estar bien ajustado para evitar conversaciones mal dirigidas
- La configuración de gobernanza de marca es más extensa para cubrir tanto los contextos de producto como de navegación

**Ventajas:**

- Proporciona la experiencia de conversación más completa para los visitantes
- Un solo punto de entrada gestiona distintas intenciones del visitante sin necesidad de interfaces independientes
- Las conversaciones de especialización cruzada (por ejemplo, las preguntas sobre productos que conducen a la navegación de soporte) se gestionan de forma natural
- Mayor enriquecimiento de perfiles a partir de diversas señales de conversación

**Limitaciones:**

- Máximo esfuerzo de implementación y mantenimiento continuo
- Requiere coordinación entre el catálogo de productos y los equipos de contenido
- Requisitos más complejos de comprobación y control de calidad
- La configuración de gobernanza de marca está más implicada

**Experience League:**

- [Información general de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)

### Comparación de opciones

| Criterios | Opción A: Asesor De Productos | Opción B: Site Advisory | Opción C: combinada |
| --- | --- | --- | --- |
| Mejor para | Comercio electrónico, conversión basada en productos | Sitios con contenido elevado, navegación de autoservicio | Experiencia digital de ámbito completo |
| Complejidad | Medio | Low-Medium | Alta |
| Tiempo hasta el valor | 4 a 6 semanas | 3 a 5 semanas | 6 a 10 semanas |
| Impacto en ingresos | Alto (influencia de conversión directa) | Medium (indirecto mediante participación) | Máximo (conversión y participación) |
| Requisitos de contenido | Catálogo de productos con atributos enriquecidos | Índice de contenido del sitio | Catálogo de productos e índice de contenido |
| Enriquecimiento de perfiles | Afinidad del producto, intención de compra | Intento de navegación, preferencias de contenido | Espectro de señal completo |
| Mantenimiento | Sincronización del catálogo de productos | Reindexación de contenido | Ambos en curso |

### Elija la opción correcta

Comience por evaluar su objetivo empresarial principal y las características de la propiedad digital:

1. **Si su objetivo principal es impulsar la conversión de productos** y su propiedad digital se centra en el comercio, elija **Opción A (Asesor de productos)**. Este es el punto de partida más común para las marcas de comercio minorista y electrónico.

2. **Si su objetivo principal es mejorar la detección de contenido** y su sitio tiene jerarquías de contenido profundas o flujos de trabajo de autoservicio complejos, elija **Opción B (Site Advisory)**. Esto es ideal para empresas de medios de comunicación, servicios financieros, sanidad y tecnología.

3. **Si necesita cobertura completa** y necesita tanto comercio de productos como navegación de contenido, elija **Opción C (combinada)**. Considere la posibilidad de empezar con una especialización y añadir la segunda después de la primera es estable y optimizada.

Se recomienda un enfoque por fases para la mayoría de las organizaciones: implemente primero una especialización, valide el rendimiento, recopile conocimientos y, a continuación, expanda a la implementación combinada.

## Fases de implementación

Las siguientes fases describen la secuencia de implementación recomendada.

### Fase 1: Configuración del agente

**Función de aplicación:** [!DNL Brand Concierge]: Configuración del agente

Configure el agente orquestador principal de [!DNL Brand Concierge], incluida la selección de las especializaciones del agente (Asesor de productos, Asesor de sitios o ambos), la configuración del comportamiento del agente base y el establecimiento de la conexión entre [!DNL Brand Concierge] y AEP para el acceso al perfil y la captura de eventos.

#### Decisión: selección de especialización del agente

Determine qué especializaciones de agente deben activarse para este despliegue.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo Asesor de productos | Implementación centrada en Commerce y dirigida a descubrir y convertir productos | Requiere integración del catálogo de productos; la ruta más rápida al impacto en los ingresos |
| Solo Site Advisory | Implementación de contenido y centrada en la navegación | Menor complejidad de la integración; mejor para sitios que no sean de comercio |
| Ambas especializaciones | Amplia cobertura conversacional sobre productos y contenido | Mayor complejidad; considere el despliegue gradual empezando por uno |

#### Decisión: modelo de inicio de conversación

Determine cómo deben comenzar las conversaciones sobre la propiedad digital.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Iniciado por el visitante (pasivo) | Enfoque predeterminado en el que el widget de chat está disponible pero no interactúa de forma proactiva | Menor riesgo de interrupción; depende del conocimiento del visitante de la opción de chat |
| Participación proactiva (activada) | El agente inicia una conversación en función de señales de comportamiento (por ejemplo, tiempo de permanencia prolongado, visitas repetidas a la página, vacilación en el carro de compras) | Tasas de participación más altas, pero corre el riesgo de molestar al visitante si los déclencheur son demasiado agresivos; requiere un ajuste del déclencheur de comportamiento |
| Híbrido (pasivo con indicadores contextuales) | El widget de chat es pasivo, pero muestra mensajes contextuales basados en el contenido de la página o en el comportamiento del visitante | Enfoque equilibrado; guía de indicadores sin forzar la participación |

#### Configuración del agente

**Navegación de la interfaz de usuario:** [!DNL Experience Platform] > Asistente de IA > [!DNL Brand Concierge] > Configuración del agente

Detalles de configuración clave:

- Defina el nombre y la descripción del agente que aparecerán en la interfaz conversacional
- Seleccione qué zona protegida de AEP contiene el perfil del cliente y los datos de evento a los que el agente debe acceder
- Configure el agente de orquestación para enrutar consultas entre especializaciones en función de la detección de intención
- Establecer parámetros de sesión de conversación (duración del tiempo de espera, duración máxima de la conversación, límites de sesión simultánea)
- Habilite la integración de búsqueda de perfiles en tiempo real para que el agente pueda acceder a los datos de perfil del visitante durante las conversaciones

**Donde las opciones difieren:**

**Para La Opción A (Asesor De Productos):**
Habilite la especialización Asesor de productos y configure su conexión con el origen de datos del catálogo de productos. Establezca parámetros de recomendación de productos, incluidas las recomendaciones máximas por respuesta, las preferencias de visualización de atributos de productos y las reglas de control de comparaciones.

**Para Opción B (Site Advisory):**
Habilite la especialización de Site Advisory y configure su conexión con el índice de contenido del sitio. Establezca parámetros de navegación, incluidos los límites del ámbito de contenido, la administración de categorías de página y las preferencias de generación de vínculos profundos.

**Para Opción C (Combinada):**
Habilite ambas especializaciones y configure la lógica de enrutamiento de intención del orquestador. Defina reglas de enrutamiento que determinen cuándo debe administrar un asesor de productos una conversación en lugar de un asesor de sitio, y cómo deben administrarse las transiciones entre especializaciones dentro de una sola conversación.

**Documentación de Experience League:**

- [Información general de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Información general del asistente de IA](https://experienceleague.adobe.com/es/docs/experience-platform/ai-assistant/home)
- [AEP Agent Orchestrator](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)

### Fase 2: Configuración de gobernanza de marca

**Función de aplicación:** [!DNL Brand Concierge]: Configuración de control de marca

Configure las protecciones de gobernanza de marca que dan forma a todas las interacciones conversacionales. Esto incluye definiciones de voz y tono de marca, límites de contenido aprobados, temas prohibidos, directrices de estilo de respuesta y reglas de escalación. La gobernanza de marca garantiza que cada respuesta generada por IA se ajuste a los estándares de marca.

#### Decisión: Nivel de rigidez de la gobernanza

Determine hasta qué punto las barreras de gobernanza de marca deben restringir las respuestas conversacionales.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Gobernanza estricta | Industrias altamente reguladas (servicios financieros, sanidad, seguros) o marcas premium que requieren un control preciso del tono | Limita la flexibilidad conversacional; puede dar como resultado respuestas más frecuentes de &quot;no puedo ayudar con eso&quot;; mayor seguridad de marca |
| Gobernanza moderada | La mayoría de las marcas de consumo donde la coherencia de la voz de la marca importa pero cierta flexibilidad de conversación es aceptable | Buen equilibrio entre seguridad de marca y naturalidad conversacional; punto de partida recomendado para la mayoría de las implementaciones |
| Gobernanza flexible | Marcas informales o de estilo de vida donde la personalidad conversacional y la participación tienen prioridad | La sensación de conversación más natural; requiere una monitorización más continua para las respuestas fuera de marca |

#### Decisión: estrategia de manejo fuera del tema

Determine cómo debe el agente gestionar las preguntas que se encuentran fuera del ámbito configurado.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Redirigir al ámbito | El agente reconoce la pregunta y le redirige a temas que le pueden ayudar | Mantiene la participación, pero puede frustrar a los visitantes con necesidades legítimas fuera del tema |
| Envío al agente activo | El agente ofrece conectar al visitante con un agente humano para preguntas fuera de tema | La mejor experiencia del cliente, pero requiere personal e infraestructura de agentes activos |
| Declive correcto con recursos | El agente explica que no puede ayudar con ese tema y proporciona vínculos a recursos relevantes o canales de soporte | Retroceso de baja fricción; no requiere disponibilidad del agente activo |

#### Configurar el gobierno de marca

**Navegación de la interfaz de usuario:** [!DNL Experience Platform] > Asistente de IA > [!DNL Brand Concierge] > Administración de marcas

Detalles de configuración clave:

- Defina atributos de marca: nombre de marca, lema, misión, valores y rasgos de personalidad que informen el tono conversacional
- Establecer parámetros de tono: nivel de formalidad, tolerancia al humor, nivel de empatía y asertividad para las recomendaciones de productos
- Configurar límites de contenido aprobado: temas que el agente está autorizado a discutir y temas explícitamente prohibidos
- Defina las directrices de formato de respuesta: longitud máxima de respuesta, uso de listas en comparación con prosa, política de emojis y formato de vínculos
- Establecer déclencheur de escalación: condiciones que deben enrutar automáticamente una conversación a un agente activo (por ejemplo, detección de quejas, señales de insatisfacción repetidas, identificación de clientes de alto valor)
- Configuración de la gestión de menciones competitivas: respuesta del agente cuando los visitantes preguntan por productos de la competencia
- Definir los requisitos de exención de responsabilidad y aviso legal: divulgación obligatoria para las industrias reguladas

**Documentación de Experience League:**

- [Gobernanza de marca Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Perspectivas operativas del asistente de IA](https://experienceleague.adobe.com/es/docs/experience-platform/ai-assistant/home)

### Fase 3: Integración de contenido

**Función de aplicación:** [!DNL Brand Concierge]: integración de contenido, configuración de asesor de producto, configuración de asesor de sitio

Configure las fuentes de contenido que basan las respuestas conversacionales en información precisa y aprobada por la marca. Esto incluye la integración del catálogo de productos, las conexiones de contenido de AEM, las importaciones de la base de conocimiento y las programaciones de actualización de contenido.

#### Decisión: método de integración del catálogo de productos

Determine cómo se deben proporcionar los datos del producto a Product Advisor Agent. (Sólo opciones A y C)

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Integración de conjuntos de datos AEP | El catálogo de productos ya se ha introducido en AEP como conjunto de datos de búsqueda a través de conectores de origen | Aprovecha la infraestructura de datos existente, mantiene los datos del producto sincronizados con los datos del perfil y requiere un modelado y una recopilación de datos fundacionales para incluir el catálogo de productos |
| Integración de fuentes directas | El catálogo de productos existe en un PIM o en una plataforma de comercio que puede proporcionar una fuente estructurada | Puede ofrecer más datos de precios e inventario en tiempo real; requiere configuración y programación de fuentes |
| Integración de contenido de AEM | El contenido del producto se administra en AEM y debe servir como fuente de datos autorizada del producto | Ideal para marcas donde AEM es el centro de contenido; garantiza la coherencia entre el contenido web y las respuestas conversacionales |

#### Decisión: frecuencia de actualización del contenido

Determine la frecuencia con la que se debe actualizar la base de conocimiento de contenido del agente.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Tiempo real/casi en tiempo real | La disponibilidad, los precios o los cambios de contenido de los productos cambian con frecuencia (por ejemplo, las ventas flash o el comercio minorista sensible al inventario) | Mayor precisión pero mayor carga de infraestructura; esencial para recomendaciones sensibles al inventario |
| Actualización diaria | Los cambios de contenido están planificados y programados (por ejemplo, calendarios editoriales o promociones semanales) | Buen equilibrio entre precisión y rendimiento; adecuado para la mayoría de las implementaciones |
| Actualización a petición | Los cambios de contenido son poco frecuentes y se pueden activar manualmente cuando se producen actualizaciones | Menor sobrecarga; adecuado para catálogos de productos estáticos o sitios de contenido estable |

#### Configuración de fuentes de contenido

**Navegación de la interfaz de usuario:** [!DNL Experience Platform] > Asistente de IA > [!DNL Brand Concierge] > Fuentes de contenido

Detalles de configuración clave:

- Conecte las fuentes de datos del catálogo de productos con la asignación de campos para el nombre del producto, la descripción, los atributos, los precios, la disponibilidad, las imágenes y la jerarquía de categorías
- Configure la indexación de contenido para páginas de sitios, artículos de la base de conocimiento, contenido de preguntas frecuentes y documentación de asistencia
- Definir los límites del ámbito de contenido que definen a qué contenido puede hacer referencia el agente y cuál se excluye
- Configure el comportamiento de reserva de contenido cuando el agente no encuentre contenido relevante para responder a una pregunta
- Configurar reglas de calidad de contenido: umbral mínimo de confianza de contenido para la inclusión en respuestas, requisitos de citas y atribución de fuente

**Donde las opciones difieren:**

**Para La Opción A (Asesor De Productos):**
Céntrese en la integración del catálogo de productos con la asignación de atributos de producto enriquecidos. Configure la lógica de recomendaciones de Product Advisor Agent, incluidos cuántos productos sugerir, cómo gestionar artículos sin existencias, cómo presentar comparaciones de productos y cómo incorporar datos de perfil del cliente (historial de compras, comportamiento de exploración) en la clasificación de recomendaciones.

**Para Opción B (Site Advisory):**
Céntrese en la indexación de contenido del sitio con asignación de jerarquía de páginas. Configure la lógica de navegación del Agente de asesoramiento del sitio, que incluye cómo interpretar la intención del visitante, qué categorías de contenido priorizar, cómo gestionar solicitudes de navegación ambiguas y cómo adaptar las sugerencias en función del contexto de página actual y del comportamiento de la sesión del visitante.

**Para Opción C (Combinada):**
Configure las fuentes de contenido del sitio y del catálogo de productos. Asegúrese de que la lógica de enrutamiento de contenido asigne correctamente el contenido a la especialización adecuada y de que las referencias cruzadas entre el contenido del producto y el contenido de navegación del sitio se asignen correctamente.

**Documentación de Experience League:**

- [Configuración de contenido de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [asesor de producto de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)
- [asesor del sitio de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)
- [Resumen de orígenes](https://experienceleague.adobe.com/es/docs/experience-platform/sources/home)

### Fase 4: Implementación de la experiencia de conversación

**Función de aplicación:** [!DNL Brand Concierge]: implementación de experiencia de conversación, administración de flujo de código bajo, transferencia de agente activo; [!DNL RT-CDP]: búsqueda de perfil en tiempo real

Implemente la experiencia de conversación en las propiedades digitales de Target, incluida la configuración de canal, la personalización de widgets, la integración de búsqueda de perfiles para la personalización, las reglas de transferencia de agentes en directo y las herramientas de código bajo para la administración de contenido continua.

#### Decisión: Canal de implementación

Determine en qué canal o canales se debe implementar la experiencia conversacional.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Web (widget incrustado) | La propiedad web principal es el punto de contacto principal del cliente | Punto de partida más común; requiere integración de [!DNL Web SDK]; admite visitantes anónimos y autenticados |
| Aplicación móvil (integración con SDK) | La aplicación móvil es un canal significativo de participación del cliente | Requiere integración con [!DNL Mobile SDK]; considere las restricciones de espacio en la pantalla para la IU de conversación |
| Implementación personalizada de SDK | La experiencia de conversación debe incrustarse en una aplicación, quiosco o propiedad digital no estándar personalizada | Máxima flexibilidad; requiere más esfuerzo de desarrollo; adecuado para quioscos en tienda o plataformas propietarias |
| Implementación de varios canales | Se necesita una experiencia de conversación simultánea en la web, dispositivos móviles y otros canales | Mayor alcance; requiere un control de marca coherente en todos los canales; el contexto de conversación debe persistir en todos los canales siempre que sea posible |

#### Decisión: profundidad de Personalization para las conversaciones

Determine cuántos datos de perfil del cliente debe utilizar el agente para personalizar las conversaciones.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo anónimo (contexto de sesión) | Enfoque centrado en la privacidad o cuando la mayoría de los visitantes no están identificados | Utiliza solo señales de comportamiento en la sesión; no se requiere búsqueda de perfiles; adecuado para la detección anónima de productos |
| Según el perfil (visitantes autenticados) | Los visitantes suelen iniciar sesión y realizar recomendaciones personalizadas basadas en el valor añadido del historial | Requiere búsqueda de perfiles en tiempo real mediante [!DNL RT-CDP]; calidad de recomendación significativamente mejor para clientes conocidos |
| Personalización progresiva | Combinación de lo anónimo y lo autenticado con la creación progresiva de perfiles durante la conversación | Comienza con el contexto de sesión; se enriquece a medida que el visitante proporciona información o se autentica; equilibra la privacidad y la personalización |

#### Decisión: configuración de transferencia del agente activo

Determine si las conversaciones deben ser escalables a agentes humanos vivos.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Sin transferencia (solo autoservicio) | El agente de IA puede gestionar todos los tipos de conversación esperados o los agentes en directo no están disponibles | La implementación más sencilla; puede frustrar a los visitantes con necesidades complejas; adecuado para escenarios de bajo riesgo y exploración de productos |
| Entrega basada en reglas | Los déclencheur específicos deben escalar a agentes activos (por ejemplo, detección de quejas, cliente de alto valor, consulta compleja) | Comportamiento de escalación predecible; requiere la definición de reglas y déclencheur de escalación; necesita la integración de la plataforma del agente activo |
| Entrega solicitada por el visitante | Los visitantes pueden solicitar un agente activo en cualquier momento de la conversación | La mejor experiencia del cliente; requiere personal de agente siempre disponible o administración de colas; el contexto de conversación debe transferirse |

#### Implementar la experiencia conversacional

**Navegación por la interfaz de usuario:** [!DNL Experience Platform] > Asistente de IA > [!DNL Brand Concierge] > Implementación

Detalles de configuración clave:

- Configure el aspecto del widget conversacional: posición, esquema de colores, avatar, mensaje de bienvenida y estilo de interacción (texto, voz o ambos)
- Integrar con [!DNL Web SDK] o [!DNL Mobile SDK] para la captura de eventos y la resolución de perfiles
- Configure la búsqueda de perfiles en tiempo real para acceder a los atributos del cliente, las suscripciones a segmentos y la actividad reciente durante las conversaciones
- Configure la integración de transferencia activa de agentes con la plataforma del centro de contacto, incluido el protocolo de transferencia de contexto, el enrutamiento de colas y la notificación al agente
- Habilite herramientas de administración de flujo de código bajo para que los equipos de marketing actualicen las variaciones de los inicios de conversación, los mensajes promocionales, el contenido estacional y el flujo sin la participación del desarrollador
- Configure las reglas de persistencia de sesión de conversación: cuánto tiempo se conserva el historial de conversaciones, si las conversaciones se pueden reanudar entre sesiones y la continuidad de la conversación entre dispositivos

**Documentación de Experience League:**

- [Implementación de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Información general de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home)
- [Información general sobre API de Edge Network Server](https://experienceleague.adobe.com/es/docs/experience-platform/edge-network-server-api/overview)
- [Extremo de entidades API de perfil](https://experienceleague.adobe.com/es/docs/experience-platform/profile/api/entities)
- [Resumen del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/home)

### Fase 5: Enriquecimiento del perfil

**Función de aplicación:** [!DNL Brand Concierge]: Enriquecimiento de perfil de conversación; [!DNL RT-CDP]: Enriquecimiento de perfil, Evaluación de audiencia

Configure la canalización de captura y enriquecimiento que devuelve las señales conversacionales al perfil unificado del cliente de AEP. Esto incluye la asignación de eventos de conversación a XDM, la extracción de señales de intención y opinión, la creación de atributos calculados a partir de datos conversacionales y la creación de audiencias basadas en comportamientos conversacionales.

#### Decisión: ámbito de captura de señal conversacional

Determine qué señales conversacionales deben capturarse y escribirse en el perfil del cliente.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo señales de participación principales | Enriquecimiento mínimo del perfil; captura del inicio, final, duración y estado de finalización de la conversación | Volumen de datos más bajo; suficiente para análisis básicos; valor de personalización limitado |
| Señales de intención y preferencia | Capturar los intereses inferidos del producto, las preferencias declaradas y las categorías de temas tratadas | Valor de personalización alto; volumen de datos moderado; recomendado con mayor frecuencia |
| Captura de señal completa | Captura de la intención, la opinión, las interacciones de productos, las respuestas de recomendaciones, los eventos de transferencia y las puntuaciones de comentarios | Enriquecimiento de perfil más rico; mayor volumen de datos; permite un análisis avanzado y una personalización basada en ML |

#### Decisión: Creación de audiencias a partir de datos conversacionales

Determine si las audiencias deben crearse en función de comportamientos conversacionales para la activación descendente.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| No hay audiencias de conversación | Datos de conversación utilizados únicamente para análisis, no para activación de audiencia | El enfoque más sencillo; adecuado si las conversaciones son complementarias a los canales de participación existentes. |
| Audiencias basadas en intenciones | Cree audiencias basadas en intereses de productos declarados o intenciones de navegación a partir de conversaciones | Permite volver a dirigirse a los visitantes que expresaron interés pero no se convirtieron; valor alto para el comercio |
| Audiencias de comportamiento | Cree audiencias basadas en patrones de participación en conversaciones (por ejemplo, participación alta, conversación abandonada, visitas repetidas) | Permite la orquestación de recorrido basada en la conversación y el seguimiento en canales múltiples |

#### Configuración del enriquecimiento de perfil

**Navegación de la interfaz de usuario:** [!DNL Experience Platform] > Cliente > Perfiles > Atributos calculados (para señales derivadas); Cliente > Audiencias > Crear audiencia (para audiencias conversacionales)

Detalles de configuración clave:

- Asigne eventos de conversación a campos de esquema de XDM ExperienceEvent que capturan el ID de conversación, el recuento de mensajes, los temas tratados, los productos referenciados, las puntuaciones de opinión y el estado de resolución
- Configurar el enriquecimiento del perfil [!DNL Brand Concierge] para escribir señales de intención y preferencia en el perfil unificado
- Crear atributos calculados a partir de datos de evento conversacional: conversaciones totales (duración), interés de categoría de producto dominante (30 días), puntuación de opinión promedio (90 días), tasa de conversión de conversación a compra
- Defina segmentos de audiencia de flujo continuo o por lotes basados en señales conversacionales para la activación descendente (por ejemplo, &quot;Visitantes que hablaron de la categoría de producto X en los últimos 7 días pero que no compraron&quot;)
- Valide el enriquecimiento del perfil buscando perfiles de muestra para confirmar que se rellenan atributos conversacionales

**Documentación de Experience League:**

- [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview)
- [Guía de IU de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/ui)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Resumen del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/home)

### Fase 6: Análisis y optimización

**Función de aplicación:** [!DNL Brand Concierge]: Análisis de conversación

Configure paneles e informes de análisis para medir el rendimiento de las experiencias conversacionales, identificar oportunidades de optimización y rastrear KPI. Esto incluye [!DNL Brand Concierge] análisis integrados, integración [!DNL CJA] opcional para análisis de impacto de conversaciones en canales múltiples y flujos de trabajo de optimización en curso.

#### Decisión: profundidad de Analytics

Determine qué nivel de análisis conversacional se necesita.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Análisis [!DNL Brand Concierge] integrados | Los informes estándar sobre el volumen de conversación, la participación, la satisfacción y la conversión son suficientes | El más rápido de activar; cubre los KPI principales; correlación limitada entre canales |
| Integración de [!DNL Brand Concierge] + [!DNL CJA] | Análisis en canales múltiples necesario para comprender cómo las conversaciones influyen en los recorridos más amplios de los clientes | Requiere conexión de [!DNL CJA] y configuración de vista de datos; habilita el análisis de atribución en conversaciones y otros canales |
| Pila de análisis completa ([!DNL Brand Concierge] + [!DNL CJA] + paneles personalizados) | Informes de nivel ejecutivo, modelado de atribución avanzado y creación de audiencias personalizadas a partir de las perspectivas de Analytics | Máxima capacidad analítica; requiere experiencia de [!DNL CJA]; habilita la optimización de conversaciones basada en datos |

#### Configuración de análisis y optimización

**Navegación de la interfaz de usuario:** [!DNL Experience Platform] > Asistente de IA > [!DNL Brand Concierge] > Analytics; [!DNL Analytics Platform] > Workspace (para [!DNL CJA])

Detalles de configuración clave:

- Revise [!DNL Brand Concierge] paneles de análisis integrados: tendencias del volumen de conversación, tasa de participación, tasa de finalización, puntuaciones de CSAT, tasa de aceptación de recomendaciones y frecuencia de transferencia
- Configure la conexión de [!DNL CJA] para incluir conjuntos de datos de evento conversacional para análisis en canales múltiples (si elige la integración de [!DNL CJA])
- Generar análisis del espacio de trabajo [!DNL CJA] para la atribución de conversación a conversión, identificando qué temas de conversación se correlacionan con el comportamiento de compra
- Configurar la monitorización de la calidad de las conversaciones: realizar un seguimiento de los temas en los que el agente tiene problemas, preguntas comunes sin responder y tendencias de opinión a lo largo del tiempo
- Definir flujos de trabajo de optimización: cadencia de revisión regular para actualizaciones de la gobernanza de marca, déclencheur de actualización de contenido y mejoras del flujo de conversación en función de las perspectivas de análisis

**Documentación de Experience League:**

- [Brand Concierge Analytics](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Información general sobre CJA Analysis Workspace](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/home)
- [Creación o edición de una conexión de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-connections/create-connection)
- [Creación o edición de una vista de datos de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/create-dataview)

## Consideraciones sobre la implementación

Las secciones siguientes abarcan protecciones, escollos comunes, prácticas recomendadas y decisiones de compensación que se deben tener en cuenta durante la implementación.

### Protecciones y límites

- [!DNL Brand Concierge] experiencias conversacionales están sujetas a límites de tasa de generación de respuestas de IA; la capacidad de conversación simultánea depende del nivel de asignación de derechos
- La búsqueda de perfiles en tiempo real durante las conversaciones está sujeta a límites de tasa de API de perfil por zona protegida — [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- La ingesta de datos de evento de conversación sigue los límites estándar de ingesta de transmisión de AEP: [protecciones de ingesta](https://experienceleague.adobe.com/es/docs/experience-platform/ingestion/guardrails)
- El tamaño del catálogo de productos y el volumen del índice de contenido están sujetos a [!DNL Brand Concierge] límites de integración de contenido
- Se aplica un máximo de 25 atributos calculados por zona protegida a las agregaciones de señales conversacionales: [protecciones de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview)
- Se aplica un máximo de 4000 definiciones de segmento por espacio aislado a las audiencias conversacionales: [Protecciones de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)

### Peligros comunes

- **Definición de control de marca insuficiente:** La implementación sin una configuración de control de marca exhaustiva resulta en respuestas fuera de la marca que dañan la confianza del cliente. Invierta mucho tiempo en la Fase 2 definiendo el tono, los límites y las reglas de escalación antes de la implementación.
- **Datos de catálogo de productos obsoletos:** Las recomendaciones del Asesor de productos basadas en datos de disponibilidad, precios o inventario obsoletos frustran a los clientes y erosionan la confianza. Establezca canalizaciones de actualización de contenido automatizadas con comprobaciones de validación.
- **déclencheur de participación proactiva excesivamente agresivos:** La configuración de déclencheur de comportamiento de forma demasiado agresiva (por ejemplo, si se activa una conversación después de 3 segundos en la página) molesta a los visitantes y aumenta las tasas de devolución. Comience con déclencheur conservadores y ajuste según los datos de participación.
- **Ignorar la experiencia de los visitantes anónimos:** Si se centra la personalización solo en visitantes autenticados, se ignora la mayoría del tráfico. Diseñe flujos de conversación que proporcionen valor a los visitantes anónimos mediante señales de comportamiento dentro de la sesión.
- **Omitir la configuración de enriquecimiento del perfil:** Implementar conversaciones sin capturar señales al perfil desperdicia datos valiosos de intención y preferencia. Configure el enriquecimiento de perfiles en paralelo con la implementación, no como una idea tardía.
- **Ignorar la experiencia de transferencia de agentes en vivo:** Las malas experiencias de transferencia (contexto perdido, preguntas repetidas, tiempos de espera largos) dañan la experiencia de conversación general más que no ofrecer transferencia. Pruebe el flujo de transferencia completo de extremo a extremo antes del lanzamiento.

### Prácticas recomendadas

- Comience con una sola especialización de agente (Asesor de productos o Asesor de sitios) y expanda después de establecer el rendimiento de línea de base.
- Realice talleres de gobernanza de marca con partes interesadas en el marketing, el área legal y la experiencia del cliente antes de configurar las protecciones.
- Utilice la personalización progresiva: inicie conversaciones con respuestas basadas en el contexto de la sesión y profundice la personalización a medida que el visitante proporciona información o se autentica.
- Implemente pruebas A/B de iniciadores de conversación, indicadores y formatos de presentación de recomendaciones con las herramientas de administración de flujo de código bajo.
- Programe una revisión periódica (semanal o quincenal) de los análisis de conversación para identificar lagunas de contenido, puntos de error comunes y oportunidades de optimización.
- Cree un bucle de comentarios entre análisis conversacionales y actualizaciones del control de marca; use los datos de conversación para refinar el tono, agregar nuevos temas aprobados y ajustar las reglas de escalación.
- Monitorice las tendencias de opinión de conversación como sistema de advertencia anticipada para problemas de productos, problemas del sitio o cambios en la percepción de la marca.
- Flujos de conversación de diseño que capturan de forma natural señales que enriquecen el perfil sin hacer que la interacción parezca un interrogatorio.

### Decisiones de compensación

>[!NOTE]
>Las siguientes decisiones de compensación deben evaluarse en función de los requisitos y restricciones específicos de su organización.

**Profundidad de personalización de la conversación vs. simplicidad de privacidad**

Una integración de perfiles más profunda permite conversaciones más personalizadas y eficaces, pero aumenta la complejidad de la recopilación de datos, los requisitos de consentimiento y la carga del cumplimiento de la privacidad.

- **Favoritos de personalización profunda:** mayores tasas de conversión, mejor calidad de recomendación, mayor enriquecimiento de perfiles y conversaciones más atractivas para los clientes que regresan
- **La simplicidad de la privacidad favorece:** Implementación más rápida, administración de consentimiento más sencilla, menor riesgo regulatorio y un posicionamiento de marca con prioridad en la privacidad
- **Recomendación:** Comience con una personalización progresiva que funcione bien para visitantes anónimos y agregue personalización basada en perfiles para sesiones autenticadas. Esto proporciona valor en todos los niveles de identificación y mantiene el cumplimiento de la privacidad manejable. Implemente la captura de consentimiento para la creación de perfiles conversacionales alineados con los marcos de consentimiento existentes.

**Restricción de la gobernanza de marca frente a naturalidad conversacional**

Las estrictas protecciones de gobernanza de marca garantizan que cada respuesta se ajuste a los estándares de la marca, pero las restricciones excesivamente rígidas hacen que las conversaciones se sientan robóticas y reducen la participación.

- **Favoritos estrictos de administración:** Seguridad de marca, cumplimiento normativo, mensajes coherentes y comportamiento predecible de los agentes
- **El control flexible favorece:** Flujo de conversación natural, mayor participación, mejor satisfacción del cliente y la capacidad de manejar una gama más amplia de consultas
- **Recomendación:** Comience con un control moderado y apriételo o afloje según los análisis de conversación. Monitorice la tasa de respuestas &quot;No puedo ayudar con eso&quot; como indicador de sobre-restricción. Utilice las herramientas de administración de flujo de código bajo para iterar en la configuración de gobernanza rápidamente sin la participación del desarrollador.

**Actualización de contenido en tiempo real vs. rendimiento del sistema**

La sincronización de contenido en tiempo real garantiza que el agente siempre tenga datos de contenido y productos actuales, pero una actualización continua consume más recursos de infraestructura y puede introducir latencia.

- **Favoritos de actualización en tiempo real:** Precisión para recomendaciones que dependen del inventario, promociones que dependen del tiempo y contenido que cambia rápidamente
- **Favoritos de actualización programados:** Estabilidad del sistema, consumo de recursos predecible y menores costos de infraestructura
- **Recomendación:** Utilice la actualización diaria de contenido como valor predeterminado, con actualización casi en tiempo real sólo para los datos de disponibilidad de inventario y precios que afecten de manera importante a la experiencia del cliente. Monitorice las métricas de precisión de contenido para determinar si la frecuencia de actualización es adecuada.

**Captura de señal completa frente a sobrecarga de administración de datos**

La captura de cada señal conversacional proporciona el mayor enriquecimiento de perfiles y análisis, pero aumenta el volumen de datos, los costes de almacenamiento y la complejidad de la gobernanza.

- **Favoritos de captura de señal completa:** Análisis avanzados, aprendizaje del modelo ML, enriquecimiento completo del perfil y valor máximo de personalización descendente
- **La captura selectiva favorece:** menores costos de almacenamiento, administración de datos más sencilla, rendimiento de búsqueda de perfiles más rápido y cumplimiento más sencillo de los principios de minimización de datos
- **Recomendación:** Comience con la captura de señal por intención y preferencia (el punto medio) y expanda a captura de señal completa solo después de validar que los datos adicionales crean un valor descendente mensurable. Aplique políticas de caducidad de conjuntos de datos a los datos de evento conversacional para administrar el crecimiento del almacenamiento.

## Documentación relacionada

Los siguientes recursos proporcionan información adicional para implementar este patrón de caso de uso.

**[!DNL Brand Concierge]**

- [Información general de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [asesor de producto de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)
- [asesor del sitio de Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)
- [Información general del asistente de IA](https://experienceleague.adobe.com/es/docs/experience-platform/ai-assistant/home)

**[!DNL Adobe Experience Platform]**

- [Información general de AEP](https://experienceleague.adobe.com/es/docs/experience-platform/landing/home)
- [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/composition)
- [Resumen del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/home)

**Recopilación e integración de datos**

- [Información general de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home)
- [Información general de Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure)
- [Información general sobre API de Edge Network Server](https://experienceleague.adobe.com/es/docs/experience-platform/edge-network-server-api/overview)
- [Resumen de orígenes](https://experienceleague.adobe.com/es/docs/experience-platform/sources/home)

**Identidad y perfil**

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview)
- [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview)

**Audiencias y segmentación**

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)

**Gobernanza de datos y privacidad**

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Grupo de campos de consentimiento y preferencias](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/field-groups/profile/consents)
- [Información general de Privacy Service](https://experienceleague.adobe.com/es/docs/experience-platform/privacy/home)
- [Información general sobre Advanced Data Lifecycle Management](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/home)

**Control y observabilidad**

- [Resumen de Observability Insights](https://experienceleague.adobe.com/es/docs/experience-platform/observability/home)
- [Resumen de alertas](https://experienceleague.adobe.com/es/docs/experience-platform/observability/alerts/overview)

**Análisis e informes**

- [Información general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview)
- [Información general sobre CJA Connections](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-connections/overview)
- [Resumen de vistas de datos de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/data-views)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/home)

**Protecciones**

- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- [Protecciones de ingesta](https://experienceleague.adobe.com/es/docs/experience-platform/ingestion/guardrails)
- [Protecciones de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
