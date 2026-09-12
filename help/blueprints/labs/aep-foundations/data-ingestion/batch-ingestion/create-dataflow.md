---
title: Crear flujo de datos
description: Configure un flujo de datos de origen por lotes con un nuevo conjunto de datos, habilite Perfil e ingesta parcial, y cargue un archivo CSV de cuenta de cliente de ejemplo.
doc-type: article
solution: Experience Platform
exl-id: 70145966-d6c0-4741-8216-903de0d61e1d
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---


# Crear flujo de datos

## Navegar a orígenes

1. En la interfaz de usuario de Adobe Experience Platform, vaya a la siguiente ubicación:\
   **Fuentes** -> **Catálogo** -> **Sistema local**
1. Siguiente clic en el botón **Agregar datos** para la tarjeta **Carga de archivos locales**

![Botón Agregar datos para la tarjeta de carga de archivos locales en el catálogo de fuentes](assets/create-dataflow-local-file-upload-add-data.png "Acceso a la zona de aterrizaje de datos")



## Configuración del flujo de datos

1. En la pantalla Detalles del flujo de datos, elija **Nuevo conjunto de datos**.
1. Asigne un nombre al conjunto de datos de salida **Cuenta de cliente - \&lt;Sus iniciales>**
1. Seleccione el esquema **dep: Customer Account** de la lista desplegable.
1. Active la casilla de verificación **Conjunto de datos del perfil**.
(Si no lo activa, el Almacenamiento de perfiles no puede supervisar los nuevos datos que entran en este conjunto de datos y, por lo tanto, no ingiere estos datos en el Perfil)
1. Active **Habilitar la ingesta parcial**.
(Si no activa esta opción, puede producirse un error en toda la ingesta si solo uno de los registros contiene un error).
1. Establezca el nombre del flujo de datos como **Lote de cuenta de cliente - \&lt;Sus iniciales>**
1. Activar todas las alertas **Inicio/Éxito/Error del flujo de datos de origen**

   ![Pantalla de detalles de flujo de datos con los nuevos ajustes de conjunto de datos, perfil e ingesta parcial configurados](assets/create-dataflow-new-dataset-flow-details.png "Detalles del flujo de datos")

   >[!NOTE]
   >
   >**Al habilitar la ingesta parcial**, se especifica el número de errores (**INGESTA** y **DCVS**) como porcentaje del número total de registros que pueden fallar antes de que se declare un error en todo el flujo de datos.

   >[!CAUTION]
   >
   >Asegúrese de haber **habilitado el conjunto de datos** tanto para la ingesta de perfiles como para la ingesta parcial antes de continuar.

1. Si todo parece correcto, haga clic en el botón **Siguiente** en la esquina superior derecha de la pantalla para continuar con el siguiente paso.



## Cargar archivo de muestra

1. Descargar los archivos de muestra de [Archivos de muestra](../sample-files.md) para usarlos con este laboratorio
1. Arrastre y suelte o cargue el archivo **Lab\_Customer\_Account.csv** en la interfaz de usuario.  Cuando termine, la pantalla debería tener el aspecto siguiente.

   ![Vista previa del archivo CSV de cuenta de cliente cargado en la pantalla de datos de origen](assets/create-dataflow-uploaded-csv-preview.png "Acceso a los archivos del Explorador de almacenamiento de Azure en Adobe Experience Platform")

1. En el panel de vista previa, observe los siguientes atributos y tenga en cuenta lo siguiente:

   - **sms\_optIn** es un campo de consentimiento con varios valores que faltan (se muestran en la vista previa como - )
   - **account\_create\_date** no tiene el formato de fecha adecuado. Tiene valores de cadena junto con valores de fecha y hora en una cadena.
   - **account\_end\_date** tiene el formato de fecha correcto.



   ![Vista previa que muestra el campo sms_optIn con varios valores de consentimiento que faltan](assets/create-dataflow-sms-optin-missing-values.png "sms_optin")



   ![Vista previa de los valores de los campos account_create_date y account_end_date que muestran un formato incoherente](assets/create-dataflow-account-create-end-date-preview.png "account_create_date y account_end_date")

   >[!NOTE]
   >
   >Más adelante en este laboratorio tendrá que lidiar con los valores, fechas y campos con formato incorrecto que faltan en los pasos de asignación

1. Haga clic en el botón **Siguiente** en la esquina superior derecha de la pantalla para continuar con el paso siguiente
