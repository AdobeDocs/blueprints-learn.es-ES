---
hold: true
title: Ramificar el resultado
description: Aprenda a añadir una actividad de bifurcación a una campaña orquestada para ramificar un resultado y guardar una audiencia y enviar mensajes SMS.
doc-type: article
solution: Experience Platform
exl-id: 8f1d0839-e4ca-4b7c-bc97-4e271a457296
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Ramificar el resultado

## Objetivo

Este paso es sencillo, ya que lo único que desea hacer es agregar una actividad de bifurcación para poder duplicar el resultado y hacer dos cosas diferentes con él en pasos futuros:

1. Guarde la audiencia para que otros la utilicen con fines publicitarios o multicanal
1. Envíe mensajes SMS a las líneas individuales.



## Creación de la bifurcación

1. En el lienzo del flujo de trabajo, haga clic en el **+** **icono** después de crear la actividad de audiencia y seleccione la **Actividad de bifurcación**

![Agregue una actividad Fork después de la actividad Build Audience](assets/fork-the-result-add-fork-activity.png)



&#x200B;2. Actualice los nombres de cada transición en la ramificación haciendo clic en la transición y asignando después los nombres como se indica a continuación:
   - **Principales** —> `Save Audience`
   - **Inferior** —> `SMS`

![Se cambió el nombre de las transiciones de bifurcación a Guardar audiencia y SMS](assets/fork-the-result-rename-transitions.png)



Cuando termine, el lienzo debería verse así...

![Lienzo de flujo de trabajo después de agregar la actividad de bifurcación](assets/fork-the-result-final-canvas.png)

>[!NOTE]
>
>Una actividad de bifurcación básicamente solo duplica el resultado de la actividad anterior en dos ramas independientes



&#x200B;3. Haga clic en **Guardar** en la parte superior del lienzo del flujo de trabajo.

![Botón Guardar en la barra de herramientas del lienzo del flujo de trabajo](assets/fork-the-result-click-save.png)

>[!TIP]
>
>Fue bastante difícil, ¿no es así 😁?



## Resumen

Bueno, ha creado una bifurcación del resultado (es decir, duplicar el resultado) que le permite dictar claramente una rama para procesar una audiencia guardada, mientras que la otra se puede utilizar para el envío de SMS.

>[!NOTE]
>
>Debe utilizar Bifurcaciones, especialmente si planea guardar la audiencia, ya que la actividad Guardar audiencia no permite que las actividades la sigan.
