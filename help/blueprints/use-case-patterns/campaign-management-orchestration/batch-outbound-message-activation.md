---
title: Activación de mensaje saliente por lotes
description: Obtenga información sobre cómo evaluar una audiencia y enviar un mensaje saliente programado en una sola ejecución por lotes.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '8246'
ht-degree: 1%

---


# Activación de mensaje saliente por lotes

Esta guía proporciona una referencia de implementación completa para enviar mensajes salientes programados a segmentos de audiencia definidos mediante [!DNL Adobe Journey Optimizer] (AJO) y [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP). Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten comprender todos los enfoques de implementación viables, las consideraciones de decisión que impulsan cada opción y dónde encontrar la documentación detallada sobre [!DNL Adobe Experience League].

La activación de mensajes salientes por lotes es el patrón de campaña básico para la mensajería saliente de uno a varios. Abarca todo el ciclo de vida, desde la definición de la audiencia hasta la entrega de mensajes y el análisis de rendimiento. Esta guía presenta tres opciones de implementación (Campaña programada, Recorrido activado por la audiencia y Campaña activada por la API) y proporciona una guía de decisión estructurada para seleccionar el enfoque adecuado para cada caso de uso.

Proporciona opciones de implementación, análisis de compensación, rutas de navegación de interfaz de usuario y referencias de documentación de [!DNL Experience League].

## Resumen del caso de uso

Con frecuencia, las organizaciones necesitan enviar un solo mensaje a un segmento de audiencia conocido en un momento específico o en respuesta a un evento del sistema. Este patrón resuelve ese requisito combinando la evaluación de audiencias en [!DNL RT-CDP] con la creación de mensajes y la ejecución de campañas en [!DNL Journey Optimizer].

El escenario empresarial es sencillo: defina quién debe recibir el mensaje, cree el contenido del mensaje con personalización, vincule la audiencia y el mensaje a una campaña o recorrido y ejecute el envío según una programación, mediante calificación de audiencia o a través de un déclencheur del sistema. El resultado es un mensaje enviado con informes completos sobre las métricas de entrega, participación y conversión.

Este patrón se aplica siempre que se puede avanzar en un objetivo empresarial enviando un solo mensaje a una audiencia conocida en una ejecución. Se diferencia de la mensajería activada por eventos, que responde a eventos de comportamiento en tiempo real, y de los recorridos organizados de varios pasos, que guían los perfiles a través de varios puntos de contacto a lo largo del tiempo. La activación por lotes es el patrón de campaña más sencillo y el punto de partida más común para los casos de uso de mensajería saliente.

## Objetivos empresariales clave

Esta sección identifica los objetivos comerciales principales que admite la activación de mensajes salientes por lotes.

### Aumentar la participación en campañas y correos electrónicos

**Descripción:** mejore las tasas de apertura, las tasas de pulsaciones y la respuesta general de la campaña mediante el contenido optimizado y el direccionamiento.

**KPI:** tasas de apertura, participación, tasas de conversión

### Aumentar ingresos y ventas

**Descripción:** Impulse el crecimiento de los ingresos de primera línea a través de canales digitales optimizados, campañas y recorridos de clientes.

**KPI:** tasas de conversión, ingresos incrementales, valor de pedido promedio

**Objetivo comercial relacionado:** [Aumentar ingresos y ventas](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

### Optimización de la ejecución de campañas

**Descripción:** Reduzca el tiempo de compilación de la campaña y simplifique la entrega de campañas multicanal a través de plantillas, automatización y procesos estandarizados.

**KPI:** velocidad de comercialización, eficiencia, tiempo de finalización %

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran aplicaciones comunes de la activación de mensajes salientes por lotes.

- **Anuncio de venta o explosión de correo electrónico promocional** — Difunde una oferta promocional a un segmento de clientes elegibles en una fecha programada
- **Notificación push de lanzamiento del producto** — Notificar a los clientes interesados sobre la disponibilidad de un nuevo producto mediante notificación push
- **Boletín o correo electrónico de resumen** — Enviar resúmenes de contenido periódicos a las audiencias de los suscriptores
- **Invitación de registro de evento** — Invite a posibles clientes calificados a seminarios web, conferencias o eventos presenciales
- **Correo electrónico de recordatorio de renovación de suscripción**: recuerde a los clientes que se acercan a las fechas de renovación que deben tomar medidas
- **Notificación de hito del programa de fidelización**: felicite a los miembros que alcanzan niveles de fidelidad o umbrales de puntos
- **Correo electrónico específico de call-to-action**: Impulse una acción de destino como completar una compra, actualizar las preferencias o registrarse en un programa
- **Campaña de SMS para venta flash u oferta por tiempo limitado** — Envíe promociones urgentes por tiempo limitado a través de SMS a audiencias de inclusión

## Indicadores clave de rendimiento

En la tabla siguiente se definen los KPI utilizados para medir la eficacia de la campaña.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de entrega | Porcentaje de mensajes enviados correctamente a los destinatarios | Entregado/enviado x 100 |
| Tasa de apertura | Porcentaje de mensajes enviados abiertos por los destinatarios | Aperturas únicas / Entregas x 100 |
| Tasa de clics (CTR) | Porcentaje de mensajes entregados en los que se hizo clic en un vínculo | Clics únicos / Entregados x 100 |
| Tasa de pulsaciones para abrir (CTOR) | Porcentaje de mensajes abiertos en los que se hizo clic en un vínculo | Clics únicos/Aperturas únicas x 100 |
| Tasa de conversión | Porcentaje de destinatarios que completaron la acción deseada | Conversiones / Entregado x 100 |
| Tasa de cancelación de suscripción | Porcentaje de destinatarios que cancelaron la suscripción después de recibir el mensaje | Cancelaciones de la suscripción/Entregas x 100 |
| Tasa de devoluciones | Porcentaje de mensajes que no se han podido entregar | Devoluciones / Enviados x 100 |
| Ingresos por correo electrónico enviado | Ingresos atribuidos a la campaña divididos por los mensajes enviados | Ingresos totales / Enviados |

## Patrón de caso de uso

**Activación de mensaje saliente en lote**

Evalúe una audiencia y luego envíe un mensaje saliente programado (correo electrónico, SMS, push) a todos los perfiles aptos en una sola ejecución por lotes.

**Cadena de funciones:** Evaluación de audiencias > Creación de mensajes > Ejecución de campañas > Informes

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón.

- **[!DNL Adobe Journey Optimizer] (AJO)**: creación de mensajes, configuración de canal, ejecución de campañas, orquestación de recorrido, experimentación de contenido, reglas de frecuencia y generación de informes
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)**: evaluación de audiencias, cumplimiento de consentimiento y gobernanza
- **[!DNL Adobe Experience Platform] (AEP)**: almacén de perfiles, servicio de identidad, esquemas, conjuntos de datos, recopilación de datos

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Se asume en contexto | La zona protegida de AJO está aprovisionada con una configuración de canal activa. Envío de subdominios delegados, grupo de IP asignado y calentamiento de IP completo. Roles de usuario con permisos de creación de recorrido/campaña asignados. | [Resumen de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home), [Resumen de control de acceso](https://experienceleague.adobe.com/es/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | Esquema de perfil individual de XDM con atributos utilizados para la segmentación y personalización (por ejemplo, nombre, correo electrónico, preferencias, nivel). El esquema XDM ExperienceEvent captura la acción de conversión de destino (por ejemplo, `commerce.purchases`, `web.webInteraction`) para el seguimiento de conversión posterior a la campaña. Conjuntos de datos habilitados para perfil para ambos esquemas. | [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home), [Conceptos básicos de composición de esquemas](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/composition) |
| Fuentes de datos y recopilación | Se asume en contexto | El etiquetado de Web SDK o Analytics en el destino de CTA debe estar activo para capturar eventos de conversión. Las canalizaciones de flujo continuo o ingesta por lotes para atributos de perfil deben estar operativas. | [Información general de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home), [Resumen de orígenes](https://experienceleague.adobe.com/es/docs/experience-platform/sources/home) |
| Configuración de identidad y perfil | Se asume en contexto | Áreas de nombres de identidad para correo electrónico (y cualquier identificador entre dispositivos) configurado. Atributos de perfil necesarios para la personalización asignados, ingeridos y solucionables en el momento del envío. Política de combinación configurada. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home), [Introducción a las políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview) |
| Definición de audiencia y segmentación | Requerido | Audiencia de destino definida en RT-CDP mediante el Generador de segmentos o la Composición de audiencias. Audiencia publicada y evaluada con una población distinta de cero. Cubierto en la Fase de implementación 1 mediante la Evaluación de audiencia de RT-CDP. | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home), [Guía de la interfaz de usuario del generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Los atributos calculados, como los días transcurridos desde la última compra, el recuento de pedidos acumulados o la puntuación de participación, mejoran la precisión de la audiencia y permiten una mayor personalización del mensaje. | [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview) |
| Administración del ciclo de datos | Recomendado | Las políticas de retención de datos (caducidad) deben estar implementadas para los conjuntos de datos de evento que controlan el seguimiento de conversiones. Los campos de esquema de consentimiento deben configurarse para la aplicación de inclusión/exclusión a nivel de canal. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/home), [grupo de campos de preferencias y consentimiento](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/field-groups/profile/consents) |
| Etiquetado y aplicación del uso de datos | Recomendado | Las etiquetas de gobernanza en los campos PII utilizados en la personalización garantizan el cumplimiento durante la activación. Evita el uso no autorizado de datos de perfil confidenciales en el contenido del mensaje o en las exportaciones de audiencia. | [Resumen de control de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home), [Resumen de etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview) |
| Monitorización y observabilidad | Incluido | La monitorización de envíos en tiempo real forma parte de la fase de Creación de informes. Las alertas a nivel de plataforma sobre errores de ingesta o uso de licencias proporcionan visibilidad operativa más allá de las métricas a nivel de campaña. | [Resumen de Observability Insights](https://experienceleague.adobe.com/es/docs/experience-platform/observability/home), [Resumen de alertas](https://experienceleague.adobe.com/es/docs/experience-platform/observability/alerts/overview) |
| Informes y análisis | Incluido | Los informes de campaña y recorrido se tratan en la fase Creación de informes. Para un análisis más profundo entre canales, la integración de CJA proporciona análisis de funnel, modelado de atribución y análisis de cohorte más allá de los informes integrados de AJO. | [descripción general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview), [guía de integración de AJO + CJA](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Journey Optimizer] (AJO)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Configuración de canal | Fase 2: Configuración de canal | Configure o valide la superficie de canal (correo electrónico, SMS o push), incluidos el subdominio, el grupo de IP, la configuración del remitente y la lista de supresión |
| Creación de mensajes | Fase 3: Creación de mensajes | Cree contenido de mensaje con plantillas, Email Designer, expresiones de personalización, bloques de contenido condicional y fragmentos de contenido |
| Ejecución de campaña | Fase 4: Creación de campañas o Recorridos | Cree, configure y active una campaña programada o activada por API que enlace la audiencia, el mensaje y la programación de ejecución |
| Experimentación de contenido | Fase 4: Creación de campañas o Recorridos | Si lo desea, puede configurar experimentos de contenido A/B o multivariable para optimizar el rendimiento del mensaje |
| Frecuencia y reglas comerciales | Fase 4: Creación de campañas o Recorridos | Opcionalmente, aplique reglas de límite de frecuencia para evitar el exceso de mensajes en las campañas simultáneas |
| Administración de conflictos y prioridades | Fase 4: Creación de campañas o Recorridos | Asigne puntuaciones de prioridad y configure la resolución de conflictos cuando varias campañas se dirijan a audiencias superpuestas |
| Informes y análisis de rendimiento | Fase 5: Informes y análisis de rendimiento | Monitorice las métricas de entrega a través de informes en vivo durante la ejecución y analice el rendimiento de la campaña a través de informes históricos una vez finalizados |

### [!DNL Real-Time CDP] (RT-CDP)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Evaluación de audiencia | Fase 1: Evaluación de audiencias | Defina las reglas de audiencia mediante el Generador de segmentos o la Composición de audiencia, seleccione el método de evaluación (por lotes, streaming o Edge) y valide la población de audiencias |
| Cumplimiento del consentimiento y la gobernanza | Fase 1: Evaluación de audiencias | Aplicar preferencias de consentimiento y políticas de uso de datos para garantizar que solo los perfiles consentidos reciban el mensaje de la campaña |

## Prerrequisitos

Complete lo siguiente antes de comenzar la implementación.

- La zona protegida de AJO está aprovisionada y activa
- El envío del subdominio está delegado y verificado (SPF, DKIM, DMARC configurado)
- El grupo de IP se asigna y calienta para el volumen de envío de producción
- Existe al menos una superficie de canal activa (correo electrónico, SMS o push)
- Las cuentas de usuario tienen permisos de creación de campañas/recorridos y contenido
- El esquema de perfil XDM incluye atributos necesarios para la segmentación de audiencias y la personalización de mensajes
- El esquema de eventos XDM captura eventos de conversión para el seguimiento posterior a la campaña
- Los datos de perfil se incorporan y unifican mediante el servicio de identidad
- El etiquetado de Web SDK o Analytics está activo en la página de destino de CTA para capturar eventos de conversión
- Los campos de consentimiento se rellenan en perfiles para el canal de mensajería de destinatario
- Los activos de contenido (imágenes, logotipos, directrices de marca) están disponibles para el diseño de mensajes

## Opciones de implementación

En esta sección se describen tres opciones de implementación para la activación de mensajes salientes por lotes, junto con una guía de comparación y decisión.

### Opción A: campaña programada (envío único por lotes)

**Ideal para:** Envíos con fecha fija: anuncios de venta, lanzamientos de productos, plazos de registro de eventos, recordatorios de renovación, voladuras de boletines informativos y cualquier envío en el que se conozca de antemano la fecha de ejecución.

**Cómo funciona:**

Una campaña programada es la variante más sencilla de la mensajería saliente por lotes. El especialista en marketing define la audiencia de destino, crea el contenido del mensaje, establece una fecha y una hora de envío y activa la campaña. En el momento de la ejecución programada, AJO evalúa la audiencia para determinar la población apta actual y, a continuación, envía el mensaje a todos los perfiles aptos en un solo lote.

Toda la configuración se realiza en la interfaz de AJO Campaign: no hay lienzo de recorrido, lógica de ramificación ni pasos de espera. Esto hace que las campañas programadas sean las más rápidas de configurar y las más fáciles de administrar. La campaña se puede configurar para una ejecución inmediata, una fecha/hora futura específica o una programación recurrente (diaria, semanal, mensual).

**Consideraciones clave:**

- La audiencia se evalúa en el momento de la ejecución, por lo que se incluyen los perfiles que se clasifican entre la programación y la ejecución
- No hay disponible ninguna lógica de ramificación, espera o condición: el mensaje se envía a todos los perfiles aptos
- Admite la experimentación de contenido (pruebas A/B) directamente en la configuración de la campaña
- Las propiedades de campaña incluyen una puntuación de prioridad para la resolución de conflictos con otras campañas

**Ventajas:**

- La configuración más sencilla con menos sobrecarga
- El tiempo de inicio más rápido para envíos directos por lotes
- Compatibilidad integrada con programas recurrentes
- Experimentación de contenido admitida de forma nativa
- Audiencia reevaluada en el momento de la ejecución por motivos de actualización

**Limitaciones:**

- Sin pasos de espera, condiciones ni ramas antes del envío
- No se puede reaccionar al comportamiento del perfil entre la programación y la ejecución
- Solo acción de mensaje único: sin secuencias multitáctiles
- No se puede editar una vez activado (debe duplicarse y modificarse)

**Experience League:**

- [Introducción a las campañas](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

### Opción B: recorrido activado por la audiencia

**Es ideal para:** envíos basados en el comportamiento: notificaciones de carros de compras abandonados, recordatorios de caducidad de pruebas, celebraciones de hitos, alcance basado en calificaciones y cualquier envío en el que el déclencheur sea una calificación de audiencia o un evento empresarial en lugar de una fecha programada.

**Cómo funciona:**

Un recorrido activado por la audiencia utiliza el lienzo de recorrido para enviar un mensaje cuando un perfil cumple los requisitos para una audiencia definida o activa un evento correspondiente. La entrada de recorrido se activa por cambios de miembros de audiencia (perfiles que entran en la audiencia) en lugar de una programación fija. El lienzo de recorrido permite pasos de espera opcionales, ramas de condición y lógica de supresión antes de la acción del mensaje, lo que proporciona más flexibilidad que una campaña programada.

El recorrido se configura en la interfaz de Recorridos de AJO mediante el evento de entrada Leer audiencia. Cuando los perfiles cumplen los requisitos para la audiencia, entran en el recorrido y continúan a través de los nodos de lienzo. Una implementación sencilla puede contener un solo nodo de acción de correo electrónico, lo que la hace funcionalmente similar a una campaña programada, pero con un tiempo de entrada basado en la calificación de audiencia. Las implementaciones más complejas pueden agregar nodos de espera (por ejemplo, esperar 24 horas después de la calificación), nodos de condición (por ejemplo, comprobar si el perfil abrió un correo electrónico anterior) o lógica de supresión antes de la entrega de mensajes.

**Consideraciones clave:**

- La entrada de recorrido se activa por la calificación de audiencia, no por una fecha de calendario
- El lienzo de recorrido admite nodos de espera, condición y división para la lógica previa al envío
- Las reglas de reentrada de recorrido controlan si los perfiles pueden entrar en la recorrido varias veces
- La configuración de mediación de recorrido determina la conducta cuando un perfil ya está en un recorrido de la competencia

**Ventajas:**

- Horario de entrada flexible basado en la calificación de audiencias en lugar de en un horario fijo
- Los nodos de espera y condición permiten la lógica previa al envío (por ejemplo, retrasar, comprobar, suprimir)
- Los controles de reentrada impiden los envíos duplicados al mismo perfil
- Se puede ampliar a un recorrido de varios pasos si el caso de uso evoluciona
- Admite informes de nivel de recorrido con métricas de nivel de entrada, salida y nodo

**Limitaciones:**

- Más sobrecarga de configuración que una campaña programada
- El lienzo de recorrido añade complejidad incluso para casos de uso de un solo mensaje
- El recorrido debe publicarse y no puede editarse mientras esté activo (debe crear una nueva versión)
- El límite de entrada puede limitar el número de perfiles que se introducen en un intervalo de tiempo

**Experience League:**

- [Introducción a recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Leer recorrido de audiencia](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

### Opción C: campaña activada por API

**Ideal para:** envíos iniciados por el sistema: confirmación de pedido con contenido de ampliación de venta, seguimiento de resolución de tickets de asistencia, notificaciones transaccionales con contenido de marketing y cualquier envío en el que el evento de activación se origine desde un sistema externo en un momento específico.

**Cómo funciona:**

Una campaña activada por API se activa mediante una llamada a la API de REST en el momento en que se produce un evento del sistema que la activa. La campaña está preconfigurada en AJO con contenido de mensaje y configuración de canal, pero en lugar de enlazar una audiencia predefinida, la llamada de API especifica los perfiles de destinatario y puede pasar datos contextuales que rellenan parámetros de mensaje dinámico.

Esta variante es ideal cuando el tiempo de envío está determinado por un sistema externo (por ejemplo, un sistema de gestión de pedidos, un flujo de trabajo CRM o una plataforma de soporte) en lugar de por una evaluación de audiencia o una programación de calendario. Los datos contextuales pasados en la carga útil del déclencheur de API, como detalles de pedidos, números de vale o nombres de productos, pueden personalizar el contenido del mensaje mediante atributos contextuales que no se almacenan en el perfil.

**Consideraciones clave:**

- No se requiere ninguna audiencia enlazada previamente: los destinatarios se especifican en la solicitud de déclencheur de la API
- Los datos contextuales en la carga útil de déclencheur permiten la personalización dinámica más allá de los atributos de perfil
- La campaña debe ser de tipo &quot;activada por API&quot; y debe activarse antes de poder recibir solicitudes de déclencheur
- Cada solicitud de déclencheur de API admite hasta 20 destinatarios de perfil
- La Evaluación de audiencias (fase 1) se puede omitir porque los destinatarios proceden de la llamada de API

**Ventajas:**

- Activación en tiempo real desde sistemas externos en el momento del evento
- Personalización contextual con datos no almacenados en el perfil (detalles del pedido, información del ticket)
- Sin sobrecarga de evaluación de audiencia: los destinatarios se especifican directamente
- Admite mensajería transaccional + marketing híbrida

**Limitaciones:**

- Requiere integración de sistema externo para enviar el déclencheur de API
- Máximo de 20 destinatarios por solicitud de déclencheur de API
- Sin evaluación de audiencia integrada: el sistema de llamada debe determinar los destinatarios
- Mayor complejidad técnica debido a los requisitos de integración de API
- La experimentación de contenido no es compatible con campañas activadas por API

**Experience League:**

- [Campañas activadas por API](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)
- [Déclencheur de campañas mediante API](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### Comparación de opciones

En la tabla siguiente se comparan las tres opciones de implementación en función de criterios clave.

| Criterios | Opción A: Campaña Programada | Opción B: Recorrido activado por la audiencia | Opción C: campaña activada por API |
| --- | --- | --- | --- |
| Mejor para | Envíos anclados por fecha (promociones, lanzamientos, boletines) | Envíos impulsados por el comportamiento (eventos de calificación, hitos) | Envíos iniciados por el sistema (confirmaciones de pedidos, transaccionales) |
| Complejidad | Baja | Medio | Medium-High |
| tipo de déclencheur | Fecha/hora del calendario o programación recurrente | Calificación de audiencias o evento empresarial | Llamada de API del sistema externo |
| Lógica previa al envío | Ninguno | Espera, condición, nodos divididos disponibles | Ninguno (lógica al llamar al sistema) |
| Enlace de audiencia | Audiencia RT-CDP predefinida | Audiencia RT-CDP predefinida | Destinatarios especificados en carga útil de API |
| Datos contextuales | Solo atributos de perfil | Solo atributos de perfil | Atributos de perfil + datos de carga útil de API |
| Experimentación de contenido | Admitido | Admitido (en la acción de mensaje) | No compatible |
| Restricción de frecuencia | Admitido | Admitido | Admitido |
| Control de reentrada | N/D (ejecución única) | Reglas de reentrada configurables | N/D (por solicitud) |
| Interfaz de configuración | AJO Campaigns | AJO Recorrido | AJO Campaign + sistema externo |
| Requiere | Audiencia, superficie de canal, mensaje | Audiencia, superficie de canal, mensaje, lienzo de recorrido | Superficie de canal, mensaje, integración de API |

### Elija la opción correcta

Utilice el siguiente flujo de decisión para seleccionar la opción de implementación adecuada:

1. **¿Se activa el envío debido a un evento externo del sistema (por ejemplo, un pedido realizado, un ticket resuelto)?** Si es así, elige **Opción C: Campaña activada por API**. Esta es la única opción que admite déclencheur iniciados por el sistema con datos de carga útil contextuales.

2. **¿El envío está anclado a una fecha de calendario específica o a una programación recurrente?** Si es así, elija **Opción A: Campaña programada**. Es la configuración más sencilla y rápida para envíos por fecha.

3. **¿El envío debe reaccionar a la calificación de audiencia o requerir lógica previa al envío (espera, condición, supresión)?** Si es así, elija **Opción B: Recorrido activado por la audiencia**. El lienzo de recorrido proporciona la flexibilidad para la entrada basada en el comportamiento y la lógica de decisión previa a la entrega.

4. **¿El envía una difusión simple a una audiencia conocida sin requisitos de lógica o temporización especiales?** Elija **Opción A: Campaña programada** para la sobrecarga de configuración más baja.

## Fases de implementación

Esta sección analiza en detalle cada fase de la implementación, incluidos los puntos de decisión y las directrices específicas de las opciones.

### Fase 1: Evaluar la audiencia

**Función de aplicación:** RT-CDP: Evaluación de audiencia

Esta fase define y evalúa el segmento de audiencia objetivo que recibirá el mensaje de la campaña. Determina qué perfiles cumplen los requisitos para la entrega en función de atributos de perfil, señales de comportamiento y reglas de supresión.

>[!NOTE]
>Para la opción C (campaña activada por API), esta fase puede omitirse si los destinatarios se especifican completamente en la carga útil de déclencheur de API. Sin embargo, incluso las campañas activadas por API se benefician de tener una audiencia de supresión para filtrar los perfiles que no deben recibir mensajes.

#### Decisión: Criterios de audiencia

¿Qué condiciones definen la audiencia objetivo? ¿Qué reglas de supresión deben excluir los perfiles?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Audiencia basada en atributos de perfil | La audiencia de destino se define mediante atributos demográficos, de preferencia o de estado | El más sencillo de generar; admite todos los métodos de evaluación |
| Audiencia basada en eventos de comportamiento | La audiencia de destino se define por las acciones realizadas (o no realizadas) en un período de tiempo determinado | Requiere la ingesta de datos de evento; las reglas de ventana de tiempo pueden limitar la elegibilidad de transmisión |
| Composición de audiencias (audiencia derivada) | La audiencia de Target requiere operaciones de clasificación, división, exclusión o enriquecimiento en varias audiencias de origen | Evaluación más potente, pero solo por lotes; limitada a 10 composiciones por zona protegida |

#### Decisión: método de evaluación

¿Con qué rapidez debe actualizar la audiencia para reflejar los nuevos perfiles calificativos o descalificadores?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Evaluación por lotes | Campañas programadas en las que se acepta la actualización de la audiencia en un día; audiencias grandes y complejas | Predeterminado para la mayoría de los tipos de segmentos; procesa en un horario diario o bajo demanda; admite todas las funciones de reglas de segmentos |
| Evaluación de streaming | Recorridos activados por la audiencia en los que los perfiles deben entrar en tiempo casi real a medida que se califican | Automático para expresiones de regla de segmento aptas; no todos los tipos de segmento cumplen los requisitos para streaming; latencia casi en tiempo real (de segundos a minutos) |
| Evaluación de Edge | No es típico de este patrón (se utiliza para la personalización de la misma página) | Compatibilidad con reglas de segmentos limitadas; latencia de milisegundos; relevante solo si se combina con patrones de personalización web |

#### Decisión: política de combinación

¿Qué política de combinación debe utilizar la audiencia para resolver fragmentos de perfil?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Política de combinación predeterminada (marca de tiempo solicitada) | Más común para los casos de uso de campañas por lotes | El valor de atributo más reciente gana; estándar para la mensajería saliente |
| Política de combinación personalizada (prioridad del conjunto de datos) | Cuando una fuente de datos específica debe tener prioridad para los atributos clave | Resulta útil cuando los datos CRM deben anular los datos recopilados por la web para determinados campos |

#### Navegación de IU

Cliente > Audiencias > Crear audiencia > Generar regla

#### Detalles de configuración clave

- Defina la audiencia mediante el Generador de segmentos con reglas de segmento para atributos de perfil, eventos de comportamiento y abono a segmentos
- Aplique reglas de supresión para excluir perfiles que ya se han convertido, que han recibido recientemente un mensaje similar o que han optado por excluirse
- Antes de continuar, compruebe que la audiencia tenga una población distinta de cero
- Para las campañas por lotes, asegúrese de que haya una programación de evaluación de segmentos activa o un déclencheur de evaluación bajo demanda
- Confirmar campos de consentimiento (`consents.marketing.email.val`, `consents.marketing.sms.val`, etc.) se rellenan y aplican

#### Dónde divergen las opciones

**Para La Opción A (Campaña Programada):**

La evaluación por lotes es típica. La audiencia se vuelve a evaluar en el momento de la ejecución de la campaña, por lo que se dirige a la población elegible más actual. Defina la audiencia y verifique su población y, a continuación, continúe con la creación de campañas.

**Para Opción B (Recorrido Activado Por Audiencia):**

Se prefiere la evaluación de streaming para que los perfiles entren en el recorrido según califiquen. Asegúrese de que la expresión de regla de segmento sea apta para flujo continuo (déclencheur de evento simples, comparaciones de atributos, ventanas de tiempo limitado). Configure la audiencia y compruebe que la calificación de flujo continuo esté activa.

**Para la opción C (campaña activada por API):**

La evaluación de audiencias puede omitirse por completo. Si se utiliza, cree una audiencia de supresión para filtrar los perfiles que no deben recibir el mensaje (por ejemplo, suscripciones recientes, conversiones anteriores). El sistema de llamada determina los destinatarios principales.

#### Documentación de Experience League

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Composición de audiencia](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/audience-composition)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/pql/overview)

### Fase 2: Configuración del canal

**Función de aplicación:** AJO: Configuración de canal

Esta fase valida o crea la superficie de canal (ajuste preestablecido) que define la infraestructura de envío del mensaje: subdominio, grupo de IP, identidad del remitente, dirección de respuesta y configuración de cancelación de suscripción. Debe existir una superficie de canal válida para poder crear contenido de mensaje o activar campañas.

#### Decisión: Canal de destino

¿Qué canal de mensajería enviará el mensaje de la campaña?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Correo electrónico | La mayoría de los tipos de campaña: boletines informativos, promociones, notificaciones, renovaciones | Requiere una configuración de subdominio delegado, grupo de IP calentadas, identidad del remitente y cancelación de suscripción |
| SMS | Mensajes breves o con distinción de tiempo: ventas flash, recordatorios de citas, códigos OTP | Requiere credenciales de proveedor de SMS (Sinch, Twilio o Infobip); mayor coste por mensaje; requisitos de consentimiento más estrictos |
| Notificación push | Audiencias que interactúan con dispositivos móviles: actualizaciones de la aplicación, ofertas basadas en la ubicación y anuncios de funciones en la aplicación. | Requiere credenciales de APNS (iOS) o FCM (Android); los usuarios deben tener la aplicación instalada con los permisos push concedidos |

#### Decisión: selección de superficie de canal

¿Ya existe una superficie de canal adecuada en la zona protegida o se debe crear una nueva?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Reutilización de superficies existentes | Una superficie activa y verificada coincide con el subdominio, la identidad del remitente y el tipo de canal necesarios | Ruta más rápida; no se necesita ninguna configuración de DNS o de calentamiento |
| Crear nueva superficie | Ninguna superficie existente coincide con los requisitos o se necesita una nueva identidad de subdominio/remitente | Requiere delegación de subdominios, verificación DNS, asignación de grupos de IP y calentamiento de IP potencial (de 2 a 4 semanas para nuevas IP) |

#### Decisión: gestión de cancelación de suscripción

¿Cómo se debe administrar la exclusión en la superficie del canal?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Encabezado de cancelación de suscripción a lista de un clic | Estándar para todos los correos electrónicos de marketing; requerido por los principales ISP (Gmail, Yahoo) para la entrega | Agrega un encabezado de cancelación de suscripción basado en mailto: o URL que los ISP muestran como un botón &quot;Cancelar suscripción&quot; |
| Cancelar suscripción al vínculo en el cuerpo del correo electrónico | Necesario como alternativa para los clientes de correo electrónico que no admiten encabezados de cancelación de suscripción a listas | Incluya un vínculo para cancelar la suscripción en el pie de página del correo electrónico junto al encabezado de cancelación de suscripción a una lista |
| Ambos (recomendado) | Práctica recomendada para todos los correos electrónicos de marketing | Máxima cobertura de cumplimiento y mejor perfil de entrega |

#### Navegación de IU

Administración > Canales > Superficies de canal > Crear superficie (o seleccione una existente)

#### Detalles de configuración clave

- Para el correo electrónico: enlace el subdominio de envío, el grupo de IP, el nombre del remitente, el correo electrónico del remitente, la dirección de respuesta y la dirección de CCO (si se requiere una copia de auditoría)
- Para SMS: configure las credenciales del proveedor de SMS y la configuración de código corto o código largo
- Para push: configure APNS o credenciales de FCM con el certificado o la clave de servidor de la aplicación
- Compruebe que la superficie de canal muestra el estado &quot;Activo&quot; antes de continuar
- Confirme que los registros DNS (SPF, DKIM, DMARC) están correctamente configurados para el subdominio de envío
- Revise la lista de supresión para ver si hay entradas obsoletas; limpie antes de la activación

#### Documentación de Experience League

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Crear grupos de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [planes de calentamiento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configuración de superficie de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configuración del canal SMS](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Administrar lista de supresión](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Fase 3: Crear el mensaje

**Función de aplicación:** AJO: Creación de mensajes

Esta fase crea el contenido del mensaje que se entregará a la audiencia. Incluye la selección o creación de una plantilla de contenido, el diseño del mensaje, la adición de personalización mediante atributos de perfil, la configuración de bloques de contenido condicional para variaciones específicas de la audiencia, la creación de fragmentos de contenido reutilizables y la previsualización/prueba del mensaje con perfiles de muestra.

#### Decisión: enfoque del contenido

¿Cómo se debe crear el contenido del mensaje?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Empezar desde una plantilla existente | Existen plantillas aprobadas por la marca que coinciden con el tipo de mensaje (promocional, transaccional, boletín informativo) | Ruta de creación más rápida; garantiza la coherencia de la marca; las plantillas son específicas de la zona protegida |
| Diseñe desde cero | No existe una plantilla adecuada o el mensaje requiere un diseño único | Más flexibilidad pero más esfuerzo; considere la posibilidad de guardar como plantilla para reutilizarla |
| Importar HTML | El diseño del mensaje se ha creado externamente (por ejemplo, en una herramienta de diseño) y HTML está listo para importarse | Conserva el diseño externo; puede necesitar ajustes para los tokens de compatibilidad y personalización de AJO |

#### Decisión: profundidad de Personalization

¿Qué atributos de perfil deben personalizar el mensaje y son necesarios los bloques de contenido condicional?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Personalización básica (nombre, saludo) | Campañas sencillas en las que el contenido genérico con un saludo personalizado es suficiente | Esfuerzo bajo; riesgo mínimo de problemas de procesamiento; utiliza atributos de perfil estándar |
| Personalización basada en atributos | El contenido del mensaje varía según los atributos del perfil (nivel, preferencia, ubicación) | Requiere rutas XDM verificadas; realice pruebas con varios perfiles para garantizar que todas las variaciones se representen correctamente |
| Bloques de contenido condicionales | Se deben mostrar diferentes secciones de contenido a diferentes segmentos de audiencia dentro del mismo mensaje | Creación más compleja; cada condición necesita una reserva predeterminada; pruebe todas las permutaciones |
| Personalización contextual (solo opción C) | Las campañas activadas por API deben procesar los datos pasados en la carga útil de déclencheur (detalles del pedido, información del ticket) | Los atributos contextuales no se almacenan en el perfil; defina marcadores de posición en el mensaje y asígnelos a campos de carga útil |

#### Decisión: Estrategia de fragmento

¿Deben crearse bloques de contenido compartido como fragmentos reutilizables?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Fragmentos reutilizables | Los encabezados, pies de página, exenciones de responsabilidad legales o bloques de cancelación de suscripción se comparten en varias campañas | Los cambios en un fragmento se propagan a todos los mensajes que hacen referencia a él (activos y borrador); máximo de 30 fragmentos por mensaje |
| Contenido en línea | Mensaje único sin elementos compartidos en otras campañas | Más sencillo para contenido de un solo uso; sin riesgo de propagación |

#### Navegación de IU

Campañas > Seleccionar campaña > Editar contenido > Enviar correo electrónico a Designer (o editor SMS/Push)

#### Detalles de configuración clave

- Diseño del diseño del mensaje con componentes de contenido de arrastrar y soltar (texto, imagen, botón, divisor, columnas)
- Establezca las propiedades del encabezado del correo electrónico: línea de asunto, texto de preencabezado y superficie del remitente
- Inserte expresiones de personalización utilizando la sintaxis Handlebars (p. ej., `{{profile.person.name.firstName}}`)
- Configurar las funciones de ayuda para el formato (fecha, número, manipulación de cadenas)
- Añada reglas de contenido condicionales para mostrar contenido diferente en función de los atributos del perfil o la pertenencia a un segmento
- Configuración del contenido de reserva predeterminado cuando no se cumple ninguna condición
- Para SMS, redacte el cuerpo del mensaje teniendo en cuenta el límite de caracteres
- Para push, configure el título, el cuerpo, la imagen y la acción (vínculo profundo o URL)
- Previsualice el mensaje con perfiles de muestra para verificar la renderización de la personalización
- Envíe correos electrónicos de prueba a las partes interesadas internas para su revisión
- Prueba del procesamiento en clientes de correo electrónico con la función de procesamiento de correo electrónico

#### Documentación de Experience League

- [Crear un correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/create-email)
- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Uso de componentes de contenido de Email Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funciones de ayuda](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Envío de pruebas de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [Procesamiento de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)
- [Creación de un mensaje SMS](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/sms/create-sms)
- [Diseño de una notificación push](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/push/design-push)

### Fase 4: crear la campaña o el recorrido

**Función de la aplicación:** AJO: Campaign Execution (Opciones A y C) o AJO: Journey Orchestration (Opción B)

Esta fase crea la campaña o el recorrido que une la audiencia, el mensaje y el mecanismo de ejecución en una unidad de entrega. Aquí es donde las tres opciones de implementación difieren más significativamente.

#### Decisión: Experimentación de contenido

¿Debe la campaña incluir una prueba A/B o un experimento multivariable para optimizar el rendimiento del mensaje?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Sin experimento | Variante de mensaje único con alta confianza en la eficacia del contenido | Configuración más sencilla; activación más rápida |
| Prueba A/B (2 variantes) | Prueba de líneas de asunto, CTA o diseños de contenido con una hipótesis clara | Dividir tráfico 50/50 o con una asignación ponderada; requiere un tamaño de audiencia suficiente para la relevancia estadística |
| Prueba multivariable (3+ variantes) | Prueba simultánea de varios elementos de contenido | Requiere audiencias más grandes; mayor duración para alcanzar el umbral de confianza; máximo de 10 tratamientos por experimento |

#### Decisión: Límite de frecuencia

¿Debe esta campaña respetar las reglas globales de restricción de frecuencia para evitar el exceso de mensajes?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Aplicación de reglas de frecuencia | Campaign forma parte de un programa de mensajería más amplio con varios envíos simultáneos | Evita la fatiga del cliente; los perfiles que exceden el límite se suprimen de la entrega |
| Exento de límite | Campaign es esencial para el tiempo o es transaccional y debe llegar a todos los perfiles cualificados, independientemente del historial de mensajes reciente | Utilice con moderación; si exime a las campañas de las reglas de frecuencia, se corre el riesgo de enviar mensajes excesivos |

#### Decisión: puntuación de prioridad

¿Qué nivel de prioridad debe tener esta campaña en relación con otras campañas activas?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Alta prioridad (75-100) | Campañas críticas: principales lanzamientos de productos, ofertas por tiempo limitado, notificaciones regulatorias | Tendrá prioridad sobre las campañas de menor prioridad cuando surjan conflictos |
| Prioridad de Medium (25-74) | Campañas de marketing estándar: boletines informativos, campañas de participación, promociones generales. | Equilibrado con otras campañas; puede suprimirse si una campaña de prioridad más alta entra en conflicto |
| Prioridad baja (0-24) | Envía cosas buenas: actualizaciones informativas, promociones secundarias | Se suprimirá en favor de campañas de mayor prioridad |

#### Dónde divergen las opciones

**Para La Opción A (Campaña Programada):**

**Navegación de la interfaz de usuario:** Campañas > Crear campaña > Programado > Marketing

1. Creación de una nueva campaña de marketing programada
2. Seleccione la audiencia de destino en el selector de audiencias
3. Seleccione la superficie de canal y vincule el contenido del mensaje creado
4. Configure la programación de ejecución: inmediata, específica, de fecha y hora o recurrente
5. Opcionalmente, habilitar la experimentación de contenido y definir variantes de tratamiento
6. Configurar opcionalmente el límite de frecuencia y la puntuación de prioridad
7. Revise la configuración completa de la campaña
8. Activación de la campaña

**Para Opción B (Recorrido Activado Por Audiencia):**

**Navegación por la interfaz de usuario:** Recorrido > Crear Recorrido

1. Crear un nuevo recorrido con un evento de entrada &quot;Leer audiencia&quot;
2. Seleccione la audiencia de destino como origen de la entrada
3. Configurar reglas de reentrada (permitir la reentrada, la entrada única o la reentrada después del período de espera)
4. Si lo desea, agregue nodos de espera (por ejemplo, espere 24 horas después de la calificación)
5. Si lo desea, puede añadir nodos de condición (por ejemplo, comprobar si el perfil cumple criterios adicionales)
6. Añada el nodo de acción del mensaje y seleccione la superficie de canal y el contenido creado
7. Configurar criterios de salida (por ejemplo, conversiones de perfil, cancelaciones de suscripción de perfil)
8. Opcionalmente, habilitar la experimentación de contenido en la acción de mensaje
9. Revisión y publicación del recorrido

**Para la opción C (campaña activada por API):**

**Navegación de la interfaz de usuario:** Campañas > Crear campaña > Activado por API

1. Creación de una nueva campaña activada por API
2. Seleccione la superficie de canal y vincule el contenido del mensaje creado
3. Configure tokens de personalización contextual para los datos que se pasarán en la carga útil del déclencheur de API
4. Revisión y activación de la campaña
5. Tenga en cuenta el ID de campaña para su uso en la integración de déclencheur de API del sistema externo
6. El sistema de llamada envía solicitudes de déclencheur al punto final de la campaña con perfiles de destinatario y datos contextuales

#### Documentación de Experience League

- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introducción a las campañas](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Campañas activadas por API](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)
- [Introducción a recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Leer recorrido de audiencia](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Introducción al experimento de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificación de posibles conflictos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### Fase 5: Analizar la creación de informes y el rendimiento

**Función de aplicación:** AJO: Informes y análisis de rendimiento

Esta fase monitoriza las métricas de entrega durante la ejecución a través de informes en vivo y analiza el rendimiento de la campaña después de la finalización a través de informes históricos. Si lo desea, puede configurar la integración de CJA para un análisis más profundo entre canales.

#### Decisión: método de creación de informes

¿Qué nivel de creación de informes se necesita para esta campaña?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo informes nativos de AJO | Las métricas de entrega y participación estándar son suficientes (envíos, envíos, aperturas, clics, devoluciones) | No hay configuración adicional; los informes están incorporados en la interfaz de usuario de la campaña/recorrido |
| Informes nativos de AJO + análisis de CJA | El análisis de impacto en canales múltiples, el modelado de atribución o el análisis de funnel son necesarios más allá de las métricas de entrega | Requiere una conexión de CJA y una vista de datos vinculada a conjuntos de datos de AJO; proporciona una capacidad analítica más profunda |
| informes programáticos de CJA | Las partes interesadas necesitan paneles automatizados o la entrega programada de informes | Requiere integración de API de informes de CJA; útil para paneles ejecutivos y resúmenes de rendimiento recurrentes |

#### Decisión: Seguimiento de conversión

¿Cómo se medirá el éxito de la campaña más allá de las métricas de entrega y participación?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Sin seguimiento de conversión | El objetivo de la campaña es la sensibilización o la participación (aperturas, clics) sin una acción descendente específica | Lo más sencillo; no se requiere seguimiento de eventos adicional |
| Seguimiento de conversión web | Campaign CTA vincula una página web donde se rastrean eventos de conversión (compras, registros y envíos de formularios) | Requiere etiquetado Web SDK o Analytics en la página de destino; los eventos deben capturarse en conjuntos de datos de AEP |
| Evento de conversión personalizado | El éxito de la campaña se mide por un evento específico de la empresa que no se captura en la web (por ejemplo, compra en la tienda, interacción con el centro de llamadas) | Requiere que el evento personalizado se incorpore en AEP y se incluya en los conjuntos de datos de informes |

#### Navegación de IU

- Informes en vivo: Campañas > Seleccionar campaña > Informe en vivo (o Recorridos > Seleccionar recorrido > Informe en vivo)
- Informes históricos: Campañas > Seleccionar campaña > Informe de todos los tiempos (o Recorridos > Seleccionar recorrido > Informe de todos los tiempos)

#### Detalles de configuración clave

- Acceda a informes en directo durante la ejecución de la campaña para monitorizar la entrega y la participación en tiempo real
- Revise las métricas clave: Enviado, Entregado, Devoluciones, Aperturas, Clics, Cancelaciones de suscripción (correo electrónico); Enviado, Entregado, Clics, Errores (SMS); Enviado, Entregado, Aperturas, Acciones (push)
- Una vez finalizada la campaña, acceda a los informes históricos (de todo el tiempo) para obtener un análisis completo
- Analice la entrega funnel: Objetivos > Enviado > Entregado > Aperturas > Clics
- Revisar los motivos de error y exclusión para identificar los problemas de envío
- Si la experimentación de contenido estaba habilitada, revise los resultados del experimento y espere a que se alcance la confianza estadística antes de declarar un ganador
- Para la integración con CJA, compruebe que la vista de datos de AJO incluye los conjuntos de datos de AJO relevantes (conjunto de datos de evento de comentarios de mensajes, conjunto de datos de evento de experiencia de seguimiento de correo electrónico)

#### Documentación de Experience League

- [Informe en vivo de la campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Consideraciones sobre la implementación

Esta sección abarca protecciones, escollos comunes, prácticas recomendadas y decisiones de compensación.

### Protecciones y límites

- Máximo de 500 campañas activas por zona protegida: [protecciones de Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 4000 definiciones de segmento por zona protegida: [protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- Máximo de 10 superficies de canal por tipo de canal y zona protegida
- Las campañas activadas por API admiten hasta 20 destinatarios de perfil por solicitud de déclencheur
- Las campañas no se pueden editar una vez activadas; en su lugar, duplique y modifique
- Los informes en vivo se actualizan cada 60 segundos y muestran las últimas 24 horas de datos
- Los informes históricos pueden tardar hasta dos horas en rellenarse completamente después de la finalización de la campaña
- Máximo de 10 tratamientos (variantes) por experimento de contenido
- Máximo de 10 configuraciones de límite por zona protegida
- Máximo de 30 fragmentos de contenido por mensaje
- Se recomienda un tamaño máximo de correo electrónico de 100 KB para una entrega óptima
- Los planes de calentamiento de la IP deberían aumentar el volumen gradualmente en 2-4 semanas para las nuevas IP
- Las entradas de la lista de supresión se conservan durante un periodo configurable (14 días de forma predeterminada para las devoluciones leves)

### Peligros comunes

- **Envío antes de que se complete el calentamiento de la IP:** Los ISP marcarán las nuevas direcciones IP que envíen volúmenes altos inmediatamente, lo que resultará en una capacidad de envío deficiente y en posibles listas negras. Complete siempre un plan de calentamiento de IP antes de que la producción envíe nuevas IP.

- **No se está probando la personalización en varios perfiles:** los tokens de Personalization que funcionan para un perfil de prueba pueden fallar para otros si la ruta XDM a la que se hace referencia no existe o es nula en algunos perfiles. Obtenga siempre una vista previa con varios perfiles de prueba que representen niveles de integridad de datos diferentes.

- **Omitiendo revisión de lista de supresión:** Las entradas de lista de supresión antiguas pueden bloquear la entrega a direcciones válidas, mientras que las entradas que faltan pueden dar como resultado la entrega a direcciones no válidas que generan devoluciones. Revise y limpie la lista de supresión antes de las campañas principales.

- **Ignorar la restricción de frecuencia para las campañas promocionales:** El envío de una campaña promocional sin límite de frecuencia mientras que otras campañas también están activas puede dar como resultado que los perfiles reciban varios mensajes en un corto período, lo que genera cancelaciones de suscripción y quejas de correo no deseado.

- **Programar campañas sin comprobar la población de la audiencia:** Activar una campaña antes de confirmar que la audiencia de destino tiene una población evaluada distinta de cero da como resultado que no se envíen mensajes. Compruebe siempre el tamaño de la audiencia antes de la activación.

- **Usando evaluación por lotes para recorridos activados por audiencias:** Si el recorrido usa una entrada Leer audiencia con evaluación por lotes, los perfiles no entrarán en tiempo casi real. Utilice la evaluación de flujo continuo para la audiencia cuando se requiera la entrada de recorrido en tiempo casi real.

- **No se puede configurar la aplicación del consentimiento:** El envío de mensajes a perfiles sin un consentimiento de marketing válido infringe las regulaciones y daña la reputación de la capacidad de envío. Asegúrese de que los campos de consentimiento se rellenen y apliquen en el nivel de superficie de canal.

### Prácticas recomendadas

- Comience con la opción A (Campaña programada) para casos de uso de difusión sencillos y pase a la opción B (Recorrido activado por la audiencia) solo cuando sea necesario un tiempo previo a la entrega o basado en el comportamiento
- Incluya siempre un encabezado de cancelación de suscripción de lista de un solo clic y un vínculo de cancelación de suscripción en el cuerpo del correo electrónico para lograr el máximo cumplimiento
- Cree fragmentos de contenido reutilizables para encabezados, pies de página y exenciones de responsabilidad legal para garantizar la coherencia en las campañas
- Establezca reglas de límite de frecuencia antes de activar las campañas para evitar el exceso de mensajes en los envíos simultáneos
- Utilice la experimentación de contenido para optimizar las líneas de asunto y las CTA, empezando por las pruebas A/B, antes de progresar a experimentos multivariables
- Asigne puntuaciones de prioridad a todas las campañas activas para garantizar una resolución de conflictos coherente
- Programe la evaluación de audiencias por lotes para que se complete antes del momento de ejecución de la campaña a fin de garantizar nuevos datos de audiencia
- Envíe correos electrónicos de prueba y utilice la función de procesamiento de correo electrónico para comprobar que el mensaje se muestra correctamente en los clientes de correo electrónico antes de la activación
- Monitorice el informe en vivo inmediatamente después de la activación de la campaña para detectar problemas de envío antes de tiempo
- Archivar configuraciones de campaña y resultados de experimentos para referencia futura y optimización continua

### Decisiones de compensación

Se deben evaluar las siguientes compensaciones cuando se tomen decisiones de implementación.

#### Simplicidad frente a flexibilidad

Las campañas programadas (Opción A) ofrecen la configuración más sencilla, pero no una lógica previa al envío. Los recorridos activados por la audiencia (Opción B) proporcionan una lógica previa al envío, pero añaden complejidad a la configuración.

- **La opción A favorece:** velocidad de lanzamiento, simplicidad operativa, autoservicio para especialistas en marketing
- **La opción B favorece:** Segmentación basada en el comportamiento, supresión condicional, extensibilidad a recorridos de varios pasos
- **Recomendación:** Comience con la opción A para envíos directos. Cambie a la opción B solo cuando el caso de uso requiera genuinamente una lógica de espera, condición o bifurcación antes de la entrega. Evite utilizar el lienzo de recorrido para envíos por lotes simples que no se benefician de las capacidades de orquestación.

#### Actualización de audiencia frente a coste de evaluación

La evaluación de streaming proporciona actualizaciones de audiencia casi en tiempo real, pero tiene restricciones de reglas de segmentos. La evaluación por lotes admite todas las funciones de reglas de segmentos, pero se evalúa en una programación diaria.

- **Favoritos de streaming:** Puntualidad, precisión basada en el comportamiento, entrada de recorrido activada por la audiencia
- **Favoritos por lotes:** Lógica de audiencia compleja, poblaciones grandes, menor sobrecarga de evaluación
- **Recomendación:** Use la evaluación por lotes para campañas programadas (Opción A) donde la actualización diaria sea suficiente. Utilice la evaluación de streaming para recorridos activados por la audiencia (Opción B) en los que los perfiles deben introducir según cumplen los requisitos. Si la expresión de regla de segmento de audiencia no es apta para flujo continuo, reorganice las reglas o acepte la latencia a nivel de lote.

#### Profundidad de Personalization frente a complejidad de creación

Una personalización más profunda (bloques de contenido condicional, secciones dinámicas) mejora la participación, pero aumenta el esfuerzo de creación y prueba.

- **Favoritos de personalización profunda:** mayores tasas de participación, experiencia del cliente más relevante y mejor conversión
- **Favoritos de personalización sencillos:** menor tiempo de inicio, menor carga de pruebas y menor riesgo de errores de procesamiento
- **Recomendación:** Comience con la personalización básica (nombre, categoría de producto relevante) y coloque bloques de contenido condicional basados en las ganancias de rendimiento medidas. Pruebe siempre todas las variaciones de contenido en varios perfiles de prueba antes de la activación.

#### Control de frecuencia frente a alcance de mensaje

La restricción estricta de frecuencia evita el exceso de mensajería, pero puede suprimir la entrega de campañas a perfiles que han recibido recientemente otros mensajes.

- **Favoritos estrictos de límite:** Calidad de la experiencia del cliente, tasas de cancelación de suscripción más bajas, reputación de marca
- **Favoritos de límite relajados:** Alcance máximo del mensaje, impresiones totales más altas, cobertura de la campaña
- **Recomendación:** Habilite siempre la restricción de frecuencia para las campañas de marketing. Defina límites específicos de canal (por ejemplo, 3-5 correos electrónicos por semana, 1-2 SMS por semana). Excluir solo los mensajes transaccionales o críticos en el tiempo de las reglas de límite.

## Documentación relacionada

Esta sección proporciona vínculos completos a la documentación de [!DNL Experience League] organizada por temas.

### Campañas

- [Introducción a las campañas](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Campañas activadas por API](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### Recorridos

- [Introducción a recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Leer recorrido de audiencia](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Crear grupos de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [planes de calentamiento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configuración de superficie de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configuración del canal SMS](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Administrar lista de supresión](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Creación y personalización de mensajes

- [Crear un correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/create-email)
- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Uso de componentes de contenido de Email Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Importación o codificación del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/code-content)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funciones de ayuda](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### Gestión de contenido

- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Envío de pruebas de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [Procesamiento de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)

### Experimentación de contenido

- [Introducción al experimento de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Cálculos estadísticos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### Administración de frecuencia y conflictos

- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Información general sobre reglas comerciales](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Introducción a la administración de conflictos y prioridades](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Puntuaciones de prioridad](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificación de posibles conflictos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [restricción y arbitraje de recorridos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Composición de audiencia](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/audience-composition)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/pql/overview)

### Informes

- [Informe en vivo de la campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Informe en vivo del recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### Gobernanza de datos y consentimiento

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Grupo de campos de consentimiento y preferencias](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/field-groups/profile/consents)
- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Modelado de datos e identidad

- [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/composition)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- [Protecciones de ingesta](https://experienceleague.adobe.com/es/docs/experience-platform/ingestion/guardrails)

### Tutoriales e introducción

- [Introducción a Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/get-started)
- [Cree su primera campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Creación de su primer recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/journey)
