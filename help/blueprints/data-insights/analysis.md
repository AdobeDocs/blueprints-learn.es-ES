---
title: Análisis de datos y modelo de inteligencia
description: Este modelo muestra la capacidad de Adobe Experience Platform para realizar consultas y análisis exploratorios de los datos que existen en el lago de datos.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039,a972ea56-d1c8-45da-9044-ed31222a2441
translation-type: tm+mt
source-git-commit: 009a55715b832c3167e9a3413ccf89e0493227df
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Análisis de datos y modelo de inteligencia

El análisis de datos y la inteligencia comprenden la capacidad de Adobe Experience Platform para realizar consultas y análisis exploratorios de los datos que existen en el lago de datos.

El [!UICONTROL servicio de consulta] del Experience Platform permite realizar consultas SQL en los datos. [!UICONTROL El espacio de ] trabajo de la ciencia de datos permite que la exploración de datos, la ciencia de datos y las cargas de trabajo del aprendizaje automático se realicen en los datos.

Además, el Experience Platform permite que las conexiones con clientes SQL de terceros, interfaces y herramientas de Business Intelligence (BI) se conecten directamente a los datos en el Experience Platform, accedan a ellos y realicen consultas con ellos mediante el protocolo [!DNL PostgreSQL].

Algunas protecciones se aplican para el tiempo de espera de la consulta y para la cantidad de datos que se incluye en el resultado de la consulta, como se indica en los detalles del modelo.

## Casos de uso

* Consulta interactiva y agregación de datos
* Acceso de fila y columna a datos ingestados para exploración y validación
* Panorama y visualización de datos mediante herramientas de Business Intelligence

## Aplicaciones

* Adobe Experience Platform

## Arquitectura

<img src="assets/dataexplore.svg" alt="Arquitectura de referencia para el modelo de informes y exploración de datos empresariales" style="border:1px solid #4a4a4a" />

## Seguridad

* Límite de tiempo de 10 minutos para consultas interactivas
* Límite de 100 registros devuelto en la interfaz de usuario
* Límite de 50 000 registros devuelto mediante el conector SQL

## Pasos de la implementación

1. Configure conjuntos de datos y esquemas para la ingesta de datos en el lago de datos.
1. Ingesta de datos.
1. Confirme que los datos están disponibles para [!UICONTROL Query Service] y [!UICONTROL Data Science Workspace] para acceso sin procesar y consulta.
1. Conecte las herramientas del Business Intelligence y los clientes SQL a [!UICONTROL Query Service] para la visualización, consulta de datos y exploración.

## Documentación relacionada

* [Descripción del producto de Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL Documentación del ] servicio de consultas](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en)
