---
title: Casos de uso B2B
description: Descubra cómo las organizaciones B2B utilizan Adobe Experience Platform para acelerar la canalización, mejorar la calidad del cliente potencial e impulsar la expansión del cliente.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 6073bdc4-e148-455e-aa4e-3d5226d4b5a2
source-git-commit: 0236bd326730ee9a0be621ee0e60ddc3d352410d
workflow-type: tm+mt
source-wordcount: '3479'
ht-degree: 0%

---

# Casos de uso B2B

Las organizaciones entre empresas utilizan Adobe Experience Platform para unificar los datos de cuentas y de personas, lo que permite a los equipos de marketing y ventas ofrecer experiencias coordinadas y relevantes en todas las etapas del recorrido de compra. Desde la aceleración de la canalización hasta la expansión de los clientes, estos casos de uso muestran cómo los equipos B2B convierten los datos complejos en resultados comerciales mensurables.

>[!NOTE]
>
>Para ver modelos de arquitectura específicos de B2B, como la activación basada en cuentas y la administración de grupos de compra, consulte [Modelos de marketing y activación de B2B](/help/blueprints/b2b/overview.md).

## Account-Based Marketing Personalization

Personalice las comunicaciones de marketing y el contenido para cuentas de Target en función del perfil de la cuenta, el historial de participación y las señales de compra. Al alinear la mensajería con el contexto único de cada cuenta, los equipos de marketing pueden romper con el ruido y atraer a las partes interesadas adecuadas con el contenido adecuado.

### Impacto empresarial

Las organizaciones que implementan la personalización de marketing basada en cuentas ven una participación mejorada de la cuenta, lo que fortalece la canalización y acelera la progresión de los acuerdos.

### Cómo implementar

Use el patrón [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md) para crear audiencias de nivel de cuenta y activar contenido personalizado en todos los canales. Este patrón está diseñado específicamente para estrategias basadas en cuentas y admite la segmentación a nivel de cuenta y persona. Este es el patrón correcto cuando la segmentación debe operar a nivel de cuenta en lugar de a nivel individual: la activación de audiencia de RT-CDP estándar no admite el modelo de datos basado en cuentas requerido para las estrategias ABM.

### Consideraciones técnicas

- Integre datos de CRM (por ejemplo, [!DNL Salesforce] o [!DNL Microsoft Dynamics]) para mantener jerarquías de cuentas actualizadas, etapas de oportunidad y asignaciones de propiedad.
- Configure esquemas de perfil a nivel de cuenta para capturar atributos firmográficos como la industria, el recuento de empleados, el intervalo de ingresos y la pila de tecnología.
- Asigne relaciones persona a cuenta para garantizar que las señales de participación individuales se acumulen en la puntuación y segmentación a nivel de cuenta.
- Coordínese con [!DNL Marketo Engage] para alinear las campañas de automatización de marketing con las audiencias de cuenta impulsadas por la plataforma.


## Puntuación y nutrición de plomo

Puntúe automáticamente los posibles clientes en función de los datos y el comportamiento del perfil y, a continuación, dirija los posibles clientes de alta puntuación a ventas con campañas de crianza personalizadas para otros. Este enfoque garantiza que los equipos de ventas se centren en las oportunidades más prometedoras mientras que el marketing continúa desarrollando perspectivas en etapas anteriores.

### Impacto empresarial

Las empresas que implementan la puntuación de posibles clientes y la nutrición automatizada ven una mejor conversión de posible cliente a oportunidad, lo que acelera la velocidad de la canalización y mejora la productividad de las ventas.

### Cómo implementar

Use el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para diseñar recorridos de crianza ramificados que respondan a los cambios de puntuación de posibles clientes y a los déclencheur de comportamiento. Este patrón admite la lógica condicional necesaria para enrutar posibles clientes entre las pistas de cultivo y los flujos de trabajo de transferencia de ventas. Este es el patrón correcto cuando el caso de uso requiere un flujo de varios mensajes secuenciado en días con ramificación condicional basada en cambios de puntuación de posibles clientes y eventos de comportamiento: un solo mensaje activado no puede dar cabida a la lógica de dependencia entre las fases de puntuación y las decisiones de enrutamiento.

### Consideraciones técnicas

- Establezca una sincronización CRM bidireccional (por ejemplo, [!DNL Salesforce] o [!DNL Microsoft Dynamics]) para que las puntuaciones de posibles clientes y los estados de calificación sean coherentes entre los sistemas de marketing y ventas.
- Defina las dimensiones de puntuación demográficas (función, tamaño de la empresa, sector) y de comportamiento (descargas de contenido, asistencia a seminarios web, visitas a la página del producto).
- Coordine los modelos de puntuación de posibles clientes con [!DNL Marketo Engage] para evitar puntuaciones conflictivas entre plataformas.
- Establezca reglas de deterioro de puntuación para garantizar que los posibles clientes que se mantienen en silencio pierdan prioridad con el tiempo.


## Personalization de contenido para clientes potenciales

Personalice el contenido, los recursos y las ofertas del sitio web en función del sector, la función, el tamaño de la empresa y el historial de participación del cliente potencial. Cuando los clientes potenciales ven contenido relevante para su situación específica, se involucran más profundamente y se mueven a través de funnel más rápido.

### Impacto empresarial

Las organizaciones B2B que personalizan las experiencias web para clientes potenciales conocidos ven una mejor participación en el contenido, lo que conduce a una canalización más calificada y a ciclos de ventas más cortos.

### Cómo implementar

Utilice el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones/web de visitantes conocidos para ofrecer experiencias de contenido adaptadas según perfiles de clientes potenciales unificados. Este patrón aprovecha los datos de perfil en tiempo real para ofrecer los recursos, casos prácticos y llamadas a la acción más relevantes para cada visitante. Este es el patrón correcto cuando la personalización está impulsada por atributos de perfil y la pertenencia a segmentos en lugar de por un modelo de afinidad de comportamiento, lo que permite que los atributos de nivel de cuenta y de nivel individual controlen la experiencia.

### Consideraciones técnicas

- Implemente la resolución de identidad para hacer coincidir el comportamiento de navegación anónima con los registros de clientes potenciales conocidos una vez que se autentican o envían un formulario.
- Defina reglas de personalización basadas en atributos de nivel de cuenta (sector, segmento, fase de negocio) así como atributos de nivel individual (función, consumo de contenido anterior).
- Integre con su sistema de administración de contenido para intercambiar dinámicamente titulares, recomendaciones de recursos y llamadas a la acción.
- Asegúrese de que [!DNL Marketo Engage] fuentes de datos de seguimiento web se incluyan en el perfil unificado para obtener una imagen de comportamiento completa.


## Registro y seguimiento de eventos

Automatice las confirmaciones de registro de eventos personalizadas, los recordatorios y el seguimiento posterior al evento en función del tipo de evento y el perfil del asistente. Esto mantiene a los posibles clientes comprometidos antes, durante y después de los eventos, al tiempo que libera al equipo de marketing de la coordinación manual.

### Impacto empresarial

Los flujos de trabajo de comunicación de eventos automatizados y personalizados impulsan una asistencia de eventos mejorada, maximizando el retorno de la inversión en eventos y fortaleciendo las relaciones con los posibles clientes.

### Cómo implementar

Utilice el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para organizar el ciclo de vida completo del evento desde el registro hasta la organización posterior al evento. Este patrón admite déclencheur basados en tiempo, ramificaciones condicionales por tipo de evento y secuencias de seguimiento de varios canales. Este es el patrón correcto cuando el caso de uso requiere un flujo de mensajes múltiples secuenciado a lo largo de los días con ramificación condicional basada en el registro de eventos y la asistencia: la mensajería basada en el tiempo por sí sola no puede gestionar la compleja lógica de ramificación entre rutas registradas, atendidas y sin presentación.

### Consideraciones técnicas

- Integre los datos de registro de las plataformas de seminarios web (por ejemplo, [!DNL ON24], [!DNL Zoom Webinar]) y los sistemas de eventos en persona en el perfil unificado.
- Capture señales de asistencia y participación (duración de la sesión, preguntas formuladas, respuestas de las encuestas) para personalizar los mensajes de seguimiento.
- Coordine los recorridos de eventos con los estados del programa [!DNL Marketo Engage] para mantener la coherencia en los informes entre sistemas.
- Diseñe ramas de recorrido independientes para los inscritos que asistieron a la reunión y para los que no, con contenido personalizado para cada uno.


## Campañas de conversión de prueba de productos

Fomente la participación de los usuarios de prueba con recomendaciones de productos personalizadas, recursos de formación y ofertas que fomenten la conversión a planes de pago. Al conocer a los usuarios de prueba donde se encuentran en la exploración de productos, los equipos pueden eliminar la fricción y acelerar el camino hacia la compra.

### Impacto empresarial

Las organizaciones que implementan campañas de conversión de prueba personalizadas ven una conversión de prueba a pago mejorada, que afecta directamente a los nuevos ingresos comerciales y reduce los costes de adquisición de los clientes.

### Cómo implementar

Use el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para generar recorridos de conversión basados en el tiempo y en el comportamiento para los usuarios de prueba. Este patrón admite rutas condicionales basadas en hitos de uso del producto, lo que permite realizar empujones dirigidos en los momentos adecuados. Este es el patrón correcto cuando el caso de uso requiere un flujo secuenciado de varios mensajes activado por hitos de uso con ramificación condicional: la mensajería activada por eventos no puede gestionar la lógica predictiva de tiempo y dependencia necesaria para la nutrición basada en hitos.

### Consideraciones técnicas

- Introduzca telemetría de uso del producto (adopción de funciones, frecuencia de inicio de sesión, tiempo en el producto) para crear perfiles de participación de prueba en tiempo real.
- Defina hitos basados en el uso (por ejemplo, primer proyecto creado, función clave utilizada, colaboración invitada) como déclencheur de recorrido para una divulgación oportuna.
- Sincronizar el estado de prueba y los eventos de conversión a [!DNL Salesforce] o [!DNL Microsoft Dynamics] para que los representantes de ventas tengan una visibilidad completa de la actividad de prueba.
- Coordinar con [!DNL Marketo Engage] programas de nutrición para evitar comunicaciones superpuestas durante el período de prueba.


## Éxito del cliente e incorporación

Personalice los recorridos de incorporación del cliente con formación, recursos y asistencia relevantes en función del producto comprado y del perfil del cliente. La incorporación efectiva reduce el tiempo de respuesta al valor y establece las bases para la retención y el crecimiento del cliente a largo plazo.

### Impacto empresarial

Las organizaciones con programas de incorporación personalizados ven una mejor adopción de funciones en los primeros 90 días, lo que contribuye directamente a una mayor retención y a los ingresos de expansión.

### Cómo implementar

Utilice el patrón [Recorrido orquestado en varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para organizar secuencias de incorporación adaptadas al producto, nivel de plan y segmento de clientes. Este patrón admite la progresión basada en hitos, lo que garantiza que los clientes reciban la orientación adecuada en cada fase de su incorporación. Este es el patrón correcto cuando el caso de uso requiere un flujo secuenciado de varios mensajes con avance condicional basado en hitos de uso del producto: la mensajería activada por eventos no puede dar cabida a la compleja lógica de ensayo necesaria para la progresión guiada de la incorporación.

### Consideraciones técnicas

- Introduzca telemetría de uso del producto para rastrear los hitos de incorporación (primer inicio de sesión, configuración inicial, primer flujo de trabajo completado) y el déclencheur del siguiente paso de recorrido en consecuencia.
- Asigne perfiles de clientes a la pista de incorporación correcta en función del producto comprado, el nivel de plan y la cantidad de usuarios con licencia.
- Integre los datos de la plataforma de éxito del cliente para mostrar las puntuaciones de estado y marcar las cuentas en riesgo para la intervención proactiva.
- Sincronice las métricas de estado de incorporación y adopción de nuevo a [!DNL Salesforce] o [!DNL Microsoft Dynamics] para que los administradores de éxito de los clientes puedan priorizar el alcance.


## Campañas de renovación de contratos

Involucre de forma proactiva a los clientes que se acercan a la renovación del contrato con ofertas personalizadas, perspectivas de uso e incentivos de renovación. El alcance de la renovación oportuno y basado en datos reduce la pérdida y protege los ingresos recurrentes.

### Impacto empresarial

Las empresas que implementan campañas de renovación personalizadas y proactivas ven tasas de renovación mejoradas, lo que protege los ingresos recurrentes y reduce el coste de la recuperación del cliente.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para entregar la oferta de renovación correcta a través del canal correcto en el momento adecuado. Este patrón combina la orquestación de recorridos con Offer Decisioning, lo que permite incentivos de renovación dinámica basados en el valor y el uso de la cuenta. Este es el patrón correcto cuando el recorrido debe coordinar la entrega a través de los canales y la selección de ofertas requiere restricciones de uso y valor de cuenta; la orquestación de recorridos por sí sola no proporciona la capa de toma de decisiones en tiempo real necesaria para hacer coincidir dinámicamente los incentivos de renovación.

### Consideraciones técnicas

- Extraer las fechas de finalización del contrato, las condiciones de renovación y el valor de la cuenta de [!DNL Salesforce] o [!DNL Microsoft Dynamics] a los recorridos de renovación de déclencheur en el tiempo de espera adecuado (por ejemplo, dentro de 90, 60 o 30 días).
- Incorpore datos de uso del producto y puntuaciones de estado del cliente para determinar el riesgo de renovación y adaptar la estrategia de oferta en consecuencia.
- Utilice la toma de decisiones para seleccionar el incentivo óptimo de renovación (descuento, términos ampliados, actualización de la prima) en función del valor de duración de la cuenta y la probabilidad de pérdida.
- Coordine la extensión de la renovación con los equipos de éxito y ventas del cliente para evitar mensajes conflictivos mediante la asignación de tareas de [!DNL Marketo Engage] y CRM.


## Oportunidades de ampliación de ventas y expansión

Identifique a los clientes listos para recibir actualizaciones de productos o licencias adicionales en función de patrones de uso, indicadores de crecimiento y datos de éxito de los clientes. El alcance de la expansión proactiva convierte el impulso del cliente en crecimiento de ingresos.

### Impacto empresarial

Las organizaciones que identifican sistemáticamente las señales de expansión y actúan en ellas generan mayores ingresos de expansión, lo que mejora la retención de ingresos netos y el valor de duración del cliente.

### Cómo implementar

Use el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para ofrecer ofertas personalizadas de ampliación y ventas adicionales basadas en señales de cuenta y uso en tiempo real. Este patrón utiliza la toma de decisiones para hacer coincidir cada cuenta con la oferta de expansión más relevante entre canales. Este es el patrón correcto cuando el recorrido debe coordinar la entrega a través de los canales y la selección de ofertas requiere reglas de elegibilidad que regulen qué ofertas de expansión coinciden con cuentas específicas: la orquestación de recorridos por sí sola no proporciona el nivel de toma de decisiones necesario para la coincidencia de ofertas impulsada por restricciones.

### Consideraciones técnicas

- Introduzca telemetría de uso del producto para detectar señales de expansión como umbrales de utilización de licencias, visitas al techo de funciones y recuentos de usuarios en aumento.
- Cree modelos de tendencia de nivel de cuenta con datos de expansión históricos, tendencias de uso y atributos firmográficos.
- Sincronice las oportunidades de expansión y las ofertas recomendadas de nuevo en [!DNL Salesforce] o [!DNL Microsoft Dynamics] para que los equipos de ventas puedan hacer un seguimiento de la canalización generada por el marketing.
- Coordínese con [!DNL Marketo Engage] para asegurarse de que los mensajes de expansión no entren en conflicto con las comunicaciones de soporte o renovación en curso.


## Campañas de sustitución competitivas

Segmente a los posibles clientes con productos de la competencia, mensajes personalizados, ofertas de migración y comparaciones competitivas. Al abordar los puntos problemáticos específicos asociados con cada competidor, los equipos de marketing pueden diferenciarse de forma más eficaz y acelerar las decisiones de cambio.

### Impacto empresarial

Las organizaciones B2B que llevan a cabo campañas de sustitución competitivas específicas ven mejores tasas de beneficio competitivas, capturando cuota de mercado y desplazando a los proveedores históricos.

### Cómo implementar

Use el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para orquestar campañas competitivas de varios contactos adaptadas al perfil específico del competidor y del posible cliente. Este patrón admite la ramificación condicional basada en los competidores identificados, lo que permite enviar mensajes que abordan los puntos problemáticos únicos de cada escenario competitivo. Este es el patrón correcto cuando el caso de uso requiere un flujo secuenciado de varios mensajes con ramificación condicional basada en el perfil específico del competidor y del cliente potencial: la mensajería activada por eventos no puede gestionar la complejidad de la lógica de ramificación específica del competidor en varios puntos de contacto.

### Consideraciones técnicas

- Integre datos de inteligencia competitiva (por ejemplo, proveedores tecnográficos, campos de competidor de CRM) en el perfil unificado para identificar qué competidor utiliza actualmente un cliente potencial.
- Cree recursos de contenido específicos de la competencia (guías de migración, hojas comparativas, calculadoras de ROI) y asígnelos a bloques de contenido de recorrido.
- Coordínese con [!DNL Marketo Engage] para eliminar las campañas competitivas de los posibles clientes que ya están en ciclos de ventas activos o en los clientes existentes.
- Rastree la canalización de desplazamiento competitivo en [!DNL Salesforce] o [!DNL Microsoft Dynamics] con atribución de campaña dedicada para medir la eficacia del programa.


## Programación de seminarios web y demostraciones

Personalice las invitaciones a seminarios web y la programación de demostraciones en función de los intereses del cliente potencial, el sector y el historial de participación. Las invitaciones relevantes y oportunas aumentan la asistencia y generan una canalización de mayor calidad a partir de interacciones en vivo.

### Impacto empresarial

Los programas personalizados de invitaciones a seminarios web y demostraciones ven tasas de asistencia a seminarios web mejoradas, lo que impulsa una canalización más calificada a partir de oportunidades de participación en vivo.

### Cómo implementar

Use el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para enviar invitaciones personalizadas cuando los posibles clientes muestren señales de interés alineadas con los próximos temas de seminarios web o demostraciones. Este patrón responde en tiempo real a los déclencheur de comportamiento, lo que garantiza que las invitaciones lleguen cuando el interés es más alto. Este es el patrón correcto cuando el déclencheur es una acción discreta del cliente alineada con la relevancia del seminario web y la respuesta requerida es una invitación única y con distinción de tiempo, en lugar de una secuencia de varios pasos o un programa de nutrición continuo.

### Consideraciones técnicas

- Defina eventos de déclencheur basados en intereses (por ejemplo, visita una página de producto, descarga de un recurso relacionado, participación en una comparación de competidores) que se alineen con los temas programados de seminarios web o demostración.
- Integre los datos de la plataforma del seminario web (por ejemplo, [!DNL ON24], [!DNL Zoom Webinar]) para rastrear las métricas de registro, asistencia y participación dentro del perfil unificado.
- Sincronizar solicitudes de demostración y datos de programación con [!DNL Salesforce] o [!DNL Microsoft Dynamics] para garantizar que los equipos de ventas reciban notificaciones y contexto a tiempo.
- Coordine la cadencia de la invitación con los límites de comunicación de [!DNL Marketo Engage] para evitar que los posibles clientes que califican para varios eventos sobrepasen los mensajes.


## Caso práctico y ROI Personalization

Ofrezca casos prácticos personalizados, calculadoras de ROI e historias de éxito basadas en el sector del cliente potencial, el tamaño de la empresa y el caso de uso. Cuando los clientes potenciales ven puntos de prueba de organizaciones similares a las suyas, la confianza se genera más rápido y las decisiones de compra se aceleran.

### Impacto empresarial

Las organizaciones que personalizan el contenido de puntos de prueba ven una participación mejorada en los estudios de casos, lo que contribuye a una mayor confianza en los acuerdos y a tasas de cierre más rápidas.

### Cómo implementar

Utilice el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones/web de visitantes conocidos para obtener dinámicamente los casos prácticos y las pruebas de retorno de la inversión más relevantes en función del perfil de cada posible cliente. Este patrón hace coincidir los atributos del visitante con una biblioteca de contenido, lo que garantiza que todos los clientes potenciales vean puntos de prueba de su sector y grupo de compañeros. Este es el patrón correcto cuando la personalización está impulsada por atributos de perfil y pertenencia a segmentos en lugar de por un modelo de afinidad de comportamiento, lo que permite que los atributos de tamaño del sector y de la empresa coincidan con los posibles clientes y los puntos de prueba relevantes.

### Consideraciones técnicas

- Etiquete el estudio del caso práctico y los activos de contenido de ROI con metadatos (sector, tamaño de la empresa, caso de uso, producto) para permitir la coincidencia dinámica con perfiles de clientes potenciales.
- Implemente reglas de personalización que prioricen primero la coincidencia en el sector y, después, el tamaño de la empresa y el caso de uso, con contenido de reserva para clientes potenciales con datos de perfil limitados.
- Integre las señales de participación de contenido (descargas, tiempo en la página, recursos compartidos) en el perfil unificado para informar la puntuación de posibles clientes y el alcance de las ventas.
- Coordínese con [!DNL Marketo Engage] para incluir contenido de puntos de prueba personalizado en las secuencias de correo electrónico de nutrición, no solo en las experiencias en el sitio.


## Programas de defensa del cliente

Identifique y capte a los clientes satisfechos con respecto a las oportunidades de promoción, como referencias, estudios de casos y testimonios, en función del uso y los datos de satisfacción. Los clientes felices son un poderoso motor de crecimiento cuando son reconocidos e invitados a compartir su éxito.

### Impacto empresarial

Los programas estructurados de defensa del cliente impulsan una mejor participación en la defensa, generando un flujo constante de referencias, estudios de casos y testimonios que apoyan la adquisición de nuevos negocios.

### Cómo implementar

Utilice el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para generar flujos de trabajo de participación e identificación de actividades de promoción que respondan a las señales de satisfacción y uso. Este patrón apoya las tareas de promoción progresivas, empezando con una participación ligera (por ejemplo, una revisión) y avanzando hacia compromisos más profundos (por ejemplo, una llamada de referencia o un estudio de caso). Este es el patrón correcto cuando el caso de uso requiere un flujo secuenciado de varios mensajes con avance condicional basado en las señales de satisfacción y uso: un solo mensaje activado no puede admitir la lógica de participación progresiva necesaria para escalar las solicitudes de promoción a lo largo del tiempo.

### Consideraciones técnicas

- Ingeste los resultados de la encuesta de satisfacción (por ejemplo, la puntuación de Net Promoter, las puntuaciones de satisfacción del cliente) y los datos de uso del producto para generar una puntuación de preparación para la promoción para cada cuenta.
- Defina criterios de elegibilidad para la promoción que combinen umbrales de satisfacción, hitos de uso y tenencia de cuenta para evitar el alcance prematuro.
- Sincronice el estado de la promoción y el historial de participación a [!DNL Salesforce] o [!DNL Microsoft Dynamics] para que los equipos de ventas puedan hacer referencia a los defensores de los clientes durante la prospección.
- Coordinar con [!DNL Marketo Engage] para suprimir la divulgación de promoción durante las negociaciones activas de ampliación o renovación de apoyo.

## Audience Activation basado en cuentas B2B

Cree audiencias de nivel de cuenta que combinen datos firmográficos, señales de grupo de compra y participación de nivel de persona y, a continuación, actívelas en LinkedIn, plataformas del lado de la demanda y destinos CRM. La activación de audiencias basada en cuentas permite a las organizaciones B2B dirigirse a organizaciones de compra completas con publicidad digital coordinada en lugar de a contactos individuales, alineando el gasto en medios pagados con las prioridades del flujo de cuentas.

### Impacto empresarial

Las organizaciones B2B con activación de audiencia basada en cuentas ven una influencia más fuerte en la canalización desde programas de medios de pago, con un impacto especialmente alto cuando los segmentos de audiencia están alineados con las prioridades del territorio de ventas y se actualizan con frecuencia a medida que cambian las puntuaciones de participación de la cuenta.

### Cómo implementar

Utilice el patrón [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md) para generar segmentos de nivel de cuenta mediante relaciones entre la cuenta y la persona y activarlos en destinos de medios de pago compatibles con B2B. Este es el patrón correcto cuando la creación de audiencias debe funcionar a nivel de cuenta (combinando señales de varios contactos dentro de una organización compradora) en lugar de a nivel de persona individual.

### Consideraciones técnicas

- La configuración del gráfico de identidad B2B debe vincular con precisión a las personas conocidas con sus registros de cuenta; las lagunas en las asociaciones de personas de cuentas resultarán en una agregación incompleta de la señal de grupo de compra.
- Los segmentos de audiencia de cuenta deben actualizarse con una programación que se ajuste a las fechas de vuelo de la campaña y a la cadencia de revisión de la canalización; los segmentos que se alejan del estado de canalización actual reducen la eficacia del gasto en medios.
- Las audiencias coincidentes de LinkedIn y plataformas B2B similares coinciden en las direcciones de correo electrónico profesionales, que pueden diferir de las direcciones de correo electrónico personales almacenadas en CRM; ambos tipos de correo electrónico deben incluirse en las cargas de audiencia.
- Las audiencias de activación deben excluir las cuentas en etapas de acuerdo activo en las que la publicidad de pago podría crear una superposición incómoda con el alcance de ventas directo.


## Grupo de compra Journey Orchestration

Orqueste recorridos a nivel de cuenta que nutren a los miembros del grupo de compra en función de sus funciones, puntuaciones de participación y estado de calificación de la cuenta, con transferencia automatizada a ventas. La coordinación de la lógica de recorrido a nivel de grupo de compra en lugar de a nivel individual garantiza que cada parte interesada reciba mensajes adecuados a su función y fase de decisión, al tiempo que mantiene la coherencia dentro de la cuenta.

### Impacto empresarial

Las organizaciones B2B que utilizan la orquestación de recorrido de grupo de compra ven tasas de creación de oportunidades mejoradas a partir de la canalización con fuentes de marketing y una progresión más rápida a través de las primeras etapas de las operaciones, especialmente cuando el traspaso de ventas se activa automáticamente en función de umbrales de participación mensurables.

### Cómo implementar

Use el patrón [Marketing basado en grupos de compras](/help/blueprints/use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md) para crear recorridos calificados para la cuenta que segmenten a los miembros del grupo de compras por función, evalúen las señales de participación a nivel de grupo y organicen campañas multipersona y multitáctil coordinadas con ramificación condicional basada en el estado de la cuenta. Este es el patrón correcto cuando la lógica de recorrido debe funcionar a nivel de grupo de cuentas en lugar de a nivel de persona individual: la orquestación de recorrido estándar a nivel de persona no puede gestionar los requisitos de cualificación de grupo y coordinación interpersonal de la gestión de grupos de compra B2B.

### Consideraciones técnicas

- Las definiciones de pertenencia a grupos compradores deben mantenerse en el modelo de datos B2B, vinculando los contactos conocidos a sus cuentas y asignándoles funciones como campeón, comprador económico o evaluador técnico.
- La puntuación de participación en la cuenta debe acumular señales de varios individuos dentro del grupo comprador; la participación de un solo contacto es insuficiente para determinar la preparación de la cuenta.
- La supresión de recorridos debe sincronizarse con las fases de oportunidad de CRM para evitar que los mensajes de automatización de marketing entren en conflicto con las conversaciones de ventas activas.
- Las notificaciones de entrega y alerta de ventas deben integrarse con CRM y la plataforma de participación de ventas para que los representantes reciban un contexto oportuno y procesable cuando las cuentas alcancen el umbral de entrega.


## Account-Based Marketing (ABM) Personalization

Personalice las comunicaciones de marketing y el contenido para cuentas de Target en función del perfil de la cuenta, el historial de participación y las señales de compra. La personalización ABM va más allá de la segmentación de cuentas al personalizar el contenido de los mensajes y las experiencias web para los desafíos empresariales conocidos, el tamaño y el sector específico de cada cuenta, lo que crea una relevancia que los mensajes de campaña genéricos no pueden alcanzar.

### Impacto empresarial

Las organizaciones B2B con personalización a nivel de cuenta informan de tasas de participación mejoradas en las campañas salientes y de una mayor conversión de la web a la canalización para cuentas de destino, con resultados especialmente sólidos cuando la personalización se extiende a las páginas de destino y a las experiencias del sitio web visitadas a través de medios de pago.

### Cómo implementar

Utilice el patrón [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md) para activar perfiles de nivel de cuenta para la personalización en canales web y de salida. Este es el patrón correcto cuando el requisito principal es la segmentación a nivel de cuenta para la personalización en lugar de la orquestación de recorrido a nivel de contacto: los datos de perfil de cuenta impulsan las decisiones de personalización en lugar de las señales de comportamiento individuales.

### Consideraciones técnicas

- Los datos de los firmográficos de la cuenta (sector, tamaño de la empresa, ubicación geográfica y pila de tecnología) deben estar actualizados y estar modelados de forma coherente para impulsar una personalización de contenido significativa más allá de la segmentación genérica a nivel de sector.
- La personalización web para visitantes B2B conocidos requiere resolución de IP a cuenta o autenticación directa; la resolución basada en IP tiene una precisión menor y no se debe confiar en ella para decisiones de cuenta de alto valor.
- El contenido debe desarrollarse para cada segmento de cuenta segmentado con personalización; activar la personalización sin variaciones de contenido suficientes hará que algunas cuentas reciban experiencias sin cambios.
- Las decisiones de Personalization a nivel de cuenta deben alinearse con la fase actual de CRM y la actividad de ventas para evitar ofrecer contenido de reconocimiento de funnel superior a las cuentas que ya están en acuerdos activos.
