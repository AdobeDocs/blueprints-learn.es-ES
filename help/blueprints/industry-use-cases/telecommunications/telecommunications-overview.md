---
title: Casos de uso de telecomunicaciones
description: Descubra cómo las organizaciones de telecomunicaciones utilizan Adobe Experience Platform para reducir la pérdida, impulsar las actualizaciones de los dispositivos y mejorar la participación de los clientes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2295'
ht-degree: 1%

---


# Casos de uso de telecomunicaciones

Las organizaciones de telecomunicaciones utilizan Adobe Experience Platform para crear una vista unificada de cada suscriptor y ofrecer experiencias personalizadas que reduzcan la pérdida, aumenten las actualizaciones de los planes y los dispositivos y refuercen las relaciones con los clientes a largo plazo. Al conectar los datos de uso de la red, la información de facturación y las interacciones con los clientes, los proveedores de telecomunicaciones pueden anticipar las necesidades de los suscriptores y comprometerlos en el momento adecuado a través de sus canales preferidos.

## Recomendaciones de actualización de dispositivos

Identifique a los clientes aptos para las actualizaciones de dispositivos y presente recomendaciones y ofertas de actualización de dispositivos personalizadas en función de los patrones de uso y las preferencias. Al analizar los plazos contractuales, la edad de los dispositivos y el comportamiento de navegación individual, los proveedores de telecomunicaciones pueden mostrar los dispositivos y las opciones de financiación más relevantes a cada suscriptor.

### Impacto empresarial

Las organizaciones que implementan recomendaciones de actualización de dispositivos suelen ver un aumento de entre el 30 y el 40 % en las tasas de conversión de la actualización al ofrecer la oferta correcta en el momento adecuado a través del canal preferido del cliente.

### Cómo implementar

Use el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para organizar recorridos de actualización que evalúen la elegibilidad, las preferencias del dispositivo y la afinidad del canal de cada suscriptor y así ofrecer ofertas de actualización personalizadas por correo electrónico, notificaciones de aplicaciones y experiencias en la tienda.

### Consideraciones técnicas

- Integre el inventario de dispositivos y los sistemas de precios para garantizar que las recomendaciones reflejen la disponibilidad actual y los precios promocionales.
- Conecte los datos de administración de contratos para identificar con precisión las ventanas de idoneidad para la actualización y las ofertas de actualización anticipada.
- Incorporar telemetría de uso del dispositivo (capacidad de almacenamiento, estado de la batería, métricas de rendimiento) para reforzar la relevancia de la recomendación.
- Coordínese con las plataformas de comercio minorista y electrónico para mantener una experiencia de actualización coherente en los canales digitales y en las tiendas.


## Planificar campañas de optimización

Analice los patrones de uso de los clientes y recomiende cambios de plan óptimos para ahorrar dinero u obtener mejores funciones según sus necesidades reales. Ponerse en contacto proactivamente con las recomendaciones del plan crea confianza y reduce el riesgo de que los suscriptores se vayan a la competencia con precios más sencillos.

### Impacto empresarial

Las campañas de optimización del plan suelen impulsar un aumento de entre el 25 y el 35 % en las tasas de cambio del plan, lo que mejora la satisfacción del cliente y, al mismo tiempo, aumenta los ingresos promedio por usuario cuando los suscriptores se trasladan a planes que se adaptan mejor a su consumo.

### Cómo implementar

Use el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para crear una campaña multitáctil que identifique las discrepancias de uso a plan, eduque a los suscriptores sobre mejores opciones y los guíe a través del proceso de cambio de plan con seguimientos oportunos.

### Consideraciones técnicas

- Ingeste datos de uso en tiempo real e históricos (minutos de voz, consumo de datos, llamadas internacionales) para identificar las discrepancias del plan con precisión.
- Conecte los datos del sistema de facturación para calcular los ahorros potenciales o las ganancias de las funciones para cada cambio de plan recomendado.
- Tenga en cuenta las reglas de precios promocionales y las obligaciones contractuales al generar recomendaciones de plan.
- Integre con portales de autoservicio para que los suscriptores puedan completar los cambios del plan directamente desde los puntos de contacto de la campaña.


## Prevención de pérdida para clientes de alto valor

Identifique a los clientes de alto valor que corren el riesgo de sufrir una pérdida de tiempo y actívelos con ofertas de retención personalizadas y un servicio de atención al cliente proactivo. Al combinar señales de comportamiento como una disminución del uso, llamadas de servicio repetidas y una navegación competitiva con datos de valor de duración, los proveedores pueden intervenir antes de que un suscriptor decida irse.

### Impacto empresarial

Los programas de prevención de pérdida dirigidos a suscriptores de alto valor generalmente logran una reducción de entre el 20 y el 30 % en la pérdida, lo que protege los ingresos recurrentes significativos y reduce el coste de adquirir clientes de reemplazo.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para monitorizar las señales de riesgo de pérdida en tiempo real, determinar la mejor oferta de retención para cada suscriptor y organizar una comunicación personalizada entre canales digitales y el centro de llamadas.

### Consideraciones técnicas

- Genere puntuaciones de tendencia a la pérdida combinando las tendencias de uso, el historial de interacciones del servicio y los datos de opinión de las transcripciones del centro de llamadas.
- Integre los sistemas de centros de llamadas y comercios minoristas para que los agentes tengan visibilidad de las ofertas de retención ya presentadas a través de canales digitales.
- Conecte datos de inteligencia competitiva (solicitudes de exclusión, comparaciones de planes de competidores) para refinar la puntuación de riesgo y las estrategias de oferta.
- Establezca reglas de gobernanza para evitar ponerse en contacto de forma excesiva con suscriptores en riesgo, lo que puede acelerar la pérdida en lugar de evitarla.


## Nuevo Recorrido de incorporación del cliente

Automatice un recorrido de incorporación personalizado para nuevos clientes con información de bienvenida, directrices de configuración de cuentas y tutoriales de funciones. Una experiencia de incorporación estructurada ayuda a los suscriptores a descubrir rápidamente todo el valor de su plan y servicios, sentando las bases para una retención a largo plazo.

### Impacto empresarial

Los recorridos de incorporación bien diseñados suelen aumentar las tasas de activación de las funciones en un 50-60 %, lo que conduce a puntuaciones de satisfacción más altas y a una menor pérdida de la vida útil temprana entre los nuevos suscriptores.

### Cómo implementar

Utilice el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para crear una experiencia de incorporación secuenciada que se adapte según el tipo de plan, el dispositivo y la participación de cada suscriptor con los pasos de incorporación anteriores.

### Consideraciones técnicas

- Integre sistemas de aprovisionamiento de cuentas para almacenar en déclencheur el recorrido de incorporación inmediatamente después de la activación y adapte el contenido al plan y el dispositivo específicos del suscriptor.
- Conecte los datos de participación de la aplicación para rastrear qué funciones ha explorado el suscriptor y ajustar los mensajes de incorporación subsiguientes en consecuencia.
- Coordine esta acción con la plataforma de asistencia al cliente para asegurarse de que los agentes conozcan la fase de incorporación de un suscriptor si llaman con preguntas.
- Admitir varias rutas de incorporación para diferentes segmentos de clientes, como suscriptores individuales, administradores de planes familiares y cuentas empresariales.


## Alertas y recomendaciones de uso de datos

Envíe alertas personalizadas cuando los clientes se aproximen a los límites de datos y recomienden actualizaciones de planes o complementos de datos basados en patrones de uso. Las notificaciones oportunas y útiles transforman una experiencia potencialmente frustrante en un momento de participación en el desarrollo de la confianza.

### Impacto empresarial

Las alertas proactivas de uso de datos suelen impulsar un aumento del 40 al 50 % en las compras de complementos de datos, a la vez que reducen las quejas por shock en las facturas y mejoran la satisfacción general del cliente.

### Cómo implementar

Use el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para enviar alertas en tiempo real cuando se superen los umbrales de uso, con recomendaciones personalizadas basadas en los patrones de consumo históricos y los detalles del plan del suscriptor.

### Consideraciones técnicas

- Conéctese a fuentes de datos de uso de red que proporcionan actualizaciones de consumo casi en tiempo real para las alertas de déclencheur con umbrales significativos (75 %, 90 % y 100 % de los límites del plan).
- Integre los sistemas de facturación y administración de planes para presentar precios exactos de complementos y permitir compras de un solo toque directamente desde el mensaje de alerta.
- Contabilice los conjuntos de datos compartidos en los planes de la familia alertando tanto al usuario individual como al administrador del plan.
- Implemente un límite de frecuencia para evitar la fatiga de alertas para los suscriptores que utilizan de forma consistente altas cantidades de datos en cada ciclo de facturación.


## Notificaciones de interrupción del servicio

Notificar a los clientes de forma proactiva sobre interrupciones del servicio, mantenimiento o problemas de red en su área con actualizaciones personalizadas y ofertas de compensación. Si se contacta antes de que los clientes experimenten frustración, se demuestra la responsabilidad y se reduce significativamente el volumen de asistencia entrante.

### Impacto empresarial

Las notificaciones proactivas de interrupción suelen lograr una tasa de reconocimiento de notificaciones del 60-70% y reducir sustancialmente el volumen del centro de llamadas durante las interrupciones del servicio, lo que reduce los costes de asistencia y mejora la percepción de los clientes.

### Cómo implementar

Use el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para detectar eventos de red y notificar inmediatamente a los suscriptores afectados a través de sus canales preferidos con detalles relevantes, tiempos de resolución estimados y una compensación apropiada cuando esté justificado.

### Consideraciones técnicas

- Integración con los sistemas de supervisión del centro de operaciones de red para recibir datos de eventos de interrupción en tiempo real y mantenimiento con información del ámbito geográfico.
- Utilice los datos de dirección y ubicación del suscriptor para identificar con precisión a los clientes afectados y evitar notificar a los que se encuentran fuera del área afectada.
- Conéctese al sistema de facturación y créditos para automatizar las ofertas de crédito de servicio para interrupciones prolongadas en función del plan del suscriptor y la duración de la interrupción.
- Coordine la mensajería entre canales para proporcionar actualizaciones de estado coherentes y evitar enviar información conflictiva a medida que evoluciona la situación.


## Administración del plan familiar

Personalice las comunicaciones y ofertas para los administradores de planes familiares en función de los patrones de uso familiar y las necesidades individuales de los miembros. Los planes familiares representan cuentas multilínea de alto valor donde la participación con el administrador del plan genera retención en todas las líneas.

### Impacto empresarial

Las comunicaciones personalizadas de administración de planes familiares suelen aumentar la participación en los planes familiares en un 30-40%, lo que conduce a una mayor retención de líneas y a un mayor valor de duración por cuenta.

### Cómo implementar

Use el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para analizar el uso en todos los miembros de la familia, identificar oportunidades como agregar líneas o ajustar límites individuales, y ofrecer recomendaciones personalizadas al administrador del plan.

### Consideraciones técnicas

- Jerarquías de cuentas de familia de modelos para distinguir entre el administrador del plan y los miembros individuales, respetando los niveles de permisos para las comunicaciones y los cambios de cuenta.
- Agregue datos de uso en todas las líneas de la cuenta para identificar patrones y oportunidades a nivel familiar, como datos compartidos infrautilizados o ciclos de actualización de dispositivos desiguales.
- Integre el control parental y los sistemas de filtrado de contenido para admitir funciones específicas de la familia en la personalización.
- Asegúrese de que existan controles de privacidad para que los detalles de uso de los miembros individuales se compartan apropiadamente con el administrador del plan en función de los permisos de la cuenta.


## Campañas de actualización 5G

Clientes objetivo elegibles para actualizaciones de red 5G con ofertas y beneficios personalizados en función de su ubicación y patrones de uso. A medida que la cobertura 5G se expande, llegar a los suscriptores en las áreas recién cubiertas con mensajes relevantes acelera la adopción y aumenta la utilización de la red.

### Impacto empresarial

Las campañas de actualización 5G dirigidas suelen impulsar un aumento del 25 al 35% en las tasas de adopción de 5G entre los suscriptores elegibles, lo que respalda los retornos de inversión en red y la diferenciación competitiva.

### Cómo implementar

Utilice el patrón [Activación de mensaje saliente por lotes](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) para segmentar a los suscriptores según la disponibilidad de cobertura 5G, la compatibilidad del dispositivo y la elegibilidad del plan. Luego, ofrezca campañas de actualización personalizadas que resalten los beneficios más relevantes para el perfil de uso de cada suscriptor.

### Consideraciones técnicas

- Integre mapas de cobertura de red para identificar con precisión a los suscriptores en áreas con servicio 5G activo y evitar promocionar actualizaciones donde la cobertura aún no está disponible.
- Conecte los datos de compatibilidad del dispositivo para determinar qué suscriptores necesitan un dispositivo nuevo en comparación con aquellos que ya tienen hardware compatible con 5G.
- Coordínese con los sistemas de inventario minorista para garantizar que los dispositivos y planes promocionados estén disponibles en la tienda preferida del suscriptor o en línea.
- Mensajería de segmentos por perfil de uso para que los usuarios de datos pesados reciban beneficios centrados en el rendimiento mientras que los usuarios ocasionales reciben mensajes de cobertura y fiabilidad.


## Recordatorios de pago de factura

Envíe recordatorios personalizados de pago de factura a través de los canales preferidos con opciones de pago e información de saldo de cuenta. Los recordatorios oportunos y convenientes reducen la demora en los pagos y los costes de cobranza asociados, al tiempo que mantienen una relación positiva con el cliente.

### Impacto empresarial

Los recordatorios personalizados de pago de factura generalmente mejoran las tasas de pago a tiempo en un 20-30%, reduciendo los gastos de cobro y minimizando las suspensiones de servicio que generan insatisfacción en los clientes.

### Cómo implementar

Usa el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para enviar recordatorios en momentos óptimos antes de la fecha límite, personalizados con el saldo del suscriptor, el método de pago preferido y un enlace directo para completar el pago.

### Consideraciones técnicas

- Integre con la plataforma de facturación para acceder a los saldos de cuentas en tiempo real, las fechas de vencimiento y el historial de pagos para obtener un contenido de recordatorio preciso.
- Conéctese a los sistemas de procesamiento de pagos para habilitar el pago mediante un solo toque o un solo clic directamente desde el mensaje recordatorio.
- Implemente una lógica de escalación que ajuste la urgencia y la frecuencia del recordatorio a medida que se acerca la fecha de vencimiento, respetando al mismo tiempo las preferencias de comunicación.
- Admite múltiples métodos de pago (inscripción de pago automático, cartera digital, transferencia bancaria) y personaliza las opciones presentadas en función del historial del suscriptor.


## Recomendaciones del servicio de complementos

Recomendar servicios adicionales relevantes, como seguros de dispositivos, almacenamiento en la nube y paquetes de streaming, en función del plan, el uso y las preferencias del cliente. Las recomendaciones contextuales aumentan el valor que los suscriptores reciben de su relación con el proveedor, a la vez que aumentan los ingresos promedio por usuario.

### Impacto empresarial

Las recomendaciones de servicios de complementos personalizados suelen impulsar un aumento de entre el 15 y el 25 % en las tasas de adopción de complementos, lo que amplía los ingresos de la base de suscriptores existente sin el coste de la adquisición de nuevos clientes.

### Cómo implementar

Utilice el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) para evaluar el perfil, los servicios actuales y las señales de comportamiento de cada suscriptor con el fin de determinar la oferta de complemento más relevante y presentarla en el canal y el momento óptimos.

### Consideraciones técnicas

- Conéctese al catálogo de servicios actual del suscriptor para evitar recomendar servicios que ya tiene e identificar complementos naturales para su plan existente.
- Integre datos de socios y servicios de terceros (proveedores de streaming, compañías de seguros) para presentar precios precisos y ofertas agrupadas.
- Utilice los datos de uso y del dispositivo para informar las recomendaciones, como sugerir un seguro del dispositivo para los suscriptores con nuevos dispositivos Premium o almacenamiento en la nube para aquellos que se queden sin almacenamiento del dispositivo.
- Coordine la personalización en la aplicación y la web para reforzar las recomendaciones de complementos en los puntos de contacto de autoservicio.


## Personalization de rendimiento de red

Personalice la información y las recomendaciones de rendimiento de red en función de la ubicación, el dispositivo y los patrones de uso del cliente. Ayudar a los suscriptores a optimizar su experiencia de conectividad crea confianza y reduce los contactos de asistencia asociados con problemas de rendimiento.

### Impacto empresarial

Las experiencias de rendimiento de red personalizadas suelen aumentar la participación de la aplicación en un 35-45 %, a medida que los suscriptores regresan para comprobar la cobertura, solucionar problemas y descubrir consejos de optimización adaptados a su situación.

### Cómo implementar

Use el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones y web de visitantes conocidos para ofrecer paneles de rendimiento de red personalizados, información de cobertura y recomendaciones de optimización dentro de la experiencia de la cuenta web y la aplicación del suscriptor.

### Consideraciones técnicas

- Integre métricas de calidad de red y datos de cobertura para proporcionar información de rendimiento específica de la ubicación relevante para el hogar, el trabajo y las áreas visitadas con frecuencia del suscriptor.
- Conecte los datos de diagnóstico del dispositivo para ofrecer recomendaciones de resolución de problemas adaptadas en función del modelo de dispositivo y la versión de software específicos del suscriptor.
- Utilice los servicios perimetrales [!DNL Adobe Experience Platform] para ofrecer personalización con baja latencia dentro de la experiencia de la aplicación sin afectar el rendimiento.
- Implemente bucles de comentarios para que los suscriptores puedan informar sobre problemas de cobertura, enriqueciendo los datos de red y mostrando al mismo tiempo la capacidad de respuesta a su experiencia.


## Participación del programa de fidelización

Personalice las comunicaciones, las recompensas y las ofertas del programa de fidelidad en función del nivel del cliente, el saldo de puntos y el historial de canje. Una experiencia de lealtad bien personalizada fortalece la conexión emocional con la marca y crea costes de cambio significativos más allá de los términos del contrato.

### Impacto empresarial

La participación personalizada en el programa de fidelización suele aumentar la participación en el programa y recompensar el canje en un 30-40 %, lo que aumenta las tasas de retención entre los suscriptores inscritos.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para organizar comunicaciones de fidelidad personalizadas que destaquen recompensas relevantes, notifiquen a los suscriptores del progreso del nivel y presenten oportunidades de canje alineadas con sus preferencias y comportamientos.

### Consideraciones técnicas

- Integre la plataforma de fidelidad para acceder a los saldos de puntos en tiempo real, el estado del nivel y el historial de canje para conseguir una personalización precisa.
- Conecte los catálogos de recompensas de los socios para presentar una amplia gama de opciones de canje adaptadas a los intereses demostrados y las amortizaciones anteriores de cada suscriptor.
- Coordine la mensajería de fidelidad con otros recorridos de la campaña para garantizar que las ofertas de retención y las recompensas de fidelidad se complementen en lugar de entrar en conflicto entre sí.
- Apoye los empujones de progresión del nivel calculando qué tan cerca está un suscriptor del siguiente nivel y presentando pasos procesables para alcanzarlo.
