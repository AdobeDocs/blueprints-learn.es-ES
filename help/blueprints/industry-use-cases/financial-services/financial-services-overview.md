---
title: Casos prácticos de servicios financieros
description: Descubra cómo las organizaciones de servicios financieros utilizan Adobe Experience Platform para personalizar ofertas de productos, evitar la pérdida y profundizar las relaciones con los clientes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 1f22d684-11bd-473d-8b10-5f88cb0cd088
source-git-commit: 0236bd326730ee9a0be621ee0e60ddc3d352410d
workflow-type: tm+mt
source-wordcount: '4039'
ht-degree: 0%

---

# Casos prácticos de servicios financieros

Las organizaciones de servicios financieros dependen de Adobe Experience Platform para unificar los datos de los clientes en los canales bancario, de préstamo y de inversión, lo que permite experiencias personalizadas que fortalecen las relaciones e impulsan el crecimiento. Al reunir la actividad de la cuenta, el historial de transacciones y las señales de comportamiento, estas organizaciones pueden ofrecer la oferta correcta en el momento adecuado y, al mismo tiempo, mantener la confianza y el cumplimiento que esperan sus clientes.

## Nutrición de plomo de alto valor

Identifique los posibles clientes de alto valor en función de los datos y el comportamiento del perfil y, a continuación, nutra a los mismos con contenido y ofertas personalizados mediante recorridos automatizados. Al combinar los detalles demográficos, la actividad de navegación y las señales de participación, las instituciones financieras pueden priorizar a los posibles clientes más propensos a convertirlos y guiarlos a través de un camino adaptado para convertirse en clientes.

### Impacto empresarial

Las organizaciones que implementan la nutrición de clientes potenciales de alto valor ven tasas de conversión de clientes potenciales mejoradas mientras construyen un canal de ventas más saludable y predecible.

### Cómo implementar

Utilice el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para crear secuencias de nutrición automatizadas que se adapten según las señales de participación y preparación del posible cliente. Este es el patrón correcto cuando el caso de uso requiere un flujo secuenciado de varios mensajes a lo largo de días con ramificación condicional basada en métricas de participación: un solo mensaje activado no puede dar cabida a la lógica de nutrición adaptativa o a la lógica de dependencia entre pasos de calificación.

### Consideraciones técnicas

- Integre datos de puntuación de posibles clientes CRM y eventos de comportamiento del sitio web en perfiles de clientes potenciales unificados para potenciar la lógica de entrada y ramificación del recorrido.
- Asegúrese de que las preferencias de consentimiento y de inclusión se apliquen en cada punto de contacto, especialmente en el caso de la divulgación por teléfono y correo electrónico regida por las regulaciones de marketing financiero.
- Configure la restricción de recorrido para evitar perspectivas abrumadoras con varias comunicaciones durante períodos cortos de evaluación.
- Tenga en cuenta la latencia de datos entre las interacciones de sucursales o asesores y la participación digital para mantener relevante la mensajería nutritiva.


## Recomendación de productos para clientes existentes

Recomendar productos financieros relevantes, como tarjetas de crédito, préstamos y productos de inversión, a clientes existentes en función de su perfil, historial de transacciones y fase de vida. Este caso de uso convierte los datos de cuenta diarios en perspectivas procesables que muestran el siguiente mejor producto para cada cliente.

### Impacto empresarial

Las recomendaciones personalizadas de productos impulsan mayores tasas de adopción de productos y aumentan de forma mensurable el valor de duración del cliente al profundizar el uso compartido de billeteras.

### Cómo implementar

Use el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) para evaluar a cada cliente con respecto a ofertas de productos elegibles en tiempo real, clasificando las recomendaciones por relevancia y prioridad comercial. Este es el patrón correcto cuando la selección de ofertas debe tener en cuenta las reglas de idoneidad financiera y las restricciones de elegibilidad regulatorias, restricciones que requieren una lógica de toma de decisiones regida en lugar de una clasificación de afinidad de comportamiento por sí sola.

### Consideraciones técnicas

- Unificar los datos de transacción, los saldos de cuenta y las tenencias de productos en un único perfil de cliente para que los modelos de toma de decisiones tengan una visión completa de las relaciones existentes.
- Aplique reglas de idoneidad financiera y restricciones de elegibilidad regulatorias como barreras duras dentro del motor de decisión antes de clasificar las ofertas.
- Coordine la entrega de ofertas en los canales de banca en línea, aplicación móvil, correo electrónico y asesor para evitar recomendaciones conflictivas o duplicadas.
- Implemente límites de frecuencia por categoría de producto para evitar la fatiga de las recomendaciones, especialmente para productos de alta consideración como hipotecas y cuentas de inversión.


## Campañas de prevención de pérdida

Identifique a los clientes en riesgo de pérdida mediante el uso de la predicción de pérdida con tecnología de IA e inclúyalos en ofertas de retención y comunicaciones personalizadas. La detección temprana de señales de desconexión permite que las instituciones financieras intervengan antes de que un cliente cierre cuentas o mueva activos a otro lugar.

### Impacto empresarial

Los esfuerzos proactivos de prevención de pérdida ayudan a reducir la desgaste del cliente, protegiendo los flujos de ingresos recurrentes y reduciendo el coste de sustitución del cliente.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para almacenar en déclencheur los recorridos de retención cuando las puntuaciones de riesgo de pérdida excedan los umbrales definidos, con toma de decisiones integrada para seleccionar la oferta de retención más atractiva. Este es el patrón correcto cuando el recorrido debe coordinar la entrega a través de los canales para evitar ofertas de retención duplicadas y cuando la selección de ofertas requiere umbrales de puntuación de riesgo y restricciones empresariales: la orquestación de varios pasos por sí sola no proporciona el nivel de toma de decisiones en tiempo real necesario para seleccionar la oferta de retención óptima por cliente.

### Consideraciones técnicas

- Tendencias de actividad de cuenta de fuente, historial de interacción de servicio y frecuencia de participación en [!DNL Customer AI] modelos de tendencia a la pérdida para generar puntuaciones de riesgo.
- Defina umbrales de riesgo de pérdida específicos para las líneas de producto, ya que las señales de desconexión para las cuentas de cheques difieren de las de las carteras de inversión.
- Revise los criterios de segmentación y supresión con sus equipos legales y de privacidad para garantizar el cumplimiento de las regulaciones aplicables de préstamo justo e igualdad de trato antes de activar ofertas de retención.
- Genere una lógica de supresión para excluir a los clientes que se producen debido a acciones de fraude o cumplimiento, donde el alcance de la retención sería inapropiado.


## Tablero de cuenta personalizado

Personalice el tablero de banca en línea y la experiencia de la aplicación móvil en función de la actividad de la cuenta, las preferencias y los objetivos financieros de cada cliente. Un tablero personalizado ayuda a los clientes a encontrar lo que más importa y muestra perspectivas relevantes sin que tengan que buscar.

### Impacto empresarial

Los paneles personalizados aumentan las tasas de participación y mejoran significativamente las puntuaciones de satisfacción del cliente al hacer que la banca digital se sienta intuitiva y relevante.

### Cómo implementar

Use el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones y web de visitantes conocidos para ofrecer bloques de contenido personalizado en tiempo real, detalles de productos y perspectivas financieras dentro de experiencias digitales autenticadas. Este es el patrón correcto cuando la personalización está impulsada por atributos de perfil y actividad de cuenta en lugar de un modelo de afinidad de comportamiento y cuando la latencia de subsegundos es crítica para la experiencia del usuario.

### Consideraciones técnicas

- Aproveche [!DNL Edge Network] para decisiones de personalización por debajo del segundo en sesiones bancarias autenticadas en las que la latencia afecte directamente a la experiencia del usuario.
- Agregue datos de transacciones en atributos de perfil precalculados, como categorías de gasto y tendencias de ahorro, para evitar el cálculo en tiempo real de grandes conjuntos de datos.
- Cumplan con los estándares de accesibilidad y garanticen que el contenido personalizado cumpla los mismos requisitos regulatorios de divulgación que el contenido estático.
- Coordine la lógica de personalización entre los canales web y móvil para que los clientes vean una experiencia coherente independientemente del dispositivo.


## Ofertas de productos por fases de Life

Identifique a los clientes que entran en nuevas etapas de vida, como el matrimonio, la compra de una vivienda o la jubilación, y ofrezca de forma proactiva productos y servicios financieros relevantes. Anticipar estos hitos permite a las instituciones posicionarse como socios de confianza durante momentos financieros cruciales.

### Impacto empresarial

Las ofertas activadas por etapas de duración logran tasas de adopción de productos más sólidas, superando a las campañas genéricas, a la vez que fortalecen las relaciones con los clientes a largo plazo.

### Cómo implementar

Utilice el patrón [Cross-Channel Recorrido with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para detectar indicadores de etapa de vida y orquestar recorridos multitáctiles con selección de ofertas incrustadas adaptadas a cada hito. Este es el patrón correcto cuando el recorrido debe coordinar la entrega a través de los canales durante los momentos financieros fundamentales y cuando la selección de la oferta requiere comprobaciones de idoneidad y reglas comerciales: la orquestación de varios pasos por sí sola no proporciona el nivel de toma de decisiones necesario para garantizar la conformidad y la relevancia.

### Consideraciones técnicas

- Combine señales de origen, como cambios de dirección, aperturas de cuentas conjuntas y grandes depósitos, con datos de terceros autorizados para deducir transiciones de fase de vida.
- Gestione los eventos personales confidenciales con cuidado en el tono y la frecuencia de la mensajería, ya que los hitos inferidos incorrectamente pueden erosionar la confianza.
- Capar las comprobaciones de idoneidad regulatoria en Offer Decisioning para que los productos recomendados se alineen con la situación financiera verificada del cliente.
- Cree periodos de enfriamiento entre las campañas de fase de vida para evitar la superposición de alcance cuando varios indicadores se activen en una ventana corta.


## Alertas y recomendaciones basadas en transacciones

Envíe alertas en tiempo real de transacciones y proporcione recomendaciones personalizadas basadas en patrones de gasto y actividad de cuenta. Las notificaciones oportunas y relevantes mantienen informados a los clientes y crean momentos naturales para que aparezcan directrices financieras útiles.

### Impacto empresarial

Las alertas basadas en transacciones impulsan una participación sólida, mejorando la concienciación sobre la seguridad y creando puntos de contacto de alto valor para recomendaciones personalizadas.

### Cómo implementar

Use el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para responder a eventos de transacción en tiempo real con alertas y recomendaciones relevantes para el contexto. Este es el patrón correcto cuando el déclencheur es un evento del sistema en lugar de un comportamiento del cliente y cuando la comunicación necesaria es inmediata y reactiva en lugar de una secuencia de nutrición sostenida: la latencia de la alerta afecta directamente a la eficacia de la seguridad.

### Consideraciones técnicas

- Ingeste eventos de transacción a través de una canalización de flujo continuo con requisitos de entrega de baja latencia, ya que las alertas de seguridad pierden valor si se retrasan más de unos minutos.
- Aplique las preferencias y umbrales de alerta definidos por el cliente para que las notificaciones reflejen la configuración individual en lugar de las reglas únicas para todos los casos.
- Separe las alertas de seguridad obligatorias de los mensajes de recomendación opcionales en la arquitectura de mensajería para garantizar que las notificaciones de conformidad nunca se supriman.
- Tenga en cuenta los altos volúmenes de transacciones durante los períodos de mayor actividad, como los días de pago y los festivos, diseñando una capacidad de rendimiento que se escale según la demanda.


## Recuperación de abandono de solicitud de tarjeta de crédito

Identifique a los clientes que iniciaron las solicitudes de tarjeta de crédito, pero no las completaron, y vuelva a interactuar con ellos con mensajes y ofertas personalizados. El abandono de aplicaciones representa una audiencia con muchas intenciones que a menudo solo necesita un pequeño empujón para completar el proceso.

### Impacto empresarial

Las campañas de recuperación de abandonos mejoran las tasas de finalización de las aplicaciones, lo que aumenta directamente la adquisición de nuevas cuentas de una audiencia que ya ha expresado interés.

### Cómo implementar

Utilice el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para detectar eventos de abandono de aplicaciones y mensajes de seguimiento oportunos de déclencheur que aborden motivos comunes de abandono. Este es el patrón correcto cuando una acción de cliente discreta (abandono) es el déclencheur y la respuesta necesaria es un mensaje con distinción de tiempo que se envía antes de que los datos de la aplicación se vuelvan obsoletos: una secuencia de varios pasos no puede dar cabida a la ventana de recuperación de urgencia y estrecha.

### Consideraciones técnicas

- Capture el paso específico en el que se abandonó la aplicación para adaptar la mensajería, ya que alguien que abandonó en la verificación de identidad necesita una tranquilidad diferente a alguien que abandonó en la revisión de términos.
- Trabaje con sus equipos legales y de cumplimiento para confirmar que todas las comunicaciones de recuperación cumplen los requisitos aplicables de divulgación de marketing crediticio y las reglas de consentimiento específicas del canal antes de la implementación.
- Implemente una lógica de decadencia de tiempo para que el alcance de la recuperación se detenga después de una ventana definida, ya que los datos de aplicaciones antiguas pueden dejar de ser válidos para la precalificación.
- Coordínese con el sistema de solicitud para suprimir los mensajes de recuperación para los solicitantes que completaron a través de un canal diferente, como una visita a una sucursal o una llamada telefónica.


## Recomendaciones de Portfolio de inversión

Proporcione recomendaciones de inversión personalizadas en función del perfil de riesgo, el historial de inversión y los objetivos financieros de cada cliente. La orientación de portafolios basada en datos ayuda a los clientes a tomar decisiones informadas a la vez que profundizan su participación en los servicios de gestión de patrimonios.

### Impacto empresarial

Las recomendaciones de inversión personalizadas impulsan una mayor adopción de productos de inversión y mejoran la diversificación de la cartera en toda la base de clientes.

### Cómo implementar

Use el patrón [Recomendación de comportamiento](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) para analizar el comportamiento y las preferencias de la inversión y, a continuación, mostrar recomendaciones de portafolio relevantes a través de canales digitales y herramientas de asesoramiento. Este es el patrón correcto cuando el conjunto de elementos (entorno de inversión) es grande y la selección está impulsada por la afinidad del comportamiento y la alineación del riesgo, en lugar de un conjunto limitado de ofertas gobernadas por reglas de idoneidad estrictas o decisiones de comprobación de idoneidad por sí solas.

### Consideraciones técnicas

- Integre fuentes de datos de corretaje y custodia para mantener una vista precisa y actualizada de las tenencias y asignaciones actuales de cada cliente.
- Haga cumplir los requisitos de idoneidad exigidos por las regulaciones de valores para que las recomendaciones se ajusten a la tolerancia al riesgo y los objetivos de inversión documentados del cliente.
- Etiquete claramente el contenido de inversión personalizado como educativo o informativo cuando sea necesario, distinguiéndolo del asesoramiento de inversión formal que conlleva obligaciones fiduciarias.
- Actualice los modelos de recomendación en una cadencia regular para tener en cuenta los cambios de mercado, la deriva de la cartera y los cambios en los objetivos de los clientes.


## Alerta de fraude Personalization

Personalice las alertas de fraude y las comunicaciones de seguridad en función de las preferencias de comunicación de cada cliente y del historial de interacción anterior. Las alertas personalizadas aumentan la probabilidad de que los clientes detecten y comprendan las notificaciones de seguridad críticas y actúen en consecuencia.

### Impacto empresarial

Las alertas de fraude personalizadas mejoran las tasas de respuesta a las alertas, fortaleciendo el cumplimiento de la seguridad y reduciendo la ventana de exposición durante actividades sospechosas.

### Cómo implementar

Utilice el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para entregar alertas de fraude a través del canal preferido de cada cliente con detalles contextuales que faciliten la confirmación o la disputa de la actividad. Este es el patrón correcto cuando el déclencheur es un evento del sistema en lugar de un comportamiento del cliente y cuando la comunicación necesaria es inmediata y reactiva sin tiempo para secuencias de varios pasos: la latencia de la alerta se correlaciona directamente con la exposición a pérdidas financieras.

### Consideraciones técnicas

- Priorice la velocidad y fiabilidad de entrega por encima de todas las demás consideraciones de diseño, ya que la latencia de las alertas de fraude se correlaciona directamente con la exposición a pérdidas financieras.
- Enrute las alertas a través del canal preferido verificado del cliente mientras mantiene los canales de reserva para garantizar la entrega incluso si falla el canal principal.
- Historial de interacción de alertas de tienda para mejorar la relevancia de alertas futuras y reducir la fatiga por falsos positivos para los clientes que viajan con frecuencia o realizan compras atípicas.
- Asegúrese de que todo el contenido y los flujos de trabajo de alertas de fraude cumplan con las normas de seguridad bancaria y no expongan los detalles confidenciales de la cuenta en las vistas previas de los mensajes o las líneas de asunto.


## Participación del programa de fidelización

Personalice las comunicaciones, las recompensas y las ofertas del programa de fidelización organizando la mediación de ofertas en tiempo real en los canales de banca en línea, aplicación móvil, correo electrónico y sucursal para evitar que las ofertas de fidelidad duplicadas o en conflicto lleguen al mismo miembro simultáneamente. Las reglas de elegibilidad basadas en niveles (que rigen a qué recompensas, promociones y opciones de canje puede acceder cada miembro) se aplican en el nivel de toma de decisiones en lugar de resolverse únicamente a través de la segmentación, lo que garantiza que la selección de ofertas respete las restricciones del programa en todos los canales. Los recorridos de fidelización se coordinan con campañas de marketing más amplias para que las ofertas de productos y fidelidad no entren en conflicto, lo que proporciona a los miembros una experiencia coherente en lugar de mensajes de la competencia.

### Impacto empresarial

La participación de lealtad personalizada aumenta la participación en el programa e impulsa una canje de puntos significativamente mayor, lo que fortalece la percepción de valor del programa.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para orquestar las comunicaciones de fidelidad entre canales, con toma de decisiones incrustada para seleccionar la recompensa u oferta más relevante para cada miembro. Este es el patrón correcto cuando el recorrido debe coordinar la entrega a través de los canales para evitar la fatiga del mensaje y las ofertas conflictivas, y cuando la selección de ofertas requiere reglas basadas en niveles y restricciones de miembros: la orquestación de varios pasos por sí sola no proporciona la capa de toma de decisiones en tiempo real necesaria para respetar las reglas de lealtad y el tratamiento diferenciado de los miembros.

### Consideraciones técnicas

- Sincronice los datos de la plataforma de fidelización, incluido el estado del nivel, los saldos de puntos y el historial de canje, en los perfiles de los clientes en tiempo casi real para evitar promocionar los saldos caducados o inexactos.
- Segmente la lógica de recorrido por nivel para ofrecer experiencias diferenciadas, ya que los miembros de alto nivel esperan un tratamiento exclusivo y un acceso anticipado a las promociones.
- Coordine la mensajería de fidelidad con campañas de marketing más amplias para evitar que los mensajes se agoten y las ofertas conflictivas entre programas.
- Realice un seguimiento de la atribución de canje en todos los canales para medir qué comunicaciones personalizadas generan el mayor retorno de la inversión en el programa.


## Campañas de preaprobación de hipotecas

Clientes objetivo que es probable que estén en el mercado de una hipoteca en función de datos de perfil, señales de comportamiento e indicadores de fase de vida. El alcance proactivo previo a la aprobación posiciona a la institución como una primera opción conveniente durante una de las mayores decisiones financieras que un cliente tomará.

### Impacto empresarial

Las campañas de preaprobación de hipotecas dirigidas aumentan las tasas de solicitud y mejoran el volumen de originación de préstamos al alcanzar perspectivas calificadas en el momento adecuado.

### Cómo implementar

Use el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para guiar a los posibles clientes hipotecarios a través de una secuencia de nutrición multitáctil, desde la concienciación hasta la aprobación previa, adaptándose en función de las señales de participación y calificación. Este es el patrón correcto cuando el caso de uso requiere un flujo secuenciado de varios mensajes en una cronología extendida con ramificación condicional basada en señales de participación y calificación; un solo mensaje activado no puede admitir la lógica de nutrición adaptativa o el traspaso a procesos de aplicación formales.

### Consideraciones técnicas

- Combine el comportamiento de búsqueda de propiedades, las tendencias de crecimiento de ahorros y las señales de caducidad de arrendamientos para construir un modelo de tendencia que identifique a los probables solicitantes de hipotecas.
- Asegúrese de que todos los mensajes de preaprobación cumplan con las regulaciones de publicidad hipotecaria, incluidas las divulgaciones requeridas, la precisión de la tasa y el lenguaje de vivienda equitativo.
- Coordine el tiempo de la campaña con los cambios del entorno de tasas para que el alcance se ajuste a las condiciones de endeudamiento favorables y evite referencias de tasas obsoletas.
- Cree flujos de trabajo de transferencia a los responsables de préstamos para que los posibles clientes alimentados digitalmente realicen la transición sin problemas al proceso formal de solicitud y suscripción.


## Contenido personalizado de educación financiera

Ofrezca contenido, sugerencias y recursos personalizados de educación financiera en función del perfil financiero, los objetivos y los intereses de cada cliente. El contenido educativo relevante genera confianza, mejora la alfabetización financiera y crea oportunidades orgánicas para introducir productos relevantes.

### Impacto empresarial

El contenido educativo personalizado aumenta las tasas de participación en el contenido y mejora la alfabetización financiera de los clientes, lo que a su vez aumenta la confianza en la adopción de productos.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para ofrecer una secuencia revisada de contenido educativo en canales múltiples, usando la toma de decisiones para relacionar los temas con la situación financiera y los intereses de cada cliente. Este es el patrón correcto cuando el recorrido debe coordinar la entrega a través de canales con rutas de aprendizaje progresivas y cuando la selección de temas requiere reglas de idoneidad basadas en el perfil financiero: la orquestación de varios pasos por sí sola no proporciona la capa de toma de decisiones necesaria para hacer coincidir el contenido con la situación financiera del cliente o evitar infracciones de requisitos previos.

### Consideraciones técnicas

- Asigne contenido educativo a atributos de perfil financiero como la relación deuda-ingresos, la tasa de ahorro y la experiencia de inversión para garantizar la relevancia del tema.
- Etiquete contenido con niveles de dificultad y temas de requisitos previos para crear rutas de aprendizaje progresivo en lugar de enviar artículos aislados desconectados.
- Rastree la participación en el contenido en el nivel de tema para refinar los modelos de personalización e identificar áreas de interés emergentes en la base de clientes.
- Garantizar que el contenido educativo se distinga claramente del marketing de productos para mantener el cumplimiento de la normativa y preservar la confianza del cliente en la objetividad del programa.


## Guía del producto financiero de AI

Las organizaciones de servicios financieros ofrecen carteras de productos (cuentas de cheques y ahorros, tarjetas de crédito, productos de préstamo, opciones de seguros y vehículos de inversión) que son difíciles de manejar para los clientes sin una guía personalizada. Las restricciones regulatorias impiden que las experiencias digitales de primera línea proporcionen recomendaciones de inversión a medida, pero existe un valor sustancial para ayudar a los clientes a comprender cómo funcionan los productos, qué cuentas se adaptan a sus necesidades declaradas y cómo dar el siguiente paso hacia la aplicación. Una guía de productos financieros de IA involucra a los clientes en una conversación natural, hace preguntas de calificación sobre los objetivos financieros y la etapa de la vida, y los guía hacia los productos adecuados, sin cruzar al territorio de asesoramiento regulado.

### Impacto empresarial

El descubrimiento conversacional guiado mejora las tasas de inicio de aplicaciones de productos y reduce la caída entre la conciencia y la aplicación, al tiempo que captura señales de intención que mejoran los flujos de trabajo de referencia de consejeros y nutrición descendente.

### Cómo implementar

Usar el patrón [Experiencia de conversación en Brand Concierge](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md). Este método implementa Product Advisor Agent con la biblioteca de contenido de producto y la base de conocimiento aprobadas, utilizando AEP Agent Orchestrator y datos de perfil del cliente en tiempo real para guiar a los clientes hacia productos adecuados a través de un diálogo de varias vueltas basado en contenido controlado por la marca y revisado por la conformidad. Este es el patrón correcto cuando el objetivo es el descubrimiento conversacional interactivo con varias vueltas para ayudar a los clientes a comprender y seleccionar productos financieros, distinto de la mensajería activada por eventos, que es unidireccional y responde a eventos de cuentas discretas, y de las experiencias web personalizadas, que muestran el contenido de los productos de forma pasiva sin involucrar a los clientes en un diálogo calificado. Requiere la configuración de AEP Agent Orchestrator y gobernanza de marca.

### Consideraciones técnicas

- Las protecciones de gobernanza de marca deben configurarse con cumplimiento y revisión legal para definir límites de contenido estrictos: el agente debe guiar a los clientes hacia productos adecuados basados en necesidades declaradas sin constituir asesoramiento de inversión, y los temas prohibidos (proyecciones de retorno específicas, garantías, afirmaciones de rendimiento comparativo) deben definirse explícitamente y aplicarse.
- La capa de integración de contenido debe basarse en descripciones de productos, divulgaciones y preguntas frecuentes aprobadas por el cumplimiento, en lugar de reclamaciones generadas dinámicamente, lo que garantiza que cada respuesta que proporcione el agente haya sido revisada por equipos legales y reguladores antes de la implementación.
- La búsqueda de perfiles de clientes en tiempo real debe mostrar datos de relación (productos existentes retenidos, tenencia de cuenta y segmento de clientes) para que el agente pueda evitar recomendar productos que el cliente ya tiene y pueda adaptar la guía a la relación existente del cliente con la institución.
- El traspaso de agentes activos debe configurarse para situaciones en las que las necesidades del cliente exceden el ámbito de la guía conversacional, como situaciones complejas de préstamo o solicitudes de planificación financiera personalizada, con un contexto de conversación completo transferido al asesor receptor para evitar que el cliente se repita.


## Funnel y Análisis de controladores de pérdida

Analice dónde caen los clientes durante la apertura de cuentas digitales, la solicitud de préstamos o los flujos de incorporación de inversión, e identifique las señales de comportamiento que preceden a la desgaste del producto. Las instituciones financieras que no pueden ver estos puntos de entrega o precursores de pérdida son incapaces de distinguir entre fallas en la experiencia de los productos y descalificación, haciendo que los esfuerzos de remediación sean imprecisos.

### Impacto empresarial

Comprender exactamente dónde abandonan los solicitantes los flujos digitales y qué comportamientos preceden al cierre de cuentas permite a los equipos de producto y marketing priorizar las mejoras de experiencia que reducen el abandono y amplían la tenencia de los clientes.

### Cómo implementar

Usar el patrón [Customer Analytics y Insight Generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Este método conecta los datos de comportamiento digital, los registros CRM y los flujos de eventos de producto con Customer Journey Analytics, donde las visualizaciones de visitas en el orden previsto identifican pasos de entrega y el análisis de cohorte muestra diferencias de retención entre líneas de productos y segmentos de adquisición. Este es el patrón correcto cuando el objetivo es comprender y diagnosticar (analizar dónde se desglosan los recorridos y qué provoca el desgaste), en lugar de activar una audiencia de supresión o activar un mensaje de retención.

### Consideraciones técnicas

- Los datos de evento de la aplicación digital deben capturar cada paso del flujo de incorporación o aplicación como eventos discretos con identificadores de paso coherentes para que el análisis de visitas en el orden previsto de CJA pueda aislar exactamente dónde se pierde el volumen.
- Los datos de estado de cuenta y tenencia del producto CRM deben unirse en la conexión de CJA junto con los datos de comportamiento para que el análisis de pérdida pueda correlacionar los comportamientos previos a la desgaste con los resultados reales de cierre de cuenta.
- Las etiquetas de gobernanza de datos deben aplicarse a cualquier campo financiero o de identidad confidencial incluido en la conexión de CJA para evitar la exposición de PII en paneles compartidos a los que acceden los analistas sin permisos de administrador de datos.
- El análisis de cohorte de retención requiere una profundidad de datos histórica suficiente (por lo general de 12 a 24 meses), por lo que las políticas de retención de conjuntos de datos en AEP deben configurarse para conservar el historial de eventos necesario para realizar comparaciones de cohortes significativas.

## Próxima mejor Offer Decisioning

Utilice la lógica de decisión centralizada para seleccionar la oferta más relevante para cada cliente en todos los canales, combinando reglas de elegibilidad, restricciones comerciales y estrategias de clasificación impulsadas por IA. La centralización de la selección de ofertas garantiza que cada cliente reciba la oferta de productos financieros más adecuada según el contexto, respetando al mismo tiempo los requisitos de elegibilidad reglamentarios y las restricciones comerciales.

### Impacto empresarial

Las organizaciones de servicios financieros que utilizan la toma de decisiones de oferta de siguiente mejor centralizado ven tasas de absorción de productos mejoradas y mayores ingresos por interacción de clientes, con el mayor rendimiento cuando la selección de ofertas tiene en cuenta tanto las puntuaciones de tendencia como las barreras de elegibilidad.

### Cómo implementar

Utilice el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) para generar un motor de decisión centralizado que evalúe la elegibilidad del cliente, aplique restricciones comerciales y utilice la clasificación de IA para seleccionar la oferta óptima para cada interacción de cliente en canales web, aplicación y salientes. Este es el patrón correcto cuando la selección de ofertas es demasiado compleja para la personalización basada en reglas por sí sola; para ello, se requiere una combinación de lógica de idoneidad, reglas de prioridad y clasificación adaptable para realizar la selección óptima entre un catálogo de ofertas.

### Consideraciones técnicas

- Las reglas de aceptación de ofertas deben mantenerse en el motor de toma de decisiones y sincronizarse con los criterios de idoneidad de los productos de los sistemas principales de banca o productos para evitar que aparezcan ofertas no aptas.
- Los modelos de clasificación de IA requieren datos de formación suficientes de interacciones de ofertas anteriores para generar puntuaciones de tendencia fiables; los productos recién lanzados necesitan estrategias de clasificación de reserva hasta que se acumulen suficientes datos.
- Los requisitos regulatorios en los servicios financieros pueden restringir lo que se puede ofrecer a quién y a través de qué canal; la lógica de toma de decisiones debe codificar estas restricciones como reglas duras en lugar de preferencias blandas.
- El seguimiento de la fatiga de las ofertas es importante: los clientes que reciben repetidamente ofertas para el mismo producto que no han aceptado deben tener esa oferta despriorizada o suprimida después de un número definido de exposiciones.


## Panel de Customer Journey Analytics

Cree espacios de trabajo de análisis en canales múltiples que combinen datos de la web, la aplicación, el correo electrónico y el centro de llamadas para visualizar los recorridos de los clientes, identificar puntos de entrega y medir la atribución de campañas. Un espacio de trabajo de análisis unificado proporciona a los equipos de producto y marketing una vista completa de cómo se mueven los clientes entre canales y puntos de contacto, lo que permite tomar decisiones basadas en datos sobre dónde invertir para mejorar los recorridos.

### Impacto empresarial

Las organizaciones de servicios financieros con análisis de recorrido en canales múltiples reducen el tiempo de espera de insight para los equipos de campañas y productos, lo que permite identificar más rápidamente las oportunidades de optimización de alto impacto en los flujos de incorporación, los canales de aplicaciones y los recorridos de servicio al cliente.

### Cómo implementar

Utilice el patrón [Customer Analytics &amp; Insight Generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md) para unir flujos de eventos de todos los canales digitales y sin conexión en un conjunto de datos de análisis unificado y, a continuación, generar visualizaciones de espacio de trabajo que exponen flujos de recorrido, listas desplegables de funnel y modelos de atribución. Este es el patrón correcto cuando el requisito principal es la insight analítica y la visualización en lugar de la activación en tiempo real: los datos se utilizan para informar las decisiones en lugar de las acciones del déclencheur de cara al cliente.

### Consideraciones técnicas

- La vinculación de datos entre canales requiere un identificador de cliente coherente en todos los sistemas de origen; las organizaciones con estrategias de identidad fragmentadas verán recorridos incompletos que socavan el análisis.
- Los datos de interacción del centro de llamadas y sin conexión deben ingerirse y marcarse con precisión para colocarlos correctamente en la secuencia de recorrido en relación con los puntos de contacto digitales.
- La latencia de datos entre los sistemas de origen y el espacio de trabajo de analytics afecta a la rapidez con la que están disponibles las perspectivas; los casos de uso de análisis de alta frecuencia pueden requerir una ingesta casi en tiempo real en lugar de fuentes por lotes diarias.
- Los controles de privacidad y control de datos deben aplicarse a los conjuntos de datos de Analytics para evitar que la información de identificación personal aparezca en paneles accesibles para analistas que no deberían tener acceso a registros de clientes individuales.
