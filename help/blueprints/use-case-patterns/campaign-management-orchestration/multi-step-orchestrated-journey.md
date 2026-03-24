---
title: Recorrido orquestado de varios pasos
description: Aprenda a guiar un perfil a través de un recorrido ramificado y multitáctil con esperas, condiciones y varias acciones de mensaje a lo largo del tiempo.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 5667b188-1b20-4a85-aebb-74efd5f771a1
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8211'
ht-degree: 1%

---

# Recorrido orquestado de varios pasos

Esta guía proporciona un modelo de implementación completo para crear recorridos organizados de varios pasos con [!DNL Adobe Journey Optimizer] (AJO) y [!DNL Real-Time Customer Data Platform] (RT-CDP). Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesitan orquestar recorridos de clientes multitáctiles y ramificados que entreguen varios mensajes a lo largo del tiempo.

Presenta todas las opciones de implementación viables, consideraciones de decisión en cada punto de configuración y vínculos a la documentación de [!DNL Adobe Experience League]. Utilice esta guía para planificar, configurar y validar su implementación de recorrido de varios pasos.

## Resumen del caso de uso

Los recorridos organizados en varios pasos se dirigen a escenarios comerciales en los que un solo mensaje es insuficiente para lograr el resultado deseado del cliente. En lugar de un envío único, el recorrido guía a cada perfil a través de una secuencia de puntos de contacto (correos electrónicos, mensajes SMS, notificaciones push o mensajes en la aplicación) espaciados entre días o semanas, con una lógica de ramificación que adapta la ruta en función de atributos de perfil, señales de comportamiento o datos de evento.

Estos recorridos son el patrón de campaña más complejo de AJO. Combinan entradas basadas en audiencias o en eventos con un lienzo de nodos de acción (mensajes), nodos de condición (lógica de ramificación), nodos de espera (retrasos de tiempo) y criterios de salida (eventos de conversión o tiempos de espera). Cada perfil progresa a través del recorrido de forma independiente, a su propio ritmo, recibiendo contenido relevante contextualmente en cada paso.

Este patrón subsume los patrones más simples: activación de mensajes salientes por lotes para campañas de un solo envío y mensajería activada por eventos para respuestas de un solo evento. Utilice este patrón cuando el caso de uso requiera alimentar un perfil a través de varias interacciones a lo largo del tiempo.

>[!NOTE]
>Si su recorrido requiere una selección dinámica de la oferta, el contenido o el canal óptimos en puntos de decisión individuales, consulte [recorrido en canales múltiples con toma de decisiones](cross-channel-journey-with-decisioning.md). Ese patrón amplía este con la integración de AJO Decisioning.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Mejorar la retención de clientes

Mantenga el compromiso de los clientes existentes y renuévelos mediante experiencias basadas en valores y una nutrición continua de las relaciones.

**KPI:** retención, valor de duración del cliente, participación

[Más información sobre la mejora de la retención de clientes](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### Mejore la incorporación del cliente

Acelere el tiempo de respuesta al valor para los nuevos clientes con experiencias de bienvenida y recorridos de activación optimizados y personalizados.

**KPI:** participación, retención, tasas de conversión

[Más información sobre la mejora de la incorporación del cliente](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)

### Reactivar clientes inactivos

Recupere clientes inactivos o caducados con campañas de reactivación dirigidas basadas en señales de comportamiento.

**KPI:** participación, retención, tasas de conversión

[Más información sobre la mejora de la retención de clientes](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### Recuperar carros y recorridos abandonados

Vuelva a atraer a los usuarios que abandonaron durante los flujos de compra, solicitud o inscripción con seguimientos personalizados y oportunos.

**KPI:** tasas de conversión, ingresos incrementales, participación

[Más información sobre la recuperación de carros de compras y recorridos abandonados](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran aplicaciones comunes del patrón de recorrido orquestado de varios pasos.

- **Serie de incorporación del cliente**: correo electrónico de bienvenida, seguido de educación sobre las funciones y un mensaje de activación durante los primeros 14 días posteriores al registro
- **Campaña de goteo de renovación de participación**: un correo electrónico recordatorio, una oferta de incentivo y un aviso final para los clientes caducados durante 3 semanas.
- **recorrido de hito de fidelización**: notificación de actualización de nivel, seguida de una oferta exclusiva y, a continuación, un recordatorio de renovación conforme se acerca el aniversario de la pertenencia
- **Secuencia de recuperación**: correo electrónico de &quot;Te echamos de menos&quot;, después una oferta de descuento por correo electrónico y, por último, un recordatorio SMS para los compradores que hayan caducado
- **recorrido de adopción de productos**: bienvenida de prueba, sugerencias de uso y solicitud de actualización a medida que avance el período de prueba
- **Secuencia de renovación de suscripción**: aviso con 30 días de antelación, recordatorio de 7 días y un mensaje de día de caducidad para próximas renovaciones de suscripción
- **Servicio poscompra**: correo electrónico de agradecimiento, guía de uso, recomendación de venta cruzada y solicitud de revisión más de 30 días después de la compra

## Indicadores clave de rendimiento

Utilice los siguientes KPI para medir la eficacia de la implementación de recorridos organizados en varios pasos.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de finalización de recorridos | Porcentaje de perfiles que completan el recorrido completo sin una salida anticipada | Informe de recorrido: Salido (completado) / Ingresado |
| Tasa de conversión de etapas | Porcentaje de perfiles que progresan de un paso al siguiente | Métricas por nodo en el informe de recorrido |
| Tasa de participación en canal | Tasas de apertura, tasas de pulsaciones y tasas de respuesta en cada punto de contacto | Métricas de envío y participación por mensaje |
| Tasa de conversión de criterios de salida | Porcentaje de perfiles que almacenan en déclencheur el evento de salida (por ejemplo, compra, registro) antes del tiempo de espera de recorrido | Recuento de visitas de criterios de salida/Total introducido |
| Tiempo de conversión | Duración media desde la entrada de recorrido hasta el evento de criterios de salida | Recorrido analytics: marca de tiempo de entrada a la marca de tiempo del evento de conversión |
| Tasa de entrega de recorridos | Porcentaje de perfiles que dejan de interactuar en cada paso (análisis de abandonos) | Visualización de abandonos de CJA en varios pasos del recorrido |
| Tasa de retención/renovación de la participación | Porcentaje de perfiles objetivo que vuelven al estado activo | Análisis de comportamiento posterior al recorrido en CJA |

## Patrón de caso de uso

**Recorrido orquestado de varios pasos**

Guía de un perfil a través de un recorrido ramificado y multitáctil con esperas, condiciones y varias acciones de mensaje a lo largo del tiempo.

**Cadena de funciones:** Evaluación de audiencias > Ejecución de Recorridos (varios nodos) > Bifurcación de condiciones > Entrega de mensajes (xN) > Criterios de salida > Informes

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón de caso de uso.

- **[!DNL Adobe Journey Optimizer](AJO)**: motor de orquestación de Recorrido, creación de mensajes, configuración de canal, experimentación de contenido, administración de frecuencia y conflictos y sistema de informes
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)**: evaluación y definición de audiencias para audiencias de entrada de recorrido, datos de perfil para personalización y bifurcación de condiciones
- **[!DNL Adobe Experience Platform](AEP)**: almacén de perfiles, servicio de identidad, ingesta de datos de evento e infraestructura de datos básica

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Se asume en contexto | Zona protegida de AJO con permisos de creación y publicación de recorrido. Se deben configurar las superficies de canal para todos los canales utilizados en el recorrido. Los usuarios deben tener las funciones adecuadas (experto en marketing, administrador de Recorridos) con permisos de recorrido y campaña. | [Resumen de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home), [Resumen de control de acceso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | Esquema de perfil XDM con atributos utilizados para la bifurcación de condiciones y la personalización en varios mensajes (por ejemplo, nivel de lealtad, interés del producto, puntuación de participación). Esquemas de eventos de experiencia para eventos de conversión que impulsan los criterios de salida y la evaluación de condiciones (por ejemplo, eventos de compra y envíos de formularios). | [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [Conceptos básicos de composición de esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Fuentes de datos y recopilación | Se asume en contexto | La transmisión de eventos debe estar activa si los criterios o las condiciones de salida dependen de eventos en tiempo real (por ejemplo, un evento de compra para salir del recorrido). Ingesta por lotes de atributos de perfil utilizados en ramificaciones. SDK web o API del lado del servidor para la recopilación de eventos de comportamiento. | [Resumen de ingesta de transmisión](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview), [Resumen de fuentes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| Configuración de identidad y perfil | Se asume en contexto | Los perfiles deben poder resolverse en todos los canales utilizados en la recorrido (correo electrónico, SMS, push). La identidad entre dispositivos debe configurarse si el recorrido abarca puntos de contacto web y móviles. La política de combinación debe configurarse para la zona protegida. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Introducción a las políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Definición de audiencia y segmentación | Requerido | La audiencia de entrada debe definirse para los recorridos de lectura de audiencia. Los segmentos también se pueden utilizar en nodos de condición para la ramificación. El método de evaluación (por lotes o streaming) debe coincidir con los requisitos de entrada de recorrido. | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Guía de la interfaz de usuario del generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Los atributos calculados, como las puntuaciones de participación, los días transcurridos desde la última actividad o el valor de compra de duración, mejoran la lógica de ramificación de condiciones, lo que permite decisiones más inteligentes sobre la ruta de recorrido. | [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Administración del ciclo de datos | Recomendado | La retención de datos de evento de recorrido debe configurarse con políticas de caducidad de conjuntos de datos para administrar el almacenamiento y cumplir con las regulaciones de retención de datos. La aplicación del consentimiento garantiza que solo los perfiles seleccionados reciban mensajes en cada punto de contacto de canal. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Caducidad de conjuntos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| Etiquetado y aplicación del uso de datos | Recomendado | Las etiquetas de gobernanza garantizan una personalización compatible en varios puntos de contacto de mensajes, lo que es especialmente importante cuando los recorridos utilizan PII o datos confidenciales para la personalización en todos los canales. | [Resumen de control de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Resumen de etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview) |
| Monitorización y observabilidad | Incluido | supervisión de la ejecución de recorridos alertas sobre errores de procesamiento, cuellos de botella de entrada de perfil y problemas de entrega. Esencial para recorridos de producción en los que los retrasos o errores afectan a la experiencia del cliente. | [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Informes y análisis | Incluido | CJA funnel y el análisis de abandonos en todo el recorrido proporcionan una insight más profunda que los informes nativos de AJO por sí solos. Permite realizar análisis de conversión paso a paso, comparar cohortes y optimizar recorridos. | [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del Catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Journey Optimizer] (AJO)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Configuración de canal | Fase 1: Configuración del canal | Configuración de superficies de canal (correo electrónico, SMS, push) para cada punto de contacto de mensajería en el recorrido |
| Creación de mensajes | Fase 2: Creación de contenido de mensaje | Creación de contenido de mensaje con personalización, contenido dinámico y plantillas para cada nodo de acción de recorrido |
| Journey Orchestration | Fase 3: Diseño y activación del Recorrido | Diseñar el lienzo de recorrido de varios pasos con nodos de entrada, acción, condición, espera y salida; probar y publicar |
| Frecuencia y reglas comerciales | Fase 4: Gobernanza y optimización | Configure límites de frecuencia para evitar mensajes excesivos en puntos de contacto de recorrido y otras campañas simultáneas |
| Administración de conflictos y prioridades | Fase 4: Gobernanza y optimización | Asignar puntuaciones de prioridad y configurar la detección de recorridos que compitan con otras comunicaciones activas |
| Experimentación de contenido | Fase 4: Gobernanza y optimización | Ejecute pruebas A/B en el contenido del mensaje dentro de los nodos de acción del recorrido para optimizar el rendimiento |
| Informes y análisis de rendimiento | Fase 5: Informes y monitorización | Monitorice la ejecución del recorrido, las métricas de entrega por paso y el rendimiento de la participación |

### [!DNL Real-Time CDP] (RT-CDP)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Evaluación de audiencia | Fase 1: Configuración del canal (requisito previo) | Defina y evalúe la audiencia de entrada para recorridos de lectura de audiencia; defina audiencias de condición para ramificación |
| Cumplimiento del consentimiento y la gobernanza | Fase 4: Gobernanza y optimización | Aplicar preferencias de consentimiento y políticas de uso de datos en las acciones de mensajes de recorrido |

## Prerrequisitos

Complete los siguientes requisitos previos antes de comenzar la implementación.

- [ ] La zona protegida de AJO está aprovisionada con permisos de creación y publicación de recorrido
- [ ]: Al menos una superficie de canal (correo electrónico, SMS o push) está configurada y activa
- [ ] El esquema de perfil incluye atributos necesarios para la bifurcación y personalización de condiciones
- [ El esquema de evento de experiencia ] está configurado para eventos de conversión utilizados en criterios de salida
- [ ] El streaming de eventos está activo para los eventos en tiempo real que se usan en los criterios de salida o en las entradas activadas por eventos
- [ ]: las áreas de nombres de identidad y las políticas de combinación están configuradas para la resolución de perfiles en canales múltiples
- [ ] Los recursos de contenido (imágenes, copias, CTA) se preparan para cada punto de contacto de mensaje
- [ ] La audiencia de entrada se ha definido y evaluado (para recorridos de lectura de audiencia)
- [ ] El esquema de eventos de activación está configurado (para recorridos activados por eventos)
- [ ] perfiles de prueba están disponibles para la validación del modo de prueba de recorrido
- [ ]: la lista de supresión se ha revisado y actualizado para todos los canales utilizados

## Opciones de implementación

Revise las siguientes opciones para determinar el mejor enfoque para su recorrido orquestado de varios pasos.

### Opción A: recorrido orquestado de lectura de audiencia

**Mejor para:** Secuencias de aprendizaje basadas en el tiempo en las que una audiencia conocida entra en el recorrido y progresa a través de puntos de contacto programados: series de incorporación, secuencias de renovación, goteos de renovación de participación, recorridos de hito de lealtad.

**Cómo funciona:**

Una audiencia se lee en la entrada de recorrido, ya sea como una lectura única o en una programación recurrente. Todos los perfiles aptos entran en el recorrido simultáneamente y luego progresan a través del lienzo a su propio ritmo, regido por duraciones de espera y evaluaciones de condición. La ruta de cada perfil a través del recorrido es independiente: algunos pueden tomar la rama &quot;comprometida&quot;, mientras que otros toman la rama &quot;no comprometida&quot; en función de su comportamiento o atributos.

La audiencia se evalúa en el momento en que se ejecuta la actividad Leer audiencia. En el caso de los recorridos recurrentes, la audiencia se reevalúa en cada recurrencia y los nuevos perfiles cualificados entran en el recorrido mientras los perfiles que ya están en el recorrido continúan su ruta. Este método proporciona un tiempo de entrada predecible y es adecuado para programas de ciclo de vida programados.

**Consideraciones clave:**

- La audiencia debe definirse y evaluarse antes de la activación del recorrido
- La lectura recurrente permite introducir nuevos cualificadores en cada ciclo
- Los perfiles del recorrido no se vuelven a leer; solo los calificadores nuevos se introducen en lecturas posteriores
- Los pasos de espera tienen una duración mínima de 1 hora para los recorridos de lectura de audiencia

**Ventajas:**

- Horario de entrada predecible alineado con los horarios comerciales
- Admite grandes volúmenes de audiencia (hasta 20 000 perfiles por segundo acelerador predeterminado)
- Fácil de probar y supervisar con poblaciones de audiencia conocidas
- Se puede programar para entradas recurrentes (diarias, semanales, mensuales)

**Limitaciones:**

- La entrada se basa en lotes, no en tiempo real: los perfiles se introducen en el momento de lectura programado, no cuando cumplen los requisitos
- No es adecuado para secuencias iniciadas por el comportamiento que requieran respuesta inmediata
- Los cambios de audiencia entre lecturas no se reflejan para perfiles que ya están en el recorrido

**Experience League:**

- [Leer actividad de audiencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Creación de un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)

### Opción B: recorrido orquestado activado por eventos

**Mejor para:** Secuencias iniciadas por el comportamiento en las que un evento en tiempo real inicia el recorrido: escalación de abandono del carro de compras, nutrición posterior a la compra, recorrido de lealtad activado por hitos y secuencias de activación de prueba.

**Cómo funciona:**

Un evento unitario (por ejemplo, una compra, el abandono del carro de compras, el envío de formularios o la instalación de una aplicación) déclencheur la entrada de recorrido para perfiles individuales en tiempo real. Cuando se recibe el evento, el perfil entra en el recorrido y luego progresa a través de la secuencia de puntos de contacto con condiciones, esperas y ramas. Este método combina la inmediatez de la mensajería activada por eventos con la organización en varios pasos de un recorrido completo.

El evento de activación debe configurarse como un evento de recorrido con su esquema y condiciones definidos. El recorrido escucha el evento continuamente e introduce los perfiles de uno en uno a medida que llegan los eventos. Los nodos de recorrido posteriores pueden evaluar la respuesta del perfil para determinar qué rama seguir.

**Consideraciones clave:**

- Requiere flujo de eventos en tiempo real para estar activo
- El esquema y las condiciones de evento deben configurarse con precisión para evitar déclencheur falsos
- Las reglas de reentrada son críticas: determine si un perfil puede volver a entrar si el evento se activa de nuevo
- Admite hasta 5000 eventos por segundo por zona protegida

**Ventajas:**

- Entrada en tiempo real basada en el comportamiento del cliente: altamente contextual
- Cada perfil introduce de forma independiente cuando se produce el evento, no en una programación
- Ajuste natural para secuencias de respuesta de comportamiento (abandono del carro de compras, poscompra)
- Se puede combinar con datos de perfil para ramas personalizadas después de la entrada

**Limitaciones:**

- Requiere que la infraestructura de eventos de streaming esté implementada
- Mayor complejidad en la configuración y prueba de esquemas de eventos
- Cada evento introduce un perfil, que no es adecuado para la activación de audiencias en lote
- La depuración requiere el seguimiento de recorridos de perfil individuales

**Experience League:**

- [Eventos generales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de calificación de público](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)

### Opción C: recorrido orquestado multicanal

**Ideal para:** secuencias en canales múltiples que usan diferentes canales en cada punto de contacto: correo electrónico, SMS, escalación push o correo electrónico, además de mensajería complementaria en la aplicación. Puede utilizar una entrada leída por la audiencia o activada por un evento.

**Cómo funciona:**

Esta opción amplía la opción A o la opción B al incorporar varios canales de mensajería dentro del mismo recorrido. Cada nodo de acción del recorrido puede dirigirse a un canal diferente (correo electrónico, SMS, push, en la aplicación o web), que requiere una superficie de canal independiente para cada uno. El diseñador de recorridos selecciona el canal adecuado en cada paso y habilita patrones de escalación (por ejemplo, correo electrónico primero y SMS si no hay participación) o patrones complementarios (por ejemplo, correo electrónico con refuerzo en la aplicación).

Los recorridos entre canales requieren superficies de canal para cada canal utilizado y deben tener en cuenta la personalización, los límites de caracteres y los requisitos de inclusión específicos del canal. Los nodos de condición pueden comprobar la participación con mensajes anteriores (por ejemplo, &quot;¿correo electrónico abierto?&quot; como condición de rama) para determinar el canal siguiente.

**Consideraciones clave:**

- Requiere superficies de canal activas para cada canal utilizado en el recorrido
- Cada canal tiene diferentes capacidades de personalización y restricciones de contenido
- El consentimiento debe verificarse por canal: se puede activar un perfil para el correo electrónico, pero no para los SMS
- Los límites de frecuencia específicos del canal deben configurarse para evitar el exceso de mensajes entre canales

**Ventajas:**

- Maximiza el alcance al atraer perfiles en sus canales preferidos
- Habilita estrategias de escalación para perfiles no adaptables
- Admite mensajes complementarios entre canales para refuerzo
- La experiencia del cliente más sofisticada posible

**Limitaciones:**

- Mayor complejidad de implementación: requiere configuración para cada canal
- El contenido debe crearse para cada canal en cada punto de contacto
- La administración de consentimiento y frecuencia se vuelve más compleja entre canales
- Las pruebas requieren validación en todas las superficies de canal

**Experience League:**

- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Comparación de opciones

En la tabla siguiente se comparan las tres opciones de implementación en función de criterios clave.

| Criterios | Opción A: Lectura de audiencia | Opción B: activado por evento | Opción C: multicanal |
| --- | --- | --- | --- |
| Mejor para | Programas de ciclo de vida programados, serie Nutrición | Secuencias de respuesta de comportamiento, abandono del carro de compras | Escalación en canales múltiples, mensajería complementaria |
| Horario de entrada | Programado (lote) | Tiempo real (impulsado por evento) | Programado o en tiempo real |
| Complejidad | Medio | Medium-High | Alta |
| Volumen de entrada | Hasta 20.000 perfiles/s | Hasta 5.000 eventos/s | Igual que el método de entrada subyacente |
| Ámbito del canal | Uno o varios canales | Uno o varios canales | Se requieren varios canales |
| Requiere | Audiencia definida, programación de evaluación | Infraestructura de eventos de streaming | Superficies de canal para cada canal |
| Respuesta en tiempo real | No — registro por lotes | Sí, inmediatamente después del evento | Depende del método de entrada |

### Elija la opción correcta

Utilice el siguiente flujo de decisión para seleccionar el método de implementación adecuado:

1. **¿El recorrido lo inició un comportamiento o evento del cliente?** Si es así, elija **Opción B** (desencadenada por eventos). Si el recorrido se inicia mediante una lectura de audiencia programada, elija **Opción A** (Lectura de audiencia).

2. **¿El recorrido utiliza varios canales de mensajería (por ejemplo, correo electrónico Y SMS)?** En caso afirmativo, aplique **Opción C** (Multicanal) sobre el método de entrada que elija (A o B). Si el recorrido utiliza un solo canal en, la opción A o B por sí sola es suficiente.

3. **¿Necesita escalar a un canal diferente según la participación?** Si es así, elija **Opción C** con nodos de condición que comprueben la participación con mensajes anteriores y se ramifiquen a canales alternativos.

4. **¿La audiencia se conoce de antemano y se procesa según una programación?** Si es así, elija **Opción A**. Si los perfiles deben ingresar al recorrido en el momento en que realizan una acción, elija **Opción B**.

## Fases de implementación

Las siguientes fases recorren la implementación integral de un recorrido orquestado de varios pasos.

### Fase 1: Configuración de canales y preparación de audiencias

**Funciones de aplicación:** AJO: Configuración de canal, RT-CDP: Evaluación de audiencia

Antes de diseñar el recorrido, todas las superficies de canal deben estar activas y la audiencia de entrada (para la opción A) debe definirse y evaluarse. Esta fase garantiza que la infraestructura esté lista para la entrega de mensajes.

#### Decida el tipo de canal de cada punto de contacto

¿Qué canales de mensajería utilizará el recorrido en cada punto de contacto?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo correo electrónico | El recorrido se comunica exclusivamente por correo electrónico (incorporación, crianza) | Configuración más sencilla; requiere subdominio de correo electrónico y grupo de IP; sujeto a la ubicación de la bandeja de entrada |
| Solo SMS | Alertas con distinción de tiempo, recordatorios de citas | Requiere credenciales de proveedor de SMS (Sinch, Twilio, Infobip); mayor coste por mensaje; reglas de exclusión más estrictas |
| Solo push | Secuencias de participación en la aplicación para usuarios móviles | Requiere credenciales de APNS/FCM; los usuarios deben tener la aplicación instalada |
| Multicanal | Mensajería escalable o complementaria entre canales | Requiere superficie de canal por canal; alcance más complejo pero más alto |

#### Decidir el método de evaluación de audiencias (Opción A)

¿Con qué rapidez deben cumplir los perfiles los requisitos para la audiencia de entrada?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Evaluación por lotes | La audiencia se lee con arreglo a una programación (diaria, semanal); no se necesita ninguna entrada en tiempo real | Configuración sencilla; audiencia evaluada antes de leer el recorrido; admite reglas de segmentos complejas |
| Evaluación de streaming | Los perfiles deben cumplir los requisitos en tiempo casi real a medida que cambian los atributos | La expresión de regla de segmento debe ser apta para streaming; calificación casi en tiempo real |

#### Decidir el método de delegación de subdominios (canal de correo electrónico)

¿Cómo se debe delegar el subdominio de envío de correo electrónico a Adobe?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Delegación completa | Adobe administra los registros DNS; la configuración más sencilla | La configuración más rápida; Adobe gestiona SPF, DKIM y DMARC |
| Delegación CNAME | La organización retiene el control DNS | Requiere la participación del administrador DNS; se deben configurar registros CNAME |

#### Navegación de IU

- Superficies de canal: Administración > Canales > Superficies de canal > Crear superficie
- Subdominios: Administración > Canales > Subdominios
- Configuración de SMS: Administración > Canales > Configuración de SMS
- Configuración push: Administración > Canales > Configuración de notificaciones push
- Audiencias: Cliente > Audiencias > Crear audiencia > Generar regla

#### Detalles de configuración clave

- Verificar el estado de calentamiento del grupo de IP para el correo electrónico: los nuevos grupos de IP requieren un plan de calentamiento gradual durante 2 a 4 semanas
- Para SMS, configure las credenciales del proveedor y verifique el registro del número de remitente
- Para las notificaciones push, cargue certificados APNS y claves de servidor FCM
- Defina la audiencia de entrada mediante el Generador de segmentos con reglas de segmento que abarquen la población objetivo
- Incluir reglas de supresión en la definición de audiencia (excluir convertidos recientemente y cancelada la suscripción globalmente)

#### Dónde divergen las opciones

**Para La Opción A (Lectura De Audiencia):**
Defina y evalúe la audiencia de entrada. Confirme que la audiencia tiene una población distinta de cero. Determine si la recorrido utilizará una lectura de audiencia única o una programación de lectura recurrente.

**Para La Opción B (Activada Por Evento):**
Compruebe que el esquema de evento de activación esté configurado y que los eventos se transmitan a la plataforma. No se requiere una audiencia predefinida: los perfiles se introducen individualmente tras la recepción del evento.

**Para Opción C (Multicanal):**
Configure las superficies de canal para CADA canal utilizado en el recorrido (correo electrónico, SMS, push, en la aplicación). Compruebe el estado de consentimiento por canal para la población objetivo.

#### Documentación de Experience League

- [Configuración de superficies de canal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [planes de calentamiento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)


### Fase 2: Creación del contenido del mensaje

**Función de aplicación:** AJO: Creación de mensajes

Cree el contenido del mensaje para cada punto de contacto del recorrido. Cada mensaje puede tener un contenido, una profundidad de personalización y un canal diferentes. Esta fase crea todo el contenido de la entrega al que hacen referencia los nodos de acción del recorrido.

#### Decidir el enfoque del contenido

¿Cada mensaje debe comenzar desde una plantilla, diseñarse desde cero o importar HTML?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Plantilla de contenido existente | Mensajes coherentes con la marca con diseños establecidos | Más rápido; garantiza el cumplimiento de la marca; la plantilla debe existir y coincidir con el tipo de canal |
| Diseñe desde cero | Diseños únicos y personalizados para cada punto de contacto | El más flexible; mayor tiempo de compilación; usar arrastrar y soltar de Email Designer |
| Importar HTML | HTML creado previamente a partir de herramientas de diseño externas | Requiere HTML limpio; puede que necesite un ajuste para la capacidad de respuesta |

#### Decidir la profundidad de personalización

¿Cuánta personalización debe incluir cada mensaje?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Inserción de token básico | Nombre, ciudad, atributos de perfil simples | Baja complejidad; utiliza sintaxis de Handlebars con rutas XDM |
| Bloques de contenido condicionales | Contenido diferente mostrado en función del segmento o atributo | Complejidad de Medium; requiere reglas de contenido dinámico |
| Personalización contextual-recorrido | El contenido varía según la ruta del recorrido y las interacciones anteriores | Mayor complejidad; aprovecha las variables de contexto de recorrido y los datos de evento |

#### Decidir la estrategia del fragmento

¿Deben crearse bloques de contenido compartido (encabezados, pies de página, texto legal) como fragmentos reutilizables?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Fragmentos reutilizables | Varios mensajes comparten elementos comunes; se requiere coherencia de marca | Los cambios se propagan a todos los mensajes mediante el fragmento; máximo de 30 fragmentos por mensaje |
| Contenido en línea | Mensajes únicos con diseños únicos | Más rápido para contenido de un solo uso; sin beneficios de coherencia entre mensajes |

#### Navegación de IU

- Gestión de contenido > Plantillas de contenido > Examinar
- Correo electrónico en Designer (dentro de la campaña o de la acción de recorrido)
- Administración de contenido > Fragmentos > Crear fragmento

#### Detalles de configuración clave

- Contenido de autor para CADA acción de mensaje del recorrido: un recorrido de 4 pasos puede requerir 4 diseños de mensaje independientes
- Utilice expresiones de personalización que hagan referencia a rutas de perfil XDM (por ejemplo, `{{profile.person.name.firstName}}`)
- Configurar bloques de contenido dinámico para variaciones específicas de segmentos
- Vista previa de cada mensaje con perfiles de prueba para verificar la renderización de la personalización
- Envíe pruebas a las partes interesadas internas para que revisen el contenido
- Para SMS, respete los límites de caracteres (160 caracteres para la codificación GSM estándar)
- Para las notificaciones push, configure el título, el cuerpo, la imagen y la acción de vínculo profundo/URL

#### Documentación de Experience League

- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Crear un correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Creación de un mensaje SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Diseño de una notificación push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)


### Fase 3: Diseño y activación del recorrido

**Función de aplicación:** AJO: Journey Orchestration

Diseñe el lienzo de recorrido de varios pasos, incluidos el nodo de entrada, los nodos de acción (mensajes), los nodos de condición (ramificación), los nodos de espera (retrasos de tiempo) y los criterios de salida. A continuación, realice pruebas con perfiles de prueba y publique.

#### Decidir el tipo de entrada

¿Cómo deben entrar los perfiles en el recorrido?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Leer audiencia | Secuencias de nutrición programadas; audiencia conocida procesada en lote | Audiencia evaluada en tiempo de lectura; admite lecturas únicas o recurrentes; hasta 20 000 perfiles/s |
| Evento unitario | Déclencheur de comportamiento en tiempo real (compra, abandono del carro de compras) | Entrada en tiempo real; requiere flujo continuo de eventos; hasta 5000 eventos/s |
| Calificación de audiencias | Entrada cuando un perfil entra o sale de una audiencia en tiempo casi real | Evaluación de flujo; desencadenada por un cambio en el abono de segmentos |
| Evento empresarial | El evento de toda la organización déclencheur el recorrido para una audiencia | Útil para lanzamientos de productos, eventos meteorológicos y alertas del sistema |

#### Decidir la política de reentrada

¿Puede un perfil volver a entrar en el recorrido después de completarse o salir?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Permitir la reentrada (con reutilización) | Es posible que los perfiles tengan que repetir el recorrido (compras recurrentes, renovación de la participación estacional) | Reutilización mínima de 5 minutos; evita entradas duplicadas en la ventana de reutilización |
| No hay reentrada | Recorridos únicos (incorporación, evento de ciclo vital único) | El perfil completa o sale del recorrido y no puede volver a entrar |

#### Decidir las duraciones de espera entre los puntos de contacto

¿Cuánto tiempo debe esperar el recorrido entre cada mensaje?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Duración fija (por ejemplo, 3 días) | Ritmo coherente independientemente del comportamiento del perfil | Sencillo; tiempo predecible; mínimo de 1 hora para recorridos leídos por la audiencia |
| Fecha y hora específicas | El mensaje debe llegar a una hora precisa (por ejemplo, la fecha de renovación) | Utiliza el atributo o la expresión de perfil para determinar la fecha/hora exacta |
| Expresión personalizada | Espera dinámica basada en datos de perfil o contexto de recorrido | Más flexible; requiere la creación de expresiones |

#### Decidir las condiciones de ramificación

¿Qué condiciones determinan la ruta que sigue un perfil?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Comprobación de atributos de perfil | Rama basada en el nivel de lealtad, interés del producto y ubicación geográfica | Utiliza los datos de perfil disponibles en el momento de la evaluación |
| Comprobación de abono de segmentos | Rama basada en si el perfil pertenece a una audiencia específica | Requiere que se defina la audiencia y se realice la evaluación |
| Comprobación de datos de evento | Rama basada en si el perfil realizó una acción (correo electrónico abierto, vínculo pulsado) | Evalúa datos de eventos con alcance de recorrido; útil para la bifurcación basada en la participación |
| División porcentual | Distribuya perfiles aleatoriamente por rutas (para pruebas A/B o despliegues controlados) | No utiliza datos de perfil; asignación puramente aleatoria |

#### Decidir los criterios de salida

¿Qué evento o condición hace que un perfil salga del recorrido antes de tiempo?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Evento de conversión | El perfil completa la acción deseada (compra, registro, envío de formulario) | Requiere flujo de eventos; criterios de salida más comunes |
| Salida de pertenencia a audiencia | El perfil deja la audiencia de entrada o se une a una audiencia de exclusión | Evalúa en tiempo casi real las audiencias de streaming |
| Tiempo de espera | Se alcanzó la duración máxima del recorrido (hasta 91 días) | Red de seguridad predeterminada; configurable en propiedades de recorrido |
| Sin criterios de salida | El perfil completa toda la ruta de recorrido de forma natural | Lo más simple; todos los perfiles atraviesan todo el recorrido a menos que se eliminen manualmente |

#### Decidir el tiempo de espera del recorrido

¿Cuál es la duración máxima que un perfil puede permanecer en el recorrido?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| 91 días (máximo) | Recorridos de larga duración (renovación trimestral, incorporación extendida) | Máximo permitido; los perfiles que siguen en el recorrido en el tiempo de espera se abandonan automáticamente |
| Duración personalizada más corta | El recorrido debe completarse en un plazo definido (7 días, 14 días, 30 días) | Configurado en función del ciclo de vida natural del caso de uso |

#### Navegación de IU

- Crear recorrido: Recorrido > Crear Recorrido
- Propiedades del recorrido: lienzo de Recorrido > Panel Propiedades
- Nodo de entrada: lienzo de Recorrido > Arrastrar &quot;Leer audiencia&quot; o actividad de evento
- Nodos de acción: lienzo de Recorrido > Arrastrar acción de canal (correo electrónico, SMS, push)
- Nodos de condición: lienzo de Recorrido > Arrastrar la actividad &quot;Condición&quot;
- Nodos de espera: lienzo de Recorrido > Arrastrar actividad &quot;Wait&quot;
- Criterios de salida: Propiedades de la Recorrido > Criterios de salida > Configurar
- Modo de prueba: lienzo de Recorrido > Alternar modo de prueba
- Publicar: Lienzo de Recorrido > Publicar

#### Detalles de configuración clave

- Asigne un nombre al recorrido con una convención clara y descriptiva (por ejemplo, &quot;Onboarding_Series_Email_v1&quot;)
- Establezca la zona horaria de recorrido para un procesamiento coherente de los pasos de espera
- Configure cada nodo de acción con la superficie de canal adecuada y vincúlelo al contenido de mensaje creado
- Cada rama debe finalizar con una actividad End
- Configurar las reglas de reentrada adecuadas para el caso de uso
- Utilice el modo de prueba con perfiles de prueba para simular la ruta de recorrido completa antes de la publicación
- Compruebe que los perfiles de prueba siguen las rutas esperadas y reciben los mensajes correctos

#### Dónde divergen las opciones

**Para La Opción A (Lectura De Audiencia):**

- Arrastre la actividad &quot;Leer audiencia&quot; como nodo de entrada
- Selección de la audiencia de destino definida en la fase 1
- Opcionalmente, configurar una programación de lectura recurrente (diaria, semanal)
- Configure el acelerador de velocidad de lectura si la carga descendente del sistema es un problema

**Para La Opción B (Activada Por Evento):**

- Arrastre el evento de activación como nodo de entrada
- Configuración del esquema de eventos y las condiciones de entrada
- Establezca las reglas de reentrada con cuidado para evitar entradas duplicadas de eventos repetidos

**Para Opción C (Multicanal):**

- Utilice el método de entrada de la opción A o B
- En cada nodo de acción, seleccione la superficie de canal adecuada para ese punto de contacto
- Añada nodos de condición entre canales para comprobar la participación (por ejemplo, &quot;¿el perfil abrió el correo electrónico?&quot;) y ruta a canales alternativos

#### Documentación de Experience League

- [Creación de un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propiedades del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Leer actividad de audiencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Eventos generales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de calificación de público](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Añadir un mensaje en un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Actividad de condición](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Actividad Esperar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Criterios de salida](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Actividad Finalizar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/end-activity)
- [administración de entradas de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Prueba del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicación del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)


### Fase 4: Configuración de la gobernanza y la optimización

**Funciones de la aplicación:** AJO: Frequency &amp; Business Rules, AJO: Conflict &amp; Priority Management, AJO: Content Experimentation, RT-CDP: Consent &amp; Governance Enforcement

Aplique límites de frecuencia para evitar mensajes excesivos, asigne puntuaciones de prioridad para la resolución de conflictos con otras comunicaciones activas, configure opcionalmente pruebas A/B dentro de los mensajes de recorrido y compruebe la aplicación del consentimiento.

#### Decidir la configuración del límite de frecuencia

¿Deben los mensajes de recorrido respetar los límites de frecuencia globales?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Aplicación de reglas de frecuencia | El recorrido funciona junto con otras campañas y recorridos; los perfiles no deben enviarse en exceso | Los mensajes se pueden suprimir si el perfil ya ha alcanzado el límite de otras comunicaciones |
| Exento de límite | Los mensajes de recorrido son esenciales y siempre deben entregarse (transaccionales, normativos) | Usar con moderación; puede contribuir a la fatiga del mensaje si se utiliza en exceso |

#### Decidir la asignación de puntuación de prioridad

¿Cómo debe clasificarse este recorrido en relación con otras campañas y recorridos activos?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Alta prioridad (70-100) | Los mensajes de recorrido son comunicaciones esenciales del ciclo vital (incorporación, renovación) | La prioridad mayor prevalece cuando surgen conflictos con otras comunicaciones |
| Prioridad de Medium (30-69) | Los mensajes de recorrido son importantes pero no urgentes (educación, educación) | Puede ser suprimido por comunicaciones de mayor prioridad |
| Prioridad baja (0-29) | Los mensajes de recorrido son complementarios o promocionales | Se suprimirá al competir con mensajes de mayor prioridad |

#### Decidir la experimentación de contenido

¿Debería algún mensaje de recorrido incluir una prueba A/B o multivariable?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Sí: prueba A/B | Optimizar líneas de asunto, CTA o diseños de contenido en un punto de contacto específico | Requiere volumen suficiente por variante para obtener relevancia estadística; se admiten de 2 a 10 tratamientos |
| Sin experimentación | El contenido ha finalizado o el volumen es demasiado bajo para realizar pruebas significativas | Configuración más sencilla; no se necesita seguimiento de variantes |

#### Navegación de IU

- Reglas de frecuencia: Administración > Reglas de negocio > Crear regla
- Puntuaciones de prioridad: propiedades de Recorrido > Puntuación de prioridad
- Detección de conflictos: Administración > Reglas de negocio > Conflicto y prioridad
- Experimento de contenido: lienzo de Recorrido > Seleccionar acción de mensaje > Alternar experimento de contenido
- Políticas de consentimiento: Privacidad > Políticas > Políticas de consentimiento

#### Detalles de configuración clave

- Definir límites de frecuencia específicos del canal (por ejemplo, máximo 3 correos electrónicos/semana, máximo 1 SMS/día, máximo 2 notificaciones push/día)
- Asigne una puntuación de prioridad al recorrido (0-100) que refleje su importancia comercial con respecto a otras comunicaciones activas
- Revise el panel de detección de conflictos para identificar cualquier campaña o recorrido que se superponga
- Si ejecuta un experimento de contenido, defina las variantes de tratamiento, defina la asignación de tráfico, elija la métrica de éxito (aperturas, clics o conversiones) y establezca el umbral de confianza (normalmente del 95 %)
- Compruebe que la aplicación del consentimiento esté activa para cada canal utilizado en el recorrido

#### Documentación de Experience League

- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Información general sobre reglas comerciales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificación de posibles conflictos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [restricción y arbitraje de recorridos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Introducción al experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)


### Fase 5: Configuración de la creación de informes y monitorización

**Funciones de la aplicación:** AJO: Informes y análisis de rendimiento, supervisión y observabilidad, Informes y análisis

Monitorice la ejecución del recorrido durante y después de la activación, revise las métricas de entrega y participación por paso, configure alertas para errores de procesamiento del recorrido y, opcionalmente, cree un análisis de CJA Workspace para la visualización profunda de funnel y visitas en el orden previsto.

#### Decidir el método de creación de informes

¿Qué herramientas de creación de informes se necesitan para este recorrido?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo informes nativos de AJO | La supervisión básica de la entrega y la participación es suficiente | Informe en vivo (durante la ejecución) e informe Todo el tiempo (después de la ejecución); se actualiza cada 60 segundos para el informe en vivo |
| Análisis de AJO + CJA | Se necesita un análisis funnel profundo, tasas de conversión de pasos, una visualización de abandonos o una comparación de recorridos cruzados | Requiere conexión de CJA y vista de datos vinculada a conjuntos de datos de AJO; el más completo |
| Solo CJA | La organización utiliza CJA como plataforma principal de análisis | Requiere la configuración de CJA; los informes nativos de AJO siguen estando disponibles como copia de seguridad |

#### Decidir la configuración de alertas

¿Qué errores de recorrido deben provocar las alertas de déclencheur?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Recorrido de alertas de procesamiento | Siempre recomendado para recorridos de producción | Alertas sobre errores de entrada de perfil, errores de nodos de acción y interrupciones del recorrido |
| Alertas de errores de entrega | Esencial para recorridos con comunicaciones de alto valor | Alertas de tasas de devolución que superan los umbrales y errores de entrega |

#### Navegación de IU

- Informe en vivo de recorrido: Recorrido > Seleccionar recorrido > Informe en vivo
- Informe de recorridos en todo el tiempo: Recorridos > Seleccionar recorrido > Informe de todos los tiempos
- Alertas: Alertas > Reglas de alerta > Suscribirse
- CJA Workspace: Proyectos > Crear nuevo proyecto

#### Detalles de configuración clave

- Acceda al informe en directo durante la ejecución del recorrido para monitorizar las entradas de perfil, las salidas y las métricas de entrega por paso en tiempo real
- Una vez finalizado el recorrido (o una vez que se hayan acumulado los datos suficientes), revise el informe Todo el tiempo para obtener un análisis exhaustivo
- Configuración de alertas de plataforma para errores de procesamiento de recorrido y problemas de envío
- Para el análisis de CJA, asegúrese de que la conexión de CJA incluye conjuntos de datos de evento de experiencia de AJO (comentarios de mensajes, seguimiento de correo electrónico, eventos de paso de Recorrido)
- Crear un Workspace de CJA con:
   - Visualización de funnel que muestra los recuentos de perfiles en cada paso del recorrido
   - Visualización de abandonos para identificar puntos de entrega
   - Cálculos de tasa de conversión de etapas
   - Análisis del tiempo de conversión
   - Desglose de la participación a nivel de canal (para recorridos multicanal)

#### Documentación de Experience League

- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Consideraciones sobre la implementación

Revise las siguientes barreras, escollos, prácticas recomendadas y compensaciones antes y durante la implementación.

### Protecciones y límites

- Máximo de **500 recorridos activos** por zona protegida — [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- La duración máxima del recorrido de **es de 91 días** (tiempo de espera global): los perfiles que aún están en el recorrido en el tiempo de espera se cierran automáticamente
- Máximo de **50 actividades** por lienzo de recorrido
- Procesamiento de recorridos de audiencia de lectura de hasta **20.000 perfiles por segundo** (acelerador predeterminado)
- Los recorridos de eventos unitarios admiten hasta **5,000 eventos por segundo** por zona protegida
- Los pasos de espera tienen una duración mínima de **1 hora** para los recorridos de lectura de audiencia
- el tiempo de reutilización de la reentrada al recorrido **es de 5 minutos**
- Máximo de **10 superficies de canal por tipo de canal** por zona protegida
- Se recomienda un tamaño máximo de correo electrónico de **100 KB** para una entrega óptima
- Máximo de **30 fragmentos de contenido** por mensaje
- Máximo de **10 tratamientos de experimento con contenido** (variantes) por experimento
- Máximo de **10 configuraciones de límite** por zona protegida
- Máximo de **4.000 definiciones de segmento** por zona protegida

### Peligros comunes

- **Publicación sin prueba:** Use siempre el modo de prueba con perfiles de prueba para validar la ruta de recorrido completa antes de publicar. Compruebe que los perfiles atraviesan las ramas esperadas, que los pasos de espera avanzan correctamente y que los mensajes se representan correctamente.
- **Faltan actividades de finalización en las ramas:** Cada rama de recorrido debe finalizar con una actividad de finalización. El recorrido no se podrá publicar si alguna rama queda sin un nodo de terminación.
- **Condiciones de entrada demasiado amplias:** Una condición de evento o audiencia de entrada definida de forma imprecisa puede inundar el recorrido con perfiles no deseados. Restrinja los criterios de entrada con comprobaciones de atributos y reglas de supresión específicas.
- **Ignorando las reglas de reentrada:** Para los recorridos activados por eventos, los perfiles pueden activar el evento activador varias veces. Sin la configuración de reentrada adecuada (período de denegación de reentrada o de reutilización), los perfiles se pueden acumular en el recorrido, lo que provoca la duplicación de mensajes.
- **Confusión de zona horaria de paso de espera:** Las duraciones de espera se procesan en UTC. Establezca la zona horaria de recorrido explícitamente en las propiedades del recorrido para garantizar que los pasos de espera avancen a la hora local esperada.
- **Editar un recorrido activo:** Los recorridos activos no se pueden editar directamente. Para realizar cambios, duplique el recorrido, modifique la copia, detenga el original y publique la nueva versión. Planifique el control de versiones del recorrido antes de activarlo.
- **No se definieron criterios de salida:** Sin criterios de salida, los perfiles que conviertan a mitad del recorrido seguirán recibiendo mensajes posteriores, potencialmente irrelevantes o contradictorios. Configure siempre los criterios de salida para los eventos de conversión.
- **Desalineación del consentimiento del canal:** Se puede activar un perfil para el correo electrónico, pero no para los SMS. Los recorridos multicanal deben respetar el consentimiento por canal. Compruebe que los campos de consentimiento se rellenan y aplican en cada superficie de canal.

### Prácticas recomendadas

- **Comience con una iteración simple:** Comience con un recorrido de pasos lineal de 2 a 3 antes de agregar ramas complejas. Valide el funcionamiento del flujo principal antes de crear capas en condiciones y canales.
- **Use convenciones de nomenclatura descriptiva:** Asigne claramente nombres a los nodos, condiciones y pasos de espera del recorrido (por ejemplo, &quot;Wait_3_Days_After_Welcome&quot; en lugar de &quot;Wait 1&quot;). Esto hace que la depuración del modo de prueba y la interpretación de informes sean mucho más sencillas.
- **Configurar los criterios de salida de forma anticipada:** Defina el evento de conversión como un criterio de salida antes de diseñar las rutas de recorrido. Esto garantiza que los perfiles que se convierten se eliminen del recorrido independientemente del paso en el que se encuentren.
- **Establecer duraciones de espera significativas:** Base las duraciones de espera en los datos de comportamiento del cliente: tiempo entre interacciones típicas, ventanas de respuesta esperadas y cadencia apropiada para el canal (por ejemplo, 2-3 días entre correos electrónicos, 1 semana entre SMS).
- **Use nodos de condición para comprobar la participación:** Después de una acción de mensaje, agregue una condición para comprobar si el perfil está activado (lo abrió, hizo clic). Dirija los perfiles comprometidos a una ruta y los perfiles no comprometidos a una ruta de escalación o de canal alternativo.
- **Aproveche los atributos calculados para la bifurcación:** Use atributos calculados como puntuaciones de participación, frecuencia de compra o días transcurridos desde la última actividad para tomar decisiones de bifurcación basadas en datos en lugar de arbitrarias.
- **Supervisar y optimizar de forma iterativa:** Revisar informes de recorrido semanalmente durante la ejecución inicial. Identifique los puntos de entrega, ajuste las duraciones de espera, perfeccione las condiciones y optimice el contenido del mensaje en función de los datos de rendimiento por paso.
- **Versión de los recorridos:** Cuando realice cambios, duplique el recorrido para crear una nueva versión. Mantenga un registro de cambios de versión para el seguimiento de auditoría y optimización.

### Decisiones de compensación

Las siguientes compensaciones deben evaluarse en el contexto de sus requisitos comerciales específicos.

#### Entrada de lectura de audiencia frente a entrada activada por evento

La entrada de lectura de audiencia proporciona un procesamiento predecible basado en lotes que es más fácil de administrar y probar. La entrada activada por eventos proporciona una capacidad de respuesta en tiempo real más relevante para el contexto, pero requiere una infraestructura de streaming y una administración de reentrada más cuidadosa.

- **Favoritos de lectura de audiencia:** previsibilidad, procesamiento de gran volumen, programas de ciclo de vida programados, pruebas más sencillas
- **Favoritos activados por eventos:** relevancia en tiempo real, contexto de comportamiento, ritmo de perfil individual, respuesta inmediata a las acciones de los clientes
- **Recomendación:** Use lectura de audiencia para los programas de ciclo de vida planificados (incorporación, renovación) en los que el tiempo depende de la empresa. Utilice activadas por eventos para secuencias de respuesta de comportamiento (abandono del carro de compras, poscompra) donde el tiempo es impulsado por el cliente.

#### Recorrido de un solo canal frente a multicanal

Los recorridos de un solo canal son más fáciles de implementar, probar y administrar. Los recorridos multicanal proporcionan un alcance y una capacidad de escalación más amplios, pero aumentan la complejidad en la creación de contenido, la administración de consentimientos y la gobernanza de las frecuencias.

- **Favoritos de canal único:** Implementación más rápida, administración de consentimiento más sencilla, menor esfuerzo de producción de contenido, depuración más sencilla
- **Favoritos multicanal:** mayor potencial de participación, escalación de canal para perfiles que no responden y experiencia de cliente más completa
- **Recomendación:** Comience con un recorrido de un solo canal y valide el flujo y el impacto empresarial antes de expandirse a multicanal. Añada canales de forma incremental donde los datos de participación muestren que el canal principal no está llegando a la audiencia de forma eficaz.

#### Complejidad del recorrido frente a capacidad de administración

Un recorrido muy ramificado con muchas condiciones y rutas puede abordar más escenarios, pero se vuelve más difícil de probar, depurar y optimizar. Un recorrido más sencillo con menos ramas es más fácil de administrar, pero puede ofrecer una experiencia menos personalizada.

- **Los recorridos complejos favorecen:** personalización granular, rutas específicas de segmentos, cobertura de escenario integral
- **Los recorridos más simples favorecen:** implementación más rápida, pruebas más sencillas, informes más claros, menor carga de mantenimiento
- **Recomendación:** Limite los recorridos a 3-5 ramas principales y 15-25 actividades. Si la lógica requiere más complejidad, considere la posibilidad de dividirse en varios recorridos con coordinación entre recorridos en lugar de un único recorrido monolítico.

#### Restricción del límite de frecuencia frente a finalización del recorrido

Los límites de frecuencia estrictos protegen contra la mensajería excesiva, pero pueden suprimir los mensajes de recorrido, lo que provoca que los perfiles omitan pasos y reducen las tasas de finalización de recorridos. Los límites indulgentes garantizan que los mensajes de recorrido se envíen, pero suponen un riesgo de fatiga del canal.

- **Ventajas estrictas:** Protección de la experiencia del cliente, tasas de cancelación de suscripción reducidas, confianza de marca
- **Mayúsculas indulgentes a favor:** tasas de finalización de Recorridos, entrega de secuencia de mensajes completa, efectividad del programa de marketing
- **Recomendación:** Asigne puntuaciones de prioridad más altas a los mensajes de recorrido críticos (incorporación, renovación) para que tengan prioridad sobre las campañas promocionales cuando se alcancen los límites. Reserve &quot;exento de límite&quot; solo para comunicaciones verdaderamente esenciales.

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las capacidades utilizadas en esta implementación.

### Recorridos

- [Introducción a recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Creación de un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propiedades del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Publicación del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)
- [Prueba del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)

### actividades de recorrido

- [Leer actividad de audiencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Eventos generales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de calificación de público](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Actividad de condición](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Actividad Esperar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Añadir un mensaje en un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Actividad Finalizar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/end-activity)
- [Configuración de una acción personalizada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions)

### Administración de entrada y salida

- [administración de entradas de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Criterios de salida](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configuración de superficies de canal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Crear grupos de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [planes de calentamiento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Creación y personalización de mensajes

- [Crear un correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Uso de componentes de contenido de Email Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funciones de ayuda](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Experimentación de contenido

- [Introducción al experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Cálculos estadísticos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### Frecuencia, conflicto y prioridad

- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Información general sobre reglas comerciales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Introducción a la administración de conflictos y prioridades](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [restricción y arbitraje de recorridos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Identificación de posibles conflictos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/edge-segmentation)

### Informes y análisis

- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)

### Consentimiento y control

- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Administrar lista de supresión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Base de datos

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Resumen del perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
