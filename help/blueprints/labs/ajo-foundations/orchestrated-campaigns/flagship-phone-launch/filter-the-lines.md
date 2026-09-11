---
title: Filtrar las líneas
description: Obtenga información sobre cómo filtrar las líneas de cliente excluidas con una actividad Dividir y utilizar Cambiar dimensión para alinear la dimensión objetivo de un flujo de trabajo con la configuración del canal SMS.
doc-type: article
solution: Experience Platform
exl-id: fb556a27-5c73-4457-ae98-dba43d445c7f
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '776'
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



## Añadir la actividad SMS

1. En el lienzo del flujo de trabajo, haga clic en el icono **+** después de la condición dividida que agregó y seleccione la **Actividad de SMS**

   ![Añada la actividad SMS después de la condición dividida](assets/filter-the-lines-add-sms-activity.png)

   ![Se agregó la actividad SMS al lienzo del flujo de trabajo](assets/filter-the-lines-sms-activity-on-canvas.png)



2. En el carril derecho, haga clic en el botón Editar SMS para iniciar la configuración del mensaje SMS

   ![Botón Editar SMS en el carril derecho](assets/filter-the-lines-edit-sms-button.png)



3. En la parte de navegación superior, haga clic en el elemento de menú Acciones y, a continuación, en la lista desplegable Configuración de SMS, seleccione el canal que creó anteriormente.

![Error de error en la configuración de SMS que no muestra resultados](assets/filter-the-lines-sms-configuration-no-results.png)

>[!CAUTION]
>
>¡Oh, no 🫨!  ¿Por qué no obtienes resultados?  ¿No has configurado ya tu canal SMS?  ¿Está roto el producto?
>
>¡QUÉ LOCO!!!!!!!!!



## Momento de asustar

La transición de la ramificación tiene actualmente una dimensión de segmentación de Línea del cliente (es decir, a qué tabla se relaciona el resultado actual en el Almacén relacional).  Sin embargo, lo que es único con las campañas orquestadas es que siempre se vuelve a unir al Perfil del cliente en tiempo real en el momento de la entrega, de modo que la información de entrega y seguimiento de los mensajes se atribuye a un perfil.  Esta unión se ha creado previamente para usted desde la tabla Cuenta de cliente.

La configuración de canal para SMS ya se había configurado previamente para usted y actualmente parece ser así...

![Configuración de detalles de ejecución configurada durante el laboratorio Configurar canal de SMS](assets/configure-sms-channel-final-execution-details.png)

**La forma de leer esto es la siguiente:**

- Enviar un mensaje por la dimensión de destino (es decir, Cuenta del cliente) sobre el número de registros relacionados encontrados en la dimensión secundaria (es decir, Línea del cliente)
- Ejecute cada envío SMS con el número de teléfono móvil encontrado en la dimensión secundaria (es decir, Línea del cliente)

Esta capacidad única para enviar muchos mensajes a un perfil es una de las funciones principales de las campañas orquestadas, lo que las diferencia de los Recorridos.


Entonces, ¿cómo hacer que esto funcione?  Agregar un cambio de dimensión 😀



## Añadir dimensión de cambio

1. Haga clic en el botón Atrás en la pantalla de edición de SMS

   ![Botón Atrás para salir de la pantalla de edición de SMS](assets/filter-the-lines-exit-sms-editor.png)



2. En el lienzo del flujo de trabajo, haga clic en el **+** **icono** entre las actividades Filter y SMS y seleccione **Cambiar dimensión**.

   ![Agregar una actividad Cambiar dimensión entre Filtro y SMS](assets/filter-the-lines-add-change-dimension.png)



3. En la parte derecha, actualice la dimensión de cambio con la siguiente información:
   - **Etiqueta:** `Convert Line to Account`
   - **Nueva dimensión de destino:**`dep-rel: Customer Account`

   ![Cambiar dimensión configurada para convertir línea en cuenta](assets/filter-the-lines-change-dimension-settings.png)



4. Haga clic en el botón **Guardar** en la parte superior derecha del lienzo para guardar el trabajo. Cuando termina, el flujo de trabajo tiene este aspecto...

![Lienzo de flujo de trabajo después de agregar el cambio de dimensión](assets/filter-the-lines-workflow-after-change-dimension.png)



## Configuración de mensaje SMS

Ahora que ha corregido el flujo de trabajo, vuelva a configurar el SMS.



1. Haz clic en la actividad SMS en el lienzo del flujo de trabajo y luego, en el carril izquierdo, haz clic en el botón **Editar SMS**

   ![Editar botón de SMS para reconfigurar el mensaje SMS](assets/filter-the-lines-edit-sms-button.png)

   >[!NOTE]
   >
   >Esta pantalla tarda unos minutos en cargarse.  Sé que es molesto, confía en mí que está siendo arreglado





2. En la barra de navegación superior, haga clic en el elemento de menú **Actions** y, a continuación, en la lista desplegable de configuración de SMS, seleccione el canal que creó anteriormente.

![Configuración de SMS que muestra correctamente el canal seleccionado](assets/filter-the-lines-sms-configuration-selected.png)

>[!TIP]
>
>Se siente bien, ¿no es así 😮‍💨?



## Resumen

Has pasado por esto y, con suerte, has aprendido dos cosas muy importantes:

1. La dimensión de segmentación de resultados finales debe coincidir con la configuración de canal que desee utilizar
1. La actividad Cambiar dimensión probablemente se convierta en su mejor amigo para garantizar que esto suceda
