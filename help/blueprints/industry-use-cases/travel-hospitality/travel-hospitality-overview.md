---
title: Casos de uso de viajes y hospitalidad
description: Descubra cómo las organizaciones de viajes y hospitalidad utilizan Adobe Experience Platform para personalizar las experiencias de reserva, recuperar las reservas abandonadas y crear lealtad de los huéspedes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: fbdcc015-96a4-4015-93e2-3fc7db375c13
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '3648'
ht-degree: 0%

---

# Casos de uso de viajes y hospitalidad

Las organizaciones de viajes y hospitalidad utilizan Adobe Experience Platform para reunir los datos de los huéspedes de los motores de reservas, los programas de fidelidad, los sistemas de administración de propiedades y los puntos de contacto digitales en una sola vista de cada viajero. Esta base unificada potencia experiencias personalizadas que inspiran reservas, recuperan reservas abandonadas y crean el tipo de lealtad de los huéspedes que impulsa las visitas repetidas.

## Página principal personalizada para nuevos visitantes

Muestre recomendaciones personalizadas sobre cruceros, hoteles y destinos en la página de inicio en función de la ubicación geográfica y el comportamiento de navegación del visitante. Los visitantes nuevos que ven opciones de viaje relevantes de inmediato son mucho más propensos a explorar más y comenzar el proceso de reserva.

### Impacto empresarial

La personalización de la página de inicio para nuevos visitantes mejora las tasas de conversión al presentar opciones de viaje que coinciden con la ubicación y los intereses del visitante, en lugar de contenido genérico.

### Cómo implementar

Usar el patrón [Personalization web de visitante anónimo](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md). Este método ofrece contenido personalizado a los visitantes que aún no se han identificado a sí mismos, mediante señales disponibles como geolocalización, tipo de dispositivo y fuente de referencia para personalizar la experiencia desde la primera página. Este es el patrón correcto cuando el visitante aún no se ha identificado y la personalización debe depender de señales disponibles como geolocalización, tipo de dispositivo y fuente de referencia: la personalización de visitante conocido requiere un perfil autenticado que aún no existe.

### Consideraciones técnicas

- Los datos de geolocalización deben resolverse con precisión en el perímetro de para que sirvan a destinos, divisas y puertos de salida adecuados para la región sin añadir latencia a la carga de la página principal.
- Las reglas de Personalization deben tener en cuenta las tendencias estacionales de los viajes por región, mostrando destinos con clima cálido a visitantes en climas fríos durante los meses de invierno, por ejemplo.
- Las estrategias de contenido de reserva son esenciales para los visitantes cuya ubicación no se puede determinar o que llegan a través de servicios de anonimato.
- La integración con la fuente de disponibilidad del sistema de reservas garantiza que las propiedades e itinerarios destacados se puedan reservar, lo que evita que la frustración promocione las opciones agotadas.


## Recorrido de recuperación de abandono del carro

Detecte automáticamente cuando un cliente abandone su carro de déclencheur y envíe un recorrido de correo electrónico de varios pasos con ofertas personalizadas para fomentar la finalización. Las reservas abandonadas representan una de las mayores fugas de ingresos en viajes y hospitalidad, y el seguimiento oportuno mientras la intención de viaje sigue siendo fresca recupera una parte significativa de esas reservas.

### Impacto empresarial

Los programas efectivos de recuperación de reservas logran tasas significativas de recuperación del carro de compras y pueden generar ingresos incrementales significativos en función del volumen de reserva y el valor promedio del viaje.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método responde a un evento de abandono del carro de compras en tiempo real, lo que envía un recordatorio oportuno mientras la intención de viaje del cliente sigue siendo alta. Este es el patrón correcto cuando el déclencheur es un evento de comportamiento del cliente en tiempo real y la respuesta requerida es un mensaje único y con distinción de tiempo, en lugar de una secuencia de cultivo de varios pasos o una selección de ofertas dinámicas que cambian según la respuesta del cliente.

### Consideraciones técnicas

- Los umbrales de detección de abandono del carro de compras deben tener en cuenta los ciclos de consideración más largos típicos de las compras de viajes; un retraso de 2 a 4 horas antes del primer recordatorio suele ser más apropiado que los 30 a 60 minutos utilizados en el comercio minorista.
- El contenido del correo electrónico debe extraer dinámicamente los precios actuales, la disponibilidad de la habitación o la cabina y las imágenes del sistema de reservas en el momento de la entrega, ya que el inventario de viajes y las tarifas cambian con frecuencia.
- Los incentivos personalizados, como las actualizaciones gratuitas o los créditos de resort, se deben administrar a través de reglas comerciales que tengan en cuenta el margen, la estacionalidad y el nivel de lealtad del cliente.
- La lógica de supresión debe excluir a los clientes que completaron su reserva a través de otro canal, como un centro de llamadas o una agencia de viajes, para evitar mensajes de seguimiento irrelevantes.


## Segmentación de visitantes con intención alta

Identifique a los visitantes con una intención de compra alta mediante una puntuación de tendencia basada en IA y divídalos con ofertas y contenido personalizados. Reconocer qué visitantes tienen más probabilidades de reservar permite a la organización enfocar sus ofertas más atractivas y alcance de ventas en los viajeros que están más cerca de tomar una decisión.

### Impacto empresarial

La segmentación de visitantes con intención alta con ofertas personalizadas mejora la conversión de estos segmentos y concentra la inversión en marketing donde ofrece el mayor rendimiento.

### Cómo implementar

Usar el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones/web de visitantes conocidos. Este método utiliza datos de perfil en tiempo real y señales de comportamiento para personalizar la experiencia web para visitantes identificados, ofreciendo contenido y ofertas adaptados que coinciden con su nivel de preparación para la compra. Este es el patrón correcto cuando la personalización está impulsada por atributos de perfil y puntuaciones de tendencia para clientes identificados en lugar de un modelo de afinidad de comportamiento y cuando el cliente ya se ha autenticado, lo que hace que los miembros de su segmento y las señales de intención estén disponibles.

### Consideraciones técnicas

- Los modelos de tendencia deben recibir formación sobre señales de intención específicas para el viaje, como búsquedas de fechas, vistas de páginas de precios, actividad de comparación de salas y visitas repetidas al mismo destino en un corto periodo de tiempo.
- Las intervenciones de alta intención, como los mensajes de chat en vivo u ofertas de tiempo limitado, deben aparecer en los puntos de decisión naturales en el flujo de reservas en lugar de interrumpir la experiencia de navegación.
- El modelo de puntuación debe distinguir entre la intención de investigación y la intención de reserva, ya que los viajeros suelen investigar meses antes de estar listos para comprar.
- [!DNL Real-Time Customer Data Platform] atributos calculados pueden agregar señales de comportamiento entre sesiones para mantener una puntuación de intención actualizada para cada visitante.


## Campañas de ampliación de venta posterior a la reserva

Una vez que el cliente completa una reserva, déclencheur automáticamente campañas de ampliación de ventas para mejoras de cabina, excursiones a tierra, paquetes de comedor y otros accesorios. El período entre la reserva y el viaje es cuando los huéspedes están más entusiasmados con su próximo viaje y más receptivos a mejorar su experiencia.

### Impacto empresarial

Las campañas de ampliación de ventas posteriores a la reserva aumentan el valor promedio de los pedidos y aumentan los ingresos complementarios, lo que convierte una sola reserva en una transacción significativamente más valiosa.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Este recorrido de varios pasos guía a los clientes que realizaron su reserva a través de una secuencia programada de oportunidades de ampliación de venta, adaptando las ofertas en función de lo que el huésped ya ha comprado y su participación con mensajes anteriores. Este es el patrón correcto cuando el caso de uso requiere un flujo de mensajes múltiples secuenciado a lo largo de los días con ramificación condicional basada en eventos de participación y disponibilidad de inventario: un solo mensaje activado no puede dar cabida a la lógica de dependencia entre momentos de ampliación de venta o ajustes de tiempo basados en la proximidad de la fecha de viaje.

### Consideraciones técnicas

- El recorrido debe integrarse con el sistema de reservas para saber exactamente qué ha reservado el huésped, qué actualizaciones están disponibles para su itinerario específico y los precios actuales para cada opción auxiliar.
- El horario de las ventas adicionales debe escalonarse estratégicamente; las mejoras de la cabina pueden ofrecerse poco después de la reserva, mientras que las excursiones y los paquetes de comedor funcionan mejor a medida que se acerca la fecha del viaje.
- El inventario y la disponibilidad de los productos auxiliares deben comprobarse en el momento de la presentación de la oferta, ya que la capacidad de excursión y la disponibilidad de la actualización cambian continuamente.
- La personalización de [!DNL Journey Optimizer] debe tener en cuenta la cantidad de viajeros en la reserva y recomendar excursiones apropiadas para la familia para reservas familiares y experiencias orientadas a parejas para reservas de dos personas.


## Campañas de recuperación para clientes caducados

Identifique a los clientes que no hayan reservado en doce o más meses y ocúpese de ellos con ofertas y contenido personalizados de recuperación en función de sus preferencias de viaje anteriores. Volver a atraer a los huéspedes caducados es significativamente más rentable que adquirir clientes completamente nuevos, y los viajeros anteriores ya tienen una familiaridad de marca que reduce la barrera para volver a reservar.

### Impacto empresarial

Las campañas de recuperación bien dirigidas logran tasas de reactivación significativas entre los clientes caducados, recuperando los ingresos de los huéspedes que, de lo contrario, nunca regresarían.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Este recorrido de varios pasos vuelve a atraer a los clientes caducados con una serie progresiva de mensajes que evolucionan desde la inspiración hasta los incentivos en función de la respuesta del cliente. Este es el patrón correcto cuando no hay ningún evento de activación discreto y el tiempo debe calcularse a partir de los modelos de ciclo de vida del cliente y los patrones de reserva estacionales: los mensajes activados por evento no pueden manejar la lógica de escalación progresiva o la necesidad de programar ofertas en ventanas típicas de planificación de viajes.

### Consideraciones técnicas

- La segmentación de clientes caducada debe tener en cuenta la frecuencia típica de reserva en la categoría de viajes; un cliente que reserve anualmente no debe marcarse como caducado después de solo seis meses de inactividad.
- El contenido de recuperación debe hacer referencia a las preferencias de viaje anteriores del cliente, como destinos preferidos, tipos de cabina o temporadas de viaje, para demostrar que la marca los recuerda y los valora.
- Las ofertas deberían escalar a lo largo del recorrido, empezando por contenido inspirador y avanzando hacia incentivos monetarios solo si los mensajes anteriores no generan participación.
- Los registros del cliente deben comprobarse con el sistema de reservas para cualquier reserva realizada a través de canales sin conexión, como agencias de viajes o centros de llamadas, a fin de evitar enviar mensajes de recuperación a los clientes que están realmente activos.


## Recomendaciones de itinerarios dinámicos

Muestre itinerarios de crucero y destinos personalizados en función de las reservas anteriores del cliente, el historial de navegación y las preferencias establecidas. Cuando los viajeros ven itinerarios adaptados a sus intereses y estilo de viaje, se relacionan más profundamente con la experiencia de planificación y avanzan hacia la reserva más rápidamente.

### Impacto empresarial

Las recomendaciones de itinerarios personalizadas mejoran la participación con las páginas de itinerarios, lo que ayuda a los clientes a encontrar el viaje correcto más rápido y reduce el tiempo de entrega que se produce cuando los viajeros se sienten abrumados por demasiadas opciones.

### Cómo implementar

Usar el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones/web de visitantes conocidos. Este enfoque personaliza el contenido del sitio web para visitantes identificados, utilizando los datos de perfil y el historial de comportamiento para mostrar los itinerarios y destinos más relevantes. Este es el patrón correcto cuando la personalización está impulsada por atributos de perfil e historial de reservas en lugar de un modelo de afinidad de comportamiento, lo que permite que la lógica basada en reglas tenga en cuenta la logística de viajes, como los puertos y las fechas de salida, junto con las preferencias de los clientes.

### Consideraciones técnicas

- La lógica de recomendación de itinerarios debe incorporar fechas de navegación o estancia, puertos de salida y preferencias de duración junto con el interés de destino para presentar opciones que sean atractivas y prácticas para el cliente.
- La integración con el sistema central de reservas garantiza que los itinerarios recomendados tengan inventario disponible y reflejen los precios actuales, lo que evita la frustración de promocionar viajes agotados o propiedades totalmente reservadas.
- Los factores estacionales deberían influir mucho en las recomendaciones; los clientes que reservaron cruceros mediterráneos de verano deberían ver opciones de temporada similares en lugar de alternativas fuera de temporada.
- [!DNL Experience Platform]: las políticas de combinación de perfiles deben unificar correctamente el comportamiento de navegación desde varios dispositivos, de modo que la investigación realizada en dispositivos móviles se refleje en las recomendaciones de escritorio.


## Productos consultados recientemente en la página principal

Muestre los cruceros, hoteles o destinos vistos recientemente en la página de inicio para recordar a los visitantes su interés y animar a las visitas de retorno. Los viajeros a menudo investigan en varias sesiones antes de reservar, y mostrar sus intereses anteriores elimina la fricción de iniciar su búsqueda cada vez que regresan.

### Impacto empresarial

Al mostrar los productos de viajes consultados recientemente en la página principal, aumenta la participación en las visitas de retorno, lo que ayuda a los clientes a recoger lo que han dejado y acorta el camino hacia la reserva.

### Cómo implementar

Usar el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones/web de visitantes conocidos. Este método utiliza los datos de perfil almacenados del visitante para representar los elementos visualizados anteriormente en la página principal, lo que crea continuidad entre las sesiones de navegación. Este es el patrón correcto cuando la personalización se basa en datos de perfil persistentes entre sesiones y dispositivos, en lugar de en la afinidad de comportamiento en tiempo real, y cuando las reglas para la relevancia se basan en el tiempo (actualización) en lugar de en la clasificación algorítmica.

### Consideraciones técnicas

- Los datos vistos recientemente deben persistir entre dispositivos y sesiones mediante la resolución de identidad, de modo que un cliente que navega por teléfono vea los mismos elementos cuando regresa en un equipo de escritorio.
- Los artículos mostrados deben mostrar el precio actual y el estado de disponibilidad, con indicadores claros si una opción vista anteriormente ya no está disponible o si el precio ha cambiado desde la última visita.
- La ventana de actualización para los artículos mostrados debe ajustarse a los ciclos de reserva de viajes; mostrar un crucero visto hace tres meses puede seguir siendo relevante, a diferencia de un producto minorista visto hace mucho tiempo.
- Las consideraciones de privacidad requieren que el contenido visualizado recientemente esté vinculado al estado de consentimiento del cliente, y que se pueda acceder fácilmente a una opción para borrar el historial de navegación.


## Salir del modo por intención con ofertas segmentadas

Cuando un visitante muestra el intento de salida, muestra un modal personalizado con ofertas relevantes en función de su comportamiento de navegación durante la sesión. Atrapar a un visitante que sale con una oferta atractiva y relevante para el contexto proporciona una oportunidad final para convertir el interés en una reserva antes de que se vaya.

### Impacto empresarial

Los modelos de intención de salida con ofertas de viajes personalizadas recuperan conversiones significativas entre visitantes que, de lo contrario, se irían sin reservar, capturando ingresos que se perderían por completo.

### Cómo implementar

Usar el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Este método utiliza la lógica de decisión centralizada para evaluar todas las ofertas disponibles y seleccionar la más relevante para el visitante que sale en función del comportamiento de su sesión y los datos de perfil. Este es el patrón correcto cuando la selección de ofertas debe tener en cuenta la idoneidad del nivel de lealtad y las restricciones empresariales en torno a la restricción de frecuencia: restricciones que requieren una lógica de toma de decisiones regida en lugar de una recomendación de comportamiento simple o un mensaje activado único.

### Consideraciones técnicas

- La detección de intención de salida en los sitios de reservas de viajes debe tener en cuenta el comportamiento de navegación con varias pestañas, ya que los viajeros suelen abrir varios itinerarios o propiedades en pestañas independientes sin tener la intención de salir.
- La selección de ofertas debe reflejar lo que el visitante navegó durante su sesión, con un descuento en el destino o la propiedad específicos que exploró en lugar de una promoción genérica.
- La frecuencia modal debe limitarse estrictamente para evitar que los visitantes vean la misma oferta en cada visita, lo que erosiona la urgencia y la exclusividad percibida de la promoción.
- Las reglas de elegibilidad de ofertas de [!DNL Journey Optimizer] deben considerar el nivel de lealtad del visitante y el historial de reservas para presentar incentivos debidamente valorados, ofreciendo a los huéspedes premium beneficios significativos en lugar de pequeños descuentos.


## Personalization del programa de fidelización

Personalice la experiencia del sitio web, las ofertas y las comunicaciones en función del nivel de lealtad del cliente, el saldo de puntos y el historial de participación. Los miembros fieles que ven su estado reflejado en cada punto de contacto se sienten reconocidos y valorados, lo que refuerza su compromiso con la marca y fomenta el avance del nivel.

### Impacto empresarial

La personalización basada en niveles impulsa una participación mejorada de los miembros fieles, lo que profundiza la relación y acelera los comportamientos de ingresos y canje que mantienen los ingresos a largo plazo.

### Cómo implementar

Usar el patrón [Cross-Channel Recorrido with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Este método combina la orquestación de recorridos con la toma de decisiones en tiempo real para ofrecer la oferta correcta a través del canal adecuado para cada miembro socio, adaptándose a su nivel, preferencias y actividad reciente. Este es el patrón correcto cuando el recorrido debe coordinar la entrega a través de los canales para evitar ofertas duplicadas y cuando la selección de ofertas requiere reglas de elegibilidad basadas en niveles y restricciones de canje: la orquestación de recorridos por sí sola no proporciona el nivel de toma de decisiones multicanal necesario.

### Consideraciones técnicas

- Los datos del programa de fidelización, incluido el estado de la capa, los saldos de puntos y el historial de ganancias, deben introducirse y mantenerse actualizados para garantizar que la personalización y las ofertas del sitio web reflejen la posición real del cliente.
- Las ventajas específicas de nivel, como el acceso anticipado a las reservas, las actualizaciones gratuitas y los precios exclusivos, deben aplicarse en el momento del canje, lo que requiere una integración estrecha con los sistemas de reservas y precios.
- Los cambios en el saldo de puntos de las reservas, las estancias y las transacciones con socios deberían suponer un déclencheur para volver a calcular las reglas de personalización en tiempo casi real, de modo que un cliente que acaba de obtener suficientes puntos por una recompensa vea inmediatamente esa opción.
- Las audiencias de [!DNL Real-Time Customer Data Platform] deben estructurarse en torno a niveles de lealtad e hitos de participación clave como aproximarse al siguiente nivel o correr el riesgo de disminuir de nivel.


## Recordatorios de reserva multicanal

Envíe recordatorios de reserva personalizados por correo electrónico, mensajes de texto y notificaciones push a los clientes que hayan iniciado pero no hayan completado sus reservas. Los viajeros suelen comenzar el proceso de reserva y son interrumpidos, y llegar a ellos a través de sus canales preferidos con un recordatorio y los detalles guardados del viaje les lleva de vuelta a completar la reserva.

### Impacto empresarial

Los recordatorios de reservas multicanal mejoran las tasas de finalización de las reservas, recuperando ingresos significativos de los clientes que tenían la intención de reservar, pero que fueron desviados antes de finalizar.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método déclencheur automáticamente los recordatorios cuando se detecta un evento de reserva incompleto y envía mensajes puntuales a través de los canales preferidos del cliente. Este es el patrón correcto cuando el déclencheur es una acción del cliente discreta (iniciar una reserva) y la respuesta necesaria es una entrega con distinción de tiempo en todos los canales preferidos, en lugar de una secuencia de varios pasos en la que cada mensaje depende de la participación previa o de los cambios de disponibilidad.

### Consideraciones técnicas

- La lógica de selección de canales debe respetar las preferencias de comunicación de los clientes y optimizar la entrega en función de patrones de participación anteriores, enviando notificaciones push a los clientes que responden bien al móvil y al correo electrónico a quienes lo prefieren.
- El contenido del recordatorio debe incluir un vínculo profundo que devuelva al cliente directamente a su reserva guardada con todas las selecciones intactas, lo que elimina la fricción de volver a introducir las fechas de viaje, las preferencias de habitación y los detalles del huésped.
- Las reglas de tiempo y frecuencia deben coordinarse entre los canales para evitar saturar al cliente; un correo electrónico y una notificación push sobre la misma reserva deben espaciarse correctamente en lugar de enviarse simultáneamente.
- La integración con la administración de la propiedad o el sistema de reserva central debe verificar que el tipo de habitación, la tarifa y las fechas seleccionadas originalmente siguen estando disponibles antes de enviar el recordatorio, actualizando el mensaje si la disponibilidad ha cambiado.


## Personalization de campaña estacional

Personalice campañas y ofertas en función de las preferencias de temporada, las reservas de temporada anteriores y las tendencias de temporada actuales. Los viajeros se ven muy influidos por las temporadas, y las campañas que se alinean con sus intereses de temporada demostrados y las tendencias actuales de viaje son mucho más convincentes que las promociones genéricas.

### Impacto empresarial

Las campañas personalizadas de temporada aumentan la conversión de reservas estacionales, lo que garantiza que la inversión en marketing se concentre en los destinos y los productos de viaje que tienen más probabilidades de interesar a cada cliente.

### Cómo implementar

Usar el patrón [Activación de mensaje saliente por lotes](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). Este método permite enviar mensajes personalizados de campañas de temporada a grandes audiencias de forma programada, segmentando a los clientes según sus patrones y preferencias de viajes estacionales. Este es el patrón correcto cuando la audiencia es grande y está predefinida por el historial de reservas estacionales, el tiempo de entrega se programa en función de los períodos de planificación estacional en lugar de basarse en el evento, y no se requiere bifurcación ni toma de decisiones en tiempo real.

### Consideraciones técnicas

- Los perfiles de preferencias estacionales de los clientes deben crearse a partir de los datos históricos de reservas, identificando patrones como vacaciones de playa de verano consistentes o viajes de esquí de invierno para informar la segmentación de la campaña.
- La programación de campañas debe tener en cuenta los plazos de ejecución de la industria de viajes; las campañas de vacaciones de verano deben iniciarse a principios de primavera cuando las familias están planificando, no en junio, cuando la mayoría de las reservas ya están hechas.
- Las tarifas de precios y disponibilidad para el inventario estacional deben estar integradas para que las ofertas promocionadas reflejen las tarifas en tiempo real y la disponibilidad real de la habitación o cabina durante los períodos de viaje destacados.
- Las audiencias de [!DNL Experience Platform] deben combinar los datos de preferencias de temporada con los indicadores de actualización para priorizar a los clientes que se encuentran en su ventana de planificación típica para la próxima temporada.


## Recomendaciones de reserva de grupo

Identifique a los clientes que reservan con frecuencia viajes de grupo y recomienden proactivamente paquetes de grupo, opciones familiares o reservas de varias habitaciones. Las reservas de grupo representan ingresos significativamente mayores por transacción, y los clientes con un patrón demostrado de viajes de grupo responden bien a las opciones depuradas que simplifican el proceso de planificación.

### Impacto empresarial

Las recomendaciones proactivas de reservas de grupo aumentan el valor promedio de pedido por reserva, capturando el valor completo de las transacciones de viajes de grupo que de otra manera podrían dividirse en varias reservas individuales.

### Cómo implementar

Usar el patrón [Behavioral Recommendations](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Este enfoque utiliza modelos impulsados por IA que aprenden de los patrones y el comportamiento de las reservas de los clientes para recomendar las opciones de viaje en grupo más relevantes para cada cliente. Este es el patrón correcto cuando el conjunto de artículos es grande y cambia continuamente (los paquetes de grupos evolucionan con los precios y la disponibilidad) y la selección se basa en patrones de comportamiento del historial de reservas de grupos en lugar de un conjunto limitado de ofertas gobernadas por reglas de elegibilidad.

### Consideraciones técnicas

- La identificación de viajes grupales requiere analizar el historial de reservas para patrones como reservas de varias habitaciones, reservas con varios pasajeros y reservas coordinadas realizadas en estrecha colaboración para las mismas fechas y destinos.
- Los precios de los paquetes grupales se deben extraer del sistema de reservas de forma dinámica, ya que las tarifas grupales a menudo difieren de las tarifas individuales y pueden requerir tamaños mínimos de partes o ventanas de reservas por adelantado.
- El contenido de la recomendación debe abordar las necesidades únicas de los organizadores del grupo, incluida la información sobre opciones de restaurantes para grupos, espacios de reunión, descuentos de reserva de bloques y disponibilidad de excursiones para grupos.
- El enriquecimiento del perfil [!DNL Real-Time Customer Data Platform] debe marcar a los clientes como organizadores de viajes grupales según sus patrones de reserva, lo que permite campañas dirigidas durante períodos de planificación de grupos pico, como la temporada de reuniones familiares o períodos de retiro corporativos.


## AI Booking Concierge

Las organizaciones de viajes y hospitalidad ofrecen recorridos de compra complejos y de alta consideración en los que los huéspedes deben navegar por vuelos, habitaciones, categorías de habitaciones, servicios auxiliares y beneficios de fidelidad antes de comprometerse con una reserva. Las interfaces estáticas de exploración y filtrado crean fatiga de decisión y aumentan la capacidad de entrega. Un conserje de reservas de IA involucra a los huéspedes en una conversación natural para comprender su intención de viaje, tamaño de la fiesta, preferencias y presupuesto, y luego los guía paso a paso a través de la planificación del itinerario, la selección del alojamiento y las opciones de complementos, todo mientras muestra los beneficios de lealtad relevantes para el nivel del huésped.

### Impacto empresarial

La guía de reserva conversacional mejora las tasas de finalización del itinerario y el apego auxiliar, al tiempo que reduce el volumen del centro de llamadas para los huéspedes que, de lo contrario, llamarían por teléfono para aclarar opciones.

### Cómo implementar

Usar el patrón [Experiencia de conversación en Brand Concierge](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md). Este método implementa Product Advisor Agent con el catálogo de propiedades e itinerarios, utilizando AEP Agent Orchestrator y datos de perfil del cliente en tiempo real para mostrar opciones personalizadas y recomendaciones relevantes para la lealtad a través del diálogo guiado de varias vueltas. Este es el patrón correcto cuando el objetivo es un descubrimiento conversacional interactivo y de varias vueltas que se construye hacia una decisión de reserva compleja, distinta de la mensajería activada por evento, que reacciona a las acciones discretas del viajero con un alcance unidireccional, y de las experiencias web personalizadas, que muestran recomendaciones pasivamente sin involucrar al huésped en el diálogo. Requiere la configuración de AEP Agent Orchestrator y gobernanza de marca.

### Consideraciones técnicas

- Los datos de disponibilidad y tarifa deben mantenerse actualizados mediante la integración casi en tiempo real entre el sistema de reservas y la capa de contenido de Brand Concierge, ya que recomendar tipos de habitaciones no disponibles o precios incorrectos dentro de una conversación erosiona la confianza inmediatamente.
- La búsqueda del perfil del cliente en tiempo real debe mostrar el nivel de lealtad, el historial de estancia y las preferencias declaradas para que el agente pueda reconocer de forma proactiva el estado del huésped y adaptar las recomendaciones sin que este tenga que volver a explicar sus preferencias en cada visita.
- El control de marca debe definir cómo gestiona el agente las consultas de coincidencia de tarifas, las referencias de la competencia y las situaciones en las que las fechas preferidas del invitado o el tipo de habitación no están disponibles, lo que garantiza que el agente responda correctamente dentro de la voz de la marca en lugar de presentar un callejón sin salida.
- Las señales de intención de conversación, incluidos el interés de destino, la composición de la parte de viaje y las preferencias auxiliares expresadas durante el diálogo, deben volver a AEP como datos de ExperienceEvent, lo que enriquece los perfiles de los invitados para informar las campañas de correo electrónico descendente, lealtad y renovación de la participación.
