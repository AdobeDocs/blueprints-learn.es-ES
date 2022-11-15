---
title: Modelo de acceso y exportación de datos
description: Este modelo proporciona información general sobre todos los métodos mediante los cuales se puede acceder y exportar datos desde Adobe Experience Platform y aplicaciones.
product: adobe experience platform
solution: Experience Platform, Journey Optimizer, Real-time Customer Data Platform, Tags
exl-id: 2ca51a29-2db2-468f-8688-fc8bc061b47b
source-git-commit: c0fe0e94e30351f593e32ea0e6809dd832f976ad
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 5%

---

# Modelo de acceso y exportación de datos

El modelo de acceso a datos y exportación describe todos los métodos posibles para acceder a los datos o exportarlos desde Adobe Experience Platform y aplicaciones.

El modelo se divide en dos categorías para el acceso a los datos desde el Experience Platform y las aplicaciones. En primer lugar, los enfoques para extraer datos de los Experience Platform y las aplicaciones; esto se consideraría un método de tipo push de salida de datos. En segundo lugar, los enfoques para el acceso a los datos de los Experience Platform y las aplicaciones; esto se consideraría un método de tipo pull para el acceso a los datos.

Enfoques de acceso a datos

* [API de acceso al perfil del cliente en tiempo real](#rtcp-profile-access-api)
* [API de acceso a datos](#data-access-api)
* [Servicio de consultas](#query-service)

Enfoques de exportación de datos

* [Etiquetas del lado del cliente](#client-side-tags-extensions)
* [Reenvío de eventos](#event-forwarding)
* [Destinos de Real-time Customer Data Platform](#RTCDP-destinations)
* [Acciones personalizadas de Journey Optimizer](#jo-custom-actions)

## Arquitectura de información general de acceso a datos y exportación

<img src="../experience-platform/assets/aep_data_flow.svg" alt="Arquitectura de referencia para el modelo de preparación e ingesta de datos" style="width:90%; border:1px solid #4a4a4a" />

## Enfoques para el acceso a los datos

### API de acceso al perfil del cliente en tiempo real {#rtcp-profile-access-api}

Los clientes pueden acceder a perfiles unificados únicos desde el almacén de perfiles del cliente en tiempo real, que incluye todas las identidades de perfil, las suscripciones a audiencias, los atributos y los eventos de experiencia mediante la API de acceso al perfil del cliente en tiempo real.

Consulte la [API de acceso al perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=en) documentación para obtener más información.

#### Casos de uso

* Busque un perfil único para agregar contexto a la interacción con el cliente del agente, como interacciones de soporte a través de chat y centro de llamadas, o una interacción de ventas en el punto de venta.
* Permite añadir contexto a una descripción de personalización realizada por un sistema externo, por ejemplo, un sistema de personalización web o un sistema de decisión de ofertas.

#### Consideraciones

* Perfil del cliente en tiempo real [guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) .
* Diseñado para la búsqueda de un solo perfil a la vez. No se utiliza para el acceso de perfiles en lote o la descarga de toda la población de perfiles para el uso de análisis o ciencia de datos.
* El tiempo de respuesta de búsqueda de perfiles se amplía hasta las protecciones de perfil. Requisitos de latencia baja en tiempo real: por ejemplo, para los requisitos de personalización de la misma página, debe utilizar el perfil de Edge desde a [Conexión de Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=es) o [Conexión de personalización personalizada](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en) para acceder a perfiles en tiempo real de en el navegador y en la personalización de la aplicación.

### API de acceso a datos {#data-access-api}

Los clientes de API de acceso a datos pueden acceder directamente a los archivos de conjuntos de datos sin procesar almacenados en el lago de datos del Experience Platform.

* Para obtener más información sobre el uso de la API de acceso a datos, consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=en).

#### Casos de uso

* Extraiga archivos de datos sin procesar y procesados de Experience Platform para almacenamiento y evaluación en entornos empresariales.

#### Consideraciones

* Como se accede a los datos de forma asíncrona y por lotes, el acceso a los datos se verá inherentemente latente, en comparación con los enfoques de salida de datos de flujo continuo, como la utilización de etiquetas, el reenvío de eventos o los destinos RTCDP.
* Los archivos de datos que se procesan en el Experience Platform se almacenan como colecciones de archivos en lotes y se comprimen y almacenan en formato de parqué. Como tal, al acceder y descargar los archivos a un entorno diferente, se debe acceder sistemáticamente a ellos por lote y archivo, en oposición a todo un conjunto de datos, y cualquier operación en los datos debe tener en cuenta los archivos comprimidos en formato de parqué.

### Servicio de consultas {#query-service}

El uso de experience platform Query Service permite a los clientes consultar conjuntos de datos dentro del Experience Platform y mantener los resultados de la consulta. Un cliente SQL se puede utilizar para consultar y mantener la respuesta de consulta en el destino de almacenamiento deseado que el cliente SQL puede soportar. La interfaz de usuario del servicio de consulta se puede utilizar para almacenar el resultado SQL en un conjunto de datos de destino en el Experience Platform o los resultados se pueden guardar en el equipo local.

* Para obtener más información sobre la conexión con clientes SQL para mantener los resultados SQL del servicio de consulta de Experience Platform, consulte lo siguiente [documentación](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=en).

#### Casos de uso

* Consulte los datos sin procesar de los conjuntos de datos del Experience Platform y mantenga los resultados de la consulta.
* Consulte el conjunto de datos de instantánea de perfil para extraer perspectivas sobre el perfil del cliente en tiempo real. [Documentación](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=en#profile-attribute-datasets).
* Almacene los resultados de la consulta en un conjunto de datos independiente para el acceso o en un conjunto de datos habilitado para perfil que luego se puede registrar a través de RTCDP y otras aplicaciones Experience Cloud que acceden al Perfil del cliente en tiempo real.

#### Consideraciones

* Como los datos se consultan de forma asíncrona por lotes, el acceso a los datos estará inherentemente latente en comparación con los enfoques de salida de datos de flujo continuo, como la utilización de etiquetas, el reenvío de eventos o los destinos RTCDP.
* Solo se pueden consultar los datos disponibles en el lago de datos del Experience Platform mediante el servicio de consulta. El almacén de perfiles de cliente en tiempo real, el gráfico de identidad y el Customer Journey Analytics no se pueden consultar directamente mediante el servicio de consulta. Solo cuando se exportan conjuntos de datos al lago de datos se pueden consultar estos conjuntos de datos, como en el ejemplo del conjunto de datos de instantánea de perfil.
* Tenga en cuenta que las protecciones para el número de resultados de la consulta y el tiempo de espera de la consulta se aplican tal como se describe en la sección [Protecciones de los servicios de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=en) documentación.

## Enfoques para la exportación de datos

### Extensiones de etiquetas del cliente {#client-side-tags-extensions}

Las extensiones se pueden implementar mediante la solución Etiquetas de Adobe. Una vez implementada la extensión, las solicitudes de datos se implementan directamente en un explorador o aplicación cliente y se puede invocar una solicitud para enviar datos y solicitudes al destino deseado.

Consulte la [Información general sobre etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en) documentación para obtener más información.

#### Casos de uso

* Recopile información de flujo sin procesar directamente desde entornos del lado del cliente mediante el etiquetado.

#### Consideraciones

* No hay acceso directo a ninguna información del lado del servidor, como el Perfil del cliente en tiempo real del Experience Platform y las suscripciones a la audiencia.
* La adición de etiquetas adicionales de recopilación de datos a la página puede aumentar los tiempos de carga de las páginas.
* Posibilidad de configurar reglas para que solo soliciten datos cuando se cumplan determinados criterios.
* Los datos se recopilan directamente del cliente, lo que limita los tipos de transformaciones y enriquecimiento que se pueden realizar antes de recopilar los datos.

### Reenvío de eventos {#event-forwarding}

Las solicitudes de recopilación de datos se recopilan directamente en la red perimetral de Adobe. Desde las solicitudes de red perimetral hasta los extremos externos RESTful se pueden configurar para reenviar estas solicitudes al destino externo.

Consulte lo siguiente [Reenvío de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en) documentación para obtener más información.

#### Casos de uso

* Recopile información de flujo sin procesar directamente desde entornos del lado del cliente a un extremo empresarial mediante el reenvío de eventos del lado del servidor de Adobe.

#### Consideraciones

* Para utilizar el reenvío de eventos, los datos deben enviarse a la red perimetral mediante WebSDK o MobileSDK.
* El método de reenvío de eventos reduce el tiempo y el peso de la carga de la página debido a que se agregan etiquetas adicionales a la página.
* Actualmente no se admite ningún enriquecimiento del perfil perimetral u otras fuentes de datos.
* Se admite un filtrado de datos limitado y transformaciones de asignación sencillas.

### Destinos de Real-time Customer Data Platform {#RTCDP-destinations}

Los datos de atributos de perfil y de pertenencia a audiencia se pueden activar en destinos empresariales y publicitarios. Esto significa que los datos registrados deben ingerirse en el Perfil del cliente en tiempo real del Experience Platform.

Consulte la [Destinos de Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en) documentación para obtener más información.

#### Casos de uso

* Active la información de atributos de perfil, incluida la pertenencia a audiencias, en almacenes de datos empresariales internos, herramientas de análisis, sistemas de correo electrónico o sistemas de asistencia.
* Active la pertenencia de la audiencia de perfil a un anunciante externo para dirigirse a y personalizar el contenido del perfil.

#### Consideraciones

* Se pueden activar los atributos de perfil y las suscripciones de audiencia. Actualmente, los eventos de experiencia sin procesar no se pueden activar como parte de destinos RTCDP.
* Las activaciones se producen en flujo continuo o por lotes según la naturaleza de la evaluación del segmento y la naturaleza del protocolo de ingesta que acepte el destino.

### Acciones personalizadas de Journey Optimizer {#jo-custom-actions}

Los clientes de Journey Optimizer pueden invocar una acción personalizada desde el lienzo de recorrido para enviar una carga útil o un mensaje a un extremo de API externo configurado. Se puede configurar una acción para cualquier servicio de cualquier proveedor al que se pueda llamar mediante una API de REST con una carga útil con formato JSON. Esta carga útil puede incluir información de evento, atributos de perfil y datos de evento anteriores, transformaciones y enriquecimientos configurados en el recorrido.

Consulte la [Acciones personalizadas de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=en) documentación para obtener más información.

#### Casos de uso

* Eventos de activación de Experience Platform y Journey Optimizer que incluyen información adicional del Perfil del cliente en tiempo real.
* Notificar a sistemas externos cuando un cliente ha alcanzado un punto específico de un recorrido.

#### Consideraciones

* Protección del rendimiento soportado por [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=es) y enriquecimientos admitidos por el [Perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) .
* Las acciones personalizadas se pueden llevar a cabo de una en una de forma continua para cada evento o perfil de un recorrido. No se pueden realizar operaciones masivas ni flujos masivos de datos en forma de archivos o solicitudes agregadas entre recorridos de clientes.
* Acceso de flujo continuo a los atributos de perfil del cliente en tiempo real y a los eventos de experiencia que se pueden incluir en la carga útil de activación.
* Los datos de evento se pueden filtrar y se pueden aplicar transformaciones de asignación sencillas antes de enviar eventos a destinos externos.
