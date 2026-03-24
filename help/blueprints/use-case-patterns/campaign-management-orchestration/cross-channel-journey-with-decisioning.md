---
title: Recorrido en canales múltiples con toma de decisiones
description: Aprenda a organizar un recorrido de varios pasos que incorpore decisiones en tiempo real para seleccionar un canal, contenido u oferta óptimos.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: eabdd91f-bb7d-4de3-adb5-5940d3ca4a78
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '9029'
ht-degree: 2%

---

# Recorrido en canales múltiples con toma de decisiones

Esta guía proporciona una referencia completa de implementación para el recorrido entre canales con la toma de decisiones. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesitan orquestar recorridos de varios pasos y canales que incorporen la toma de decisiones en tiempo real en uno o más nodos de recorrido.

Utilice esta guía para comprender el panorama completo de las opciones de implementación, evaluar los sacrificios y navegar hasta la documentación de Experience League correspondiente para obtener instrucciones de configuración detalladas.

El recorrido en canales múltiples con toma de decisiones es el patrón de orquestación de campaña más sofisticado en el ecosistema [!DNL Adobe Experience Platform]. Amplía los recorridos organizados en varios pasos al incorporar la toma de decisiones en tiempo real (mediante [!DNL AJO] Decisioning) para evaluar el contexto actual de un perfil y seleccionar dinámicamente el canal, el contenido o la oferta óptimos en uno o más puntos de decisión dentro del lienzo de recorrido.

## Resumen del caso de uso

Las organizaciones necesitan cada vez más ofrecer recorridos de cliente adaptables y personalizados que respondan dinámicamente al contexto en tiempo real de cada individuo en lugar de seguir una secuencia fija y predeterminada. El canal preferido de un cliente, su historial de participación, su nivel de lealtad, su valor de duración predicho y sus intereses actuales de productos dependen de cuál debe ser la mejor acción siguiente en cada punto de contacto.

El recorrido en canales múltiples con toma de decisiones aborda esta necesidad combinando dos potentes capacidades de [!DNL AJO]: orquestación de recorrido (que administra el flujo de varios pasos, el tiempo, las condiciones y la entrega de canal) y toma de decisiones (que evalúa las reglas de elegibilidad, aplica estrategias de clasificación y selecciona la oferta óptima o la variante de contenido en cada punto de decisión).

Este patrón es adecuado cuando:

- El recorrido debe adaptarse dinámicamente al estado en tiempo real de cada perfil en lugar de seguir un canal fijo o una secuencia de contenido
- Varias ofertas, variantes de contenido o canales son candidatos en uno o más nodos de recorrido y la mejor opción debe seleccionarse en función del contexto del perfil
- Se necesita una clasificación asistida por IA o basada en fórmulas para optimizar la selección de ofertas en todo el recorrido
- La organización desea consolidar la lógica de selección de canales y la administración de ofertas en un marco de decisión centralizado, en lugar de mantener una lógica de ramificación compleja

La audiencia de destino incluye a los especialistas en marketing que administran programas del ciclo vital, recorridos de lealtad, secuencias de recuperación e flujos de incorporación en los que la personalización a escala requiere la toma de decisiones automatizada en cada punto de contacto.

>[!NOTE]
>Si el recorrido no requiere la toma de decisiones dinámica en nodos individuales (por ejemplo, un programa de nutrición o de incorporación de secuencia fija), consulte [recorrido orquestado de varios pasos](multi-step-orchestrated-journey.md). Ese patrón es más sencillo de configurar y no requiere AJO Decisioning.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

**[Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo de vida individuales.
**KPI:** participación, tasas de conversión, satisfacción del cliente (CSAT)

**[Aumentar la lealtad del cliente y el valor de duración](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
Profundice las relaciones con los clientes y maximice el valor a largo plazo mediante programas de fidelidad, recompensas y participación personalizada.
**KPI:** valor de duración del cliente, retención, aumento de venta/venta cruzada %

**[Mejorar la retención de clientes](../../business-objectives/customer-experience/improve-customer-retention.md)**
Mantenga el compromiso de los clientes existentes y renuévelos mediante experiencias basadas en valores y una nutrición continua de las relaciones.
**KPI: retención de**, valor de duración del cliente, participación

**[Aumentar los ingresos de ventas cruzadas y ventas adicionales](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
Promocione productos o servicios complementarios y de primera calidad a los clientes existentes en función del comportamiento y el historial de compras.
**KPI:**, porcentaje de ampliación de venta/venta cruzada, ingresos incrementales, valor de duración del cliente

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran cómo se puede aplicar en la práctica el recorrido entre canales con la toma de decisiones.

- **recorrido adaptable de recuperación**: un recorrido de varios pasos donde la toma de decisiones selecciona el canal (correo electrónico, push o SMS) en función del historial de participación de cada perfil y selecciona dinámicamente la mejor oferta de incentivos en función del valor de duración predicho
- **recorrido del ciclo de vida de la siguiente mejor acción**: la toma de decisiones determina qué comunicar en cada fase del ciclo de vida del cliente, seleccionando entre contenido de incorporación, ofertas de venta cruzada, recompensas por fidelidad o incentivos de retención
- **Incorporación personalizada con selección de contenido dinámico**: nuevo recorrido de incorporación del cliente en el que cada punto de contacto utiliza la toma de decisiones para seleccionar el contenido de educación del producto, las sugerencias o las ofertas de activación más relevantes
- **recorrido de programas de fidelización en canales múltiples con recompensas personalizadas**: los miembros de fidelidad progresan a través de un recorrido en el que la toma de decisiones selecciona ofertas de recompensas personalizadas basadas en el nivel, el historial de compras y la afinidad de la categoría
- **Reparticipación dinámica con la optimización de canales e incentivos**: reparticipación inactiva de clientes donde tanto el canal de alcance como el incentivo se seleccionan dinámicamente para maximizar la probabilidad de respuesta
- **Nutrición del ciclo de vida del cliente con recomendaciones de contenido clasificado por IA**: recorrido de nutrición continua en el que la toma de decisiones clasificadas por IA selecciona las recomendaciones de contenido o producto más relevantes en cada punto de contacto

## Indicadores clave de rendimiento

Utilice los siguientes KPI para medir la eficacia de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de finalización de recorridos | Porcentaje de perfiles que completan el recorrido completo | Informe de recorrido: completado/introducido |
| Tasa de aceptación de ofertas | Porcentaje de ofertas seleccionadas para la toma de decisiones que participan en (se hace clic y se canjea) | Informe de decisiones: clics en ofertas / impresiones de ofertas |
| Tasa de participación en canal | Tasas de apertura y clics en cada canal utilizado en el recorrido | Métricas de envío por canal en el informe de recorrido |
| Tasa de conversión | Porcentaje de participantes en el recorrido que completan la acción de conversión de destino | Seguimiento de eventos de salida de recorrido para análisis de CJA funnel |
| Tasa de ofertas de reserva | Porcentaje de solicitudes de decisión que devuelven la oferta de reserva en lugar de una oferta personalizada | Informe de decisiones: selecciones de reserva/selecciones totales |
| Impacto en valor de duración de cliente | Cambio en CLV para los participantes del recorrido frente al grupo de control | Análisis de cohorte de CJA con comparación de exclusión |
| Ingresos de venta cruzada/aumento de ventas | Ingresos incrementales atribuidos a ofertas seleccionadas para la toma de decisiones | Análisis de atribución de CJA en conversiones impulsadas por ofertas |
| Eficacia de clasificación de decisiones | Diferencia de rendimiento entre ofertas clasificadas por IA y selección aleatoria/basada en prioridad | Experimento A/B que compara estrategias de clasificación |

## Patrón de caso de uso

**recorrido en canales múltiples con toma de decisiones**

Orqueste un recorrido de varios pasos y canales que incorpore la toma de decisiones en tiempo real en uno o más nodos para seleccionar el canal, el contenido o la oferta óptimos.

**Cadena de funciones:** Evaluación de audiencias > Ejecución de Recorrido > Nodo de decisión > Selección de canal > Entrega de mensaje > Informes

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón de caso de uso.

- **[!DNL Adobe Journey Optimizer]([!DNL AJO])**: orquestación de Recorrido (diseño de lienzo de varios pasos, condiciones de entrada, esperas, condiciones, criterios de salida), creación de mensajes en todos los canales, configuración de superficie de canal, administración de conflictos y prioridades
- **[!DNL Adobe Journey Optimizer]decisión**: administración de ofertas y elementos de contenido, reglas de elegibilidad, estrategias de clasificación (prioridad, fórmula, IA), políticas de decisión, ubicaciones, ofertas de reserva
- **[!DNL Adobe Real-Time Customer Data Platform]([!DNL RT-CDP])**: evaluación de audiencia para segmentos de idoneidad de entrada de recorrido y oferta, enriquecimiento de perfil con atributos calculados y puntuaciones de tendencia, aplicación de consentimiento y gobernanza
- **[!DNL Adobe Experience Platform]([!DNL AEP])**: almacén de perfiles de cliente en tiempo real, servicio de identidad para resolución en canales múltiples, modelado de datos e infraestructura de ingesta

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Se asume en contexto | [!DNL AJO] zona protegida con permisos de recorrido, campaña y toma de decisiones configurados. Superficies de canal para todos los canales de envío posibles. Funciones de usuario para diseñadores de recorrido, administradores de decisiones y autores de contenido. | [Resumen de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home), [Resumen de control de acceso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | El esquema de perfil debe incluir atributos utilizados para la toma de decisiones (por ejemplo, nivel de lealtad, historial de compras, preferencias de canal y puntuaciones de participación). Se deben configurar los esquemas de catálogo de ofertas y elemento de decisión. Los esquemas ExperienceEvent deben capturar señales de comportamiento utilizadas por las reglas de idoneidad y las fórmulas de clasificación. | [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [Conceptos básicos de composición de esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Fuentes de datos y recopilación | Se asume en contexto | Los atributos de perfil y las señales de comportamiento utilizados por la toma de decisiones deben ser actuales. La transmisión de eventos en tiempo real es necesaria si el recorrido utiliza criterios de entrada o salida activados por eventos. Web SDK, Mobile SDK o la colección del lado del servidor deben estar activos para los canales que alimentan el contexto de toma de decisiones. | [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Resumen de orígenes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| Configuración de identidad y perfil | Requerido | La resolución de identidades en canales múltiples es crítica: el recorrido debe resolver perfiles en correos electrónicos, notificaciones push, SMS y web. Las políticas de combinación deben producir un perfil unificado para la toma de decisiones. Deben configurarse las áreas de nombres de identidad para todos los identificadores de cliente (ID de CRM, correo electrónico, ECID, teléfono). | [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Introducción a las políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Definición de audiencia y segmentación | Requerido | Definición de audiencia de entrada para el recorrido. Segmentos adicionales utilizados para reglas de idoneidad de ofertas y ramas de condiciones dentro del recorrido. El método de evaluación debe coincidir con los requisitos de latencia (flujo continuo para la entrada en tiempo real, lote para la programada). | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Guía de la interfaz de usuario del generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Los atributos calculados, como las puntuaciones de tendencia de la inteligencia artificial aplicada al cliente, las puntuaciones de participación, las puntuaciones de preferencias de canal y los cálculos de valor de duración, mejoran significativamente la calidad de la toma de decisiones. Estos atributos de perfil enriquecidos permiten reglas de elegibilidad y fórmulas de clasificación más sofisticadas. | [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Resumen de inteligencia artificial aplicada al cliente](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Administración del ciclo de datos | Recomendado | El historial de ofertas y los datos del evento de decisión se acumulan con el tiempo y deben tener políticas de retención. La aplicación del consentimiento en varios canales es crítica: los perfiles sin consentimiento válido para un canal deben excluirse de la ruta de entrega de ese canal. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted) |
| Etiquetado y aplicación del uso de datos | Recomendado | La aplicación de la gobernanza en varios canales y tipos de oferta es importante cuando la toma de decisiones puede enrutar perfiles a diferentes canales con diferentes restricciones del uso de datos. Garantiza la entrega de ofertas compatibles en todos los canales. | [Información general sobre el control de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Aplicación de directivas](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview) |
| Monitorización y observabilidad | Incluido | La supervisión del recorrido y la toma de decisiones es esencial para las operaciones de producción. Las alertas para errores de entrada de recorrido, picos de reserva de toma de decisiones y errores de entrega permiten la resolución rápida de problemas. | [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Informes y análisis | Incluido | Los informes de recorrido y toma de decisiones se tratan en la fase de creación de informes. El análisis de CJA de la efectividad de las decisiones, la optimización de la combinación de canales, el rendimiento de las ofertas y el ROI de los recorridos proporciona la información necesaria para refinar las estrategias de clasificación y optimizar los recorridos a lo largo del tiempo. | [descripción general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Journey Optimizer] ([!DNL AJO])

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Configuración de canal | Fase 2: Configuración de canal | Configure las superficies de canal para todos los canales que seleccione Decisioning o que utilice el recorrido (correo electrónico, SMS, push, en la aplicación) |
| Creación de mensajes | Fase 4: Creación de mensajes | Crear contenido de mensaje para cada canal e integrar salida de decisión: ubicaciones de ofertas, bloques de contenido dinámico, tokens de personalización de ofertas seleccionadas |
| Decisioning | Fase 3: Configuración de decisiones | Configure elementos de oferta, reglas de elegibilidad, estrategias de clasificación, políticas de decisión y ofertas de reserva para cada punto de decisión en el recorrido |
| Journey Orchestration | Fase 5: Diseño y activación del Recorrido | Diseñe el lienzo de recorrido de varios pasos con condiciones de entrada, nodos de decisión, enrutamiento de canales, pasos de espera, acciones de mensajes y criterios de salida |
| Administración de conflictos y prioridades | Fase 5: Diseño y activación del Recorrido | Configure las puntuaciones de prioridad y la detección de conflictos si varios recorridos pueden dirigirse a los mismos perfiles simultáneamente |
| Frecuencia y reglas comerciales | Fase 5: Diseño y activación del Recorrido | Haga cumplir los límites de frecuencia de los mensajes en todos los canales para evitar el exceso de mensajes dentro del recorrido multicanal |
| Informes y análisis de rendimiento | Fase 6: Informes y monitorización | Monitorización de las métricas de entrega de recorridos y por nodo, toma de decisiones, rendimiento y participación en el canal |

### [!DNL Real-Time CDP] ([!DNL RT-CDP])

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Evaluación de audiencia | Fase 1: Evaluación de audiencias | Defina y evalúe la audiencia de entrada o el evento de entrada correspondiente; cree segmentos de idoneidad utilizados por la toma de decisiones |
| Enriquecimiento de perfiles | Requisito previo/asistencia | Enriquezca los perfiles con atributos calculados y puntuaciones de tendencia que mejoren la calidad de las decisiones |
| Cumplimiento del consentimiento y la gobernanza | Fase 2: Configuración de canal | Aplicar las preferencias de consentimiento en todos los canales; garantizar la entrega de ofertas compatibles |

## Prerrequisitos

Complete lo siguiente antes de comenzar la implementación.

- [ ] [!DNL AJO] zona protegida está aprovisionada con las capacidades de orquestación de recorrido y toma de decisiones habilitadas
- [ ] Todos los canales de destino (correo electrónico, SMS, push) tienen superficies de canal activas y verificadas
- [ ]: el esquema de perfil incluye los atributos necesarios para la toma de decisiones (nivel de lealtad, historial de compras, preferencias de canal y puntuaciones de participación)
- [ ] Se ha configurado la resolución de identidad en canales múltiples: los perfiles se pueden resolver en correos electrónicos, tokens push, números de teléfono e identificadores web
- [ ] La audiencia de entrada se ha definido y se está evaluando con una población distinta a cero
- [ ]: el contenido del catálogo de ofertas (recursos creativos, texto, exenciones de responsabilidad legal) está aprobado y listo para su configuración
- [ ] Se están ingiriendo datos de consentimiento y la aplicación del consentimiento está activa para todos los canales de destino
- [ Se diseñaron y aprobaron ] plantillas y fragmentos de contenido para cada canal
- [ ]: las reglas de restricción de frecuencia se definen e implementan si la organización tiene directivas de frecuencia entre campañas
- [ ] Si utiliza la toma de decisiones clasificadas por IA, existen un mínimo de 1000 eventos de conversión para la formación de modelos

## Opciones de implementación

Revise las siguientes opciones y seleccione el método que mejor se adapte a sus necesidades.

### Opción A: Recorrido con Offer Decisioning (canal fijo, contenido dinámico)

**Ideal para:** Recorridos en los que la secuencia de canal está predeterminada, pero el contenido u oferta de cada punto de contacto debe seleccionarse de forma dinámica: recorridos de fidelidad con recompensas personalizadas, renovación de la participación con incentivos dinámicos, nutrición del ciclo vital con recomendaciones de contenido clasificado por IA.

#### Cómo funciona

El lienzo de recorrido define la secuencia fija de canales y el tiempo (por ejemplo, Día 0: Correo electrónico, Día 3: Push, Día 7: SMS). En cada nodo de acción de mensaje, una política de decisión selecciona la mejor oferta o contenido para incluir en el mensaje desde un catálogo configurado de elementos aptos. Las ofertas se administran en el catálogo [!DNL AJO] Decisioning con reglas de aceptación que filtran las ofertas para las que cumple los requisitos de un perfil y estrategias de clasificación que determinan qué oferta elegible es la más adecuada.

Este enfoque separa el &quot;cuándo y dónde&quot; (orquestación de recorrido) del &quot;qué&quot; (toma de decisiones). El diseñador de recorridos controla el flujo de canal, mientras que el administrador de decisiones controla el catálogo de ofertas, las reglas de idoneidad y la lógica de clasificación de forma independiente. Esta separación de preocupaciones hace que la implementación sea más mantenible y permite que el catálogo de ofertas evolucione sin modificar el lienzo de recorrido.

Las ubicaciones de ofertas están incrustadas directamente en el contenido del mensaje mediante el correo electrónico Designer u otros editores de canal. Cuando el mensaje se procesa en el momento de la entrega, el motor de toma de decisiones evalúa la idoneidad y la clasificación del perfil para seleccionar la oferta óptima para cada ubicación en el mensaje.

#### Consideraciones clave

- La secuencia de canal es estática: todos los perfiles siguen la misma ruta de canal independientemente de sus preferencias
- La complejidad de la toma de decisiones es menor, ya que solo selecciona contenido/ofertas, no canales
- El catálogo de ofertas se puede administrar independientemente del recorrido
- Las ofertas de reserva deben configurarse para cada ubicación a fin de gestionar perfiles sin ofertas personalizadas aptas

#### Ventajas

- Lienzo de recorrido más sencillo: no hay lógica de ramificación para la selección de canales
- Clara separación de las preocupaciones entre el diseño del recorrido y la gestión de ofertas
- Más fácil de probar y validar: cada ruta de canal es determinística
- Menor complejidad de implementación y tiempo de comercialización más rápido
- Los cambios del catálogo de ofertas se aplican inmediatamente sin modificaciones del recorrido

#### Limitaciones

- No se puede adaptar el canal en función del comportamiento o las preferencias de perfil individuales
- Los perfiles que prefieren un canal sobre otro siguen recibiendo mensajes en los canales predeterminados
- No se optimiza para las tasas de participación a nivel de canal

#### Referencias de Experience League

- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)

### Opción B: Recorrido con selección de canal dinámico (contenido fijo, canal dinámico)

**Ideal para:** Recorridos donde el contenido en cada punto de contacto es similar, pero el canal debe seleccionarse dinámicamente en función del contexto del perfil: recuperación adaptable (correo electrónico frente a push frente a SMS en función de la participación), programas de acción óptima en los que la optimización de canal es el objetivo principal.

#### Cómo funciona

El recorrido utiliza nodos de condición basados en atributos de perfil (como puntuaciones de preferencia de canal, canal de última participación o estado de consentimiento) o salida de decisión para enrutar perfiles a diferentes rutas de canal. Cada ruta ofrece contenido específico del canal a través de su propio nodo de acción de mensaje. La lógica de toma de decisiones determina qué canal tiene más probabilidades de generar participación según el historial de comportamiento del perfil.

La selección de canales se puede implementar mediante nodos de condición de recorrido con evaluaciones de atributo de perfil (por ejemplo, si `channelPreference = "push"` se dirige a la ruta de inserción), o mediante la toma de decisiones con elementos específicos de canal en los que cada &quot;oferta&quot; representa un canal y la estrategia de clasificación determina el mejor canal.

Este método optimiza el canal de envío, a la vez que mantiene el contenido relativamente coherente en todos los canales. Requiere que se cree contenido de mensaje para cada canal posible y que se configuren las superficies de canal para todos los canales candidatos.

#### Consideraciones clave

- Requiere variantes de contenido de mensaje para cada canal candidato
- Las superficies de canal deben estar activas para todos los canales posibles
- La configuración de la lógica de condición o de toma de decisiones debe tener en cuenta el consentimiento: los perfiles sin consentimiento SMS no se pueden enrutar a la ruta SMS
- El lienzo de recorrido es más complejo con rutas ramificadas para cada canal

#### Ventajas

- Optimiza la selección de canales para cada perfil individual
- Aumenta la participación general al llegar a los perfiles de su canal preferido
- Respeta automáticamente el consentimiento específico del canal mediante el enrutamiento según el consentimiento
- Puede incorporar el historial de participación y las puntuaciones de preferencias de canal en las decisiones de enrutamiento

#### Limitaciones

- Lienzo de recorrido más complejo con varias ramas de canal
- El contenido debe crearse por separado para cada canal (aunque la intención del mensaje sea la misma)
- Difícil de probar: debe validar todas las rutas de canal posibles
- La personalización de contenido dentro de cada canal es estática (sin decisión de oferta)

#### Referencias de Experience League

- [Actividad de condición](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Creación de un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)

### Opción C: recorrido adaptable completo (canal dinámico + contenido dinámico)

**Mejor para:** Personalización máxima: tanto el canal como el contenido/oferta se seleccionan dinámicamente en cada nodo. Adecuado para segmentos de clientes de alto valor, programas de fidelidad sofisticados y organizaciones con prácticas de toma de decisiones maduras y datos de perfil enriquecidos.

#### Cómo funciona

Esta opción combina las opciones A y B. El recorrido utiliza la toma de decisiones en dos niveles: primero, para determinar qué canal utilizar para cada punto de contacto y, segundo, para determinar qué contenido u oferta enviar en el canal seleccionado. Cada punto de decisión del recorrido evalúa el contexto actual del perfil para realizar la selección de canal y contenido.

La implementación requiere una configuración completa de la toma de decisiones con políticas de decisión tanto para la selección de canales como para la selección de contenido/oferta. La selección del canal puede utilizar una política de decisión en la que cada elemento represente un canal con reglas de idoneidad basadas en el consentimiento y la participación, mientras que la selección de contenido utiliza una política de decisión independiente con elementos de oferta clasificados por relevancia.

Esta es la variante más compleja y requiere la integración más profunda entre la orquestación de recorrido y la toma de decisiones. Ofrece el mayor grado de personalización, pero también requiere la mayor cantidad de configuración, pruebas y administración continua.

#### Consideraciones clave

- Requiere dos niveles de toma de decisiones: selección de canal y selección de contenido
- La complejidad del lienzo de recorrido es mayor con la ramificación y la toma de decisiones anidadas en cada nodo
- Se requieren pruebas exhaustivas en todas las combinaciones posibles de contenido de canal
- Exige datos de perfil enriquecidos (historial de participación, preferencias de canal, afinidad de producto, puntuaciones de tendencia) para una toma de decisiones eficaz
- Las decisiones clasificadas por IA se benefician significativamente de los atributos calculados

#### Ventajas

- Máxima personalización: cada punto de contacto está optimizado para el canal y el contenido
- El mejor potencial de participación y conversión para implementaciones bien configuradas
- Centraliza toda la lógica de personalización en la toma de decisiones en lugar de ramas de recorrido estáticas
- Puede mejorar continuamente mediante el aprendizaje del modelo de clasificación de IA

#### Limitaciones

- Máxima complejidad de implementación y mayor tiempo de comercialización
- Requiere el catálogo de ofertas y la preparación de contenido de canal más completos
- Es más difícil solucionar problemas cuando surgen problemas de envío
- Exige una infraestructura de datos madura con atributos de perfil enriquecidos
- La clasificación de IA requiere un volumen de evento de conversión suficiente para la formación de modelos

#### Referencias de Experience League

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Comparación de opciones

Utilice la siguiente tabla para comparar las tres opciones de implementación de un vistazo.

| Criterios | Opción A: Offer Decisioning | Opción B: canal dinámico | Opción C: totalmente adaptable |
| --- | --- | --- | --- |
| Mejor para | Secuencia de canal fija, contenido dinámico | Optimización de canal, contenido coherente | Personalización máxima en ambas dimensiones |
| Complejidad | Medio | Medium-High | Alta |
| Lienzo del recorrido | Simple (lineal con nodos de toma de decisiones en acción) | Moderar (ramificación para rutas de canales) | Complejo (ramificación anidada con toma de decisiones en varios niveles) |
| Ámbito de decisión | Solo selección de contenido/oferta | Solo selección de canal | Selección de canal y de contenido |
| Requisitos de contenido | Un conjunto de contenido por canal (con ubicaciones de ofertas) | Contenido para cada canal candidato | Contenido con ubicaciones de ofertas para cada canal candidato |
| Necesidades de datos de perfil | Moderar (atributos de idoneidad de la oferta) | Moderar (preferencia de canal, participación) | Alto (atributos de canal y de oferta) |
| Tiempo de salida al mercado | Más rápido | Moderar | Más largo |
| Gestión continua | Administración del catálogo de ofertas | Administración de lógica de enrutamiento de canales | Tanto el catálogo de ofertas como el enrutamiento de canales |
| Profundidad de Personalization | El contenido varía, el canal está fijo | Canal variable, contenido similar | El canal y el contenido varían |

### Elija la opción correcta

Siga estas directrices para determinar la mejor opción para su situación.

- **Empiece con la opción A** si su estrategia de canal ya está definida (por ejemplo, &quot;siempre enviamos correo electrónico primero, luego push, luego SMS&quot;) y la necesidad de personalización principal es seleccionar la oferta o el contenido adecuado en cada punto de contacto. Este es el punto de partida más común para organizaciones nuevas en la toma de decisiones.

- **Elija la opción B** si la optimización de canales es su objetivo principal; desea llegar a cada cliente en el canal con el que es más probable que interactúe, pero el contenido del mensaje es relativamente coherente en todos los canales. Esto requiere datos de preferencias de canal en los perfiles.

- **Elija la opción C** solo cuando tenga una infraestructura de decisiones madura, datos de perfil enriquecidos (incluidos atributos calculados y puntuaciones de tendencia), un catálogo de ofertas bien completado y la capacidad organizativa para administrar la complejidad. Muchas organizaciones comienzan con la Opción A o B y evolucionan a la Opción C a medida que aumenta su madurez en la toma de decisiones.

- **Si no está seguro**, empiece con la Opción A. Ofrece una personalización significativa con la menor complejidad, y el catálogo de ofertas que cree para la opción A se puede reutilizar directamente si más adelante cambia a la opción C.

## Fases de implementación

Las siguientes fases recorren la implementación de extremo a extremo de este patrón de caso de uso.

### Fase 1: Evaluación de audiencias

**Función de aplicación:** [!DNL RT-CDP]: Evaluación de audiencia

Esta fase configura la audiencia de entrada que determina qué perfiles entran en el recorrido y cualquier segmento adicional utilizado para reglas de aceptación de ofertas o ramificación de condiciones dentro del recorrido. La definición de audiencia es la base de todo el recorrido descendente y la lógica de toma de decisiones.

#### Decisión: Tipo de entrada

¿Cómo deben entrar los perfiles en el recorrido, a través de una lectura de audiencia programada o un déclencheur de eventos en tiempo real?

>[!NOTE]
>Seleccione un tipo de entrada en función de los requisitos de activación y temporización del recorrido.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Leer audiencia (entrada por lotes) | Programas de ciclo vital, recorridos de fidelidad, campañas de renovación de participación programadas | Los perfiles se introducen por lotes en horas programadas; la audiencia se evalúa en tiempo de lectura; admite tamaños de audiencia grandes |
| Calificación de audiencias (streaming) | Recorridos activados por el comportamiento en los que la entrada debe producirse cuando un perfil entra o sale de un segmento | Entrada casi en tiempo real; requiere definición de segmento apta para streaming; buena para recorridos basados en hitos |
| Evento unitario (déclencheur de evento) | Un evento específico debe almacenar en déclencheur el recorrido (por ejemplo, compra, abandono del carro de compras, registro) | Entrada en tiempo real en evento; requiere configuración de esquema de evento; limitada a 5000 eventos/segundo |

#### Decisión: método de evaluación de audiencia

¿Con qué rapidez debe calificar la audiencia los perfiles?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Lote | Son suficientes las actualizaciones diarias o periódicas de la audiencia; recorridos programados de estilo de campaña | Procesos de hasta 24 millones de perfiles por trabajo; basados en programación; se admiten la mayoría de las expresiones de reglas de segmentos |
| Transmisión | La pertenencia a audiencias en tiempo real es necesaria para las entradas activadas por eventos o basadas en cualificaciones | Casi en tiempo real; conjunto de funciones de regla de segmento limitado; sin agregaciones basadas en el tiempo |
| Edge | Se necesita calificación de la misma sesión | Latencia de milisegundos; solo comprobaciones de atributos simples; limitada a atributos de perfil de Edge |

#### Detalles de configuración clave

**Navegación de la interfaz de usuario:** Cliente > Audiencias > Crear audiencia > Generar regla

- Defina la audiencia de entrada mediante el Generador de segmentos con expresiones de reglas de segmentos dirigidas a los atributos de perfil y eventos de comportamiento relevantes
- Cree segmentos de idoneidad adicionales si las reglas de idoneidad para la oferta hacen referencia a la pertenencia a segmentos (por ejemplo, &quot;Clientes de alto valor&quot;, &quot;Nivel Oro de fidelidad&quot;)
- Verifique que la población de audiencia no sea cero antes de continuar con la configuración del recorrido
- Seleccione la política de combinación que produce la vista de perfil unificada necesaria para la toma de decisiones

#### Documentación de Experience League

- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Fase 2: Configuración del canal

**Función de la aplicación:** [!DNL AJO]: Configuración del canal

Esta fase configura las superficies de canal para cada canal que el recorrido puede utilizar para la entrega de mensajes. Todos los canales candidatos deben tener superficies activas y verificadas antes de poder crear mensajes o publicar el recorrido. Para este patrón, normalmente configurará superficies para correo electrónico, SMS y push como mínimo, y potencialmente en la aplicación o web si la toma de decisiones puede seleccionar esos canales.

#### Decisión: qué canales configurar

¿Qué canales son candidatos para el recorrido, ya sea como pasos de recorrido fijos (Opciones A/B) o como canales seleccionables para la toma de decisiones (Opciones B/C)?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo correo electrónico | Recorrido de canal único con Offer Decisioning (opción A, solo correo electrónico) | Configuración más sencilla; requiere delegación de subdominios y calentamiento de IP |
| Correo electrónico + push | Recorrido de dos canales; común para recorridos centrados en la participación | La funcionalidad push requiere credenciales de APNS/FCM; la aplicación móvil debe estar integrada en SDK |
| Correo electrónico + SMS + push | Recorrido multicanal completo; el más común para las opciones B y C | SMS requiere credenciales de proveedor (Sinch, Twilio, Infobip); cada canal necesita su propia superficie |
| Correo electrónico + SMS + push + en la aplicación | Cobertura máxima del canal, incluidas las superficies de la sesión | La aplicación requiere una SDK móvil y una configuración de superficie de aplicación |

#### Decisión: método de delegación de subdominios (correo electrónico)

¿Cómo se debe delegar el subdominio de envío a Adobe?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Delegación completa | La organización desea que Adobe administre todos los registros DNS del subdominio de envío | Configuración más sencilla; Adobe gestiona SPF, DKIM y DMARC; menos control sobre DNS |
| Delegación CNAME | La organización necesita mantener el control de los registros DNS | Configuración más compleja; el cliente administra el DNS; proporciona más flexibilidad |

#### Detalles de configuración clave

**Navegación de interfaz de usuario:** Administración > Canales > Superficies de canal > Crear superficie

- Para el correo electrónico: configurar el subdominio, el grupo de IP, el nombre del remitente, la dirección de respuesta y la gestión de cancelación de suscripción
- Para SMS: configure las credenciales del proveedor de SMS y el número de remitente
- Para push: configurar APNS y credenciales de FCM para iOS y Android
- Compruebe que cada superficie está en estado Activo antes de continuar
- Se ha completado la preparación de IP para el envío de direcciones IP por correo electrónico

#### Documentación de Experience League

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Crear grupos de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fase 3: Configuración de decisiones

**Función de la aplicación:** [!DNL AJO]: Toma de decisiones

Esta fase configura el marco de decisión completo, incluidas las ubicaciones, las reglas de idoneidad, las ofertas personalizadas, las ofertas de reserva, los calificadores de recopilación, las colecciones, las estrategias de clasificación y las políticas de decisión. Esta fase crea la lógica de decisión que se invocará en los puntos de decisión de recorrido.

#### Decisión: ámbito de decisión

¿Qué debe seleccionar Decisioning: ofertas/contenido (Opción A), canales (Opción B) o ambos (Opción C)?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo selección de ofertas/contenido | La secuencia del canal es fija, la personalización está en el contenido | Las políticas de decisión dirigen los elementos de oferta con representaciones de contenido por ubicación |
| Solo selección de canal | El contenido es coherente; la optimización se realiza en el canal de envío | Los elementos de decisión representan canales; la idoneidad incluye comprobaciones de consentimiento; la clasificación utiliza datos de participación |
| Canal y contenido | Personalización adaptable completa en canales y contenido | Requiere dos capas de políticas de decisión; la personalización más compleja pero la más alta |

#### Decisión: Estrategia de clasificación

¿Cómo se deben clasificar las ofertas aptas para seleccionar la mejor?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Basado en prioridades (manual) | Clasificación simple donde las reglas comerciales determinan la importancia de la oferta | Cada oferta obtiene una puntuación de prioridad; la prioridad más alta gana; es determinista y fácil de entender |
| Basado en fórmulas (expresión personalizada) | La clasificación debe tener en cuenta los atributos del perfil (por ejemplo, CLV, nivel, puntuación de afinidad) | La fórmula de clasificación personalizada evalúa el contexto del perfil; es más dinámica que la prioridad; no se requiere ML |
| Clasificación de IA (optimización automática) | La clasificación debe optimizarse automáticamente en función de los datos de conversión históricos | El modelo de IA aprende de los eventos de conversión; requiere un mínimo de 1000 eventos para formación; mejora continuamente |

#### Decisión: Límite de oferta

¿Debería haber límites en cuanto a la cantidad de veces que se muestra una oferta?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Límite por perfil | Evitar que la misma oferta se muestre repetidamente al mismo perfil | Protege contra la fatiga de la oferta; es posible el retardo bajo un alto rendimiento |
| Límite global | Limitar el total de impresiones en todos los perfiles (por ejemplo, promociones de inventario limitadas) | Controla la exposición total; útil para ofertas de suministro limitado |
| Sin límite | Cada impresión elegible debe mostrar la oferta | Lo más sencillo; adecuado para contenido permanente u ofertas ilimitadas |

#### Detalles de configuración clave

**Navegación de la interfaz de usuario:** Componentes > Administración de decisiones > Ubicaciones / Ofertas / Decisiones

- Cree ubicaciones para cada combinación de canal y tipo de contenido (por ejemplo, banner de HTML de correo electrónico, JSON push, texto SMS)
- Defina reglas de aceptación mediante expresiones de reglas de segmentos que hagan referencia a atributos de perfil o a miembros de audiencia
- Cree ofertas personalizadas con representaciones para cada ubicación, asigne reglas de elegibilidad y establezca la prioridad
- Crear una oferta de reserva que cubra todas las ubicaciones: esto se devuelve cuando no se califica ninguna oferta personalizada
- Organización de ofertas en colecciones mediante calificadores de colección (etiquetas)
- Configurar la estrategia de clasificación: basada en prioridades, en fórmulas o en IA
- Cree políticas de decisión que enlacen ubicaciones, colecciones, estrategia de clasificación y ofertas de reserva
- Aprobar todas las ofertas antes de poder seleccionarlas mediante toma de decisiones

#### Dónde divergen las opciones

**Para la opción A (Offer Decisioning):**
Cree ubicaciones y ofertas centradas en la personalización de contenido dentro de cada canal (por ejemplo, ofertas de banner a pantalla completa de correo electrónico, ofertas de pie de página de correo electrónico, ofertas de cuerpo de notificación push). Las políticas de decisión seleccionan el mejor contenido para cada ubicación en el mensaje.

**Para La Opción B (Selección De Canal Dinámico):**
Cree elementos de decisión que representen cada canal. Las reglas de elegibilidad incluyen comprobaciones de consentimiento (por ejemplo, un perfil debe tener consentimiento SMS para poder optar al elemento SMS). La clasificación utiliza puntuaciones de participación del canal o expresiones basadas en fórmulas.

**Para Opción C (Adaptable Completo):**
Configure dos capas de toma de decisiones: un conjunto de políticas de decisión para la selección de canales y un conjunto independiente para la selección de contenido/oferta dentro del canal seleccionado. Ambas capas requieren ubicaciones, ofertas, reglas de elegibilidad y estrategias de clasificación.

#### Documentación de Experience League

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fase 4: Creación de mensajes

**Función de aplicación:** [!DNL AJO]: Creación de mensajes

Esta fase configura el contenido del mensaje para cada canal y punto de contacto del recorrido e integra la salida de toma de decisiones (contenido de oferta seleccionado) en las plantillas de mensajes. Cada nodo de acción de mensaje del recorrido requiere contenido creado con la superficie de canal adecuada, tokens de personalización e integraciones de ubicación de ofertas.

#### Decisión: enfoque del contenido

¿Cómo se debe crear el contenido del mensaje para cada canal?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Basado en plantillas | La organización ha establecido plantillas de marca; la coherencia es importante | Creación más rápida; garantiza la coherencia de la marca; puede limitar la flexibilidad del diseño |
| Diseñe desde cero | Creativo único para este recorrido; no hay plantillas existentes | Control de diseño completo, mayor tiempo de creación, uso de arrastrar y soltar de Email Designer |
| Importar HTML | El equipo de Creative produce HTML externamente; importe a [!DNL AJO] | Conserva el flujo de trabajo de diseño externo; requiere la compatibilidad de HTML con Email Designer |

#### Decisión: ámbito de Personalization

¿Qué nivel de personalización deben incluir los mensajes más allá de la salida de decisión?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Personalización básica (nombre, saludo) | Necesidades de personalización mínimas más allá de la selección de ofertas | Expresiones de Handlebars simples; baja complejidad |
| Bloques de contenido condicionales | Diferentes secciones de contenido para diferentes segmentos o atributos | Utiliza reglas de contenido dinámico; el contenido varía según el atributo del perfil o la pertenencia al segmento |
| Personalización completa con integración de decisiones | Ubicaciones de ofertas incrustadas en mensajes, combinadas con personalización basada en perfiles | Combina la salida de Offer Decisioning con tokens de personalización Handlebars; la experiencia más rica |

#### Detalles de configuración clave

**Navegación de la interfaz de usuario:** Seleccione la acción de campaña o del recorrido > Editar contenido > Enviar correo electrónico a Designer/Editor de canales

- Contenido de mensaje del autor para cada canal utilizado en el recorrido (correo electrónico, SMS, push, en la aplicación)
- Incrustar ubicaciones de decisiones de oferta en contenido de mensaje donde deben aparecer las ofertas seleccionadas para la toma de decisiones
- Agregue expresiones de personalización utilizando la sintaxis Handlebars para los atributos de perfil (por ejemplo, `{{profile.person.name.firstName}}`)
- Configurar bloques de contenido condicional para mensajes específicos de segmentos
- Crear fragmentos de contenido reutilizables para elementos compartidos (encabezados, pies de página, exenciones de responsabilidad legal)
- Previsualización y prueba con perfiles de muestra para verificar que la personalización se procese correctamente
- Enviar mensajes de prueba para revisión de partes interesadas

#### Dónde divergen las opciones

**Para la opción A (Offer Decisioning):**
Cada mensaje incluye ubicaciones de ofertas en las que aparece contenido seleccionado para la toma de decisiones. El diseño del mensaje es coherente, pero el área de oferta muestra dinámicamente la mejor oferta para cada perfil.

**Para La Opción B (Selección De Canal Dinámico):**
Cada canal tiene su propio contenido de mensaje creado por separado. El contenido es similar en todos los canales, pero se adapta a las restricciones de canal (correo electrónico, HTML frente a texto SMS frente al formato de notificaciones push).

**Para Opción C (Adaptable Completo):**
Cada canal tiene su propio contenido de mensaje con ubicaciones de ofertas incrustadas. Tanto el canal como el contenido de la oferta dentro de ese canal se seleccionan dinámicamente.

#### Documentación de Experience League

- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Creación de un mensaje SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Diseño de una notificación push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### Fase 5: Diseño y activación del Recorrido

**Función de aplicación:** [!DNL AJO]: Journey Orchestration, [!DNL AJO]: Administración de conflictos y prioridades, [!DNL AJO]: frecuencia y reglas de negocio

Esta fase configura el lienzo de recorrido completo, incluida la configuración de entrada, los nodos de decisión vinculados a las políticas de decisión configuradas, las divisiones de condición para el enrutamiento de canal (Opciones B/C), los nodos de acción de mensaje para cada ruta de canal, los nodos de espera entre puntos de contacto, los criterios de salida, la configuración de conflicto/prioridad y las reglas de límite de frecuencia. Esta fase monta todos los componentes configurados previamente en el flujo de recorrido orquestado y lo activa.

#### Decisión: política de reentrada

¿Pueden los perfiles volver a entrar en el recorrido después de completarse o salir?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Permitir la reentrada (con reutilización) | Recorridos recurrentes en los que los perfiles pueden volver a calificarse (por ejemplo, renovación de lealtad trimestral) | Establezca un período de reutilización (mínimo 5 minutos) para evitar la reentrada inmediata; el perfil se reinicia desde el principio |
| No hay reentrada | Recorridos únicos en los que cada perfil solo debe atravesar una vez (por ejemplo, la incorporación) | El perfil no puede volver a entrar tras la finalización o salida; comportamiento más sencillo |

#### Decisión: criterios de salida

¿En qué condiciones se debe eliminar un perfil de la recorrido antes de completarlo?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Cambio de pertenencia a audiencia | El perfil debe salir cuando abandone la audiencia de entrada o entre en una audiencia de supresión | Salida en tiempo real al cambiar de segmento; útil para salidas &quot;convertidas&quot; u &quot;excluidas&quot; |
| Ocurrencia del evento | Un evento específico (por ejemplo, compra, cancelación de suscripción) debe cerrar el déclencheur | Salida en tiempo real en evento; requiere la configuración del esquema de eventos |
| Tiempo de espera | Ha transcurrido la duración máxima en el recorrido | El valor máximo predeterminado es 91 días, lo que impide que los perfiles permanezcan indefinidamente |

#### Decisión: tiempo de espera de Recorrido

¿Cuál es la duración máxima que un perfil puede permanecer en el recorrido?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| 91 días (máximo) | Recorridos de ciclo vital de larga duración con secuencias de nutrición extendidas | Duración máxima permitida; los perfiles salen después de 91 días, independientemente |
| Duración personalizada más corta | Campañas con plazos específicos o recorridos de temporada | Se configura en función de la lógica empresarial del recorrido; un tiempo de espera más corto reduce los perfiles antiguos |

#### Decisión: configuración de conflicto y prioridad

¿Debe este recorrido tener una puntuación prioritaria para la resolución de conflictos con otros recorridos o campañas?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Alta prioridad (70-100) | Recorridos críticos del cliente (retención, lealtad) que deben tener prioridad | La prioridad más alta gana cuando varias comunicaciones compiten; utilice con moderación |
| Prioridad de Medium (30-69) | Recorridos de ciclo vital estándar | Prioridad equilibrada; se puede suprimir mediante comunicaciones de prioridad más alta |
| Prioridad baja (0-29) | Recorridos complementarios o informativos | Se suprimirá al competir con comunicaciones más importantes |

#### Detalles de configuración clave

**Navegación por la interfaz de usuario:** Recorrido > Crear Recorrido

- Cree el recorrido y configure las propiedades (nombre, descripción, zona horaria, tiempo de espera)
- Configuración de la entrada: Leer audiencia (para lote) o déclencheur de eventos (para tiempo real)
- Agregar nodos de decisión vinculados a las directivas de decisión configuradas de la fase 3
- Adición de divisiones de condición para el enrutamiento de canal en función de la salida de decisión o los atributos de perfil (Opciones B/C)
- Añada nodos de acción de mensaje para cada ruta de canal y vincúlelos al contenido creado desde la fase 4
- Agregar nodos de espera entre puntos de contacto (mínimo de 1 hora para recorridos de lectura de audiencia)
- Definir criterios de salida (cambio de audiencia, evento, tiempo de espera)
- Asignar puntuación de prioridad para la resolución de conflictos
- Configurar límite de frecuencia si se aplican límites de recorrido cruzado
- Pruebe el recorrido en modo de prueba con perfiles de prueba antes de publicar
- Publique el recorrido para activarlo

#### Dónde divergen las opciones

**Para la opción A (Offer Decisioning):**
El lienzo de recorrido es lineal con políticas de decisión incrustadas en cada nodo de acción de mensaje. No hay ramas para la selección de canales. La decisión de oferta se toma en el momento del procesamiento del mensaje dentro del nodo de acción.

**Para La Opción B (Selección De Canal Dinámico):**
Después de cada paso de espera, agregue un nodo de condición que evalúe los criterios de selección de canal (atributos de perfil, salida de decisión o estado de consentimiento). Cada rama de condición lleva a un nodo de acción de mensaje específico del canal. Incluya una ruta predeterminada para los perfiles que no coincidan con ninguna condición.

**Para Opción C (Adaptable Completo):**
Combine nodos de condición de selección de canal con nodos de acción de mensajes incrustados en directivas de decisión. At each touchpoint: primero, una condición o decisión determina el canal; luego, dentro de la acción de mensaje del canal seleccionado, una política de decisión selecciona la oferta/contenido óptimo.

#### Documentación de Experience League

- [Creación de un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propiedades del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Leer actividad de audiencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Actividad de condición](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Actividad Esperar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Añadir un mensaje en un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Criterios de salida](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [administración de entradas de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Prueba del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicación del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Resumen de administración de conflictos y prioridades](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### Fase 6: Creación de informes y supervisión

**Función de aplicación:** [!DNL AJO]: Informes y análisis de rendimiento

Esta fase configura la monitorización del rendimiento del recorrido y la toma de decisiones mediante informes en directo (durante la ejecución) e informes históricos (después de la finalización). Métricas específicas de la toma de decisiones, incluida la distribución de la selección de ofertas, las tasas de reserva y la eficacia de la clasificación. De forma opcional, CJA Workspace Analysis para el análisis profundo de recorridos entre canales y la toma de decisiones sobre el retorno de la inversión.

#### Decisión: profundidad del informe

¿Qué nivel de análisis de creación de informes se necesita?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo informes nativos de [!DNL AJO] | Monitorización operativa de las métricas de entrega y participación | Informes integrados activos e históricos; sin configuración adicional; limitados a [!DNL AJO] métricas |
| [!DNL AJO] + análisis de CJA | Análisis profundo en canales múltiples, efectividad en la toma de decisiones, ROI de recorrido, análisis de cohorte | Requiere conexión con CJA y vista de datos; proporciona funciones de atribución, funnel y análisis de cohorte |

#### Detalles de configuración clave

**Navegación de la interfaz de usuario:** Recorridos > Seleccionar recorrido > Informe en vivo / Informe de todo tiempo

- Monitorizar el informe de recorrido activo durante la ejecución inicial para las métricas de entrada, salida y por nodo
- Rendimiento de Review Decisioning: distribución de selección de ofertas, tasa de oferta de reserva, eficacia de clasificación
- Una vez finalizada la recorrido, revise los informes históricos para un análisis completo de funnel
- Para el análisis de CJA: asegúrese de que la conexión de CJA incluye [!DNL AJO] conjuntos de datos (evento de comentarios de mensajes, evento de seguimiento de correo electrónico)
- Cree CJA Workspace con paneles para el análisis de mezcla de canales, la comparación de rendimiento de ofertas y los canales de conversión de recorridos
- Crear anotaciones para las fechas de inicio del recorrido y los cambios de configuración significativos

#### Documentación de Experience League

- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Consideraciones sobre la implementación

Revise las siguientes barreras, escollos comunes, prácticas recomendadas y decisiones de compensación antes y durante la implementación.

### Protecciones y límites

- Máximo de 500 recorridos activos por zona protegida — [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- La duración máxima del recorrido es de 91 días (tiempo de espera global)
- Máximo de 50 actividades por lienzo de recorrido
- Leer Los recorridos de audiencia pueden procesar hasta 20 000 perfiles por segundo
- Los recorridos de eventos unitarios admiten hasta 5000 eventos por segundo por zona protegida
- Máximo de 10 000 ofertas personalizadas aprobadas por zona protegida
- Máximo de 30 colocaciones por decisión
- Tiempo de respuesta de entrega de la oferta SLA: menos de 500 ms a P95 para solicitudes de un solo ámbito
- Los modelos de clasificación de IA requieren un mínimo de 1000 eventos de conversión para la formación.
- Máximo de 10 superficies de canal por tipo de canal y zona protegida
- Los pasos de espera tienen una duración mínima de 1 hora para los recorridos de lectura de audiencia
- El tiempo mínimo de reutilización de la reentrada al recorrido es de 5 minutos
- Máximo de 4000 definiciones de segmento por zona protegida — [Protecciones de plataforma](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

### Peligros comunes

**La decisión siempre devuelve la oferta de reserva:** Compruebe que las ofertas personalizadas estén aprobadas (no en estado de borrador), dentro de su intervalo de fechas de validez y que las reglas de elegibilidad coincidan con los atributos de los perfiles de destinatario. Compruebe que no se han alcanzado los límites de límite de ofertas. Realice pruebas con un perfil que claramente deba cumplir los requisitos para una oferta personalizada.

**El Recorrido se publica pero los perfiles no están entrando:** Para los recorridos leídos por la audiencia, confirme que la audiencia tiene una población evaluada mayor que cero. En el caso de los recorridos activados por eventos, compruebe el esquema de eventos, las condiciones de activación y que se están enviando eventos. Compruebe que la política de combinación de audiencias de entrada coincide con la política de combinación esperada del recorrido.

**La fórmula de clasificación no se ha aplicado correctamente:** Compruebe que la sintaxis de la fórmula es válida y hace referencia a atributos de perfil accesibles. Los errores de fórmula vuelven silenciosamente a la clasificación basada en prioridades sin previo aviso. La clasificación de prueba con perfiles que tienen diferentes valores de atributo para confirmar que la fórmula produce el orden esperado.

**El enrutamiento de canal ignora el consentimiento:** Los nodos de condición para la selección de canales deben incluir comprobaciones de consentimiento. Un perfil sin consentimiento SMS no debe enrutarse a la ruta SMS. Incorporar el consentimiento en las reglas de idoneidad al utilizar la toma de decisiones para la selección de canales (Opción B/C).

**Los contadores de límite de ofertas se quedan rezagados en un rendimiento alto:** Los contadores de límite de ofertas pueden tener un retraso de unos segundos en escenarios de rendimiento alto. Si el límite exacto es crítico, utilice límites globales con un búfer o combine con reglas de frecuencia.

**El lienzo de Recorrido sobrepasa el límite de 50 actividades:** Los recorridos complejos de la opción C con muchas ramas de canal y nodos de decisión pueden acercarse al límite de 50 actividades. Simplifique consolidando la lógica de condición, reduciendo el número de puntos de contacto o dividiéndola en varios recorridos secuenciales.

**Las decisiones de Edge devuelven personalización vacía:** Si usa la toma de decisiones perimetral para decisiones en tiempo real, asegúrese de que la secuencia de datos tenga habilitado el servicio [!DNL Adobe Journey Optimizer] y de que el ámbito de decisión tenga el formato correcto. Las decisiones de Edge se limitan a atributos de perfil disponibles en el almacén de perfiles Edge.

### Prácticas recomendadas

**Empiece simple y evolucione:** Empiece con la opción A (canal fijo, ofertas dinámicas) para validar el marco de toma de decisiones y, a continuación, evolucione a las opciones B o C a medida que aumente la madurez de los datos y la capacidad organizativa.

**Invierta en el enriquecimiento de perfiles:** Los atributos calculados, como las puntuaciones de participación, los índices de preferencias de canal y las puntuaciones de tendencia de inteligencia artificial aplicada al cliente, mejoran considerablemente la calidad de las decisiones. Genere estos atributos de enriquecimiento antes de configurar estrategias de clasificación complejas.

**Configurar siempre ofertas de reserva:** Cada directiva de decisión debe tener una oferta de reserva. Diseñe ofertas de reserva como contenido realmente valioso (no como marcadores de posición vacíos), ya que sirven a perfiles que no cumplen los requisitos para ninguna oferta personalizada.

**Prueba con diversos perfiles:** Usa el modo de prueba con perfiles que representen diferentes rutas de elegibilidad, preferencias de canal y combinaciones de atributos. Compruebe que cada posible ruta de recorrido y resultado de la toma de decisiones funciona correctamente antes de publicar.

**Monitorizar tasas de reserva como métrica de estado:** Una tasa de oferta de reserva alta indica que las reglas de elegibilidad son demasiado restrictivas o que el catálogo de ofertas no cubre suficientes segmentos de perfil. Establezca una tasa de reserva por debajo del 20 % para las decisiones bien configuradas.

**Use fragmentos de contenido para lograr la coherencia en canales múltiples:** Cree fragmentos de contenido compartido (encabezados, pies de página, exenciones de responsabilidad legales, bloques para cancelar la suscripción) para mantener la coherencia de la marca en el correo electrónico, los SMS y los mensajes push dentro del recorrido.

**Configurar criterios de salida de forma proactiva:** Defina criterios de salida para los eventos de conversión (por ejemplo, compras o registros) de modo que los perfiles que completen la acción deseada se eliminen de la recorrido inmediatamente en lugar de seguir recibiendo mensajes.

**Asignar puntuaciones de prioridad significativas:** Cuando ejecute varios recorridos y campañas, asigne puntuaciones de prioridad en función del impacto en la empresa. Los recorridos de retención de alto valor deben tener mayor prioridad que las comunicaciones informativas.

### Decisiones de compensación

Revise las siguientes compensaciones para informar las opciones de implementación.

#### Complejidad de la toma de decisiones frente al tiempo de salida al mercado

Una toma de decisiones más sofisticada (opción C con clasificación de IA) ofrece una mayor personalización, pero requiere una configuración, preparación de datos y tiempo de prueba significativamente mayores.

- **La opción A/B favorece:** implementación más rápida, pruebas más sencillas, reducción de la sobrecarga de administración continua
- **La opción C favorece:** Personalización máxima, optimización continua impulsada por IA, mayor potencial de participación
- **Recomendación:** Comience con la opción A o B para el primer inicio. Recopile datos de rendimiento y cree atributos de enriquecimiento de perfil en paralelo. Cambie a la opción C cuando tenga al menos 1000 eventos de conversión para la formación en clasificación de IA y un catálogo de ofertas bien rellenado.

#### Bifurcación estática frente a toma de decisiones para la selección de canales

La selección de canales se puede implementar mediante nodos de condición de recorrido simples (evaluando directamente los atributos de perfil) o a través del marco de toma de decisiones (donde los canales se modelan como elementos de decisión con elegibilidad y clasificación).

- **Los nodos de condición estática favorecen:** Simplicidad, transparencia, fácil solución de problemas. Es mejor cuando la lógica de selección de canales es sencilla (por ejemplo, si existe un token push y la última apertura push se realiza en un plazo de 30 días, utilice push; de lo contrario, envíe un correo electrónico).
- La selección de canales basada en **decisiones favorece:** Administración centralizada, potencial de optimización de IA, capacidad para evolucionar la lógica de clasificación sin modificar el lienzo de recorrido. Es mejor cuando la selección de canales es compleja y debe mejorar con el tiempo.
- **Recomendación:** Use nodos de condición estática para la opción B cuando los criterios de selección de canal sean simples y estén bien definidos. Utilice la selección de canales basada en decisiones cuando desee que la IA optimice la selección de canales con el paso del tiempo o cuando la lógica de selección de canales sea lo suficientemente compleja como para beneficiarse de la administración centralizada de elegibilidad y clasificación.

#### Granularidad de ofertas frente a administración de catálogos

Un catálogo de ofertas grande y granular con muchas ofertas segmentadas produce una personalización más precisa, pero requiere más esfuerzo de administración. Un catálogo más pequeño con una idoneidad más amplia es más fácil de administrar, pero menos personalizado.

- **Favoritos de catálogo grande (muchas ofertas específicas):** mayor precisión de personalización, selecciones más relevantes para diversas audiencias y tasas de reserva más bajas
- **Favoritos de catálogo pequeño (menos ofertas amplias):** Administración más sencilla, configuración más rápida, pruebas más sencillas y menor riesgo de ofertas huérfanas
- **Recomendación:** Comience con 5-15 ofertas personalizadas más una reserva por decisión. Añada más ofertas a medida que observa qué segmentos reciben ofertas de reserva con mayor frecuencia. Use calificadores de recopilación para organizar ofertas por categoría, nivel o línea de producto para un crecimiento manejable.

#### Decisiones basadas en prioridades frente a decisiones clasificadas por IA

La clasificación basada en prioridades es determinista y transparente. La toma de decisiones por clasificación de IA se optimiza automáticamente, pero requiere datos de formación y es menos transparente.

- **Favoritos de clasificación basados en prioridad:** Previsibilidad, transparencia, implementación inmediata, sin requisito de datos de capacitación
- **Favoritos de la toma de decisiones con clasificación de IA:** Optimización continua, selección basada en datos, capacidad para descubrir afinidades no obvias entre perfiles de oferta
- **Recomendación:** Use la clasificación basada en prioridades o en fórmulas para la implementación inicial. La transición a la toma de decisiones clasificadas por IA se produce una vez que haya acumulado al menos 1000 eventos de conversión y desee pasar de la optimización basada en reglas a la basada en modelos.

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las capacidades utilizadas en este patrón de caso de uso.

### orquestación de recorrido

- [Introducción a recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Creación de un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propiedades del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Leer actividad de audiencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Eventos generales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de calificación de público](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Actividad de condición](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Actividad Esperar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Añadir un mensaje en un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Criterios de salida](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [administración de entradas de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Prueba del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicación del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### Administración de decisiones

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear calificadores de colección](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Crear grupos de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [planes de calentamiento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configuración de superficie de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Creación y personalización de mensajes

- [Crear un correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Administración de conflictos, prioridades y frecuencias

- [Resumen de administración de conflictos y prioridades](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificación de posibles conflictos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [restricción y arbitraje de recorridos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Composición de audiencia](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Informes y análisis

- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### Perfil e identidad

- [Resumen del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Información general sobre Customer AI](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Gobernanza de datos y consentimiento

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Administrar lista de supresión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones del servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
