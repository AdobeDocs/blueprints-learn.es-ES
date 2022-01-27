---
title: Modelo de ciencia de datos personalizada para el enriquecimiento de perfiles
description: Este modelo muestra cómo Data Science Workspace de Adobe Experience Platform puede utilizar los datos existentes en Experience Platform para entrenar, implementar y calificar modelos, y así ofrecer información recopilada por aprendizaje automático de esos datos.
solution: Experience Platform,Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
source-git-commit: f323d2deee5547abd0ccc8247a23ac7a144b2f07
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Modelo de ciencia de datos personalizada para el enriquecimiento de perfiles

El modelo de ciencia de datos personalizada para el enriquecimiento de perfiles muestra cómo se pueden usar los datos de Adobe Experience Platform en [!UICONTROL Data Science Workspace] para entrenar, implementar y calificar modelos que proporcionen datos de aprendizaje automático. Estos modelos pueden generar directamente un conjunto de datos habilitado para [!UICONTROL Real-time Customer Profile], con el fin de enriquecer aún más los perfiles del cliente. Estos datos se pueden activar para la personalización. Algunos ejemplos de datos recogidos por el aprendizaje informático incluyen calificación de valor de duración, afinidad de categoría y producto o tendencia a la conversión o cancelación.

## Casos de uso

* Extraer datos y descubrir patrones con los datos del cliente de Experience Platform. Entrenar y calificar modelos según esos datos.
* Enriquecer [!UICONTROL Real-time Customer Profile] con datos y atributos según modelo para una personalización más granular y una optimización mejorada de recorrido.
* Entrenar y calificar modelos para determinar datos del cliente tales como el valor de tiempo de vida del cliente, la tendencia a la conversión o cancelación, la afinidad de contenido y producto, y la calificación de participación.

## Arquitectura

<img src="assets/data_science.svg" alt="Arquitectura de referencia del modelo de ciencia de datos personalizada para el enriquecimiento de perfiles" style="width:80%; border:1px solid #4a4a4a" />

## Pasos de implementación

1. [Crear esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) para la ingesta de datos.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) para la ingesta de datos.
1. [Ingesta de datos](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) a Experience Platform.
1. [Crear un cuaderno de notas de DSW](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/load-data-in-jupyterlab-notebooks.html?lang=es).
1. Elegir un idioma. Compatible con Python y PySpark.
1. [Crear un modelo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/recipe-builder-template.html?lang=es) en el cuaderno de notas.
1. [Entrenar el modelo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/schedule-training-scoring.html?lang=es).
1. [Calificar el modelo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/schedule-training-scoring.html?lang=en) para que genere predicciones con los datos de destino.
1. [Activar el conjunto de datos de resultados del modelo del perfil si envía los resultados del modelo a [!UICONTROL Real-time Customer Profile]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/dsw-profile-segmentation.html?lang=es).

## Documentación relacionada

* [Descripción del producto de inteligencia Adobe Experience Platform](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* Documentación de [[!UICONTROL Data Science Workspace]](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=es)
* Tutoriales de [[!UICONTROL Data Science Workspace]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/understanding-data-science-workspace.html?lang=es)

## Entradas relacionadas en el blog

* [[!DNL Simplifying the Data Science Lifecycle with Adobe Platform Experience]](https://medium.com/adobetech/simplifying-the-data-science-lifecycle-with-adobe-platform-experience-8ea4f056d82f)
* [[!DNL Content and Commerce AI: Personalizing Your Interactions with Customers Through Content Intelligence]](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [[!DNL Gaining a Deeper Understanding of Churn Using Data Science Workspace]](https://medium.com/adobetech/gaining-a-deeper-understanding-of-churn-using-data-science-workspace-18a2190e0cf3)
* [[!DNL Understanding Data Science In Adobe Experience Platform]](https://medium.com/adobetech/understanding-data-science-in-adobe-experience-platform-5bce5a17b42)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7)
* [[!DNL Segmentation.AI: Automated Audience-Clustering-as-a-Service in Adobe Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)
* [[!DNL Reimagining Jupyter Notebooks for Enterprise Scale]](https://medium.com/adobetech/reimagining-jupyter-notebooks-for-enterprise-scale-8bc6340d504a)
* [[!DNL Accelerate Intelligent Insights with Adobe Experience Platform Data Science Workspace]](https://medium.com/adobetech/accelerate-intelligent-insights-with-adobe-experience-platform-data-science-workspace-89538bacbbea)
* [[!DNL Una vista previa de la previsión de series temporales con Adobe Experience Platform]](https://medium.com/adobetech/preview-of-time-series-forecasting-with-adobe-experience-platform-38a2fc778e89)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
