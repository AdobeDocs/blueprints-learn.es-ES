---
title: Reenvío de eventos
description: Aprenda a reenviar datos de evento en tiempo real recopilados mediante Edge Network a destinos que no sean de Adobe para análisis, almacenamiento o publicidad.
solution: Experience Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '6342'
ht-degree: 0%

---


# Reenvío de eventos

Esta guía cubre la implementación del reenvío de eventos del lado del servidor mediante [!DNL Adobe Experience Platform] Edge Network. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten distribuir datos de eventos en tiempo real recopilados mediante Edge Network a destinos que no sean de Adobe, como plataformas de análisis de terceros, extremos de almacenamiento en la nube, redes de publicidad o ganchos web personalizados.

Presenta todos los enfoques viables para configurar el reenvío de eventos, explica las compensaciones entre ellos y vincula la documentación de [!DNL Adobe Experience League] para obtener instrucciones de procedimiento detalladas.

## Resumen del caso de uso

Las organizaciones que recopilan datos de comportamiento a través de la API de servidor, SDK móvil o Web SDK [!DNL Adobe Experience Platform] suelen tener que compartir el mismo flujo de eventos con sistemas que no sean de Adobe (plataformas de análisis como [!DNL Google Analytics] o [!DNL Snowflake], redes de publicidad para el seguimiento de conversiones, almacenes de datos para almacenamiento a largo plazo o servicios internos personalizados). Tradicionalmente, esto requería la proliferación de etiquetas del lado del cliente, que aumenta el peso de la página, introduce latencia y crea riesgos de privacidad y gobernanza.

El reenvío de eventos resuelve esto al operar en el lado del servidor en Edge Network. Cuando la interacción de un visitante déclencheur un evento a través de la API del servidor o Web SDK, ese evento se enruta a través de un conjunto de datos a Edge Network. Reglas de reenvío de eventos (configuradas en una propiedad de reenvío de eventos específica) evalúan los datos de evento entrantes y los reenvían de forma selectiva a uno o varios destinos configurados. Este método del lado del servidor reduce la sobrecarga de etiquetas del lado del cliente, mejora el rendimiento de la página, centraliza la gobernanza de datos y proporciona a la organización control sobre los datos que salen del ecosistema de Adobe.

La audiencia de destino de este patrón incluye organizaciones que ya han implementado (o planean implementar) la API de servidor o Web SDK [!DNL Adobe Experience Platform] para la recopilación de datos y desean ampliar esa inversión distribuyendo datos de evento a extremos que no sean de Adobe sin agregar etiquetas de JavaScript del lado del cliente.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Mejore la calidad y la gobernanza de los datos

Garantice datos limpios, completos y compatibles para un direccionamiento preciso, una reducción de residuos y análisis fiables. El reenvío de eventos centraliza la distribución de datos en el servidor, lo que proporciona a la organización un único punto de control sobre los datos que se comparten con sistemas externos, reduce el riesgo de fuga de datos y garantiza que las políticas de gobernanza se apliquen antes de que los datos salgan de la Edge Network [!DNL Adobe].

**KPI:** eficiencia, ahorros en costos

Para obtener más información, consulte [Mejorar la calidad y el control de los datos](../../business-objectives/cost-efficiency/improve-data-quality-governance.md).

### Consolidar y modernizar la tecnología de marketing

Reduzca la fragmentación de herramientas y la deuda técnica migrando a plataformas unificadas y escalables. El reenvío de eventos permite a las organizaciones reemplazar varias etiquetas de proveedor del lado del cliente con un único mecanismo de distribución de datos del lado del servidor, lo que reduce la sobrecarga de carga de página y simplifica la pila de tecnología.

**KPI:** Ahorro en costos, eficiencia y velocidad de comercialización

Para obtener más información, vea [Consolidar y modernizar la tecnología de marketing](../../business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md).

## Casos de uso tácticos de ejemplo

Los siguientes son escenarios tácticos comunes en los que se aplica este patrón de caso de uso.

- **Enriquecimiento de análisis de terceros**: reenvía eventos de visualización de página, clics y conversión a [!DNL Google Analytics], [!DNL Snowflake] u otras plataformas de análisis en tiempo real sin agregar etiquetas del lado del cliente
- **Seguimiento de conversión de Advertising**: envíe eventos de compra y de generación de posibles clientes a la API de conversiones [!DNL Meta], [!DNL Google Ads], [!DNL TikTok] o [!DNL Snap] para la medición y optimización de conversiones en el servidor
- **Flujo de Data Warehouse**: enrute los datos de evento sin procesar a un almacén de datos en la nube ([!DNL Google BigQuery], [!DNL Amazon S3], [!DNL Azure Event Hubs]) para el almacenamiento a largo plazo y el análisis sin conexión
- **Integración de ganchos web personalizados**: reenvíe datos de evento filtrados o transformados a microservicios internos, sistemas CRM o plataformas asociadas a través de extremos HTTP
- **Reducción de etiquetas y mejora del rendimiento de la página**: reemplace varias etiquetas JavaScript de proveedor del lado del cliente con una sola implementación de Web SDK más reglas de reenvío de eventos del lado del servidor, reduciendo el peso de la página y mejorando Core Web Vitals
- **Uso compartido de datos compatible con la privacidad**: aplique reglas de filtrado de datos y de redacción en el nivel de campo en el servidor antes de compartir datos de evento con terceros, asegurándose de que la PII se elimine o se utilice como hash antes de que llegue a los sistemas externos
- **Distribución de eventos en varias nubes**: reenvía simultáneamente el mismo flujo de eventos a varios destinos (por ejemplo, análisis, publicidad y Data Warehouse) desde un único conjunto de reglas del lado del servidor
- **Reenvío de señales de fraude en tiempo real**: reenvíe eventos de transacciones de alto valor a sistemas de detección de fraude para la puntuación y las alertas de riesgos en tiempo real

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir el éxito de este patrón de caso de uso.

- **Reducción del tiempo de carga de la página**: se ha medido la mejora en la velocidad de carga de la página y en Core Web Vitals después de migrar las etiquetas del lado del cliente al reenvío de eventos del lado del servidor
- **Tasa de éxito de entrega de datos**: porcentaje de eventos reenviados correctamente a extremos de destino sin errores ni tiempos de espera
- **Reducción de recuento de etiquetas**: número de etiquetas de proveedor del lado del cliente eliminadas después de implementar equivalentes del lado del servidor
- **Actualización/latencia de datos**: tiempo entre la ocurrencia del evento en el cliente y la llegada del evento en el extremo de destino (destino: de subsegundo a segundos)
- **Tasa de cumplimiento de control**: porcentaje de recursos compartidos de datos salientes que pasan por las reglas de filtrado del lado del servidor, lo que garantiza que ningún PII o datos restringidos llegue a destinos no autorizados
- **Eficiencia operativa**: reducción en las horas de desarrollador que invierten en administrar implementaciones de etiquetas del lado del cliente y en solucionar conflictos de etiquetas

## Patrón de caso de uso

En esta sección se describe el patrón y la cadena de funciones utilizada para implementar el reenvío de eventos.

**Reenvío de eventos**: reenvía datos de eventos en tiempo real recopilados mediante Edge Network a destinos que no sean de Adobe para análisis, almacenamiento o publicidad.

**Cadena De Funciones:** Configuración De Flujo De Datos > Definición De Regla De Evento > Asignación De Destino > Ejecución De Reenvío > Supervisión

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Adobe Experience Platform] (Edge Network)**: recibe y enruta datos de evento en tiempo real desde Web SDK, Mobile SDK o la API de servidor a través de flujos de datos configurados
- **[!DNL Adobe Experience Platform] (Reenvío de eventos)**: proporciona el motor de reglas del lado del servidor para evaluar, filtrar, transformar y reenviar datos de eventos a destinos externos
- **[!DNL Adobe Experience Platform] (Etiquetas / Recopilación de datos)**: administra el ciclo de vida de la propiedad de reenvío de eventos, las extensiones, las reglas y el flujo de trabajo de publicación

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Requerido | Una zona protegida debe estar activa con las funciones de usuario y los permisos adecuados configurados. Los usuarios que administran el reenvío de eventos necesitan permisos de recopilación de datos en [!DNL Adobe Admin Console], incluidos los derechos para administrar las propiedades, extensiones y reglas del reenvío de eventos. | [Resumen de control de acceso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | Se deben definir esquemas XDM para los datos de evento que fluyen a través de Edge Network. La secuencia de datos debe hacer referencia a un esquema XDM ExperienceEvent válido para que las reglas del reenvío de eventos puedan acceder a campos estructurados para el filtrado, la transformación y la asignación. | [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home) |
| Fuentes de datos y recopilación | Requerido | Un mecanismo de recopilación de datos debe estar activo (Web SDK, Mobile SDK o API de servidor de Edge Network) y enviar eventos a través de un flujo de datos configurado. La secuencia de datos es la capa de enrutamiento fundamental que conecta la colección del lado del cliente con el reenvío de eventos del lado del servidor. | [Configurar flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Configuración de identidad y perfil | No aplicable | El reenvío de eventos funciona con datos de evento sin procesar en la capa de Edge Network, antes de que se produzca la resolución de identidades o la unificación de perfiles. Las áreas de nombres de identidad y las políticas de combinación no son necesarias a menos que los eventos reenviados también tengan que contribuir al Perfil del cliente en tiempo real (que es una configuración de servicio de flujo de datos independiente, no un problema de reenvío de eventos). | |
| Definición de audiencia y segmentación | No aplicable | El reenvío de eventos procesa eventos individuales en tiempo real y no evalúa la pertenencia a audiencias. El filtrado basado en audiencias no forma parte de la cadena de funciones del reenvío de eventos. Si es necesaria la activación basada en audiencias, consulte el plan de referencia de Audience Activation a destinos. | |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | No aplicable | El reenvío de eventos funciona con datos de evento sin procesar, no con atributos calculados de nivel de perfil. Los atributos calculados no están disponibles en el contexto del reenvío de eventos. | |
| Administración del ciclo de datos | Recomendado | Si los datos de evento también se están introduciendo en conjuntos de datos de AEP (a través del mismo flujo de datos), deben configurarse políticas de retención de datos (caducidad) para esos conjuntos de datos a fin de administrar los costes de almacenamiento y el cumplimiento de la normativa. El reenvío de eventos en sí no almacena datos, pero la ruta de ingesta de AEP paralela sí. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Etiquetado y aplicación del uso de datos | Recomendado | Aunque las reglas del reenvío de eventos proporcionan un filtrado a nivel de campo (que le permite excluir datos confidenciales de las cargas útiles reenviadas), la aplicación de etiquetas de uso de datos a los esquemas y conjuntos de datos subyacentes garantiza que las políticas de gobernanza se apliquen si los mismos datos se utilizan para la activación o personalización de audiencias. | [Resumen de control de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Monitorización y observabilidad | Incluido | La monitorización es esencial para el reenvío de eventos. El panel Supervisión del reenvío de eventos proporciona visibilidad sobre las tasas de éxito de reenvío, las tasas de error y los códigos de respuesta de destino. Las alertas deben configurarse para los errores de destino. | [Supervisión del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring) |
| Informes y análisis | Recomendado | Si los eventos reenviados alimentan una plataforma de análisis de terceros, considere la posibilidad de conectar los mismos conjuntos de datos de eventos de AEP a CJA para obtener una vista unificada en canales múltiples. Esto permite comparar análisis del lado de Adobe con análisis de terceros. | [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del Catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Adobe Experience Platform] (AEP)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Configuración de flujo de datos | Fase 1: Configuración del flujo de datos | Configuración de una secuencia de datos para recibir eventos de Edge Network y habilitar el servicio de reenvío de eventos |
| Configuración de propiedad de reenvío de eventos | Fase 2: Propiedad y extensiones del reenvío de eventos | Crear una propiedad de reenvío de eventos e instalar extensiones específicas de destino |
| Definición de regla de evento | Fase 3: Definición de regla de evento | Defina reglas que evalúen los datos de evento entrantes y determinen qué reenviar y dónde |
| Asignación de destino | Fase 3: Definición de regla de evento | Asignar elementos de datos de evento a formatos de carga útil específicos de destino dentro de las reglas de reenvío |
| Reenviando ejecución | Fase 4: Publicación y activación | Publicar la configuración del reenvío de eventos en Edge Network para su ejecución en directo |
| Monitorización | Fase 5: Monitorización y validación | Monitorizar las tasas de éxito de reenvío, los códigos de error y el estado de destino |

## Prerrequisitos

Asegúrese de que las siguientes opciones estén implementadas antes de comenzar la implementación.

- [ Licencia de ] [!DNL Adobe Experience Platform] con derecho de Edge Network y reenvío de eventos
- [ ] permisos de recopilación de datos configurados en [!DNL Adobe Admin Console] (administrar propiedades, extensiones, reglas y publicaciones para el reenvío de eventos)
- [ ]: al menos un mecanismo de recopilación de datos activo (Web SDK, Mobile SDK o API de servidor) que envía eventos a través de una secuencia de datos
- [ Esquema XDM ExperienceEvent ] definido para los datos de evento que se recopilan
- [ ] secuencia de datos creada y vinculada al mecanismo de recopilación
- [ ] credenciales y documentación de extremo de destino disponibles (por ejemplo, [!DNL Meta] token de acceso a la API de conversiones, [!DNL Google Analytics] ID de medición, URL de webhook, credenciales de almacenamiento en la nube)
- [ ] Descripción del modelo de datos de evento y de los campos/eventos que requiere cada destino

## Opciones de implementación

En esta sección se describen los enfoques disponibles para implementar el reenvío de eventos y se proporciona orientación para elegir la opción correcta.

### Opción A: reenvío de eventos basado en extensiones

**Ideal para:** equipos que utilizan plataformas de destino compatibles ([!DNL Meta], [!DNL Google], [!DNL AWS], [!DNL Azure], [!DNL Snowflake], etc.) que tienen extensiones de reenvío de eventos creadas previamente disponibles en el catálogo de recopilación de datos.

**Cómo funciona:**

El reenvío de eventos basado en extensiones aprovecha las integraciones creadas previamente y mantenidas por Adobe o socios de terceros. Cada extensión está diseñada específicamente para un destino específico y administra la autenticación, el formato de carga útil y la comunicación de extremos. El implementador instala la extensión en la propiedad de reenvío de eventos, configura las credenciales de autenticación y crea reglas que asignan elementos de datos XDM a los campos de acción de la extensión.

Este método minimiza el desarrollo personalizado, ya que la extensión abstrae los requisitos de API del destino. Por ejemplo, la extensión de la API de conversiones [!DNL Meta] traduce los eventos de comercio de XDM al formato que espera [!DNL Meta], y gestiona el hash de los campos PII, los parámetros de anulación de duplicación y la administración de tokens de acceso. Del mismo modo, las extensiones [!DNL Google Cloud Platform] o [!DNL AWS] administran la autenticación y el formato de carga útil para sus respectivos servicios en la nube.

La compensación es que la disponibilidad de la extensión determina qué destinos son compatibles. Si no existe ninguna extensión para un destino de destino, se debe utilizar la opción B (webhook personalizado).

**Consideraciones clave:**

- La disponibilidad de la extensión varía: compruebe el [catálogo de extensiones de recopilación de datos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview) antes de planificar
- Adobe o sus socios mantienen las extensiones; las actualizaciones pueden introducir cambios importantes que requieran ajustes de las reglas
- Algunas extensiones solo admiten tipos de evento específicos o requieren asignaciones de campo XDM específicas
- Las extensiones administran la autenticación y la administración de credenciales en su IU de configuración

**Ventajas:**

- El tiempo más rápido de implementación para los destinos admitidos
- El formato de carga útil generado previamente reduce los errores de asignación
- Administración de autenticación y credenciales gestionada por la extensión
- Mantenido y actualizado por Adobe o socios certificados
- Código personalizado reducido y menor carga de mantenimiento

**Limitaciones:**

- Limitado a destinos con extensiones disponibles
- Menos flexibilidad para personalizar la carga útil en comparación con los webhooks personalizados
- Las actualizaciones de extensión pueden requerir la reconfiguración de reglas
- Es posible que algunas extensiones no admitan todas las funciones de la API de destino

**Experience League:**

- [Catálogo de extensiones de reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Extensión de API de conversiones de Meta](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/meta/overview)
- [Extensión de Google Cloud Platform](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [Extensión de AWS](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/aws/overview)
- [Extensión de Snowflake](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/snowflake/overview)

### Opción B: reenvío de eventos de webhook personalizado (API de recuperación)

**Es ideal para:** equipos que necesitan reenviar eventos a destinos sin una extensión prediseñada o que requieren control total sobre la carga útil de la solicitud HTTP, los encabezados y el mecanismo de autenticación.

**Cómo funciona:**

El reenvío de eventos personalizado basado en ganchos web utiliza la extensión [!DNL Adobe Cloud Connector] (incluida de forma predeterminada) para realizar solicitudes HTTP arbitrarias a cualquier extremo. El implementador define elementos de datos para extraer y transformar valores del evento XDM entrante y, a continuación, configura una acción de regla con el tipo de acción &quot;Hacer llamada de recuperación&quot; del conector de nube. Esta acción permite un control total sobre el método HTTP, la dirección URL, los encabezados y el cuerpo de la solicitud.

El cuerpo de la solicitud se construye generalmente utilizando elementos de datos y código personalizado para dar formato a la carga útil según la especificación de API de destino. Este método admite cualquier extremo accesible mediante HTTP (API de REST, ganchos web, funciones de nube o servicios internos), lo que lo convierte en la opción más flexible.

La compensación es un mayor esfuerzo de implementación y mantenimiento continuo. El implementador debe comprender la API de destino, controlar la autenticación manualmente (por ejemplo, estableciendo encabezados de autorización, administrando la actualización de tokens) y mantener el formato de carga útil si la API de destino evoluciona.

**Consideraciones clave:**

- Requiere comprender la especificación de la API de destino (método HTTP, estructura de URL, formato de carga útil, autenticación)
- Las credenciales de autenticación se deben administrar manualmente en elementos de datos o secretos
- Puede ser necesario un código personalizado para la transformación de la carga útil (hashing, codificación y reestructuración)
- No hay actualizaciones automáticas cuando cambia la API de destino: se requiere mantenimiento manual
- La función Secretos de la recopilación de datos puede almacenar de forma segura claves y tokens de API

**Ventajas:**

- Admite cualquier extremo accesible mediante HTTP: sin dependencia de la extensión
- Control total sobre la carga útil de la solicitud, los encabezados y la autenticación
- Puede reenviar a servicios internos, API personalizadas o plataformas de nicho
- Habilita transformaciones de carga útil complejas mediante código personalizado
- Puede implementar la lógica de reintentos y la administración de errores en el código personalizado

**Limitaciones:**

- Mayor esfuerzo de implementación inicial
- Responsabilidad de mantenimiento continua para el formato y la autenticación de carga útil
- No hay gestión de errores prediseñada ni rotación de credenciales; debe implementarse manualmente
- Requiere experiencia del desarrollador en protocolos HTTP y detalles específicos de la API de destino

**Experience League:**

- [Extensión de conector de Adobe Cloud](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [Secretos del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)

### Opción C: híbrida (extensiones + webhooks personalizados)

**Ideal para:** organizaciones que reenvían eventos a varios destinos donde algunos tienen extensiones generadas previamente y otros requieren integración personalizada.

**Cómo funciona:**

El enfoque híbrido combina el reenvío basado en extensiones para destinos bien admitidos con acciones de gancho web personalizadas para destinos que carecen de extensiones. Una sola propiedad de reenvío de eventos contiene varias reglas: algunas utilizan acciones de extensión (por ejemplo, la extensión de API Conversiones [!DNL Meta] para el seguimiento de conversión de publicidad) y otras utilizan acciones de captura del conector de nube (por ejemplo, el reenvío a un extremo de lago de datos interno).

Este método maximiza la cobertura y minimiza el desarrollo personalizado innecesario. Cada regla funciona de forma independiente, por lo que las reglas basadas en extensiones se benefician del formato de carga útil generado previamente, mientras que las reglas personalizadas mantienen una flexibilidad total.

**Consideraciones clave:**

- La complejidad de la propiedad aumenta con el número de reglas y destinos
- Las pruebas y la depuración pueden requerir diferentes enfoques para las reglas basadas en extensiones frente a las personalizadas
- Los cambios de publicación afectan a todas las reglas de la propiedad: utilice bibliotecas y entornos para almacenar en zona intermedia los cambios de forma segura
- Considere la posibilidad de organizar reglas con convenciones de nomenclatura claras para distinguir las acciones basadas en extensiones de las personalizadas

**Ventajas:**

- Mejor cobertura en diversos tipos de destino
- Aprovecha las extensiones creadas previamente cuando están disponibles, lo que reduce el esfuerzo
- Mantiene la flexibilidad para los destinos personalizados
- La propiedad de reenvío de evento único administra toda la lógica de reenvío

**Limitaciones:**

- Mayor complejidad de la propiedad con varios tipos de reglas
- Modelo de mantenimiento mixto: algunas reglas se actualizan automáticamente mediante extensiones y otras requieren mantenimiento manual
- La depuración requiere estar familiarizada con las configuraciones de extensión y los patrones de llamada de recuperación personalizados

**Experience League:**

- [Resumen del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [Introducción al reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)

### Comparación de opciones

La siguiente tabla compara las tres opciones de implementación.

| Criterios | Opción A: Basada En Extensiones | Opción B: webhook personalizado | Opción C: híbrida |
| --- | --- | --- | --- |
| Mejor para | Destinos compatibles ([!DNL Meta], [!DNL Google], [!DNL AWS], etc.) | Extremos personalizados, plataformas de nicho, servicios internos | Varios destinos con compatibilidad mixta |
| Complejidad | Baja | Medium-High | Medio |
| Tiempo para la implementación | Días | Días-semanas | Varía según la combinación de destino |
| Flexibilidad | Limitado a las funcionalidades de extensión | Control total | Control total donde sea necesario |
| Mantenimiento | Baja (administrada por extensión) | Alto (mantenimiento manual) | Mixto |
| Requiere | Extensión disponible para destino | Documentación de API de destino | Ambos, según el destino |
| Se necesita código personalizado | Mínimo | Moderado-Significativo | Varía |

### Elija la opción correcta

Comience por realizar un inventario de los destinos y comprobar si existen extensiones de reenvío de eventos creadas previamente para cada uno.

1. **Si todos los destinos tienen extensiones** — Elija la opción A. Esto le proporciona la implementación más rápida con la carga de mantenimiento más baja. Las extensiones administran la autenticación, el formato de carga útil y la administración de versiones de API.

2. **Si ningún destino tiene extensiones o necesita control total de la carga útil** — Elija la opción B. Utilice la extensión de conector de nube para realizar solicitudes HTTP personalizadas a cualquier extremo. Esta también es la opción correcta cuando necesita aplicar transformaciones complejas, hash personalizado o enviar a servicios internos.

3. **Si tiene una combinación de destinos admitidos y no admitidos**, elija la opción C. Utilice extensiones para plataformas como [!DNL Meta], [!DNL Google] y [!DNL AWS], y ganchos web personalizados para todo lo demás. Este es el escenario de producción más común para organizaciones con diversas pilas de análisis y publicidad.

## Fases de implementación

Las siguientes fases describen el proceso de implementación de extremo a extremo para el reenvío de eventos.

### Fase 1: Configuración del flujo de datos

**Función de aplicación:** AEP: Configuración de secuencia de datos

**Lo que configurará:** Un conjunto de datos que recibe eventos de su implementación de Web SDK, Mobile SDK o API de servidor y los enruta a Edge Network, donde las reglas de reenvío de eventos pueden procesarlos. Si se agrega el reenvío de eventos a una implementación de recopilación de datos existente, habilitará el reenvío de eventos en la secuencia de datos existente.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: nueva secuencia de datos vs. secuencia de datos existente**
>
>¿Debe crear un nuevo flujo de datos para el reenvío de eventos o habilitar el reenvío de eventos en un flujo de datos existente?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Usar flujo de datos existente | Ya tiene Web SDK o API de servidor enviando eventos a través de una secuencia de datos | El escenario más común; el reenvío de eventos simplemente se habilita como servicio adicional en el conjunto de datos. No se necesitan cambios del lado del cliente. |
>| Crear nueva secuencia de datos | Se trata de una implementación sin formato sin recopilación de datos o necesita un flujo de datos independiente para tipos de eventos específicos | Requiere la configuración de SDK del lado del cliente para que apunte al nuevo ID de flujo de datos. Permite la configuración aislada. |

>[!NOTE]
>
>**Decisión: qué servicios de AEP se habilitarán junto con el reenvío de eventos**
>
>El conjunto de datos puede enrutar eventos a varios servicios de AEP simultáneamente. El reenvío de eventos es un servicio; otros (ingesta de datos de AEP, [!DNL Target], [!DNL Analytics]) se pueden ejecutar en paralelo.
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Solo reenvío de eventos | Solo es necesario reenviar eventos a destinos que no sean de Adobe y no necesita los datos de los conjuntos de datos de AEP | Minimice los costes de procesamiento de datos. Los eventos fluyen a través de Edge Network para reenviar reglas, pero no se incorporan al lago de datos de AEP. |
>| Reenvío de eventos + ingesta de AEP | Necesita los mismos eventos tanto en AEP (para perfiles, audiencias y recorridos) como en reenviados a sistemas externos | Más común para organizaciones que usan [!DNL RT-CDP] o [!DNL AJO] junto con análisis de terceros. La secuencia de datos envía eventos tanto a los conjuntos de datos de AEP como a las reglas de reenvío de eventos. |
>| Reenvío de eventos + varios servicios de Adobe | Necesita que los eventos se enruten simultáneamente a AEP, [!DNL Target], [!DNL Analytics] y destinos externos | Habilite todos los servicios necesarios en la secuencia de datos. Cada servicio recibe el evento de forma independiente. |

**Navegación de la interfaz de usuario:** [!DNL Experience Platform] > Recopilación de datos > Flujos de datos > Seleccionar o crear flujo de datos

**Detalles de configuración de clave:**

- La secuencia de datos debe tener habilitado el reenvío de eventos en su Configuración avanzada o configuración de servicio
- Vincule la propiedad de reenvío de eventos (creada en la fase 2) al conjunto de datos
- Confirme que el esquema XDM asignado al conjunto de datos coincide con la estructura de eventos que envía el mecanismo de recopilación

**Documentación de Experience League:**

- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Resumen de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)
- [Resumen del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)

### Fase 2: propiedad y extensiones del reenvío de eventos

**Función de aplicación:** AEP: Configuración de propiedad de reenvío de eventos

**Lo que configurará:** Una propiedad de reenvío de eventos en la IU de recopilación de datos, junto con las extensiones necesarias para los destinos. La propiedad de reenvío de eventos es el contenedor de todas las reglas, elementos de datos y extensiones que definen la lógica de reenvío del lado del servidor.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: propiedad única frente a propiedades múltiples**
>
>¿Debe utilizar una propiedad de reenvío de eventos para todos los destinos o propiedades independientes?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Propiedad única | La mayoría de las implementaciones; todas las reglas de reenvío comparten el mismo flujo de eventos | Más fácil de administrar, con un solo flujo de trabajo de publicación, todas las reglas se evalúan en relación con cada evento. Utilice condiciones de regla para filtrar qué eventos se dirigen a qué destinos. |
>| Varias propiedades | Necesita equipos diferentes para administrar diferentes integraciones de destino de forma independiente o tiene requisitos estrictos de aislamiento de entornos | Cada propiedad tiene su propio flujo de trabajo de publicación y se puede vincular a diferentes flujos de datos. Aumenta la sobrecarga de administración, pero mejora los límites de control de acceso. |

>[!NOTE]
>
>**Decisión: Qué extensiones instalar**
>
>Seleccione las extensiones en función de sus destinos y de la opción de implementación elegida (A, B o C desde arriba).
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Extensiones específicas del destino ([!DNL Meta], [!DNL Google], [!DNL AWS], etc.) | El destino tiene una extensión prediseñada y desea una configuración personalizada mínima (opción A o C) | Cada extensión requiere credenciales específicas del destino (tokens de API, ID de medición e ID de cuenta). Revise la documentación de extensión para ver los tipos de evento admitidos y los campos obligatorios. |
>| Solo extensión de conector de nube | Todos los destinos utilizarán solicitudes HTTP personalizadas (opción B) | La extensión Cloud Connector está instalada de forma predeterminada. Utilice la función Secretos para almacenar de forma segura las claves API y los tokens de autenticación. |
>| Conector específico de destino y conector de nube | Tiene una combinación de destinos admitidos y personalizados (Opción C) | Instale extensiones específicas para destinos bien admitidos y utilice Cloud Connector para el resto. |

**Navegación de la interfaz de usuario:** [!DNL Experience Platform] > Recopilación de datos > Reenvío de eventos > Crear propiedad (o seleccione una existente)

**Detalles de configuración de clave:**

- Asigne un nombre a la propiedad con una convención clara (por ejemplo, &quot;Reenvío de eventos: producción&quot; o &quot;EF: Analytics y Advertising&quot;)
- Instalar la extensión [!DNL Adobe Cloud Connector] (incluida de forma predeterminada para las acciones personalizadas de los ganchos web)
- Instalar extensiones específicas de destino y configurar sus credenciales
- Utilice la función Secretos (Recopilación de datos > Reenvío de eventos > Secretos) para almacenar de forma segura claves de API, tokens y credenciales
- Configure entornos (desarrollo, ensayo y producción) para flujos de trabajo de publicación seguros

**Documentación de Experience League:**

- [Introducción al reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)
- [Catálogo de extensiones de reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Secretos del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)
- [Extensión de conector de Adobe Cloud](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)

### Fase 3: Definición de regla de evento

**Función de aplicación:** AEP: Definición de regla de evento, AEP: Asignación de destino

**Lo que va a configurar:** Reglas que evalúan los datos de eventos entrantes, aplican condiciones para filtrar qué eventos deben reenviarse y definen acciones que envían los datos a los extremos de destino. Cada regla consta de condiciones (cuándo activar) y acciones (qué hacer). Los elementos de datos extraen y transforman valores de la carga útil de evento XDM para su uso en condiciones de regla y configuraciones de acción.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: estrategia de filtrado de eventos**
>
>¿Cómo se determina qué eventos se reenvían a cada destino?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Reenviar todos los eventos | El destino necesita un flujo de evento completo (por ejemplo, Data Warehouse para el almacenamiento de evento sin procesar) | Configuración más sencilla: no se necesitan condiciones. Volumen de datos alto en el destino. Considere los límites de coste y tasa de destino. |
>| Filtrar por tipo de evento | Los distintos destinos necesitan diferentes tipos de eventos (por ejemplo, compras en publicidad, vistas de página en análisis) | Use condiciones basadas en `arc.event.xdm.eventType` o campos XDM similares. Reduce los datos innecesarios en el destino. |
>| Filtrar por atributos de evento | Solo se deben reenviar eventos específicos que cumplan determinados criterios (por ejemplo, compras por encima de un umbral, eventos de rutas de página específicas) | Utilice valores de elementos de datos en condiciones de regla. Más complejo pero reduce el ruido en el destino. |

>[!NOTE]
>
>**Decisión: enfoque de transformación de datos**
>
>¿Cómo se deben transformar los datos de evento XDM para la carga útil de destino?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Asignación de campos XDM directa mediante elementos de datos | Los campos de destino se asignan claramente a campos XDM (lo común con el reenvío basado en extensiones) | Crear elementos de datos que hagan referencia a rutas XDM (por ejemplo, `arc.event.xdm.commerce.order.priceTotal`). Las extensiones suelen proporcionar una interfaz de usuario de asignación. |
>| Transformación de código personalizado | El destino requiere un formato de carga útil significativamente diferente de XDM, o los campos necesitan hash, concatenación o reestructuración | Utilice elementos de datos de código personalizado o código personalizado de nivel de acción para transformar la carga útil. Más flexible, pero más difícil de mantener. |
>| Combinación de elementos de datos y código personalizado | Algunos campos se asignan directamente, mientras que otros necesitan transformación | Utilice elementos de datos para asignaciones simples y bloques de código personalizado para transformaciones complejas. Equilibre la capacidad de mantenimiento con la flexibilidad. |

>[!NOTE]
>
>**Decisión: administración de PII en los datos reenviados**
>
>¿Cómo se debe gestionar la información de identificación personal antes de reenviarla?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Excluir los campos PII por completo | El destino no necesita PII y las políticas de gobernanza limitan el uso compartido | Configure reglas para omitir campos PII de la carga útil reenviada. El enfoque más sencillo para el cumplimiento de privacidad. |
>| Campos PII de hash antes del reenvío | El destino requiere identificadores hash (por ejemplo, [!DNL Meta] requiere un correo electrónico con hash SHA-256 para la API de conversiones) | Utilice elementos de datos de código personalizado para aplicar el hashing SHA-256. Algunas extensiones gestionan automáticamente el hash. |
>| PII a plazo con base contractual | El destino tiene un acuerdo de procesamiento de datos y la base legal para compartir PII | Asegúrese de que las etiquetas de uso de datos y las políticas de gobernanza (S3) permitan el uso compartido. Documente la base jurídica. |

**Navegación de la interfaz de usuario:** [!DNL Experience Platform] > Recopilación de datos > Reenvío de eventos > Seleccionar propiedad > Elementos de datos / Reglas

**Detalles de configuración de clave:**

- **Elementos de datos** hacen referencia al evento XDM entrante con el prefijo de ruta de acceso `arc.event.xdm.` (por ejemplo, `arc.event.xdm.web.webPageDetails.URL` para la dirección URL de la página)
- **Condiciones de regla** evalúan valores de elementos de datos para determinar si la regla debe activarse
- **Las acciones de regla** utilizan acciones específicas de extensión (para la opción A) o acciones &quot;Realizar llamada de recuperación&quot; del conector de nube (para la opción B) para enviar datos a los destinos
- Cada regla puede tener varias acciones, lo que permite reenviar un solo evento a varios destinos
- Utilice la ordenación de reglas para controlar la secuencia de evaluación cuando se activen varias reglas para el mismo evento
- Pruebe exhaustivamente las reglas en el entorno de desarrollo antes de publicarlas en producción

**Donde las opciones difieren:**

**Para La Opción A (Basada En Extensiones):**

Configure las acciones de regla con los tipos de acción creados previamente de la extensión de destino. Por ejemplo, la extensión de la API de conversiones [!DNL Meta] proporciona una acción &quot;Enviar evento&quot; en la que se asignan campos XDM a [!DNL Meta] parámetros de evento (event_name, event_time, user_data, custom_data). La extensión gestiona el formato de carga útil, el hashing y la comunicación API.

**Para Opción B (Webhook Personalizado):**

Configure las acciones de regla con la acción &quot;Hacer llamada de recuperación&quot; de la extensión de Cloud Connector. Especifique la dirección URL de destino, el método HTTP (normalmente POST), los encabezados de solicitud (incluida la autorización) y construya el cuerpo de la solicitud utilizando elementos de datos o código personalizado. Usted es responsable de hacer coincidir exactamente el formato de carga útil esperado de la API de destino.

**Para Opción C (Híbrida):**

Cree reglas independientes para cada destino. Las reglas basadas en extensiones utilizan los tipos de acción de la extensión; las reglas personalizadas utilizan llamadas de captura de Cloud Connector. Todas las reglas coexisten en la misma propiedad y se evalúan de forma independiente con cada evento entrante.

**Documentación de Experience League:**

- [Reglas de reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [Elementos de datos en el reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements)
- [Reglas en la recopilación de datos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules)
- [Extensión de conector de Adobe Cloud](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)

### Fase 4: Publicación y activación

**Función de aplicación:** AEP: Reenviando ejecución

**Lo que configurará:** Flujo de trabajo de publicación que promueve las reglas de reenvío de eventos desde el desarrollo hasta el ensayo y la producción. El reenvío de eventos utiliza el mismo modelo de publicación basado en bibliotecas que las etiquetas, con entornos y artefactos de compilación que controlan qué configuración está activa en Edge Network.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: publicación del rigor del flujo de trabajo**
>
>¿Cuán riguroso debe ser el proceso de publicación?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Directo a producción (Desarrollo > Producción) | Equipos pequeños, destinos de bajo riesgo o implementaciones de prueba de concepto | Implementación más rápida, pero con mayor riesgo de problemas de producción. Adecuado para pruebas iniciales con destinos no críticos. |
>| Progresión completa del entorno (Desarrollo > Ensayo > Producción) | Implementaciones de producción con destinos críticos (plataformas de publicidad, almacenes de datos) | Recomendado para todos los casos de uso de producción. El ensayo permite la validación con tráfico real antes de la implementación de producción. |

**Navegación de la interfaz de usuario:** [!DNL Experience Platform] > Recopilación de datos > Reenvío de eventos > Seleccionar propiedad > Flujo de publicación

**Detalles de configuración de clave:**

- Cree una biblioteca que contenga todas las reglas, elementos de datos y configuraciones de extensión que desee publicar
- Genere y pruebe primero en el entorno de desarrollo utilizando la herramienta de monitorización del reenvío de eventos para verificar que los eventos se reenvían correctamente
- Enviar a ensayo para la validación previa a la producción con tráfico en directo
- Publicar en producción solo después de confirmar el envío de eventos correcto en Ensayo
- Utilice las versiones de la biblioteca para rastrear cambios y habilitar la reversión si es necesario

**Documentación de Experience League:**

- [Resumen de publicación](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/overview)
- [Bibliotecas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/libraries)
- [Entornos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/environments)
- [Versiones](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/builds)

### Fase 5: Monitorización y validación

**Función de aplicación:** AEP: Monitoring

**Lo que configurará:** Supervisar los paneles y los procesos de validación para confirmar que los eventos se están reenviando correctamente, diagnosticar errores y mantener el estado operativo de la implementación del reenvío de eventos.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: profundidad de supervisión**
>
>¿Con qué profundidad se debe monitorizar el reenvío de eventos?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Solo panel de monitorización del reenvío de eventos | Supervisión básica de destinos no críticos o implementaciones iniciales | Proporciona información general sobre las tasas de éxito/error de reenvío y los códigos de respuesta de destino. Suficiente para la mayoría de las implementaciones. |
>| Monitorización del reenvío de eventos + validación del lado del destino | Destinos críticos en los que la integridad de los datos afecta directamente a los resultados empresariales (seguimiento de conversión de publicidad, integridad del Data Warehouse) | Hacer referencia a métricas de reenvío del lado de Adobe con confirmación de recepción del lado de destino. Detecta casos extremos en los que el destino acepta la solicitud pero no procesa los datos. |
>| Pila de observabilidad completa (Supervisión del reenvío de eventos + validación de destino + Alertas de AEP) | Implementaciones a escala empresarial con requisitos de SLA en la entrega de datos | Combine la monitorización del reenvío de eventos con las alertas de la plataforma AEP para obtener una vista completa. Configure notificaciones de alerta para reenviar los umbrales de error. |

**Navegación de la interfaz de usuario:** [!DNL Experience Platform] > Recopilación de datos > Reenvío de eventos > Seleccionar propiedad > Supervisión

**Detalles de configuración de clave:**

- La herramienta de monitorización del reenvío de eventos muestra el volumen de eventos, las tasas de éxito y los detalles de error por regla y por destino
- Monitorización de códigos de respuesta HTTP desde destinos: 2xx indica éxito, 4xx indica errores de cliente (probablemente problemas de carga útil o autenticación) y 5xx indica errores de destino.
- Utilice la extensión del explorador [!DNL Adobe Experience Platform Debugger] para inspeccionar los eventos que fluyen desde el cliente a través de Edge Network a las reglas de reenvío de eventos
- Valide de extremo a extremo comprobando que los eventos reenviados aparezcan en el sistema de destino (por ejemplo, compruebe [!DNL Google Analytics] informes en tiempo real, [!DNL Meta] administrador de eventos o tablas del almacén de datos)
- Configure las Alertas de AEP para los errores de origen y flujo de datos a fin de detectar problemas de subida que impidan que los eventos lleguen a las reglas de reenvío de eventos

**Documentación de Experience League:**

- [Supervisión del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring)
- [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/en/docs/experience-platform/debugger/home)
- [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)

## Consideraciones sobre la implementación

Esta sección cubre las barreras, los escollos comunes, las prácticas recomendadas y las decisiones de compensación que se deben tener en cuenta a lo largo de la implementación.

### Protecciones y límites

- El reenvío de eventos procesa los eventos en tiempo real en Edge Network; no hay modo por lotes ni cola de reintentos para los envíos fallidos de forma predeterminada
- Los límites de tasa de Edge Network se aplican al volumen total de evento procesado por flujo de datos: [protecciones de Edge Network](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/guardrails)
- Las reglas de reenvío de eventos se ejecutan en el servidor y no pueden acceder a los recursos del lado del cliente (DOM, cookies, localStorage)
- El código personalizado en las reglas de reenvío de eventos se ejecuta en un entorno limitado; no todas las API de JavaScript del explorador están disponibles
- La llamada de captura de Cloud Connector tiene límites de tiempo de espera: los destinos que responden lentamente pueden causar tiempos de espera
- El reenvío de eventos está sujeto al enrutamiento geográfico de Edge Network: los eventos se procesan en la ubicación de Edge más cercana
- El tamaño máximo de carga útil para las solicitudes reenviadas se rige por los límites de Edge Network

### Peligros comunes

- **Al reenviar todos los campos XDM sin filtrar:** Al enviar toda la carga útil de evento XDM a un destino que solo necesita unos pocos campos, se desperdicia ancho de banda, aumenta los costos de destino y puede compartir PII de forma involuntaria. Asigne siempre solo los campos obligatorios en las reglas de reenvío.

- **No proteger las credenciales con secretos:** El cifrado de claves API o tokens en elementos de datos o acciones de regla crea un riesgo de seguridad. Utilice siempre la función Secretos de recopilación de datos para almacenar las credenciales de forma segura y hacer referencia a ellas en las reglas.

- **Ignorando los límites de tasa de destino:** Los destinos de terceros a menudo tienen límites de tasa de API. Si el volumen de evento supera la capacidad de un destino, es posible que se pierdan eventos o que se restrinja el acceso a la API. Revise la documentación de destino para límites de velocidad e implemente filtros para reducir el volumen de evento si es necesario.

- **Publicar directamente en Producción sin ensayo:** Si se omite el entorno de ensayo, los errores solo se detectarán en Producción, lo que podría causar la pérdida de datos en destinos críticos. Valide siempre en Ensayo primero con tráfico en directo.

- **No se supervisan los códigos de respuesta HTTP:** Una regla que se activa sin errores no garantiza que el destino haya procesado correctamente los datos. Controle los códigos de respuesta de destino (disponibles en la herramienta de monitorización del reenvío de eventos) e investigue cualquier respuesta que no sea de 2xx.

- **Referencias de ruta XDM mal configuradas:** Los elementos de datos utilizan el prefijo `arc.event.xdm.` para hacer referencia a campos de evento entrantes. Una ruta incorrecta (por ejemplo, la falta de un nivel de anidación) produce silenciosamente valores nulos en lugar de generar errores. Valide los valores de los elementos de datos con Debugger.

### Prácticas recomendadas

- **Comience con un solo destino y expanda gradualmente** — Valide el reenvío de eventos de extremo a extremo con un destino antes de agregar reglas y destinos adicionales. Esto simplifica la depuración y genera confianza en la infraestructura.

- **Use convenciones de nomenclatura coherentes**: Asigne un nombre a los elementos de datos, las reglas y las bibliotecas con una convención clara que identifique el destino, el tipo de evento y el entorno (por ejemplo, &quot;Regla: Meta - Eventos de compra&quot;, &quot;DE: Total de pedido&quot;).

- **Implemente el filtrado a nivel de campo para la privacidad**: incluso si el destino afirma gestionar correctamente la PII, aplique el filtrado del lado del servidor para eliminar o hash los campos confidenciales antes de que abandonen Edge Network. Esta es la principal ventaja de control del reenvío de eventos sobre las etiquetas del lado del cliente.

- **Versión de sus configuraciones**: utilice el flujo de trabajo de publicación de la biblioteca para mantener instantáneas con versiones de su configuración de reenvío de eventos. Documente lo que contiene cada versión de la biblioteca con fines de auditoría y reversión.

- **Prueba con Platform Debugger**: la extensión [!DNL Adobe Experience Platform Debugger] proporciona visibilidad sobre el ciclo de vida del evento desde SDK del lado del cliente hasta el procesamiento de Edge Network. Utilícelo durante el desarrollo y la resolución de problemas.

- **Alinee las reglas de reenvío de eventos con el diseño de esquema XDM**: si el reenvío de eventos es un requisito conocido, diseñe el esquema XDM y la taxonomía de eventos para incluir los campos que necesitarán los destinos. La adaptación de los cambios de esquema después de la implementación es más perturbadora.

### Decisiones de compensación

>[!NOTE]
>
>**Compensación: simplicidad de la extensión vs. flexibilidad del gancho web**
>
>Las extensiones creadas previamente minimizan el esfuerzo de implementación y el mantenimiento, pero limitan las funciones compatibles con la extensión y los formatos de carga útil. Los webhooks personalizados proporcionan control total, pero requieren más desarrollo y mantenimiento continuo.
>
>- **Favoritos basados en extensiones (Opción A):** velocidad de salida al mercado, menor dependencia del desarrollador, administración automática de credenciales, menor mantenimiento
>- **Basado en webhook (Opción B) favorece:** Control de carga útil completo, compatibilidad con cualquier punto final HTTP, lógica de transformación personalizada, independencia de los ciclos de lanzamiento de extensión
>- **Recomendación:** Use extensiones cuando estén disponibles y sean suficientes. Vuelva a los webhooks personalizados solo cuando el destino no tenga extensión o cuando la extensión no admita las funciones específicas de la API que necesita. El enfoque híbrido (opción C) es la opción pragmática para la mayoría de las organizaciones.

>[!NOTE]
>
>**Compensación: Reenviar todos los eventos frente a filtrado selectivo**
>
>El reenvío de todos los eventos a un destino garantiza la integridad, pero aumenta el volumen de datos, los costes de destino y la exposición a la privacidad. El filtrado selectivo reduce el ruido, pero corre el riesgo de perder eventos que pueden ser valiosos.
>
>- **Reenviar todos los eventos a favor de:** Complejidad, simplicidad y corrección de errores en el futuro (los datos estarán disponibles si son necesarios más adelante)
>- **Favoritos de filtrado selectivo:** Eficiencia en los costos, menor riesgo de privacidad, datos de destino más limpios, cumplimiento de los principios de minimización de datos
>- **Recomendación:** De forma predeterminada, el filtrado selectivo se basa en el tipo de evento y la relevancia empresarial. Reenviar solo los eventos y campos que cada destino necesita. Esto se ajusta a los principios de minimización de datos (artículo 5 del RGPD) y reduce los costes operativos.

>[!NOTE]
>
>**Compensación: propiedad única frente a varias propiedades**
>
>Una sola propiedad de reenvío de eventos es más fácil de administrar, pero significa que todas las reglas comparten un flujo de trabajo de publicación. Varias propiedades proporcionan aislamiento, pero aumentan la sobrecarga de administración.
>
>- **Una sola propiedad favorece:** Simplicidad, publicación unificada, elementos de datos compartidos, depuración más sencilla
>- **Varias propiedades favorecen:** Control de acceso de nivel de equipo, cadencias de publicación independientes, aislamiento de errores de destino
>- **Recomendación:** Comience con una sola propiedad para la mayoría de las implementaciones. Solo se divide en varias propiedades si distintos equipos poseen integraciones de destino diferentes y necesitan ciclos de versión independientes, o si los requisitos regulatorios exigen un aislamiento estricto entre los flujos de datos.

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre los temas tratados en esta guía.

**Reenvío de eventos**

- [Resumen del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [Introducción al reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)
- [Supervisión del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring)
- [Secretos del reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)

**Extensiones de reenvío de eventos**

- [Catálogo de extensiones del lado del servidor](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Extensión de conector de Adobe Cloud](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [Extensión de API de conversiones de Meta](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/meta/overview)
- [Extensión de Google Cloud Platform](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [Extensión de AWS](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/aws/overview)
- [Extensión de Snowflake](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/snowflake/overview)
- [Extensión de conversiones mejoradas de Google Ads](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-ads-enhanced-conversions/overview)
- [Extensión de Mailchimp](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/mailchimp/overview)

**Recopilación de datos y Edge Network**

- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Resumen de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)
- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Información general sobre API de Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Información general sobre etiquetas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
