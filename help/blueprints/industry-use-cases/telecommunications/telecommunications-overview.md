---
title: Casos de uso de telecomunicaciones
description: Descubra cómo las organizaciones de telecomunicaciones utilizan Adobe Experience Platform para reducir la pérdida, impulsar las actualizaciones de los dispositivos y mejorar la participación de los clientes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 653632f0-81be-435c-a703-56c5bc132794
source-git-commit: 0236bd326730ee9a0be621ee0e60ddc3d352410d
workflow-type: tm+mt
source-wordcount: '3822'
ht-degree: 0%

---

# Casos de uso de telecomunicaciones

Las organizaciones de telecomunicaciones utilizan Adobe Experience Platform para crear una vista unificada de cada suscriptor y ofrecer experiencias personalizadas que reduzcan la pérdida, aumenten las actualizaciones de los planes y los dispositivos y refuercen las relaciones con los clientes a largo plazo. Al conectar los datos de uso de la red, la información de facturación y las interacciones con los clientes, los proveedores de telecomunicaciones pueden anticipar las necesidades de los suscriptores y comprometerlos en el momento adecuado a través de sus canales preferidos.

## Recomendaciones de actualización de dispositivos

Identifique a los clientes aptos para las actualizaciones de dispositivos y presente recomendaciones y ofertas de actualización de dispositivos personalizadas en función de los patrones de uso y las preferencias. Al analizar los plazos contractuales, la edad de los dispositivos y el comportamiento de navegación individual, los proveedores de telecomunicaciones pueden mostrar los dispositivos y las opciones de financiación más relevantes a cada suscriptor.

### Impacto empresarial

Las organizaciones que implementan recomendaciones de actualización de dispositivos ven tasas de conversión de actualización mejoradas al ofrecer la oferta correcta en el momento adecuado a través del canal preferido del cliente.

### Cómo implementar

Use el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para organizar recorridos de actualización que evalúen la elegibilidad, las preferencias del dispositivo y la afinidad del canal de cada suscriptor y así ofrecer ofertas de actualización personalizadas por correo electrónico, notificaciones de aplicaciones y experiencias en la tienda. Este es el patrón correcto cuando la selección de ofertas debe tener en cuenta las ventanas de idoneidad del dispositivo, las preferencias de canal y las restricciones de inventario: restricciones que requieren una lógica de toma de decisiones controlada en lugar de simples recomendaciones de comportamiento por sí solas.

### Consideraciones técnicas

- Integre el inventario de dispositivos y los sistemas de precios para garantizar que las recomendaciones reflejen la disponibilidad actual y los precios promocionales.
- Conecte los datos de administración de contratos para identificar con precisión las ventanas de idoneidad para la actualización y las ofertas de actualización anticipada.
- Incorporar telemetría de uso del dispositivo (capacidad de almacenamiento, estado de la batería, métricas de rendimiento) para reforzar la relevancia de la recomendación.
- Coordínese con las plataformas de comercio minorista y electrónico para mantener una experiencia de actualización coherente en los canales digitales y en las tiendas.


## Planificar campañas de optimización

Analice los patrones de uso de los clientes y recomiende cambios de plan óptimos para ahorrar dinero u obtener mejores funciones según sus necesidades reales. Ponerse en contacto proactivamente con las recomendaciones del plan crea confianza y reduce el riesgo de que los suscriptores se vayan a la competencia con precios más sencillos.

### Impacto empresarial

Las campañas de optimización del plan mejoran las tasas de cambio del plan, mejoran la satisfacción del cliente y, al mismo tiempo, aumentan los ingresos promedio por usuario cuando los suscriptores se mudan a planes que mejor se ajustan a su consumo.

### Cómo implementar

Use el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para crear una campaña multitáctil que identifique las discrepancias de uso a plan, eduque a los suscriptores sobre mejores opciones y los guíe a través del proceso de cambio de plan con seguimientos oportunos. Este es el patrón correcto cuando el caso de uso requiere un flujo secuenciado de varios mensajes a lo largo de los días con ramas condicionales basadas en la participación del suscriptor y la adopción del plan: un solo mensaje activado no puede adaptarse al recorrido educativo y a la lógica de dependencia entre los pasos de educación y conversión.

### Consideraciones técnicas

- Ingeste datos de uso en tiempo real e históricos (minutos de voz, consumo de datos, llamadas internacionales) para identificar las discrepancias del plan con precisión.
- Conecte los datos del sistema de facturación para calcular los ahorros potenciales o las ganancias de las funciones para cada cambio de plan recomendado.
- Tenga en cuenta las reglas de precios promocionales y las obligaciones contractuales al generar recomendaciones de plan.
- Integre con portales de autoservicio para que los suscriptores puedan completar los cambios del plan directamente desde los puntos de contacto de la campaña.


## Prevención de pérdida para clientes de alto valor

Identifique a los clientes de alto valor que corren el riesgo de sufrir una pérdida de tiempo y actívelos con ofertas de retención personalizadas y un servicio de atención al cliente proactivo. Al combinar señales de comportamiento como una disminución del uso, llamadas de servicio repetidas y una navegación competitiva con datos de valor de duración, los proveedores pueden intervenir antes de que un suscriptor decida irse.

### Impacto empresarial

Los programas de prevención de pérdida dirigidos a suscriptores de alto valor logran reducciones significativas en la pérdida, protegiendo ingresos recurrentes significativos y reduciendo el coste de adquisición de clientes de reemplazo.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para monitorizar las señales de riesgo de pérdida en tiempo real, determinar la mejor oferta de retención para cada suscriptor y organizar una comunicación personalizada entre canales digitales y el centro de llamadas. Este es el patrón correcto cuando el recorrido debe coordinar la entrega a través de canales digitales y asistidos por agentes para evitar ofertas de retención duplicadas y cuando la selección de ofertas requiere puntuación de riesgo y restricciones empresariales: la orquestación de varios pasos por sí sola no proporciona la capa de toma de decisiones en tiempo real ni la coordinación de agentes necesaria.

### Consideraciones técnicas

- Genere puntuaciones de tendencia a la pérdida combinando las tendencias de uso, el historial de interacciones del servicio y los datos de opinión de las transcripciones del centro de llamadas.
- Integre los sistemas de centros de llamadas y comercios minoristas para que los agentes tengan visibilidad de las ofertas de retención ya presentadas a través de canales digitales.
- Conecte datos de inteligencia competitiva (solicitudes de exclusión, comparaciones de planes de competidores) para refinar la puntuación de riesgo y las estrategias de oferta.
- Establezca reglas de gobernanza para evitar ponerse en contacto de forma excesiva con suscriptores en riesgo, lo que puede acelerar la pérdida en lugar de evitarla.


## Nuevo Recorrido de incorporación del cliente

Automatice un recorrido de incorporación personalizado para nuevos clientes con información de bienvenida, directrices de configuración de cuentas y tutoriales de funciones. Una experiencia de incorporación estructurada ayuda a los suscriptores a descubrir rápidamente todo el valor de su plan y servicios, sentando las bases para una retención a largo plazo.

### Impacto empresarial

Los recorridos de incorporación bien diseñados mejoran las tasas de activación de funciones, lo que conduce a puntuaciones de satisfacción más altas y a una menor pérdida de la vida útil temprana entre los nuevos suscriptores.

### Cómo implementar

Utilice el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para crear una experiencia de incorporación secuenciada que se adapte según el tipo de plan, el dispositivo y la participación de cada suscriptor con los pasos de incorporación anteriores. Este es el patrón correcto cuando el caso de uso requiere un flujo secuenciado de varios mensajes a lo largo de días con ramificación condicional basada en la detección de funciones y la participación: un solo mensaje activado no puede admitir la lógica de dependencia adaptable entre los pasos de incorporación basados en el plan del suscriptor y el tipo de dispositivo.

### Consideraciones técnicas

- Integre sistemas de aprovisionamiento de cuentas para almacenar en déclencheur el recorrido de incorporación inmediatamente después de la activación y adapte el contenido al plan y el dispositivo específicos del suscriptor.
- Conecte los datos de participación de la aplicación para rastrear qué funciones ha explorado el suscriptor y ajustar los mensajes de incorporación subsiguientes en consecuencia.
- Coordine esta acción con la plataforma de asistencia al cliente para asegurarse de que los agentes conozcan la fase de incorporación de un suscriptor si llaman con preguntas.
- Admitir varias rutas de incorporación para diferentes segmentos de clientes, como suscriptores individuales, administradores de planes familiares y cuentas empresariales.


## Alertas y recomendaciones de uso de datos

Envíe alertas personalizadas cuando los clientes se aproximen a los límites de datos y recomienden actualizaciones de planes o complementos de datos basados en patrones de uso. Las notificaciones oportunas y útiles transforman una experiencia potencialmente frustrante en un momento de participación en el desarrollo de la confianza.

### Impacto empresarial

Las alertas proactivas de uso de datos impulsan compras de complementos de datos mejorados, a la vez que reducen las quejas por shock en las facturas y mejoran la satisfacción general del cliente.

### Cómo implementar

Use el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para enviar alertas en tiempo real cuando se superen los umbrales de uso, con recomendaciones personalizadas basadas en los patrones de consumo históricos y los detalles del plan del suscriptor. Este es el patrón correcto cuando el déclencheur es un evento del sistema (cruce del umbral de uso) en lugar de una conducta del cliente, y la comunicación necesaria es inmediata y reactiva en lugar de una secuencia de nutrición sostenida.

### Consideraciones técnicas

- Conéctese a fuentes de datos de uso de red que proporcionan actualizaciones de consumo casi en tiempo real para las alertas de déclencheur con umbrales significativos (75 %, 90 % y 100 % de los límites del plan).
- Integre los sistemas de facturación y administración de planes para presentar precios exactos de complementos y permitir compras de un solo toque directamente desde el mensaje de alerta.
- Contabilice los conjuntos de datos compartidos en los planes de la familia alertando tanto al usuario individual como al administrador del plan.
- Implemente un límite de frecuencia para evitar la fatiga de alertas para los suscriptores que utilizan de forma consistente altas cantidades de datos en cada ciclo de facturación.


## Notificaciones de interrupción del servicio

Notificar a los clientes de forma proactiva sobre interrupciones del servicio, mantenimiento o problemas de red en su área con actualizaciones personalizadas y ofertas de compensación. Si se contacta antes de que los clientes experimenten frustración, se demuestra la responsabilidad y se reduce significativamente el volumen de asistencia entrante.

### Impacto empresarial

Las notificaciones de interrupción proactivas logran tasas de confirmación de notificaciones sólidas y reducen sustancialmente el volumen del centro de llamadas durante las interrupciones del servicio, lo que reduce los costes de asistencia y mejora la percepción del cliente.

### Cómo implementar

Use el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para detectar eventos de red y notificar inmediatamente a los suscriptores afectados a través de sus canales preferidos con detalles relevantes, tiempos de resolución estimados y una compensación apropiada cuando esté justificado. Este es el patrón correcto cuando el déclencheur es un evento del sistema (interrupción de la red) en lugar de una conducta del cliente, y la comunicación necesaria es inmediata y reactiva en lugar de una secuencia de nutrición sostenida.

### Consideraciones técnicas

- Integración con los sistemas de supervisión del centro de operaciones de red para recibir datos de eventos de interrupción en tiempo real y mantenimiento con información del ámbito geográfico.
- Utilice los datos de dirección y ubicación del suscriptor para identificar con precisión a los clientes afectados y evitar notificar a los que se encuentran fuera del área afectada.
- Conéctese al sistema de facturación y créditos para automatizar las ofertas de crédito de servicio para interrupciones prolongadas en función del plan del suscriptor y la duración de la interrupción.
- Coordine la mensajería entre canales para proporcionar actualizaciones de estado coherentes y evitar enviar información conflictiva a medida que evoluciona la situación.


## Administración del plan familiar

Personalice las comunicaciones y ofertas para los administradores de planes familiares en función de los patrones de uso familiar y las necesidades individuales de los miembros. Los planes familiares representan cuentas multilínea de alto valor donde la participación con el administrador del plan genera retención en todas las líneas.

### Impacto empresarial

Las comunicaciones personalizadas de administración de planes familiares mejoran la participación en los planes familiares, lo que conduce a una mayor retención de líneas y a un mayor valor de por vida por cuenta.

### Cómo implementar

Use el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para analizar el uso en todos los miembros de la familia, identificar oportunidades como agregar líneas o ajustar límites individuales, y ofrecer recomendaciones personalizadas al administrador del plan. Este es el patrón correcto cuando la selección de ofertas debe tener en cuenta los permisos de la jerarquía familiar, la agregación de uso de varios miembros y las restricciones de privacidad, restricciones que requieren una lógica de toma de decisiones controlada en lugar de recomendaciones de suscriptores individuales por sí solos.

### Consideraciones técnicas

- Jerarquías de cuentas de familia de modelos para distinguir entre el administrador del plan y los miembros individuales, respetando los niveles de permisos para las comunicaciones y los cambios de cuenta.
- Agregue datos de uso en todas las líneas de la cuenta para identificar patrones y oportunidades a nivel familiar, como datos compartidos infrautilizados o ciclos de actualización de dispositivos desiguales.
- Integre el control parental y los sistemas de filtrado de contenido para admitir funciones específicas de la familia en la personalización.
- Asegúrese de que existan controles de privacidad para que los detalles de uso de los miembros individuales se compartan apropiadamente con el administrador del plan en función de los permisos de la cuenta.


## Campañas de actualización 5G

Clientes objetivo elegibles para actualizaciones de red 5G con ofertas y beneficios personalizados en función de su ubicación y patrones de uso. A medida que la cobertura 5G se expande, llegar a los suscriptores en las áreas recién cubiertas con mensajes relevantes acelera la adopción y aumenta la utilización de la red.

### Impacto empresarial

Las campañas de actualización 5G dirigidas impulsan tasas de adopción de 5G mejoradas entre los suscriptores elegibles, lo que respalda los retornos de inversión en red y la diferenciación competitiva.

### Cómo implementar

Utilice el patrón [Activación de mensaje saliente por lotes](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) para segmentar a los suscriptores según la disponibilidad de cobertura 5G, la compatibilidad del dispositivo y la elegibilidad del plan. Luego, ofrezca campañas de actualización personalizadas que resalten los beneficios más relevantes para el perfil de uso de cada suscriptor. Este es el patrón correcto cuando la audiencia está predefinida y es grande, el tiempo de entrega está programado en lugar de depender del evento y no se requiere bifurcación en tiempo real ni toma de decisiones. La campaña se puede planificar completamente por adelantado en función de los plazos de despliegue de la cobertura.

### Consideraciones técnicas

- Integre mapas de cobertura de red para identificar con precisión a los suscriptores en áreas con servicio 5G activo y evitar promocionar actualizaciones donde la cobertura aún no está disponible.
- Conecte los datos de compatibilidad del dispositivo para determinar qué suscriptores necesitan un dispositivo nuevo en comparación con aquellos que ya tienen hardware compatible con 5G.
- Coordínese con los sistemas de inventario minorista para garantizar que los dispositivos y planes promocionados estén disponibles en la tienda preferida del suscriptor o en línea.
- Mensajería de segmentos por perfil de uso para que los usuarios de datos pesados reciban beneficios centrados en el rendimiento mientras que los usuarios ocasionales reciben mensajes de cobertura y fiabilidad.


## Recordatorios de pago de factura

Envíe recordatorios personalizados de pago de factura a través de los canales preferidos con opciones de pago e información de saldo de cuenta. Los recordatorios oportunos y convenientes reducen la demora en los pagos y los costes de cobranza asociados, al tiempo que mantienen una relación positiva con el cliente.

### Impacto empresarial

Los recordatorios personalizados de pago de factura mejoran las tasas de pago a tiempo, reduciendo los gastos de cobro y minimizando las suspensiones de servicio que generan insatisfacción en los clientes.

### Cómo implementar

Usa el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para enviar recordatorios en momentos óptimos antes de la fecha límite, personalizados con el saldo del suscriptor, el método de pago preferido y un enlace directo para completar el pago. Este es el patrón correcto cuando el déclencheur es un evento del sistema basado en el tiempo (fecha de vencimiento de facturación) en lugar de un comportamiento del cliente, y la comunicación necesaria es inmediata y transaccional, en lugar de una secuencia de participación de varios pasos.

### Consideraciones técnicas

- Integre con la plataforma de facturación para acceder a los saldos de cuentas en tiempo real, las fechas de vencimiento y el historial de pagos para obtener un contenido de recordatorio preciso.
- Conéctese a los sistemas de procesamiento de pagos para habilitar el pago mediante un solo toque o un solo clic directamente desde el mensaje recordatorio.
- Implemente una lógica de escalación que ajuste la urgencia y la frecuencia del recordatorio a medida que se acerca la fecha de vencimiento, respetando al mismo tiempo las preferencias de comunicación.
- Admite múltiples métodos de pago (inscripción de pago automático, cartera digital, transferencia bancaria) y personaliza las opciones presentadas en función del historial del suscriptor.


## Recomendaciones del servicio de complementos

Recomendar servicios adicionales relevantes, como seguros de dispositivos, almacenamiento en la nube y paquetes de streaming, en función del plan, el uso y las preferencias del cliente. Las recomendaciones contextuales aumentan el valor que los suscriptores reciben de su relación con el proveedor, a la vez que aumentan los ingresos promedio por usuario.

### Impacto empresarial

Las recomendaciones de servicios de complementos personalizados mejoran las tasas de adopción de complementos, lo que aumenta los ingresos de la base de suscriptores existente sin el coste de la adquisición de nuevos clientes.

### Cómo implementar

Utilice el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) para evaluar el perfil, los servicios actuales y las señales de comportamiento de cada suscriptor con el fin de determinar la oferta de complemento más relevante y presentarla en el canal y el momento óptimos. Este es el patrón correcto cuando la selección de ofertas debe tener en cuenta la propiedad del servicio actual y las reglas comerciales que rigen la elegibilidad del servicio complementario: reglas que requieren una lógica de toma de decisiones regida en lugar de una clasificación de afinidad de comportamiento por sí sola.

### Consideraciones técnicas

- Conéctese al catálogo de servicios actual del suscriptor para evitar recomendar servicios que ya tiene e identificar complementos naturales para su plan existente.
- Integre datos de socios y servicios de terceros (proveedores de streaming, compañías de seguros) para presentar precios precisos y ofertas agrupadas.
- Utilice los datos de uso y del dispositivo para informar las recomendaciones, como sugerir un seguro del dispositivo para los suscriptores con nuevos dispositivos Premium o almacenamiento en la nube para aquellos que se queden sin almacenamiento del dispositivo.
- Coordine la personalización en la aplicación y la web para reforzar las recomendaciones de complementos en los puntos de contacto de autoservicio.


## Personalization de rendimiento de red

Personalice la información y las recomendaciones de rendimiento de red en función de la ubicación, el dispositivo y los patrones de uso del cliente. Ayudar a los suscriptores a optimizar su experiencia de conectividad crea confianza y reduce los contactos de asistencia asociados con problemas de rendimiento.

### Impacto empresarial

Las experiencias de rendimiento de red personalizadas mejoran la participación de la aplicación, a medida que los suscriptores vuelven para comprobar la cobertura, solucionar problemas y descubrir consejos de optimización adaptados a su situación.

### Cómo implementar

Use el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones y web de visitantes conocidos para ofrecer paneles de rendimiento de red personalizados, información de cobertura y recomendaciones de optimización dentro de la experiencia de la cuenta web y la aplicación del suscriptor. Este es el patrón correcto cuando la personalización está impulsada por atributos de perfil y datos de ubicación en lugar de un modelo de afinidad de comportamiento.

### Consideraciones técnicas

- Integre métricas de calidad de red y datos de cobertura para proporcionar información de rendimiento específica de la ubicación relevante para el hogar, el trabajo y las áreas visitadas con frecuencia del suscriptor.
- Conecte los datos de diagnóstico del dispositivo para ofrecer recomendaciones de resolución de problemas adaptadas en función del modelo de dispositivo y la versión de software específicos del suscriptor.
- Utilice los servicios perimetrales [!DNL Adobe Experience Platform] para ofrecer personalización con baja latencia dentro de la experiencia de la aplicación sin afectar el rendimiento.
- Implemente bucles de comentarios para que los suscriptores puedan informar sobre problemas de cobertura, enriqueciendo los datos de red y mostrando al mismo tiempo la capacidad de respuesta a su experiencia.


## Participación del programa de fidelización

Personalice las comunicaciones, las recompensas y las ofertas del programa de fidelidad en función del nivel del cliente, el saldo de puntos y el historial de canje, al tiempo que arbitra en tiempo real en los canales de aplicaciones, web, SMS y tiendas minoristas para evitar que las ofertas duplicadas o en conflicto lleguen al mismo suscriptor. Las restricciones de elegibilidad basadas en la capa determinan a qué recompensas, canjes de socios y promociones puede acceder cada suscriptor, y esas reglas deben aplicarse en el nivel de toma de decisiones en lugar de incrustarse en la lógica de campaña individual. El programa de fidelización también debe coordinarse con campañas de retención y actualización activas para que las ofertas de prevención de pérdida y las recompensas de fidelidad se complementen en lugar de duplicarse la entrega a los suscriptores que están simultáneamente en varios recorridos.

### Impacto empresarial

La participación personalizada en el programa de fidelización mejora la participación en el programa y recompensa el canje, lo que aumenta las tasas de retención entre los suscriptores inscritos.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para organizar comunicaciones de fidelidad personalizadas que destaquen recompensas relevantes, notifiquen a los suscriptores del progreso del nivel y presenten oportunidades de canje alineadas con sus preferencias y comportamientos. Este es el patrón correcto cuando el recorrido debe coordinar la entrega a través de los canales para evitar ofertas de lealtad duplicadas y cuando la selección de ofertas requiere estado de nivel e historial de canje: la orquestación de varios pasos por sí sola no proporciona el nivel de toma de decisiones en tiempo real necesario.

### Consideraciones técnicas

- Integre la plataforma de fidelidad para acceder a los saldos de puntos en tiempo real, el estado del nivel y el historial de canje para conseguir una personalización precisa.
- Conecte los catálogos de recompensas de los socios para presentar una amplia gama de opciones de canje adaptadas a los intereses demostrados y las amortizaciones anteriores de cada suscriptor.
- Coordine la mensajería de fidelidad con otros recorridos de la campaña para garantizar que las ofertas de retención y las recompensas de fidelidad se complementen en lugar de entrar en conflicto entre sí.
- Apoye los empujones de progresión del nivel calculando qué tan cerca está un suscriptor del siguiente nivel y presentando pasos procesables para alcanzarlo.


## Asesor de plan de IA

Los suscriptores de telecomunicaciones se enfrentan a un desafío persistente: comprender cómo se compara su plan actual con las opciones disponibles, y si un plan diferente se ajustaría mejor a su uso real. Las páginas de comparación de planes estáticos requieren que los suscriptores se autointerpreten los datos que es posible que no comprendan por completo, lo que conduce a selecciones de planes subóptimas, shock en las facturas y pérdidas evitables. Un asesor del plan de IA involucra a los suscriptores en una conversación natural, revisa sus patrones de uso desde su perfil en tiempo real, hace preguntas de calificación sobre las necesidades del equipo y los requisitos del hogar y los guía hacia el plan —o combinación de planes y complementos— que mejor se adapte a su situación.

### Impacto empresarial

La guía del plan conversacional reduce la pérdida basada en el plan, aumenta el archivo adjunto de actualización para los suscriptores que no reciben el servicio de su plan actual y reduce el volumen del centro de contacto para las consultas de facturación y cambio de plan.

### Cómo implementar

Usar el patrón [Experiencia de conversación en Brand Concierge](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md). Este método implementa Product Advisor Agent con el plan y el catálogo de complementos, utilizando AEP Agent Orchestrator y datos de perfil del cliente en tiempo real, incluido el historial de uso y los detalles del plan actual, para guiar a los suscriptores a través de la selección personalizada de planes mediante el diálogo natural. Este es el patrón correcto cuando el objetivo es un descubrimiento conversacional interactivo de varias vueltas que ayuda a los suscriptores a evaluar y seleccionar activamente el plan correcto, distinto de la mensajería activada por eventos, que notifica a los suscriptores de forma reactiva sobre los umbrales de uso o los cambios del plan, y de las experiencias web personalizadas, que muestran las comparaciones del plan de forma pasiva sin involucrar a los suscriptores en el diálogo correspondiente. Requiere la configuración de AEP Agent Orchestrator y gobernanza de marca.

### Consideraciones técnicas

- La búsqueda de perfiles de clientes en tiempo real debe mostrar detalles actuales del plan, patrones de uso de voz y datos, compatibilidad de dispositivos y estado del contrato para que el asesor pueda proporcionar orientación precisa y específica de la cuenta en lugar de descripciones genéricas del plan que requieran que el suscriptor se aplique a sí mismo en su situación.
- El plan y el catálogo de complementos deben mantenerse actualizados mediante la integración con el sistema de administración de productos, ya que recomendar un plan o precio promocional que ya no está disponible (u omitir una opción recién lanzada) socava directamente la confianza de los suscriptores y puede crear problemas de expectativas de servicio.
- Las protecciones de gobernanza de marca deben definir cómo gestiona el agente las comparaciones competitivas de operadores, las reclamaciones de precios promocionales y las discusiones de compromiso de contratos, lo que garantiza que las respuestas del agente se ajusten a las normas regulatorias y de marca sin crear compromisos engañosos que el suscriptor pueda impugnar más adelante.
- Las señales de conversación, incluido el tamaño del hogar declarado, el recuento de dispositivos, el interés de uso internacional y la intención de cambio de plan expresada durante el diálogo, deben capturarse como ExperienceEvents de XDM y transmitirse de nuevo a AEP, enriqueciendo los perfiles de los suscriptores para informar sobre las campañas de prevención de pérdida, actualización y venta cruzada en el flujo descendente.


## Tendencia de cancelación y análisis de experiencia de red

Correlacione las métricas de experiencia de red (caídas de llamadas, degradación del rendimiento de datos, exposición a interrupciones) con las tasas de contacto del servicio al cliente y los resultados de cancelación de suscripciones para identificar dónde se traducen los problemas de calidad de la red en un riesgo de desgaste mensurable. Los proveedores de telecomunicaciones que analizan el rendimiento de la red y el comportamiento de los clientes en sistemas separados no pueden determinar qué fallos de calidad del servicio realmente provocan la pérdida en comparación con cuáles se absorben sin consecuencias.

### Impacto empresarial

La conexión de los datos de experiencia de red con los resultados de comportamiento y pérdida del cliente permite que las operaciones de red, los productos y los equipos de retención prioricen las inversiones de corrección en función del impacto de desgaste demostrado, en lugar de la gravedad técnica por sí sola.

### Cómo implementar

Usar el patrón [Customer Analytics y Insight Generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Este método conecta los datos de eventos de red, los registros de interacción del servicio de atención al cliente, las señales de comportamiento digital y los eventos del ciclo vital de los suscriptores con Customer Journey Analytics, donde el análisis correlacionado identifica los umbrales de experiencia de red y los patrones de contacto que están asociados estadísticamente con la pérdida y la no renovación de contrato. Este es el patrón correcto cuando el objetivo es la generación de insight y el análisis de las causas raíz (comprender qué eventos de calidad de servicio provocan la desgaste) en lugar de activar una oferta de retención o activar una audiencia de riesgo de pérdida en un CDP.

### Consideraciones técnicas

- Los eventos de experiencia de red deben unirse a los registros de suscriptor mediante identificadores de cuenta o dispositivo que sean coherentes con el ID de persona configurado en la conexión de CJA, ya que los sistemas de telemetría de red suelen utilizar identificadores de equipo en lugar de identificadores de cliente de forma nativa.
- Los datos de contacto del servicio al cliente, incluidos los códigos de motivo de contacto, el canal utilizado y el estado de resolución, deben ingerirse como eventos con marcas de tiempo que permitan a los analistas crear rutas secuenciales desde incidencias de red hasta contactos de servicio, pasando por la pérdida en las visualizaciones de flujo o visitas en orden previsto de CJA.
- Los datos de plan y contrato del suscriptor, incluidas las fechas de finalización del contrato, el nivel de plan y el ejercicio, deben estar disponibles como dimensiones de consulta en la vista de datos de CJA para que el análisis de cancelación se pueda segmentar por proximidad de contrato y nivel de valor en lugar de tratar la base de suscriptor como homogénea.
- Los volúmenes de datos de telemetría de red pueden ser extremadamente grandes; se deben considerar estrategias de muestreo de conjuntos de datos o preagregación en AEP para mantener el rendimiento de las consultas de conexión de CJA dentro de intervalos aceptables para el uso de autoservicio de analistas.

## Prevención de pérdida y recuperación

Utilice modelos predictivos y señales de comportamiento para identificar a los clientes en riesgo y déclencheur campañas de retención personalizadas con ofertas adaptadas antes de que se produzcan. Los proveedores de telecomunicaciones se enfrentan a una presión de pérdida persistente, y llegar a los suscriptores en riesgo con la oferta correcta antes de que contacten con la cola de cancelación es significativamente más rentable que las campañas de recuperación después del hecho.

### Impacto empresarial

Los proveedores de telecomunicaciones con programas proactivos de prevención de pérdida ven reducciones significativas en la pérdida voluntaria para segmentos específicos, con el mayor impacto entre los clientes de valor medio donde las ofertas de retención específicas son más rentables que los descuentos generales.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para generar un recorrido de retención que identifique a los suscriptores en riesgo en función de las puntuaciones de tendencia a la pérdida, seleccione la oferta de retención adecuada mediante la lógica de toma de decisiones y envíela a través de los canales preferidos del suscriptor con pasos de seguimiento si se ignora el primer contacto. Este es el patrón correcto cuando se requieren la selección de ofertas y la orquestación de recorrido: un solo mensaje activado no puede admitir la lógica de clasificación de ofertas y el seguimiento multitáctil necesarios para una retención eficaz.

### Consideraciones técnicas

- Los modelos de tendencia a la pérdida deben recibir formación sobre los datos de pérdida históricos que incluyen experiencia de red, eventos de facturación, llamadas de servicio y edad del dispositivo. Los modelos formados solo en datos de participación suelen tener un rendimiento inferior al de los controladores de pérdida específicos de telecomunicaciones.
- Las ofertas de retención deben estar restringidas por umbrales de coste a conservar por segmento de valor del cliente; el motor de decisión debe evitar que las ofertas de retención de alto coste se apliquen a suscriptores de bajo valor.
- El procesamiento de señales de pérdida en tiempo real debe detectar eventos de consulta de contratos y visitas a la página de cancelación de servicios para almacenar en déclencheur respuestas de retención urgentes antes de que el suscriptor escale.
- La integración del servicio de atención al cliente es fundamental: los suscriptores que llaman a la cola de retención deben reconocerse como participantes del recorrido para que los agentes tengan el contexto de oferta de retención listo antes de que comience la llamada.
