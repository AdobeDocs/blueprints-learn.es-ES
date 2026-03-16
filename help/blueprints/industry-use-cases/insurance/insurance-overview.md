---
title: Casos de uso del seguro
description: Descubra cómo las organizaciones de seguros utilizan Adobe Experience Platform para personalizar la administración de pólizas, mejorar las experiencias de las reclamaciones e impulsar la retención de clientes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2494'
ht-degree: 0%

---


# Casos de uso del seguro

Las organizaciones de seguros utilizan Adobe Experience Platform para unificar los datos del asegurado en los sistemas de gestión de pólizas, reclamaciones y participación para ofrecer comunicaciones personalizadas en cada fase de la relación con los clientes. Al conectar las señales de comportamiento con la información de la póliza y las reclamaciones, las aseguradoras pueden atraer de forma proactiva a los clientes con ofertas relevantes, actualizaciones de servicio oportunas y una asistencia significativa que aumente la retención y el valor de la duración.

## Campañas de renovación de directivas

Envíe recordatorios y ofertas personalizados de renovación de pólizas en función del historial de pólizas, el registro de reclamaciones y las preferencias de cobertura de cada cliente. El alcance oportuno y relevante de la renovación reduce las tasas de caída de las políticas y fortalece las relaciones con los clientes a largo plazo al facilitar a los asegurados comprender sus opciones y tomar medidas.

### Impacto empresarial

Las organizaciones que implementan campañas personalizadas de renovación de políticas generalmente ven una mejora de entre el 25 y el 35 por ciento en las tasas de renovación, lo que reduce directamente la pérdida de clientes y protege los ingresos recurrentes por primas.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Las fechas de renovación de las pólizas son déclencheur de eventos naturales que inician una divulgación oportuna y personalizada en el momento en que los asegurados toman su decisión de renovación.

### Consideraciones técnicas

- Integrarse con el sistema de gestión de políticas para recibir eventos de fecha de renovación y detalles de políticas actuales, asegurándose de que los mensajes reflejen una cobertura precisa y la información de primas.
- Aplique etiquetas de gobernanza de datos a todos los datos de políticas financieras y de identificación personal para cumplir con las regulaciones de seguros estatales y los requisitos de privacidad de datos.
- Configure reglas de supresión para evitar que se envíen mensajes de renovación a los tomadores de seguros que ya hayan renovado o que tengan reclamaciones activas que puedan afectar a sus condiciones de renovación.
- Coordine el tiempo con las asignaciones de agentes o agentes para que los mensajes directos al cliente se alineen con cualquier alcance que el agente asignado también pueda estar realizando.


## Recomendaciones de productos de venta cruzada

Recomiende productos de seguro adicionales, como cobertura de vida, vivienda o automóviles, en función de las pólizas existentes, la etapa de vida y el perfil de riesgo de cada cliente. Las recomendaciones personalizadas de productos ayudan a los asegurados a descubrir brechas de cobertura y construir una cartera de protección más completa.

### Impacto empresarial

Las recomendaciones de venta cruzada personalizadas suelen impulsar una mejora de entre el 20 y el 30 % en las tasas de conversión de venta cruzada, lo que aumenta las políticas por hogar y el valor de vida útil general del cliente.

### Cómo implementar

Usar el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). La toma de decisiones en tiempo real evalúa la cobertura, la fase de vida y las señales de comportamiento existentes de cada cliente para seleccionar la recomendación de producto más relevante del catálogo disponible.

### Consideraciones técnicas

- Integre los datos de directivas de todas las líneas de productos en un perfil de cliente unificado para que el motor de decisión tenga una vista completa de la cobertura existente al seleccionar recomendaciones.
- Configure reglas de idoneidad dentro del modelo de toma de decisiones para excluir los productos que un cliente ya tiene o que entran en conflicto con las directrices de suscripción para su perfil de riesgo.
- Aplique reglas de cumplimiento regulatorio para garantizar que las recomendaciones de productos cumplan con los requisitos de idoneidad y marketing de seguros específicos del estado.
- Coordine el resultado de la toma de decisiones con el portal del agente para que los productos recomendados sean visibles para los agentes asignados que puedan estar teniendo conversaciones directas con el cliente.


## Personalization de proceso de reclamaciones

Personalice las comunicaciones del proceso de reclamaciones, las actualizaciones de estado y los recursos de asistencia en función del tipo de reclamación, las preferencias del cliente y el historial de reclamaciones. Una experiencia de reclamaciones transparente y bien comunicada reduce la ansiedad durante los momentos de estrés y genera una confianza duradera con los asegurados.

### Impacto empresarial

Las comunicaciones de reclamaciones personalizadas generalmente logran una mejora de 40 a 50 por ciento en las puntuaciones de satisfacción de reclamaciones, reduciendo las quejas y reforzando la probabilidad de renovación de la política después de una reclamación.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). El proceso de reclamos es una experiencia de varias etapas con diferentes fases (presentación, investigación, ajuste y liquidación), cada una de las cuales requiere comunicaciones adaptadas y tiempo de adaptación.

### Consideraciones técnicas

- Integre con el sistema de administración de reclamaciones para recibir eventos de cambio de estado en tiempo real que hagan avanzar al cliente a través de la fase de recorrido adecuada.
- Lógica de ramificación de recorrido de diseño que adapta el tono y el contenido de la mensajería en función del tipo de reclamación, como la colisión automática frente a las reclamaciones por daños a la propiedad frente a las reclamaciones de responsabilidad.
- Implemente reglas de supresión durante las investigaciones de reclamaciones activas para evitar que los mensajes de marketing o de venta cruzada lleguen a los clientes en momentos confidenciales.
- Asegúrese de que todos los datos relacionados con las reclamaciones que fluyen al perfil del cliente estén etiquetados con las restricciones de control de datos adecuadas para evitar su uso fuera de las comunicaciones del servicio.


## Evaluación y prevención de riesgos

Proporcione información personalizada de evaluación de riesgos y consejos de prevención en función del tipo de política, la ubicación geográfica y los factores de riesgo específicos de cada cliente. La educación proactiva del riesgo ayuda a los asegurados a reducir su exposición a las pérdidas, beneficiando tanto al cliente como a la aseguradora.

### Impacto empresarial

El alcance personalizado de la prevención de riesgos suele impulsar una mejora de entre el 30 y el 40 por ciento en la participación en la prevención, lo que contribuye a reducir la frecuencia de las reclamaciones y mejorar la satisfacción del cliente.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). La educación para la prevención de riesgos es más eficaz como un recorrido multi-táctil sostenido que ofrece una orientación relevante a lo largo del tiempo y se adapta en función de la participación del cliente y los factores de riesgo estacionales.

### Consideraciones técnicas

- Integre con proveedores de datos de riesgo de terceros para obtener información sobre el clima, el peligro geográfico y el riesgo inmobiliario que enriquezca los perfiles de los clientes con puntuaciones de riesgo específicas de la ubicación.
- Diseñe una lógica de recorrido estacional que ofrezca contenido relevante antes de los períodos de alto riesgo, como la preparación para la temporada de huracanes para los asegurados costeros o consejos sobre el clima invernal para los clientes de clima frío.
- Aplicar etiquetas de gobernanza de datos para distinguir los datos de evaluación de riesgos utilizados para la educación de los clientes de los datos utilizados en las decisiones de suscripción actuarial.
- Coordinar el contenido de prevención de riesgos con la cobertura específica del asegurado para que las recomendaciones sean relevantes para los peligros que realmente cubre su póliza.


## Notificaciones de cambio de directiva

Envíe notificaciones personalizadas sobre cambios de políticas, actualizaciones de cobertura y nuevas opciones en función de las preferencias de políticas y comunicaciones específicas de cada cliente. Las notificaciones claras y oportunas mantienen informados a los asegurados y reducen la confusión sobre su estado de cobertura.

### Impacto empresarial

Las notificaciones personalizadas de cambio de política suelen lograr una mejora de entre el 50 y el 60 por ciento en las tasas de acuse de recibo de notificaciones, lo que reduce las consultas sobre el servicio al cliente y mejora la comprensión general del tomador de seguros.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de cambio de directivas del sistema de administración sirven como déclencheur naturales para las notificaciones inmediatas y relevantes a través del canal preferido de cada cliente.

### Consideraciones técnicas

- Integrarse con el sistema de administración de políticas para capturar eventos de cambio de aprobación, modificación y renovación en tiempo real, lo que garantiza que las notificaciones reflejen el estado de la política más actual.
- Aplique reglas de cumplimiento regulatorio para garantizar que las notificaciones cumplan con los requisitos de comunicación exigidos por el estado para los cambios de políticas, incluidos los lenguajes requeridos y los marcos de tiempo de entrega.
- Configure la lógica de prioridad de canal en función de la urgencia y el tipo de cambio; por ejemplo, las reducciones de cobertura pueden justificar canales más inmediatos que las actualizaciones informativas.
- Mantenga una pista de auditoría de entrega para todas las notificaciones de cambio de política con el fin de admitir la documentación de cumplimiento normativo y la resolución de disputas.


## Recuperación de abandono de presupuesto

Vuelva a atraer a los clientes que empezaron pero no completaron una cotización de seguro con mensajes de seguimiento personalizados y ofertas adaptadas. El alcance de la recuperación oportuna lleva a los clientes potenciales de nuevo al proceso de cotización y aborda las barreras comunes para la finalización.

### Impacto empresarial

Las campañas de recuperación de abandono de cotizaciones suelen impulsar una mejora de entre el 20 y el 30 por ciento en las tasas de finalización de cotizaciones, convirtiendo más perspectivas en titulares de pólizas y reduciendo los costes de adquisición de clientes.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). El abandono de las cotizaciones es un evento de comportamiento que déclencheur un seguimiento oportuno mientras el interés y la intención del posible cliente siguen siendo frescos.

### Consideraciones técnicas

- Integre con la plataforma de cotización en línea para capturar eventos de abandono junto con los detalles de la cotización que el cliente ya había proporcionado, lo que permite una renovación de la participación personalizada.
- Configurar reglas de tiempo que equilibren la urgencia con el respeto: seguimiento inicial en cuestión de horas, con un número limitado de recordatorios posteriores en los días siguientes.
- Aplique reglas de consentimiento y privacidad para garantizar que el seguimiento solo se envíe a los posibles clientes que hayan elegido participar en comunicaciones de marketing, especialmente a los clientes que aún no hayan establecido una relación de directiva.
- Incluya vínculos profundos que devuelvan al cliente potencial directamente a su cotización guardada en lugar de exigirle que reinicie el proceso desde el principio.


## Ofertas de productos por fases de Life

Identifique a los clientes que entran en nuevas etapas de vida, como matrimonio, compra de vivienda, familia en crecimiento o jubilación, y ofrezca productos de seguro relevantes que coincidan con sus cambiantes necesidades de protección. La segmentación por etapas de vida ayuda a los asegurados a construir la cobertura correcta en el momento adecuado.

### Impacto empresarial

Las ofertas de productos basadas en etapas de vida suelen lograr una mejora de entre el 35 y el 45 por ciento en las tasas de adopción de productos de etapas de vida, lo que profundiza las relaciones con los clientes durante los momentos clave de toma de decisiones.

### Cómo implementar

Usar el patrón [Cross-Channel Recorrido with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Las transiciones de fase de vida se benefician de la orquestación entre canales combinada con la toma de decisiones en tiempo real para seleccionar el producto más relevante y entregarlo a través del canal preferido del cliente en el momento óptimo.

### Consideraciones técnicas

- Genere modelos de detección de etapas de vida usando señales de comportamiento como cambios de dirección, actualizaciones de beneficiarios y patrones de investigación en línea, combinados con eventos de cambio de políticas.
- Configure el motor de toma de decisiones con reglas de idoneidad y elegibilidad del producto que coincidan con cada fase de vida útil y con las recomendaciones de cobertura adecuadas.
- Coordine las ofertas de fase de vida con el agente o corredor asignado para que estén preparados para ayudar al cliente con una conversación consultiva cuando se entregue la oferta.
- Aplique etiquetas de control de datos a cualquier fuente de datos de terceros que se utilice para la inferencia de la fase de vida a fin de garantizar el cumplimiento de las normas de privacidad de datos y las prácticas de marketing leales.


## Oportunidades de Descuento y Ahorro

Identifique y comunique oportunidades de descuento personalizadas, como paquetes, controladores seguros, fidelidad y descuentos de facturación electrónica, en función del perfil y el comportamiento de cada cliente. Las comunicaciones proactivas de ahorro demuestran valor y fortalecen la relación precio-valor.

### Impacto empresarial

Las comunicaciones personalizadas de descuentos y ahorros suelen impulsar una mejora de entre el 25 y el 35 por ciento en las tasas de utilización de los descuentos, mejorando la satisfacción del cliente y reduciendo la pérdida basada en los precios.

### Cómo implementar

Usar el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Real-time Decisioning evalúa la elegibilidad de cada cliente para los descuentos disponibles y selecciona la oportunidad de ahorro más impactante para presentar en el momento adecuado.

### Consideraciones técnicas

- Integre con los sistemas de clasificación de pólizas y facturación para calcular la elegibilidad exacta del descuento y las cantidades de ahorro potencial para cada cliente en tiempo real.
- Configure reglas de decisión que tengan en cuenta las limitaciones de apilamiento de descuentos y garantice que las cantidades de ahorro comunicadas sean precisas actuarialmente y aprobadas por el equipo de asignación de precios.
- Aplique reglas reguladoras específicas del estado a las comunicaciones de descuento, ya que ciertos estados tienen restricciones sobre cómo se pueden comercializar y aplicar los descuentos de seguro.
- Realice un seguimiento de los resultados de adopción de descuentos para perfeccionar continuamente el modelo de toma de decisiones y priorizar los mensajes de ahorro que más interesan a los distintos segmentos de clientes.


## Prevención de fraude de reclamaciones

Utilice la detección inteligente de fraudes para identificar patrones de reclamaciones sospechosas y personalizar las comunicaciones de investigación al tiempo que mantiene la confianza de los clientes. La prevención eficaz del fraude protege a los asegurados honestos al mantener las primas justas y garantizar que las reclamaciones legítimas se procesen rápidamente.

### Impacto empresarial

Los programas inteligentes de prevención del fraude de reclamaciones generalmente logran una mejora del 15 al 25 por ciento en las tasas de detección del fraude, reduciendo los pagos fraudulentos y reduciendo los costes generales de las reclamaciones.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de puntuación de riesgo de fraude déclencheur comunicaciones de investigación y ajustes de proceso adecuados en tiempo real, lo que garantiza que las reclamaciones marcadas reciban atención inmediata.

### Consideraciones técnicas

- Integre las puntuaciones de riesgo de fraude del sistema de análisis de reclamaciones en el perfil del cliente, al tiempo que aplica etiquetas estrictas de gobernanza de datos para evitar que los datos de investigación de fraude aparezcan en comunicaciones dirigidas al cliente.
- Diseñe rutas de comunicación que mantengan un tono profesional y respetuoso para los clientes cuyas reclamaciones están en revisión, preservando la relación independientemente del resultado de la investigación.
- Implemente controles de acceso basados en funciones para garantizar que los indicadores de fraude solo estén visibles para los equipos de investigación autorizados y que nunca aparezcan en las vistas estándar del agente o del servicio al cliente.
- Coordínese con el servicio de resolución de identidades [!DNL Adobe Experience Platform] para detectar patrones en perfiles relacionados, como direcciones compartidas o números de teléfono vinculados a varias notificaciones sospechosas.


## Programas de Bienestar y Prevención

Personalice las comunicaciones del programa de bienestar, los recordatorios de participación y las notificaciones de recompensa para los clientes de seguros de salud y vida en función de sus objetivos y nivel de participación. Los programas activos de bienestar mejoran los resultados de salud de los asegurados y construyen una base de clientes más fuerte y comprometida.

### Impacto empresarial

Las comunicaciones personalizadas de los programas de salud y prevención suelen impulsar una mejora del 30 al 40 por ciento en las tasas de participación en los programas, lo que contribuye a mejores resultados de salud y a una menor frecuencia de reclamaciones.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Los programas de bienestar son experiencias de participación sostenida con hitos, desafíos y recompensas que requieren orquestación adaptativa basada en la actividad y el progreso de cada participante.

### Consideraciones técnicas

- Integre con fuentes de datos de aplicaciones de salud y dispositivos portátiles usando la ingesta de transmisión [!DNL Adobe Experience Platform], aplicando etiquetas de control de datos claras para distinguir los datos de salud de los datos de suscripciones o reclamaciones.
- Implemente mecanismos de consentimiento independientes para la recopilación de datos de bienestar a fin de garantizar que los participantes comprendan cómo se utilizan los datos de sus actividades de salud y puedan excluirse sin afectar a su política.
- Diseñe una lógica de recorrido que ajuste la intensidad del programa y la frecuencia de la comunicación en función del nivel de participación de cada participante para evitar la fatiga y fomentar la participación sostenida.
- Asegúrese de que el seguimiento de incentivos y recompensas de bienestar cumpla con las regulaciones de seguro aplicables en torno a los incentivos para asegurados y programas de descuento por primas.


## Coordinación entre agentes e intermediarios

Permita una comunicación y coordinación personalizadas entre los clientes y sus agentes o agentes asignados en función de las necesidades de las directivas, el historial de servicios y las preferencias. Una mejor coordinación crea una experiencia perfecta en la que los clientes se sienten respaldados por un asesor experto que entiende su relación completa.

### Impacto empresarial

Las comunicaciones eficaces de coordinación entre agentes y agentes suelen dar como resultado una mejora del 35 al 45 por ciento en la participación de los agentes, lo que conduce a relaciones de cliente más sólidas y a una mayor retención impulsada por interacciones de asesoramiento de confianza.

### Cómo implementar

Usar el patrón [Activación de mensaje saliente por lotes](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). La mejor manera de coordinar a los agentes es mediante activaciones por lotes programadas que les proporcionen a los agentes listas de contacto con los clientes, puntos de conversación y acciones recomendadas prioritarias en una cadencia regular.

### Consideraciones técnicas

- Integre con el sistema de administración de agentes para mantener asignaciones precisas de agente-cliente y garantizar que las comunicaciones reflejen la relación correcta, especialmente durante las transiciones de agentes.
- Diseñe la activación de datos en el portal del agente para que los agentes reciban una vista consolidada de las perspectivas del cliente, las próximas renovaciones y las acciones recomendadas sin exponer los datos de comportamiento sin procesar.
- Aplique etiquetas de gobernanza de datos para restringir qué elementos de datos del cliente se comparten con socios de corredores externos en comparación con agentes cautivos, respetando los límites contractuales y regulatorios de uso compartido de datos.
- Implemente bucles de comentarios desde las interacciones del agente de nuevo en el perfil del cliente, de modo que los datos de las conversaciones telefónicas o en persona enriquezcan la vista unificada y mejoren la personalización futura.


## Respuesta a evento catastrófico

Comuníquese proactivamente con los clientes en las áreas afectadas durante desastres naturales o eventos catastróficos con información de apoyo personalizada, guía de presentación de reclamaciones y recursos de emergencia. Un alcance rápido y empático durante una crisis demuestra el compromiso de la aseguradora de estar ahí cuando los clientes más lo necesitan.

### Impacto empresarial

Las comunicaciones proactivas de respuesta a eventos catastróficos generalmente logran una mejora del 60 al 70 por ciento en las tasas de comunicación de los clientes durante los eventos, lo que acelera significativamente la presentación de reclamaciones y fortalece la confianza y lealtad de los clientes a largo plazo.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Las declaraciones de sucesos catastróficos constituyen déclencheur prioritarios para una comunicación inmediata y personalizada con todos los asegurados de la zona geográfica afectada.

### Consideraciones técnicas

- Integrarse rápidamente con los servicios de monitoreo de catástrofes y las fuentes de declaración de catástrofes del gobierno a las comunicaciones de déclencheur cuando se declaran eventos para áreas geográficas específicas.
- Genere segmentos geográficos de audiencia utilizando los datos de direcciones de los asegurados e información de ubicación de propiedades para identificar con precisión a los clientes en la zona afectada sin sobrecomunicar a los clientes no afectados.
- Configure el enrutamiento de mensajes de alta prioridad que anula las reglas estándar de restricción y supresión de frecuencia para garantizar la seguridad crítica y que la información de las reclamaciones llegue a los clientes inmediatamente.
- Genere plantillas de mensajes y configuraciones de recorrido previamente para tipos de eventos catastróficos comunes, de modo que las comunicaciones se puedan activar pocas horas después de una declaración de evento en lugar de requerir la creación de contenido durante la crisis.
