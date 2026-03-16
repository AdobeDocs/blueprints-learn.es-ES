---
title: Casos de uso minorista
description: Descubra cómo las organizaciones de minoristas utilizan Adobe Experience Platform para personalizar las experiencias de compra, recuperar los carros de compras abandonados e impulsar la lealtad de los clientes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2590'
ht-degree: 0%

---


# Casos de uso minorista

Las organizaciones minoristas utilizan Adobe Experience Platform para unificar los datos de clientes de tiendas en línea, ubicaciones físicas y programas de fidelidad en una sola vista de cada comprador. Esta base permite experiencias de compra personalizadas, un alcance oportuno que recupera los ingresos perdidos y estrategias de lealtad que mantienen a los clientes regresando.

## Recomendaciones de productos personalizadas

Muestre recomendaciones de productos personalizadas en la página de inicio, en las páginas de categoría y en las páginas de detalles del producto, en función del historial de navegación, el historial de compras y un comportamiento similar del cliente. Cuando los compradores ven productos adaptados a sus intereses, pasan más tiempo explorando y es mucho más probable que compren.

### Impacto empresarial

Los minoristas suelen ver un aumento de entre el 20 y el 30 % en las tasas de clics y una mejora de entre el 15 y el 25 % en las tasas de conversión al ofrecer recomendaciones personalizadas en lugar de listas de productos estáticas.

### Cómo implementar

Usar el patrón [Behavioral Recommendations](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Este enfoque utiliza modelos de recomendación impulsados por IA que aprenden continuamente de las interacciones de los clientes para mostrar los productos más relevantes para cada individuo.

### Consideraciones técnicas

- Los datos del catálogo de productos deben ingerirse y mantenerse actualizados, incluidos los atributos de productos, las imágenes, los precios y la disponibilidad, para garantizar que las recomendaciones reflejen lo que los clientes pueden comprar realmente.
- Las señales de comportamiento, como las vistas de productos, los eventos de complementos al carro de compras y las compras, deben fluir en tiempo casi real para que las recomendaciones estén actualizadas en una sola sesión de navegación.
- Los modelos de recomendación requieren una estrategia de inicio en frío para los nuevos visitantes que carecen de historial de navegación, lo que generalmente vuelve a los productos de tendencias o más vendidos.
- El rendimiento de carga de la página debe monitorizarse cuidadosamente, ya que las llamadas de personalización no deben añadir una latencia marcada a la experiencia de compra.


## Recuperación de correo electrónico del carro abandonado

Envíe automáticamente recordatorios por correo electrónico personalizados a los clientes que abandonaron su carro de compras, incluidos los artículos exactos que quedaron y las ofertas relevantes para fomentar la finalización. El abandono del carro de compras es una de las mayores fuentes de pérdida de ingresos en el comercio minorista, y el seguimiento oportuno puede recuperar una parte significativa de esas ventas.

### Impacto empresarial

Los programas efectivos de recuperación del carro de compras ofrecen una tasa de recuperación del carro de compras del 25-35% y pueden generar ingresos mensuales adicionales de entre 100 000 y 500 000 dólares, según el volumen de la tienda.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método responde a un evento de abandono del carro de compras en tiempo real, lo que envía un recordatorio oportuno mientras la intención de compra sigue siendo alta.

### Consideraciones técnicas

- La detección de abandonos del carro de compras requiere la definición de un umbral de inactividad (normalmente, de 30 a 60 minutos) antes de activar el primer recordatorio, lo que evita enviar mensajes a los clientes que aún realizan compras de forma activa.
- El contenido del correo electrónico debe extraer dinámicamente las imágenes del producto, los precios y la disponibilidad actuales del catálogo en el momento de la entrega, ya que los artículos pueden agotarse o cambiar el precio entre el abandono y la entrega.
- Las reglas de restricción de frecuencia deben evitar que los clientes reciban varios correos electrónicos sobre el carro de compras de abandono en un corto período, especialmente si abandonan el carro de compras con frecuencia.
- Las listas de consentimiento y supresión deben comprobarse antes de la entrega, y los clientes que completaron su compra a través de otro canal deben excluirse en tiempo real.


## Campañas de urgencia basadas en inventario

Déclencheur alertas y campañas en tiempo real cuando el inventario de productos es bajo, lo que crea urgencia y fomenta la compra inmediata. Los compradores que ven que solo quedan unos pocos artículos están motivados a actuar rápidamente en lugar de retrasar su decisión.

### Impacto empresarial

Las campañas de baja urgencia de inventario generalmente impulsan un aumento de entre el 30 y el 40 % en la conversión de los productos destacados, a la vez que ayudan a reducir el exceso de existencias al acelerar las ventas de artículos de movimiento lento.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método responde a los eventos de umbral de inventario, activando automáticamente los mensajes de urgencia cuando los niveles de stock caen por debajo de los límites definidos.

### Consideraciones técnicas

- Las fuentes de inventario deben integrarse con la plataforma de datos del cliente en tiempo casi real para que la mensajería de urgencia refleje los niveles de stock reales en lugar de los datos antiguos.
- Los niveles de umbral deben configurarse por categoría de producto, ya que un umbral de &quot;existencias bajas&quot; para una mercancía de gran volumen difiere significativamente de uno para un artículo de lujo.
- La mensajería debe ser veraz y cumplir con las regulaciones de protección al consumidor; mostrar una falsa escasez puede dañar la confianza de la marca y puede violar los estándares de publicidad en ciertos mercados.
- Los canales de mensajería in situ y de correo electrónico deben coordinarse para que un cliente que ya ha adquirido no siga recibiendo notificaciones de urgencia para el mismo producto.


## Recomendaciones de venta cruzada y ampliación de venta

Muestre los productos de venta cruzada y de ampliación de ventas relevantes al cerrar la compra, en correos electrónicos y en páginas de productos basadas en patrones de compra y relaciones de productos. La sugerencia de alternativas complementarias o premium en el momento adecuado aumenta el tamaño de la cesta sin requerir que los clientes busquen artículos relacionados ellos mismos.

### Impacto empresarial

Las estrategias de venta cruzada y aumento de ventas bien ejecutadas aumentan el valor promedio de los pedidos en 25 a 75 dólares y aumentan los ingresos por transacción en un 10 a 15%.

### Cómo implementar

Usar el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Este método emplea una lógica de decisión centralizada que evalúa todas las ofertas disponibles y selecciona la mejor opción de venta cruzada o ampliación de venta para cada cliente y contexto.

### Consideraciones técnicas

- Los datos de relación de productos, incluidas las asociaciones &quot;compradas juntas con frecuencia&quot; y las rutas de actualización, deben mantenerse y actualizarse regularmente para reflejar los patrones de compra actuales.
- La lógica de clasificación de ofertas debe tener en cuenta los niveles de margen, relevancia e inventario para que las opciones más rentables y disponibles aparezcan primero.
- Las recomendaciones de venta cruzada al finalizar la compra deben cargarse rápidamente y no interrumpir el flujo de compra. Las sugerencias lentas o intrusivas pueden reducir la conversión.
- [!DNL Journey Optimizer] reglas de decisión deben incluir ofertas de reserva para que todos los clientes elegibles reciban una recomendación, incluso cuando la opción de mayor clasificación no esté disponible.


## Nueva serie de bienvenida al cliente

Automatice una serie de bienvenida de varios correos electrónicos para nuevos clientes con recomendaciones de productos personalizadas, narración de marcas y ofertas especiales. Las primeras interacciones después de que un cliente se una dan forma a su relación a largo plazo con la marca, lo que convierte a esta serie en uno de los programas de mayor impacto que puede ejecutar un retailer.

### Impacto empresarial

Una serie de bienvenida bien diseñada genera una tasa de participación del 40-50 % entre los nuevos clientes y mejora significativamente el valor de duración al crear afinidad de marca desde el principio.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Este recorrido de nutrición multitáctil guía a los nuevos clientes a través de una secuencia de mensajes de presentación de marca, descubrimiento de productos e incentivos, adaptándose en función de su participación.

### Consideraciones técnicas

- El déclencheur de entrada de recorrido debe capturar de forma fiable los nuevos eventos de creación de clientes desde todas las fuentes de registro, incluidos los mercados web, de aplicaciones móviles, de puntos de venta en tienda y de terceros.
- Los pasos de espera entre correos electrónicos deben configurarse en función de los datos de participación; los clientes que abran y hagan clic pueden recibir el siguiente mensaje antes, mientras que los clientes menos comprometidos se benefician de un mayor espaciado.
- Las recomendaciones de productos dentro de los correos electrónicos de bienvenida deben reflejar lo que el cliente navegó o compró durante su primera visita, no los productos genéricos más vendidos.
- Los clientes que realizan una compra durante la serie de bienvenida deben ramificarse en un flujo posterior a la compra en lugar de seguir recibiendo mensajes centrados en la adquisición.


## Alertas de bajada de precios

Notificar a los clientes por correo electrónico o mediante una notificación push cuando los productos de su lista de deseos o los artículos vistos anteriormente bajen de precio. Los compradores que mostraron interés pero no compraron son muy receptivos a las reducciones de precios, lo que lo convierte en una de las formas más eficientes de convertir la consideración en ventas.

### Impacto empresarial

Las alertas de caída de precios generan una tasa de conversión del 20 al 30 % entre los destinatarios y aumentan de forma mensurable la satisfacción del cliente, ya que ayudan a los compradores a sentir que obtienen el mejor valor.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método responde a los eventos de cambio de precios de los productos, contrastándolos con las señales de interés de los clientes para enviar notificaciones oportunas.

### Consideraciones técnicas

- La detección de cambios de precios requiere comparar los precios actuales con los valores anteriores en la fuente del catálogo de productos y activar solo alertas para reducciones significativas en lugar de fluctuaciones menores.
- Las señales de interés del cliente (adiciones a listas de deseos, vistas de páginas de productos, tiempo invertido en páginas de productos) deben almacenarse y compararse de forma eficaz con posibles miles de cambios diarios de precios.
- Las notificaciones deben incluir el precio original, el nuevo precio y la cantidad de ahorro para comunicar claramente el valor; los mensajes vagos de &quot;precio reducido&quot; no permiten llamadas de ahorro específicas.
- Se pueden usar [!DNL Real-Time Customer Data Platform] segmentos para compradores sensibles al precio para priorizar la entrega de alertas y adaptar el tono de la mensajería.


## Recordatorios de reposición

Envíe recordatorios automatizados a los clientes sobre los productos que compran con regularidad, como artículos de suscripción y consumibles, para animar a que realicen compras más frecuentes antes de que se agoten. Los recordatorios proactivos reducen la posibilidad de que los clientes cambien a un competidor simplemente porque se olvidaron de reordenar.

### Impacto empresarial

Los programas de recordatorio de reposición ofrecen una tasa de repetición de compras del 30-40% y mejoran significativamente la retención de clientes al hacer que sea fácil para los compradores reponer los productos en los que dependen.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Este recorrido programado recurrente utiliza predicciones de frecuencia de compra para enviar recordatorios en el momento óptimo antes de que sea probable que un cliente necesite una recarga.

### Consideraciones técnicas

- El cálculo de la frecuencia de compra debe tener en cuenta las diferentes tasas de consumo entre categorías de productos; un recordatorio para el café debe llegar en una cadencia diferente a la de los suministros de limpieza.
- El recorrido debe ajustar su temporización de forma dinámica cuando un cliente realiza nuevos pedidos antes o después de lo previsto, recalibrando el siguiente recordatorio en función de los datos de compra actualizados.
- Los recordatorios deben incluir un enlace de reorden directo o una opción de recompra con un solo clic para minimizar la fricción y maximizar la conversión a partir de la notificación.
- Los clientes que ya hayan realizado un repedido a través de otro canal (en tienda, servicio de suscripción) deben suprimirse para evitar el envío de recordatorios irrelevantes.


## Páginas de categoría personalizadas

Personalice de forma dinámica las páginas de categorías para mostrar primero los productos más relevantes en función de las preferencias, las compras anteriores y el comportamiento de navegación de cada cliente. Cuando los compradores ven los productos alineados con sus gustos en la parte superior de la página, descubren lo que quieren más rápido y convierten a tasas más altas.

### Impacto empresarial

Las páginas de categoría personalizadas generan un aumento de entre un 25 y un 35 % en la participación en páginas de categoría y mejoran significativamente la detección de productos, especialmente para los minoristas con catálogos grandes.

### Cómo implementar

Usar el patrón [Behavioral Recommendations](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Este método utiliza estrategias de selección y modelos de clasificación para reordenar los productos en páginas de categoría en función del perfil de cada visitante y del comportamiento en tiempo real.

### Consideraciones técnicas

- La clasificación de productos debe ejecutarse con la rapidez suficiente para evitar los retrasos de carga de página percibidos; la personalización del lado del servidor o la toma de decisiones basada en Edge suelen ser necesarias para las páginas de categorías con cientos de productos.
- La lógica de personalización debe combinar las preferencias individuales con las reglas de comercialización, lo que garantiza que los productos promocionados, los recién llegados y los artículos de temporada sigan recibiendo la visibilidad adecuada.
- Debe contarse con una infraestructura de prueba A/B para medir de forma continua el impacto en los ingresos de la clasificación personalizada frente a las reglas de comercialización predeterminadas.
- La implementación de Web SDK de [!DNL Experience Platform] debe capturar las interacciones entre páginas de categorías (profundidad de desplazamiento, clics en productos, uso de filtros) para refinar continuamente los modelos de clasificación.


## Campañas de seguimiento posteriores a la compra

Envíe correos electrónicos posteriores a la compra con consejos de atención del producto, sugerencias de productos relacionados, solicitudes de revisión e información del programa de fidelidad. El periodo inmediatamente posterior a una compra es cuando los clientes están más comprometidos con la marca, lo que la convierte en una ventana ideal para profundizar la relación e impulsar la actividad futura.

### Impacto empresarial

Las campañas efectivas posteriores a la compra aumentan las tasas de envío de revisión en un 15-20 % y generan una tasa de repetición de compras del 10-15 %, lo que convierte a los compradores únicos en clientes leales.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Este flujo posterior a la compra de varios pasos utiliza la lógica de ramificación para adaptar los mensajes de seguimiento en función del tipo de producto, el segmento del cliente y la participación con correos electrónicos anteriores de la serie.

### Consideraciones técnicas

- El recorrido debe tener en cuenta el estado de cumplimiento del pedido; las sugerencias de atención y las solicitudes de revisión solo deben enviarse después de que se haya entregado el producto, no inmediatamente después de la compra.
- El contenido específico del producto (instrucciones de cuidado, guías de uso, sugerencias de accesorios) requiere un sistema de asignación de contenido que asocie cada categoría de producto con materiales de seguimiento relevantes.
- El tiempo de solicitud de revisión debe optimizarse en función de la categoría del producto; los productos electrónicos pueden necesitar un periodo de uso más largo antes de una revisión significativa, mientras que la ropa puede revisarse poco después de la entrega.
- Los clientes que inician una devolución o un intercambio deben eliminarse automáticamente del flujo estándar posterior a la compra y redirigirse a una ruta de recuperación del servicio.


## Ofertas exclusivas para clientes de VIP

Identifique clientes de alto valor y proporcione ofertas exclusivas, acceso anticipado a ventas y experiencias de compra personalizadas que recompensen su lealtad. Retener a los clientes de alto nivel es mucho más rentable que adquirir nuevos clientes, y el tratamiento exclusivo fortalece la conexión emocional que los mantiene gastando.

### Impacto empresarial

Los programas de VIP suelen generar una tasa de participación del 50 % al 70 % entre los clientes de nivel superior y mejoran de forma mensurable el valor de duración del cliente al reducir la pérdida entre los segmentos más rentables.

### Cómo implementar

Usar el patrón [Cross-Channel Recorrido with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Este enfoque combina la orquestación de recorridos con la toma de decisiones en tiempo real para la selección de ofertas, lo que garantiza que cada cliente de VIP reciba la oferta exclusiva más relevante en cada canal.

### Consideraciones técnicas

- Los criterios de segmentación de VIP deben definirse claramente mediante métricas de actualización, frecuencia y valor monetario, y los segmentos deben actualizarse con la frecuencia suficiente para capturar a los clientes que cumplen los requisitos o no cumplen los requisitos recientemente.
- Las ofertas exclusivas deben aplicarse en el momento del canje (web, aplicación, tienda) para evitar que los clientes que no son de VIP accedan a ellas, lo que requiere la integración con sistemas de promoción y precios.
- Las preferencias de canal varían significativamente entre los clientes de alto valor; algunos prefieren el correo electrónico, otros responden a notificaciones de aplicaciones o al correo directo, por lo que el recorrido debe adaptar los canales de entrega en función de la participación anterior.
- La toma de decisiones de [!DNL Journey Optimizer] debe coordinarse entre canales para evitar que un cliente de VIP reciba la misma oferta por correo electrónico, push y SMS simultáneamente.


## Notificaciones de falta de existencias

Permita que los clientes se registren para recibir notificaciones cuando los productos sin existencias estén disponibles y, a continuación, notifíquelos automáticamente por correo electrónico o mensaje de texto. Capturar la demanda de productos no disponibles evita la pérdida de ventas y da a los clientes una razón para regresar a la tienda en lugar de comprar a un competidor.

### Impacto empresarial

Las notificaciones de vuelta en stock logran una tasa de conversión del 40-50% entre los suscriptores y reducen significativamente la pérdida de ventas de productos de alta demanda que experimentan existencias temporales.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método pone en déclencheur las notificaciones de eventos de reserva, comparando las actualizaciones de inventario con los registros de notificaciones de clientes para ofrecer alertas oportunas.

### Consideraciones técnicas

- La monitorización del inventario debe detectar los eventos de reabastecimiento rápidamente; los retrasos de incluso unas pocas horas pueden resultar en que el producto se vuelva a vender antes de que los clientes notificados tengan la oportunidad de comprar.
- Cuando un producto popular vuelve a estar disponible en cantidades limitadas, las notificaciones deben escalonarse o priorizarse por fecha de registro para evitar enviar alertas a más clientes de los que puede entregar el inventario disponible.
- El mecanismo de registro de notificaciones debe capturar la preferencia de canal (correo electrónico o mensaje de texto) y cumplir con los requisitos de inclusión de cada canal, especialmente en el caso de los SMS.
- [!DNL Real-Time Customer Data Platform] atributos de perfil deben rastrear qué productos está viendo cada cliente, de modo que se eviten las notificaciones duplicadas si el mismo producto se reabastece varias veces.


## Personalization de Social Proof

Muestre pruebas sociales personalizadas, incluidas críticas, clasificaciones y sugerencias de &quot;los clientes que compraron esto también compraron&quot;, en función del perfil y las preferencias de cada cliente. Adaptar la prueba social para reflejar las experiencias de clientes similares crea confianza de forma más eficaz que las clasificaciones genéricas por sí solas.

### Impacto empresarial

La prueba social personalizada aumenta las tasas de conversión en un 10-15 % y mejora la confianza de los compradores, especialmente en el caso de los compradores nuevos y los productos con precios más altos, donde las dudas sobre las compras son mayores.

### Cómo implementar

Usar el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones/web de visitantes conocidos. Este método personaliza el contenido web de los visitantes identificados, seleccionando las revisiones más relevantes y los elementos de prueba social en función del perfil del cliente, las preferencias y el contexto de navegación.

### Consideraciones técnicas

- Los datos de revisión y clasificación deben estar estructurados y etiquetados por atributos del cliente (como el contexto de compra, el segmento del cliente y el caso de uso del producto) para permitir un filtrado y una personalización significativos.
- Los elementos de prueba de Social se deben cargar de forma asíncrona para evitar el bloqueo del procesamiento de la página del producto principal, ya que los datos de revisión pueden proceder de una plataforma de revisión de terceros con tiempos de respuesta variables.
- Las regulaciones de privacidad requieren que cualquier dato de cliente utilizado para relacionar las reseñas con los visitantes se gestione de acuerdo con las preferencias de consentimiento; la visualización del contenido &quot;clientes como usted&quot; implica la creación de perfiles que pueden requerir divulgación.
- [!DNL Experience Platform] miembros de la audiencia pueden usarse para seleccionar qué críticas resaltar, mostrando las opiniones de los amantes de las actividades al aire libre de otros compradores en lugar de las críticas genéricas de mejor puntuación.
