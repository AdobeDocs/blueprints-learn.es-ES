---
title: Casos de uso de atención sanitaria
description: Descubra cómo las organizaciones de atención médica utilizan Adobe Experience Platform para mejorar la participación de los pacientes, optimizar la coordinación de la atención e impulsar mejores resultados en materia de salud.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 8da82711-a783-488d-a0ed-070b33ecbbc4
source-git-commit: 0236bd326730ee9a0be621ee0e60ddc3d352410d
workflow-type: tm+mt
source-wordcount: '3818'
ht-degree: 0%

---

# Casos de uso de atención sanitaria

Las organizaciones de atención sanitaria utilizan Adobe Experience Platform para crear perfiles unificados de pacientes y ofrecer comunicaciones personalizadas y oportunas en todos los puntos de contacto. Al conectar los datos clínicos, de comportamiento y de preferencias en un solo lugar, los equipos de atención pueden atraer a los pacientes de forma más eficaz, manteniendo al mismo tiempo los más altos estándares de privacidad y cumplimiento.

>[!IMPORTANT]
>Los casos de uso de atención médica implican información médica protegida (PHI) sujeta a la HIPAA y otras regulaciones aplicables. Antes de implementar cualquiera de estos patrones, asegúrese de que [!DNL Adobe Experience Platform] esté aprovisionado como un servicio apto para HIPAA y de que se haya establecido un Contrato de socio comercial (BAA) con Adobe. Las consideraciones técnicas de cada sección destacan los requisitos de cumplimiento clave, pero no son exhaustivas. Trabaje con sus equipos jurídicos, de cumplimiento normativo y de seguridad para validar su implementación con respecto a todos los requisitos regulatorios aplicables.

## Automatización de recordatorio de cita

Envíe recordatorios de cita personalizados por correo electrónico, mensajes de texto y notificaciones push en función de las preferencias de comunicación y el tipo de cita de cada paciente. Los recordatorios automatizados reducen las citas perdidas y mantienen los horarios funcionando sin problemas, lo que permite que el personal se concentre en la atención del paciente.

### Impacto empresarial

Las organizaciones que implementan recordatorios de citas automatizadas ven mejoras mensurables en las tasas de citas demostradas y una reducción significativa en las no-presentaciones costosas.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de creación y actualización de citas del sistema de programación sirven como déclencheur naturales para mensajes recordatorios oportunos y relevantes. Este es el patrón correcto cuando el déclencheur es un evento de cita discreta y la respuesta necesaria es una notificación única, con distinción de tiempo, en lugar de una secuencia de participación sostenida, ya que los pacientes necesitan confirmación inmediata sin pasos de seguimiento.

### Consideraciones técnicas

- Asegúrese de que toda la información de contacto del paciente y los detalles de la cita se transmitan y almacenen de acuerdo con los requisitos de la HIPAA, utilizando etiquetas de uso de datos adecuadas para restringir el acceso no autorizado.
- Integrarse con el sistema electrónico de programación de registros médicos para capturar la creación de citas, la cancelación y la reprogramación de eventos en tiempo real.
- Aplique políticas de administración de consentimiento para que los recordatorios solo se envíen a través de los canales en los que el paciente ha decidido participar explícitamente.
- Configure reglas de supresión para evitar recordatorios duplicados o excesivos cuando las citas se vuelvan a programar en sucesión rápida.


## Campañas de adherencia a medicamentos

Envíe recordatorios personalizados y contenido educativo para ayudar a los pacientes a mantenerse al día con sus horarios de medicación y planes de tratamiento. La mensajería personalizada basada en el tipo de medicamento, el horario de dosificación y los antecedentes de los pacientes mejora la adherencia y mejora los resultados de salud.

### Impacto empresarial

Las campañas personalizadas de adherencia a la medicación ayudan a mejorar las tasas de adherencia, lo que conduce a mejores resultados de salud y menos reingresos hospitalarios.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). El cumplimiento de la medicación requiere un enfoque sostenido y multitáctil con recordatorios crecientes, puntos de contacto educativos y chequeos de seguimiento durante el transcurso de un plan de tratamiento. Este es el patrón correcto porque la administración de medicamentos requiere un flujo secuenciado de varios mensajes a lo largo de días o semanas con ramas condicionales basadas en eventos de recarga y señales de participación; un solo mensaje activado no puede acomodar la lógica de dependencia entre los pasos educativos y las rutas de escalación.

### Consideraciones técnicas

- Aplique etiquetas estrictas de uso de datos a toda la información de salud protegida relacionada con los datos de medicamentos y diagnósticos para evitar la activación descendente no autorizada.
- Integrarse con los sistemas de farmacia y registros electrónicos de salud para recibir los datos de llenado y recarga de recetas que déclencheur los pasos de recorrido.
- Implementar una gestión de consentimiento sólida para garantizar que los pacientes hayan aceptado recibir comunicaciones relacionadas con la medicación y puedan retirar el consentimiento en cualquier momento.
- Diseñe una lógica de recorrido para detectar patrones de no participación y escalar a las notificaciones del equipo de atención cuando un paciente pueda estar en riesgo de no cumplimiento.


## Recordatorios de atención preventiva

Recuerde proactivamente a los pacientes sobre la atención preventiva recomendada, como vacunas, exámenes y revisiones anuales en función de su edad, antecedentes médicos y factores de riesgo. Los recordatorios oportunos de atención preventiva ayudan a cerrar las brechas en la atención y mejorar la salud general de la población.

### Impacto empresarial

El alcance de la atención preventiva proactiva mejora las tasas de finalización de la atención preventiva, lo que contribuye a mejorar la salud de la población y a reducir los costos del tratamiento a largo plazo.

### Cómo implementar

Usar el patrón [Activación de mensaje saliente por lotes](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). Los recordatorios de atención preventiva se entregan mejor a través de campañas programadas por lotes que evalúan la elegibilidad del paciente en comparación con las directrices clínicas en una cadencia regular. Este es el patrón correcto cuando la audiencia está predefinida por criterios de directrices clínicas, el tiempo de envío se programa en una cadencia regular en lugar de depender del evento, y no se requiere bifurcación o toma de decisiones en tiempo real.

### Consideraciones técnicas

- Genere segmentos de audiencia utilizando criterios de directrices clínicas (edad, sexo, antecedentes familiares, fechas de detección previas) mientras aplica etiquetas de uso de datos a toda la información de salud protegida que se usa en la segmentación.
- Coordine con los equipos clínicos para asegurarse de que el contenido del recordatorio se ajuste a las directrices de atención preventiva actuales basadas en la evidencia y a los protocolos organizativos.
- Implemente un límite de frecuencia para evitar abrumar a los pacientes que cumplen con los requisitos para recibir múltiples recomendaciones de atención preventiva simultáneamente.
- Mantener una pista de auditoría de todas las comunicaciones de atención preventiva enviadas para la presentación de informes reglamentarios y la documentación de medidas de calidad.


## Campañas de seguimiento posteriores a la visita

Envíe automáticamente encuestas posteriores a la visita, instrucciones de atención y recordatorios de citas de seguimiento en función del tipo de visita y de las necesidades específicas de cada paciente. El seguimiento oportuno mejora la satisfacción del paciente y garantiza la continuidad de la atención después de cada encuentro.

### Impacto empresarial

Las campañas automatizadas de seguimiento después de la visita logran tasas de respuesta mejoradas y puntuaciones de satisfacción del paciente más altas.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de finalización de visitas del sistema de registros electrónicos de salud proporcionan un déclencheur natural y oportuno para las comunicaciones de seguimiento adaptadas al tipo de encuentro. Este es el patrón correcto cuando el déclencheur es un evento de finalización de visita discreta y la respuesta necesaria es un seguimiento inmediato adaptado al tipo de encuentro, en lugar de una secuencia de varios pasos, ya que cada visita genera su propia necesidad de seguimiento independiente.

### Consideraciones técnicas

- Integrarse con el sistema de registros electrónicos de salud para recibir eventos de alta por visita que incluyen tipo de visita, proveedor e instrucciones de atención relevantes sin exponer las notas clínicas completas.
- Aplique etiquetas de uso de datos a cualquier contenido de instrucciones de atención médica para garantizar que la información médica protegida se comparta únicamente a través de canales seguros y autorizados por el paciente.
- Configure reglas de tiempo que tengan en cuenta el tipo de visita; por ejemplo, los controles postquirúrgicos pueden requerir un tiempo diferente al de las revisiones de rutina.
- Incluya enlaces seguros al portal del paciente para la finalización de la encuesta y la programación de citas en lugar de recopilar información médica a través de canales no seguros.


## Programas de manejo de enfermedades crónicas

Personalice las comunicaciones sobre el manejo de enfermedades crónicas, el contenido educativo y los recordatorios de monitoreo basados en la condición específica y el plan de tratamiento de cada paciente. La participación sostenida y relevante ayuda a los pacientes a tomar un papel activo en la gestión de su salud a lo largo del tiempo.

### Impacto empresarial

Los programas personalizados de manejo de enfermedades crónicas ven mayores tasas de participación en el programa, lo que conduce a mejores resultados de manejo de enfermedades y a una menor utilización de la atención de emergencia.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). La gestión de enfermedades crónicas es inherentemente una experiencia de largo plazo, con múltiples puntos de contacto que requiere mensajes adaptables basados en la participación del paciente y los hitos de salud. Este es el patrón correcto porque la gestión de enfermedades crónicas requiere mensajes adaptativos durante un período prolongado con ramificación condicional basada en métricas clínicas y patrones de participación; la mensajería activada por eventos no puede manejar la reevaluación dinámica y continua necesaria para ajustar las intervenciones en función de los datos de salud en evolución.

### Consideraciones técnicas

- Diseñe una lógica de ramificación de recorridos que se adapte en función de las métricas específicas de la enfermedad (por ejemplo, las tendencias de la glucosa en sangre para el tratamiento de la diabetes o las lecturas de la presión arterial para los programas de hipertensión).
- Implemente un control de datos estricto con [!DNL Adobe Experience Platform] etiquetas de uso de datos para clasificar y proteger los datos de mantenimiento específicos de la condición en todo el recorrido.
- Integre con dispositivos remotos de monitorización de pacientes y sistemas de resultados informados por los pacientes para alimentar los datos de salud en tiempo real en los puntos de decisión del recorrido.
- Cree rutas de escalación del equipo de atención médica dentro del recorrido para que la falta de participación o las tendencias sanitarias generen déclencheur de alerta para el personal clínico apropiado.


## Nuevo Recorrido de incorporación del paciente

Automatice un recorrido de incorporación de varios pasos para nuevos pacientes que incluya información de bienvenida, instrucciones de acceso al portal del paciente y guía de programación de citas. Una experiencia de incorporación sin problemas marca la pauta para una relación de paciente comprometida y a largo plazo.

### Impacto empresarial

Los nuevos recorridos automatizados de incorporación del paciente ayudan a mejorar las tasas de activación del portal y a aumentar la participación temprana del paciente.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). La incorporación del paciente es un proceso naturalmente secuencial de varios pasos en el que cada comunicación se basa en la anterior y se adapta en función de si el paciente ha completado acciones clave. Este es el patrón correcto porque la incorporación requiere un flujo secuenciado y dependiente durante varios días con ramificación basada en las acciones del paciente (activación del portal, finalización del formulario): un solo mensaje o enfoque por lotes no puede dar cabida a las interdependencias entre pasos ni adaptarse a la finalización progresiva.

### Consideraciones técnicas

- Integrarse con el sistema de registro de pacientes para almacenar en déclencheur el recorrido de incorporación inmediatamente después de la creación de la nueva historia clínica del paciente, lo que garantiza una primera impresión oportuna.
- Utilice la resolución de identidad para combinar cualquier registro preexistente (por ejemplo, de una visita al sitio web o una solicitud de cita) con el nuevo perfil del paciente para evitar comunicaciones duplicadas.
- Asegúrese de que los vínculos y las credenciales de activación del portal se entreguen a través de canales seguros y compatibles con HIPAA y caduquen después de un periodo definido.
- Diseñe el recorrido para detectar los eventos de activación del portal y de finalización del formulario, de modo que los pasos siguientes se adapten en lugar de repetir la información sobre la que el paciente ya ha actuado.


## Entrega personalizada de contenido de mantenimiento

Ofrezca contenido personalizado de educación para la salud, consejos para el bienestar y recursos adaptados a las condiciones, los intereses y los objetivos de salud de cada paciente. El contenido relevante genera confianza, mejora la alfabetización sanitaria y capacita a los pacientes para tomar decisiones informadas sobre su atención.

### Impacto empresarial

La entrega personalizada de contenido de salud logra tasas de participación de contenido más altas, lo que conduce a una mejor educación del paciente y alfabetización en salud.

### Cómo implementar

Usar el patrón [Cross-Channel Recorrido with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). La entrega de contenido para la salud se beneficia de una toma de decisiones en tiempo real que selecciona el contenido más relevante para cada paciente en función de sus condiciones, preferencias y participación pasada, entregada a través de su canal preferido. Este es el patrón correcto cuando la selección de contenido debe tener en cuenta las condiciones del paciente, las preferencias de consentimiento y las preferencias de canal, al tiempo que evita la entrega duplicada o fatigosa: la orquestación de varios pasos por sí sola no proporciona la capa de toma de decisiones en tiempo real necesaria para hacer coincidir el inventario de contenido dinámico con las necesidades individuales del paciente.

### Consideraciones técnicas

- Aplique etiquetas de clasificación de contenido y uso de datos a todos los materiales de educación para la salud a fin de garantizar que el contenido específico de la condición se entregue solamente a los pacientes que han consentido recibir información de salud sobre ese tema.
- Integre el motor de toma de decisiones con un repositorio de contenido que los equipos clínicos revisen y aprueben regularmente para garantizar la precisión médica.
- Implemente reglas de fatiga de contenido para evitar la entrega excesiva de contenido sobre un solo tema y para equilibrar el material educativo entre las diversas necesidades de salud de un paciente.
- Rastree las señales de participación en el contenido (aperturas, clics, tiempo empleado) para refinar continuamente la relevancia del contenido sin recopilar ni almacenar información médica protegida adicional.


## Notificación de resultados de laboratorio

Notificar a los pacientes cuando los resultados de laboratorio estén disponibles a través de su canal de comunicación preferido con mensajes personalizados y seguros. La notificación rápida anima a los pacientes a revisar los resultados rápidamente y a realizar un seguimiento con su equipo de atención cuando sea necesario.

### Impacto empresarial

Las notificaciones automatizadas de resultados de laboratorio ayudan a aumentar las tasas de visualización de resultados, mejorando la comunicación con el paciente y permitiendo un seguimiento clínico más rápido cuando los resultados requieren acción.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). La disponibilidad de resultados de laboratorio es un evento discreto que requiere una notificación inmediata y única a través del canal preferido del paciente. Este es el patrón correcto cuando un evento de resultados de laboratorio discretos es el déclencheur y la respuesta necesaria es una notificación única e inmediata, en lugar de una secuencia de mensajes múltiples, ya que los pacientes necesitan una alerta rápida para comprobar su portal sin comunicaciones de seguimiento adicionales.

### Consideraciones técnicas

- Nunca incluya valores de resultados de laboratorio reales en los mensajes de notificación; sólo notifique al paciente que los resultados están disponibles y diríjalos al portal seguro del paciente para obtener detalles.
- Integrarse con el sistema de información de laboratorio para recibir eventos listos para los resultados mientras se aplican etiquetas estrictas de uso de datos para evitar que cualquier dato clínico fluya a los canales de marketing.
- Implemente la lógica de retención del proveedor para que las notificaciones solo se envíen después de que el médico que realiza el pedido haya revisado y publicado los resultados para que los vea el paciente.
- Asegúrese de que todos los vínculos de notificación apunten a sesiones del portal del paciente autenticadas y cifradas que cumplan los requisitos de seguridad de HIPAA.


## Verificación de cobertura de seguro

Verificar y comunicar proactivamente la información de cobertura de seguro a los pacientes antes de sus citas para reducir las sorpresas de facturación y mejorar la experiencia general del paciente. La comunicación clara y de cobertura inicial genera confianza y reduce las disputas de facturación posteriores a la visita.

### Impacto empresarial

La verificación proactiva de la cobertura del seguro resulta en mejores tasas de confirmación de cobertura previa a la visita y una reducción significativa de las disputas de facturación y las quejas de los pacientes.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de programación de citas sirven como déclencheur para iniciar la verificación de la cobertura y comunicar los resultados al paciente antes de la visita. Este es el patrón correcto cuando el evento de programación de una cita discreta es el déclencheur y la respuesta necesaria es una notificación de cobertura única y con distinción de tiempo, en lugar de una secuencia de participación de varios pasos, ya que el paciente necesita un mensaje claro antes de la cita.

### Consideraciones técnicas

- Integre con los sistemas de verificación de elegibilidad del seguro para recuperar el estado de cobertura en tiempo real sin almacenar los datos completos de las reclamaciones del seguro en la plataforma de datos del cliente.
- Aplique etiquetas de uso de datos a toda la información financiera y de seguros para restringir su uso únicamente a las comunicaciones relacionadas con la facturación.
- Configure el tiempo del mensaje para permitir tiempo de espera suficiente antes de la cita para que los pacientes resuelvan cualquier problema de cobertura o contacten con su proveedor de seguros.
- Incluya instrucciones claras e información de contacto para el departamento de facturación para que los pacientes puedan hacer preguntas o proporcionar detalles actualizados del seguro antes de su visita.


## Recordatorios de citas de Telehealth

Envíe recordatorios personalizados para citas de salud por teléfono que incluyan instrucciones de conexión, consejos de preparación e información de soporte técnico. Los recordatorios de telesalud efectivos reducen las visitas virtuales perdidas y ayudan a los pacientes a sentirse seguros de sí mismos usando herramientas de atención digital.

### Impacto empresarial

Los recordatorios personalizados de citas de telesalud ayudan a impulsar mejoras en las tasas de visualización de visitas virtuales y acelerar la adopción general de telesalud en toda la población de pacientes.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de programación de citas de telesalud proporcionan un déclencheur natural para recordatorios oportunos que incluyen detalles de conexión y guía de preparación. Este es el patrón correcto cuando el déclencheur es un evento de cita de telesalud discreto y la respuesta requerida es un recordatorio único e inmediato con guía técnica, en lugar de una secuencia de varios pasos, ya que los pacientes necesitan instrucciones claras antes de la cita sin mensajes de seguimiento subsiguientes.

### Consideraciones técnicas

- Incluya instrucciones de conexión específicas de la plataforma (escritorio frente a móvil) basadas en las preferencias conocidas del dispositivo del paciente o en los datos anteriores de la sesión de telesalud.
- Asegúrese de que todos los vínculos de conexión de salud y los identificadores de sesión se entreguen a través de canales cifrados y compatibles con HIPAA y caduquen después de la ventana de citas programadas.
- Integrarse con la plataforma de telesalud para detectar cuándo un paciente se ha conectado correctamente de modo que los mensajes recordatorios secundarios puedan suprimirse.
- Proporcione una ruta alternativa a la información de contacto del soporte técnico para los pacientes que no se han conectado dentro de una ventana definida antes de la hora de inicio de la cita.


## Participación en programas de bienestar

Personalice las comunicaciones, los desafíos y las recompensas del programa de bienestar en función de los objetivos de salud, el nivel de actividad y las preferencias de cada paciente. Los programas de bienestar motivan a los pacientes a adoptar hábitos más saludables y mantener el bienestar a largo plazo.

### Impacto empresarial

Las campañas personalizadas de participación en programas de bienestar logran tasas de participación en programas más altas, lo que contribuye a mejorar los resultados de salud y a fortalecer la lealtad de los pacientes.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Los programas de bienestar son experiencias de participación sostenida con múltiples hitos, desafíos y puntos de contacto de recompensa que requieren orquestación adaptativa basada en la participación y el progreso del paciente. Este es el patrón correcto porque los programas de bienestar requieren un flujo secuenciado de varios mensajes durante un periodo prolongado con ramas condicionales basadas en hitos de participación y patrones de participación: la mensajería activada por eventos no puede gestionar la orquestación adaptativa sostenida necesaria para ajustar los desafíos y las recompensas en función del seguimiento del progreso continuo.

### Consideraciones técnicas

- Integre con fuentes de datos de aplicaciones de fitness y dispositivos portátiles mientras aplica etiquetas de uso de datos claras para distinguir los datos de bienestar de los datos de salud clínica sujetos a requisitos regulatorios más estrictos.
- Implementar la gestión de consentimiento que permita a los pacientes conceder y revocar permisos para la recopilación de datos de bienestar independientemente de sus preferencias de comunicación clínica.
- Diseñe una lógica de recorrido que ajuste la dificultad de desafío y la frecuencia de comunicación en función de los patrones de compromiso de cada paciente para evitar el desaliento o la fatiga.
- Asegúrese de que el seguimiento de recompensas e incentivos cumpla con las regulaciones de atención médica aplicables en relación con los incentivos para pacientes y los requisitos contra las devoluciones.


## Coordinación del equipo de atención

Permita una comunicación y coordinación personalizadas entre los pacientes y los miembros de su equipo de atención en función del plan de atención y las preferencias individuales. Una mejor coordinación conduce a transiciones de cuidado más fluidas y a mejores resultados para los pacientes con necesidades de cuidado complejas.

### Impacto empresarial

Las comunicaciones eficaces de coordinación del equipo de atención mejoran la participación del equipo de atención y los resultados de coordinación de la atención en los planes de atención de múltiples proveedores.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). La coordinación del equipo de atención implica varias partes interesadas y flujos de comunicación continuos que deben adaptarse en función de los hitos del plan de atención, los cambios de estado del paciente y las acciones del proveedor. Este es el patrón correcto porque la coordinación de la atención requiere flujos de mensajería adaptables de varios pasos que se ramifican en función de los hitos del plan de atención y las acciones del proveedor en varias partes interesadas: un solo mensaje o patrón más sencillo no puede dar cabida a las complejas interdependencias y al enrutamiento de mensajes basado en funciones que se necesitan en los equipos clínicos.

### Consideraciones técnicas

- Implemente controles de acceso basados en funciones y etiquetas de uso de datos para garantizar que cada miembro del equipo de atención solo reciba la información del paciente relevante para su función en el plan de atención.
- Integrarse con los sistemas de gestión de la atención y registros electrónicos de salud para recibir actualizaciones del plan de atención, finalizaciones de derivaciones y eventos de transición de atención que generen mensajes de coordinación de déclencheur.
- Diseñe rutas de comunicación independientes para los mensajes dirigidos al paciente y al proveedor, lo que garantiza que la terminología clínica se utilice correctamente para los proveedores, mientras que los mensajes al paciente siguen siendo claros y accesibles.
- Mantener una pista de auditoría completa de todas las comunicaciones de coordinación de la atención para el cumplimiento de las regulaciones de continuidad de la atención y los requisitos de acreditación.


## Funnel de Recorrido del paciente y análisis de la brecha asistencial

Mapa del recorrido de pacientes de extremo a extremo desde la investigación web inicial hasta la programación de citas, la entrega de atención y el seguimiento para identificar dónde se desconectan los pacientes y qué poblaciones tienen lagunas en la atención preventiva o crónica recomendada. Los sistemas de salud que carecen de visibilidad de recorrido en canales múltiples no pueden distinguir entre la fricción programada y la desconexión del paciente, lo que limita su capacidad para mejorar el acceso y cerrar las brechas de atención a escala.

### Impacto empresarial

Comprender dónde abandonan los pacientes las rutas de atención y qué segmentos de miembros tienen la mayor concentración de brechas de atención permite a los equipos de gestión y marketing de la atención enfocar los recursos de alcance en las poblaciones y los puntos de fricción que producirán la mayor mejora en la adherencia a la atención.

### Cómo implementar

Usar el patrón [Customer Analytics y Insight Generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Este método conecta los datos de comportamiento del portal y la web, los registros del sistema de citas y los datos de las solicitudes de asistencia con Customer Journey Analytics, donde el análisis de abandonos mide el abandono en cada paso de planificación o atención y el análisis de cohorte identifica qué segmentos de miembros tienen las tasas más bajas de cumplimiento de la atención. Este es el patrón correcto cuando el objetivo es la generación de insight y el análisis a nivel de población —comprender dónde se desglosan los recorridos y quién está en mayor riesgo— en lugar de activar la divulgación o activar una lista de supresión.

### Consideraciones técnicas

- Los datos de citas y reclamaciones de los sistemas clínicos deben asignarse a esquemas XDM compatibles con HIPAA antes de su incorporación a AEP, y deben aplicarse etiquetas de uso de datos para restringir el acceso a la información médica protegida dentro de las vistas de datos de CJA.
- Los identificadores de paciente o miembro a través del portal web, el sistema de programación y EHR deben resolverse en un ID de persona coherente en la conexión de CJA para producir una vista de recorrido coherente entre sistemas sin duplicar individuos.
- El análisis de carencias de atención requiere conjuntos de datos de búsqueda que codifican definiciones de directrices clínicas, como intervalos de detección recomendados por edad y condición, para que los campos derivados de la CJA puedan marcar a los miembros que no han completado la atención recomendada dentro de la ventana de guía.
- La programación del análisis de funnel debe capturar tanto las sesiones de programación completadas como las abandonadas, incluidos los puntos de salida en flujos de programación de varios pasos, de modo que los puntos de fricción sean visibles en el nivel de paso en lugar de como tasas de caída agregadas.


## Personalization de contenido del portal para pacientes

Personalice la experiencia del portal del paciente autenticado mostrando el contenido, las herramientas y los recursos de salud más relevantes en función del comportamiento de navegación en la sesión de cada paciente y el historial de participación. Un portal que se adapta a lo que un paciente está investigando activamente, en lugar de presentar la misma experiencia estática a cada visitante, facilita a los pacientes encontrar lo que necesitan y fomenta una participación más profunda con los recursos de salud disponibles.

### Impacto empresarial

La personalización de la experiencia del portal del paciente basada en el comportamiento de participación mejora las tasas de detección de contenido y de finalización del autoservicio, lo que ayuda a los pacientes a navegar por su atención con mayor seguridad sin necesidad de la intervención del equipo de atención.

### Cómo implementar

Usar el patrón [Behavioral Recommendations](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Las señales de comportamiento en la sesión procedentes del portal autenticado (incluidas las vistas de páginas de contenido, el uso de herramientas de mantenimiento, la participación en temas de preguntas frecuentes y la actividad de programación de citas) forman un modelo de recomendación que muestra los recursos más relevantes para cada paciente en función de lo que esté explorando activamente, sin requerir datos clínicos como entrada. Este es el patrón correcto cuando la personalización está impulsada por señales de comportamiento implícitas dentro de una sesión autenticada y el objetivo es la clasificación de relevancia de un catálogo de contenido y recursos, en lugar de la toma de decisiones de elegibilidad regidas, lo que es más apropiado cuando los criterios clínicos deben confirmar lo que ve un paciente.

### Consideraciones técnicas

- Limite las señales de comportamiento utilizadas para las recomendaciones a los datos de interacción del portal (vistas de contenido, uso de herramientas y patrones de navegación) e implemente etiquetas de uso de datos que impidan que cualquier interés de mantenimiento deducido fluya fuera de la sesión del portal autenticado o a los canales de marketing.
- Implemente una biblioteca de contenido revisado clínicamente como grupo de recomendaciones para que el modelo solo pueda mostrar materiales de educación para la salud aprobados previamente, lo que garantiza que todos los recursos recomendados se hayan validado para comprobar su precisión antes de su implementación.
- Asegúrese de que el sistema de recomendaciones cumpla los requisitos de protección técnica de la HIPAA para el entorno de portal autenticado, incluidos los controles de tiempo de espera de sesión y el registro de auditoría del contenido que se presentó a cada paciente y cuándo.
- Proporcione a los pacientes controles visibles para borrar el historial de navegación del portal y excluirse de la personalización del comportamiento, manteniendo la transparencia y la confianza en cómo se utilizan los datos de participación dentro de la experiencia del portal.

## Confirmación del paciente y recordatorios de cita

Envíe recordatorios de citas personalizados, consejos médicos y comunicaciones de atención de seguimiento a través de recorridos multicanal compatibles y con conocimiento de consentimiento. Los recordatorios de citas personalizados y automatizados reducen las tasas de no presentación, a la vez que garantizan que las comunicaciones cumplan con las regulaciones de privacidad de la atención médica y las preferencias de consentimiento del paciente.

### Impacto empresarial

Las organizaciones de atención médica con programas de recordatorio de citas automatizadas ven reducciones significativas en las tasas de no presentación y de cancelación tardía, mejorando la utilización de los horarios de los proveedores y los resultados de salud del paciente a través de una mejor adherencia a las citas.

### Cómo implementar

Use el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para responder a los eventos de programación de citas con recordatorios personalizados y oportunos a intervalos óptimos antes de la fecha de la cita. Este es el patrón correcto cuando la comunicación se activa por un evento de interacción específico del paciente y la respuesta es un mensaje individualizado y sensible al tiempo, en lugar de una secuencia de crianza de varias semanas o una selección de ofertas complejas.

### Consideraciones técnicas

- Todas las comunicaciones de los pacientes deben cumplir con las regulaciones de privacidad de atención médica aplicables; el contenido de la mensajería debe evitar incluir información médica protegida más allá de lo estrictamente necesario para la comunicación.
- La administración del consentimiento debe aplicarse a nivel de canal: los pacientes que no han elegido los recordatorios por SMS no deben recibir mensajes de texto, incluso cuando los SMS serían el canal de recordatorio más eficaz para su población.
- La integración con el sistema de programación debe entregar eventos de cita en tiempo casi real para permitir que el tiempo de recordatorio sea preciso para el horario de cita real, incluyendo las reprogramaciones y cancelaciones del mismo día.
- Las secuencias de recordatorio multicanal deben incluir lógica de supresión para que los pacientes que confirmen su cita no sigan recibiendo mensajes de recordatorio para esa cita.
