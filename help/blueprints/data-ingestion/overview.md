---
title: Modelo de preparación e ingesta de datos
description: Este modelo muestra todos los métodos mediante los cuales se pueden introducir y preparar datos en Adobe Experience Platform.
solution: Experience Platform, Data Collection
kt: 7204
thumbnail: null
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Modelo de preparación e ingesta de datos

El modelo de preparación e inserción de datos incluye todos los métodos mediante los cuales se pueden preparar e incorporar datos en Adobe Experience Platform.

La preparación de datos incluye la asignación de datos de origen al esquema del Modelo de datos de experiencia (XDM). También incluye la realización de transformaciones en los datos, incluido el formato de fecha, la división/concatenación/conversiones de campos y la unión, combinación y reclaves de registros. La preparación de datos ayuda a unificar los datos de los clientes para proporcionar análisis agregados/filtrados, incluido el sistema de informes o la preparación de datos para el ensamblado de perfiles de clientes, la ciencia de datos o la activación.

## Arquitectura

<img src="assets/dataingest.svg" alt="Arquitectura de referencia para el modelo de preparación e ingesta de datos" style="border:1px solid #4a4a4a" />

## Métodos de inserción de datos

| Métodos de ingesta | Descripción |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SDK web/móvil | Latencia:<ul><li>Tiempo real: misma colección de páginas para la red perimetral</li><li>Incorporación de flujo a perfil ~1 minuto</li><li>Ingesta de flujo a lago de datos (micro lote ~15 minutos)</ul>Documentación: <ul><li>[SDK web](https://experienceleague.corp.adobe.com/docs/web-sdk.html)</li><li>[SDK móvil](https://experienceleague.adobe.com/docs/mobile.html?lang=en)</li></ul> |
| Fuentes de transmisión | Latencia:<ul><li>Tiempo real: misma colección de páginas para la red perimetral</li><li>Incorporación de flujo a perfil ~1 minuto</li><li>Ingesta de flujo a lago de datos (micro lote ~15 minutos)</li></ul>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors) |
| API de flujo continuo | Latencia:<ul><li>Tiempo real: misma colección de páginas para la red perimetral</li><li>Incorporación de flujo a perfil ~1 minuto</li><li>Ingesta de flujo a lago de datos (micro lote ~15 minutos)</li><li>7 GB/hora</li></ul>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en#what-can-you-do-with-streaming-ingestion%3F) |
| Herramientas ETL | Utilice las herramientas de ETL para modificar y transformar los datos empresariales antes de la ingesta en Experience Platform.<br><br>Latencia:<ul><li>El tiempo depende de la programación de herramientas de ETL externas, por lo que se aplican barreras de ingesta estándar en función del método utilizado para la ingesta.</li></ul> |
| Fuentes por lotes | Recuperación programada de orígenes<br>Latencia: ~ 200 GB/hora<br><br>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>[Tutorials de vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html) |
| API por lotes | Latencia:<ul><li>Ingesta por lotes al perfil en función del tamaño y las cargas de tráfico ~45 minutos</li><li>Ingesta por lotes al lago de datos en función del tamaño y las cargas de tráfico</li></ul>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en#batch) |
| Conectores de aplicaciones de Adobe | Ingesta automática de datos procedentes de aplicaciones de Adobe Experience Cloud<ul><li>Adobe Analytics: [Documentación](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en#connectors) y [Tutorial de vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html)</li><li>Audience Manager: [Documentación](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en#connectors) y [Tutorial de vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html)</li></ul> |


## Métodos de preparación de datos

| Métodos de preparación de datos | Descripción |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Data Science Workspace: Preparación de datos | Transformación impulsada por el modelo, transformación con secuencias de comandos.<br>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en) |
>[!NOTE]
>
>| Herramienta ETL externa ([!DNL Snaplogic], [!DNL Mulesoft], [!DNL Informatica], etc.) | Realice transformaciones complejas en las herramientas de ETL y utilice conectores o API de origen de Experience Platform estándar para introducir los datos resultantes.                                                                                                                                                               |

| Servicio de consulta - Preparación de datos                                  | Une, divide, combina, transforma, consulta y filtra datos en un nuevo conjunto de datos. Uso de Crear tabla como Seleccionar (CTAS) <br>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en#sql)                                                                       |
| Funciones XDM Mapper y Preparación de datos (Streaming y Batch)     | Asigne atributos de origen en formato CSV o JSON a atributos XDM durante la ingesta del Experience Platform.<br>Compute las funciones de los datos a medida que se incorporan; es decir, formato de datos, división, concatenación, etc.<br>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=en) |

## Publicaciones de blog relacionadas

* [Aprovechamiento de las plataformas de datos externas en el Journey Orchestration de Adobe Experience Platform](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page-------------------------------------)
* [Ingesta de gran rendimiento con Iceberg](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page-------------------------------------)
* [Trucos del servicio de consulta en Adobe Experience Platform (escritura de consultas y almacenamiento de conjuntos de datos derivados)](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page-------------------------------------)
* [Descubra el modelo de datos de experiencia de Adobe Experience Platform para comprender mejor el poder del perfil del cliente en tiempo real](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page-------------------------------------)
* [Un vistazo introductorio al análisis de datos exploratorios en Adobe Experience Platform](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page-------------------------------------)
* [Modelado de datos XDM para ciencia de datos a escala en Adobe Experience Platform](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page-------------------------------------)

