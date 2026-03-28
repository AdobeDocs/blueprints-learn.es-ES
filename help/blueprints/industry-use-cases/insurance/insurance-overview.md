---
title: Casos de uso del seguro
description: Descubra cómo las organizaciones de seguros utilizan Adobe Experience Platform para personalizar la administración de pólizas, mejorar las experiencias de las reclamaciones e impulsar la retención de clientes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: a082598f-555b-49a4-b201-a55bee793959
source-git-commit: 3542d76106fada9019b70a8cc9fd4c74872d4995
workflow-type: tm+mt
source-wordcount: '3016'
ht-degree: 0%

---

# Casos de uso del seguro

Las organizaciones de seguros utilizan Adobe Experience Platform para unificar los datos del asegurado en los sistemas de gestión de pólizas, reclamaciones y participación para ofrecer comunicaciones personalizadas en cada fase de la relación con los clientes. Al conectar las señales de comportamiento con la información de la póliza y las reclamaciones, las aseguradoras pueden atraer de forma proactiva a los clientes con ofertas relevantes, actualizaciones de servicio oportunas y una asistencia significativa que aumente la retención y el valor de la duración.

## Campañas de renovación de directivas

Envíe recordatorios y ofertas personalizados de renovación de pólizas en función del historial de pólizas, el registro de reclamaciones y las preferencias de cobertura de cada cliente. El alcance oportuno y relevante de la renovación reduce las tasas de caída de las políticas y fortalece las relaciones con los clientes a largo plazo al facilitar a los asegurados comprender sus opciones y tomar medidas.

### Impacto empresarial

Las organizaciones que implementan campañas personalizadas de renovación de políticas ven mejoradas las tasas de renovación, lo que reduce directamente la pérdida de clientes y protege los ingresos recurrentes por primas.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Este método crea una secuencia de renovación cronometrada que progresa desde la notificación inicial a través de recordatorios escalonados y, si es necesario, un mensaje de urgencia final, adaptando la cadencia y la oferta en función de si el tomador del seguro ha realizado toques anteriores. Este es el patrón correcto cuando el tiempo está gobernado por una fecha de contrato en lugar de un evento de cliente discreto, y la intención empresarial requiere un flujo secuenciado de varios mensajes durante 30 días o más con ramificación condicional basada en la participación: la mensajería activada por evento gestiona las respuestas reactivas a eventos discretos, pero no puede dar cabida a la lógica de programación basada en calendario o a las dependencias de escalación necesarias para una campaña de renovación.

### Consideraciones técnicas

- Integrarse con el sistema de gestión de políticas para recibir eventos de fecha de renovación y detalles de políticas actuales, asegurándose de que los mensajes reflejen una cobertura precisa y la información de primas.
- Aplique etiquetas de gobernanza de datos a todos los datos de políticas financieras y de identificación personal para cumplir con las regulaciones de seguros estatales y los requisitos de privacidad de datos.
- Configure reglas de supresión para evitar que se envíen mensajes de renovación a los tomadores de seguros que ya hayan renovado o que tengan reclamaciones activas que puedan afectar a sus condiciones de renovación.
- Coordine el tiempo con las asignaciones de agentes o agentes para que los mensajes directos al cliente se alineen con cualquier alcance que el agente asignado también pueda estar realizando.


## Recomendaciones de productos de venta cruzada

Recomiende productos de seguro adicionales, como cobertura de vida, vivienda o automóviles, en función de las pólizas existentes, la etapa de vida y el perfil de riesgo de cada cliente. Las recomendaciones personalizadas de productos ayudan a los asegurados a descubrir brechas de cobertura y construir una cartera de protección más completa.

### Impacto empresarial

Las recomendaciones de venta cruzada personalizadas mejoran las tasas de conversión de venta cruzada, lo que aumenta las políticas por hogar y el valor de vida útil general del cliente.

### Cómo implementar

Usar el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). La toma de decisiones en tiempo real evalúa la cobertura, la fase de vida y las señales de comportamiento existentes de cada cliente para seleccionar la recomendación de producto más relevante del catálogo disponible. Este es el patrón correcto cuando la selección de productos debe tener en cuenta las reglas de elegibilidad, las directrices de suscripción y los requisitos de idoneidad regulatoria, restricciones que requieren una lógica de toma de decisiones regida en lugar de una clasificación de afinidad de comportamiento por sí sola.

### Consideraciones técnicas

- Integre los datos de directivas de todas las líneas de productos en un perfil de cliente unificado para que el motor de decisión tenga una vista completa de la cobertura existente al seleccionar recomendaciones.
- Configure reglas de idoneidad dentro del modelo de toma de decisiones para excluir los productos que un cliente ya tiene o que entran en conflicto con las directrices de suscripción para su perfil de riesgo.
- Póngase en contacto con los equipos legales y de cumplimiento para validar que las reglas de elegibilidad de recomendaciones de productos se alinean con los requisitos de idoneidad y marketing de seguros del estado aplicables antes del lanzamiento.
- Coordine el resultado de la toma de decisiones con el portal del agente para que los productos recomendados sean visibles para los agentes asignados que puedan estar teniendo conversaciones directas con el cliente.


## Personalization de proceso de reclamaciones

Personalice las comunicaciones del proceso de reclamaciones, las actualizaciones de estado y los recursos de asistencia en función del tipo de reclamación, las preferencias del cliente y el historial de reclamaciones. Una experiencia de reclamaciones transparente y bien comunicada reduce la ansiedad durante los momentos de estrés y genera una confianza duradera con los asegurados.

### Impacto empresarial

Las comunicaciones personalizadas de reclamaciones logran mejores puntuaciones de satisfacción de reclamaciones, reduciendo las quejas y reforzando la probabilidad de renovación de la política después de una reclamación.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). El proceso de reclamos es una experiencia de varias etapas con diferentes fases (presentación, investigación, ajuste y liquidación), cada una de las cuales requiere comunicaciones adaptadas y tiempo de adaptación. Este es el patrón correcto cuando el caso de uso requiere un flujo secuenciado de varios mensajes a lo largo de días con ramificación condicional basada en eventos de estado de notificaciones: un solo mensaje activado no puede dar cabida a la lógica de dependencia entre fases de notificaciones secuenciales.

### Consideraciones técnicas

- Integre con el sistema de administración de reclamaciones para recibir eventos de cambio de estado en tiempo real que hagan avanzar al cliente a través de la fase de recorrido adecuada.
- Lógica de ramificación de recorrido de diseño que adapta el tono y el contenido de la mensajería en función del tipo de reclamación, como la colisión automática frente a las reclamaciones por daños a la propiedad frente a las reclamaciones de responsabilidad.
- Implemente reglas de supresión durante las investigaciones de reclamaciones activas para evitar que los mensajes de marketing o de venta cruzada lleguen a los clientes en momentos confidenciales.
- Asegúrese de que todos los datos relacionados con las reclamaciones que fluyen al perfil del cliente estén etiquetados con las restricciones de control de datos adecuadas para evitar su uso fuera de las comunicaciones del servicio.


## Evaluación y prevención de riesgos

Proporcione información personalizada de evaluación de riesgos y consejos de prevención en función del tipo de política, la ubicación geográfica y los factores de riesgo específicos de cada cliente. La educación proactiva del riesgo ayuda a los asegurados a reducir su exposición a las pérdidas, beneficiando tanto al cliente como a la aseguradora.

### Impacto empresarial

El alcance personalizado de la prevención de riesgos impulsa una mejor participación en la prevención, lo que contribuye a reducir la frecuencia de las reclamaciones y a mejorar la satisfacción del cliente.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). La educación para la prevención de riesgos es más eficaz como un recorrido multi-táctil sostenido que ofrece una orientación relevante a lo largo del tiempo y se adapta en función de la participación del cliente y los factores de riesgo estacionales. Este es el patrón correcto cuando el recorrido debe entregar contenido durante períodos prolongados con ajustes de temporización estacionales y ramas basadas en la participación; la mensajería activada por eventos no puede gestionar la programación predictiva o la cadencia de varios pasos necesaria para una educación sostenida.

### Consideraciones técnicas

- Integre con proveedores de datos de riesgo de terceros para obtener información sobre el clima, el peligro geográfico y el riesgo inmobiliario que enriquezca los perfiles de los clientes con puntuaciones de riesgo específicas de la ubicación.
- Diseñe una lógica de recorrido estacional que ofrezca contenido relevante antes de los períodos de alto riesgo, como la preparación para la temporada de huracanes para los asegurados costeros o consejos sobre el clima invernal para los clientes de clima frío.
- Aplicar etiquetas de gobernanza de datos para distinguir los datos de evaluación de riesgos utilizados para la educación de los clientes de los datos utilizados en las decisiones de suscripción actuarial.
- Coordinar el contenido de prevención de riesgos con la cobertura específica del asegurado para que las recomendaciones sean relevantes para los peligros que realmente cubre su póliza.


## Notificaciones de cambio de directiva

Envíe notificaciones personalizadas sobre cambios de políticas, actualizaciones de cobertura y nuevas opciones en función de las preferencias de políticas y comunicaciones específicas de cada cliente. Las notificaciones claras y oportunas mantienen informados a los asegurados y reducen la confusión sobre su estado de cobertura.

### Impacto empresarial

Las notificaciones personalizadas de cambio de póliza logran tasas de reconocimiento de notificaciones mejoradas, reduciendo las consultas de servicio al cliente y mejorando la comprensión general del asegurado.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de cambio de directivas del sistema de administración sirven como déclencheur naturales para las notificaciones inmediatas y relevantes a través del canal preferido de cada cliente. Este es el patrón correcto cuando el déclencheur es un evento del sistema (cambio de política) en lugar de una conducta del cliente, y la comunicación necesaria es inmediata y reactiva en lugar de una secuencia de nutrición sostenida.

### Consideraciones técnicas

- Integrarse con el sistema de administración de políticas para capturar eventos de cambio de aprobación, modificación y renovación en tiempo real, lo que garantiza que las notificaciones reflejen el estado de la política más actual.
- Póngase en contacto con su equipo legal para confirmar que las notificaciones de cambio de directiva cumplen con los requisitos de tiempo, idioma y canal de entrega establecidos por el estado antes de activar las comunicaciones automatizadas.
- Configure la lógica de prioridad de canal en función de la urgencia y el tipo de cambio; por ejemplo, las reducciones de cobertura pueden justificar canales más inmediatos que las actualizaciones informativas.
- Mantenga una pista de auditoría de entrega para todas las notificaciones de cambio de política con el fin de admitir la documentación de cumplimiento normativo y la resolución de disputas.


## Recuperación de abandono de presupuesto

Vuelva a atraer a los clientes que empezaron pero no completaron una cotización de seguro con mensajes de seguimiento personalizados y ofertas adaptadas. El alcance de la recuperación oportuna lleva a los clientes potenciales de nuevo al proceso de cotización y aborda las barreras comunes para la finalización.

### Impacto empresarial

Las campañas de recuperación del abandono de cotizaciones mejoran las tasas de finalización de las cotizaciones, convirtiendo a más posibles clientes en titulares de pólizas y reduciendo los costes de adquisición de clientes.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). El abandono de las cotizaciones es un evento de comportamiento que déclencheur un seguimiento oportuno mientras el interés y la intención del posible cliente siguen siendo frescos. Este es el patrón correcto cuando el déclencheur es un comportamiento de cliente discreto (abandono) y la respuesta necesaria es una renovación de la participación sensible al tiempo, en lugar de una secuencia de nutrición de varios pasos o una decisión de oferta compleja.

### Consideraciones técnicas

- Integre con la plataforma de cotización en línea para capturar eventos de abandono junto con los detalles de la cotización que el cliente ya había proporcionado, lo que permite una renovación de la participación personalizada.
- Configurar reglas de tiempo que equilibren la urgencia con el respeto: seguimiento inicial en cuestión de horas, con un número limitado de recordatorios posteriores en los días siguientes.
- Aplique reglas de consentimiento y privacidad para garantizar que el seguimiento solo se envíe a los posibles clientes que hayan elegido participar en comunicaciones de marketing, especialmente a los clientes que aún no hayan establecido una relación de directiva.
- Incluya vínculos profundos que devuelvan al cliente potencial directamente a su cotización guardada en lugar de exigirle que reinicie el proceso desde el principio.


## Oportunidades de Descuento y Ahorro

Identifique y comunique oportunidades de descuento personalizadas, como paquetes, controladores seguros, fidelidad y descuentos de facturación electrónica, en función del perfil y el comportamiento de cada cliente. Las comunicaciones proactivas de ahorro demuestran valor y fortalecen la relación precio-valor.

### Impacto empresarial

Las comunicaciones personalizadas de descuentos y ahorros mejoran las tasas de utilización de los descuentos, mejoran la satisfacción del cliente y reducen la pérdida basada en los precios.

### Cómo implementar

Usar el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Real-time Decisioning evalúa la elegibilidad de cada cliente para los descuentos disponibles y selecciona la oportunidad de ahorro más impactante para presentar en el momento adecuado. Este es el patrón correcto cuando la selección de descuentos debe tener en cuenta las limitaciones de apilamiento, las restricciones regulatorias y los cálculos actuariales precisos, restricciones que requieren una lógica de toma de decisiones regida en lugar de simples comprobaciones de elegibilidad solamente.

### Consideraciones técnicas

- Integre con los sistemas de clasificación de pólizas y facturación para calcular la elegibilidad exacta del descuento y las cantidades de ahorro potencial para cada cliente en tiempo real.
- Configure reglas de decisión que tengan en cuenta las limitaciones de apilamiento de descuentos y garantice que las cantidades de ahorro comunicadas sean precisas actuarialmente y aprobadas por el equipo de asignación de precios.
- Aplique reglas reguladoras específicas del estado a las comunicaciones de descuento, ya que ciertos estados tienen restricciones sobre cómo se pueden comercializar y aplicar los descuentos de seguro.
- Realice un seguimiento de los resultados de adopción de descuentos para perfeccionar continuamente el modelo de toma de decisiones y priorizar los mensajes de ahorro que más interesan a los distintos segmentos de clientes.


## Prevención de fraude de reclamaciones

Utilice la detección inteligente de fraudes para identificar patrones de reclamaciones sospechosas y personalizar las comunicaciones de investigación al tiempo que mantiene la confianza de los clientes. La prevención eficaz del fraude protege a los asegurados honestos al mantener las primas justas y garantizar que las reclamaciones legítimas se procesen rápidamente.

### Impacto empresarial

Los programas inteligentes de prevención del fraude de reclamaciones logran mejores tasas de detección del fraude, reduciendo los pagos fraudulentos y reduciendo los costes generales de las reclamaciones.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de puntuación de riesgo de fraude déclencheur comunicaciones de investigación y ajustes de proceso adecuados en tiempo real, lo que garantiza que las reclamaciones marcadas reciban atención inmediata. Este es el patrón correcto cuando un evento derivado del sistema (puntuación de riesgo de fraude) es el déclencheur y la acción necesaria es el ajuste inmediato del proceso interno con una comunicación cuidadosa con el cliente, en lugar de un recorrido de varios pasos o un escenario de toma de decisiones.

### Consideraciones técnicas

- Integre las puntuaciones de riesgo de fraude del sistema de análisis de reclamaciones en el perfil del cliente, al tiempo que aplica etiquetas estrictas de gobernanza de datos para evitar que los datos de investigación de fraude aparezcan en comunicaciones dirigidas al cliente.
- Diseñe rutas de comunicación que mantengan un tono profesional y respetuoso para los clientes cuyas reclamaciones están en revisión, preservando la relación independientemente del resultado de la investigación.
- Implemente controles de acceso basados en funciones para garantizar que los indicadores de fraude solo estén visibles para los equipos de investigación autorizados y que nunca aparezcan en las vistas estándar del agente o del servicio al cliente.
- Coordínese con el servicio de resolución de identidades [!DNL Adobe Experience Platform] para detectar patrones en perfiles relacionados, como direcciones compartidas o números de teléfono vinculados a varias notificaciones sospechosas.


## Programas de Bienestar y Prevención

Personalice las comunicaciones del programa de bienestar, los recordatorios de participación y las notificaciones de recompensa para los clientes de seguros de salud y vida en función de sus objetivos y nivel de participación. Los programas activos de bienestar mejoran los resultados de salud de los asegurados y construyen una base de clientes más fuerte y comprometida.

### Impacto empresarial

Las comunicaciones personalizadas del programa de bienestar y prevención impulsan mejores tasas de participación en el programa, lo que contribuye a mejores resultados de salud y a una menor frecuencia de reclamaciones.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Los programas de bienestar son experiencias de participación sostenida con hitos, desafíos y recompensas que requieren orquestación adaptativa basada en la actividad y el progreso de cada participante. Este es el patrón correcto cuando el caso de uso requiere un flujo de varios mensajes a largo plazo con ramas basadas en la participación y ajustes de tiempo adaptables: la mensajería activada por eventos no puede gestionar la compleja lógica de hito ni la necesidad de ajustar la cadencia de la comunicación en función del seguimiento de actividad sostenido.

### Consideraciones técnicas

- Integre con fuentes de datos de aplicaciones de salud y dispositivos portátiles usando la ingesta de transmisión [!DNL Adobe Experience Platform], aplicando etiquetas de control de datos claras para distinguir los datos de salud de los datos de suscripciones o reclamaciones.
- Implemente mecanismos de consentimiento independientes para la recopilación de datos de bienestar a fin de garantizar que los participantes comprendan cómo se utilizan los datos de sus actividades de salud y puedan excluirse sin afectar a su política.
- Diseñe una lógica de recorrido que ajuste la intensidad del programa y la frecuencia de la comunicación en función del nivel de participación de cada participante para evitar la fatiga y fomentar la participación sostenida.
- Involucre a sus equipos legales y de cumplimiento para revisar las estructuras de incentivos de bienestar y los programas de descuento por primas para el cumplimiento con las regulaciones de seguros estatales aplicables antes del lanzamiento.


## Coordinación entre agentes e intermediarios

Permita una comunicación y coordinación personalizadas entre los clientes y sus agentes o agentes asignados en función de las necesidades de las directivas, el historial de servicios y las preferencias. Una mejor coordinación crea una experiencia perfecta en la que los clientes se sienten respaldados por un asesor experto que entiende su relación completa.

### Impacto empresarial

Las comunicaciones eficaces de coordinación entre agentes y agentes resultan en una participación mejorada de los agentes, lo que conduce a relaciones de cliente más sólidas y a una mayor retención impulsada por interacciones de asesoramiento de confianza.

### Cómo implementar

Usar el patrón [Activación de mensaje saliente por lotes](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). La mejor manera de coordinar a los agentes es mediante activaciones por lotes programadas que les proporcionen a los agentes listas de contacto con los clientes, puntos de conversación y acciones recomendadas prioritarias en una cadencia regular. Este es el patrón correcto cuando la audiencia es grande y está predefinida, el tiempo de envío se programa de forma recurrente en lugar de depender de un evento y no se requiere bifurcación ni toma de decisiones en tiempo real.

### Consideraciones técnicas

- Integre con el sistema de administración de agentes para mantener asignaciones precisas de agente-cliente y garantizar que las comunicaciones reflejen la relación correcta, especialmente durante las transiciones de agentes.
- Diseñe la activación de datos en el portal del agente para que los agentes reciban una vista consolidada de las perspectivas del cliente, las próximas renovaciones y las acciones recomendadas sin exponer los datos de comportamiento sin procesar.
- Aplique etiquetas de gobernanza de datos para restringir qué elementos de datos del cliente se comparten con socios de corredores externos en comparación con agentes cautivos, respetando los límites contractuales y regulatorios de uso compartido de datos.
- Implemente bucles de comentarios desde las interacciones del agente de nuevo en el perfil del cliente, de modo que los datos de las conversaciones telefónicas o en persona enriquezcan la vista unificada y mejoren la personalización futura.


## Respuesta a evento catastrófico

Comuníquese proactivamente con los clientes en las áreas afectadas durante desastres naturales o eventos catastróficos con información de apoyo personalizada, guía de presentación de reclamaciones y recursos de emergencia. Un alcance rápido y empático durante una crisis demuestra el compromiso de la aseguradora de estar ahí cuando los clientes más lo necesitan.

### Impacto empresarial

Las comunicaciones proactivas de respuesta a eventos catastróficos logran mejores tasas de comunicación con los clientes durante los eventos, lo que acelera la presentación de reclamaciones y fortalece la confianza y lealtad de los clientes a largo plazo.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Las declaraciones de sucesos catastróficos constituyen déclencheur prioritarios para una comunicación inmediata y personalizada con todos los asegurados de la zona geográfica afectada. Este es el patrón correcto cuando un evento externo de alta prioridad es el déclencheur y la respuesta necesaria es un alcance geográfico inmediato y amplio con información crítica en el tiempo, en lugar de patrones de conducta de clientes individuales o secuencia compleja.

### Consideraciones técnicas

- Integrarse rápidamente con los servicios de monitoreo de catástrofes y las fuentes de declaración de catástrofes del gobierno a las comunicaciones de déclencheur cuando se declaran eventos para áreas geográficas específicas.
- Genere segmentos geográficos de audiencia utilizando los datos de direcciones de los asegurados e información de ubicación de propiedades para identificar con precisión a los clientes en la zona afectada sin sobrecomunicar a los clientes no afectados.
- Configure el enrutamiento de mensajes de alta prioridad que anula las reglas estándar de restricción y supresión de frecuencia para garantizar la seguridad crítica y que la información de las reclamaciones llegue a los clientes inmediatamente.
- Genere plantillas de mensajes y configuraciones de recorrido previamente para tipos de eventos catastróficos comunes, de modo que las comunicaciones se puedan activar pocas horas después de una declaración de evento en lugar de requerir la creación de contenido durante la crisis.


## Personalization de contenido del portal del asegurado

Personalice el portal de autoservicio autenticado y la experiencia de la aplicación móvil para los asegurados mostrando la información de cobertura, las herramientas y los recursos más relevantes en función de su comportamiento de navegación, el portafolio de políticas y las interacciones de servicio recientes. Un portal que se adapta al contexto actual de cada asegurado reduce la fricción y facilita a los clientes encontrar lo que necesitan cuando lo necesitan.

### Impacto empresarial

La personalización de la experiencia del portal del asegurado aporta mejoras mensurables en la finalización de tareas de autoservicio y la participación digital, reduciendo el volumen del centro de contacto entrante y reforzando la satisfacción del cliente con el canal digital.

### Cómo implementar

Usar el patrón [Behavioral Recommendations](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Las señales de comportamiento de las sesiones de portal autenticadas (uso de la calculadora de cobertura, vistas de documentos de pólizas, comprobaciones de estado de reclamaciones y participación en temas de preguntas frecuentes) forman un modelo de recomendación que muestra dinámicamente el contenido y las herramientas más relevantes para el contexto actual de cada asegurado. Este es el patrón correcto cuando la personalización está impulsada por señales de comportamiento implícitas dentro de una sesión autenticada y el objetivo es la clasificación de relevancia de un catálogo de contenido o recursos, en lugar de Offer Decisioning, que requiere elegibilidad regida y aprobación actuarial antes de presentar una oferta de producto, o Cross-Channel with Decisioning, que es más adecuado al coordinar una oferta de producto en varios canales.

### Consideraciones técnicas

- Aplique etiquetas de gobernanza de datos a las señales de comportamiento recopiladas en el portal del asegurado para distinguir los análisis de participación de los datos de seguros regulados, y restrinja cualquier señal derivada del historial de reclamaciones de fluir hacia modelos de personalización sin una revisión actuarial y de cumplimiento explícita.
- Integrar el modelo conductual con el sistema de gestión de políticas para asegurar que las recomendaciones de contenido y herramientas reflejen la cartera de políticas activa de cada asegurado, mostrando herramientas de cobertura automática para asegurados automáticos y recursos de propiedad para propietarios de viviendas, sin exponer los datos de políticas brutas al modelo de recomendaciones más allá de la clasificación de la línea de productos.
- Implemente controles de cumplimiento específicos del estado para garantizar que la personalización del comportamiento no constituya una recomendación de seguro o una solicitud de marketing según las regulaciones estatales aplicables, especialmente cuando las señales de comportamiento podrían implicar la detección de brechas de cobertura.
- Coordine las señales de personalización del portal con el portal del agente para que los agentes que atienden a los asegurados que han mostrado un fuerte comportamiento de investigación de autoservicio reciban una vista consolidada de la participación digital del cliente junto con su historial de servicios.
