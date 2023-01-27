---
title: Modelo de análisis de datos e inteligencia
description: Este modelo muestra la habilidad de Adobe Experience Platform para realizar consultas y análisis de los datos presentes en el repositorio de datos.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: a972ea56-d1c8-45da-9044-ed31222a2441
source-git-commit: b18d491fdefc57762932d1570401b5437bf97c76
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Modelo de análisis de datos e inteligencia

El análisis de datos e inteligencia componen la habilidad de Adobe Experience Platform para realizar consultas y análisis de los datos presentes en el repositorio de datos.

[!UICONTROL Query Service] de Experience Platform permite realizar consultas SQL sobre los datos.

Experience Platform puede conectarse con clientes SQL, interfaces y herramientas de inteligencia empresarial de terceros para acceder a los datos de Experience Platform y consultarlos directamente mediante el protocolo [!DNL PostgreSQL].

## Casos de uso

* Consulta interactiva y adición de datos
* Acceso por fila y columna a los datos ingeridos para su análisis y validación
* Creación de paneles y visualización de datos a través de las herramientas de inteligencia empresarial

Los casos de uso comunes adicionales para el servicio de consulta se describen aquí [Casos de uso de Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/use-cases/abandoned-browse.html?lang=es)

## Aplicaciones

* Adobe Experience Platform 

## Arquitectura

<img src="assets/data_exploration.svg" alt="Arquitectura de referencia para el modelo de análisis de datos empresariales y creación de informes" style="width:90%; border:1px solid #4a4a4a" />

## Guardas

Consulte la documentación del producto Query Service para obtener más información sobre las prácticas recomendadas y los guardas.
[Guía de Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=es)

## Pasos de implementación

1. [Crear esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=es) para la ingesta de datos.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) para la ingesta de datos.
1. [Ingesta de datos](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) a Experience Platform.
1. Confirme que los datos están disponibles para [[!UICONTROL Query Service]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=es).
1. [Conectar herramientas de inteligencia empresarial y clientes SQL a [!UICONTROL Query Service]](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=es) para la posterior visualización, consulta y análisis de datos.

## Documentación relacionada

* [Descripción del producto de inteligencia Adobe Experience Platform](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* Documentación de [[!UICONTROL Query Service]](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=es)
