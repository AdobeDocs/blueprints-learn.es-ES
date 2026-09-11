---
title: Depuración de errores
description: Utilice los diagnósticos de error de previsualización para investigar una ejecución de flujo de datos fallida y distinguir los errores de formato de INGESTA de las advertencias de conversión de MAPPER.
doc-type: article
solution: Experience Platform
exl-id: beee191b-a860-494c-873f-ab2e407ffbf5
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Depuración de errores

## Previsualizar diagnósticos de error

Después de unos minutos, observará que **Status** muestra un error. Profundice en los detalles del error para ver la causa.

1. Haga clic en la fecha **Inicio de ejecución del flujo de datos**
1. Haga clic en **Previsualizar diagnósticos de error** para ver los detalles específicos de cada fila que falla

![Estado de ejecución de flujo de datos que muestra un error](assets/debugging-errors-dataflow-run-failure.png "Error de ejecución de flujo de datos")

![Previsualizar vínculo de diagnósticos de error en la pantalla de detalles de ejecución del flujo de datos](assets/debugging-errors-preview-error-diagnostics-link.png "Previsualizar diagnóstico de error")



La pantalla que ahora ve muestra un conjunto de detalles sobre lo que significan los códigos de error con el mensaje de error completo y la fila que ha fallado.

![Pantalla de detalles de diagnóstico de errores que muestra códigos de error, mensajes y la fila con errores](assets/debugging-errors-error-diagnostics-detail-screen.png "Vista previa de diagnóstico de error")

>[!NOTE]
>
>Desplácese hacia la derecha para ver los datos de origen asociados con este código de error



## Explicación de los tipos de error

### Error de INGESTA-XXXX-XXX

Este error se produce porque se espera **person.birthDayAndMonth** con el formato de un mes de dos dígitos más un día de dos dígitos (es decir, el 27 de abril debería tener el formato 04-27)

```none
The value (9-27) does not conform to the specified
regex pattern: [0-1][0-9]-[0-9][0-9] in field: 
person.birthDayAndMonth of type: String
```

>[!CAUTION]
>
>Tenga en cuenta que person.birthDayAndMonth no es un campo obligatorio, pero el sistema trata la falta de conformidad con la expresión regular como un &quot;problema de corrupción de datos&quot; y es un error grave.



### Error de MAPPER-XXXX-XXX

Este error se debe a que el campo de origen de **createDate** tiene valores de cadena de `Created on 2022-04-22T19:34:17Z`. Este valor no se puede convertir automáticamente en una fecha debido al texto del principio: `Created on`. Se debe utilizar un campo calculado para limpiar los datos.

```none
Error transforming data for destination path 
_dep.account.createDate. Details: Unable to convert 
Created on 2023-09-24T10:19:58Z to schema type DATE_TIME
```

>[!NOTE]
>
>Este error no es grave, ya que solo provoca advertencias durante la asignación. La ejecución del flujo de datos no falla debido a esto, por lo que este laboratorio no corrige este error.
