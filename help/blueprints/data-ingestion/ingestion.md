---
title: Modelo de preparación e ingesta de datos
description: Este modelo muestra todos los métodos por los cuales se puede realizar la ingesta y preparación de datos en Adobe Experience Platform.
solution: Experience Platform,Data Collection
kt: 7204
thumbnail: null
exl-id: 21f8a73e-6be7-448e-8cd3-ebee9fc848e1,5c3c94b6-c928-4d93-8b38-f8bd2aad2e68
translation-type: tm+mt
source-git-commit: 53914ce36ef0e48734c04818fbf8a5285fbb14ab
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 99%

---

# Modelo de preparación e ingesta de datos

El modelo de preparación e ingesta de datos engloba todos los métodos por los cuales se puede realizar la ingesta y preparación de datos en Adobe Experience Platform.

La preparación de datos incluye mapear los datos de origen en el esquema del Modelo de datos de experiencia (XDM). También incluye realizar transformaciones de datos, como dar formato a las fechas, unir/concatenar/convertir campos o unir/fusionar/reescribir registros. La preparación de datos ayuda a unificar la información del cliente, lo que ofrece un análisis agregado/filtrado, incluyendo la creación de informes o la preparación de datos para el ensamblaje/ciencia de datos/activación de perfiles de los clientes.

## Arquitectura

<img src="assets/data_ingestion.svg" alt="Arquitectura de referencia para el modelo de preparación e ingesta de datos" style="border:1px solid #4a4a4a" />

## Métodos de ingesta de datos

| Métodos de ingesta | Descripción |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SDK Web/Mobile | Latencia:<ul><li>Tiempo real, misma colección de páginas que Edge Network.</li><li>Ingesta de flujo al perfil ~1 minuto.</li><li>Ingesta de flujo al repositorio de datos (lote pequeño ~15 minutos).</ul>Documentación: <ul><li>[SDK Web](https://experienceleague.adobe.com/docs/web-sdk.html)</li><li>[SDK Mobile](https://experienceleague.adobe.com/docs/mobile.html?lang=es)</li></ul> |
| Orígenes de flujo | Latencia:<ul><li>Tiempo real, misma colección de páginas que Edge Network.</li><li>Ingesta de flujo al perfil ~1 minuto.</li><li>Ingesta de flujo al repositorio de datos (lote pequeño ~15 minutos).</li></ul>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=es#connectors) |
| API de flujo | Latencia:<ul><li>Tiempo real, misma colección de páginas que Edge Network.</li><li>Ingesta de flujo al perfil ~1 minuto.</li><li>Ingesta de flujo al repositorio de datos (lote pequeño ~15 minutos).</li><li>7 GB/hora</li></ul>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=es#what-can-you-do-with-streaming-ingestion%3F) |
| Herramientas ETL | Utiliza herramientas ETL para modificar y transformar datos empresariales antes de su ingesta en Experience Platform.<br><br>Latencia:<ul><li>El tiempo depende de la programación de la herramienta ETL externa. A continuación, se aplican guardas estándar de ingesta según el método de ingesta utilizado.</li></ul> |
| Orígenes por lote | Extracción programada desde origen<br>Latencia: ~ 200 GB/hora.<br><br>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>[Tutoriales en vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html?lang=es) |
| API por lote | Latencia:<ul><li>Ingesta por lotes a perfiles condicionados por tamaño y carga de tráfico ~45 minutos.</li><li>Ingesta por lotes a repositorios de datos condicionados por tamaño y carga de tráfico.</li></ul>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=es#batch) |
| Conectores de aplicaciones Adobe | Realizan la ingesta de datos procedentes de las aplicaciones de Adobe Experience Cloud automáticamente.<ul><li>Adobe Analytics: [documentación](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=es#connectors) y [tutorial en vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=es)</li><li>Audience Manager: [documentación](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=es#connectors) y [tutorial en vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html?lang=es)</li></ul> |


## Métodos de preparación de datos

| Métodos de preparación de datos | Descripción |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!UICONTROL Data Science Workspace]: preparación de datos | Transformación por modelo, transformación por script.<br>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=es) |
| Herramienta ETL externa ([!DNL Snaplogic], [!DNL Mulesoft], [!DNL Informatica], etc.) | Realizar transformaciones complejas en herramientas ETL y utilizar las API o los conectores de origen estándar de [!UICONTROL Flow Service] de Experience Platform para la ingesta de datos resultantes. |
| [!UICONTROL Query Service]: preparación de datos | Une, divide, fusiona, transforma, consulta y filtra datos en un nuevo conjunto de datos. <br>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=es#sql) sobre el uso de Create Table as Select (CTAS) |
| Funciones del mapeador XDM y preparación de datos (flujo y lotes) | Mapear atributos de origen en formato CSV o JSON en atributos XDM durante la ingesta de Experience Platform.<br>Computa funciones de datos mientras se realiza la ingesta; esto es, les da formato, los divide, los concatena, etc.<br>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=es) |

## Entradas relacionadas en el blog

* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page-------------------------------------)
* [[!DNL High Throughput Ingestion with Iceberg]](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page-------------------------------------)
* [[!DNL Query Service Tricks in Adobe Experience Platform (Writing Queries and Storing Derived Datasets)]](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page-------------------------------------)
* [[!DNL Digging into Adobe Experience Platform’s Experience Data Model to More Fully Understand the Power of Real-time Customer Profile]](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page-------------------------------------)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page-------------------------------------)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page-------------------------------------)
