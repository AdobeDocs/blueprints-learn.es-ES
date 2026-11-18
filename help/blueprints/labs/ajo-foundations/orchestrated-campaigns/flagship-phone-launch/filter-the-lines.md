---
title: Filtrar las líneas
description: Obtenga información sobre cómo filtrar las líneas de cliente excluidas con una actividad Dividir y utilizar Cambiar dimensión para alinear la dimensión objetivo de un flujo de trabajo con la configuración del canal SMS.
doc-type: article
solution: Experience Platform
exl-id: fb556a27-5c73-4457-ae98-dba43d445c7f
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: f189618dc8bfa198b25d646faa3ca0e0f5af5916
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%
---

# Filtrar las líneas

## Objetivo

En el siguiente conjunto de pasos va a filtrar todas las líneas que realmente no pueden segmentarse con un mensaje SMS debido a su exclusión en el nivel de línea.  No puede confiar en el consentimiento del perfil aquí porque es un destinatario de nivel de línea.



## Configuración de la actividad División

1. Haga clic en el icono **+** en la transición inferior de la actividad Bifurcación y seleccione la actividad **Dividir** en la ventana emergente.

   ![Agregar una actividad de división a la bifurcación inferior](assets/filter-the-lines-add-split-activity.png)



2. En el carril derecho, actualice Label para que indique lo siguiente: `Filter out opt'd out lines`

   ![Dividir etiqueta de actividad establecida en Filtrar líneas de exclusión](assets/filter-the-lines-set-split-label.png)



3. En el carril derecho, expanda la sección del segmento predeterminado **Subconjunto** y haga clic en el botón **Crear filtro**

   ![Botón Crear filtro en la sección Subconjunto](assets/filter-the-lines-create-filter-button.png)



4. Añada una condición para asegurarse de eliminar todas las líneas de cliente que no están incluidas en los mensajes SMS y, a continuación, haga clic en **Confirmar**.

   ![La condición que elimina las líneas del cliente se excluyó de SMS](assets/filter-the-lines-sms-optin-condition.png)

   >[!NOTE]
   >
   >Debe averiguar cómo crear la condición, pero el resultado final coincide con la captura de pantalla anterior.  ¡Lo tienes!



5. Haga clic en el botón Save en la esquina superior derecha para guardar el trabajo.  El lienzo tiene el aspecto, así que ahora\...

![Lienzo de flujo de trabajo después de guardar la actividad dividida](assets/filter-the-lines-canvas-after-split-save.png)



## Añadir dimensión de cambio

1. En el lienzo del flujo de trabajo, haga clic en el icono **+** después de la condición de división que agregó y seleccione la actividad **Cambiar dimensión**

   ![Agregue la actividad Change dimension después de la condición dividida](assets/filter-the-lines-add-change-dimension-activity.png)

2. Actualice las propiedades de la dimensión de cambio como se describe a continuación y haga clic en **Confirmar**:
Etiqueta: `Convert Line to Account`
Nueva dimensión de destino: `dep-rel: Customer Account`

   ![Editar dimensión de destino](assets/filter-the-lines-add-edit-target-dimension.png)

   ![Editar dimensión de destino](assets/filter-the-lines-add-select-target-dimension.png)



## Añadir la actividad SMS

1. Haga clic en el icono **+** después de la dimensión Cambiar que agregó y seleccione la **Actividad del mensaje móvil**

   ![Agregue la actividad de mensajes de Mobile después de la condición dividida](assets/filter-the-lines-add-sms-activity.png)

   ![Se agregó la actividad SMS al lienzo del flujo de trabajo](assets/filter-the-lines-sms-activity-on-canvas.png)



2. En el carril derecho, primero cambie la opción de Target a **Un mensaje por dimensión secundaria** y luego haga clic en el botón **Editar mensaje móvil** para iniciar la configuración del mensaje SMS

   ![Botón Target y Edit Mobile message en el carril derecho](assets/filter-the-lines-edit-sms-button.png)



3. En la parte de navegación superior, haga clic en el elemento de menú Acciones y, a continuación, en la lista desplegable Configuración de mensajes de Mobile, seleccione el canal que ha creado anteriormente.

![Configuración de SMS que muestra correctamente el canal seleccionado](assets/filter-the-lines-sms-configuration-selected.png)




## Resumen

Ha filtrado todas las líneas a las que no se permitía dirigir con un mensaje SMS debido a la exclusión, ha cambiado la dimensión de línea a cuenta y ha añadido una actividad SMS para las que se permitía dirigir.
