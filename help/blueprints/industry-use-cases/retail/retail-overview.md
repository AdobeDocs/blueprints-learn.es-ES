---
title: Casos de uso minorista
description: Descubra cómo las organizaciones de minoristas utilizan Adobe Experience Platform para personalizar las experiencias de compra, recuperar los carros de compras abandonados e impulsar la lealtad de los clientes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 89a5b6b5-bb71-4154-bb3b-f6dbbbef13eb
source-git-commit: 0236bd326730ee9a0be621ee0e60ddc3d352410d
workflow-type: tm+mt
source-wordcount: '6166'
ht-degree: 0%

---

# Casos de uso minorista

Las organizaciones minoristas utilizan Adobe Experience Platform para unificar los datos de clientes de tiendas en línea, ubicaciones físicas y programas de fidelidad en una sola vista de cada comprador. Esta base permite experiencias de compra personalizadas, un alcance oportuno que recupera los ingresos perdidos y estrategias de lealtad que mantienen a los clientes regresando.

## Recomendaciones de productos personalizadas

Muestre recomendaciones de productos personalizadas en la página de inicio, en las páginas de categoría y en las páginas de detalles del producto, en función del historial de navegación, el historial de compras y un comportamiento similar del cliente. Cuando los compradores ven productos adaptados a sus intereses, pasan más tiempo explorando y es mucho más probable que compren.

### Impacto empresarial

Los minoristas ven tasas de clics y tasas de conversión mejoradas al ofrecer recomendaciones personalizadas en lugar de listas de productos estáticas.

### Cómo implementar

Usar el patrón [Behavioral Recommendations](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Este enfoque utiliza modelos de recomendación impulsados por IA que aprenden continuamente de las interacciones de los clientes para mostrar los productos más relevantes para cada individuo. Este es el patrón correcto cuando el conjunto de elementos es grande y cambia continuamente, y la selección depende de la afinidad del comportamiento, en lugar de un conjunto limitado de ofertas gobernadas por reglas de idoneidad.

### Consideraciones técnicas

- Los datos del catálogo de productos deben ingerirse y mantenerse actualizados, incluidos los atributos de productos, las imágenes, los precios y la disponibilidad, para garantizar que las recomendaciones reflejen lo que los clientes pueden comprar realmente.
- Las señales de comportamiento, como las vistas de productos, los eventos de complementos al carro de compras y las compras, deben fluir en tiempo casi real para que las recomendaciones estén actualizadas en una sola sesión de navegación.
- Los modelos de recomendación requieren una estrategia de inicio en frío para los nuevos visitantes que carecen de historial de navegación, lo que generalmente vuelve a los productos de tendencias o más vendidos.
- El rendimiento de carga de la página debe monitorizarse cuidadosamente, ya que las llamadas de personalización no deben añadir una latencia marcada a la experiencia de compra.


## Recuperación de correo electrónico del carro abandonado

Envíe automáticamente recordatorios por correo electrónico personalizados a los clientes que abandonaron su carro de compras, incluidos los artículos exactos que quedaron y las ofertas relevantes para fomentar la finalización. El abandono del carro de compras es una de las mayores fuentes de pérdida de ingresos en el comercio minorista, y el seguimiento oportuno puede recuperar una parte significativa de esas ventas.

### Impacto empresarial

Los programas eficaces de recuperación del carro de compras mejoran las tasas de recuperación del carro de compras y pueden generar ingresos incrementales significativos según el volumen de la tienda.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método responde a un evento de abandono del carro de compras en tiempo real, lo que envía un recordatorio oportuno mientras la intención de compra sigue siendo alta. Este es el patrón correcto cuando el déclencheur es una acción de cliente discreta y la respuesta necesaria es un mensaje único, con distinción de tiempo, en lugar de una secuencia de varios pasos o una selección de oferta dinámica.

### Consideraciones técnicas

- La detección de abandonos del carro de compras requiere la definición de un umbral de inactividad (normalmente, de 30 a 60 minutos) antes de activar el primer recordatorio, lo que evita enviar mensajes a los clientes que aún realizan compras de forma activa.
- El contenido del correo electrónico debe extraer dinámicamente las imágenes del producto, los precios y la disponibilidad actuales del catálogo en el momento de la entrega, ya que los artículos pueden agotarse o cambiar el precio entre el abandono y la entrega.
- Las reglas de restricción de frecuencia deben evitar que los clientes reciban varios correos electrónicos sobre el carro de compras de abandono en un corto período, especialmente si abandonan el carro de compras con frecuencia.
- Las listas de consentimiento y supresión deben comprobarse antes de la entrega, y los clientes que completaron su compra a través de otro canal deben excluirse en tiempo real.


## Campañas de urgencia basadas en inventario

Déclencheur alertas y campañas en tiempo real cuando el inventario de productos es bajo, lo que crea urgencia y fomenta la compra inmediata. Los compradores que ven que solo quedan unos pocos artículos están motivados a actuar rápidamente en lugar de retrasar su decisión.

### Impacto empresarial

Las campañas de baja urgencia de inventario impulsan una conversión mejorada para los productos destacados, a la vez que ayudan a reducir el exceso de existencias al acelerar la venta de artículos de movimiento lento.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método responde a los eventos de umbral de inventario, activando automáticamente los mensajes de urgencia cuando los niveles de stock caen por debajo de los límites definidos. Este es el patrón correcto cuando el déclencheur es un evento del sistema en lugar de un comportamiento del cliente, y la comunicación necesaria es inmediata y reactiva en lugar de una secuencia de nutrición sostenida.

### Consideraciones técnicas

- Las fuentes de inventario deben integrarse con la plataforma de datos del cliente en tiempo casi real para que la mensajería de urgencia refleje los niveles de stock reales en lugar de los datos antiguos.
- Los niveles de umbral deben configurarse por categoría de producto, ya que un umbral de &quot;existencias bajas&quot; para una mercancía de gran volumen difiere significativamente de uno para un artículo de lujo.
- La mensajería debe ser veraz y cumplir con las regulaciones de protección al consumidor; mostrar una falsa escasez puede dañar la confianza de la marca y puede violar los estándares de publicidad en ciertos mercados.
- Los canales de mensajería in situ y de correo electrónico deben coordinarse para que un cliente que ya ha adquirido no siga recibiendo notificaciones de urgencia para el mismo producto.


## Recomendaciones de venta cruzada y ampliación de venta

Muestre los productos de venta cruzada y de ampliación de ventas relevantes al cerrar la compra, en correos electrónicos y en páginas de productos basadas en patrones de compra y relaciones de productos. La sugerencia de alternativas complementarias o premium en el momento adecuado aumenta el tamaño de la cesta sin requerir que los clientes busquen artículos relacionados ellos mismos.

### Impacto empresarial

Las estrategias de venta cruzada y de ampliación de ventas bien ejecutadas aumentan el valor promedio de los pedidos y aumentan los ingresos por transacción, lo que contribuye a una economía general de la canasta más sólida.

### Cómo implementar

Usar el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Este método emplea una lógica de decisión centralizada que evalúa todas las ofertas disponibles y selecciona la mejor opción de venta cruzada o ampliación de venta para cada cliente y contexto. Este es el patrón correcto cuando la selección de ofertas debe tener en cuenta el margen, la disponibilidad de inventario y las reglas de relación de productos: restricciones empresariales que requieren una lógica de toma de decisiones controlada en lugar de una clasificación de afinidad de comportamiento por sí sola.

### Consideraciones técnicas

- Los datos de relación de productos, incluidas las asociaciones &quot;compradas juntas con frecuencia&quot; y las rutas de actualización, deben mantenerse y actualizarse regularmente para reflejar los patrones de compra actuales.
- La lógica de clasificación de ofertas debe tener en cuenta los niveles de margen, relevancia e inventario para que las opciones más rentables y disponibles aparezcan primero.
- Las recomendaciones de venta cruzada al finalizar la compra deben cargarse rápidamente y no interrumpir el flujo de compra. Las sugerencias lentas o intrusivas pueden reducir la conversión.
- [!DNL Journey Optimizer] reglas de decisión deben incluir ofertas de reserva para que todos los clientes elegibles reciban una recomendación, incluso cuando la opción de mayor clasificación no esté disponible.


## Nueva serie de bienvenida al cliente

Automatice una serie de bienvenida de varios correos electrónicos para nuevos clientes con recomendaciones de productos personalizadas, narración de marcas y ofertas especiales. Las primeras interacciones después de que un cliente se una dan forma a su relación a largo plazo con la marca, lo que convierte a esta serie en uno de los programas de mayor impacto que puede ejecutar un retailer.

### Impacto empresarial

Una serie de bienvenida bien diseñada genera una fuerte participación entre los nuevos clientes y mejora significativamente el valor de por vida al crear afinidad de marca desde el principio.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Este recorrido de nutrición multitáctil guía a los nuevos clientes a través de una secuencia de mensajes de presentación de marca, descubrimiento de productos e incentivos, adaptándose en función de su participación. Este es el patrón correcto cuando el caso de uso requiere un flujo de mensajes múltiples secuenciado a lo largo de días con ramificación condicional basada en eventos de participación: un solo mensaje activado no puede dar cabida a la lógica de dependencia entre pasos.

### Consideraciones técnicas

- El déclencheur de entrada de recorrido debe capturar de forma fiable los nuevos eventos de creación de clientes desde todas las fuentes de registro, incluidos los mercados web, de aplicaciones móviles, de puntos de venta en tienda y de terceros.
- Los pasos de espera entre correos electrónicos deben configurarse en función de los datos de participación; los clientes que abran y hagan clic pueden recibir el siguiente mensaje antes, mientras que los clientes menos comprometidos se benefician de un mayor espaciado.
- Las recomendaciones de productos dentro de los correos electrónicos de bienvenida deben reflejar lo que el cliente navegó o compró durante su primera visita, no los productos genéricos más vendidos.
- Los clientes que realizan una compra durante la serie de bienvenida deben ramificarse en un flujo posterior a la compra en lugar de seguir recibiendo mensajes centrados en la adquisición.


## Alertas de bajada de precios

Notificar a los clientes por correo electrónico o mediante una notificación push cuando los productos de su lista de deseos o los artículos vistos anteriormente bajen de precio. Los compradores que mostraron interés pero no compraron son muy receptivos a las reducciones de precios, lo que lo convierte en una de las formas más eficientes de convertir la consideración en ventas.

### Impacto empresarial

Las alertas de bajada de precios generan tasas de conversión mejoradas entre los destinatarios y aumentan de forma mensurable la satisfacción del cliente, ya que ayudan a los compradores a sentir que obtienen el mejor valor.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método responde a los eventos de cambio de precios de los productos, contrastándolos con las señales de interés de los clientes para enviar notificaciones oportunas. Este es el patrón correcto cuando el déclencheur es un evento del sistema de catálogo y la ventana de envío es sensible al tiempo: un recorrido sostenido sería demasiado lento y no se necesita un seguimiento de varios pasos más allá de la notificación inicial.

### Consideraciones técnicas

- La detección de cambios de precios requiere comparar los precios actuales con los valores anteriores en la fuente del catálogo de productos y activar solo alertas para reducciones significativas en lugar de fluctuaciones menores.
- Las señales de interés del cliente (adiciones a listas de deseos, vistas de páginas de productos, tiempo invertido en páginas de productos) deben almacenarse y compararse de forma eficaz con posibles miles de cambios diarios de precios.
- Las notificaciones deben incluir el precio original, el nuevo precio y la cantidad de ahorro para comunicar claramente el valor; los mensajes vagos de &quot;precio reducido&quot; no permiten llamadas de ahorro específicas.
- Se pueden usar [!DNL Real-Time Customer Data Platform] segmentos para compradores sensibles al precio para priorizar la entrega de alertas y adaptar el tono de la mensajería.


## Recordatorios de reposición

Envíe recordatorios automatizados a los clientes sobre los productos que compran con regularidad, como artículos de suscripción y consumibles, para animar a que realicen compras más frecuentes antes de que se agoten. Los recordatorios proactivos reducen la posibilidad de que los clientes cambien a un competidor simplemente porque se olvidaron de reordenar.

### Impacto empresarial

Los programas de recordatorio de reposición impulsan las tasas de repetición de compras mejoradas y mejoran la retención de clientes al hacer que sea fácil para los compradores reponer existencias de los productos en los que dependen.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Este recorrido programado recurrente utiliza predicciones de frecuencia de compra para enviar recordatorios en el momento óptimo antes de que sea probable que un cliente necesite una recarga. Este es el patrón correcto cuando no hay ningún evento de activación discreto y el tiempo debe calcularse a partir de modelos de frecuencia de compra que se recalibran dinámicamente. Los mensajes activados por eventos no pueden gestionar la programación predictiva o los ajustes de tiempo cuando los clientes realizan un pedido anticipado o tardío.

### Consideraciones técnicas

- El cálculo de la frecuencia de compra debe tener en cuenta las diferentes tasas de consumo entre categorías de productos; un recordatorio para el café debe llegar en una cadencia diferente a la de los suministros de limpieza.
- El recorrido debe ajustar su temporización de forma dinámica cuando un cliente realiza nuevos pedidos antes o después de lo previsto, recalibrando el siguiente recordatorio en función de los datos de compra actualizados.
- Los recordatorios deben incluir un enlace de reorden directo o una opción de recompra con un solo clic para minimizar la fricción y maximizar la conversión a partir de la notificación.
- Los clientes que ya hayan realizado un repedido a través de otro canal (en tienda, servicio de suscripción) deben suprimirse para evitar el envío de recordatorios irrelevantes.


## Páginas de categoría personalizadas

Personalice de forma dinámica las páginas de categorías para mostrar primero los productos más relevantes en función de las preferencias, las compras anteriores y el comportamiento de navegación de cada cliente. Cuando los compradores ven los productos alineados con sus gustos en la parte superior de la página, descubren lo que quieren más rápido y convierten a tasas más altas.

### Impacto empresarial

Las páginas de categoría personalizadas mejoran la participación de las páginas de categoría y el descubrimiento de productos, especialmente para los minoristas con catálogos grandes.

### Cómo implementar

Usar el patrón [Behavioral Recommendations](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Este método utiliza estrategias de selección y modelos de clasificación para reordenar los productos en páginas de categoría en función del perfil de cada visitante y del comportamiento en tiempo real. Este es el patrón correcto cuando la tarea clasifica un conjunto de productos grande y abierto mediante señales de afinidad de comportamiento . Offer Decisioning no es adecuado aquí porque no hay reglas de elegibilidad ni restricciones comerciales que limiten qué productos aparecen.

### Consideraciones técnicas

- La clasificación de productos debe ejecutarse con la rapidez suficiente para evitar los retrasos de carga de página percibidos; la personalización del lado del servidor o la toma de decisiones basada en Edge suelen ser necesarias para las páginas de categorías con cientos de productos.
- La lógica de personalización debe combinar las preferencias individuales con las reglas de comercialización, lo que garantiza que los productos promocionados, los recién llegados y los artículos de temporada sigan recibiendo la visibilidad adecuada.
- Debe contarse con una infraestructura de prueba A/B para medir de forma continua el impacto en los ingresos de la clasificación personalizada frente a las reglas de comercialización predeterminadas.
- La implementación de Web SDK de [!DNL Experience Platform] debe capturar las interacciones entre páginas de categorías (profundidad de desplazamiento, clics en productos, uso de filtros) para refinar continuamente los modelos de clasificación.


## Campañas de seguimiento posteriores a la compra

Envíe correos electrónicos posteriores a la compra con consejos de atención del producto, sugerencias de productos relacionados, solicitudes de revisión e información del programa de fidelidad. El periodo inmediatamente posterior a una compra es cuando los clientes están más comprometidos con la marca, lo que la convierte en una ventana ideal para profundizar la relación e impulsar la actividad futura.

### Impacto empresarial

Las campañas efectivas posteriores a la compra aumentan las tasas de envío de revisión y aumentan las tasas de repetición de compras, convirtiendo a los compradores únicos en clientes fieles.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Este flujo posterior a la compra de varios pasos utiliza la lógica de ramificación para adaptar los mensajes de seguimiento en función del tipo de producto, el segmento del cliente y la participación con correos electrónicos anteriores de la serie. Este es el patrón correcto porque el seguimiento abarca varios días, depende de eventos de estado de cumplimiento y ramas basadas en la categoría del producto y eventos de devolución: un solo mensaje activado no puede admitir la lógica condicional requerida en toda la cronología posterior a la compra.

### Consideraciones técnicas

- El recorrido debe tener en cuenta el estado de cumplimiento del pedido; las sugerencias de atención y las solicitudes de revisión solo deben enviarse después de que se haya entregado el producto, no inmediatamente después de la compra.
- El contenido específico del producto (instrucciones de cuidado, guías de uso, sugerencias de accesorios) requiere un sistema de asignación de contenido que asocie cada categoría de producto con materiales de seguimiento relevantes.
- El tiempo de solicitud de revisión debe optimizarse en función de la categoría del producto; los productos electrónicos pueden necesitar un periodo de uso más largo antes de una revisión significativa, mientras que la ropa puede revisarse poco después de la entrega.
- Los clientes que inician una devolución o un intercambio deben eliminarse automáticamente del flujo estándar posterior a la compra y redirigirse a una ruta de recuperación del servicio.


## Ofertas exclusivas para clientes de VIP

Identifique clientes de alto valor y proporcione ofertas exclusivas, acceso anticipado a ventas y experiencias de compra personalizadas que recompensen su lealtad. Retener a los clientes de alto nivel es mucho más rentable que adquirir nuevos clientes, y el tratamiento exclusivo fortalece la conexión emocional que los mantiene gastando.

### Impacto empresarial

Los programas de VIP generan una fuerte participación de los clientes de nivel superior y mejoran de forma mensurable el valor de duración del cliente al reducir la pérdida entre los segmentos más rentables.

### Cómo implementar

Usar el patrón [Cross-Channel Recorrido with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Este enfoque combina la orquestación de recorridos con la toma de decisiones en tiempo real para la selección de ofertas, lo que garantiza que cada cliente de VIP reciba la oferta exclusiva más relevante en cada canal. Este es el patrón correcto cuando el recorrido debe coordinar la entrega a través de los canales para evitar ofertas duplicadas y cuando la selección de ofertas requiere reglas de elegibilidad y restricciones empresariales: la orquestación de varios pasos por sí sola no proporciona el nivel de toma de decisiones en tiempo real necesario para gobernar qué oferta exclusiva recibe cada VIP.

### Consideraciones técnicas

- Los criterios de segmentación de VIP deben definirse claramente mediante métricas de actualización, frecuencia y valor monetario, y los segmentos deben actualizarse con la frecuencia suficiente para capturar a los clientes que cumplen los requisitos o no cumplen los requisitos recientemente.
- Las ofertas exclusivas deben aplicarse en el momento del canje (web, aplicación, tienda) para evitar que los clientes que no son de VIP accedan a ellas, lo que requiere la integración con sistemas de promoción y precios.
- Las preferencias de canal varían significativamente entre los clientes de alto valor; algunos prefieren el correo electrónico, otros responden a notificaciones de aplicaciones o al correo directo, por lo que el recorrido debe adaptar los canales de entrega en función de la participación anterior.
- La toma de decisiones de [!DNL Journey Optimizer] debe coordinarse entre canales para evitar que un cliente de VIP reciba la misma oferta por correo electrónico, push y SMS simultáneamente.


## Notificaciones de falta de existencias

Permita que los clientes se registren para recibir notificaciones cuando los productos sin existencias estén disponibles y, a continuación, notifíquelos automáticamente por correo electrónico o mensaje de texto. Capturar la demanda de productos no disponibles evita la pérdida de ventas y da a los clientes una razón para regresar a la tienda en lugar de comprar a un competidor.

### Impacto empresarial

Las notificaciones de vuelta en stock logran fuertes tasas de conversión entre los suscriptores y reducen significativamente la pérdida de ventas de productos de alta demanda que experimentan agotamientos temporales de existencias.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método pone en déclencheur las notificaciones de eventos de reserva, comparando las actualizaciones de inventario con los registros de notificaciones de clientes para ofrecer alertas oportunas. Este es el patrón correcto porque el déclencheur es un evento de sistema de inventario discreto, la entrega es esencial en función del tiempo (el inventario puede agotarse de nuevo rápidamente) y la comunicación es una sola notificación, no un recorrido continuo.

### Consideraciones técnicas

- La monitorización del inventario debe detectar los eventos de reabastecimiento rápidamente; los retrasos de incluso unas pocas horas pueden resultar en que el producto se vuelva a vender antes de que los clientes notificados tengan la oportunidad de comprar.
- Cuando un producto popular vuelve a estar disponible en cantidades limitadas, las notificaciones deben escalonarse o priorizarse por fecha de registro para evitar enviar alertas a más clientes de los que puede entregar el inventario disponible.
- El mecanismo de registro de notificaciones debe capturar la preferencia de canal (correo electrónico o mensaje de texto) y cumplir con los requisitos de inclusión de cada canal, especialmente en el caso de los SMS.
- [!DNL Real-Time Customer Data Platform] atributos de perfil deben rastrear qué productos está viendo cada cliente, de modo que se eviten las notificaciones duplicadas si el mismo producto se reabastece varias veces.


## Personalization de Social Proof

Muestre pruebas sociales personalizadas, incluidas críticas, clasificaciones y sugerencias de &quot;los clientes que compraron esto también compraron&quot;, en función del perfil y las preferencias de cada cliente. Adaptar la prueba social para reflejar las experiencias de clientes similares crea confianza de forma más eficaz que las clasificaciones genéricas por sí solas.

### Impacto empresarial

La prueba social personalizada aumenta las tasas de conversión y mejora la confianza de los compradores, especialmente en el caso de los compradores nuevos y los productos con precios más altos, donde las dudas sobre las compras son mayores.

### Cómo implementar

Usar el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones/web de visitantes conocidos. Este método personaliza el contenido web de los visitantes identificados, seleccionando las revisiones más relevantes y los elementos de prueba social en función del perfil del cliente, las preferencias y el contexto de navegación. Este es el patrón correcto cuando la personalización está impulsada por atributos de perfil y la pertenencia a segmentos en lugar de por un modelo de afinidad de comportamiento: la recomendación de comportamiento no es apropiada aquí porque la selección de pruebas sociales depende de quién sea el cliente, no de qué artículos haya buscado.

### Consideraciones técnicas

- Los datos de revisión y clasificación deben estar estructurados y etiquetados por atributos del cliente (como el contexto de compra, el segmento del cliente y el caso de uso del producto) para permitir un filtrado y una personalización significativos.
- Los elementos de prueba de Social se deben cargar de forma asíncrona para evitar el bloqueo del procesamiento de la página del producto principal, ya que los datos de revisión pueden proceder de una plataforma de revisión de terceros con tiempos de respuesta variables.
- Las regulaciones de privacidad requieren que cualquier dato de cliente utilizado para relacionar las reseñas con los visitantes se gestione de acuerdo con las preferencias de consentimiento; la visualización del contenido &quot;clientes como usted&quot; implica la creación de perfiles que pueden requerir divulgación.
- [!DNL Experience Platform] miembros de la audiencia pueden usarse para seleccionar qué críticas resaltar, mostrando las opiniones de los amantes de las actividades al aire libre de otros compradores en lugar de las críticas genéricas de mejor puntuación.


## Asesor de productos de IA

Los minoristas en línea llevan miles de SKU a través de complejas jerarquías de categorías, lo que dificulta a los compradores encontrar el producto adecuado sin una navegación prolongada o búsquedas abandonadas. Un asesor de productos con tecnología de IA involucra a los compradores en diálogos naturales de varias vueltas (haciendo preguntas de calificación sobre necesidades, preferencias y presupuesto) y luego reduce la variedad a un conjunto seleccionado de recomendaciones personalizadas. La experiencia refleja la orientación que un experto en la tienda podría proporcionar, ofrecida a escala digital.

### Impacto empresarial

Los minoristas que implementan la detección conversacional guiada ven tasas de conversión mejoradas y un valor de pedido promedio en comparación con la exploración no asistida, a la vez que reducen la devolución de productos a través de decisiones de compra mejor informadas.

### Cómo implementar

Usar el patrón [Experiencia de conversación en Brand Concierge](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md). Este enfoque implementa Product Advisor Agent con un catálogo de productos estructurado, utilizando AEP Agent Orchestrator y datos de perfil del cliente en tiempo real para generar recomendaciones de productos personalizadas y seguras de marca a través del diálogo natural. Este es el patrón correcto cuando el objetivo es un descubrimiento conversacional interactivo de varias vueltas impulsado por necesidades declaradas por el cliente, distinto de la mensajería activada por eventos, que es unidireccional y reactiva a una acción específica, y de las experiencias web personalizadas, que muestran recomendaciones de forma pasiva en lugar de involucrar a los clientes en una conversación. Requiere la configuración de AEP Agent Orchestrator y gobernanza de marca.

### Consideraciones técnicas

- El catálogo de productos debe estar estructurado con datos de atributos enriquecidos, incluidos el tamaño, el material, la compatibilidad, la disponibilidad y los precios, porque Product Advisor Agent basa las recomendaciones en el contenido del catálogo y no puede aconsejar de forma fiable sobre los productos con atributos incompletos.
- La búsqueda de perfiles de clientes en tiempo real mediante RT-CDP debe configurarse con activación de Edge para que el historial de compras, el comportamiento de navegación y los datos del nivel de lealtad sean accesibles durante la conversación en directo sin latencia que interrumpa la experiencia.
- Deben definirse protecciones de gobernanza de marca para especificar cómo gestiona el agente los artículos sin existencias, las comparaciones de productos competitivos, las declaraciones de precios promocionales y los temas prohibidos, lo que garantiza que cada respuesta se ajuste a los estándares de marca minorista.
- Los eventos de conversación, incluidas las señales de intención, las interacciones de productos y la aceptación de recomendaciones, deben capturarse como ExperienceEvents de XDM y transmitirse de nuevo a AEP, lo que enriquece los perfiles de los clientes con los datos de afinidad del producto y mejora la futura personalización en todos los canales.


## Análisis de atribución en canales múltiples

Mida cómo cada punto de contacto de marketing (búsquedas de pago, promociones por correo electrónico, medios sociales y en tienda) contribuye a las conversiones de compras en línea y sin conexión. Los minoristas que dependen de la atribución de último contacto infravaloran sistemáticamente los canales de funnel superior y toman decisiones de asignación de presupuesto basadas en una imagen incompleta de la ruta de compra.

### Impacto empresarial

Los equipos de marketing minorista que pasan de la atribución de último contacto a la de múltiples contactos obtienen una visión más clara de qué canales impulsan la intención de compra, lo que conduce a decisiones de presupuesto mejor informadas y a un rendimiento mejorado del gasto en marketing.

### Cómo implementar

Usar el patrón [Customer Analytics y Insight Generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Este método conecta los datos de eventos en línea y sin conexión (clics en la web, participaciones por correo electrónico, transacciones de fidelidad y registros del punto de venta) con Customer Journey Analytics, donde los modelos de atribución se pueden configurar y comparar en la ruta de compra completa. Este es el patrón correcto cuando el objetivo es la medición y la generación de insight en un recorrido complejo de varios canales, en lugar de activar audiencias o activar mensajes, y cuando el análisis requiere Customer Journey Analytics en lugar de una herramienta CDP o de orquestación de campaña.

### Consideraciones técnicas

- Los datos de transacciones de puntos de venta y comercio electrónico deben compartir un identificador de cliente coherente para que las conversiones en tienda y en línea se puedan vincular en una sola vista multicanal en CJA.
- Los modelos de atribución múltiple (de primer toque, de último toque, lineal y de decadencia de tiempo) deben configurarse en la vista de datos de CJA para que los analistas puedan compararlos en paralelo sin reconstruir el análisis.
- Los datos de impresiones y clics de medios pagados de plataformas de publicidad externas deben ingerirse mediante conectores de origen o cargas por lotes para incluir canales pagados en la ruta de atribución junto con los canales propios.
- Las ventanas de conversión y los periodos retrospectivos de crédito deben definirse por tipo de canal, ya que la ventana de atribución relevante para un clic de búsqueda de pago difiere significativamente de la de una campaña de correo electrónico estacional.

## Segmentación de audiencias y activación para medios de pago

Cree segmentos de audiencia de alto valor a partir de perfiles de clientes unificados y actívelos en destinos de medios de pago como Google Ads, Meta y Trade Desk para campañas de adquisición y retargeting. La unificación de los datos de comportamiento, transaccionales y de lealtad permite un direccionamiento más preciso que reduce el gasto publicitario desperdiciado y mejora la rentabilidad de la inversión en la campaña.

### Impacto empresarial

Los minoristas que activan audiencias de origen de alta calidad ven tasas de coincidencia mejoradas en las plataformas de medios de pago, coste por adquisición reducido y un mayor retorno de la inversión en publicidad en comparación con los segmentos de terceros.

### Cómo implementar

Utilice el patrón [Audience Activation a destinos](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md) para evaluar la pertenencia de la audiencia con perfiles unificados y publicar segmentos en destinos de medios de pago conectados de forma programada o por streaming. Este es el patrón correcto cuando el requisito principal es la publicación de segmentos en sistemas externos, en lugar de la mensajería organizada o la toma de decisiones en tiempo real.

### Consideraciones técnicas

- Se requiere la resolución de identidades en los datos web, móviles y de fidelidad para crear perfiles de cliente completos antes de la activación: los perfiles fragmentados reducen la calidad de la audiencia y las tasas de coincidencia.
- Los conectores de destino deben configurarse para cada plataforma de medios de pago, con indicadores de consentimiento adecuados respetados en el nivel de perfil para evitar que se activen los datos no consentidos.
- La frecuencia de actualización de los segmentos debe alinearse con los objetivos de la campaña: las audiencias de adquisición pueden necesitar actualizaciones diarias, mientras que las audiencias de retargeting se benefician de las actualizaciones casi en tiempo real para excluir a los compradores recientes.
- El análisis de superposición entre audiencias de adquisición y retención ayuda a evitar la contaminación cruzada en la que los clientes existentes reciben mensajes de adquisición de nuevos clientes.


## Supresión de clientes para campañas de adquisición

Elimine los clientes existentes y los convertidores recientes de la adquisición y el gasto mediante la activación de audiencias de exclusión en destinos de medios de pago, lo que reduce el gasto desperdiciado. La sincronización continua de las listas de supresión garantiza que los presupuestos pagados se dirijan a nuevos clientes potenciales netos en lugar de a personas que ya se han convertido o que participan activamente.

### Impacto empresarial

La supresión de los clientes existentes de las campañas de adquisición reduce el gasto en medios pagados desperdiciados, mejora las métricas de coste por adquisición y evita que los clientes existentes reciban mensajes que son irrelevantes en su fase de relación.

### Cómo implementar

Use el patrón [Audience Activation a destinos](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md) para publicar audiencias de exclusión (compradores recientes, suscriptores activos y clientes de alto valor) en cada destino de medios de pago con una programación frecuente. Este es el patrón correcto cuando el objetivo es la publicación de segmentos para su supresión en lugar de orquestar un recorrido orientado al cliente.

### Consideraciones técnicas

- Las audiencias de supresión requieren una definición clara de a quién excluir, normalmente clientes que compraron en los últimos 30-90 días, miembros de fidelidad activos y conversiones de correo electrónico recientes.
- Las listas de exclusión deben actualizarse con la frecuencia suficiente para excluir a los compradores antes de que se publiquen los anuncios; las listas de supresión antiguas causan la mayor fricción de marca en los períodos de venta minorista de gran volumen.
- La calidad de coincidencia de identidad afecta directamente a la precisión de la supresión: la coincidencia deficiente de ID de dispositivo o correo electrónico hará que los clientes existentes sigan viendo anuncios de adquisición.
- Asegúrese de que las audiencias de supresión sean independientes de las audiencias de retención para que las campañas de recuperación puedan llegar a los clientes que hayan caducado y que no se deban suprimir.


## Experiencias web personalizadas para visitantes conocidos

Ofrezca titulares personalizados, recomendaciones de productos y contenido promocional a los visitantes de sitios web autenticados en función de su perfil en tiempo real, pertenencia a segmentos e historial de comportamiento. Cuando los clientes que regresan ven experiencias adaptadas a su estado de lealtad, historial de compras y preferencias, las tasas de participación y la conversión mejoran significativamente en comparación con las experiencias de página principal genéricas.

### Impacto empresarial

Los minoristas que personalizan para visitantes conocidos ven una mejora significativa en las métricas de participación, incluido el tiempo en el sitio, las páginas por sesión y la tasa de conversión, con el mayor impacto entre los miembros fieles que visitan con frecuencia.

### Cómo implementar

Use el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones/web de visitantes conocidos para ofrecer experiencias personalizadas basadas en perfiles al cargar la página mediante la pertenencia a segmentos en tiempo real y atributos de perfil. Este es el patrón correcto cuando la experiencia debe estar impulsada por datos de perfil vinculados a la identidad en lugar de señales de solo sesión y cuando las decisiones de contenido no requieren restricciones comerciales o de clasificación de ofertas complejas.

### Consideraciones técnicas

- La autenticación debe producirse antes de que se pueda activar la personalización basada en perfiles; el sitio web necesita un mecanismo para identificar al visitante y resolver su ECID en un perfil conocido.
- Las búsquedas de perfiles en tiempo real deben completarse dentro del presupuesto de latencia de carga de página, lo que generalmente requiere una evaluación de perfiles implementada en el perímetro en lugar de llamadas de API del lado del servidor en la ruta de procesamiento crítica.
- Las variaciones de contenido deben diseñarse para todos los segmentos de audiencia a los que se van a dirigir, incluida una experiencia predeterminada para los visitantes que no coinciden con ninguna regla de personalización.
- Las decisiones de Personalization deben registrarse para su análisis, lo que permite realizar pruebas A/B de las variaciones de contenido y atribuir mejoras de participación a segmentos específicos.


## Personalization web de visitante anónimo

Personalice el contenido para visitantes de sitios web no identificados mediante señales de comportamiento en la sesión, como páginas vistas, categorías de productos exploradas y fuentes de referencia. Dado que la mayoría del tráfico web minorista es anónimo, la personalización para visitantes no reconocidos amplía significativamente el alcance de la personalización en el sitio más allá del segmento autenticado.

### Impacto empresarial

Los minoristas que ofrecen experiencias personalizadas a visitantes anónimos ven tasas de participación y conversión en la primera visita mejoradas, con un impacto especialmente fuerte en los visitantes que llegan desde fuentes de campañas específicas o exploran páginas de categorías de alta intención.

### Cómo implementar

Use el patrón [Personalization web de visitantes anónimos](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md) para evaluar las señales de comportamiento en la sesión en el perímetro y servir variaciones de contenido relevantes sin requerir autenticación. Este es el patrón correcto cuando la personalización debe funcionar inmediatamente desde la primera interacción sin depender de un perfil persistente, especialmente para el tráfico de adquisición y los visitantes que aún no han iniciado sesión.

### Consideraciones técnicas

- La personalización en sesión se basa en los datos de evento de streaming recopilados mediante Edge Network; las reglas de evaluación de Edge deben implementarse y probarse antes de que se les envíe el tráfico.
- Las variaciones de contenido deben diseñarse en torno a comportamientos de alta señal en la sesión (fuente de referencia, primera página vista, categoría de producto explorada) en lugar de atributos de baja señal que no predicen la intención de forma fiable.
- Los requisitos de privacidad deben evaluarse cuidadosamente; algunas jurisdicciones tratan la personalización del comportamiento como un requisito de consentimiento, incluso para visitantes anónimos.
- Las reglas de Personalization para visitantes anónimos deberían ser más sencillas y rápidas de evaluar que las reglas de visitantes conocidos, ya que las restricciones de latencia de Edge son más estrictas.


## Recorrido de serie de bienvenida

Organice un recorrido de bienvenida de varios pasos para los clientes recién registrados, lo que ofrece contenido de incorporación, educación sobre productos y un incentivo de primera compra en canales push y de correo electrónico. Una serie de bienvenida bien diseñada establece el tono de la relación con el cliente y aumenta significativamente la probabilidad de que un nuevo registrante se convierta en su primera compra.

### Impacto empresarial

Los programas de la serie Welcome impulsan mejoras significativas en las nuevas tasas de activación de clientes y en la conversión de primera compra, con el mayor impacto cuando la serie combina contenido educativo con un incentivo personalizado y oportuno.

### Cómo implementar

Use el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para diseñar una secuencia de incorporación de varios días con pasos de espera, ramificación de canales basada en la participación y supresión cuando se logre el primer objetivo de compra. Este es el patrón correcto cuando el caso de uso requiere un flujo de comunicación secuenciado y espaciado por tiempo con lógica condicional: un solo mensaje activado no es suficiente para guiar a un nuevo cliente a través de la experiencia de incorporación.

### Consideraciones técnicas

- La entrada de recorridos debe activarse mediante eventos de registro de cuenta en tiempo real para que el primer mensaje de bienvenida llegue rápidamente mientras la intención de registro sea alta.
- El recorrido debe incluir condiciones de salida que supriman los mensajes restantes cuando un nuevo cliente complete su primera compra: continuar con la serie de bienvenida después de la compra socava la relevancia del mensaje.
- La preferencia de canal debe respetarse en todo; los pasos de la notificación push requieren la instalación de la aplicación y la inclusión push, con reserva de correo electrónico para los clientes sin inclusión.
- Personalization en la serie de bienvenida mejora la conversión, pero requiere suficientes datos de perfil para que sean significativos; los nuevos perfiles suelen necesitar una alternativa a los productos más vendidos o de tendencias.


## Recuperación de abandono del carro

Déclencheur notificaciones push y por correo electrónico en tiempo real cuando un cliente abandone el carro de compras, con recordatorios de productos personalizados e incentivos limitados en el tiempo para completar la compra. El abandono del carro de compras se encuentra entre los casos de uso con un ROI más alto en el comercio minorista, ya que recupera los ingresos de los clientes que ya han demostrado tener una intención de compra sólida.

### Impacto empresarial

Los programas de abandono del carro de compras bien ejecutados recuperan una parte significativa de los ingresos abandonados, con tasas de recuperación más altas cuando el primer mensaje llega dentro de la hora de abandono e incluye los artículos exactos que quedan en el carro de compras.

### Cómo implementar

Utilice el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para responder al evento de abandono del carro de compras con una comunicación activada inmediata mientras la intención de compra aún está activa. Este es el patrón correcto cuando el déclencheur es una acción del cliente discreta y el requisito principal es una respuesta oportuna y personalizada, en lugar de una secuencia de promoción de varias semanas o una decisión de oferta compleja con restricciones comerciales.

### Consideraciones técnicas

- La detección de abandono del carro de compras requiere un umbral de inactividad definido (normalmente de 30 a 60 minutos) para evitar enviar mensajes a los clientes que aún están explorando o completando de forma activa el flujo de cierre de compra.
- El contenido del correo electrónico debe representar dinámicamente las imágenes del producto, los precios y el estado de inventario actuales en el momento de la entrega, ya que los artículos pueden agotarse o cambiar el precio entre el abandono y la entrega del mensaje.
- La lógica de supresión debe excluir a los clientes que completaron su compra a través de otro canal entre la detección de abandono y el envío de mensajes.
- Las reglas de restricción de frecuencia deben evitar mensajes repetidos de abandono del carro de compras en ventanas cortas, especialmente para los clientes que habitualmente abandonan los carros de compras como comportamiento de navegación.


## Recorrido de participación posterior a la compra

Envíe comunicaciones posteriores a la compra, incluida la confirmación del pedido, las actualizaciones de envío, las recomendaciones de venta cruzada y las solicitudes de revisión a través de un recorrido organizado de varios pasos. La ventana posterior a la compra es uno de los momentos de mayor participación en el ciclo de vida del cliente, lo que la convierte en un momento ideal para generar lealtad e introducir productos complementarios relevantes.

### Impacto empresarial

Los minoristas con recorridos estructurados después de la compra ven tasas de repetición de compras mejoradas y tasas de envío de revisiones de clientes, lo que contribuye a la lealtad a largo plazo y a una  social que respalda la adquisición futura.

### Cómo implementar

Utilice el patrón [Recorrido orquestado en varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para orquestar una secuencia de comunicaciones posteriores a la compra programadas para alcanzar hitos clave: confirmación de pedido, envío, entrega y seguimiento posterior a la entrega. Este es el patrón correcto cuando el caso de uso abarca varios días con varios objetivos: un solo mensaje activado no puede acomodar el arco desde la confirmación transaccional hasta la creación de lealtad para revisar la solicitud.

### Consideraciones técnicas

- La integración del sistema de gestión de pedidos es necesaria para recibir eventos de compra y envío en tiempo real; los retrasos en la ingesta de eventos crean tiempos incómodos en las comunicaciones posteriores a la compra.
- Las recomendaciones de venta cruzada en la secuencia posterior a la compra requieren datos del catálogo de productos en tiempo real e inferencia del modelo de recomendación en el momento del procesamiento del mensaje para reflejar el inventario y los precios actuales.
- Los mensajes de solicitud de revisión deben cumplir con los términos de servicio de la plataforma para las revisiones incentivadas y deben programarse después de que el cliente haya tenido tiempo suficiente para utilizar el producto.
- La coordinación de canales es importante: los clientes no deben recibir correos electrónicos ni mensajes push para el mismo hito a menos que se hayan comprometido con el primer canal.


## Campaña de actualización de nivel de fidelización

Identifique a los clientes que se acercan a los umbrales de nivel de lealtad y publique campañas dirigidas para alentarlos a llegar al siguiente nivel con ofertas personalizadas basadas en el historial de compras y las preferencias. Cuando los clientes están al alcance de una actualización de nivel, la mensajería segmentada con incentivos personalizados crea urgencia e impulsa un comportamiento de compra incremental.

### Impacto empresarial

Las campañas de actualización del nivel de fidelización aumentan el volumen de compra incremental y mejoran la participación en el programa, con el mayor impacto entre los miembros de nivel medio que están cerca del siguiente umbral y que han mostrado una actividad de compra reciente.

### Cómo implementar

Use el patrón [Recorrido orquestado en varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para crear una campaña de proximidad de nivel que entre a los clientes cuando alcancen un umbral de gasto definido por debajo de su siguiente nivel y los guíe a través de una secuencia de mensajes de beneficios y ofertas de incentivos. Este es el patrón correcto cuando el caso de uso requiere monitorizar un atributo de perfil calculado a lo largo del tiempo y organizar una campaña de varios pasos vinculada al progreso del cliente hacia un objetivo.

### Consideraciones técnicas

- Los datos de la plataforma de fidelización (saldo de puntos, estado de nivel, umbrales de nivel) deben introducirse y mantenerse actualizados en el perfil del cliente para que los cálculos de proximidad de nivel sean precisos.
- Las campañas de actualización de nivel deben suprimirse para los clientes que ya han alcanzado el nivel de objetivo o cuyo estado de lealtad ha cambiado desde la entrada de la campaña.
- Los incentivos personalizados en la campaña de actualización deben limitarse a las ofertas para las que el cliente es realmente elegible y que no socavan el valor percibido de la estructura de niveles.
- La campaña debe incluir condiciones de salida claras para los clientes que completen la actualización de su nivel a mitad del recorrido, pivotando hacia un mensaje de felicitación en lugar de continuar con la secuencia de persuasión.


## Orquestación de campañas en canales múltiples

Orqueste campañas de marketing coordinadas en canales web, push, SMS y de correo electrónico con ramificación de recorridos, pasos de espera y límite de frecuencia para maximizar la participación sin fatiga. La orquestación coordinada entre canales garantiza que los clientes reciban una experiencia de campaña coherente independientemente del canal al que respondan primero, lo que elimina los mensajes duplicados y las ofertas en conflicto.

### Impacto empresarial

Los minoristas con funciones de orquestación entre canales ven tasas de participación y conversión de campañas más altas que las de un solo canal, al tiempo que reducen las tasas de cancelación de suscripción impulsadas por la fatiga del canal debido a la mensajería descoordinada.

### Cómo implementar

Utilice el patrón [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para crear campañas que dirijan a los clientes a través de secuencias de canales personalizadas en función de su historial de participación, preferencias de canal y señales de respuesta en tiempo real. Este es el patrón correcto cuando la campaña requiere una selección de ofertas regida, un enrutamiento de preferencias de canal y una ramificación dinámica basada en la participación en el recorrido, en lugar de una secuencia fija enviada a todos los destinatarios de la campaña.

### Consideraciones técnicas

- Los límites de frecuencia globales deben configurarse en todos los canales para evitar que los clientes reciban comunicaciones excesivas cuando se ejecuten simultáneamente varios recorridos.
- Los datos de preferencias de canal deben estar actualizados y ser procesables. Los perfiles de preferencias que estén meses desactualizados enrutarán a los clientes hacia canales con los que ya no interactúan.
- La lógica de orquestación de recorrido debe gestionar la reentrada correctamente, lo que evita que los clientes entren en la misma campaña dos veces y, al mismo tiempo, garantiza que no se excluyan de las campañas realmente nuevas.
- Las señales de participación en tiempo real (aperturas de correo electrónico, clics en vínculos, sesiones web) deben retroceder al recorrido para habilitar el cambio de canal y la salida anticipada para los clientes que ya se han convertido.


## Experiencia de conversación en Brand Concierge

Implemente un agente conversacional con tecnología de IA y seguridad de marca en todas las propiedades digitales para proporcionar orientación personalizada sobre el producto, ayuda para la navegación del sitio y transferencia perfecta a los agentes activos. Un conserje de IA en el sitio amplía el servicio personalizado a escala, ayudando a los compradores a descubrir productos, comparar opciones y completar compras sin requerir la intervención de un agente humano para consultas comunes.

### Impacto empresarial

Los minoristas con capacidades de conserjería de IA informan de tasas de resolución de autoservicio mejoradas, volumen de asistencia entrante reducido para preguntas sobre productos y navegación, y mayor conversión entre los clientes que interactúan con la orientación conversacional antes de realizar la compra.

### Cómo implementar

Utilice el patrón de [Experiencia conversacional de Brand Concierge](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md) para implementar un agente de IA controlado basado en los datos del catálogo de productos, las directrices de marca y el contexto del perfil del cliente en tiempo real. Este es el patrón correcto cuando el caso de uso requiere interacción de lenguaje natural en un conjunto de productos grande y dinámico, en lugar de un bot de chat con scripts e intenciones fijas o un patrón que coincida con un canal específico, como el correo electrónico.

### Consideraciones técnicas

- El agente de IA debe basarse en los datos actuales del catálogo de productos, incluidas las descripciones, especificaciones, disponibilidad y precios, para proporcionar una orientación precisa; los datos de productos antiguos conducen a recomendaciones incorrectas.
- Las protecciones de seguridad de marca deben configurarse para evitar que el agente hable de productos de la competencia, realice compromisos de precios que entren en conflicto con las promociones o responda a consultas fuera de tema.
- La lógica de transferencia a los agentes activos requiere integración con la plataforma de servicio y debe activarse cuando el agente de IA no pueda resolver la consulta del cliente después de un número definido de turnos.
- La integración de datos de perfil permite al agente personalizar las respuestas en función del historial de compras y el estado de lealtad, pero esto requiere la resolución de la identidad antes de que comience la sesión conversacional.
