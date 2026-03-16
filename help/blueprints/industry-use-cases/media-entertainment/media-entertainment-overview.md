---
title: Casos de uso de medios y entretenimiento
description: Descubra cómo las organizaciones de medios y entretenimiento utilizan Adobe Experience Platform para personalizar la detección de contenido, reducir la pérdida de suscriptores y aumentar la participación de la audiencia.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2644'
ht-degree: 0%

---


# Casos de uso de medios y entretenimiento

Los medios de comunicación y las organizaciones de entretenimiento utilizan Adobe Experience Platform para unificar los datos de audiencia de las plataformas de streaming, las bibliotecas de contenido y las cuentas de suscriptor en una sola vista de cada espectador u oyente. Esta base permite la detección de contenido personalizado, la retención proactiva de suscriptores y las estrategias de participación que mantienen a las audiencias regresando para obtener más información.

## Motor de recomendación de contenido

Proporcione recomendaciones de contenido personalizadas, incluidas películas, programas de TV, música y artículos, en función del historial de visualización y escucha, las preferencias y un comportamiento similar del usuario. Cuando las audiencias ven contenido adaptado a sus intereses, pasan más tiempo explorando el catálogo y descubriendo títulos que de otra manera se habrían perdido.

### Impacto empresarial

Las organizaciones que implementan motores de recomendación de contenido personalizado suelen ver un aumento de entre el 30 y el 40 % en la participación en el contenido y un aumento significativo del tiempo total de visualización o escucha por usuario.

### Cómo implementar

Usar el patrón [Behavioral Recommendations](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Este enfoque utiliza modelos de recomendación impulsados por IA que aprenden continuamente de las interacciones de audiencia para mostrar el contenido más relevante para cada individuo.

### Consideraciones técnicas

- Los metadatos del catálogo de contenido, como género, elenco, director, etiquetas de estado de ánimo y clasificaciones de contenido, deben ingerirse y mantenerse actualizados para garantizar que las recomendaciones reflejen la amplia gama de títulos disponibles.
- Las señales de visualización y escucha deben fluir en tiempo casi real para que las recomendaciones se actualicen en una sola sesión de navegación a medida que un usuario ve u omite el contenido.
- Los modelos de recomendación requieren una estrategia de inicio en frío para los nuevos suscriptores que carecen de historial de visualización, que generalmente regresan a contenidos de tendencias, editoriales o regionales populares.
- Las ventanas de disponibilidad y licencias de contenido deben tenerse en cuenta en la lógica de recomendación para que los usuarios nunca sean títulos recomendados que no estén disponibles en su región o que se hayan eliminado del catálogo.


## Prevención de cancelación de suscripción

Identifique a los suscriptores que corren el riesgo de cancelarse y envíeles recomendaciones de contenido personalizado, ofertas y campañas de retención. La retención de los suscriptores existentes es mucho más rentable que la adquisición de nuevos suscriptores, y la divulgación proactiva en el momento adecuado puede evitar una parte significativa de las cancelaciones.

### Impacto empresarial

Los programas eficaces de prevención de pérdida ofrecen una reducción del 20-30 % en la pérdida de suscriptores, protegen los ingresos recurrentes y mejoran el valor de duración de la audiencia a largo plazo.

### Cómo implementar

Usar el patrón [Cross-Channel Recorrido with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Este método combina la orquestación de recorridos con la toma de decisiones en tiempo real para seleccionar la mejor oferta de retención o recomendación de contenido para cada suscriptor en riesgo de todos los canales.

### Consideraciones técnicas

- La puntuación de riesgo de pérdida debe incorporar señales de participación como la disminución del tiempo de reloj, la reducción de la frecuencia de inicio de sesión y las caídas de finalización de contenido para identificar a los suscriptores en riesgo antes de que lleguen a la página de cancelación.
- Las ofertas de retención deben clasificarse según el valor del suscriptor y el nivel de riesgo, que va desde los aspectos destacados del contenido personalizado hasta las extensiones del plan con descuento, para equilibrar la protección de los ingresos con el impacto del margen.
- El recorrido debe suprimir los mensajes de retención para los suscriptores que ya hayan renovado o actualizado, lo que requiere una integración en tiempo real con el sistema de facturación de suscripciones.
- [!DNL Journey Optimizer] las reglas de toma de decisiones deben tener en cuenta el tipo de plan, el ejercicio y el historial de canje de ofertas anteriores del suscriptor para evitar presentar ofertas que se sientan genéricas o repetitivas.


## Notificaciones de nueva versión de contenido

Notificar a los suscriptores sobre nuevas versiones de contenido que coincidan con sus preferencias y el historial de visualización. Las notificaciones oportunas sobre contenido nuevo impulsan la participación inmediata y recuerdan a los suscriptores el valor continuo de su suscripción.

### Impacto empresarial

Las notificaciones personalizadas de la versión suelen impulsar un aumento de entre el 40 y el 50 % en la participación del nuevo contenido durante la primera semana de la versión, lo que acelera la audiencia y aumenta las métricas de rendimiento del contenido.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método responde a los eventos de lanzamiento de contenido, comparando los nuevos títulos con los perfiles de preferencias del suscriptor para enviar notificaciones oportunas y relevantes.

### Consideraciones técnicas

- Los calendarios de publicación de contenido deben integrarse para que las notificaciones se puedan programar o activar en el momento en que los nuevos títulos estén disponibles, lo que evita alertas prematuras para contenido que aún no es accesible.
- La coincidencia de preferencias del suscriptor debe tener en cuenta varias dimensiones, incluida la afinidad de género, actores o directores favoritos, series vistas anteriormente e intereses de la franquicia, para garantizar que las notificaciones se sientan personalmente relevantes.
- El volumen de notificaciones debe administrarse cuidadosamente mediante la restricción de frecuencia para evitar que los suscriptores se sientan abrumados durante períodos de publicaciones de contenido pesadas.
- La zona horaria y los datos del hábito de visualización deben informar el momento de la entrega para que las notificaciones lleguen cuando sea más probable que cada suscriptor se involucre, en lugar de en una sola hora de envío global.


## Experiencia personalizada en página de inicio

Personalice de forma dinámica las páginas de inicio y de detección de contenido para mostrar primero el contenido más relevante en función del perfil y el comportamiento de cada usuario. Cuando los espectadores ven el contenido alineado con sus gustos inmediatamente al abrir la aplicación, se relacionan más rápido y exploran más tiempo.

### Impacto empresarial

Las experiencias personalizadas de página principal impulsan un aumento de entre el 25 y el 35 % en la participación en la página principal y mejoran significativamente la detección de contenido, especialmente para plataformas con bibliotecas de contenido grandes y en crecimiento.

### Cómo implementar

Usar el patrón [Behavioral Recommendations](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Este método utiliza estrategias de selección y modelos de clasificación para reordenar las filas de contenido y los títulos destacados de la página principal en función del perfil de cada visitante y del comportamiento en tiempo real.

### Consideraciones técnicas

- La personalización de la página principal debe ejecutarse con la rapidez suficiente para evitar retrasos de carga percibidos; la toma de decisiones basada en Edge o el procesamiento del lado del servidor suelen ser necesarios para satisfacer las expectativas de tiempo de respuesta de menos de segundo.
- La lógica de personalización debe combinar las preferencias individuales con las prioridades editoriales y promocionales, lo que garantiza que las versiones de tipoles, el contenido estacional y los títulos promocionados por los socios sigan recibiendo la visibilidad adecuada.
- Las estrategias de fila de contenido, como &quot;Seguir viendo&quot;, &quot;Porque has visto&quot; y &quot;Tendencia ahora&quot;, requieren entradas de datos distintas y una lógica de clasificación que deben organizarse en un diseño de página coherente.
- [!DNL Experience Platform] La implementación de Web SDK debe capturar las interacciones de la página principal, incluidos los desplazamientos de fila, los clics en mosaico y el comportamiento al pasar el ratón por encima, para refinar continuamente los modelos de clasificación.


## Recordatorios de lista de observación y favoritos

Envíe recordatorios a los usuarios sobre el contenido de su lista de observación que aún no han visto, junto con recomendaciones personalizadas para títulos similares. Las listas de observación representan señales de intención potentes y los recordatorios suaves pueden convertir esa intención en una visualización real.

### Impacto empresarial

Los programas de recordatorio de listas de observación suelen lograr un aumento del 30 al 40 % en la tasa de finalización de listas de observación, lo que convierte la intención guardada en participación activa y aumenta el uso general de la plataforma.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método déclencheur los recordatorios en función de las señales de actividad e inactividad de la lista de observación, y envía avisos puntuales cuando el contenido se ha guardado, pero aún no se ha iniciado.

### Consideraciones técnicas

- El tiempo de los recordatorios debe calibrarse en función del tiempo que el contenido haya estado en la lista de observación y de si el usuario ha estado activo en la plataforma recientemente, lo que evita los recordatorios durante los períodos de participación intensa cuando son innecesarios.
- Los datos de las listas de observación deben sincronizarse entre dispositivos en tiempo real para que el título añadido en dispositivos móviles se refleje inmediatamente en los cálculos de idoneidad del recordatorio y no se duplique entre plataformas.
- Los recordatorios deben resaltar detalles contextuales como las ventanas de disponibilidad que caducan o las nuevas temporadas de series guardadas para crear una urgencia natural sin sentirse presionado.
- El contenido que se haya eliminado del catálogo o que ya no esté disponible en la región del suscriptor debe excluirse automáticamente de los mensajes de recordatorio y reemplazarse por recomendaciones alternativas.


## Campañas de conversión de prueba gratuita

Fomente la participación de usuarios de prueba gratuita con recomendaciones y ofertas de contenido personalizadas para fomentar la conversión de suscripciones antes de que finalice el periodo de prueba. La ventana de prueba es una oportunidad crítica para demostrar el valor suficiente que los usuarios están dispuestos a pagar, y un recorrido de conversión estructurado supera significativamente a un único recordatorio de fin de prueba.

### Impacto empresarial

Las campañas de conversión de prueba bien diseñadas ofrecen una mejora de entre el 25 y el 35 % en las tasas de conversión de prueba a pago, lo que aumenta directamente la eficiencia de adquisición de los suscriptores y reduce el coste por adquisición.

### Cómo implementar

Usar el patrón [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Este recorrido de nutrición multitáctil guía a los usuarios de prueba a través de una secuencia de mensajes de conversión, demostración de valor y detección de contenido, adaptándose en función de su participación durante toda la prueba.

### Consideraciones técnicas

- El recorrido debe rastrear las fechas de inicio y finalización de la prueba con precisión, con una lógica de ramificación que ajuste la cadencia de la mensajería en función de los días de prueba restantes y los niveles de participación observados.
- Las recomendaciones de contenido dentro del recorrido deben priorizar los títulos más atractivos y exclusivos de la plataforma para maximizar el valor percibido de una suscripción de pago durante la ventana de prueba limitada.
- Los usuarios que realizan la conversión antes de que finalice la prueba deben moverse automáticamente del recorrido de conversión a un nuevo flujo de bienvenida de suscriptor, lo que impide que los mensajes sigan centrados en la prueba.
- [!DNL Journey Optimizer] las condiciones de recorrido deben tener en cuenta el tipo de plan de prueba, el origen de referencia y el uso del dispositivo para adaptar el método de conversión a los distintos segmentos de audiencia.


## Recordatorios de visualización de eventos activos

Notificar a los usuarios sobre próximos eventos en directo, juegos deportivos o estrenos que coincidan con sus intereses y el historial de visualización. El contenido en directo impulsa la visualización de citas que fortalece los hábitos de los suscriptores y los recordatorios oportunos garantizan que las audiencias no se pierdan los eventos que les interesan.

### Impacto empresarial

Los recordatorios personalizados de eventos en directo suelen aumentar la audiencia de eventos en directo en un 50-60%, lo que maximiza la audiencia para una programación en tiempo real de alto valor.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método déclencheur las notificaciones en función de los datos de programación de eventos, haciendo coincidir los próximos eventos con los perfiles de interés de los suscriptores para enviar recordatorios oportunos.

### Consideraciones técnicas

- Los datos de programación de eventos, incluyendo las horas de inicio, los equipos participantes o el talento, y los detalles de difusión, deben ingerirse desde los sistemas de programación y mantenerse actualizados para gestionar cambios o cancelaciones de programación de última hora.
- La hora de entrega del recordatorio debe tener en cuenta los husos horarios y los tiempos de espera previos al evento habituales; se olvida un recordatorio enviado demasiado pronto, mientras que uno enviado demasiado tarde omite el inicio.
- La coincidencia de intereses debe incorporar preferencias explícitas, como equipos o géneros favoritos, y señales implícitas, como patrones de visualización de eventos en directo anteriores, para identificar eventos relevantes para cada suscriptor.
- La coordinación de notificaciones entre varios dispositivos es importante para que un suscriptor no reciba recordatorios redundantes en su teléfono, tableta y TV inteligente simultáneamente.


## Generación de listas de reproducción personalizadas

Genere y actualice automáticamente listas de reproducción personalizadas basadas en el historial de escucha, las preferencias y los indicadores de estado de ánimo de cada usuario. Las listas de reproducción seleccionadas reducen el esfuerzo de selección de contenido y mantienen a los oyentes comprometidos durante sesiones más largas.

### Impacto empresarial

La generación personalizada de listas de reproducción aumenta en un 40-50% la participación en la lista de reproducción y amplía significativamente la duración promedio de la sesión de escucha, fortaleciendo los hábitos diarios de uso de la plataforma.

### Cómo implementar

Usar el patrón [Behavioral Recommendations](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Este enfoque utiliza modelos impulsados por IA que analizan los patrones de escucha, el comportamiento de omisión y las señales contextuales para generar y actualizar listas de reproducción adaptadas a cada usuario.

### Consideraciones técnicas

- Los metadatos del catálogo de música, incluidos el tempo, el género, las etiquetas de estado de ánimo, las relaciones con los artistas y las funciones de audio, deben etiquetarse cuidadosamente para permitir una depuración de las listas de reproducción con matices que vaya más allá de la simple coincidencia de géneros.
- La frecuencia de actualización de la lista de reproducción debe equilibrar la frescura con la familiaridad; los oyentes esperan nuevos descubrimientos, pero también desean volver a visitar los favoritos, por lo que los modelos deben combinar la exploración con la comodidad.
- Las señales contextuales como la hora del día, el día de la semana y el dispositivo de escucha pueden informar el estado de ánimo y el nivel de energía de la lista de reproducción, creando listas de reproducción que se sientan apropiadas para el momento.
- Los datos de comportamiento de [!DNL Experience Platform] deben capturar eventos de escucha granulares, incluidos saltos, reproducciones, guardados y duración de la sesión, a fin de perfeccionar continuamente los modelos de recomendación.


## Sincronización de contenido entre plataformas

Ofrezca una experiencia de contenido perfecta en todos los dispositivos sincronizando el historial de visualización, las preferencias y las recomendaciones en tiempo real. Los espectadores esperan pausar en un dispositivo y reanudar en otro sin perder su lugar, y una experiencia coherente en todas las plataformas refuerza los hábitos de uso diarios.

### Impacto empresarial

La sincronización de contenido entre plataformas aumenta en un 30-40 % la participación entre dispositivos y reduce de forma significativa la fricción que puede provocar el abandono de la sesión cuando los usuarios cambian entre dispositivos.

### Cómo implementar

Usar el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones/web de visitantes conocidos. Este método personaliza la experiencia de los usuarios identificados en todas las plataformas web y de aplicación, lo que garantiza un estado de contenido y recomendaciones coherentes independientemente del dispositivo.

### Consideraciones técnicas

- La resolución de identidad entre dispositivos debe vincular de forma fiable las sesiones de usuario entre televisores inteligentes, aplicaciones móviles, tabletas y exploradores web para mantener un único perfil unificado para cada suscriptor.
- Los datos de progreso del reloj, incluida la posición exacta de la reproducción, el estado de finalización del episodio y las preferencias de subtítulos o pistas de audio, se deben sincronizar con una latencia mínima para ofrecer una experiencia de reanudación sin problemas.
- Los modelos de recomendación deben tener en cuenta el contexto del dispositivo, ya que las preferencias de contenido pueden diferir entre una sesión de trayecto móvil y una sesión de sala de estar por la noche en una pantalla grande.
- [!DNL Real-Time Customer Data Platform] directivas de combinación de perfiles deben configurarse para controlar sesiones simultáneas en varios dispositivos sin crear actualizaciones de estado en conflicto.


## Compartir en redes sociales Personalization

Personalice los indicadores y las recomendaciones de uso compartido en redes sociales en función de las conexiones sociales y las preferencias de contenido de cada usuario. Hacer que sea fácil y atractivo para los espectadores compartir lo que aman convierte a los suscriptores satisfechos en defensores orgánicos que impulsan la concienciación y la adquisición.

### Impacto empresarial

Los estímulos personalizados para compartir en redes sociales suelen lograr un aumento del 20 al 30% en la tasa de intercambio social, amplificando el alcance orgánico y reduciendo los costos de adquisición pagados.

### Cómo implementar

Usar el patrón [Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) de aplicaciones/web de visitantes conocidos. Este método personaliza las experiencias de uso compartido en la aplicación para usuarios identificados, y muestra mensajes de uso compartido relevantes para el contexto en función de las preferencias y los patrones de participación del usuario.

### Consideraciones técnicas

- Compartir mensajes debe activarse en momentos naturales de deleite, como completar una serie atractiva o descubrir a un nuevo artista favorito, en lugar de a intervalos arbitrarios que se sientan intrusivos.
- Los mensajes y las imágenes para compartir rellenados previamente deben generarse dinámicamente en función del contenido específico que se comparte, incluidas las miniaturas, las descripciones y los vínculos profundos adecuados que devuelvan a los destinatarios a la plataforma.
- Los controles de privacidad deben garantizar que la actividad de visualización solo se comparta cuando el usuario inicie explícitamente el uso compartido; el uso compartido pasivo o automático del historial de visualización sin consentimiento puede dañar la confianza.
- La integración de Social Platform debe cumplir con las políticas de uso compartido de cada red y gestionar la autenticación, los límites de velocidad y los requisitos de formato de contenido para plataformas como Instagram, TikTok y X.


## Ampliación de venta de funciones Premium

Identifique a los usuarios que se beneficiarían de las funciones avanzadas y presenten ofertas de ampliación de venta personalizadas en función de sus patrones de uso. La mensajería de ampliación de venta dirigida a usuarios que ya muestran comportamientos alineados con el valor premium es mucho más eficaz que las campañas de actualización generales.

### Impacto empresarial

Las campañas personalizadas de ampliación de venta de premium impulsan un aumento de entre el 15 y el 25 % en la adopción de funciones de premium, lo que aumenta los ingresos promedio por usuario y, al mismo tiempo, ofrece funciones que coinciden genuinamente con las necesidades de los suscriptores.

### Cómo implementar

Usar el patrón [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Este enfoque utiliza una lógica de decisión centralizada para evaluar los patrones de uso de cada suscriptor y seleccionar la oferta Premium más relevante en el momento adecuado.

### Consideraciones técnicas

- El análisis del patrón de uso debe identificar comportamientos específicos que indiquen una preparación premium, como el uso frecuente de funciones disponibles de forma limitada en el plan básico, el uso de varios dispositivos o el alto volumen de consumo de contenido.
- La presentación de la oferta debe resaltar los beneficios premium específicos más relevantes para el comportamiento de cada usuario en lugar de enumerar todas las funciones premium de forma genérica; un usuario que descarga contenido con frecuencia debe ver la visualización sin conexión enfatizada.
- El tiempo de ampliación de venta debería evitar momentos de frustración, como inmediatamente después de un bloqueo de Paywall, y en su lugar aprovechar los momentos de participación positiva cuando el suscriptor es más receptivo.
- [!DNL Journey Optimizer] las reglas de toma de decisiones deben coordinar las ofertas de ampliación de venta en los mensajes en la aplicación, el correo electrónico y las notificaciones push para presentar una oferta coherente sin saturar al suscriptor en los distintos canales.


## Campañas de finalización de contenido

Recuerde a los usuarios que terminen de ver o escuchar el contenido que iniciaron pero que no completaron, acompañado de recomendaciones personalizadas sobre qué disfrutar a continuación. El contenido incompleto representa una participación no realizada y un ligero empujón a menudo convierte una sesión abandonada en una experiencia completada.

### Impacto empresarial

Las campañas de finalización de contenido suelen lograr una mejora de entre el 35 y el 45 % en la tasa de finalización de contenido, lo que aumenta el tiempo total de participación y refuerza la percepción del suscriptor del valor de la plataforma.

### Cómo implementar

Usar el patrón [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Este método déclencheur los recordatorios en función de los eventos de abandono de contenido, y envía mensajes puntuales cuando un usuario se ha pausado parcialmente a través de un título y no ha regresado dentro de una ventana definida.

### Consideraciones técnicas

- Los umbrales de abandono deben calibrarse por tipo de contenido; una película en pausa al 80% es una fuerte candidata a la finalización, mientras que un podcast detenido después de dos minutos puede indicar desinterés en lugar de interrumpir la escucha.
- Los mensajes de recordatorio deben incluir el título de contenido específico, una miniatura visual y un vínculo profundo directo que reanude la reproducción en el punto exacto en el que el usuario lo dejó.
- La restricción de frecuencia debe evitar recordatorios excesivos para los usuarios que toman muestras del contenido de forma rutinaria sin terminar; los empujones repetidos para el contenido que un usuario ha elegido abandonar pueden resultar intrusivos.
- La disponibilidad del contenido debe verificarse en el momento de la entrega, ya que los títulos pueden salir de la plataforma o cambiar las regiones de disponibilidad entre el evento de abandono y la entrega del recordatorio.
