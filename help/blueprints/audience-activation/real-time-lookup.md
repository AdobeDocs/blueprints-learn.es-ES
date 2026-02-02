---
title: Acceso al perfil de Edge en tiempo real para Personalization web y móvil
description: '[!UICONTROL Acceso al Perfil del cliente en tiempo real] en el perímetro para proporcionar contexto para la personalización móvil y web en tiempo real.'
solution: Real-Time Customer Data Platform, Data Collection
kt: 719
source-git-commit: 2fad3a8a9210d703130f251b0bd7cc4c0b7cbd32
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 6%

---

# Acceso al perfil de Edge en tiempo real para Personalization web y móvil

El modelo de acceso a perfiles de Edge en tiempo real para Personalization web y móvil muestra cómo las aplicaciones web y móviles pueden acceder al [!UICONTROL Perfil del cliente en tiempo real] de Adobe Experience Platform en el límite para una personalización de alto rendimiento y baja latencia.

Las aplicaciones pueden acceder a los atributos y audiencias de perfil en tiempo real en el perímetro de con una latencia de milisegundos. Se puede acceder en tiempo real a los atributos, las suscripciones a audiencias y las funciones impulsadas por modelos almacenados en el perfil como atributos para la personalización de la misma página y de la siguiente página en canales web y móviles.

Con esta capacidad, puede ofrecer experiencias altamente personalizadas en sus sitios web y aplicaciones móviles en función del Perfil del cliente en tiempo real, incluidas audiencias derivadas de comportamientos en tiempo real, atributos introducidos en el Perfil del cliente en tiempo real y perspectivas calculadas.

>[!NOTE]
>
>El acceso al perfil de Edge está diseñado específicamente para casos de uso de alto rendimiento y baja latencia, como la personalización de entrada web/móvil y la toma de decisiones de oferta en tiempo real. Para escenarios de menor rendimiento, como soporte asistido por el agente o interacciones de ventas, la API de búsqueda de perfiles de concentrador es más apropiada. Consulte el [Modelo de acceso a perfiles en tiempo real para escenarios de soporte y ventas](customer-activity.md) para obtener acceso a perfiles basados en concentradores.

## Aplicaciones

* Real-Time Customer Data Platform
* Recopilación de datos de Adobe Experience Platform (SDK web/SDK móvil)
* API de servidor de Edge Network

## Casos de uso

* Personalización en tiempo real en canales web y móviles para experiencias de cliente conocidas
* Personalización de la misma página y de la siguiente página basada en atributos y audiencias de perfil en tiempo real
* Personalización de contenido y ofertas basada en perfiles de clientes, incluidos datos de comportamiento en tiempo real, atributos y perspectivas calculadas
* Integración con motores de personalización, sistemas de administración de contenido y aplicaciones externas para la toma de decisiones en tiempo real
* Pruebas y optimización de contenido con contexto de perfil en tiempo real

## Prerrequisitos

Este modelo requiere el uso de uno de los siguientes métodos de recopilación de datos si desea que el perfil se actualice en tiempo real con datos de flujo continuo. Es posible obtener acceso en tiempo real al perfil de Edge sin tener que recopilar datos directamente en el perfil de Edge; los datos se pueden recopilar en el concentrador y proyectarse también en el perfil de Edge. Tenga en cuenta que se añadirá latencia para los datos recopilados en el concentrador y luego proyectados en el Edge.

* Use [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html) si desea recopilar datos de su sitio web.
* Use [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) si desea recopilar datos de su aplicación móvil.
* Use la [API de servidor de Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es) si no está usando Web SDK o Mobile SDK, o si está implementando una conexión de servidor a servidor más directa.

>[!IMPORTANT]
>
>Antes de implementar la personalización de Edge, lea la guía sobre cómo [activar datos de audiencia en destinos de personalización de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations). Esta guía le explica los pasos de configuración necesarios para los casos de uso de personalización de la misma página y de la siguiente página, en varios componentes de Experience Platform.

## Diagrama de arquitectura

<img src="assets/real-time-edge-lookup.svg" alt="Arquitectura de referencia para el acceso a perfiles de Edge para Personalization web y móvil" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## Guardas

* [Guardas de los datos de [!UICONTROL Real-Time Customer Profile]](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* [Protecciones de Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* Los perfiles de Edge tienen un tiempo de vida (TTL) de 14 días. Si un usuario no ha estado activo en el perímetro de durante 14 días, el perfil de Edge puede caducar y debe recuperarse del concentrador, lo que puede afectar a la personalización de la primera página.
* La personalización de Edge admite la evaluación de pertenencia a audiencias en tiempo real para audiencias que cumplen los criterios de segmentación de Edge. Las audiencias por lotes y de streaming desde el concentrador también están disponibles en el perímetro de con la configuración adecuada.

## Patrones de implementación

La personalización Edge se puede implementar usando el destino [Custom Personalization Connection](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization) en Real-time Customer Data Platform. Este destino admite varios métodos de recopilación de datos en función del caso de uso.

### Patrón 1: Personalización basada en la pertenencia a audiencias con Web SDK/Mobile SDK

* Utilice Adobe Experience Platform Web SDK o Mobile SDK con Edge Network para la personalización basada en la pertenencia a audiencias.
* Este método proporciona baja latencia y el mejor rendimiento para la personalización de Edge en función de los miembros de audiencias.
* La segmentación de Edge en tiempo real requiere la implementación de SDK web/móvil.
* La SDK web y la SDK móvil **por sí solas admiten la personalización basada únicamente en la pertenencia a audiencias**.
* [Consulte el modelo web y SDK móvil de Experience Platform](../experience-platform/deployment/websdk.md) para la implementación basada en SDK.
* Para la implementación de Mobile SDK, la extensión [Adobe Journey Optimizer - Decisioning](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/) debe estar instalada en Mobile SDK.

### Patrón 2: personalización basada en atributos con API de servidor de Edge Network (necesaria para atributos de perfil)

>[!IMPORTANT]
>
>**Requisitos de personalización basados en atributos:** Si desea realizar personalizaciones basadas en atributos de perfil (no solo en la pertenencia a audiencias), **debe** utilizar la [API de Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es) con integración autenticada del lado del servidor, independientemente de si también utiliza Web SDK o Mobile SDK para la recopilación de datos.

* Permite la integración con motores de personalización de terceros y personalización basada en CDN.
* La API del servidor de Edge Network es **necesaria** para recuperar de forma segura los atributos de perfil para la personalización.
* Puede recuperar atributos de perfil mediante la API de servidor de Edge Network añadiendo una integración del lado del servidor que utilice el mismo conjunto de datos que ya está utilizando para su implementación de SDK web o móvil.
* Todas las llamadas de API de servidor de Edge Network para atributos de perfil deben realizarse en un contexto autenticado para proteger los datos confidenciales.
* Este patrón permite la personalización basada en la pertenencia a audiencias y la personalización basada en atributos.
* Adecuado para casos de uso de personalización del lado del servidor, integraciones basadas en API y escenarios que requieren acceso a atributos de perfil.

## Pasos de implementación

1. [Crear esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=es) para la ingesta de datos.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) para la ingesta de datos.
1. [Configure las identidades y áreas de nombres de identidad correctas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es) en el esquema para garantizar que los datos ingeridos se puedan unir a un perfil unificado.
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).
1. [Ingesta de datos](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=es) a Experience Platform.
1. [Configure las políticas de combinación](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=es) para garantizar la vinculación de identidad y la combinación de perfiles correctas.
1. [Configurar una secuencia de datos](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=es) en la recopilación de datos de Experience Platform con la configuración de destino habilitada. El conjunto de datos determina en qué conjunto de datos de recopilación de datos se incluirán las audiencias en la respuesta a la página.
1. Implemente [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html) o [Mobile SDK](https://developer.adobe.com/client-sdks/home/) en las propiedades web y móviles para la recopilación de datos.
1. Configure la segmentación de Edge para audiencias que requieran evaluación en tiempo real. [Documentación de segmentación de Edge](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=es).
1. En el catálogo Destinos, configure [Conexión personalizada de Personalization](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization) destino:
1. [Activar audiencias en el destino de personalización de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations). Seleccione las audiencias que desea activar en el destino.
1. (Opcional para la personalización basada en atributos) Si necesita personalizar en función de los atributos de perfil además de la pertenencia a audiencias, implemente la [API de Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es) con integración autenticada del lado del servidor mediante la misma secuencia de datos. Esto es **obligatorio** para acceder a los atributos del perfil.
1. Implemente la lógica de personalización en la aplicación web/móvil para consumir los datos de audiencia y los atributos de perfil exportados:
   * Si usa etiquetas en Adobe Experience Platform, use la funcionalidad [enviar evento completado](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=es) para obtener acceso a la variable `event.destinations` con los datos exportados.
   * Si no usa etiquetas, use [respuestas de comandos](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html) para analizar la respuesta JSON de Adobe Experience Platform y recuperar los ID de audiencia y los atributos de perfil.

## Consideraciones sobre la implementación

### Consideraciones de identidad

* Cualquier identidad principal se puede utilizar para la personalización de Edge al utilizar Web SDK o Mobile SDK con Edge Network.
* Para la primera personalización de inicio de sesión con datos de clientes conocidos, la solicitud de personalización debe utilizar una identidad principal que coincida con la identidad de cliente conocida en Real-time Customer Data Platform. Si el ID principal se establece en ECID o en una identidad anónima que aún no se ha vinculado con el perfil del cliente conocido, la unión de identidad tardará un tiempo en realizarse, lo que puede afectar a la disponibilidad de los datos de perfil históricos para la personalización.
* Los perfiles de Edge deben inicializarse para poder utilizarse en la personalización. Los visitantes nuevos o los visitantes que regresan cuyo perfil de Edge ha caducado (TTL de 14 días) pueden experimentar una personalización inicial basada en datos de perfil limitados hasta que el perfil de Edge se rellene por completo.

### Personalización basada en atributos

>[!IMPORTANT]
>
>Los atributos de perfil pueden contener datos confidenciales. Para proteger estos datos, **debe** usar la [API de Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es) al configurar el destino de Personalization personalizado para la personalización basada en atributos. Todas las llamadas a la API del servidor de Edge Network deben realizarse en un contexto autenticado.

* Para la personalización basada en atributos mediante atributos de perfil, debe agregar una integración del lado del servidor con la API de servidor de Edge Network que utilice el mismo flujo de datos que utiliza para la implementación de SDK web o móvil.
* Debe configurar qué atributos de perfil se incluirán en la proyección de Edge mediante la configuración de destino de conexión de Personalization personalizada.
* **Solo Web SDK y Mobile SDK admiten la personalización basada en la pertenencia a audiencias**. La API del servidor de Edge Network es **necesaria** para recuperar de forma segura los atributos de perfil para la personalización.
* Si no implementa la API de servidor de Edge Network para el acceso a atributos, la personalización se basará únicamente en la pertenencia a audiencias.
* La respuesta de la API para Personalization personalizado con atributos incluye una sección `attributes` además de los segmentos de audiencia.

### Consideraciones de audiencia

* Las audiencias evaluadas mediante streaming o segmentación por lotes en el concentrador se proyectan al perímetro y se pueden utilizar para la personalización.
* Las audiencias que cumplen los criterios de segmentación de Edge se evalúan en tiempo real en el Edge para la personalización en la misma página.
* Configure las audiencias adecuadas para la evaluación de Edge en función de su uso en casos de uso de personalización en tiempo real.

## Documentación relacionada

### Configuraciones de destino

* [Conexión personalizada de Personalization](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization) - Guía de implementación principal
* [información general sobre destinos de Personalization](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/overview)
* [Activar audiencias en destinos de personalización Edge](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)
* [Buscar atributos de perfil en Edge en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-profile-lookup)

### Documentación del SDK

* [Documentación del SDK web de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html)
* [Documentación del SDK móvil de Experience Platform](https://developer.adobe.com/client-sdks/home/)
* [Documentación de la API de Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
* [Respuestas de comandos en Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html)

### Documentación de perfil y segmentación

* Documentación de [[!UICONTROL Real-Time Customer Profile]](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html)
* [Guardas de perfil](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)

### Tutoriales

* [Personalización de próxima visita con Real-Time CDP y Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html)
* [Configuración de secuencia de datos](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=es)
