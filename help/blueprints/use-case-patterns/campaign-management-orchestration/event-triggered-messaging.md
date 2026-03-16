---
title: Mensajería activada por eventos
description: Aprenda a entregar mensajes contextuales en tiempo real en respuesta a eventos de comportamiento o del sistema.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '9039'
ht-degree: 1%

---


# Mensajería activada por eventos

Esta guía proporciona un modelo de implementación completo para la mensajería activada por eventos mediante [!DNL Adobe Journey Optimizer] (AJO), [!DNL Real-Time Customer Data Platform] (RT-CDP) y [!DNL Adobe Experience Platform] (AEP). Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten enviar mensajes contextuales en tiempo real en respuesta a eventos de comportamiento o del sistema.

Utilice esta guía para comprender qué configurar, dónde existen las opciones de implementación y qué compensaciones impulsan cada decisión.

La guía cubre el ciclo de vida completo, desde la ingesta de eventos y la creación de recorridos hasta la entrega de mensajes y la creación de informes de rendimiento, con directrices de decisión detalladas para tres opciones de implementación distintas.

## Resumen del caso de uso

La mensajería activada por eventos ofrece un mensaje contextual en respuesta a un evento del sistema o de comportamiento en tiempo real. A diferencia de la activación de mensajes salientes por lotes, que envía a una audiencia preevaluada según una programación, este patrón escucha un evento correspondiente (como el abandono del carro de compras, una sesión de exploración, un envío de formulario o un cambio de estado del sistema) e introduce inmediatamente el perfil de activación en un recorrido que evalúa las condiciones y envía un mensaje.

El patrón se basa en la transmisión de eventos en tiempo real a AEP (a través de Web SDK, Mobile SDK o API del lado del servidor), un recorrido con una entrada de evento unitario en AJO y una lógica de evaluación de condiciones que determina si se debe enviar y qué. El mensaje se envía normalmente pocos minutos después del evento de activación, lo que hace que este patrón sea ideal para comunicaciones contextualmente relevantes y con distinción de tiempo.

Las organizaciones utilizan este patrón para responder a las acciones de los clientes en tiempo real, lo que aumenta la relevancia e impulsa tasas de participación y conversión más altas en comparación con las comunicaciones por lotes programadas. Entre los escenarios comunes se incluyen la recuperación del carro de compras abandonado, el seguimiento posterior a la compra, los mensajes de bienvenida después del registro y las notificaciones con distinción de tiempo, como errores de pago o alertas de caída de precios.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

**[Recuperar carros y recorridos abandonados](../../business-objectives/customer-experience/recover-abandoned-carts-journeys.md)**

Vuelva a atraer a los usuarios que abandonaron durante los flujos de compra, solicitud o inscripción con seguimientos personalizados y oportunos.

| KPI |
| --- |
| Tasas de conversión, ingresos incrementales, participación |

**[Aumentar las tasas de conversión](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

Mejore el porcentaje de visitantes y clientes potenciales que completan las acciones deseadas, como compras, suscripciones o envíos de formularios.

| KPI |
| --- |
| Tasas de conversión, Conversión de cliente potencial, Coste por cliente potencial |

**[Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo de vida individuales.

| KPI |
| --- |
| Participación, tasas de conversión, satisfacción del cliente (CSAT) |

**[Mejorar la incorporación de los clientes](../../business-objectives/customer-experience/improve-customer-onboarding.md)**

Acelere el tiempo de respuesta al valor para los nuevos clientes con experiencias de bienvenida y recorridos de activación optimizados y personalizados.

| KPI |
| --- |
| Participación, Retención, Tasas de conversión |

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran cómo se puede aplicar la mensajería activada por eventos a distintos contextos comerciales.

- **Correo electrónico o SMS de abandono del carro de compras**: envía un mensaje recordatorio cuando un cliente agrega artículos al carro de compras, pero no completa la compra en un plazo definido
- **Seguimiento del abandono del examen**: vuelva a atraer visitantes que vieron productos o contenido pero no realizaron una acción de conversión
- **Agradecimiento o venta cruzada posterior a la compra**: envíe una confirmación y una recomendación de venta cruzada inmediatamente después de un evento de compra
- **Recordatorio de caducidad de prueba**: notifique a los usuarios que se aproximen al final de una prueba gratuita con mensajes de renovación o conversión
- **Mensaje de bienvenida después del registro**: envíe un mensaje de incorporación inmediato cuando un nuevo usuario se registre o cree una cuenta
- **Confirmación de envío de formulario**: reconozca los envíos de formularios (solicitudes de contacto, solicitudes e inscripciones) con una confirmación contextual
- **Notificación de error de pago**: avisa a los clientes cuando un pago recurrente falla y les solicita que actualicen la información de pago
- **Notificación push de recuperación tras la desinstalación de la aplicación**: Déclencheur de un mensaje de recuperación cuando un usuario desinstala una aplicación móvil
- **Confirmación de reserva o cita** — Enviar confirmación inmediata después de que se programe una reserva, reserva o cita
- **Alerta de bajada de precios para artículos en la lista de deseos** — Notificar a los clientes cuando un producto en su lista de deseos baje de precio

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir la eficacia de las implementaciones de mensajería activadas por eventos.

| KPI | Descripción | Medición |
| --- | --- | --- |
| Tasa de conversión | Porcentaje de destinatarios de mensajes activados que completan la acción deseada (compra, registro, renovación) | Conversiones / Mensajes entregados * 100 |
| Ingresos incrementales | Ingresos adicionales atribuibles a mensajes activados por eventos en comparación con los grupos de control sin envío | Ingresos de envíos activados: línea base del grupo de control |
| Tasa de apertura | Porcentaje de mensajes enviados que abren los destinatarios | Aperturas / Entregas * 100 |
| Tasa de clics (CTR) | Porcentaje de mensajes enviados que generan al menos un clic | Clics/Entregados * 100 |
| Tiempo de conversión | Tiempo promedio transcurrido entre el envío del mensaje y el evento de conversión | Avg(marca de tiempo de conversión - marca de tiempo de entrega) |
| Tasa de finalización de recorridos | Porcentaje de perfiles que entran en el recorrido y llegan al paso de entrega de mensajes (no perdidos por condiciones o salidas) | Perfiles que llegan a la entrega / Perfiles que entran en el recorrido * 100 |
| Tasa de supresión de mensajes | Porcentaje de perfiles calificados suprimidos debido a límites de frecuencia, consentimiento o evaluación de condición | Perfiles suprimidos / Perfiles cualificados totales * 100 |
| Tasa de devoluciones | Porcentaje de mensajes que no se pudieron enviar debido a mensajes devueltos no entregados o rechazados | Devoluciones / Enviados * 100 |

## Patrón de caso de uso

En esta sección se describe el patrón principal y la cadena de funciones que impulsa la mensajería activada por eventos.

**Mensajería activada por eventos**

Escuche un evento del sistema o de comportamiento en tiempo real y, a continuación, envíe un mensaje contextual al perfil de activación.

**Cadena De Funciones:** Ingesta De Eventos > Entrada De Recorridos > Evaluación De Condiciones > Entrega De Mensajes > Informes

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones de Adobe.

- **[!DNL Adobe Journey Optimizer] (AJO)**: orquestación de Recorrido con entrada de evento unitario, evaluación de condición, pasos de espera, creación de mensajes, configuración de canal, control de frecuencia e informes de envío
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)**: evaluación de audiencias para filtrado basado en condiciones dentro de los recorridos, aplicación del consentimiento y del control, enriquecimiento de perfiles
- **[!DNL Adobe Experience Platform] (AEP)**: ingesta de eventos en tiempo real mediante Web SDK, Mobile SDK o API del lado del servidor; modelado de datos; resolución de identidades; Edge Network

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Se asume en contexto | Zona protegida de AJO aprovisionada con la configuración de canal activa. Permisos de creación y publicación de recorridos asignados al equipo de implementación. Funciones de usuario configuradas para la administración de recorrido, la creación de contenido y la administración de canales. | [Resumen de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home), [Resumen de control de acceso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | Un esquema XDM ExperienceEvent debe capturar el evento de activación con todos los campos contextuales necesarios para la evaluación de condiciones y la personalización de mensajes (por ejemplo, `commerce.productListAdds` para eventos de carro de compras, detalles del producto y valor del carro de compras). El esquema debe estar habilitado para el perfil del cliente en tiempo real. Se debe crear un conjunto de datos correspondiente y habilitar para el perfil. | [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [Conceptos básicos de composición de esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Fuentes de datos y recopilación | Requerido | Se debe configurar el flujo de eventos en tiempo real: Web SDK para eventos web, Mobile SDK para eventos de aplicaciones o la API de Edge Network Server para eventos del sistema. Se debe configurar una secuencia de datos con los servicios AEP y AJO habilitados, que enruten eventos al conjunto de datos correcto. Esta es una dependencia crítica, ya que el patrón depende de la ingesta de eventos en tiempo real. | [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Configurar flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Configuración de identidad y perfil | Requerido | El evento de activación debe estar asociado a una identidad conocida (correo electrónico, ID de CRM o sesión autenticada) para que el recorrido pueda resolver el perfil y enviar el mensaje. Deben existir áreas de nombres de identidad para los identificadores utilizados por el evento de activación. Los eventos anónimos requieren la vinculación de identidad a través del gráfico de identidad antes de que se pueda enviar un mensaje. Se debe configurar una política de combinación. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Introducción a las políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Definición de audiencia y segmentación | Recomendado | Aunque no es estrictamente necesario para recorridos activados por eventos (la entrada se basa en eventos, no en audiencias), los segmentos de audiencia pueden utilizarse para la evaluación de condiciones dentro del recorrido (por ejemplo, enviar solo si el perfil está en un segmento de &quot;cliente de alto valor&quot; o suprimir si el perfil está en un segmento de &quot;contactos recientes&quot;). Se recomienda la evaluación de la transmisión para las comprobaciones de pertenencia de segmentos en tiempo real dentro de los recorridos. | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Los atributos calculados, como el recuento de abandono del carro de compras, los días transcurridos desde la última compra, el valor de pedido promedio y el total de compra de por vida, mejoran la evaluación de condiciones y la personalización dentro de los recorridos activados. Estos agregados de comportamiento permiten decisiones de segmentación más precisas (por ejemplo, diferenciar a los que abandonan por primera vez de los que abandonan repetidamente). | [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Administración del ciclo de datos | Recomendado | La caducidad de los datos de evento debe configurarse para eventos de comportamiento transitorios (vistas de página, búsquedas, clics) para administrar los costes de almacenamiento y el cumplimiento de las normas. Los campos de esquema de consentimiento deben estar presentes para la aplicación de inclusión/exclusión específica del canal durante la entrega del mensaje. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Caducidad de conjuntos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| Etiquetado y aplicación del uso de datos | Recomendado | Las etiquetas de gobernanza en los campos de evento y perfil garantizan una personalización compatible. Si los mensajes activados incluyen contenido personalizado con PII o datos de comportamiento, se deben revisar las etiquetas de uso de datos y las políticas de gobernanza para evitar el uso no autorizado de datos en el contenido del mensaje. | [Resumen de control de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Resumen de etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview) |
| Monitorización y observabilidad | Incluido | La monitorización de la ejecución del recorrido forma parte de la fase de creación de informes. Además, puede configurar alertas para errores de ingesta de eventos o retrasos en el procesamiento de recorridos para detectar problemas de canalización que impidan que se envíen mensajes activados. | [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Informes y análisis | Incluido | Los informes de rendimiento del recorrido se tratan en la fase de creación de informes. Para un análisis más profundo de la eficacia de la mensajería activada en todos los canales y a lo largo del tiempo, configure las conexiones y espacios de trabajo de CJA para analizar la atribución de conversión, el tiempo de conversión y el rendimiento del canal. | [descripción general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del Catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Journey Optimizer] (AJO)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Journey Orchestration | Creación y configuración de recorridos | Cree un recorrido con entrada de evento unitario, configure el evento correspondiente, añada nodos de condición, pasos de espera, acciones de mensajes, criterios de salida y reglas de reentrada |
| Configuración de canal | Configuración de superficie de canal | Configure o valide superficies de canal (correo electrónico, SMS, push), incluida la delegación de subdominios, grupos de IP, configuración de remitentes y administración de listas de supresión |
| Creación de mensajes | Creación de contenido de mensaje | Creación de contenido de mensaje contextual con personalización basada en eventos, bloques de contenido condicional y fragmentos reutilizables |
| Frecuencia y reglas comerciales | Creación y configuración de recorridos (opción C) | Configure límites de frecuencia y reglas de deduplicación para evitar el exceso de mensajes desde fuentes de eventos de alta frecuencia |
| Administración de conflictos y prioridades | Creación y configuración de recorridos | Asigne puntuaciones de prioridad y configure la detección de recorridos que compitan por los mismos perfiles |
| Informes y análisis de rendimiento | Informes y monitorización | Monitorice las métricas de entrega de recorrido a través de informes activos e históricos; acceda a los datos de rendimiento de la programación a través de CJA |

### [!DNL Real-Time CDP] (RT-CDP)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Evaluación de audiencia | Configuración básica (F5) | Evaluar los segmentos de audiencia utilizados para el filtrado basado en condiciones dentro del recorrido (por ejemplo, segmentos de clientes de alto valor, segmentos de supresión) |
| Cumplimiento del consentimiento y la gobernanza | Configuración básica (S2/S3) | Aplicar preferencias de consentimiento y políticas de gobernanza del uso de datos durante la entrega de mensajes para garantizar comunicaciones compatibles |

## Prerrequisitos

Complete lo siguiente antes de comenzar la implementación.

- [ ] zona protegida de AJO aprovisionada con permisos de creación y publicación de recorrido (F1)
- [ ] esquema XDM ExperienceEvent que captura el evento de activación con campos contextuales, habilitados para Perfil del cliente en tiempo real (F2)
- [ ]: flujo de eventos en tiempo real configurado mediante la API de Web SDK, Mobile SDK o Edge Network Server con un flujo de datos que enruta eventos al conjunto de datos correcto de AEP (F3).
- [ ] áreas de nombres de identidad configuradas para los identificadores en el evento de activación; reglas de vinculación de identidad establecidas (F4)
- [ ] Superficie de canal (correo electrónico, SMS o push) configurada y validada con un envío de prueba correcto
- [ ] Contenido de mensaje creado, revisado y probado con perfiles de muestra
- [ ] campos de consentimiento rellenados en perfiles para el canal de destino (por ejemplo, `consents.marketing.email.val`)
- [ ] Si utiliza el filtrado de audiencia basado en condiciones (Opción B/C), se definieron los segmentos de audiencia evaluados por flujo continuo y se evaluaron activamente

## Opciones de implementación

En esta sección se describen tres opciones de implementación para la mensajería activada por eventos. Cada opción se basa en la anterior y agrega capacidades adicionales.

### Opción A: mensaje simple activado por evento

**Ideal para:** respuestas inmediatas de un solo mensaje en las que no se necesita ningún retraso o lógica condicional: confirmación de pedido, correo electrónico de bienvenida, confirmación de envío de formulario, confirmación de reserva.

**Cómo funciona:**

El recorrido escucha un evento correspondiente a través de un nodo de entrada de evento unitario. Cuando se recibe el evento, el perfil entra en el recorrido, pasa por una evaluación de condición mínima (comprobación de consentimiento, verificación de la existencia del perfil) y recibe inmediatamente un único mensaje a través del nodo de acción del canal configurado.

Esta es la variante de implementación más sencilla. El lienzo de recorrido contiene un nodo de entrada de evento, un nodo de condición opcional para comprobaciones de idoneidad básicas, un nodo de acción de mensaje único y un nodo final. No hay pasos de espera, ni ramas complejas, ni comprobaciones de conversión. El mensaje se suele enviar de segundos a minutos después del evento de activación.

Los datos de evento del evento de activación (nombre del producto, total del pedido, detalles del formulario) se pueden utilizar para la personalización de mensajes mediante atributos contextuales en el editor de personalización. Este enfoque maximiza la velocidad de entrega y minimiza la complejidad del recorrido.

**Consideraciones clave:**

- El mensaje se envía independientemente de si el cliente se convierte automáticamente después del evento (sin comprobación de conversión)
- El más adecuado para eventos que garantizan inherentemente una respuesta inmediata (confirmaciones, reconocimientos)
- Las reglas de reentrada deben configurarse cuidadosamente: para los mensajes de estilo de confirmación, permita la reentrada para que cada evento genere un mensaje; para los mensajes de estilo de bienvenida, evite la reentrada

**Ventajas:**

- El tiempo de entrega más rápido (de segundos a minutos después del evento)
- La configuración de recorrido más sencilla con piezas móviles mínimas
- El menor riesgo de fallos de recorrido o perfiles atascados
- Fácil de probar y mantener

**Limitaciones:**

- No es posible comprobar si el cliente se convirtió automáticamente antes de enviarlo
- No se puede incorporar la lógica condicional con retraso de tiempo
- Puede generar mensajes innecesarios si el evento se produce con frecuencia sin control de frecuencia

**Experience League:**

- [Creación de un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Eventos generales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)

### Opción B: mensaje condicional activado por evento con espera

**Ideal para:** Respuestas condicionales con retraso en las que el cliente debería tener tiempo para la conversión automática antes de recibir el mensaje: abandono del carro de compras (espere de 1 a 4 horas y, a continuación, compruebe si el carro de compras sigue abandonado), abandono del explorador (espere 24 horas y compruebe si se realizó la compra) y caducidad de la prueba (espere hasta que se aproxime la fecha de caducidad).

**Cómo funciona:**

El recorrido escucha un evento correspondiente, introduce el perfil e introduce un periodo de espera antes de evaluar las condiciones. Después de la espera, un nodo de condición comprueba si el cliente se ha convertido automáticamente (por ejemplo, si ha completado la compra o renovado la suscripción) o si el contexto original sigue siendo válido. Solo si se cumple la condición (por ejemplo, si el carro de compras sigue abandonado) el recorrido continúa con la entrega de mensajes.

El lienzo de recorrido contiene un nodo de entrada de evento, un nodo de espera (duración configurable o fecha/hora específica), un nodo de condición que comprueba un evento de conversión o un cambio de estado de perfil, rutas de ramificación (enviar mensaje o salir sin enviar), un nodo de acción de mensaje en la ruta correspondiente y un nodo final en cada rama. Se pueden configurar criterios de salida para eliminar automáticamente perfiles de la recorrido si el evento de conversión se produce durante el período de espera, lo que elimina la necesidad de realizar una comprobación de condiciones explícita.

Este método reduce los mensajes innecesarios, ya que proporciona a los clientes tiempo para la conversión automática, mejora la experiencia del cliente y aumenta la relevancia percibida de los mensajes que se envían.

**Consideraciones clave:**

- La duración de la espera afecta significativamente a las tasas de conversión: las esperas más cortas (de 1 a 2 horas) producen una mayor urgencia, pero más envíos innecesarios; las esperas más largas (de 24 a 48 horas) reducen el volumen, pero pueden perderse la ventana de relevancia
- La evaluación de condiciones requiere que el evento de conversión se capture en AEP y se asocie con la misma identidad de perfil
- Los criterios de salida proporcionan una alternativa más limpia a los nodos de condición explícitos para la comprobación de conversiones
- Las reglas de reentrada deben tener en cuenta el período de espera: un perfil no debe volver a entrar en el recorrido mientras ya está esperando

**Ventajas:**

- Reduce la mensajería innecesaria al comprobar la conversión automática
- Produce comunicaciones de mayor calidad y relevancia
- Admite casos de uso sensibles al tiempo con ventanas de retardo configurables
- Los criterios de salida permiten eliminar automáticamente el recorrido durante la conversión

**Limitaciones:**

- Complejidad de recorrido aumentada con nodos de espera y condición
- Los perfiles ocupan espacios en el recorrido durante los períodos de espera (sujeto al tiempo de espera de recorrido de 91 días)
- Requiere que el evento de conversión se introduzca en AEP dentro de la ventana de espera para realizar una evaluación precisa de la condición
- Mayor tiempo de entrega en comparación con la opción A

**Experience League:**

- [Actividad Esperar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Actividad de condición](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Criterios de salida](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)

### Opción C: activado por eventos con control de frecuencia

**Ideal para:** orígenes de eventos de alta frecuencia en los que la fatiga de mensajes es un problema: vistas de página, vistas de producto, consultas de búsqueda, adiciones repetidas al carro de compras. Se puede aplicar como superposición sobre la opción A o la opción B.

**Cómo funciona:**

Esta opción añade control de frecuencia a la Opción A o a la Opción B para evitar el exceso de mensajería. Los eventos de comportamiento de alta frecuencia (como las vistas de productos o las adiciones repetidas al carro de compras) pueden almacenar el recorrido en déclencheur varias veces en un corto período de tiempo. Sin control de frecuencia, un perfil podría recibir mensajes duplicados o excesivos.

El control de frecuencia se implementa mediante dos mecanismos complementarios: reglas empresariales de AJO (límites de frecuencia) que limitan la cantidad de mensajes que recibe un perfil por canal por periodo de tiempo y reglas de reentrada de nivel de recorrido que definen un periodo de reutilización antes de que un perfil pueda volver a entrar en el mismo recorrido. Las reglas empresariales funcionan en el nivel de organización y aplican límites en todas las campañas y recorridos (por ejemplo, un máximo de 3 correos electrónicos por semana), mientras que el reutilización de reentrada funciona en el nivel de recorrido individual (por ejemplo, un perfil no puede volver a introducir este recorrido específico en las 72 horas posteriores a la última entrada).

Además, la administración de recorridos y prioridades se puede configurar para asignar puntuaciones de prioridad al recorrido activado, lo que garantiza que, cuando varios conflictos o campañas compitan por el mismo perfil, gane la comunicación de mayor prioridad.

**Consideraciones clave:**

- Los límites de frecuencia deben equilibrar entre la prevención de la fatiga y la garantía de que se envíen mensajes activados importantes
- Se recomiendan límites específicos del canal: el correo electrónico, los SMS y las notificaciones push tienen umbrales de fatiga diferentes
- El tiempo de reutilización de la reentrada de recorrido y los límites de frecuencia a nivel de organización funcionan juntos; ambos deben configurarse
- Las puntuaciones de prioridad determinan qué comunicación gana cuando se alcanzan los límites: los recorridos de mayor prioridad deben recibir puntuaciones más altas

**Ventajas:**

- Evita la fatiga de mensajes por fuentes de eventos de alta frecuencia
- Mantiene la reputación de la marca y la satisfacción del suscriptor
- Los límites a nivel de organización proporcionan una red de seguridad en todas las campañas y recorridos
- La puntuación de prioridad garantiza que los mensajes más importantes se envíen cuando se alcanzan los límites

**Limitaciones:**

- Se suprimirán algunos perfiles cualificados y podrían faltar mensajes relevantes
- La configuración del límite de frecuencia añade complejidad administrativa
- Las mayúsculas pueden interactuar inesperadamente con otras campañas activas y recorridos que comparten el mismo canal
- Requiere una monitorización y un ajuste continuos a medida que cambia la cartera de mensajería

**Experience League:**

- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Información general sobre reglas comerciales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [administración de entradas de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)

### Comparación de opciones

En la tabla siguiente se comparan las tres opciones de implementación en función de criterios clave.

| Criterios | Opción A: simple activada por eventos | Opción B: condicional con espera | Opción C: control de frecuencia |
| --- | --- | --- | --- |
| Mejor para | Confirmaciones inmediatas, confirmaciones | Recuperación del abandono, respuestas condicionales retrasadas | Fuentes de eventos de alta frecuencia, entornos de varios recorridos |
| Complejidad | Baja | Medio | Medium-Alta (se añade a A o B) |
| Latencia del mensaje | De segundos a minutos | De minutos a horas/días (espera configurable) | Igual que la opción subyacente (A o B) |
| Comprobación de conversión automática | No | Sí (mediante condición o criterios de salida) | Depende de la opción subyacente |
| Protección de frecuencia | Ninguno (a menos que se combine con C) | Ninguno (a menos que se combine con C) | Sí: límites de canal y reutilización de reentrada |
| Nodos del lienzo de recorrido | 3-4 (evento, condición opcional, acción, fin) | 5-7 (evento, espera, condición, ramas, acción, fines) | Igual que A o B, más la configuración de regla de negocio |
| Requiere | Esquema de evento, superficie de canal, contenido de mensaje | Toda la opción A + la ingesta de eventos de conversión | Toda la configuración de la regla de frecuencia de la opción A o B + |

### Elija la opción correcta

Utilice la siguiente guía de decisión para seleccionar la opción de implementación correcta.

1. **¿Es necesario enviar el mensaje inmediatamente sin demora?** Si es así, comience con **Opción A**. Los mensajes de confirmación, los correos electrónicos de bienvenida y los reconocimientos no suelen requerir un período de espera.

2. **¿Debería el cliente tener tiempo para autoconvertir antes de recibir el mensaje?** Si es así, elija **Opción B**. Los casos de uso de abandono del carro de compras, abandono del explorador y caducidad de la prueba se benefician de un período de espera que permite a los clientes completar la acción por su cuenta.

3. **¿El evento de activación es de alta frecuencia (se produce varias veces por sesión o por día para el mismo perfil)?** Si es así, agrega **Opción C** como superposición sobre la Opción A o B. Las vistas de productos, las vistas de páginas y los eventos de búsqueda pueden generar grandes volúmenes de déclencheur que requieren protección de frecuencia.

4. **¿Hay varias campañas y recorridos activados activos en la zona protegida?** Si es así, agrega **Opción C** independientemente de la frecuencia del evento para administrar la carga de comunicación entre recorridos y evitar la fatiga del canal.

En la práctica, la mayoría de las implementaciones de producción utilizan la Opción B + C para casos de uso de estilo de abandono (espera condicional con control de frecuencia) y la Opción A + C para casos de uso de estilo de confirmación (envío inmediato con control de frecuencia como red de seguridad).

## Fases de implementación

Las siguientes fases recorren la implementación integral de la mensajería activada por eventos.

### Fase 1: Configurar el esquema de eventos y la recopilación de datos

**Función de aplicación:** AEP: Modelado de datos (F2), AEP: Fuentes de datos y colección (F3)

**Lo que configurará:** El esquema XDM ExperienceEvent que captura el evento de activación, el conjunto de datos que almacena estos eventos y la canalización de recopilación de datos en tiempo real (Web SDK, Mobile SDK o API de servidor) que transmite eventos a AEP. Esta fase establece la base de datos que el recorrido escuchará.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: desencadenando tipo de evento**
>
>¿Qué evento déclencheur el mensaje? El tipo de evento determina los campos de esquema necesarios y el método de recopilación.
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Evento de Commerce (adición al carro de compras, compra, cierre de compra) | Casos de uso de comercio electrónico: abandono del carro de compras, poscompra | Requiere un grupo de campos Commerce con `productListItems`, `cart`, `order` campos |
>| Evento de interacción web (vista de página, vista de producto) | Abandono de exploración, déclencheur de participación de contenido | Requiere un grupo de campos Detalles web con `webPageDetails`, `webInteraction` campos |
>| Evento de aplicación (instalación, desinstalación y acción en la aplicación) | Déclencheur de participación móvil | Requiere implementación de Mobile SDK y grupo de campos de aplicación |
>| Evento del sistema (error de pago, cambio de suscripción, actualización de estado) | Notificaciones operativas | Requiere API del lado del servidor o conector de origen para introducir eventos del sistema |
>| Evento de envío de formulario | Generación de posibles clientes, confirmación de inscripción | Requiere que el grupo de campos personalizados capture campos de datos de formulario |

>[!NOTE]
>
>**Decisión: método de colección**
>
>¿Cómo se capturará y transmitirá el evento de activación a AEP?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| SDK web | Eventos de comportamiento basados en web (adiciones al carro de compras, vistas de página, envíos de formularios) | Requiere la instalación de Web SDK en el sitio web; los eventos se transmiten en tiempo real mediante Edge Network |
>| SDK móvil | Eventos de aplicaciones móviles (aperturas de aplicaciones, acciones en aplicaciones, registro de tokens push) | Requiere la integración de Mobile SDK en la aplicación nativa o en el envoltorio de React Native |
>| API de servidor de Edge Network | Eventos del sistema del lado del servidor (procesamiento de pagos, administración de suscripciones, déclencheur back-end) | Sin dependencia del lado del cliente; eventos enviados desde los sistemas back-end de la organización |
>| Conector de Source | Eventos de sistemas externos (CRM, automatización de marketing, plataformas heredadas) | Normalmente basado en lotes; puede que no admita la activación en tiempo real a menos que sea posible la transmisión |

**Navegación de la interfaz de usuario:** Recopilación de datos > Flujos de datos > Nuevo flujo de datos (para la configuración del flujo de datos); Esquemas > Crear esquema (para esquema de evento); Conjuntos de datos > Crear conjunto de datos a partir de esquema (para creación de conjuntos de datos)

**Detalles de configuración de clave:**

- El esquema de evento debe incluir todos los campos necesarios para la evaluación de condiciones de recorrido y la personalización de mensajes
- La secuencia de datos debe tener los servicios [!DNL Adobe Experience Platform] y [!DNL Adobe Journey Optimizer] habilitados
- El conjunto de datos debe estar habilitado para el perfil del cliente en tiempo real, de modo que los eventos estén asociados a perfiles unificados
- Los datos de evento deben incluir un campo de identidad (correo electrónico, ID de CRM, ECID) que pueda resolverse en un perfil conocido

**Documentación de Experience League:**

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Información general sobre API de Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Resumen de ingesta de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview)

### Fase 2: Configuración de la identidad y el perfil

**Función de aplicación:** AEP: Configuración de identidad y perfil (F4)

**Lo que configurará:** Áreas de nombres de identidad para los identificadores en el evento de activación, designación de identidad principal en el esquema de evento, reglas de vinculación de identidad para la resolución entre dispositivos y una política de combinación para la unificación de perfiles. Esto garantiza que el evento de activación esté asociado a un perfil de cliente unificado para que el recorrido pueda resolver la información de contacto y enviar el mensaje.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: identidad principal para el esquema de evento**
>
>¿Qué campo de identidad en el evento de activación debe servir como identidad principal para la resolución de perfiles?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Correo electrónico | Eventos de sesiones web autenticadas o formularios donde se captura el correo electrónico | Resolución directa a una identidad contactable; ruta más sencilla para la entrega de correo electrónico |
>| ID de CRM | Eventos de sistemas autenticados donde el ID de CRM es el identificador principal | Requiere la creación del área de nombres de ID de CRM; el perfil debe tener un correo electrónico o un teléfono vinculado para la entrega de mensajes |
>| ECID (Experience Cloud ID) | Eventos anónimos de aplicaciones o web en los que no hay disponible una identidad autenticada | Requiere la vinculación de identidad para vincular ECID a una identidad conocida; los mensajes no se pueden enviar solo a ECID |
>| Número telefónico | Eventos de interacciones móviles o de centros de llamadas | Admite envío SMS; requiere área de nombres de teléfono |

**Navegación de la interfaz de usuario:** Identidades > Crear área de nombres de identidad; Esquemas > Seleccionar esquema > Seleccionar campo > Identidad > Establecer como identidad principal; Perfiles > Políticas de combinación

**Detalles de configuración de clave:**

- Los eventos anónimos (solo ECID) no pueden almacenar en déclencheur el envío de mensajes hasta que ECID esté vinculado a una identidad con la que se puede contactar (correo electrónico, teléfono) a través del gráfico de identidades
- La política de combinación utilizada por AJO debe ser coherente con la utilizada para la evaluación de audiencias
- Para la mensajería activada basada en web, asegúrese de que el gráfico de identidades vincula el ECID con identidades autenticadas a través de eventos de inicio de sesión

**Documentación de Experience League:**

- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Reglas de vinculación de gráficos de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Fase 3: Configuración de superficies de canal

**Función de aplicación:** AJO: Configuración de canal

**Lo que configurará:** La superficie de canal (ajuste preestablecido) que define la infraestructura de envío para el mensaje activado: delegación de subdominios, grupo de IP, identidad de remitente, dirección de respuesta, administración de cancelación de suscripción y credenciales específicas del canal (proveedor de SMS, certificados push). Debe existir una superficie de canal válida para poder crear contenido de mensaje o publicar recorridos.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: canal de mensajes**
>
>¿Qué canal utilizará el mensaje activado?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Correo electrónico | La mayoría de los casos de uso de mensajería activada: abandono, recuperación, confirmaciones, incorporación | Requiere delegación de subdominios, grupo de IP y configuración de remitente; admite contenido y personalización HTML enriquecidos |
>| SMS | Notificaciones con distinción de tiempo, alertas concisas y audiencias con una alta participación de SMS | Requiere la integración del proveedor de SMS (Sinch, Twilio, Infobip); sujeto a límites de caracteres y requisitos de consentimiento más estrictos |
>| Notificación push | Participación de aplicaciones móviles, renovación de la participación de usuarios de aplicaciones móviles | Requiere la configuración de credenciales push (APN para iOS, FCM para Android); el usuario debe tener la aplicación instalada con la funcionalidad push habilitada |
>| Varios canales | Estrategia de participación completa que utiliza preferencias de canal o lógica de reserva | Requiere varias superficies de canal; la selección de canal se puede administrar mediante nodos de condición de recorrido |

>[!NOTE]
>
>**Decisión: método de delegación de subdominios (correo electrónico)**
>
>¿Cómo se debe delegar el subdominio de envío de correo electrónico a Adobe?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Delegación completa | La organización desea que Adobe administre todos los registros DNS del subdominio de envío | Configuración más sencilla; Adobe administra el SPF, DKIM y DMARC graba automáticamente |
>| Delegación CNAME | La organización desea mantener el control DNS mientras señala a la infraestructura de Adobe | Requiere administración manual de registros DNS; proporciona más control organizativo sobre DNS |

**Navegación de la interfaz de usuario:** Administración > Canales > Subdominios (para la configuración de subdominios); Administración > Canales > Grupos de IP (para la configuración de grupos de IP); Administración > Canales > Superficies de canal > Crear superficie (para la creación de superficies)

**Detalles de configuración de clave:**

- La verificación del subdominio y la propagación de DNS pueden tardar hasta 48 horas
- Los nuevos grupos de IP requieren un plan de calentamiento (aumento gradual del volumen de 2 a 4 semanas)
- Configuración de encabezados de cancelación de suscripción de lista de un solo clic para el cumplimiento de correo electrónico
- Para SMS, configure las credenciales del proveedor antes de crear la superficie de canal de SMS
- Para push, configure APNS y credenciales de FCM antes de crear la superficie de canal push

**Documentación de Experience League:**

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Crear grupos de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Configuración de superficies de canal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fase 4: Creación del contenido del mensaje

**Función de aplicación:** AJO: Creación de mensajes

**Lo que configurará:** El contenido del mensaje que enviará el recorrido, incluido el diseño, los tokens de personalización que usan atributos de perfil y evento, bloques de contenido condicional, fragmentos reutilizables (encabezados, pies de página, exenciones de responsabilidad legal) y la vista previa y prueba de contenido.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: enfoque de contenido**
>
>¿Cómo se debe crear el contenido del mensaje?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Empezar desde una plantilla existente | Existen plantillas organizativas y se requiere coherencia de marca | La ruta más rápida a la creación de contenido; garantiza el cumplimiento de la marca; los cambios de plantilla se propagan a los nuevos mensajes |
>| Diseño desde cero en Email Designer | Se necesita un diseño personalizado para este mensaje activado específico | Control creativo total; editor visual de arrastrar y soltar; más lento pero más flexible |
>| Importar HTML | El contenido lo diseña un equipo o una agencia externa y se proporciona como HTML | Requiere experiencia en codificación de HTML; es posible que no admita completamente todas las funciones de Designer de correo electrónico |

>[!NOTE]
>
>**Decisión: personalización de eventos**
>
>¿Qué datos de evento deben utilizarse en el contenido del mensaje?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Atributos contextuales de evento | El mensaje debe incluir detalles del evento de activación (nombre del producto, valor del carro de compras, campos de formulario) | Utilice atributos de evento contextuales en el editor de personalización; los datos proceden de la carga útil del evento de activación |
>| Atributos de perfil | El mensaje debe incluir datos de nivel de perfil (nombre, nivel de fidelidad, ubicación) | Utilizar atributos de perfil a través de rutas XDM (por ejemplo, `profile.person.name.firstName`); los datos proceden del perfil unificado |
>| Atributos de evento y de perfil | El mensaje debe combinar el contexto de evento con la personalización del perfil | El método más común para los mensajes activados es garantizar la relevancia (evento) y la personalización (perfil) |

**Navegación de la interfaz de usuario:** Administración de contenido > Plantillas de contenido > Examinar (para la selección de plantillas); Acción de campaña o Recorrido > Editar contenido > Designer de correo electrónico (para el diseño de contenido); Seleccionar componente de texto > Icono de Personalization (para agregar personalización)

**Detalles de configuración de clave:**

- Utilice atributos contextuales para personalizar con los datos del evento de activación (por ejemplo, nombre del producto, valor del carro de compras)
- Usar atributos de perfil para datos de nombre, preferencias y fidelidad
- Configure bloques de contenido condicional para variar el contenido por segmento o atributo de perfil (por ejemplo, diferentes CTA para miembros socio)
- Cree fragmentos reutilizables para encabezados, pies de página y exenciones de responsabilidad legal compartidos entre mensajes activados
- Vista previa con varios perfiles de prueba para verificar que la personalización se procese correctamente
- Envíe pruebas a las partes interesadas internas antes de publicar el recorrido

**Documentación de Experience League:**

- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Fase 5: Creación y configuración del recorrido

**Función de la aplicación:** AJO: Journey Orchestration, AJO: Frecuencia y reglas empresariales (Opción C), AJO: Administración de conflictos y prioridades

**Lo que configurará:** El recorrido que escucha el evento desencadenante y organiza la entrega de mensajes. Esta es la fase de implementación central en la que el lienzo de recorrido está diseñado con el nodo de entrada de evento, los nodos de condición, los pasos de espera (para la opción B), los nodos de acción de mensaje y los criterios de salida. Esta fase también abarca la gobernanza de la frecuencia (opción C) y la configuración de conflictos/prioridades.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: reglas de reentrada**
>
>¿Puede un perfil volver a entrar en este recorrido si el evento de activación se vuelve a producir?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Permitir la reentrada (con reutilización) | El evento puede repetirse legítimamente y cada ocurrencia garantiza un mensaje (por ejemplo, cada abandono del carro de compras debe almacenar en déclencheur un mensaje de recuperación) | Establezca un período de tiempo de reutilización (mínimo 5 minutos) para evitar la reentrada rápida de eventos duplicados; el tiempo de reutilización habitual oscila entre 1 hora y 72 horas |
>| Sin reentrada | El mensaje solo debe enviarse una vez por perfil, independientemente de la periodicidad del evento (por ejemplo, mensaje de bienvenida después del primer registro) | El perfil se excluye permanentemente tras la finalización del primer recorrido; adecuado para mensajes únicos del ciclo vital |

>[!NOTE]
>
>**Decisión: duración de espera (solo opción B)**
>
>¿Cuánto tiempo debe esperar el recorrido antes de evaluar las condiciones y enviar el mensaje?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Espera corta (1-4 horas) | Casos de uso de alta urgencia, como abandono del carro de compras, en los que el seguimiento inmediato es eficaz | Mayor volumen de mensajes; es posible que atrape a algunos autoconvertidores; la mejor opción para la recuperación del carro de compras de alto valor |
>| Espera de Medium (12 a 24 horas) | Casos de uso de urgencia moderada como abandono de exploración o participación en el contenido | Enfoque equilibrado; reduce los envíos innecesarios sin perder relevancia |
>| Larga espera (2-7 días) | Casos de uso de baja urgencia, como recordatorios de caducidad de prueba o registros periódicos | Menor volumen de mensajes; mayor riesgo de perder relevancia contextual |
>| Fecha y hora personalizadas | Casos de uso vinculados a una fecha específica (por ejemplo, enviar 3 días antes de la fecha de caducidad del ensayo) | Esperar hasta una fecha/hora calculada; utiliza el editor de expresiones personalizado |

>[!NOTE]
>
>**Decisión: criterios de salida**
>
>¿En qué condiciones se debe eliminar un perfil de la recorrido antes de llegar a la acción de enviar mensajes?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Evento de conversión (por ejemplo, compra completada) | Abandono del carro de compras o del explorador donde el objetivo es la conversión | El perfil se cierra automáticamente cuando se detecta el evento de conversión; el método más limpio para la opción B |
>| Cambio de pertenencia a audiencia | El perfil debe cerrarse si abandona un segmento correspondiente | Requiere una audiencia evaluada por flujo continuo que se actualice en tiempo casi real |
>| tiempo de espera de recorrido (máximo de 91 días) | Comportamiento predeterminado: el perfil sale después de la duración máxima del recorrido | Red de seguridad; no debe ser el principal mecanismo de salida para recorridos de corta duración activados |
>| Sin criterios de salida explícitos | Confirmaciones simples (Opción A) en las que cada perfil correspondiente debe recibir el mensaje | El perfil se cierra naturalmente después de la acción del mensaje y del nodo final |

>[!NOTE]
>
>**Decisión: control de frecuencia (Opción C)**
>
>¿Cuántos mensajes activados debe recibir un perfil por periodo de tiempo?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Límites específicos del canal (por ejemplo, 3 correos electrónicos/semana, 1 SMS/día) | Los distintos canales tienen umbrales de fatiga diferentes | Método recomendado; respeta el nivel de intrusión de cada canal |
>| Límite global (por ejemplo, 5 mensajes/semana en todos los canales) | Gobernanza simplificada en todos los tipos de comunicación | Más fácil de administrar, pero con menos matices; puede restringir en exceso los canales menos intrusivos |
>| sólo reutilización de reentrada de nivel de recorrido | Gobernanza de frecuencias necesaria para este recorrido específico, pero no para toda la organización | La implementación más sencilla; no protege contra la fatiga entre recorridos |

**Navegación de la interfaz de usuario:** Recorridos > Crear Recorrido (para la creación de recorridos); lienzo del Recorrido > Arrastrar actividad de evento (para la entrada de eventos); lienzo del Recorrido > Arrastrar actividad &quot;Espera&quot; (para la configuración de espera); lienzo del Recorrido > Arrastrar actividad &quot;Condición&quot; (para la ramificación de condiciones); propiedades del Recorrido > Criterios de salida (para la configuración de salida); Administración > Reglas de negocio > Crear regla (para límites de frecuencia)

**Detalles de configuración de clave:**

- Configure el evento de recorrido seleccionando el esquema de evento y definiendo las condiciones de calificación
- Para la Opción B, agregue el nodo de espera inmediatamente después de la entrada de evento y antes de cualquier evaluación de condición
- Configurar nodos de condición mediante atributos de perfil, datos de evento o comprobaciones de pertenencia a audiencias
- Vincule el nodo de acción del mensaje a la superficie de canal y al contenido creado desde las fases 3 y 4
- Establezca el tiempo de espera de recorrido en una duración adecuada (inferior a 91 días para los recorridos activados)
- Para la opción C, cree reglas de frecuencia mediante Administration > Business rules antes de publicar el recorrido
- Asigne una puntuación de recorrido si otras campañas o recorridos se dirigen a audiencias superpuestas

**Donde las opciones difieren:**

**Para La Opción A (Activada Mediante Evento Simple):**
El lienzo de recorrido es mínimo: entrada de evento > condición de aceptación/consentimiento opcional > acción de mensaje > finalización. No hay pasos de espera ni comprobaciones de conversión. Establezca reglas de reentrada basadas en si el evento debe generar un mensaje cada vez que se produce.

**Para la opción B (condicional con espera):**
Agregue un nodo de espera después de la entrada del evento. Después de la espera, agregue un nodo de condición para comprobar la conversión (por ejemplo, compruebe si el evento `commerce.purchases` se produjo después de la entrada de recorrido) o utilice criterios de salida para quitar automáticamente los perfiles convertidos. Ramificar a la acción de mensaje en la ruta &quot;no convertida&quot; y a un nodo final en la ruta &quot;convertida&quot;.

**Para La Opción C (Control De Frecuencia):**
Configure los límites de frecuencia a nivel de organización mediante Administración > Reglas de negocio antes de publicar. Establezca el tiempo de reutilización de reentrada de nivel de recorrido en las propiedades del recorrido. De forma opcional, asigne una puntuación de recorrido a través de las propiedades de prioridad para controlar qué comunicación gana cuando se alcanzan los límites. Esto se puede aplicar sobre la opción A o la opción B.

**Documentación de Experience League:**

- [Creación de un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propiedades del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Eventos generales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Actividad de condición](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Actividad Esperar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Añadir un mensaje en un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Criterios de salida](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [administración de entradas de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificación de posibles conflictos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### Fase 6: Prueba e implementación del recorrido

**Función de aplicación:** AJO: Journey Orchestration

**Lo que configurará:** Validación del modo de prueba para comprobar que el recorrido se comporta como se espera con los perfiles de prueba, seguida de la publicación del recorrido para activarlo.

**Navegación de la interfaz de usuario:** Lienzo de Recorrido > Alternar el modo de prueba (para pruebas); Lienzo de Recorrido > Publicar (para implementación)

**Detalles de configuración de clave:**

- Habilite el modo de prueba en el lienzo de recorrido para simular déclencheur de evento con perfiles de prueba
- Seleccione perfiles de prueba que tengan información de contacto de canal válida (dirección de correo electrónico, número de teléfono)
- Almacene en déclencheur el evento de prueba y compruebe que el perfil de prueba recorre la ruta esperada
- Para la Opción B, compruebe que el paso de espera se comporta correctamente y que la evaluación de la condición produce la ramificación esperada
- Compruebe que los tokens de personalización se representan correctamente en el mensaje de prueba
- Tras realizar la prueba correctamente, publique el recorrido para activarlo
- Monitorice el estado de recorrido y las métricas de entrada de perfil inicial después de la publicación

**Documentación de Experience League:**

- [Prueba del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicación del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### Fase 7: Supervisar el rendimiento e informar sobre él

**Función de la aplicación:** AJO: Reporting &amp; Performance Analysis, S4: Monitoring &amp; Observability, S5: Reporting &amp; Analysis

**Lo que configurará:** informes de recorridos activos e históricos para la supervisión de la entrega y la participación, alertas de plataforma para la ingesta de eventos y errores de procesamiento de recorridos, y opcionalmente espacios de trabajo de CJA para un análisis más profundo en canales múltiples de la efectividad de la mensajería activada.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: profundidad del informe**
>
>¿Cuánto análisis de creación de informes se necesita para este caso de uso?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Solo informes nativos de AJO | La monitorización operativa de las métricas de envío es suficiente | Disponible inmediatamente; cubiertas enviadas, enviadas, devueltas, abiertas, pulsadas; no se necesita configuración adicional |
>| Integración de AJO nativo + CJA | Se necesitan análisis en canales múltiples, atribución de conversión y análisis de tendencias | Requiere conexión de CJA y vista de datos vinculada a conjuntos de datos de AJO; proporciona funciones analíticas más profundas |

**Navegación de la interfaz de usuario:** Recorridos > Seleccionar recorrido > Informe en vivo (para monitoreo en vivo); Recorridos > Seleccionar recorrido > Informe en todo momento (para análisis histórico); Alertas > Reglas de alerta > Suscribirse (para configuración de alerta)

**Detalles de configuración de clave:**

- Acceda al informe de recorrido activo durante la ejecución activa para monitorizar las entradas de perfil, las salidas y las métricas de envío
- Revise el informe histórico después de que el recorrido haya estado activo durante el tiempo suficiente para acumular datos significativos
- Configurar alertas para errores de ejecución de flujo de origen (ingesta de eventos) y retrasos en el procesamiento de recorrido
- Para la integración de CJA, asegúrese de que la conexión de CJA incluye conjuntos de datos de evento de experiencia de AJO (conjunto de datos de evento de comentarios de mensajes, conjunto de datos de evento de experiencia de seguimiento de correo electrónico)

**Documentación de Experience League:**

- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Consideraciones sobre la implementación

Esta sección abarca protecciones, escollos comunes, prácticas recomendadas y decisiones de compensación para implementaciones de mensajería activadas por eventos.

### Protecciones y límites

Las siguientes protecciones y límites de la plataforma se aplican a las implementaciones de mensajería activadas por eventos.

- **Rendimiento de evento unitario:** Máximo de 5000 eventos por segundo por zona protegida para recorridos de evento unitarios: [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- **Límite de recorrido activo:** Un máximo de 500 recorridos activos por espacio aislado — [Protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- **Límite de lienzo de Recorrido:** Un máximo de 50 actividades por lienzo de recorrido
- **tiempo de espera de Recorrido:** La duración máxima de recorrido es de 91 días (tiempo de espera global)
- **Reutilización de reentrada:** El reutilización mínimo de reentrada es de 5 minutos
- **Configuraciones de límite de frecuencia:** Máximo de 10 configuraciones de límite por zona protegida
- **Superficies de canal:** Máximo de 10 superficies de canal por tipo de canal por zona protegida
- **Ingesta de transmisión:** Un máximo de 20.000 registros por segundo por conexión HTTP — [Protecciones de ingesta](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- **Atributos calculados:** Máximo de 25 atributos calculados por zona protegida — [Protecciones de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview#guardrails)
- **Fragmentos de contenido:** Un máximo de 30 fragmentos de contenido por mensaje
- **Actualización de informe activo:** Los informes activos se actualizan cada 60 segundos y muestran las últimas 24 horas de datos
- **Latencia histórica del informe:** Los informes históricos (todos los tiempos) pueden tardar hasta dos horas en completarse una vez finalizada la ejecución

### Peligros comunes

Tenga en cuenta los siguientes problemas comunes al implementar la mensajería activada por eventos.

- **Eventos anónimos sin resolución de identidad:** Los eventos desencadenadores que solo llevan un ECID (ID de cookie anónimo) no se pueden resolver en un perfil con el que se puede establecer contacto para la entrega de mensajes. Asegúrese de que el evento de activación incluya una identidad autenticada o que el gráfico de identidades vincule el ECID a un contacto conocido. Sin resolución de identidad, los perfiles entran en el recorrido pero fallan en el paso de entrega de mensajes.

- **Falta el evento de conversión para las comprobaciones de condiciones de la opción B:** Si el evento de conversión (por ejemplo, la compra) no se incorpora en AEP o no está asociado con la misma identidad de perfil que el evento de activación, la comprobación de condiciones se evaluará incorrectamente como &quot;no convertido&quot; y enviará mensajes innecesarios. Compruebe que los eventos de conversión fluyen a AEP en tiempo real y comparta una identidad con el evento de activación.

- **Reglas de reentrada excesivamente permisivas:** Si se permite la reentrada sin un período de tiempo de reutilización en orígenes de eventos de alta frecuencia, el mismo perfil puede recibir varios mensajes en cuestión de minutos. Establezca siempre un tiempo de reutilización de reentrada que coincida con el contexto empresarial (por ejemplo, un tiempo de reutilización de 4 horas para el abandono del carro de compras o de 24 horas para el abandono del explorador).

- **Desalineación de zona horaria de paso de espera:** Los pasos de espera se procesan en UTC de forma predeterminada. Si el recorrido se dirige a perfiles en varias zonas horarias y la espera debe coincidir con la hora local del destinatario, configure las opciones de zona horaria en el recorrido en consecuencia.

- **Límites de frecuencia en conflicto con otras campañas:** Los límites de frecuencia a nivel de organización se aplican a todas las campañas y recorridos. Un nuevo recorrido activado puede suprimirse si los perfiles ya han alcanzado su límite de otras campañas activas. Monitorice la tasa de supresión y ajuste las puntuaciones de prioridad para garantizar que se dé prioridad a los mensajes activados importantes.

- **Error de publicación de Recorrido debido a la falta de dependencias:** Cada rama del lienzo de recorrido debe finalizar con una actividad de finalización. Todos los nodos de acción deben hacer referencia a superficies de canal válidas con contenido de mensaje activo. Compruebe todas las dependencias antes de publicar.

### Prácticas recomendadas

Siga estas recomendaciones para implementaciones de mensajería activadas por eventos exitosas.

- **Empiece por el modo simple y, a continuación, itere:** Empiece por la opción A para los nuevos casos de uso de mensajería activada. Agregue la lógica de espera y condición (Opción B) solo después de validar la canalización de eventos y la entrega de mensajes. Añada la gobernanza de frecuencias (Opción C) cuando haya varios recorridos activados activos.

- **Use criterios de salida en lugar de nodos de condición para las comprobaciones de conversión:** Los criterios de salida quitan automáticamente los perfiles de la recorrido cuando se produce un evento calificado (por ejemplo, una compra), lo que elimina la necesidad de un nodo de condición explícito después del paso de espera. Esto genera un lienzo de recorrido más limpio y una detección de conversión más adaptable.

- **Realizar pruebas con datos de evento reales en una zona protegida de desarrollo:** Use el modo de prueba con cargas útiles de evento reales (no solo perfiles de prueba) para validar que los campos de esquema de evento, los tokens de personalización y las expresiones de condición funcionen correctamente con datos de tipo de producción.

- **Establecer reinicios de reentrada específicos del evento:** Hacer coincidir el período de reutilización con el contexto empresarial del evento desencadenante. Los recorridos de abandono del carro de compras suelen utilizar un tiempo de reutilización de 4 a 24 horas; los recorridos de confirmación pueden permitir la reentrada inmediata; los recorridos de incorporación deben evitar la reentrada por completo.

- **Supervise la tasa de supresión como métrica de estado:** Si la tasa de supresión (perfiles que cumplen los requisitos pero no reciben mensajes debido a límites o condiciones de frecuencia) supera el 30-40%, compruebe si los límites son demasiado restrictivos o si el evento de activación está definido con demasiada amplitud.

- **recorridos de versión en lugar de editar los activos:** Un recorrido activo no se puede editar directamente. Cree una nueva versión duplicando el recorrido, realizando cambios, deteniendo la versión antigua y publicando la nueva. Esto evita interrumpir los perfiles que se encuentran actualmente en el recorrido.

- **Incluir una ruta de acceso de reserva/predeterminada en los nodos de condición:** Configurar siempre una ruta de acceso predeterminada (else) en los nodos de condición para controlar estados de perfil inesperados. Los perfiles que no coinciden con ninguna rama de condición deben cerrarse correctamente en lugar de permanecer atascados.

### Decisiones de compensación

Tenga en cuenta los siguientes trucos al diseñar su implementación de mensajería activada por eventos.

>[!NOTE]
>
>**Compensación: velocidad del mensaje vs. relevancia del mensaje**
>
>La entrega inmediata de mensajes (Opción A) maximiza la velocidad, pero puede enviar mensajes a clientes que se habrían convertido a sí mismos. La entrega condicional retrasada (Opción B) mejora la relevancia al filtrar los autoconvertidores, pero introduce una latencia que puede reducir la urgencia.
>
>- **La opción A favorece:** Casos de uso de estilo de confirmación, simplicidad y velocidad en los que cada evento garantiza un mensaje
>- **La opción B favorece:** Relevancia, fatiga reducida en los mensajes, casos de uso de estilo de abandono en los que la conversión automática es común
>- **Recomendación:** Utilice la opción A para los mensajes transaccionales y de confirmación en los que la velocidad es el valor principal. Utilice la opción B para los mensajes de recuperación y renovación de la participación en los que la relevancia supera la velocidad. Experimente con las duraciones de espera para encontrar el equilibrio óptimo para cada caso de uso.

>[!NOTE]
>
>**Compensación: protección de frecuencia frente a cobertura de mensaje**
>
>Los límites de frecuencia estrictos (Opción C) evitan la fatiga, pero pueden suprimir mensajes activados importantes cuando los perfiles están cerca de su límite. Los límites permisivos o nulos maximizan la cobertura, pero suponen un riesgo de mensajería excesiva y fatiga del canal.
>
>- **Ventajas estrictas:** Experiencia del cliente, reputación de la marca, capacidad de envío (menos quejas por correo no deseado)
>- **Mayúsculas permisivas a favor:** Cobertura de mensajes, oportunidades de conversión, evitar déclencheur perdidos
>- **Recomendación:** Comience con límites estándar del sector (de 3 a 5 correos electrónicos por semana, de 1 a 2 SMS por semana, de 2 a 3 push/día) y ajuste según las métricas de participación y las tasas de cancelación de suscripción. Asigne puntuaciones de prioridad más altas a los mensajes activados para que ganen en campañas por lotes cuando se alcancen los límites.

>[!NOTE]
>
>**Compensación: simplicidad de Recorrido vs. sofisticación de recorrido**
>
>Los recorridos simples (pocos nodos, sin ramas) son más fáciles de crear, probar y mantener, pero ofrecen una adaptación contextual limitada. Los recorridos sofisticados (varias condiciones, rutas de ramificación, comprobaciones de segmentos) permiten respuestas más matizadas, pero aumentan la complejidad y el riesgo de errores.
>
>- **Los recorridos simples favorecen:** implementación más rápida, depuración más sencilla, menor carga de mantenimiento
>- **Los recorridos sofisticados favorecen:** Un direccionamiento más preciso, una mejor personalización y envíos innecesarios reducidos
>- **Recomendación:** Comience con el recorrido más sencillo que cumpla los requisitos empresariales. Agregar complejidad de forma incremental en función de los datos de rendimiento. Un recorrido simple que funciona de forma fiable es más valioso que un recorrido complejo con errores no detectados.

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las capacidades utilizadas en esta implementación.

### orquestación de recorrido

- [Introducción a recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Creación de un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propiedades del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Eventos generales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de calificación de público](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Actividad de condición](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Actividad Esperar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Añadir un mensaje en un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Criterios de salida](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [administración de entradas de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Prueba del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicación del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Crear grupos de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [planes de calentamiento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configuración de superficie de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Administrar lista de supresión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Creación y personalización de mensajes

- [Crear un correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funciones de ayuda](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Creación de un mensaje SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Diseño de una notificación push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### Frecuencia y reglas empresariales

- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Información general sobre reglas comerciales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [API de límite](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/channel-surfaces/capping)

### Administración de conflictos y prioridades

- [Introducción a la administración de conflictos y prioridades](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Identificación de posibles conflictos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [restricción y arbitraje de recorridos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### Creación de informes y rendimiento

- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### Recopilación e ingesta de datos

- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Información general de Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Información general sobre API de Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Resumen de ingesta de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview)

### Modelado de datos y esquemas

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### Identidad y perfil

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Reglas de vinculación de gráficos de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Resumen del perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Segmentación y audiencias

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)

### Gobernanza de datos y consentimiento

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Grupo de campos de consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Atributos calculados

- [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Guía de IU de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)

### Monitorización y observabilidad

- [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones de ingesta](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### Tutoriales y guías

- [Tutorial sobre Creación de un recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Instalación de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
