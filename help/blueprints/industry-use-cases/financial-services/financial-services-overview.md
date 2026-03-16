---
title: Casos prácticos de servicios financieros
description: Descubra cómo las organizaciones de servicios financieros utilizan Adobe Experience Platform para personalizar ofertas de productos, evitar la pérdida y profundizar las relaciones con los clientes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 1%

---


# Casos prácticos de servicios financieros

Las organizaciones de servicios financieros dependen de Adobe Experience Platform para unificar los datos de los clientes en los canales bancario, de préstamo y de inversión, lo que permite experiencias personalizadas que fortalecen las relaciones e impulsan el crecimiento. Al reunir la actividad de la cuenta, el historial de transacciones y las señales de comportamiento, estas organizaciones pueden ofrecer la oferta correcta en el momento adecuado y, al mismo tiempo, mantener la confianza y el cumplimiento que esperan sus clientes.

## Nutrición de plomo de alto valor

Identifique los posibles clientes de alto valor en función de los datos y el comportamiento del perfil y, a continuación, nutra a los mismos con contenido y ofertas personalizados mediante recorridos automatizados. Al combinar los detalles demográficos, la actividad de navegación y las señales de participación, las instituciones financieras pueden priorizar a los posibles clientes más propensos a convertirlos y guiarlos a través de un camino adaptado para convertirse en clientes.

### Impacto empresarial

Las organizaciones que implementan la nutrición de clientes potenciales de alto valor generalmente ven un aumento del 25 al 35% en las tasas de conversión de clientes potenciales mientras construyen un canal de ventas más saludable y predecible.

### Cómo implementar

Utilice el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para crear secuencias de nutrición automatizadas que se adapten según las señales de participación y preparación del posible cliente.

### Consideraciones técnicas

- Integre datos de puntuación de posibles clientes CRM y eventos de comportamiento del sitio web en perfiles de clientes potenciales unificados para potenciar la lógica de entrada y ramificación del recorrido.
- Asegúrese de que las preferencias de consentimiento y de inclusión se apliquen en cada punto de contacto, especialmente en el caso de la divulgación por teléfono y correo electrónico regida por las regulaciones de marketing financiero.
- Configure la restricción de recorrido para evitar perspectivas abrumadoras con varias comunicaciones durante períodos cortos de evaluación.
- Tenga en cuenta la latencia de datos entre las interacciones de sucursales o asesores y la participación digital para mantener relevante la mensajería nutritiva.


## Recomendación de productos para clientes existentes

Recomendar productos financieros relevantes, como tarjetas de crédito, préstamos y productos de inversión, a clientes existentes en función de su perfil, historial de transacciones y fase de vida. Este caso de uso convierte los datos de cuenta diarios en perspectivas procesables que muestran el siguiente mejor producto para cada cliente.

### Impacto empresarial

Las recomendaciones personalizadas de productos impulsan un aumento de entre el 20 y el 30 % en las tasas de adopción de productos y aumentan de forma mensurable el valor de duración del cliente al aumentar el uso compartido de carteras.

### Cómo implementar

Use el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) para evaluar a cada cliente con respecto a ofertas de productos elegibles en tiempo real, clasificando las recomendaciones por relevancia y prioridad comercial.

### Consideraciones técnicas

- Unificar los datos de transacción, los saldos de cuenta y las tenencias de productos en un único perfil de cliente para que los modelos de toma de decisiones tengan una visión completa de las relaciones existentes.
- Aplique reglas de idoneidad financiera y restricciones de elegibilidad regulatorias como barreras duras dentro del motor de decisión antes de clasificar las ofertas.
- Coordine la entrega de ofertas en los canales de banca en línea, aplicación móvil, correo electrónico y asesor para evitar recomendaciones conflictivas o duplicadas.
- Implemente límites de frecuencia por categoría de producto para evitar la fatiga de las recomendaciones, especialmente para productos de alta consideración como hipotecas y cuentas de inversión.


## Campañas de prevención de pérdida

Identifique a los clientes en riesgo de pérdida mediante el uso de la predicción de pérdida con tecnología de IA e inclúyalos en ofertas de retención y comunicaciones personalizadas. La detección temprana de señales de desconexión permite que las instituciones financieras intervengan antes de que un cliente cierre cuentas o mueva activos a otro lugar.

### Impacto empresarial

Los esfuerzos proactivos de prevención de pérdida suelen reducir la desgaste del cliente en un 15-25%, lo que protege los flujos de ingresos recurrentes y reduce el coste de la sustitución del cliente.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para almacenar en déclencheur los recorridos de retención cuando las puntuaciones de riesgo de pérdida excedan los umbrales definidos, con toma de decisiones integrada para seleccionar la oferta de retención más atractiva.

### Consideraciones técnicas

- Tendencias de actividad de cuenta de fuente, historial de interacción de servicio y frecuencia de participación en [!DNL Customer AI] modelos de tendencia a la pérdida para generar puntuaciones de riesgo.
- Defina umbrales de riesgo de pérdida específicos para las líneas de producto, ya que las señales de desconexión para las cuentas de cheques difieren de las de las carteras de inversión.
- Garantizar que las ofertas de retención cumplan con las regulaciones de préstamo justo e igualdad de trato para que los segmentos de alto riesgo reciban un trato equitativo.
- Genere una lógica de supresión para excluir a los clientes que se producen debido a acciones de fraude o cumplimiento, donde el alcance de la retención sería inapropiado.


## Tablero de cuenta personalizado

Personalice el tablero de banca en línea y la experiencia de la aplicación móvil en función de la actividad de la cuenta, las preferencias y los objetivos financieros de cada cliente. Un tablero personalizado ayuda a los clientes a encontrar lo que más importa y muestra perspectivas relevantes sin que tengan que buscar.

### Impacto empresarial

Los paneles personalizados aumentan las tasas de participación en un 30-40 % y mejoran significativamente las puntuaciones de satisfacción del cliente al hacer que la banca digital se sienta intuitiva y relevante.

### Cómo implementar

Use el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones y web de visitantes conocidos para ofrecer bloques de contenido personalizado en tiempo real, detalles de productos y perspectivas financieras dentro de experiencias digitales autenticadas.

### Consideraciones técnicas

- Aproveche [!DNL Edge Network] para decisiones de personalización por debajo del segundo en sesiones bancarias autenticadas en las que la latencia afecte directamente a la experiencia del usuario.
- Agregue datos de transacciones en atributos de perfil precalculados, como categorías de gasto y tendencias de ahorro, para evitar el cálculo en tiempo real de grandes conjuntos de datos.
- Cumplan con los estándares de accesibilidad y garanticen que el contenido personalizado cumpla los mismos requisitos regulatorios de divulgación que el contenido estático.
- Coordine la lógica de personalización entre los canales web y móvil para que los clientes vean una experiencia coherente independientemente del dispositivo.


## Ofertas de productos por fases de Life

Identifique a los clientes que entran en nuevas etapas de vida, como el matrimonio, la compra de una vivienda o la jubilación, y ofrezca de forma proactiva productos y servicios financieros relevantes. Anticipar estos hitos permite a las instituciones posicionarse como socios de confianza durante momentos financieros cruciales.

### Impacto empresarial

Las ofertas activadas por etapas de vida logran una tasa de adopción de productos del 35-45%, superando significativamente a las campañas genéricas, a la vez que fortalecen las relaciones con los clientes a largo plazo.

### Cómo implementar

Utilice el patrón [Cross-Channel Recorrido with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para detectar indicadores de etapa de vida y orquestar recorridos multitáctiles con selección de ofertas incrustadas adaptadas a cada hito.

### Consideraciones técnicas

- Combine señales de origen, como cambios de dirección, aperturas de cuentas conjuntas y grandes depósitos, con datos de terceros autorizados para deducir transiciones de fase de vida.
- Gestione los eventos personales confidenciales con cuidado en el tono y la frecuencia de la mensajería, ya que los hitos inferidos incorrectamente pueden erosionar la confianza.
- Capar las comprobaciones de idoneidad regulatoria en Offer Decisioning para que los productos recomendados se alineen con la situación financiera verificada del cliente.
- Cree periodos de enfriamiento entre las campañas de fase de vida para evitar la superposición de alcance cuando varios indicadores se activen en una ventana corta.


## Alertas y recomendaciones basadas en transacciones

Envíe alertas en tiempo real de transacciones y proporcione recomendaciones personalizadas basadas en patrones de gasto y actividad de cuenta. Las notificaciones oportunas y relevantes mantienen informados a los clientes y crean momentos naturales para que aparezcan directrices financieras útiles.

### Impacto empresarial

Las alertas basadas en transacciones logran una tasa de participación del 50 al 60 %, lo que mejora considerablemente la concienciación sobre la seguridad y crea puntos de contacto de alto valor para recomendaciones personalizadas.

### Cómo implementar

Use el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para responder a eventos de transacción en tiempo real con alertas y recomendaciones relevantes para el contexto.

### Consideraciones técnicas

- Ingeste eventos de transacción a través de una canalización de flujo continuo con requisitos de entrega de baja latencia, ya que las alertas de seguridad pierden valor si se retrasan más de unos minutos.
- Aplique las preferencias y umbrales de alerta definidos por el cliente para que las notificaciones reflejen la configuración individual en lugar de las reglas únicas para todos los casos.
- Separe las alertas de seguridad obligatorias de los mensajes de recomendación opcionales en la arquitectura de mensajería para garantizar que las notificaciones de conformidad nunca se supriman.
- Tenga en cuenta los altos volúmenes de transacciones durante los períodos de mayor actividad, como los días de pago y los festivos, diseñando una capacidad de rendimiento que se escale según la demanda.


## Recuperación de abandono de solicitud de tarjeta de crédito

Identifique a los clientes que iniciaron las solicitudes de tarjeta de crédito, pero no las completaron, y vuelva a interactuar con ellos con mensajes y ofertas personalizados. El abandono de aplicaciones representa una audiencia con muchas intenciones que a menudo solo necesita un pequeño empujón para completar el proceso.

### Impacto empresarial

Las campañas de recuperación de abandonos mejoran las tasas de finalización de las aplicaciones en un 20-30 %, lo que aumenta directamente la adquisición de nuevas cuentas de una audiencia que ya ha expresado interés.

### Cómo implementar

Utilice el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para detectar eventos de abandono de aplicaciones y mensajes de seguimiento oportunos de déclencheur que aborden motivos comunes de abandono.

### Consideraciones técnicas

- Capture el paso específico en el que se abandonó la aplicación para adaptar la mensajería, ya que alguien que abandonó en la verificación de identidad necesita una tranquilidad diferente a alguien que abandonó en la revisión de términos.
- Cumplir con las regulaciones de marketing crediticio, incluidas las divulgaciones requeridas y las reglas de préstamo justo en todas las comunicaciones de recuperación.
- Implemente una lógica de decadencia de tiempo para que el alcance de la recuperación se detenga después de una ventana definida, ya que los datos de aplicaciones antiguas pueden dejar de ser válidos para la precalificación.
- Coordínese con el sistema de solicitud para suprimir los mensajes de recuperación para los solicitantes que completaron a través de un canal diferente, como una visita a una sucursal o una llamada telefónica.


## Recomendaciones de Portfolio de inversión

Proporcione recomendaciones de inversión personalizadas en función del perfil de riesgo, el historial de inversión y los objetivos financieros de cada cliente. La orientación de portafolios basada en datos ayuda a los clientes a tomar decisiones informadas a la vez que profundizan su participación en los servicios de gestión de patrimonios.

### Impacto empresarial

Las recomendaciones de inversión personalizadas impulsan un aumento del 25 al 35% en la adopción de productos de inversión y mejoran la diversificación de la cartera en toda la base de clientes.

### Cómo implementar

Use el patrón [Recomendación de comportamiento](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) para analizar el comportamiento y las preferencias de la inversión y, a continuación, mostrar recomendaciones de portafolio relevantes a través de canales digitales y herramientas de asesoramiento.

### Consideraciones técnicas

- Integre fuentes de datos de corretaje y custodia para mantener una vista precisa y actualizada de las tenencias y asignaciones actuales de cada cliente.
- Haga cumplir los requisitos de idoneidad exigidos por las regulaciones de valores para que las recomendaciones se ajusten a la tolerancia al riesgo y los objetivos de inversión documentados del cliente.
- Etiquete claramente el contenido de inversión personalizado como educativo o informativo cuando sea necesario, distinguiéndolo del asesoramiento de inversión formal que conlleva obligaciones fiduciarias.
- Actualice los modelos de recomendación en una cadencia regular para tener en cuenta los cambios de mercado, la deriva de la cartera y los cambios en los objetivos de los clientes.


## Alerta de fraude Personalization

Personalice las alertas de fraude y las comunicaciones de seguridad en función de las preferencias de comunicación de cada cliente y del historial de interacción anterior. Las alertas personalizadas aumentan la probabilidad de que los clientes detecten y comprendan las notificaciones de seguridad críticas y actúen en consecuencia.

### Impacto empresarial

Las alertas de fraude personalizadas mejoran las tasas de respuesta de alerta en un 40-50%, lo que fortalece significativamente el cumplimiento de la seguridad y reduce la ventana de exposición durante actividades sospechosas.

### Cómo implementar

Utilice el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para entregar alertas de fraude a través del canal preferido de cada cliente con detalles contextuales que faciliten la confirmación o la disputa de la actividad.

### Consideraciones técnicas

- Priorice la velocidad y fiabilidad de entrega por encima de todas las demás consideraciones de diseño, ya que la latencia de las alertas de fraude se correlaciona directamente con la exposición a pérdidas financieras.
- Enrute las alertas a través del canal preferido verificado del cliente mientras mantiene los canales de reserva para garantizar la entrega incluso si falla el canal principal.
- Historial de interacción de alertas de tienda para mejorar la relevancia de alertas futuras y reducir la fatiga por falsos positivos para los clientes que viajan con frecuencia o realizan compras atípicas.
- Asegúrese de que todo el contenido y los flujos de trabajo de alertas de fraude cumplan con las normas de seguridad bancaria y no expongan los detalles confidenciales de la cuenta en las vistas previas de los mensajes o las líneas de asunto.


## Participación del programa de fidelización

Personalice las comunicaciones, las recompensas y las ofertas del programa de fidelidad en función del nivel, el saldo de puntos y el historial de canje de cada cliente. Las comunicaciones de lealtad relevantes y oportunas mantienen el compromiso de los miembros e impulsan una mayor participación en el programa.

### Impacto empresarial

La participación de lealtad personalizada aumenta la participación en el programa en un 30-40% e impulsa una canje de puntos mediblemente más alta, lo que fortalece la percepción de valor del programa.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para orquestar las comunicaciones de fidelidad entre canales, con toma de decisiones incrustada para seleccionar la recompensa u oferta más relevante para cada miembro.

### Consideraciones técnicas

- Sincronice los datos de la plataforma de fidelización, incluido el estado del nivel, los saldos de puntos y el historial de canje, en los perfiles de los clientes en tiempo casi real para evitar promocionar los saldos caducados o inexactos.
- Segmente la lógica de recorrido por nivel para ofrecer experiencias diferenciadas, ya que los miembros de alto nivel esperan un tratamiento exclusivo y un acceso anticipado a las promociones.
- Coordine la mensajería de fidelidad con campañas de marketing más amplias para evitar que los mensajes se agoten y las ofertas conflictivas entre programas.
- Realice un seguimiento de la atribución de canje en todos los canales para medir qué comunicaciones personalizadas generan el mayor retorno de la inversión en el programa.


## Campañas de preaprobación de hipotecas

Clientes objetivo que es probable que estén en el mercado de una hipoteca en función de datos de perfil, señales de comportamiento e indicadores de fase de vida. El alcance proactivo previo a la aprobación posiciona a la institución como una primera opción conveniente durante una de las mayores decisiones financieras que un cliente tomará.

### Impacto empresarial

Las campañas de preaprobación de hipotecas objetivo aumentan las tasas de solicitud en un 20-30% y mejoran el volumen de originación de préstamos al alcanzar perspectivas calificadas en el momento adecuado.

### Cómo implementar

Use el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para guiar a los posibles clientes hipotecarios a través de una secuencia de nutrición multitáctil, desde la concienciación hasta la aprobación previa, adaptándose en función de las señales de participación y calificación.

### Consideraciones técnicas

- Combine el comportamiento de búsqueda de propiedades, las tendencias de crecimiento de ahorros y las señales de caducidad de arrendamientos para construir un modelo de tendencia que identifique a los probables solicitantes de hipotecas.
- Asegúrese de que todos los mensajes de preaprobación cumplan con las regulaciones de publicidad hipotecaria, incluidas las divulgaciones requeridas, la precisión de la tasa y el lenguaje de vivienda equitativo.
- Coordine el tiempo de la campaña con los cambios del entorno de tasas para que el alcance se ajuste a las condiciones de endeudamiento favorables y evite referencias de tasas obsoletas.
- Cree flujos de trabajo de transferencia a los responsables de préstamos para que los posibles clientes alimentados digitalmente realicen la transición sin problemas al proceso formal de solicitud y suscripción.


## Contenido personalizado de educación financiera

Ofrezca contenido, sugerencias y recursos personalizados de educación financiera en función del perfil financiero, los objetivos y los intereses de cada cliente. El contenido educativo relevante genera confianza, mejora la alfabetización financiera y crea oportunidades orgánicas para introducir productos relevantes.

### Impacto empresarial

El contenido educativo personalizado aumenta las tasas de participación en el contenido en un 25-35 % y mejora la alfabetización financiera de los clientes, lo que a su vez aumenta la confianza en la adopción de productos.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para ofrecer una secuencia revisada de contenido educativo en canales múltiples, usando la toma de decisiones para relacionar los temas con la situación financiera y los intereses de cada cliente.

### Consideraciones técnicas

- Asigne contenido educativo a atributos de perfil financiero como la relación deuda-ingresos, la tasa de ahorro y la experiencia de inversión para garantizar la relevancia del tema.
- Etiquete contenido con niveles de dificultad y temas de requisitos previos para crear rutas de aprendizaje progresivo en lugar de enviar artículos aislados desconectados.
- Rastree la participación en el contenido en el nivel de tema para refinar los modelos de personalización e identificar áreas de interés emergentes en la base de clientes.
- Garantizar que el contenido educativo se distinga claramente del marketing de productos para mantener el cumplimiento de la normativa y preservar la confianza del cliente en la objetividad del programa.
