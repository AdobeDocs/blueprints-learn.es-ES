---
title: Programar flujo de datos
description: Configure una programación recurrente de flujo de datos de 15 minutos con relleno habilitado y comprenda cómo los tiempos de inicio UTC afectan a las ejecuciones.
doc-type: article
solution: Experience Platform
exl-id: 9865b1eb-0d98-4cae-a928-69ea897607ca
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# Programar flujo de datos

En el paso **Programación**:

1. Establezca la **Frecuencia** en Minuto.
1. Establezca el **intervalo** en 15, es decir, 15 minutos.
1. Activar la opción **Relleno**.

>[!NOTE]
>
>Observe que la **hora de inicio** está en UTC.
>
>La hora universal coordinada (UTC) es un estándar de tiempo global que se utiliza como punto de referencia para el cronograma en todo el mundo. Para un equipo distribuido globalmente, proporciona una referencia común para varias regiones y países, lo que facilita la coordinación de actividades y la programación de eventos en diferentes zonas horarias.
>
>En diferentes partes de la interfaz de usuario de AEP, la hora UTC se ve como la base de la programación horaria. La hora UTC está 1 hora por detrás de la hora de Londres. Si no está seguro de la hora UTC, simplemente google &quot;hora UTC ahora&quot;.

>[!NOTE]
>
>En la práctica, la opción **Relleno** realiza un relleno único de todos los archivos y las ejecuciones posteriores toman nuevos archivos.

![Programando la ejecución del flujo de datos con las opciones de frecuencia, intervalo y relleno establecidas](assets/schedule-dataflow-scheduling-dataflow-run.png "Programando la ejecución del flujo de datos")

Revise el flujo de datos y haga clic en **Finalizar.**

![Revisando la configuración final del flujo de datos antes de hacer clic en Finalizar](assets/schedule-dataflow-review-final-dataflow.png "Revisar el flujo de datos final")

>[!CAUTION]
>
>Si elige la opción **Ejecutar una vez** para el flujo de datos, no podrá editar esta programación ni actualizar el flujo de datos más adelante. Sin embargo, puede ejecutar el flujo de datos bajo demanda, es decir, ejecutar de nuevo si necesita introducir datos nuevos.

Después de hacer clic en **Finalizar**, volverá a la pantalla **Flujos de datos**. La creación del flujo de datos debería tardar unos minutos. Observe que Último estado de ejecución del flujo de datos indica **No hay ejecuciones**. La primera carrera debería comenzar en un par de minutos.

![Pantalla de flujos de datos que muestra el nuevo flujo de datos con el estado Sin ejecuciones](assets/schedule-dataflow-dataflows-screen-no-runs-status.png "Pantalla de fuentes de flujos de datos")

>[!NOTE]
>
>Debe actualizar la página continuamente para ver la actualización de estado, ya que el backend no inserta actualizaciones en la interfaz de usuario.

>[!NOTE]
>
>Si ha activado todas las alertas, recibirá una alerta en el explorador, en la esquina superior derecha del explorador, cuando el flujo comience a ejecutarse y se complete o falle correctamente
