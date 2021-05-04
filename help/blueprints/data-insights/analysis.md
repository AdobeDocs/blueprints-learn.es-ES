---
title: Análisis de datos y modelo de inteligencia
description: Este modelo muestra la habilidad de Adobe Experience Platform para realizar consultas y análisis de los datos presentes en el repositorio de datos.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039,a972ea56-d1c8-45da-9044-ed31222a2441
translation-type: tm+mt
source-git-commit: da21d1796eb9a2c9c0f087d82606874ca55bd4ea
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 36%

---

# Análisis de datos y modelo de inteligencia

El análisis de datos y la inteligencia comprenden la capacidad de Adobe Experience Platform para realizar consultas y análisis exploratorios de los datos que existen en el lago de datos.

El [!UICONTROL servicio de consulta] del Experience Platform permite realizar consultas SQL en los datos. [!UICONTROL El espacio de ] trabajo de la ciencia de datos permite que la exploración de datos, la ciencia de datos y las cargas de trabajo del aprendizaje automático se realicen en los datos.

Además, el Experience Platform permite que las conexiones con clientes SQL de terceros, interfaces y herramientas de Business Intelligence (BI) se conecten directamente a los datos en el Experience Platform, accedan a ellos y realicen consultas con ellos mediante el protocolo [!DNL PostgreSQL].

Algunas protecciones se aplican para el tiempo de espera de la consulta y para la cantidad de datos que se incluye en el resultado de la consulta, como se indica en los detalles del modelo.

## Casos de uso

* Consulta interactiva y adición de datos
* Acceso por fila y columna a los datos ingeridos para su análisis y validación
* Creación de paneles y visualización de datos a través de las herramientas de inteligencia empresarial

## Aplicaciones

* Adobe Experience Platform

## Arquitectura

<img src="assets/data_exploration.svg" alt="Arquitectura de referencia para el modelo de análisis de datos empresariales y creación de informes" style="border:1px solid #4a4a4a" />

## Guardas

Consulte la documentación del producto del servicio de consulta para obtener más información sobre las prácticas recomendadas y las protecciones.
[Guía del servicio de consultas](https://experienceleague.adobe.com/docs/experience-platform/query/best-practices/writing-queries.html?lang=en#best-practices)

## Pasos de implementación

1. Configurar conjuntos de datos y esquemas para la ingesta de datos en el repositorio.
1. Ingerir datos.
1. Confirme que los datos están disponibles para [!UICONTROL Query Service] y [!UICONTROL Data Science Workspace] para acceso sin procesar y consulta.
1. Conecte las herramientas del Business Intelligence y los clientes SQL a [!UICONTROL Query Service] para la visualización, consulta de datos y exploración.

## Documentación relacionada

* [Descripción del producto Adobe Experience Platform Intelligence](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Documentación de Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=es)
