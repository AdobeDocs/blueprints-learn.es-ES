---
title: Casos de uso automotriz
description: Descubra cómo las organizaciones automovilísticas utilizan Adobe Experience Platform para personalizar el recorrido de compra de vehículos, mejorar la retención del servicio y crear lealtad del propietario.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: ee83c739-0907-481d-ba3f-358af4e03c67
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 4%

---

# Casos de uso de automoción

Las organizaciones automovilísticas utilizan Adobe Experience Platform para unificar los datos de clientes procedentes de las interacciones con los concesionarios, la investigación en línea de vehículos, los registros de servicio y los sistemas de automóviles conectados en una sola vista de cada propietario. Esta base permite experiencias personalizadas a lo largo de todo el ciclo de vida de la propiedad, desde la investigación inicial del vehículo hasta la compra, el servicio y la lealtad.

## Resumen de casos de uso

| Ejemplo de uso | Descripción | Impacto empresarial | Patrón de implementación |
| --- | --- | --- | --- |
| [Recorrido de compra de vehículo Personalization](#vehicle-purchase-journey-personalization) | Personalice el recorrido de compra de vehículos desde la investigación hasta la compra con las recomendaciones relevantes sobre vehículos, opciones de financiamiento e información sobre distribuidores. Cuando los compradores potenciales reciben una orientación personalizada en cada fase, pasan por el funnel de ventas con mayor rapidez y confianza. | Tasas de conversión de clientes potenciales a compras mejoradas y una canalización de ventas más sólida | [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |
| [Recordatorios de cita de servicio](#service-appointment-reminders) | Envíe recordatorios de servicio personalizados en función del kilometraje del vehículo, el historial de servicio y las preferencias del cliente. El alcance proactivo mantiene los vehículos mantenidos y garantiza que los clientes regresen al concesionario en lugar de buscar proveedores externos. | Se han mejorado las tasas de espectáculo de las citas de servicio y los ingresos por servicios | [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| [Campañas de valor de intercambio](#trade-in-value-campaigns) | Ofrezca de forma proactiva evaluaciones de valor de intercambio a los clientes que puedan estar listos para la actualización. Llegar a los propietarios en el punto correcto de su ciclo de propiedad acelera el camino hacia una nueva compra de vehículo. | Mejora de la participación en el intercambio y aumento de las ventas de vehículos nuevos | [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| [Recomendaciones de piezas y accesorios](#parts-and-accessories-recommendations) | Recomendar piezas, accesorios y actualizaciones relevantes en función del modelo del vehículo, la duración de la propiedad y las preferencias del cliente. Las recomendaciones personalizadas de posventa generan ingresos incrementales a la vez que ayudan a los propietarios a obtener más de su vehículo. | Se mejoraron las tasas de compra de piezas y accesorios y se incrementaron los ingresos del mercado de accesorios | [Recomendación de comportamiento](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| [Notificaciones de retirada de vehículo](#vehicle-recall-notifications) | Envíe notificaciones de retirada personalizadas con opciones de programación de servicios e información de seguridad. Las comunicaciones de recordatorio claras y oportunas protegen la seguridad del cliente y demuestran el compromiso de la marca con el soporte de propiedad responsable. | Mejoras en las tasas de respuesta a recordatorios y mayor cumplimiento de la seguridad | [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| [Campañas de lanzamiento de modelos nuevos](#new-model-launch-campaigns) | Segmente a los clientes que puedan estar interesados en lanzamientos de nuevos modelos en función de su vehículo actual, preferencias e historial de compras. La segmentación de audiencias específica maximiza el impacto del lanzamiento y genera un impulso de pedidos anticipado. | Se ha mejorado la participación en la campaña de lanzamiento y ha aumentado el interés por los nuevos modelos | [Activación de mensaje saliente por lotes](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) |
| [Ofertas de financiación y seguros](#financing-and-insurance-offers) | Presente ofertas personalizadas de financiación y seguros basadas en el perfil de crédito, la selección de vehículos y la cronología de compra. Los productos financieros personalizados eliminan las barreras a la compra y ayudan a los clientes a sentirse seguros en sus términos. | Mejora de las tasas de aceptación de financiación y aumento de los ingresos por venta | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| [Programación de unidades de prueba](#test-drive-scheduling) | Habilite la programación personalizada de pruebas de conducción con las recomendaciones del concesionario y la disponibilidad del vehículo. Hacer que sea fácil para los compradores interesados ponerse al volante acelera el camino a la compra. | Se mejoraron las tasas de finalización de las pruebas y se reforzó la conversión de ventas | [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| [Programas de fidelización de propietarios](#owner-loyalty-programs) | Coordine las comunicaciones de lealtad entre los canales de automóviles conectados, digitales y de concesionario OEM, aplicando reglas de elegibilidad basadas en niveles para gobernar qué propietarios reciben ofertas exclusivas, acceso anticipado al vehículo y recompensas de socios. La mediación de ofertas evita que las promociones conflictivas de los canales de distribuidor y OEM lleguen al mismo propietario simultáneamente. | Mejora de la participación en el programa de fidelización y aumento de las compras repetidas | [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |
| [Planes de garantía y servicio ampliado](#warranty-and-extended-service-plans) | Recomendar planes de garantía y servicio extendido en momentos óptimos en función de la edad del vehículo, el kilometraje y los patrones de compra. La asistencia oportuna captura los ingresos antes de que caduquen las garantías de la fábrica. | Mejoras en las tasas de adopción de garantías ampliadas y mayores ingresos por servicios | [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| [Activación de característica de coche conectado](#connected-car-feature-activation) | Personalice las recomendaciones de funciones de coche conectado en función de las capacidades del vehículo y las preferencias tecnológicas. Ayudar a los propietarios a descubrir características no utilizadas aumenta la satisfacción y fortalece la relación digital. | Tasas de activación de funciones mejoradas y mejor experiencia del cliente | [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| [Coordinación de la red del concesionario](#dealer-network-coordination) | Habilite recomendaciones personalizadas para distribuidores basadas en la ubicación del cliente, las preferencias y el inventario de distribuidores. La conexión de los clientes con el concesionario adecuado mejora la experiencia de compra y servicio. | Tasas de participación del distribuidor mejoradas y una coordinación de ventas más sólida | [Personalization de aplicación/web de visitante conocido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

## Consideraciones técnicas por caso de uso

### Personalización del recorrido de compra de vehículo

- Los datos de inventario de vehículos procedentes de los sistemas de gestión de concesionarios deben integrarse y actualizarse con frecuencia para que las recomendaciones reflejen la disponibilidad real en los concesionarios cercanos.
- Se debe capturar el comportamiento de la investigación del cliente en todo el sitio web, incluida la actividad de configuración del vehículo, el uso de la herramienta de comparación y las descargas de folletos, para identificar con precisión las señales de intención de compra.
- Los modelos de puntuación de posibles clientes deben tener en cuenta tanto la participación en línea como las señales sin conexión, como las visitas al concesionario y las consultas telefónicas, para priorizar las perspectivas con mayores intenciones.
- Los perfiles de [!DNL Real-Time Customer Data Platform] deben combinar sesiones de investigación web anónimas con identidades de clientes conocidas cuando un cliente potencial se registra o visita un concesionario.

### Recordatorios de citas de servicio

- Los datos telemáticos y de kilometraje del vehículo procedentes de los sistemas de vehículo conectados o de los registros de servicio del concesionario deben fluir a los perfiles de los clientes para enviar recordatorios de déclencheur a los intervalos de servicio correctos.
- Los mensajes de recordatorio deben incluir vínculos de programación de un clic que rellenen previamente la información del vehículo del cliente y los artículos de servicio recomendados para minimizar la fricción en la reserva.
- Los registros del historial de servicios deben integrarse para evitar recomendar servicios completados recientemente y personalizar el recordatorio con los elementos de mantenimiento específicos pendientes.
- La sincronización de mensajes de [!DNL Journey Optimizer] debe tener en cuenta la capacidad de servicio del concesionario y las horas de operación para garantizar que los clientes puedan reservar citas cuando reciban el recordatorio.

### Campañas de valor de intercambio

- Los datos de valoración de vehículos de proveedores externos deben integrarse y actualizarse regularmente para garantizar que las estimaciones de intercambio compartidas con los clientes sean precisas y competitivas.
- Los modelos de ciclo vital de propiedad deben tener en cuenta factores como las fechas de caducidad del arrendamiento, los plazos de pago de los préstamos y la duración promedio de propiedad por segmento de vehículo para identificar la ventana de alcance óptima.
- La mensajería de campaña debe hacer referencia de forma dinámica al vehículo actual del cliente y sugerir opciones de actualización específicas que se ajusten a sus preferencias y presupuesto.
- Los segmentos de [!DNL Experience Platform] deben excluir a los clientes que compraron recientemente un vehículo o que están actualmente en una disputa de servicio activa para evitar una divulgación mal programada.

### Recomendaciones de piezas y accesorios

- Los datos del catálogo de productos deben incluir información sobre la compatibilidad del vehículo de modo que las recomendaciones solo muestren piezas y accesorios que se ajusten al año, la marca y el modelo del vehículo específico del cliente.
- Los factores estacionales y regionales deberían influir en las recomendaciones; los accesorios de invierno deberían promoverse en climas más fríos, mientras que las mejoras en el rendimiento podrían resonar más en regiones con comunidades de entusiastas activos.
- El comportamiento de navegación en las páginas de piezas y accesorios debe capturarse y asociarse con los perfiles de los clientes para refinar las recomendaciones en función del interés expresado.
- La implementación de Web SDK [!DNL Experience Platform] debe capturar los datos del número de identificación del vehículo de las sesiones autenticadas para garantizar que el filtrado de compatibilidad sea preciso.

### Notificaciones de retirada de vehículo

- Los registros del número de identificación del vehículo deben mantenerse con precisión en los perfiles de los clientes para que las notificaciones de retirada lleguen a todos los propietarios afectados y no vayan a clientes no afectados.
- La mensajería de recuperación debe cumplir con los requisitos regulatorios para el contenido de las notificaciones de seguridad, el tiempo y la confirmación de entrega en cada mercado aplicable.
- La entrega multicanal (correo electrónico, mensaje de texto, notificaciones push y correo físico) debe utilizarse para maximizar el alcance, ya que las comunicaciones esenciales para la seguridad requieren una mayor garantía de entrega que los mensajes de marketing.
- [!DNL Journey Optimizer] debe rastrear el estado de respuesta de recuperación en el nivel individual y escalar las comunicaciones de seguimiento para los propietarios que no hayan programado el servicio dentro de un intervalo de tiempo definido.

### Campañas de lanzamiento de nuevos modelos

- Los segmentos de audiencia de las campañas de lanzamiento deben tener en cuenta el modelo de vehículo actual, la duración de la propiedad, las señales de interés del modelo anterior y el ajuste demográfico para identificar las perspectivas de mayor tendencia.
- El contenido de Launch debe personalizarse para hacer referencia al vehículo actual del cliente y resaltar mejoras o funciones específicas que aborden sus probables prioridades.
- El tiempo de campaña debe coordinarse con las fechas de embargo y los horarios de lanzamiento regionales para garantizar que los clientes reciban la información en el momento adecuado para su mercado.
- La activación de audiencia [!DNL Real-Time Customer Data Platform] debe sincronizar los segmentos de inicio con las plataformas de publicidad para obtener soporte de medios de pago coordinado junto con el alcance de canal propio.

### Ofertas de financiación y seguros

- Las reglas de elegibilidad de las ofertas financieras deben configurarse cuidadosamente para cumplir con las regulaciones de préstamo, asegurándose de que las ofertas presentadas a los clientes sean aquellas para las que realmente puedan calificar.
- La integración de datos del perfil de crédito requiere un manejo seguro y estrictos controles de acceso, ya que la información financiera está sujeta a mayores requisitos de privacidad y regulación.
- La presentación de la oferta debe revelar claramente los términos, las tarifas y las condiciones de conformidad con las regulaciones de financiación al consumidor en cada mercado aplicable.
- [!DNL Journey Optimizer] las reglas de toma de decisiones deben tener en cuenta el precio del vehículo, el pago inicial y las preferencias a largo plazo del préstamo para clasificar las ofertas por relevancia en lugar de simplemente por tasa.

### Probar la programación de unidades

- Los sistemas de inventario del concesionario deben estar integrados para confirmar que el modelo de vehículo específico y el embellecedor en los que el cliente está interesado están disponibles para realizar pruebas de conducción en el concesionario recomendado.
- Las recomendaciones de los concesionarios basadas en la ubicación deben tener en cuenta la dirección del cliente, las clasificaciones de los concesionarios y la disponibilidad actual de citas para sugerir la opción más conveniente.
- Los mensajes de confirmación y recordatorio de la prueba de conducción deben incluir indicaciones, información de contacto del concesionario y qué esperar, lo que reduce las tasas de no presentación.
- Los datos de comportamiento de [!DNL Experience Platform] deben identificar el momento óptimo para sugerir una prueba de manejo, evitando el contacto prematuro con investigadores en etapa inicial que aún no están listos.

### Programas de fidelización de propietarios

- Los cálculos del nivel de fidelización deben incorporar varias dimensiones de participación, incluidas las visitas de servicio, las compras de piezas, las recomendaciones y la asistencia al evento, no solo el historial de compras de vehículos.
- Las reglas de elegibilidad basadas en niveles deben configurarse en la toma de decisiones de [!DNL Journey Optimizer] para determinar qué propietarios cumplen los requisitos para las ofertas exclusivas, el acceso anticipado a las nuevas revelaciones de vehículos y los reembolsos de recompensas de los socios, de modo que solo los miembros que cumplan los requisitos reciban cada categoría de beneficio.
- La lógica de mediación de ofertas debe evaluar las comunicaciones pendientes de los canales del distribuidor y del OEM antes de que se envíe cualquier mensaje, suprimiendo las promociones de prioridad inferior o conflictivas para evitar que el mismo propietario reciba ofertas contradictorias simultáneamente.
- La coordinación multicanal debe abarcar los sistemas CRM del distribuidor, las propiedades digitales del OEM, los canales de notificación del coche conectados y los puntos de contacto de servicio para que las interacciones de lealtad sean coherentes independientemente del lugar donde se involucre el propietario.
- Los sistemas de satisfacción de recompensas en los concesionarios y centros de servicio deben estar integrados para que los beneficios de fidelidad puedan canjearse sin problemas en el punto de servicio.
- Las comunicaciones deben adaptarse en función de la fase del ciclo de vida de la propiedad, entregando diferentes propuestas de valor a los nuevos propietarios en su primer año en comparación con los propietarios a largo plazo que se acercan a una posible actualización.
- La lógica de recorrido de [!DNL Journey Optimizer] debe detectar cambios de nivel en tiempo real y mensajes de felicitación o de renovación de la participación de déclencheur cuando los clientes se mueven entre niveles de lealtad.

### Garantía y planes de servicio ampliados

- Las fechas de caducidad de la garantía y los detalles de cobertura deben rastrearse con precisión en los perfiles de los clientes para llegar al déclencheur en el momento adecuado, por lo general 60-90 días antes de la caducidad.
- El kilometraje del vehículo y los patrones de uso de los datos o registros de servicio del automóvil conectado deben informar las recomendaciones del plan, ya que los conductores de alto kilometraje se benefician de una cobertura diferente a la de los propietarios de bajo kilometraje.
- El contenido de comparación del plan debe ser claro y no contener jergas, lo que ayuda a los clientes a comprender exactamente qué se cubre y el valor en relación con los posibles costes de reparación de desembolso.
- [!DNL Real-Time Customer Data Platform] segmentos deben distinguir entre los clientes con garantías de fábrica que caducan, aquellos con planes extendidos existentes que se aproximan a la renovación y aquellos sin cobertura actual.

### Activación de funciones de coche conectado

- Los datos de la plataforma del vehículo conectado deben integrarse para identificar qué características están disponibles en cada vehículo y cuáles el propietario ya ha activado o utilizado.
- El seguimiento de la adopción de funciones debe capturar los eventos de activación, la frecuencia de uso y la profundidad de participación para personalizar la secuencia y el ritmo de las recomendaciones de funciones.
- Los canales de notificación en el vehículo deben coordinarse con las notificaciones por correo electrónico y de la aplicación para ofrecer indicadores de funciones en el momento más relevante para el contexto, como sugerir características de navegación cuando se detecta un viaje por carretera.
- Los perfiles de [!DNL Experience Platform] deben almacenar los datos de configuración de la tecnología del vehículo, incluidos los paquetes instalados y las versiones de software, para garantizar que las recomendaciones de características sean compatibles con el vehículo específico del propietario.

### Coordinación de redes de distribuidores

- Las fuentes de inventario del concesionario deben integrarse y actualizarse con frecuencia para garantizar que la disponibilidad del vehículo mostrada a los clientes refleje con precisión lo que hay en el lote de cada concesionario.
- La lógica de asignación de cliente a concesionario debe tener en cuenta la proximidad, la especialización del concesionario, las preferencias de idioma y cualquier relación existente con el concesionario para proporcionar la mejor coincidencia.
- Las reglas de enrutamiento de posibles clientes deben garantizar que, cuando un cliente exprese interés en compras en línea, la consulta llegue rápidamente al concesionario correspondiente con un contexto completo sobre la actividad de investigación del cliente.
- La resolución de identidad de [!DNL Experience Platform] debe gestionar los casos en los que un cliente interactúa con varios concesionarios, manteniendo un perfil unificado y respetando la vista de cada concesionario sobre sus propias relaciones con los clientes.
