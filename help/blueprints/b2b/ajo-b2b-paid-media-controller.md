---
title: Controladora de medios de pago AJO B2B
description: Prioridad de las campañas y activación de cuentas en destinos de medios de pago
solution: Journey Optimizer B2B Edition
exl-id: a4f4982f-2b56-4ce2-9c16-abdf627f97de
source-git-commit: 388beb1609384f266f0d80a7dd5a14b03ced3110
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 0%

---

# AJO B2B - Journey Orchestration de cuenta - Controlador de medios de pago

## Información general

Los equipos de marketing que ejecutan medios de pago B2B a escala se enfrentan a un problema recurrente: **las cuentas terminan en varias campañas a la vez** (persona, reconocimiento de categorías, liderado por soluciones, seguimiento), lo que diluye la mensajería, causa fatiga de audiencia y fuerza el trabajo manual de listas (cargas, exclusiones y supresión) en la coincidencia de cuentas de LinkedIn (destino de la cuenta). Sin **priorización de cascada** y **asignación automatizada de campaña**, no hay un solo lugar para decidir qué cuenta obtiene qué mensaje y qué operaciones no se escalan.

**Paid Media Controller** es la solución perfecta para resolver este problema. Usa **Adobe Journey Optimizer B2B edition (AJO B2B)** y **Adobe Experience Platform (AEP)** juntos: un **recorrido de cuentas** lee una audiencia de cuenta calificada de Real-Time CDP, aplica una lógica de ruta dividida (cascada) **7&rbrace; para asignar cada cuenta exactamente a un nivel de campaña y** activa cada ruta directamente **a destinos de medios de pago (** por ejemplo, audiencias coincidentes de LinkedIn **), sin transferencias manuales de listas.** El resultado es un control de precisión, menos superposición y un patrón repetible para la orquestación de medios de pago B2B multicanal.

## Caso de uso: Historia de un experto en marketing: Por qué importa un controlador

*Maya lidera los medios de pago para una marca B2B global. Su equipo dirige docenas de campañas: campañas de concienciación fundacional, intención de categoría (Recorrido, datos, contenido), programas basados en soluciones, campañas personales y actividades que debe ganar. Tiene un problema.*

**El problema:** Las mismas cuentas aparecen en varias campañas. Una cuenta de Recorrido de alta intención también está en una lista de sensibilización amplia; una cuenta de preventa sigue recibiendo anuncios personales. Las cargas y exclusiones de listas son manuales. Cada vez que las ventas actualizan una lista de &quot;ganancias obligatorias&quot; o que se inicia una nueva campaña de personalidad, su equipo reexporta audiencias, concilia superposiciones en hojas de cálculo y vuelve a cargar a LinkedIn y otras plataformas. Es lento, propenso a errores y no se escala.

**Lo que ella quiere:** Un lugar donde cada cuenta calificada se evalúe una vez, se asigne a la campaña *más relevante* con reglas de prioridad claras (cascada) y se envíe al destino de medios de pago correcto—automáticamente. No hay entregas de listas manuales. Cuando cambian los datos o la estrategia, el sistema vuelve a evaluar y mueve las cuentas entre campañas sin que su equipo toque las listas.

**Respuesta de Adobe:** Con **AJO B2B y AEP trabajando juntos**, Maya puede ejecutar un solo recorrido de **controlador de medios de pago**: AEP y Real-Time CDP tienen los datos y una audiencia maestra de &quot;cuentas calificadas&quot;; AJO B2B ejecuta un recorrido de cuentas que usa **lógica de ruta dividida** (cascada) para enrutar cada cuenta al nivel correcto (por ejemplo, Persecuciones dirigidas → Conocimiento de la categoría de → Persona → dirigido por la solución → Conocimiento de fundación) y **Activar en Destino** envía cada ruta al nivel correcto LinkedIn (u otra) campaña. Un recorrido, una fuente de datos, sin exportaciones de listas manuales. Ese es el patrón del controlador de medios de pago, y es la forma en que Adobe permite la precisión y la escala de los medios de pago B2B.

## Por qué es importante para las empresas B2B:

Las organizaciones que adoptan este patrón pueden eliminar por completo la lógica de exclusión y supresión manual (por ejemplo, el 100% de la resolución de superposición gestionada en el recorrido), escalar a **decenas de miles de cuentas** a través de un solo controlador y mantener una **única fuente fiable** para la cual la cuenta va a cada campaña. El sistema **se adapta automáticamente** a medida que cambian el enfoque de la campaña, las audiencias de destino y los objetivos de ventas, sin necesidad de volver a exportar las listas ni volver a cargarlas en cada plataforma. Para cualquier empresa B2B que ejecute varias campañas de medios pagados, el patrón de controlador de medios pagados ofrece la claridad, el control y la automatización que los flujos de trabajo de listas manuales no pueden.

Los siguientes KPI se alinean bien con la medición de éxito:

- **Conocimiento:** ¿Las cuentas de Target están viendo los anuncios correctos y se están moviendo a las campañas correctas a una tasa mayor?
- **Participación:** ¿Son mejores la participación y la conversión cuando se elimina la superposición?
- **Eficiencia:** ¿Cuánto ha disminuido el trabajo manual en la lista (cargas, exclusiones, supresión)?
- **Costo:** ¿Cómo cambia el costo por cuenta adquirida o la oportunidad con la orquestación automatizada?

## Orquestación de Recorrido de medios pagados

Un caso de uso común y el centro de atención de este modelo es **orquestación de Recorrido de medios de pago B2B**: garantizar que cada cuenta calificada se asigne exactamente a un nivel de campaña y se active al destino de medios de pago correcto, sin superposiciones ni transferencias manuales.

El recorrido del controlador **lee** una audiencia de cuenta calificada (creada en Real-Time CDP a partir de los datos de AEP), **evalúa** cada cuenta mediante condiciones de ruta dividida (cascada) (por ejemplo, la búsqueda → búsqueda basada en la solución → la intención de categoría de → de persona → fundacional) y **activa** cada ruta de acceso al destino correspondiente (por ejemplo, audiencias coincidentes de LinkedIn para cada campaña).

**Solución centrada en la cuenta:** El foco de la controladora de medios de pago son **cuentas** y su **asignación de campaña**. La configuración técnica admite los datos y las audiencias que representan cuentas cualificadas y sus atributos (por ejemplo, intención, segmento, persona), que son necesarios para una segmentación correcta a nivel de cuenta y una orquestación basada en recorridos.

## Requisitos

La solución centrada en las cuentas requiere las siguientes aplicaciones y servicios:

- **Adobe Journey Optimizer B2B edition**: recorridos de cuenta, lógica de ruta dividida (cascada), Activar en destino.
- **Adobe Real-time Customer Data Platform (RTCDP) B2B edition**: perfiles de cuenta, audiencias de cuenta (por ejemplo, cuentas calificadas para medios de pago).

## Arquitectura

Flujo de alto nivel:

1. **Datos y audiencias**: AEP contiene perfiles y eventos; Real-Time CDP B2B crea audiencias de cuenta (por ejemplo, &quot;Cuentas aptas para medios de pago&quot;) que se usan como audiencia de entrada de recorrido.
2. **Orquestación** — recorrido de cuenta B2B de AJO: **Leer audiencia** (cuentas calificadas) → **Dividir ruta** (cascada: por ejemplo, Búsqueda → solución dirigida → Persona → Categoría → Fundacional) → **Activar en Destino** (por ruta a LinkedIn u otros medios de pago).
3. **Destinos**: Los canales de medios de pago (por ejemplo, Audiencias coincidentes de LinkedIn) reciben la activación a nivel de cuenta desde cada ruta de recorrido; no hay cargas manuales de lista.

## Diagrama de arquitectura

<img src="assets/ajo-b2b-paid-media-activation-architecture.svg" alt="Arquitectura de controladora de medios de pago AJO B2B" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Modelado de datos en AEP B2B

Con cualquier orquestación basada en datos, el diseño de esquemas es importante. Los perfiles de cuenta y persona en AEP/RTCDP deben incluir los atributos utilizados en **condiciones de ruta dividida** (por ejemplo, indicador de persecución, interés de solución, persona, categoría de intención, puntuación de participación). Los esquemas B2B (cuenta empresarial XDM, perfil individual XDM, relacional) deben representar la jerarquía y las fuentes de datos. Para obtener más información, consulte [Esquemas B2B de RTCDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview) y [Documentación B2B de AJO](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/home).

**Nota:** La lógica de ruta dividida del recorrido usa datos relacionales y de perfil; asegúrese de que los campos que necesita para la lógica de cascada estén disponibles en el recorrido.

### Guardas

- **Journey Optimizer B2B edition**: consulte la [descripción del producto](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer-b2b.html) para obtener información sobre los límites de recorrido, los límites de nodos y la compatibilidad con destinos.
- **Real-Time CDP** — Vea [protecciones de RTCDP](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/guardrails/overview) para los límites de segmentación y activación.

## Implementación

Los siguientes pasos proporcionan instrucciones para implementar el controlador de medios de pago con AJO B2B y AEP.

### Pasos previos a los requisitos

1. **Definir audiencias de cuenta y modelos de datos en Real-Time CDP B2B.**

   Cree la **audiencia de cuenta calificada** (por ejemplo, &quot;Cuentas elegibles para medios de pago&quot;) que entrará al recorrido del controlador. Utilice el Generador de segmentos y los atributos de cuenta/persona que definen la idoneidad (por ejemplo, ubicación geográfica, segmento, estado de MQA). Esta audiencia es el único punto de entrada para el recorrido.

2. **Defina la jerarquía de campañas y la lógica de división.**

   Documente el orden de las cascadas (por ejemplo, Búsqueda → basada en la solución → Persona → Categoría → Fundacional) y las condiciones de cada ruta (qué atributos o audiencias califican una cuenta). Asegúrese de que las condiciones se **excluyan mutuamente en orden** (de arriba a abajo): una cuenta debe coincidir como máximo con una ruta, la primera que evalúa como verdadero.

3. **Configurar destinos.**

   Configure destinos de medios de pago (por ejemplo, audiencias coincidentes de LinkedIn) en AEP/RTCDP y asegúrese de que estén disponibles para su activación desde AJO B2B. Asigne identificadores de cuenta y cualquier atributo requerido para cada destino.

### Configuración de controlador de medios de pago

1. **Crear el recorrido del controlador en AJO B2B.**

   - **Leer audiencia:** Seleccione la audiencia de cuenta calificada de Real-Time CDP.
   - **Ruta de acceso dividida:** Cree una ruta de acceso para cada audiencia de medios de pago, empezando por la Ruta 1 como prioridad principal y continuando en orden de prioridad. Para cada ruta, añada atributos para establecer los criterios de clasificación (por ejemplo, &quot;en la audiencia de búsqueda&quot;, &quot;interés de la solución = X&quot;, &quot;persona = Y&quot;, &quot;categoría de intención = Z&quot;). Las cuentas se evalúan a través del nodo de ruta dividida a en cascada, lo que cumple los criterios de la primera ruta.
   - **Activar en destino:** Para cada ruta, agregue un nodo Activar en destino al LinkedIn correcto (u otro) campaña/destino.

2. **Validar la exclusividad mutua.**

   - Confirme que cada cuenta introduce solo una ruta (la primera condición que coincida).
   - Verificar activación: las cuentas aparecen en el destino correcto y se excluyen de las campañas de prioridad inferior según lo previsto.

## Diagrama de implementación

<img src="assets/ajo-b2b-paid-media-controller-canvas.svg" alt="Lienzo de controladora de medios de pago AJO B2B" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

### Activación del público

1. **Activar en LinkedIn (y otros destinos).**

   Utilice &quot;Activar en destino&quot; en la recorrido para enviar cada ruta a la audiencia de medios de pago correcta. No se puede exportar ni cargar manualmente la lista; el recorrido impulsa la activación a medida que las cuentas fluyen por las rutas.

2. **Supervisar y ajustar.**

   Utilice los informes de recorrido para monitorizar los volúmenes por ruta.

## Resumen

El modelo de **Controlador de medios de pago** muestra cómo **AJO B2B y AEP** trabajan juntos para ofrecer a los especialistas en marketing B2B una forma única y automatizada de asignar cuentas a campañas y activarlas en medios de pago: una audiencia maestra, un recorrido, lógica de división en cascada y activación directa a destinos, sin transferencias manuales de listas. Establece un patrón repetible para la orquestación de medios de pago B2B multicanal y ayuda a reducir la superposición, mejorar la relevancia y escalar las operaciones.

## Documentación relacionada

- [Modelo de gestión de Recorridos y marketing basado en grupos de compra](https://experienceleague.adobe.com/es/docs/blueprints-learn/architecture/b2b-activation/b2b-buying-group-journeys): recorridos de cuenta y grupo de compra en AJO B2B.
- [Adobe Journey Optimizer B2B edition](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b) — Documentación del producto.
- [Real-time Customer Data Platform B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview) — Audiencias de cuenta y activación.
