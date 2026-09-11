---
title: Examinar esquemas
description: Aprenda a examinar los esquemas relacionales y ver los diagramas de relación de entidades en Adobe Experience Platform para comprender las relaciones de esquema utilizadas en las campañas.
doc-type: article
solution: Experience Platform
exl-id: ac0e6743-4a83-4a8b-9bc6-f012b636312e
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Examinar esquemas

## Objetivo

En el siguiente conjunto de pasos, se mostrará la interfaz de usuario para ver los esquemas y sus relaciones.  Esto es importante para familiarizarse con los esquemas y relaciones disponibles al crear la campaña.

## Ver esquemas

El modelo de datos relacional Connection 5G ya se ha creado para usted. Para ver los esquemas usted mismo, vaya a la página **Esquemas -> Examinar** en la interfaz de usuario.

En el cuadro de búsqueda, escriba `dep-rel` para ver todos los esquemas.

![Resultados de búsqueda que muestran todos los esquemas relacionales profundos](assets/browse-schemas-search-results.png)

>[!NOTE]
>
>Observe que el tipo de todos los esquemas es *Relacional*



## Ver diagrama de relación

Con los esquemas XDM relacionales puede ver fácilmente el diagrama de relación de entidades (ERD) seleccionando cualquier esquema y haciendo clic en el botón Ver diagrama de relación.

Haga lo siguiente:

1. Haga clic en la ficha **Relaciones** y, a continuación, haga clic en el botón **Ver diagrama de relaciones**

   ![Ficha Relaciones con el botón Ver diagrama de relaciones](assets/browse-schemas-relationships-tab.png)



2. Haga clic en **Seleccionar esquemas**
3. En la ventana emergente, seleccione `dep-rel: Customer Account` y haga clic en **Confirmar**

   ![Seleccionar esquema emergente con dep-rel: cuenta de cliente elegida](assets/browse-schemas-select-schema-popup.png)



4. En el ERD, haga clic en **3 puntos** y seleccione **Mostrar entidades relacionadas**

   ![Mostrar la opción de entidades relacionadas en el menú contextual de ERD](assets/browse-schemas-show-related-entities.png)



5. Vea el ERD con todas las tablas directamente relacionadas con dep-rel: Cuenta del cliente. Opcionalmente, puede descargar el ERD como archivo PNG.

![Diagrama de relación de entidad que muestra tablas relacionadas con la cuenta de cliente](assets/browse-schemas-erd-diagram.png)

>[!TIP]
>
>Bastante guay eh?!

## Resumen

Ahora ha visto lo fácil que es navegar por la IU de Esquema y relaciones.  Puede seleccionar esquemas específicos y navegar para ver las relaciones que le ayudarán a comprender y utilizar los datos en la orquestación de campañas.

Puede leer más [aquí](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/data-management/get-started-schemas) si está interesado.
