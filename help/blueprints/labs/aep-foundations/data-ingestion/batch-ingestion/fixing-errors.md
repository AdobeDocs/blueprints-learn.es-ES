---
title: Corrección de errores
description: Corrija una expresión de campo calculado para un error de formato de fecha y, a continuación, confirme el éxito mediante las métricas de monitorización de fuentes, identidades y perfiles.
doc-type: article
solution: Experience Platform
exl-id: 7a3d0c15-4d58-497e-bfa5-9421d5d2eea7
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Corrección de errores

## Corregir el día y el mes de nacimiento

1. Haga clic en el icono de flecha al lado del campo calculado que rellena el campo XDM **person.birthDayAndMonth**

   ![Editor de expresiones de campo calculado para la corrección birthDayAndMonth](assets/fixing-errors-update-the-calculated-expression.png)

1. Actualice la expresión utilizando el siguiente código de campo calculado y haga clic en **Vista previa**

   ```none
   concat(date_part("mm", date(birth_Date, "M/d/yyyy")).toString(),"-", date_part("dd", date(birth_Date, "M/d/yyyy")).toString())
   ```

   >[!NOTE]
   >
   >Los datos deben aparecer como un mes de 2 dígitos y un día de 2 dígitos (es decir, el 27 de abril se muestra como 04-27). Los parámetros `mm` y `dd` agregan relleno 0.

1. Si todo parece correcto **Guardar** el campo calculado

1. Luego haga clic en **Finalizar** para ejecutar la ingesta del flujo de datos.



## Validar ingesta

Después de unos minutos, la ejecución del flujo de datos debería ejecutarse y debería verse con éxito.

![Estado de ejecución del flujo de datos que muestra una ingesta de cuenta de cliente correcta](assets/fixing-errors-successful-customer-account-ingestion.png "Ingesta de cuenta de cliente correcta")



## Pantalla de monitorización

1. Vaya a la pantalla de monitorización haciendo clic en el carril izquierdo del icono **Monitorización** en la sección **Administración de datos**.
1. Haz clic en la tarjeta **Fuentes** y luego desplázate por la barra inferior para ver los detalles de la ejecución del flujo de datos. Tenga en cuenta lo siguiente:
   - **Registros recibidos:** 20 registros se recibieron del origen para su procesamiento
   - **Registros ingeridos:** 20 registros se ingerieron en el lago de datos después de la asignación y el procesamiento de datos.
   - **Error en los registros:** Debería ver un 0 aquí. Representa el número total de errores de INGESTA y CVS. Excluye las advertencias del ASIGNADOR.
   - **Tasa de ingesta:** Esta es la relación entre los registros ingeridos y los registros recibidos. El 100% de los registros recibidos se procesaron correctamente

![Tarjeta de fuentes en la pantalla de monitorización que muestra los registros recibidos, ingeridos y con errores](assets/fixing-errors-sources-ingestion-metrics.png "Métricas de ingesta de fuentes")

>[!NOTE]
>
>Con la ingesta parcial de datos habilitada, la **tasa de ingesta** para una ejecución de flujo de datos específica puede ser \&lt;100% hasta el umbral que haya establecido como parte de los detalles del flujo de datos. Además, tenga en cuenta que se informará de un éxito del 100 % en las ejecuciones de flujo de datos en las que no se haya introducido ningún dato.

>[!NOTE]
>
>Tenga en cuenta que los registros no se pueden perder.
>
>**Registros recibidos** = **Registros ingeridos** + **Registros con errores**
>
>**Tasa de ingesta = Registros ingeridos / Registros recibidos**
>
>**Umbral de ingesta parcial = Registros con errores / Registros recibidos**



## Identidades

Haga clic en la tarjeta **Identidades** y luego desplácese por la barra inferior para ver los detalles granulares de la ejecución del flujo de datos. Tenga en cuenta lo siguiente en el servicio de identidad

- **Registros recibidos:** 20 registros fueron recibidos por el *Almacén de identidad* mientras monitoreaba nuevos lotes, es decir, el conjunto de datos se marcó para el perfil.
- **Registros ingeridos:** 20 registros fueron ingeridos (es decir, procesados para información de identidad)
- **Registros omitidos:** Ninguno, ya que no teníamos registros de identidad únicos o registros con nuevas relaciones de identidad.
- **Tasa de éxito (solo disponible en la tarjeta):** Esta es la relación entre los registros recibidos y los registros ingeridos.
- **Identidades agregadas:** 40 identidades (20 para CustomerID y 20 para dirección de correo electrónico) se agregaron al gráfico de identidad general del Perfil del cliente en tiempo real
- **Gráficos creados:** Se crearon 20 gráficos únicos basados en los registros que procesó (es decir, relaciones encontradas en cada fila de datos)
- **Gráficos actualizados:** Esto le dirá si se agregaron identidades a un gráfico.

![Tarjeta de identidades en la pantalla de supervisión que muestra las métricas del gráfico de identidades](assets/fixing-errors-identity-service-ingestion-metrics.png "Métricas de ingesta del servicio de identidad")



## Perfiles

Haz clic en la tarjeta **Perfiles** y luego desplázate por la barra inferior para ver los detalles de la ejecución del flujo de datos. Tenga en cuenta lo siguiente en el servicio de perfil:

- **Registros recibidos:** El almacén de perfiles recibió 20 registros para su procesamiento
- **Error en los registros:** Ninguno de los registros produjo un error. Pero si habían fallado, entonces usted sabe que fue una ingesta en problema de perfil.
- **Fragmentos de perfil creados:** Se crearon 20 fragmentos de perfil
- **Fragmentos de perfil actualizados:** Se tocaron 20 fragmentos de perfil generales
- **Tasa de éxito:** Es del 100%. Esta es la proporción de registros que no se han recibido respecto a los registros recibidos.

>[!NOTE]
>
>Observe que la métrica **Registros omitidos** no está disponible para el perfil.

![Tarjeta de perfiles en la pantalla de monitorización que muestra métricas de fragmentos de perfil](assets/fixing-errors-profile-service-ingestion-metrics.png "Métricas de ingesta del servicio de perfil")

>[!NOTE]
>
>Tenga en cuenta que está la tarjeta de destino y tiene métricas que se parecen a las que exploramos en este laboratorio. Estas métricas solo tendrán sentido una vez que active una audiencia o un conjunto de datos.
