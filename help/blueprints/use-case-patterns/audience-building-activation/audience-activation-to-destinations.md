---
title: Activación de audiencias en destinos
description: Obtenga información sobre cómo evaluar y publicar segmentos de audiencia en destinos externos para la segmentación o supresión mediante Adobe Real-Time CDP.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: b0b9d937-45d2-48f9-ac4c-3611c6e35f58
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7043'
ht-degree: 1%

---

# Activación de audiencias en destinos

Esta guía proporciona una referencia de implementación completa para activar audiencias de Adobe [!DNL Real-Time Customer Data Platform] (RT-CDP) en destinos externos. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten evaluar segmentos de audiencia y publicarlos en plataformas de publicidad, almacenamiento en la nube, sistemas CRM o socios de datos para fines de segmentación, supresión, modelado de similitud o enriquecimiento de análisis.

Presenta todas las opciones de implementación viables con análisis de compensación, orientación para la toma de decisiones, rutas de navegación por la interfaz de usuario y referencias a la documentación de Experience League.

La guía cubre el ciclo de vida completo de la activación de audiencias, desde la definición y evaluación de segmentos de audiencia hasta la configuración de conexiones de destino y audiencias de publicación, pasando por la monitorización del estado de activación y la aplicación del cumplimiento de la gobernanza.

## Resumen del caso de uso

Las organizaciones necesitan proporcionar datos de audiencia a sistemas externos para impulsar campañas de medios de pago, enriquecer registros CRM, compartir datos con socios o alimentar análisis descendentes. Audience Activation to Destinations es el patrón de activación fundamental en RT-CDP: evalúa qué perfiles cumplen los requisitos para una audiencia de destinatario, se conecta a uno o más destinos externos, asigna atributos de perfil a campos específicos de destino y publica la audiencia para consumo descendente.

Este patrón se aplica siempre que el objetivo sea obtener datos de audiencia de un sistema externo en el formato correcto y en el momento adecuado. No implica la entrega de mensajes, personalización en el sitio ni análisis. Es el punto de partida más común para implementaciones de RT-CDP y sirve como bloque de creación que otros patrones componen por encima de.

Entre las partes interesadas habituales se incluyen equipos de marketing digital que administran medios de pago, equipos de datos que enriquecen los almacenes, equipos CRM que preparan listas de contactos para campañas y equipos de privacidad que garantizan el cumplimiento de la gobernanza en los flujos de datos salientes.

>[!NOTE]
>Si su organización utiliza [!DNL Real-Time CDP] B2B edition y activa para destinos basados en cuentas, consulte [Activación de audiencia B2B](b2b-audience-activation.md). Ese patrón comparte la misma mecánica de activación, pero utiliza una cuenta B2B y un modelo de datos de persona y requiere la licencia de B2B edition.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Adquisición de nuevos clientes

Amplíe la base de clientes con campañas de adquisición dirigidas, audiencias similares y optimización de medios de pago.

**KPI:** nuevos clientes, coste de adquisición del cliente, conversión de cliente potencial/posible cliente

[Más información sobre la adquisición de nuevos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Reducción del coste de adquisición del cliente

Mejore la eficacia de la segmentación, elimine a los clientes existentes de las campañas de adquisición y optimice el gasto en medios.

**KPI:** coste de adquisición del cliente, coste por posible cliente, eficiencia

[Obtenga más información sobre cómo reducir el coste de adquisición de clientes](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### Optimización del gasto y el ROI de marketing

Mejore el retorno de la inversión en marketing mediante una mejor segmentación, atribución, supresión de audiencias y asignación de presupuesto.

**KPI:** ahorros en costos, costo de adquisición de clientes, ingresos incrementales

[Más información sobre la optimización de los gastos de marketing y el ROI](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## Casos de uso tácticos de ejemplo

- **Segmentación de audiencia de plataforma de publicidad**: inserte segmentos calificados en plataformas de medios de pago para la segmentación de campañas
- **Supresión de medios de pago de clientes existentes**: excluye a clientes conocidos de las campañas de adquisición en plataformas de publicidad para eliminar el gasto desperdiciado
- **Audiencias semilla de similitud**: Envíe segmentos de clientes de alto valor a Facebook, Google Ads o The Trade Desk como audiencias semilla para la expansión de similitudes
- **Sincronización de CRM para la habilitación de ventas**: active audiencias de alta intención o de alto valor para que los equipos de ventas puedan priorizar el alcance
- **Uso compartido de audiencias de socios de datos**: comparta segmentos de audiencia calificados con socios de datos para la medición o la segmentación en cooperación
- **Exportación del almacenamiento en la nube para el enriquecimiento del almacén de datos**: exporte la pertenencia a audiencias y los atributos de perfil a Amazon S3, Azure Blob, Google Cloud Storage o SFTP para análisis descendentes.
- **Activación de audiencia de redireccionamiento**: active a los visitantes del sitio que no se convirtieron a plataformas de redireccionamiento
- **Sincronización de listas de contactos con proveedores de servicios de correo electrónico**: inserta la pertenencia a audiencias en plataformas de correo electrónico de terceros para una difusión coordinada.

## Indicadores clave de rendimiento

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Coste de adquisición de clientes (CAC) | Coste para adquirir un nuevo cliente mediante audiencias activadas | Gasto total en medios/nuevos clientes atribuido a audiencias activadas |
| Tasa de coincidencia de audiencia | Porcentaje de perfiles activados que coinciden correctamente en el destino | Perfiles coincidentes en el destino / perfiles exportados de RT-CDP |
| Ahorros por supresión | Se ha evitado el gasto en medios al eliminar los clientes existentes de las campañas de adquisición | Tamaño estimado de audiencia suprimido de CPM x |
| Tasa de entrega de activación | Porcentaje de perfiles entregados correctamente al destino | Perfiles entregados/perfiles en la audiencia de origen |
| Tiempo hasta la activación | Tiempo transcurrido desde la definición de la audiencia hasta el primer envío en el destino | Medición desde la creación del segmento hasta la primera ejecución del flujo de datos confirmada |
| Precisión de población de audiencia | Alineación entre los tamaños de audiencia esperados y reales en el destino | Recuento de público de destino/recuento de público RT-CDP |

## Patrón de caso de uso

**Audience Activation a destinos**: evalúe y publique un segmento de audiencia en destinos externos para fines de segmentación o supresión.

**Cadena De Funciones:** Evaluación De Audiencia > Configuración De Destino > Audience Activation > Supervisión

## Aplicaciones

- **Adobe [!DNL Real-Time Customer Data Platform] (RT-CDP)**: evaluación de audiencias, administración de destinos, activación de audiencias, consentimiento y aplicación de gobernanza
- **Adobe [!DNL Experience Platform] (AEP)**: almacén de perfiles, servicio de identidad, motor de segmentación, control de datos

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Se asume en contexto | Zona protegida de RT-CDP aprovisionada y activa. Permisos de activación y administración de destinos asignados a funciones de implementación. Credenciales de cuenta de destino disponibles para las plataformas de destino. | [Resumen de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home), [Resumen de control de acceso](https://experienceleague.adobe.com/es/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | El esquema de perfil debe incluir atributos que se asignarán a campos de destino (por ejemplo, correo electrónico, teléfono, identificadores hash, atributos demográficos). El esquema debe estar habilitado para perfiles con conjuntos de datos que reciban datos de forma activa. | [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home), [Conceptos básicos de composición de esquemas](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/composition) |
| Fuentes de datos y recopilación | Se asume en contexto | Los datos de perfil que alimentan la evaluación de audiencias deben ingerirse y estar actualizados. Canalizaciones de ingesta por lotes o streaming en funcionamiento. Web SDK, conectores de origen o ingesta por lotes que envían datos a conjuntos de datos con perfil habilitado. | [Resumen de orígenes](https://experienceleague.adobe.com/es/docs/experience-platform/sources/home), [Resumen de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home) |
| Configuración de identidad y perfil | Requerido | Deben configurarse las áreas de nombres de identidad para la coincidencia de destino (por ejemplo, correo electrónico con hash para Audiencias personalizadas de Facebook, coincidencia de clientes de Google Ads). Las políticas de combinación deben producir perfiles unificados con todos los atributos necesarios para la activación. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home), [Introducción a las políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview) |
| Definición de audiencia y segmentación | Requerido | La audiencia de destino se define mediante el Generador de segmentos, la Composición de audiencia o la Composición de audiencia federada. Método de evaluación (por lotes, streaming o Edge) seleccionado según las necesidades de latencia de activación. Esta función se ejerce en la Fase 1 de este plan. | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home), [Guía de la interfaz de usuario del generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Los atributos calculados como el valor de duración, la puntuación de participación o la puntuación de tendencia mejoran la precisión de la audiencia y proporcionan atributos de enriquecimiento para asignar a destinos. Es especialmente útil cuando los destinos se benefician de la segmentación de audiencia basada en valores o en puntuaciones. | [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview) |
| Administración del ciclo de datos | Recomendado | Las políticas de caducidad de conjuntos de datos y perfiles garantizan la actualización y el cumplimiento de datos. La configuración del esquema de consentimiento garantiza que solo se activen los perfiles consentidos. Esencial para el cumplimiento normativo al exportar datos a sistemas externos. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/home) |
| Etiquetado y aplicación del uso de datos | Recomendado | Las etiquetas y políticas de gobernanza impiden la activación de datos restringidos a destinos no autorizados (por ejemplo, PII a plataformas de publicidad, segmentos confidenciales a socios de datos). Especialmente importante para la activación de audiencias en sistemas externos de terceros. | [Resumen de control de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home), [Resumen de etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview) |
| Monitorización y observabilidad | Incluido | La monitorización de la activación forma parte de la cadena de funciones (Fase 5). Abarca la monitorización de la ejecución del flujo de datos, las alertas de estado de entrega, el seguimiento de la población de audiencias y la visibilidad del uso de licencias. | [Supervisar flujos de datos de destino](https://experienceleague.adobe.com/es/docs/experience-platform/dataflows/ui/monitor-destinations), [Resumen de alertas](https://experienceleague.adobe.com/es/docs/experience-platform/observability/alerts/overview) |
| Informes y análisis | Recomendado | El análisis de CJA de la efectividad de la activación de audiencias permite medir el rendimiento de las audiencias activadas (por ejemplo, el alza de conversión de la supresión, el ROAS de las audiencias similares). | [Información general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del Catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Real-Time CDP] (RT-CDP)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Evaluación de audiencia | Fase 1: Evaluación de audiencias | Defina reglas de audiencia y evalúe la pertenencia a segmentos mediante métodos de evaluación por lotes, de flujo continuo o de Edge |
| Composición de audiencia | Fase 1: Evaluación de audiencias | Opcionalmente, componer audiencias derivadas mediante operaciones de enriquecimiento, clasificación, división, exclusión y unión para una lógica de audiencia compleja |
| Configuración de destino | Fase 2: Configuración del destino | Configuración de conexiones autenticadas a destinos externos con asignación de campos y parámetros de programación |
| Audience Activation | Fase 3: Audience Activation | Publicación de audiencias evaluadas en destinos configurados con asignación de atributos y programación de exportación |
| Cumplimiento del consentimiento y la gobernanza | Fase 4: Validación de gobernanza | Aplicar las preferencias de consentimiento y las políticas de uso de datos antes y durante la activación de audiencias en sistemas externos |

## Prerrequisitos

- [ La licencia RT-CDP ] está activa con los derechos de activación de audiencia
- [ ] La zona protegida de Target está aprovisionada y el equipo de implementación tiene acceso a ella
- [ ] Los roles de usuario incluyen permisos de administración de destino y activación de audiencia
- [ Hay disponibles ] credenciales de autenticación para cada destino de destino (tokens de OAuth, claves de API, claves de acceso S3 o credenciales de cuenta de servicio)
- [ ] El esquema de perfil incluye todos los atributos que deben asignarse a los campos de destino
- [ ] Se han configurado los espacios de nombres de identidad necesarios para la coincidencia de destinos (por ejemplo, correo electrónico con hash, teléfono, ID de dispositivo)
- [ ] Las canalizaciones de ingesta de datos están operativas y los perfiles están rellenando el almacén de perfiles
- [ ]: las etiquetas y políticas de gobernanza de datos se revisan para los atributos que se están activando (especialmente para destinos externos)
- [ ] Los campos de consentimiento se rellenan en perfiles si se requiere un filtrado basado en el consentimiento

## Opciones de implementación

Las siguientes opciones de implementación están disponibles para este patrón de caso de uso. Revise cada opción y la tabla de comparación para determinar el mejor enfoque para sus necesidades.

### Opción A: activación de destino de streaming

**Ideal para:** actualizaciones en tiempo real de la pertenencia a plataformas de anuncios o sistemas de socios: audiencias personalizadas de Facebook, coincidencia de clientes de Google Ads, audiencias coincidentes de LinkedIn, Trade Desk y destinos similares basados en API de streaming.

**Cómo funciona:**

La activación del destino de streaming ofrece cambios de pertenencia de audiencia al destino en tiempo casi real a medida que los perfiles califican o descalifican del segmento. Cuando se cambia un atributo de perfil o se produce un evento de comportamiento que hace que un perfil entre o salga de una audiencia, la actualización de la pertenencia se transmite al destino en cuestión de minutos.

Este método requiere un conector de destino de streaming (la mayoría de las plataformas de publicidad principales lo admiten) y un método de evaluación de audiencia de streaming o Edge. La evaluación de audiencia supervisa continuamente los cambios de perfil aptos y el flujo de datos de activación inserta actualizaciones a medida que se producen. El destino recibe cambios de pertenencia incrementales en lugar de instantáneas de audiencia completa.

La activación de streaming es la predeterminada para la mayoría de los destinos de plataforma de publicidad en el catálogo RT-CDP. El conector de destino administra automáticamente la autenticación de API, la limitación de velocidad y la lógica de reintentos.

**Consideraciones clave:**

- La evaluación de audiencias debe utilizar la transmisión o la evaluación de Edge (las audiencias solo por lotes no pueden transmitir destinos de transmisión en tiempo real)
- No todas las expresiones de segmento cumplen los requisitos para la evaluación de flujo continuo: las agregaciones complejas, las consultas de varias entidades y ciertas funciones basadas en el tiempo requieren un lote
- Los límites de tasa de API del socio de destino pueden afectar al rendimiento durante los eventos de calificación de audiencias grandes
- Las actualizaciones de atributos de perfil se envían junto con los cambios de pertenencia, manteniendo los datos de destino actualizados

**Ventajas:**

- Actualización casi en tiempo real de la audiencia en el destino (minutos, no horas)
- Las actualizaciones incrementales reducen el volumen de transferencia de datos en comparación con las exportaciones completas
- Gestión automática de eventos de calificación y descalificación
- La mayoría de los destinos de plataforma de publicidad admiten el streaming nativo

**Limitaciones:**

- Requiere definiciones de segmento aptas para streaming (conjunto de funciones de segmento limitado)
- Sin control sobre el formato del archivo o la estructura de exportación: formato de datos determinado por el conector de destino
- No se puede exportar a destinos de almacenamiento basados en archivos (S3, Azure Blob, SFTP)
- Los límites de tasa de API de destino pueden acelerar los cambios de gran volumen

**Experience League:**

- [Activar audiencias en destinos de flujo continuo](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Catálogo de destinos de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/overview)

### Opción B: activación de destino por lotes (exportación de archivos)

**Ideal para:** exportaciones de audiencia programadas a almacenamiento en la nube, almacenes de datos o sistemas que consumen importaciones basadas en archivos: Amazon S3, Azure Blob Storage, Google Cloud Storage, SFTP, Data Landing Zone.

**Cómo funciona:**

La activación de destinos por lotes evalúa las audiencias en una cadencia programada y exporta los resultados como archivos (CSV, JSON o Parquet) al destino de almacenamiento configurado. La exportación puede incluir instantáneas de audiencia completas o cambios incrementales (nuevas cualificaciones y descualificaciones desde la última exportación).

La implementación implica configurar una conexión de destino basada en archivos con credenciales de almacenamiento, preferencias de formato de archivo (delimitador, compresión, convención de nomenclatura) y una programación de exportación (diaria, cada 3 horas, cada 6 horas, etc.). Cada ejecución de exportación genera archivos que contienen la pertenencia a la audiencia y cualquier atributo de perfil asignado.

Este método es compatible con la mayor variedad de consumidores intermedios, ya que el intercambio de datos basado en archivos es compatible de forma universal. También es la única opción para los casos de uso de enriquecimiento del almacenamiento en la nube y del almacén de datos.

**Consideraciones clave:**

- La evaluación de audiencias puede utilizar cualquier método (por lotes, streaming o Edge): la exportación en sí se ejecuta según una programación independientemente
- Las convenciones de formato, compresión y nomenclatura de archivos se pueden configurar por destino
- Admite exportaciones incrementales (solo cambios) y exportaciones completas (instantánea de audiencia completa)
- Exportar intervalos de granularidad de programación de cada tres horas a diario

**Ventajas:**

- Control total sobre el formato de archivo de exportación (CSV, JSON, Parquet), la compresión y la nomenclatura
- Compatible con cualquier sistema descendente que pueda consumir archivos
- Admite modos de exportación incremental y completo
- Puede exportar audiencias con cualquier método de evaluación (incluidos segmentos solo por lotes con una lógica de segmentación compleja)
- Admite ejecuciones de exportación ad hoc (bajo demanda) fuera de la programación habitual

**Limitaciones:**

- La latencia es inherentemente mayor: los datos de audiencia llegan al destino según una programación, no en tiempo real
- Las exportaciones basadas en archivos requieren que el sistema de destino procese e introduzca los archivos
- Costes de almacenamiento en el destino para archivos exportados
- Volúmenes de datos más grandes por exportación en comparación con las actualizaciones de flujo incremental

**Experience League:**

- [Activar audiencias para destinos de exportación de perfiles por lotes](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Catálogo de destinos basados en archivos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage)

### Opción C: activación de varios destinos

**Mejor opción para:** Activar la misma audiencia en varios destinos simultáneamente; por ejemplo, insertar una lista de supresión en todas las plataformas de publicidad, sincronizar un segmento de alto valor en las plataformas de publicidad y CRM, o coordinar el alcance de la audiencia entre varios socios de medios.

**Cómo funciona:**

La activación de varios destinos no es un mecanismo técnico independiente, sino una composición de opciones A y B aplicada a la misma audiencia en varias conexiones de destino. La misma audiencia se activa para dos o más destinos, cada uno con su propia configuración de conexión, asignación de campos y programación.

Cada conexión de destino funciona de forma independiente: una activación de flujo continuo a Facebook y una exportación por lotes a S3 se pueden ejecutar simultáneamente desde la misma audiencia de origen. Las asignaciones de campos se configuran por destino, por lo que se pueden enviar diferentes atributos a diferentes sistemas en función de lo que requiera cada destino y de lo que permitan las políticas de gobernanza.

Se trata de un patrón de producción común para organizaciones que operan en varias plataformas de publicidad, mantienen la sincronización CRM junto con la activación de medios o necesitan distribuir los datos de audiencia a sistemas operativos y analíticos.

**Consideraciones clave:**

- Cada destino tiene una asignación de campos, una programación y una evaluación de gobernanza independientes
- Las políticas de gobernanza se aplican por destino: se pueden permitir atributos diferentes para distintos tipos de destino
- Se puede activar una sola audiencia para una combinación de destinos de flujo continuo y por lotes simultáneamente
- Añadir un nuevo destino no requiere cambios en las activaciones existentes

**Ventajas:**

- Distribución coordinada de audiencias en todos los sistemas externos desde una sola definición de audiencia
- La configuración independiente por destino permite asignaciones y programaciones optimizadas
- La aplicación de la gobernanza por destino garantiza el cumplimiento en diferentes tipos de destino
- Centraliza la administración de audiencias y admite la activación distribuida

**Limitaciones:**

- Más conexiones de destino para configurar, autenticar y mantener
- La complejidad de la monitorización aumenta con cada destino: se deben rastrear los errores de activación por destino
- El uso de licencias (perfiles activados) puede contar por destino según los derechos
- El mantenimiento de la asignación de campos en varios destinos requiere coordinación

**Experience League:**

- [Información general sobre los destinos](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/overview)

### Comparación de opciones

| Criterios | Opción A: Transmisión | Opción B: Lote (Exportación de archivos) | Opción C: multidestino |
| --- | --- | --- | --- |
| Mejor para | Segmentación y supresión de plataformas de publicidad en tiempo real | Enriquecimiento del Data Warehouse, integración de sistemas basados en archivos | Distribución coordinada de audiencias entre plataformas |
| Complejidad | Baja | Medio | Alta |
| Latencia | Minutos (casi en tiempo real) | Horas (programadas) | Combinación de minutos y horas por destino |
| Control de formato de archivo | Ninguno (el destino determina el formato) | Completo (CSV, JSON, parquet, compresión, nomenclatura) | Por destino |
| Evaluación de audiencia | Streaming o Edge requerido | Cualquier método (por lotes, streaming, edge) | Requisitos por destino |
| Requiere | Conector de destino de streaming, segmento apto para streaming | Conector de destino basado en archivos, credenciales de almacenamiento | Varios conectores y credenciales de destino |
| Gobierno | Evaluación de destino único | Evaluación de destino único | Evaluación por destino |

### Elija la opción correcta

Utilice la siguiente lógica de decisión para seleccionar el método de implementación adecuado:

1. **¿Cuántos destinos necesitas?** Si necesita activar la misma audiencia en dos o más destinos, está implementando la opción C (que compone las opciones A y B por destino). Continúe con las preguntas 2 y 3 para cada destino.

2. **¿Admite el destino la transmisión por secuencias?** Si el destino es una plataforma de publicidad (Facebook, Google Ads, LinkedIn, The Trade Desk) o una integración de socio con una API de streaming, utilice la opción A para ese destino. Si el destino es almacenamiento en la nube (S3, Azure Blob, GCS, SFTP) o un sistema que consume archivos, utilice la opción B.

3. **¿Con qué rapidez debe llegar la audiencia al destino?** Si el abono a audiencia debe reflejarse en el destino en cuestión de minutos (por ejemplo, supresión en tiempo real durante campañas activas), utilice la opción A. Si la entrega diaria o cada hora es suficiente (por ejemplo, actualización semanal del almacén de datos, sincronización por lotes de CRM), utilice la opción B.

4. **¿Su audiencia utiliza lógica de segmentación compleja?** Si la definición de audiencia incluye acumulaciones de varios eventos, ventanas de tiempo grandes o funciones que no cumplen los requisitos para la evaluación de flujo continuo, utilice la opción B (destinos por lotes) o asegúrese de que los destinos de la opción A también reciban audiencias evaluadas por lotes según una programación.

## Fases de implementación

La implementación sigue estas fases. Cada fase incluye detalles de configuración, puntos de decisión y vínculos a la documentación de Experience League.

### Fase 1: Evaluación de audiencias

**Función de aplicación:** RT-CDP: Evaluación de audiencia, RT-CDP: Composición de audiencia

**Lo que va a configurar:** Defina la audiencia de destino que se activará en los destinos. Esto incluye especificar los criterios de audiencia (qué perfiles cumplen los requisitos), seleccionar el método de evaluación (con qué rapidez se actualiza la membresía) y validar la población de audiencias. Este es el punto de partida de todas las activaciones: sin una audiencia definida y evaluada, no hay nada que activar.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: método de creación de audiencias**
>
>¿Cómo se debe definir la audiencia objetivo?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Generador de segmentos (basado en reglas) | Definición de audiencia estándar con atributos de perfil, eventos de comportamiento y condiciones de pertenencia a segmentos | Definición de regla más flexible; admite la transmisión y la evaluación de bordes para expresiones aptas; ideal para audiencias de una sola condición o moderadamente complejas |
>| Composición de audiencia | La audiencia requiere la combinación, clasificación, división o exclusión de audiencias existentes | Lienzo visual para operaciones secuenciales; los resultados solo se evalúan por lotes; máximo de 10 bloques de composición por lienzo |
>| Composición de audiencia federada | Los criterios de audiencia deben evaluarse con datos de almacenes de datos externos sin ingerirlos en AEP | Consulta bases de datos externas directamente; evita la duplicación de datos; requiere una licencia de Composición de audiencias federada |

>[!NOTE]
>
>**Decisión: método de evaluación**
>
>¿Con qué rapidez deben entrar y salir los perfiles de la audiencia?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Lote | Campañas programadas, actualizaciones diarias de audiencias o lógica de segmentación compleja que no cumplen los requisitos para la transmisión | Procesa hasta 24 millones de perfiles por trabajo; se admiten todas las funciones de segmentación; se ejecuta en una programación (programación diaria predeterminada o personalizada) |
>| Transmisión | Cambios necesarios en la pertenencia a audiencias en tiempo real para la activación de destino de streaming o casos de uso activados por eventos | Casi en tiempo real (de segundos a minutos); conjunto de funciones de segmentación limitado: solo eventos simples, comparaciones de atributos y ventanas de tiempo limitado; sin consultas de varias entidades |
>| Edge | Personalización de la misma página o calificación de audiencia instantánea necesaria en el perímetro de | Latencia de milisegundos; conjunto de reglas más restrictivo: solo atributos de perfil y comprobaciones simples de pertenencia a segmentos; se utiliza principalmente para la personalización en el sitio (menos común para la activación de destino) |

>[!NOTE]
>
>**Decisión: política de combinación**
>
>¿Qué política de combinación debe utilizar la evaluación de audiencia?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Marca de tiempo solicitada (predeterminada) | La mayoría de los casos de uso: los datos recientes deben tener prioridad cuando entran en conflicto fragmentos de perfil | Más común; utiliza el valor de atributo actualizado más recientemente |
>| Prioridad de conjuntos de datos | Las fuentes de datos específicas deben sobrescribir las demás, independientemente de la marca de tiempo | Requiere definir un orden de prioridad de conjunto de datos; útil cuando un sistema de registro CRM siempre debe anular los datos recopilados en la web |

**Navegación de la interfaz de usuario:** Cliente > Audiencias > Crear audiencia > Generar regla (para Generador de segmentos) o Componer audiencia (para Composición de audiencias)

**Detalles de configuración de clave:**

- Defina criterios de audiencia basados en el caso de uso: atributos de perfil, eventos de comportamiento, pertenencia a segmentos o condiciones basadas en el tiempo
- Aplique reglas de supresión para excluir perfiles que no deban activarse (por ejemplo, recién convertidos, con suscripción global cancelada)
- Valide el tamaño de la población de audiencia antes de continuar con la activación
- Confirme que el método de evaluación se ajusta al tipo de destino seleccionado en la Fase 2.

**Donde las opciones difieren:**

**Para Opción A (Activación De Destino De Transmisión):**
La audiencia debe utilizar la transmisión o la evaluación de Edge para ofrecer actualizaciones de la membresía en tiempo real. Compruebe que la expresión de regla de segmento cumple los requisitos para la evaluación de flujo continuo: evite las funciones de agregación basadas en el tiempo, las consultas de varias entidades y las referencias de `inSegment()` a segmentos de solo lote.

**Para Opción B (Activación De Destino Por Lotes):**
Cualquier método de evaluación funciona. La evaluación por lotes es la opción más común, ya que la exportación en sí se ejecuta según una programación. Confirme que existe una programación de evaluación por lotes en la zona protegida o cree una.

**Para Opción C (Activación De Varios Destinos):**
El método de evaluación debe adaptarse al destino más exigente. Si algún destino requiere streaming, la audiencia debe utilizar la evaluación de streaming. Si todos los destinos son por lotes, la evaluación por lotes es suficiente.

**Documentación de Experience League:**

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/pql/overview)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Resumen de composición de audiencia](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/audience-composition)
- [Métodos de evaluación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home#evaluation-methods)


### Fase 2: Configuración del destino

**Función de aplicación:** RT-CDP: Configuración de destino

**Lo que va a configurar:** Establezca conexiones autenticadas con los destinos externos donde se publicarán las audiencias. Esto incluye la selección del destino en el catálogo, el suministro de credenciales de autenticación y la configuración de parámetros específicos de destino, como el formato de archivo, la ubicación de almacenamiento y la programación de exportaciones. Cada destino requiere su propia configuración de conexión.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: tipo de destino**
>
>¿Dónde se deben entregar las audiencias?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Destino de Advertising (streaming) | Segmentación o supresión en plataformas de publicidad (Facebook, Google Ads, LinkedIn, The Trade Desk, etc.) | Conectores de streaming; actualizaciones de suscripciones en tiempo casi real; coincidencia de identidades mediante correo electrónico, teléfono o ID de dispositivo con hash |
>| Destino de almacenamiento en la nube (lote) | Exportación a S3, Azure Blob, GCS, SFTP o zona de aterrizaje de datos para ampliar el Data Warehouse | Exportación basada en archivos; formato configurable (CSV, JSON, Parquet); cadencia programada |
>| destino CRM | Sincronizar audiencias con Salesforce, Microsoft Dynamics o HubSpot para la activación de ventas | Normalmente streaming; requiere asignación de campos específica de CRM; puede necesitar permisos de administración de CRM |
>| Destino del socio de datos | Uso compartido de datos de audiencia con socios de medición o segmentación | Varía por socio; revise las implicaciones de gobernanza de compartir datos externamente |
>| Destino personalizado (Destination SDK) | Sistema de destino no disponible en el catálogo | Requiere crear un destino personalizado con Destination SDK; mayor esfuerzo de implementación |

>[!NOTE]
>
>**Decisión: método de autenticación**
>
>¿Qué credenciales requiere el destino?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| OAuth 2.0 | Plataformas de publicidad y destinos SaaS (Facebook, Google, Salesforce) | Requiere un flujo de autorización inicial; los tokens se actualizan automáticamente; el más común es el de los destinos de flujo |
>| Clave de acceso/Clave secreta | Almacenamiento en la nube (S3, Azure Blob) | Credenciales estáticas; la rotación debe planificarse; adecuado para destinos basados en archivos |
>| Cuenta de servicio/clave de API | API de socios e integraciones personalizadas | Requiere el aprovisionamiento de credenciales del socio de destino |
>| Cadena de conexión | Destinos basados en Azure | Cadena única que contiene todos los parámetros de conexión |

>[!NOTE]
>
>**Decisión: Tipo de exportación (solo destinos por lotes)**
>
>¿Cómo se deben empaquetar los datos de audiencia para su exportación?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Exportación incremental | Solo nuevas cualificaciones y descalificaciones desde la última exportación | Tamaños de archivo más pequeños; procesamiento más rápido en el destino; requiere un sistema de destino para mantener el estado |
>| Exportación completa | Completar instantánea de audiencia en cada ejecución | Archivos más grandes; el destino obtiene una imagen completa cada vez; más sencillo para los sistemas que realizan una sustitución completa |

**Navegación por la interfaz de usuario:** Conexiones > Destinos > Catálogo > [Seleccionar destino] > Configurar

**Detalles de configuración de clave:**

- Examine el catálogo de destino y seleccione el destino de destino
- Proporcione credenciales de autenticación y pruebe la conexión
- Para destinos por lotes: configure el formato de archivo (CSV, JSON, Parquet), la compresión, la plantilla de nomenclatura de archivos y la programación de exportación
- Para destinos de flujo continuo: la conexión se suele establecer mediante el flujo de autorización de OAuth
- Compruebe que el estado de la conexión de destino se muestra como activa antes de continuar con la activación

**Donde las opciones difieren:**

**Para Opción A (Activación De Destino De Transmisión):**
Seleccione un destino de flujo continuo del catálogo (categorías Advertising o Social). Complete el flujo de autorización de OAuth. La conexión está lista para activarse una vez confirmada la autorización.

**Para Opción B (Activación De Destino Por Lotes):**
Seleccione un destino basado en archivos del catálogo (categoría Almacenamiento en la nube). Configure la ruta de almacenamiento, el formato de archivo, la compresión, la convención de nomenclatura y la programación de exportación. Compruebe la conexión comprobando el acceso de escritura a la ubicación de almacenamiento.

**Para Opción C (Activación De Varios Destinos):**
Repita esta fase para cada destino. Cada conexión es independiente: puede tener una combinación de destinos de flujo continuo y por lotes. Documente la autenticación y configuración de cada conexión para referencia operativa.

**Documentación de Experience League:**

- [Catálogo de destinos](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/overview)
- [Información general sobre los destinos](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/home)
- [Activar audiencias para destinos de exportación de perfiles por lotes](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Activar audiencias en destinos de flujo continuo](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Información general de Destination SDK](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/destination-sdk/overview)
- [Opciones de configuración de Destination SDK](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/destination-sdk/functionality/configuration-options)


### Fase 3: Activación de audiencia

**Función de aplicación:** RT-CDP: Audience Activation

**Lo que configurará:** Publique la audiencia evaluada en el destino configurado creando el flujo de datos de activación. Esto implica seleccionar qué audiencias activar, asignar atributos de perfil a campos de destino y configurar la programación de exportación. El flujo de datos de activación conecta la audiencia de origen con el destino de destino y administra la entrega de datos en curso.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: asignación de atributos**
>
>¿Qué atributos de perfil deben incluirse en la activación?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Solo campos de identidad | El destino solo debe coincidir con los perfiles (por ejemplo, pertenencia a audiencias en plataformas de publicidad) | Transferencia de datos mínima; la mayoría de las opciones de privacidad son seguras; lo habitual en la segmentación y supresión de plataformas publicitarias |
>| Identidad + atributos de perfil | El destino necesita atributos de enriquecimiento para la personalización o segmentación (por ejemplo, sincronización con CRM, uso compartido de socios) | Más datos transferidos; requiere una revisión de la gobernanza para cada atributo; compruebe las etiquetas de uso de datos con la acción de marketing de destino |
>| Identidad + atributos calculados | El destino se beneficia de puntuaciones o agregaciones derivadas (por ejemplo, nivel de valor de duración, puntuación de tendencia para la segmentación por socios) | Requiere la configuración de atributos calculados; enriquecimiento de alto valor para sistemas posteriores |

>[!NOTE]
>
>**Decisión: Programación de exportación (solo destinos por lotes)**
>
>¿Con qué frecuencia se deben exportar los datos de audiencia?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Diario | Cadencia de actualización estándar; la mayoría de los casos de uso por lotes | Equilibra la actualización con el coste de procesamiento; valor predeterminado más común |
>| Cada 3 a 6 horas | Casos de uso de mayor frecuencia, como la optimización de campañas en el día | Generación de archivos más frecuente; mayor carga de almacenamiento y procesamiento en el destino |
>| Bajo demanda (ad hoc) | Exportación única o activación urgente fuera de ciclo | El déclencheur manual evita la programación; útil para pruebas o necesidades urgentes de la campaña |

**Navegación de la interfaz de usuario:** Conexiones > Destinos > Examinar > [Seleccionar destino] > Activar audiencias

**Detalles de configuración de clave:**

- Seleccione una o varias audiencias para activarlas en el destino
- Asignar atributos de perfil y campos de identidad a campos específicos de destino
- Para destinos de flujo continuo: confirme la asignación del área de nombres de identidad (por ejemplo, correo electrónico con hash al extern_id de Facebook).
- Para destinos por lotes: configure la programación de exportación, seleccione el modo de exportación incremental o completa y establezca la primera fecha de exportación
- Revise el resumen de activación para confirmar todas las asignaciones y programaciones antes de publicar

**Donde las opciones difieren:**

**Para Opción A (Activación De Destino De Transmisión):**
Seleccione las audiencias y asigne las áreas de nombres de identidad a los campos de identidad de destino. La activación comienza inmediatamente después de la publicación: la pertenencia a la audiencia cambia de forma continua al destino en tiempo casi real. No es necesario ningún programa de exportación; la activación es continua.

**Para Opción B (Activación De Destino Por Lotes):**
Seleccione las audiencias, asigne los atributos de perfil y configure la programación de exportación. Elija entre los modos de exportación incremental y completo. Si lo desea, puede exportar una déclencheur ad hoc para su envío inmediato fuera del horario habitual.

**Para Opción C (Activación De Varios Destinos):**
Repita el flujo de trabajo de activación para cada destino. La misma audiencia se puede activar en varios destinos con diferentes asignaciones de atributos por destino. Por ejemplo, enviar solo correo electrónico con hash a las plataformas de publicidad, pero incluir atributos demográficos a CRM.

**Documentación de Experience League:**

- [Activar audiencias en destinos de flujo continuo](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Activar audiencias para destinos de exportación de perfiles por lotes](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Activar audiencias bajo demanda en destinos por lotes](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [Monitorización de flujos de datos para destinos](https://experienceleague.adobe.com/es/docs/experience-platform/dataflows/ui/monitor-destinations)


### Fase 4: Validación de la gobernanza

**Función de la aplicación:** RT-CDP: Cumplimiento del consentimiento y la gobernanza

**Lo que configurará:** Valide que las directivas de gobernanza y las preferencias de consentimiento se apliquen correctamente antes y durante la activación. Esta fase garantiza que los datos restringidos (PII, atributos confidenciales) no se envíen a destinos no autorizados y que los perfiles sin consentimiento válido se excluyan de la activación. La aplicación de la gobernanza se produce automáticamente en el momento de la activación, pero la validación proactiva evita activaciones bloqueadas y violaciones del cumplimiento.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: enfoque de cumplimiento de la gobernanza**
>
>¿Cuándo se debe validar el cumplimiento de la gobernanza?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Proactivo (preactivación) | Recomendado para todas las implementaciones, especialmente al activarse en sistemas externos de terceros | Revise las etiquetas y políticas de uso de datos antes de configurar las asignaciones de campos; evita errores de activación y garantiza el cumplimiento desde el principio |
>| Reactiva (en el momento de la activación) | Cuando las políticas de gobernanza ya están bien establecidas y el equipo confía en el cumplimiento | Platform aplica las directivas automáticamente en la activación; las infracciones bloquean la activación o excluyen los atributos restringidos; pueden provocar errores inesperados si las directivas no se comprenden bien |

>[!NOTE]
>
>**Decisión: filtrado de consentimiento**
>
>¿Cómo deberían afectar las preferencias de consentimiento a la activación?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Aplicación del consentimiento habilitada | Necesario para la activación en destinos de publicidad o marketing en los que el consentimiento es obligatorio legalmente | Los perfiles sin consentimiento válido (conents.marketing.{channel}.val = &#39;y&#39;) se excluyen automáticamente de la activación; requiere que se introduzcan datos de consentimiento |
>| Sin filtrado de consentimiento | Destinos de uso interno o exportaciones de análisis en los que el consentimiento no se aplica a la transferencia de datos | Solo es adecuado cuando el uso de datos no constituye una acción de marketing que requiera consentimiento; consulte con el equipo legal/de privacidad |

**Navegación de la interfaz de usuario:** Privacidad > Políticas > Políticas de consentimiento (para revisión de consentimiento); Control de datos > Políticas (para revisión de políticas de uso de datos)

**Detalles de configuración de clave:**

- Revise las etiquetas de uso de datos aplicadas a los conjuntos de datos y los campos de esquema que se están activando
- Compruebe que las políticas de gobernanza estén activas para la acción de marketing asociada al destino (por ejemplo, &quot;Exportar a terceros&quot; para plataformas de publicidad)
- Confirme que los campos de consentimiento se rellenan en perfiles y que la aplicación del consentimiento está habilitada para los canales relevantes
- Si se detectan infracciones de directivas, resuelva eliminando los campos restringidos de la asignación de destino o seleccionando un destino alternativo

**Documentación de Experience League:**

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Aplicación de políticas](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/enforcement/overview)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [Aplicación de políticas de consentimiento](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/policies/user-guide)


### Fase 5: Monitorización y validación

**Función de aplicación:** Supervisión y observabilidad

**Lo que configurará:** configure la monitorización continua de los flujos de datos de activación, configure alertas para detectar errores, valide la población de audiencias en los destinos y rastree el uso de licencias. La monitorización es crítica para las activaciones de producción en las que los errores de entrega afectan directamente al rendimiento de la campaña y al gasto en medios.

**Detalles de configuración de clave:**

- Revise el estado de ejecución del flujo de datos de cada destino activo para confirmar que las audiencias se entregan correctamente
- Configure alertas para errores de activación de destino, retrasos de flujo de datos y anomalías de población de audiencia
- Seguimiento de perfiles exportados frente a perfiles con errores por ejecución de flujo de datos
- Monitorizar las tasas de coincidencia de audiencia en el destino (donde los informes de destino están disponibles)
- Revise el uso de la licencia para rastrear el volumen del perfil activado en relación con los derechos

**Navegación de la interfaz de usuario:** Conexiones > Destinos > Examinar > [Seleccionar destino] > Ejecuciones del flujo de datos (para la supervisión de la activación); Alertas > Reglas de alerta > Suscribirse (para la configuración de alertas); Administración > Uso de licencias (para el seguimiento de licencias)

**Documentación de Experience League:**

- [Monitorización de flujos de datos para destinos](https://experienceleague.adobe.com/es/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Resumen de alertas](https://experienceleague.adobe.com/es/docs/experience-platform/observability/alerts/overview)
- [Resumen de Observability Insights](https://experienceleague.adobe.com/es/docs/experience-platform/observability/home)
- [Panel de control de uso de licencias](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

## Consideraciones sobre la implementación

Revise las siguientes consideraciones antes y durante la implementación.

### Protecciones y límites

- **Límite de definición de segmento:** Máximo de 4000 definiciones de segmento por zona protegida — [Protecciones de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- **Flujos de datos por destino:** Un máximo de 100 flujos de datos por conexión de destino: [Protecciones de destinos](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/guardrails)
- **Tamaño de archivo de exportación por lotes:** Los destinos basados en archivos tienen límites máximos de tamaño de archivo de exportación; las audiencias grandes se dividen automáticamente en varios archivos
- **Rendimiento de destino de streaming:** Cada socio de destino establece límites de rendimiento por segundo; los cambios de audiencia de gran volumen pueden verse limitados
- **Capacidad de evaluación por lotes:** Hasta 24 millones de perfiles por trabajo de evaluación de segmentos de forma predeterminada
- **Composición de audiencia:** máximo de 10 bloques de composición por lienzo; las audiencias compuestas solo se evalúan por lotes
- **Gráfico de identidad:** Máximo de 50 identidades por gráfico: [protecciones del servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/guardrails)
- **Atributos calculados:** Máximo de 25 atributos calculados por zona protegida — [Protecciones de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview#guardrails)
- **Introducción a las protecciones de activación:** [Protecciones de activación](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/guardrails)

### Peligros comunes

- **Segmento de streaming con lógica de regla no apta:** Definir una audiencia con funciones de agregación complejas o consultas de varias entidades y esperar evaluación de streaming. Estos segmentos vuelven silenciosamente a la evaluación por lotes, lo que provoca una latencia inesperada. Prevención: revise los requisitos de idoneidad para el streaming antes de definir la audiencia.

- **No se exportaron perfiles debido al filtrado de consentimiento:** Todos los perfiles de la audiencia carecen de valores de consentimiento válidos, lo que provoca que se filtre toda la audiencia en el momento de la activación. Prevención: compruebe que la ingesta de datos de consentimiento esté operativa y que los campos de consentimiento se rellenen antes de activarlos.

- **Inesperadamente, la directiva de gobernanza bloquea la activación:** Las etiquetas de uso de datos en los campos de esquema infringen la directiva de déclencheur que impide la activación. Prevención: evalúe el cumplimiento de la gobernanza de forma proactiva (Fase 4) antes de configurar las asignaciones de campo. Revise qué etiquetas se heredan del esquema.

- **Caducidad de la credencial de destino:** caducan los tokens de OAuth o las claves de API, lo que provoca errores de activación sin una alerta inmediata. Prevención: configure alertas para errores de activación de destino y establezca un programa de rotación de credenciales.

- **Áreas de nombres de identidad no coincidentes:** El área de nombres de identidad configurada en la asignación de activación no coincide con lo que espera el destino (por ejemplo, enviar correo electrónico de texto sin formato cuando el destino requiere correo electrónico con hash SHA-256). Prevención: revise la documentación de destino para ver los formatos de identidad necesarios antes de configurar la asignación.

- **Errores de asignación de campos que producen errores de exportación:** Asignación de un atributo de perfil a un campo de destino con un tipo o formato de datos incompatible. Prevención: pruebe primero la activación con una audiencia pequeña y revise los detalles de ejecución del flujo de datos para detectar errores de asignación antes de escalar a audiencias de producción.

- **Diferencia de población de audiencia entre RT-CDP y destino:** El recuento de público de RT-CDP no coincide con el recuento en el destino debido a diferencias de coincidencia de identidad, lógica de deduplicación de destino o tiempo. Este es un comportamiento esperado — prevención: documentar los puntos de referencia de la tasa de coincidencia esperada por destino y monitorizar las desviaciones significativas.

### Prácticas recomendadas

- **Comience con una audiencia de prueba:** Active una audiencia de prueba pequeña y bien entendida para cada nuevo destino antes de activar audiencias de producción. Valide asignaciones de campos, coincidencia de identidades y métricas de envío con la audiencia de prueba.

- **Gobernanza de capas antes:** Aplique etiquetas de uso de datos y configure directivas de gobernanza antes de configurar activaciones de destino. Esto evita las activaciones bloqueadas y garantiza el cumplimiento desde el principio.

- **Usar exportaciones incrementales para destinos por lotes:** Las exportaciones incrementales reducen el tamaño de los archivos, aceleran el procesamiento en el destino y minimizan los costos de almacenamiento. Utilice exportaciones completas solo cuando el sistema de destino requiera un reemplazo completo de la audiencia.

- **Estandarizar las convenciones de nomenclatura:** Establezca un nombre coherente para las audiencias, las conexiones de destino y los flujos de datos en toda la organización. Incluya el caso de uso, el destino y el método de evaluación en los nombres (por ejemplo, &quot;Suppression_ExistingCustomers_Facebook_Streaming&quot;).

- **Monitorizar tasas de coincidencia:** Rastree la proporción de perfiles exportados de RT-CDP a perfiles coincidentes en cada destino. Las caídas significativas en la tasa de coincidencia pueden indicar problemas de resolución de identidad, problemas de credenciales o cambios en la API de destino.

- **Coordinar la supresión en todos los destinos:** Al usar audiencias de supresión (por ejemplo, al excluir a los clientes existentes de las campañas de adquisición), active la audiencia de supresión en todas las plataformas de publicidad relevantes de forma simultánea para mantener la coherencia.

- **Revisar y eliminar activaciones inactivas:** revisar periódicamente los flujos de datos de destino y desactivar las audiencias que ya no sean necesarias. Las activaciones inactivas consumen capacidad de licencia y añaden sobrecarga de monitorización.

### Decisiones de compensación

>[!NOTE]
>
>**Compensación: Actualización de audiencia vs. flexibilidad de segmentación**
>
>La evaluación de streaming ofrece actualizaciones de audiencia casi en tiempo real, pero restringe las funciones de reglas de segmentos que puede utilizar. La evaluación por lotes admite el conjunto de funciones de regla de segmento completo, pero introduce latencia (horas en lugar de minutos).
>
>- **Favoritos de streaming:** Casos de uso en tiempo real en los que el abono a audiencia debe reflejarse en el destino en cuestión de minutos (supresión de campaña activa, redireccionamiento en tiempo real)
>- **Favoritos por lotes:** lógica de audiencia compleja que requiere funciones de agregación, consultas de varias entidades o condiciones de ventana de tiempo grande (niveles de valor de duración, segmentos de comportamiento multitáctiles)
>- **Recomendación:** Use la evaluación de flujo continuo para audiencias activadas en destinos de flujo continuo donde la actualización en tiempo real aporta valor empresarial. Utilice la evaluación por lotes para audiencias complejas activadas en destinos basados en archivos o cuando la actualización diaria sea suficiente. Para las audiencias que necesitan ambas, considere la posibilidad de crear dos versiones: un segmento de streaming simplificado para la activación en tiempo real y un segmento de lote completo para el enriquecimiento periódico.

>[!NOTE]
>
>**Compensación: exportación de datos mínima frente a asignación de atributos enriquecidos**
>
>Exportar solo campos de identidad (correo electrónico con hash, ID de dispositivo) minimiza la exposición a los datos y simplifica el control. La exportación de atributos de perfil adicionales (demografía, nivel de valor, puntuación de participación) enriquece el destino, pero aumenta la complejidad de la gobernanza y la responsabilidad de los datos.
>
>- **Favoritos mínimos de exportación:** enfoque que da prioridad a la privacidad; menor riesgo de gobernanza; asignación de campos más sencilla; suficiente para la mayoría de los casos de uso de direccionamiento y supresión de plataformas publicitarias
>- **Favoritos de exportación enriquecidos:** personalización descendente en el destino; enriquecimiento de CRM; uso compartido de datos de socios que requiere detalles de nivel de atributo
>- **Recomendación:** De forma predeterminada, se obtienen exportaciones mínimas solo de identidad para destinos publicitarios. Añada atributos de perfil solo cuando el caso de uso de destino los requiera específicamente y la revisión de la gobernanza confirme el cumplimiento. Utilice atributos calculados para proporcionar valores de enriquecimiento agregados y menos confidenciales en lugar de PII sin procesar.

>[!NOTE]
>
>**Compensación: audiencia única por destino frente a flujos de datos consolidados de varias audiencias**
>
>La activación de cada audiencia como un flujo de datos independiente proporciona aislamiento y monitorización granular. La activación de varias audiencias a través de un único flujo de datos a un destino simplifica la administración pero reduce el aislamiento.
>
>- **Favor de flujos de datos separados:** Supervisión independiente, solución de problemas más sencilla, capacidad de pausar activaciones de audiencias individuales sin afectar a otras
>- **Los flujos de datos consolidados favorecen:** Menos conexiones que mantener, administración simplificada de credenciales y menos gastos operativos
>- **Recomendación:** Utilice flujos de datos consolidados al activar varias audiencias relacionadas en el mismo destino (por ejemplo, todos los segmentos de supresión en Facebook). Utilice flujos de datos independientes cuando las audiencias tengan diferentes SLA, asignaciones de atributos diferentes o cuando el aislamiento de errores sea crítico.

## Documentación relacionada

**Destinos**

- [Información general sobre los destinos](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/overview)
- [Activar audiencias en destinos de flujo continuo](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Activar audiencias para destinos de exportación de perfiles por lotes](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Activar audiencias bajo demanda en destinos por lotes](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [Protecciones de destinos](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/guardrails)
- [Información general de Destination SDK](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/destination-sdk/overview)

**Audiencias y segmentación**

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/pql/overview)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Resumen de composición de audiencia](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/audience-composition)
- [Protecciones de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)

**Identidad y perfil**

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Reglas de vinculación de gráficos de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/identity-linking-logic)
- [Resumen del perfil](https://experienceleague.adobe.com/es/docs/experience-platform/profile/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview)

**Esquemas y modelado de datos**

- [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/composition)

**Gobernanza de datos**

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Políticas de gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/policies/overview)
- [Aplicación de políticas](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/enforcement/overview)
- [Consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**Control y observabilidad**

- [Monitorización de flujos de datos para destinos](https://experienceleague.adobe.com/es/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Resumen de alertas](https://experienceleague.adobe.com/es/docs/experience-platform/observability/alerts/overview)
- [Resumen de Observability Insights](https://experienceleague.adobe.com/es/docs/experience-platform/observability/home)
- [Panel de control de uso de licencias](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**Atributos calculados**

- [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview)
- [Guía de IU de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/ui)

**Recopilación de datos y orígenes**

- [Resumen de orígenes](https://experienceleague.adobe.com/es/docs/experience-platform/sources/home)
- [Información general de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure)

**Administración**

- [Información general de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home)
- [Información general de control de acceso](https://experienceleague.adobe.com/es/docs/experience-platform/access-control/home)
- [Control de acceso basado en atributos](https://experienceleague.adobe.com/es/docs/experience-platform/access-control/abac/overview)

**Protecciones**

- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- [Protecciones del servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/guardrails)
- [Protecciones de activación](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/guardrails)
- [Protecciones de ingesta](https://experienceleague.adobe.com/es/docs/experience-platform/ingestion/guardrails)
