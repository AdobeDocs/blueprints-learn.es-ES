---
title: Modelo de ciencia de datos personalizada para el enriquecimiento de perfiles
description: Descubra cómo se pueden ingerir perspectivas basadas en la ciencia de datos en  [!DNL Experience Platform] para enriquecer el Perfil del cliente en tiempo real.
solution: Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
source-git-commit: 7f3bc307f74aa88a7a73f3e50cc48bd16f58b37f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 69%

---

# Ciencia de datos personalizada para modelo de enriquecimiento de perfil

El modelo de enriquecimiento de perfil de ciencia de datos personalizada ilustra cómo se pueden usar los datos para entrenar, implementar y puntuar modelos para proporcionar perspectivas de aprendizaje automático de [!DNL Experience Platform] y [!DNL Real-Time Customer Data Platform] desde la ciencia de datos y las herramientas de aprendizaje automático.

Las perspectivas modeladas se pueden ingerir en [!DNL Experience Platform] para enriquecer el perfil del cliente en tiempo real. Algunos ejemplos de datos recogidos por el aprendizaje informático incluyen calificación de valor de duración, afinidad de categoría y producto o tendencia a la conversión o cancelación.

## Casos de uso

* Extraiga información y descubra patrones de datos de clientes. A continuación, entrene y califique modelos a partir de estos datos.
* Enriquecer [!UICONTROL Real-Time Customer Profile] con datos y atributos según modelo para una personalización más granular y una optimización mejorada de recorrido.
* Entrenar y calificar modelos para determinar datos del cliente tales como el valor de tiempo de vida del cliente, la tendencia a la conversión o cancelación, la afinidad de contenido y producto, y la calificación de participación.

## Arquitectura

<img src="assets/data_science.svg" alt="Arquitectura de referencia del modelo de ciencia de datos personalizada para el enriquecimiento de perfiles" style="width:90%; border:1px solid #4a4a4a" />

## Guardas

* Para obtener protecciones detalladas y latencias de extremo a extremo sobre la ingesta de resultados de ciencia de datos en [!DNL Experience Platform] y el perfil del cliente en tiempo real, consulte las protecciones de ingesta de datos y el diagrama de latencia a los que se hace referencia en el [documento de protecciones de implementación](../experience-platform/deployment/guardrails.md).

## Pasos de implementación

1. [Crear esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=es) para la ingesta de datos.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) para la ingesta de datos.
1. [Ingresar datos](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) en [!DNL Experience Platform].

Para que los resultados del modelo se ingieran en Real-Time Customer Profile, debe hacer lo siguiente antes de introducir los datos:

1. [Configurar las identidades e identidad de áreas de nombres correctas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=es) en el esquema para asegurar que los datos ingestados se puedan combinar en un perfil unificado.
1. [Activar los esquemas y los conjuntos de datos del perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).

## Consideraciones sobre la implementación

* En la mayoría de los casos, los resultados del modelo deben ingerirse como atributos de perfil y no como eventos de experiencia. Los resultados del modelo pueden ser una simple cadena de atributos. Si se van a ingerir varios resultados de modelo, se recomienda utilizar un campo de tipo matriz o mapa.
* El conjunto de datos de instantáneas de perfil diarias, que es una exportación diaria de los datos unificados de atributos de perfil, se puede aprovechar para entrenar modelos con datos de atributos de perfil. Puede acceder a la documentación del conjunto de datos de instantáneas de perfil [aquí](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=es#profile-attribute-datasets).
* Para extraer datos de [!DNL Experience Platform] se pueden utilizar los siguientes métodos
   * SDK de acceso a datos
      * Los datos están en formato de archivo sin procesar
      * Los datos de evento de experiencia de perfil se mantienen en su estado sin procesar y no unificado.
   * Destinos RTCDP
      * Se pueden extraer atributos de perfil y suscripciones a segmentos.

## Documentación relacionada

* [Adobe [!DNL Experience Platform] Descripción del producto inteligente](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Adobe [!DNL Experience Platform] Servicio de consultas](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=es)

## Entradas relacionadas en el blog

* [IA para contenido y comercio: personalizar las interacciones con el cliente a través de la inteligencia de contenido](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [Introducción al análisis exploratorio de datos en el Adobe [!DNL Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [Atajar productos de Adobe Experience con el aprendizaje automático para conseguir una mejor experiencia del usuario](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Segmentation.AI: clúster de audiencias automatizado como servicio en el Adobe [!DNL Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)