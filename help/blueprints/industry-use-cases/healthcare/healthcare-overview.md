---
title: Casos de uso de atención sanitaria
description: Descubra cómo las organizaciones de atención médica utilizan Adobe Experience Platform para mejorar la participación de los pacientes, optimizar la coordinación de la atención e impulsar mejores resultados en materia de salud.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 1%

---


# Casos de uso de atención sanitaria

Las organizaciones de atención sanitaria utilizan Adobe Experience Platform para crear perfiles unificados de pacientes y ofrecer comunicaciones personalizadas y oportunas en todos los puntos de contacto. Al conectar los datos clínicos, de comportamiento y de preferencias en un solo lugar, los equipos de atención pueden atraer a los pacientes de forma más eficaz, manteniendo al mismo tiempo los más altos estándares de privacidad y cumplimiento.

## Automatización de recordatorio de cita

Envíe recordatorios de cita personalizados por correo electrónico, mensajes de texto y notificaciones push en función de las preferencias de comunicación y el tipo de cita de cada paciente. Los recordatorios automatizados reducen las citas perdidas y mantienen los horarios funcionando sin problemas, lo que permite que el personal se concentre en la atención del paciente.

### Impacto empresarial

Las organizaciones que implementan recordatorios de citas automatizadas por lo general ven una mejora del 30 al 40 por ciento en las tasas de citas y una reducción significativa en las no-presentaciones costosas.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de creación y actualización de citas del sistema de programación sirven como déclencheur naturales para mensajes recordatorios oportunos y relevantes.

### Consideraciones técnicas

- Asegúrese de que toda la información de contacto del paciente y los detalles de la cita se transmitan y almacenen de acuerdo con los requisitos de la HIPAA, utilizando etiquetas de uso de datos adecuadas para restringir el acceso no autorizado.
- Integrarse con el sistema electrónico de programación de registros médicos para capturar la creación de citas, la cancelación y la reprogramación de eventos en tiempo real.
- Aplique políticas de administración de consentimiento para que los recordatorios solo se envíen a través de los canales en los que el paciente ha decidido participar explícitamente.
- Configure reglas de supresión para evitar recordatorios duplicados o excesivos cuando las citas se vuelvan a programar en sucesión rápida.


## Campañas de adherencia a medicamentos

Envíe recordatorios personalizados y contenido educativo para ayudar a los pacientes a mantenerse al día con sus horarios de medicación y planes de tratamiento. La mensajería personalizada basada en el tipo de medicamento, el horario de dosificación y los antecedentes de los pacientes mejora la adherencia y mejora los resultados de salud.

### Impacto empresarial

Las campañas personalizadas de adherencia a la medicación generalmente impulsan una mejora del 20 al 30 por ciento en las tasas de adherencia, lo que conduce a mejores resultados de salud medibles y menos reingresos hospitalarios.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). El cumplimiento de la medicación requiere un enfoque sostenido y multitáctil con recordatorios crecientes, puntos de contacto educativos y chequeos de seguimiento durante el transcurso de un plan de tratamiento.

### Consideraciones técnicas

- Aplique etiquetas estrictas de uso de datos a toda la información de salud protegida relacionada con los datos de medicamentos y diagnósticos para evitar la activación descendente no autorizada.
- Integrarse con los sistemas de farmacia y registros electrónicos de salud para recibir los datos de llenado y recarga de recetas que déclencheur los pasos de recorrido.
- Implementar una gestión de consentimiento sólida para garantizar que los pacientes hayan aceptado recibir comunicaciones relacionadas con la medicación y puedan retirar el consentimiento en cualquier momento.
- Diseñe una lógica de recorrido para detectar patrones de no participación y escalar a las notificaciones del equipo de atención cuando un paciente pueda estar en riesgo de no cumplimiento.


## Recordatorios de atención preventiva

Recuerde proactivamente a los pacientes sobre la atención preventiva recomendada, como vacunas, exámenes y revisiones anuales en función de su edad, antecedentes médicos y factores de riesgo. Los recordatorios oportunos de atención preventiva ayudan a cerrar las brechas en la atención y mejorar la salud general de la población.

### Impacto empresarial

El alcance de la atención preventiva proactiva suele resultar en un aumento del 25 al 35 por ciento en las tasas de finalización de la atención preventiva, lo que contribuye a mejorar la salud de la población y a reducir los costos de tratamiento a largo plazo.

### Cómo implementar

Usar el patrón [Activación de mensaje saliente por lotes](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). Los recordatorios de atención preventiva se entregan mejor a través de campañas programadas por lotes que evalúan la elegibilidad del paciente en comparación con las directrices clínicas en una cadencia regular.

### Consideraciones técnicas

- Genere segmentos de audiencia utilizando criterios de directrices clínicas (edad, sexo, antecedentes familiares, fechas de detección previas) mientras aplica etiquetas de uso de datos a toda la información de salud protegida que se usa en la segmentación.
- Coordine con los equipos clínicos para asegurarse de que el contenido del recordatorio se ajuste a las directrices de atención preventiva actuales basadas en la evidencia y a los protocolos organizativos.
- Implemente un límite de frecuencia para evitar abrumar a los pacientes que cumplen con los requisitos para recibir múltiples recomendaciones de atención preventiva simultáneamente.
- Mantener una pista de auditoría de todas las comunicaciones de atención preventiva enviadas para la presentación de informes reglamentarios y la documentación de medidas de calidad.


## Campañas de seguimiento posteriores a la visita

Envíe automáticamente encuestas posteriores a la visita, instrucciones de atención y recordatorios de citas de seguimiento en función del tipo de visita y de las necesidades específicas de cada paciente. El seguimiento oportuno mejora la satisfacción del paciente y garantiza la continuidad de la atención después de cada encuentro.

### Impacto empresarial

Las campañas automatizadas de seguimiento después de la visita generalmente logran una mejora del 40 al 50 por ciento en las tasas de respuesta a las encuestas y puntuaciones de satisfacción del paciente mediblemente más altas.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de finalización de visitas del sistema de registros electrónicos de salud proporcionan un déclencheur natural y oportuno para las comunicaciones de seguimiento adaptadas al tipo de encuentro.

### Consideraciones técnicas

- Integrarse con el sistema de registros electrónicos de salud para recibir eventos de alta por visita que incluyen tipo de visita, proveedor e instrucciones de atención relevantes sin exponer las notas clínicas completas.
- Aplique etiquetas de uso de datos a cualquier contenido de instrucciones de atención médica para garantizar que la información médica protegida se comparta únicamente a través de canales seguros y autorizados por el paciente.
- Configure reglas de tiempo que tengan en cuenta el tipo de visita; por ejemplo, los controles postquirúrgicos pueden requerir un tiempo diferente al de las revisiones de rutina.
- Incluya enlaces seguros al portal del paciente para la finalización de la encuesta y la programación de citas en lugar de recopilar información médica a través de canales no seguros.


## Programas de manejo de enfermedades crónicas

Personalice las comunicaciones sobre el manejo de enfermedades crónicas, el contenido educativo y los recordatorios de monitoreo basados en la condición específica y el plan de tratamiento de cada paciente. La participación sostenida y relevante ayuda a los pacientes a tomar un papel activo en la gestión de su salud a lo largo del tiempo.

### Impacto empresarial

Los programas personalizados de manejo de enfermedades crónicas típicamente ven un aumento del 30 al 40 por ciento en las tasas de participación del programa, lo que conduce a mejores resultados de manejo de enfermedades y a una menor utilización de la atención de emergencia.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). La gestión de enfermedades crónicas es inherentemente una experiencia de largo plazo, con múltiples puntos de contacto que requiere mensajes adaptables basados en la participación del paciente y los hitos de salud.

### Consideraciones técnicas

- Diseñe una lógica de ramificación de recorridos que se adapte en función de las métricas específicas de la enfermedad (por ejemplo, las tendencias de la glucosa en sangre para el tratamiento de la diabetes o las lecturas de la presión arterial para los programas de hipertensión).
- Implemente un control de datos estricto con [!DNL Adobe Experience Platform] etiquetas de uso de datos para clasificar y proteger los datos de mantenimiento específicos de la condición en todo el recorrido.
- Integre con dispositivos remotos de monitorización de pacientes y sistemas de resultados informados por los pacientes para alimentar los datos de salud en tiempo real en los puntos de decisión del recorrido.
- Cree rutas de escalación del equipo de atención médica dentro del recorrido para que la falta de participación o las tendencias sanitarias generen déclencheur de alerta para el personal clínico apropiado.


## Nuevo Recorrido de incorporación del paciente

Automatice un recorrido de incorporación de varios pasos para nuevos pacientes que incluya información de bienvenida, instrucciones de acceso al portal del paciente y guía de programación de citas. Una experiencia de incorporación sin problemas marca la pauta para una relación de paciente comprometida y a largo plazo.

### Impacto empresarial

Los recorridos automatizados de incorporación de nuevos pacientes suelen impulsar una mejora del 50 al 60 por ciento en las tasas de activación del portal y una participación del paciente temprana significativamente mayor.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). La incorporación del paciente es un proceso naturalmente secuencial de varios pasos en el que cada comunicación se basa en la anterior y se adapta en función de si el paciente ha completado acciones clave.

### Consideraciones técnicas

- Integrarse con el sistema de registro de pacientes para almacenar en déclencheur el recorrido de incorporación inmediatamente después de la creación de la nueva historia clínica del paciente, lo que garantiza una primera impresión oportuna.
- Utilice la resolución de identidad para combinar cualquier registro preexistente (por ejemplo, de una visita al sitio web o una solicitud de cita) con el nuevo perfil del paciente para evitar comunicaciones duplicadas.
- Asegúrese de que los vínculos y las credenciales de activación del portal se entreguen a través de canales seguros y compatibles con HIPAA y caduquen después de un periodo definido.
- Diseñe el recorrido para detectar los eventos de activación del portal y de finalización del formulario, de modo que los pasos siguientes se adapten en lugar de repetir la información sobre la que el paciente ya ha actuado.


## Entrega personalizada de contenido de mantenimiento

Ofrezca contenido personalizado de educación para la salud, consejos para el bienestar y recursos adaptados a las condiciones, los intereses y los objetivos de salud de cada paciente. El contenido relevante genera confianza, mejora la alfabetización sanitaria y capacita a los pacientes para tomar decisiones informadas sobre su atención.

### Impacto empresarial

La entrega personalizada de contenido de salud generalmente logra un aumento del 35 al 45 por ciento en las tasas de participación de contenido, lo que conduce a una mejora mensurable de la educación del paciente y la alfabetización en salud.

### Cómo implementar

Usar el patrón [Cross-Channel Recorrido with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). La entrega de contenido para la salud se beneficia de una toma de decisiones en tiempo real que selecciona el contenido más relevante para cada paciente en función de sus condiciones, preferencias y participación pasada, entregada a través de su canal preferido.

### Consideraciones técnicas

- Aplique etiquetas de clasificación de contenido y uso de datos a todos los materiales de educación para la salud a fin de garantizar que el contenido específico de la condición se entregue solamente a los pacientes que han consentido recibir información de salud sobre ese tema.
- Integre el motor de toma de decisiones con un repositorio de contenido que los equipos clínicos revisen y aprueben regularmente para garantizar la precisión médica.
- Implemente reglas de fatiga de contenido para evitar la entrega excesiva de contenido sobre un solo tema y para equilibrar el material educativo entre las diversas necesidades de salud de un paciente.
- Rastree las señales de participación en el contenido (aperturas, clics, tiempo empleado) para refinar continuamente la relevancia del contenido sin recopilar ni almacenar información médica protegida adicional.


## Notificación de resultados de laboratorio

Notificar a los pacientes cuando los resultados de laboratorio estén disponibles a través de su canal de comunicación preferido con mensajes personalizados y seguros. La notificación rápida anima a los pacientes a revisar los resultados rápidamente y a realizar un seguimiento con su equipo de atención cuando sea necesario.

### Impacto empresarial

Las notificaciones automatizadas de resultados de laboratorio suelen impulsar un aumento del 60 al 70 por ciento en las tasas de visualización de resultados, lo que mejora la comunicación con el paciente y permite un seguimiento clínico más rápido cuando los resultados requieren acción.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). La disponibilidad de resultados de laboratorio es un evento discreto que requiere una notificación inmediata y única a través del canal preferido del paciente.

### Consideraciones técnicas

- Nunca incluya valores de resultados de laboratorio reales en los mensajes de notificación; sólo notifique al paciente que los resultados están disponibles y diríjalos al portal seguro del paciente para obtener detalles.
- Integrarse con el sistema de información de laboratorio para recibir eventos listos para los resultados mientras se aplican etiquetas estrictas de uso de datos para evitar que cualquier dato clínico fluya a los canales de marketing.
- Implemente la lógica de retención del proveedor para que las notificaciones solo se envíen después de que el médico que realiza el pedido haya revisado y publicado los resultados para que los vea el paciente.
- Asegúrese de que todos los vínculos de notificación apunten a sesiones del portal del paciente autenticadas y cifradas que cumplan los requisitos de seguridad de HIPAA.


## Verificación de cobertura de seguro

Verificar y comunicar proactivamente la información de cobertura de seguro a los pacientes antes de sus citas para reducir las sorpresas de facturación y mejorar la experiencia general del paciente. La comunicación clara y de cobertura inicial genera confianza y reduce las disputas de facturación posteriores a la visita.

### Impacto empresarial

La verificación proactiva de la cobertura del seguro suele resultar en una mejora del 25 al 35 por ciento en las tasas de confirmación de cobertura previa a la visita y una reducción significativa en las disputas de facturación y las quejas de los pacientes.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de programación de citas sirven como déclencheur para iniciar la verificación de la cobertura y comunicar los resultados al paciente antes de la visita.

### Consideraciones técnicas

- Integre con los sistemas de verificación de elegibilidad del seguro para recuperar el estado de cobertura en tiempo real sin almacenar los datos completos de las reclamaciones del seguro en la plataforma de datos del cliente.
- Aplique etiquetas de uso de datos a toda la información financiera y de seguros para restringir su uso únicamente a las comunicaciones relacionadas con la facturación.
- Configure el tiempo del mensaje para permitir tiempo de espera suficiente antes de la cita para que los pacientes resuelvan cualquier problema de cobertura o contacten con su proveedor de seguros.
- Incluya instrucciones claras e información de contacto para el departamento de facturación para que los pacientes puedan hacer preguntas o proporcionar detalles actualizados del seguro antes de su visita.


## Recordatorios de citas de Telehealth

Envíe recordatorios personalizados para citas de salud por teléfono que incluyan instrucciones de conexión, consejos de preparación e información de soporte técnico. Los recordatorios de telesalud efectivos reducen las visitas virtuales perdidas y ayudan a los pacientes a sentirse seguros de sí mismos usando herramientas de atención digital.

### Impacto empresarial

Los recordatorios personalizados de citas de telesalud suelen impulsar una mejora del 40 al 50 por ciento en las tasas de visitas virtuales y acelerar la adopción general de telesalud en toda la población de pacientes.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Los eventos de programación de citas de telesalud proporcionan un déclencheur natural para recordatorios oportunos que incluyen detalles de conexión y guía de preparación.

### Consideraciones técnicas

- Incluya instrucciones de conexión específicas de la plataforma (escritorio frente a móvil) basadas en las preferencias conocidas del dispositivo del paciente o en los datos anteriores de la sesión de telesalud.
- Asegúrese de que todos los vínculos de conexión de salud y los identificadores de sesión se entreguen a través de canales cifrados y compatibles con HIPAA y caduquen después de la ventana de citas programadas.
- Integrarse con la plataforma de telesalud para detectar cuándo un paciente se ha conectado correctamente de modo que los mensajes recordatorios secundarios puedan suprimirse.
- Proporcione una ruta alternativa a la información de contacto del soporte técnico para los pacientes que no se han conectado dentro de una ventana definida antes de la hora de inicio de la cita.


## Participación en programas de bienestar

Personalice las comunicaciones, los desafíos y las recompensas del programa de bienestar en función de los objetivos de salud, el nivel de actividad y las preferencias de cada paciente. Los programas de bienestar motivan a los pacientes a adoptar hábitos más saludables y mantener el bienestar a largo plazo.

### Impacto empresarial

Las campañas personalizadas de participación en programas de bienestar generalmente logran un aumento de entre el 30 y el 40 por ciento en las tasas de participación en programas, lo que contribuye a mejorar los resultados de salud y a fortalecer la lealtad de los pacientes.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Los programas de bienestar son experiencias de participación sostenida con múltiples hitos, desafíos y puntos de contacto de recompensa que requieren orquestación adaptativa basada en la participación y el progreso del paciente.

### Consideraciones técnicas

- Integre con fuentes de datos de aplicaciones de fitness y dispositivos portátiles mientras aplica etiquetas de uso de datos claras para distinguir los datos de bienestar de los datos de salud clínica sujetos a requisitos regulatorios más estrictos.
- Implementar la gestión de consentimiento que permita a los pacientes conceder y revocar permisos para la recopilación de datos de bienestar independientemente de sus preferencias de comunicación clínica.
- Diseñe una lógica de recorrido que ajuste la dificultad de desafío y la frecuencia de comunicación en función de los patrones de compromiso de cada paciente para evitar el desaliento o la fatiga.
- Asegúrese de que el seguimiento de recompensas e incentivos cumpla con las regulaciones de atención médica aplicables en relación con los incentivos para pacientes y los requisitos contra las devoluciones.


## Coordinación del equipo de atención

Permita una comunicación y coordinación personalizadas entre los pacientes y los miembros de su equipo de atención en función del plan de atención y las preferencias individuales. Una mejor coordinación conduce a transiciones de cuidado más fluidas y a mejores resultados para los pacientes con necesidades de cuidado complejas.

### Impacto empresarial

Las comunicaciones efectivas de coordinación del equipo de atención suelen dar como resultado una mejora del 35 al 45 por ciento en la participación del equipo de atención y resultados de coordinación de atención medibles en los planes de atención de varios proveedores.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). La coordinación del equipo de atención implica varias partes interesadas y flujos de comunicación continuos que deben adaptarse en función de los hitos del plan de atención, los cambios de estado del paciente y las acciones del proveedor.

### Consideraciones técnicas

- Implemente controles de acceso basados en funciones y etiquetas de uso de datos para garantizar que cada miembro del equipo de atención solo reciba la información del paciente relevante para su función en el plan de atención.
- Integrarse con los sistemas de gestión de la atención y registros electrónicos de salud para recibir actualizaciones del plan de atención, finalizaciones de derivaciones y eventos de transición de atención que generen mensajes de coordinación de déclencheur.
- Diseñe rutas de comunicación independientes para los mensajes dirigidos al paciente y al proveedor, lo que garantiza que la terminología clínica se utilice correctamente para los proveedores, mientras que los mensajes al paciente siguen siendo claros y accesibles.
- Mantener una pista de auditoría completa de todas las comunicaciones de coordinación de la atención para el cumplimiento de las regulaciones de continuidad de la atención y los requisitos de acreditación.
