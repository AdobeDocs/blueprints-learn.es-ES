---
title: Ciencia de datos personalizada para un modelo de enriquecimiento de perfiles
description: Este modelo muestra cómo Adobe Experience Platform Data Science Workspace puede utilizar los datos en Experience Platform para entrenar, implementar y puntuar modelos con el fin de proporcionar perspectivas de aprendizaje automático a partir de los datos.
solution: Experience Platform,Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
translation-type: tm+mt
source-git-commit: 2343151a1ed5374c299fb9317f6282c232d5d23b
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Ciencia de datos personalizada para un modelo de enriquecimiento de perfiles

La ciencia de datos personalizada para el modelo de enriquecimiento de perfiles ilustra cómo se pueden usar los datos de Adobe Experience Platform en [!UICONTROL Data Science Workspace] para entrenar, implementar y puntuar modelos que proporcionen perspectivas de aprendizaje automático. Estos modelos pueden generar directamente un conjunto de datos habilitado para [!UICONTROL Perfil del cliente en tiempo real] para enriquecer aún más los perfiles del cliente. Estas perspectivas se pueden activar para personalizar. Algunos ejemplos de perspectivas de aprendizaje automático son la puntuación de valor de duración, la afinidad de productos y categorías, la propensión a convertir o la propensión a producir.

## Casos de uso

* Extraiga perspectivas y descubra patrones a partir de datos de clientes en Experience Platform. Capacite y puntee los modelos a partir de estos datos.
* Enriquezca el [!UICONTROL Perfil del cliente en tiempo real] con perspectivas y atributos basados en modelos para una personalización más granular y recorridos optimizados.
* Los modelos de formación y puntuación para determinar la perspectiva del cliente, como el valor de duración del cliente, la propensión a convertir o producir, las afinidades de producto y contenido y las puntuaciones de participación.

## Arquitectura

<img src="assets/datascience.svg" alt="Arquitectura de referencia para el modelo de ciencia de datos personalizada para el enriquecimiento de perfiles" style="border:1px solid #4a4a4a" />

## Pasos de la implementación

1. Cree esquemas y conjuntos de datos.
1. Ingeste datos en el Experience Platform.
1. Cree un bloc de notas DSW.
1. Elija un idioma. Python y PySpark son compatibles.
1. Modelo de autor en el bloc de notas.
1. Capacite al modelo.
1. Puntee el modelo para generar predicciones con los datos de destino.
1. Habilite el conjunto de datos de resultados del modelo para el perfil, si inserta los resultados del modelo en el [!UICONTROL Perfil del cliente en tiempo real].

## Documentación relacionada

* [Descripción del producto de Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL Documentación del espacio de ] trabajo de ciencia de datos](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)
* [[!UICONTROL Tutoriales sobre ] espacio de trabajo de ciencia de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/understanding-data-science-workspace.html)

## Publicaciones de blog relacionadas

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
* [[!DNL A Preview of Time Series Forecasting with Adobe Experience Platform]](https://medium.com/adobetech/preview-of-time-series-forecasting-with-adobe-experience-platform-38a2fc778e89)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
