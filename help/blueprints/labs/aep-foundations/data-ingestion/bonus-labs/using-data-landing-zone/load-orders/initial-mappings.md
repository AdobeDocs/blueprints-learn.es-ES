---
title: Asignaciones iniciales
description: Asigne manualmente los campos _id y timestamp requeridos para un conjunto de datos de evento de experiencia usando expresiones de campo calculadas.
doc-type: article
solution: Experience Platform
exl-id: 4052d104-bf0c-4b2d-a298-8075279aeaf8
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# Asignaciones iniciales

Al igual que en el ejercicio anterior, debe verificar la asignación y, en algunos casos, modificarla.

## Verificar recomendaciones de ML

1. En el paso Asignación, las recomendaciones XML asignan automáticamente la mayoría de los atributos. Sin embargo, también verá varios errores. La pantalla inicial puede tener un aspecto similar al siguiente.

![La pantalla de asignación que muestra _id y marca de tiempo como campos no asignados no recomendados por ML](assets/initial-mappings-id-timestamp-unmapped-fields.png "_id, marca de tiempo son dos campos para los que el ML Recommendations no generará la asignación para")

>[!NOTE]
>
>Dado que asignamos un conjunto de datos de evento de experiencia por primera vez, tenga en cuenta que **\_id** y **timestamp** nunca se recomiendan ni se asignan de forma predeterminada para los eventos de experiencia. Debe asegurarse manualmente de que estén asignados correctamente.

## Asignar campos \_id, timestamp y order.\_devbc.acqSource

1. Para asignar **\_id,**, escriba la siguiente expresión de campo calculado y haga clic en Vista previa

   ```none
   concat(orderID, "-", lastOrderStatusUpdate)
   ```

   ![El campo calculado para la asignación de _id, listo para guardar](assets/initial-mappings-calculated-field-for-id-mapping.png "El campo calculado para la asignación de _id tendrá un aspecto similar a este. Haga clic en Guardar para guardar el campo calculado")

   ![Asignación del campo calculado al atributo _id](assets/initial-mappings-map-calculated-field-to-id.png "Asignación del campo calculado a _id")

1. Asegúrese de que el campo **timestamp** del esquema de destino esté asignado al siguiente campo calculado:

   ```none
   lastOrderStatusUpdate
   ```

   ![Vista previa de expresiones de campo calculadas para la asignación de marca de tiempo](assets/initial-mappings-expression-preview.png "Escriba la siguiente expresión y haga clic en Vista previa. TENGA EN CUENTA que este valor distingue entre mayúsculas y minúsculas y debe escribirse exactamente de esta manera")

   ![Asignando la expresión de campo calculado &quot;inStore&quot; a order._devbc.acqSource](assets/initial-mappings-map-instore-expression-to-acqsource.png)

1. Asigne la expresión de campo calculado **&quot;inStore&quot;** a **order.\_devbc.acqSource**

![Escribiendo la expresión de campo calculado &quot;inStore&quot; y haciendo clic en Vista previa](assets/initial-mappings-write-instore-expression-preview.png "Escriba la siguiente expresión y haga clic en Vista previa. TENGA EN CUENTA que este valor distingue entre mayúsculas y minúsculas y debe escribirse exactamente de esta manera")

## Gestión de asignaciones duplicadas

Si la pantalla de asignación se queja ahora de que hay una asignación duplicada como **orderStatus** asignada a **order.\_devbc.acqSource,** haga clic en el icono &quot;-&quot; para quitar la asignación.

>[!NOTE]
>
>Recuerde que no se pueden asignar varios campos de entrada al mismo campo de salida, ya que esto hace que la asignación sea ambigua. Sin embargo, un solo campo de entrada se puede asignar a varios campos de salida en el esquema XDM.

![Advertencia de asignación duplicada para orderStatus asignada a order._devbc.acqSource](assets/initial-mappings-duplicate-mapping-warning.png "Asignación duplicada para orderStatus asignada a order._devbc.acqSource")



![Advertencia de asignación duplicada para order._devbc.acqSource después de crear el campo calculado](assets/initial-mappings-duplicate-mapping-for-acqsource.png "Asignación duplicada para order._devbc.acqSource desde que creamos un campo calculado y ya lo hemos asignado. ")
