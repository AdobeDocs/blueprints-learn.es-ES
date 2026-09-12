---
title: Crear una audiencia
description: Aprenda a utilizar la actividad Generar audiencia para dirigirse a los miembros del plan Básico desde un esquema relacional y comprobar los recuentos de filas resultantes.
doc-type: article
solution: Experience Platform
exl-id: 7576e64b-d99a-4864-b877-f4ae77e1d7bd
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Crear una audiencia

## Objetivo

En el siguiente conjunto de pasos, se creará una audiencia a partir del esquema relacional seleccionando la dimensión de segmentación correcta y configurando las condiciones adecuadas. También utilizará la opción de actualización para comprobar el número esperado de recuentos de filas.

## Generar público destinatario

1. Una vez que se represente la campaña, haga clic en **+** dentro del lienzo para abrir el menú de opciones y luego seleccione **Generar audiencia** de las **actividades de segmentación**

   ![Seleccionar audiencia de compilación de las actividades de segmentación](assets/build-an-audience-select-build-audience-activity.png)

2. La actividad **Generar audiencia** abre el panel de detalles a la derecha, haga clic en el icono Buscar para seleccionar **Dimensión de segmentación**.

   ![Seleccionar dimensión de segmentación](assets/build-an-audience-select-targeting-dimension.png)

3. Seleccione `dep-rel: Customer Account` de la lista y haga clic en **Confirmar**

   ![Seleccionar dep-rel: Esquema de cuenta de cliente](assets/build-an-audience-select-customer-account-schema.png)

4. Una vez configurada **Targeting dimension**, haga clic en Crear audiencia para iniciar el proceso de creación de la audiencia a partir del esquema relacional

   ![Haga clic en el botón Crear audiencia](assets/build-an-audience-create-audience-button.png)

5. Cuando se abra el panel Crear detalles de audiencia, haga clic en **Agregar condición**

   ![Haga clic en Agregar condición en el panel Crear audiencia](assets/build-an-audience-add-condition.png)

6. Desplácese hacia abajo y expanda `dep-rel: Plan Lookup` haciendo clic en **>** que está al lado

   ![Expandir fila profunda: búsqueda de plan](assets/build-an-audience-expand-plan-lookup.png)

7. Seleccione `dep-rel: Plan Name` y haga clic en **Confirmar**

   ![Seleccionar dep-rel: Nombre del plan](assets/build-an-audience-select-plan-name.png)

8. En el panel Personalizar condición, deje el operador como &quot;igual a&quot; y, para Valor, seleccione Básico en la lista desplegable.

   ![Condición personalizada con nombre de plan igual a Básico](assets/build-an-audience-plan-name-equals-basic.png)

   >[!NOTE]
   >
   >Observe que todos los valores distintos disponibles para la columna seleccionada se muestran en la lista desplegable, lo que facilita la creación de las condiciones personalizadas.



9. Con la condición personalizada configurada, haga clic en el icono Actualizar para calcular y ver el recuento. Existen dos ubicaciones para ayudar a calcular los resultados

   ![Haga clic en Actualizar para calcular los recuentos de filas esperados](assets/build-an-audience-refresh-row-counts.png)

   >[!NOTE]
   >
   >La operación Refresh evalúa la condición con respecto a los datos relacionales y muestra los resultados esperados. Esta operación suele tardar unos segundos y resulta extremadamente útil para ajustar los criterios y garantizar que cumple las expectativas.



10. Los recuentos (**38**) indican el número de filas del almacén relacional que coinciden con la condición especificada. Haga clic en **Confirmar** para salir del panel **Crear audiencia**

![Confirmar recuento de filas y salir del panel Crear audiencia](assets/build-an-audience-confirm-row-count.png)

>[!NOTE]
>
>Hay opciones en la sección Propiedades de la regla para obtener más detalles. Haz clic en **Ver resultados** para ver los resultados reales devueltos. Utilice la opción **Vista de código** para ver la consulta que se está ejecutando.

## Resumen

Ahora ha visto lo fácil que es utilizar la actividad Generar audiencia en la campaña eligiendo la dimensión de segmentación correcta del esquema relacional. A continuación, añadió una condición para restringir los criterios de creación de audiencias y utilizó la opción de actualización para comprobar el número esperado de filas.

Puede leer más [aquí](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/design-campaigns/build-audience) si está interesado.
