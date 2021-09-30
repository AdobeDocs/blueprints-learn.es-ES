---
title: Modelo de análisis de datos e inteligencia
description: Este modelo muestra la habilidad de Adobe Experience Platform para realizar consultas y análisis de los datos presentes en el repositorio de datos.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: a972ea56-d1c8-45da-9044-ed31222a2441
source-git-commit: 5e93d3a5a09a3a20418ec7e563b93d22aef3ddc7
workflow-type: ht
source-wordcount: '337'
ht-degree: 100%

---

# Modelo de análisis de datos e inteligencia

El análisis de datos e inteligencia componen la habilidad de Adobe Experience Platform para realizar consultas y análisis de los datos presentes en el repositorio de datos.

[!UICONTROL Query Service] de Experience Platform permite realizar consultas SQL sobre los datos. [!UICONTROL Data Science Workspace] permite que las tareas de análisis y ciencia de datos, y también el aprendizaje automático, se realicen sobre los datos.

Además, Experience Platform puede conectarse con clientes SQL de terceros, interfaces y herramientas de inteligencia empresarial para comunicar y consultar directamente los datos contenidos en Experience Platform, así como acceder a ellos, utilizando el protocolo [!DNL PostgreSQL].

Se aplican ciertos guardas por extinción de tiempo de consulta y por la cantidad de datos que se incluyen en los resultados, tal como se describe en la información del modelo.

## Casos de uso

* Consulta interactiva y adición de datos
* Acceso por fila y columna a los datos ingeridos para su análisis y validación
* Creación de paneles y visualización de datos a través de las herramientas de inteligencia empresarial

## Aplicaciones

* Adobe Experience Platform

## Arquitectura

<img src="assets/data_exploration.svg" alt="Arquitectura de referencia para el modelo de análisis de datos empresariales y creación de informes" style="border:1px solid #4a4a4a" />

## Guardas

Consulte la documentación del producto Query Service para obtener más información sobre las prácticas recomendadas y los guardas.
[Guía de Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/best-practices/writing-queries.html?lang=es#best-practices)

## Pasos de implementación

1. [Crear esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) para la ingesta de datos.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) para la ingesta de datos.
1. [Ingesta de datos](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) a Experience Platform.
1. Confirmar que [[!UICONTROL Query Service]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=es) y [[!UICONTROL Data Science Workspace]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/load-data-in-jupyterlab-notebooks.html?lang=es) puedan acceder y consultar datos brutos.
1. [Conectar herramientas de inteligencia empresarial y clientes SQL a [!UICONTROL Query Service]](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.qsvc.dash) para la posterior visualización, consulta y análisis de datos.

## Documentación relacionada

* [Descripción del producto de inteligencia Adobe Experience Platform](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* Documentación de [[!UICONTROL Query Service]](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=es)
