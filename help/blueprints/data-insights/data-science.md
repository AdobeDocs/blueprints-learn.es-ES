---
title: Ciencia de datos personalizada para un modelo de enriquecimiento de perfiles
description: Este modelo muestra cómo Adobe Experience Platform Data Science Workspace puede utilizar los datos en Experience Platform para entrenar, implementar y puntuar modelos con el fin de proporcionar perspectivas de aprendizaje automático a partir de los datos.
solution: Experience Platform, Data Collection
kt: 7203
exl-id: f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
translation-type: tm+mt
source-git-commit: 3f27f27159d9fb07124f289164dd85941ec58a25
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Ciencia de datos personalizada para un modelo de enriquecimiento de perfiles

Este modelo muestra cómo el espacio de trabajo de ciencia de datos utiliza los datos de Adobe Experience Platform para entrenar, implementar y puntuar modelos con el fin de proporcionar perspectivas de aprendizaje automático. Estos modelos pueden generar directamente un conjunto de datos habilitado para Perfil del cliente en tiempo real. Algunos ejemplos de perspectivas de aprendizaje automático son el valor de duración, la afinidad de productos y categorías, la propensión a la conversión o la propensión a producir.

## Casos de uso

* Extraiga perspectivas y descubra patrones a partir de datos de clientes en Experience Platform. Capacite y puntee los modelos a partir de estos datos.
* Enriquezca el Perfil del cliente en tiempo real con perspectivas y atributos basados en modelos para una personalización más granular y una optimización del recorrido optimizada.
* Los modelos de formación y puntuación para determinar la perspectiva del cliente, como el valor de duración del cliente, la propensión a convertir o producir, las afinidades de producto y contenido y las puntuaciones de participación.

## Situaciones

| Situación | Descripción del escenario | Aplicaciones Experience Cloud |
|---|---|---|
| Ciencia de datos exploratorios | <ul><li>Descubra señales, integridad, exactitud de los datos</li><li>Descubra nuevas perspectivas mediante herramientas de ciencia de datos</li></ul> | <ul><li>Experience Platform Inteligencia</li></ul> |
| Enriquecimiento de perfiles con AI/ML<br> - por lotes | <ul><li>Descubra, cree, entrene, implemente, puntee y operacionalice modelos.</li><li>Predicción del modelo push para perfiles o lago de datos para activación por lotes.</li></ul> | <ul><li>Experience Platform Inteligencia</li></ul> |

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
1. Habilite el conjunto de datos de resultados del modelo para el perfil, si inserta los resultados del modelo en el Perfil del cliente en tiempo real.

## Documentación relacionada

* [Descripción del producto de Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Documentación de Data Science Workspace](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)
* [Tutoriales de Data Science Workspace](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/understanding-data-science-workspace.html)

## Publicaciones de blog relacionadas

* [Simplificación del ciclo de vida de la ciencia de datos con la experiencia de la plataforma Adobe](https://medium.com/adobetech/simplifying-the-data-science-lifecycle-with-adobe-platform-experience-8ea4f056d82f)
* [AI de contenido y comercio: Personalización de las interacciones con los clientes mediante la inteligencia de contenido](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [Comprensión más profunda de la pérdida mediante Data Science Workspace](https://medium.com/adobetech/gaining-a-deeper-understanding-of-churn-using-data-science-workspace-18a2190e0cf3)
* [Explicación De La Ciencia De Datos En Adobe Experience Platform](https://medium.com/adobetech/understanding-data-science-in-adobe-experience-platform-5bce5a17b42)
* [Un vistazo introductorio al análisis de datos exploratorios en Adobe Experience Platform](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [Recorte en los productos de Adobe Experience con aprendizaje automático y una experiencia de usuario elevada](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Modelado de datos XDM para ciencia de datos a escala en Adobe Experience Platform](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7)
* [Segmentation.AI: Agrupación automatizada de audiencias como servicio en Adobe Experience Platform](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)
* [Reimaginación de portátiles Jupyter para escala empresarial](https://medium.com/adobetech/reimagining-jupyter-notebooks-for-enterprise-scale-8bc6340d504a)
* [Acelerar perspectivas inteligentes con Adobe Experience Platform Data Science Workspace](https://medium.com/adobetech/accelerate-intelligent-insights-with-adobe-experience-platform-data-science-workspace-89538bacbbea)
* [Vista previa de la previsión de series temporales con Adobe Experience Platform](https://medium.com/adobetech/preview-of-time-series-forecasting-with-adobe-experience-platform-38a2fc778e89)
* [Recorte en los productos de Adobe Experience con aprendizaje automático y una experiencia de usuario elevada](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
