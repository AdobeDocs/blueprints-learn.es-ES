---
title: Campos calculados
description: Cree expresiones de campo calculadas para rellenar los valores de consentimiento de SMS que faltan y divida una fecha de nacimiento en campos de día, mes y año.
doc-type: article
solution: Experience Platform
exl-id: ea5d006b-11c5-439c-af01-bc00b919851f
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Campos calculados

## Información general

El campo sms\_optIn es un campo obligatorio en el esquema de cuenta del cliente. El problema es que el campo sms\_optIn de nuestra fuente de flujo continuo puede enviar valores *null*, por lo que se necesita un campo calculado para solucionarlo; de lo contrario, estos registros se omiten de la ingesta, lo que es una pérdida.

![El campo conents.marketing.sms.val tal como se muestra en el campo target schema](assets/calculated-fields-consents-marketing-sms-val-schema-field.png "conents.marketing.sms.val tal como se muestra en el esquema")



## Crear campo calculado

1. Cree un campo calculado haciendo clic en el icono **Nuevo tipo de campo** y, a continuación, seleccione **Agregar campo calculado**. Para todos los valores que faltan, se supone que no se ha dado el consentimiento y se marca como **&quot;n&quot;**. Tenga en cuenta que los campos calculados aparecen en la columna izquierda, ya que la transformación a través de un campo calculado es la entrada para esta nueva asignación.

   ![Nuevo menú de icono de tipo de campo con la opción Agregar campo calculado seleccionada](assets/calculated-fields-add-a-calculated-field.png "Agregar un campo calculado")



1. En el cuadro de diálogo Crear campo calculado agregue la siguiente expresión y haga clic en **Vista previa**

   ```none
   iif(sms_optIn == null or sms_optIn == "", 'n', sms_optIn)
   ```

   ![Cuadro de diálogo Crear campo calculado con la expresión sms_optIn y el resultado de la vista previa](assets/calculated-fields-sms-optin-calculated-field.png "campo calculado sms_optIn")



1. Debería ver una marca de verificación verde en la esquina superior derecha del cuadro negro que indica la validez de la expresión y la vista previa de datos solo debería mostrar **&quot;n&quot;** o **&quot;y&quot;** como valores. Si todo parece correcto, haga clic en **Guardar**.



## Asignar a destino

Se agrega un nuevo campo a la pantalla de asignación, pero con una ruta de campo de destino no asignada.

![Nuevo campo calculado sms_optin añadido a la pantalla de asignación con un campo de destino sin asignar](assets/calculated-fields-sms-optin-unmapped.png "sms_optin sin asignar")

1. Haga clic en **Asignar campo de destino** para el nuevo campo calculado que ha creado
1. En el panel derecho, ahora verá el panel de esquema de destinatario abierto. Escriba **sms** en el cuadro de búsqueda
1. Seleccione el campo **val**

   ![Panel de esquema de destino con el campo sms.val seleccionado para la asignación de campo calculado](assets/calculated-fields-map-calculated-field-to-target-xdm-field.png)



   La asignación final debería tener un aspecto similar al siguiente:

   ![Pantalla de asignación final con el campo calculado sms_optin asignado al esquema de destino](assets/calculated-fields-final-mapping-screen.png)



1. Valide la asignación para asegurarse de que tiene buen aspecto

![Validar botón que confirma que la asignación sms_optin es válida](assets/calculated-fields-validate-mappings.png)

>[!NOTE]
>
>Las filas sin un valor SMS válido se rechazan durante la ingesta. Si la ingesta parcial no está habilitada, el error de ingesta con esta fila falla en la ingesta del lote o archivo completo en nuestro caso. Con la ingesta parcial habilitada, las filas con campos obligatorios con valores que faltan se rechazan, pero se incorporan otras filas.



## Gestión de cumpleaños

Es necesario separar el día, el mes y el año de nacimiento en campos separados, de modo que algunos de ellos no puedan utilizarse en actividades posteriores. Debe crear dos campos calculados para resolver esto.

### Crear asignación para día y mes de nacimiento

1. Añada un nuevo campo calculado para capturar los perfiles de día y mes de nacimiento
1. Utilice el siguiente código para el campo calculado:

   >[!NOTE]
   >
   >En lugar de copiar el código anterior, intente comprender lo que está sucediendo ejecutando los fragmentos de código por separado para ver cómo se ha creado para crear campos calculados más complejos en una sola línea, ya que no se permite multilínea. Pruebe lo siguiente:
   >
   >1. `date(birth_Date,"M/d/yyyy")`
   >2. `date_part("day", date(birth_Date,"M/d/yyyy")).toString()`
   >3. `date_part("month", date(birth_Date,"M/d/yyyy")).toString()`
   >4. `concat(date_part("month", date(birth_Date,"M/d/yyyy")).toString(),`
   >   `"-", date_part("day", date(birth_Date,"M/d/yyyy")).toString())`



1. Haga clic en preview y debería ver el siguiente resultado. Si todo parece correcto, haga clic en **Guardar**

   ![Vista previa del resultado de la expresión de campo calculado de día y mes de nacimiento](assets/calculated-fields-birth-day-month-preview.png)



1. Asigne el campo calculado a **person.birthDayAndMonth**

1. Validación de la asignación



### Crear asignación para año de nacimiento

1. Cree un nuevo campo calculado para capturar el año de nacimiento del perfil con el código siguiente

   ```none
   date_part("yyyy",date(birth_Date,"M/d/yyyy"))
   ```

1. Asigne el campo calculado a la ubicación de destino de **person.birthYear**

1. Validación de la asignación

>[!NOTE]
>
>Observe que las fechas están en formato **MM/DD/AAAA**, pero los datos de **birth\_Date** de la muestra se presentan como dígitos simples o dobles para el día y el mes. Para que funcione la función **date**, debe especificar el formato de entrada de datos como **M/d/aaaa** para que pueda contabilizar de 1 a 2 dígitos para el mes y el día. Sin esta especificación de formato de entrada de fecha, la validación de estas asignaciones falla.
