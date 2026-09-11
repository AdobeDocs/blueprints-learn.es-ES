---
title: Crear estrategia de selección
description: Configure una estrategia de selección que vincule una colección de ofertas, reglas de elegibilidad y una fórmula de clasificación para la toma de decisiones.
doc-type: article
solution: Experience Platform
exl-id: 066ad087-6845-4ab5-9a6e-8dad1aa848f8
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# Crear estrategia de selección

## Objetivo

Hasta este punto, ha creado ofertas, ha definido la idoneidad de las ofertas con una regla de decisión, las ha reunido en una colección y ha creado una fórmula que las reordena dinámicamente en función de los atributos del perfil que solicita la personalización. Dado que solo utilizamos un conjunto de 4 ofertas para un único caso de uso, es tentador pensar que cada uno de estos elementos está relacionado, especialmente cuando los nombramos de manera similar. Sin embargo, es importante pensar de manera más abstracta cuando se considera una estrategia a largo plazo y un alcance de tamaño empresarial. Las ofertas se pueden ordenar en una o varias colecciones. Las fórmulas de clasificación se pueden aplicar a cualquier colección de ofertas. En realidad, la primera vez que conecta estos elementos es al crear una Estrategia de selección.

Imaginen que tuviéramos cientos de ofertas utilizadas en cuarenta colecciones y una docena de fórmulas de clasificación. ¿Cómo sabría un paquete de decisión qué fórmula de clasificación aplicar a qué colección de ofertas? La estrategia de selección establece esa conexión. Al agregar Decisioning a un canal, lo que está agregando son una (o varias) Estrategias de selección.

## Crear la estrategia de selección

1. Si es necesario, expanda **Decisioning** en el carril izquierdo y haga clic en **Configuración de estrategia**. Aterriza en la página &quot;Reglas de toma de decisiones&quot;, donde verá la regla de decisión &quot;Planes de nivel superior&quot; que creó anteriormente y que utilizó como requisitos de elegibilidad para los elementos de oferta de teléfono de nivel superior.
2. Haga clic en **Estrategias de selección** justo debajo del menú &#39;Métodos de clasificación&#39;. Sin estrategias de selección disponibles, haga clic en el botón azul **Crear estrategia de selección**.

   ![Página Estrategias de selección con el botón Crear estrategia de selección](assets/create-selection-strategy-create-button.png)

3. Asigne un nombre a la estrategia de selección **iPhone 17 Selection Strategy**
4. Se puede ver que una estrategia de selección requiere 3 cosas.
   - Una colección de ofertas
   - Requisitos de elegibilidad
   - Un método de clasificación

   Haga clic en el botón **Seleccionar colección**, marque la casilla junto a la única colección que tiene (**Colección iPhone 17**) y haga clic en **Guardar**.

5. Deje la lista desplegable &quot;Elegibilidad&quot; configurada como Todos los visitantes.

   >[!NOTE]
   >
   >La idoneidad se puede aplicar en el nivel de oferta, en el nivel de estrategia de selección o en el nivel de Recorrido/campaña a través de los criterios para introducir el Recorrido o la campaña. Todo depende del caso de uso que esté intentando realizar. Si hace clic en el menú desplegable **Elegibilidad**, verá las mismas opciones de Audiencia y Regla de decisión que vio en el nivel de oferta. En nuestro caso de uso, solo queríamos limitar ofertas específicas, por lo que tenía sentido cumplir los requisitos en el nivel de oferta.

6. Establezca el **método de clasificación** en **fórmula** y, a continuación, haga clic en el botón **Seleccionar fórmula**

   >[!NOTE]
   >
   >Es posible que haya visto las opciones &quot;Prioridad de oferta&quot; y &quot;Modelo de IA&quot; en la lista desplegable Método de clasificación. Si realmente solo desea devolver ofertas que utilicen únicamente su prioridad original, debe elegir la opción &quot;Prioridad de oferta&quot;.
   >
   >La opción Modelo de IA utiliza un modelo de IA que analiza las impresiones, los clics y las conversiones de las ofertas devueltas para determinar qué oferta mostrar al usuario. No los utilizaremos en este laboratorio, ya que se requieren umbrales mínimos de datos y dos semanas para entrenar a los modelos.

7. Marque la casilla junto a la única fórmula de clasificación que tiene (**Fórmula de clasificación iPhone 17**) y haga clic en **Guardar**. Cuando termine, la estrategia de selección tendrá este aspecto:

   ![Estrategia de selección completada con colección, elegibilidad y conjunto de fórmulas de clasificación](assets/create-selection-strategy-completed-configuration.png)

8. Una vez que la estrategia de selección sea correcta, haga clic en el botón azul **Crear**.

>[!TIP]
>
>Ahora verá su Estrategia de selección de iPhone 17 en el menú &quot;Estrategia de selección&quot;

>[!NOTE]
>
>La toma de decisiones permite realizar selecciones y pedidos de ofertas muy sencillos o complejos. Con un fin sencillo, podría tener una colección de ofertas con su prioridad predeterminada, una idoneidad establecida para todos los visitantes y el método de clasificación de &quot;Prioridad de la oferta&quot;, y todos los usuarios finales verían las ofertas en el orden de sus puntuaciones de prioridad originales. En el otro extremo, podría tener una gran colección con puntuaciones de prioridad inicial complejas, una fórmula de clasificación personalizada y reglas de elegibilidad por niveles tanto a nivel de oferta como de estrategia de selección. Lo que construiste en este laboratorio se encuentra en el medio y fue diseñado para demostrar las diferentes maneras en que se pueden configurar los paquetes de decisiones.

## Resumen

En esta página, ha creado una estrategia de selección que une los componentes principales creados hasta ahora: la colección de ofertas, las reglas de elegibilidad y la fórmula de clasificación.
