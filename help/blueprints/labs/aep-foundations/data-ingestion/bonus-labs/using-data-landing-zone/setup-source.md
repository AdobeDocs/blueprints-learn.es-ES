---
hold: true
title: Configuración del origen
description: Cargue un archivo de cuenta de cliente de muestra en la zona de aterrizaje de datos y configure un nuevo flujo de datos de origen de almacenamiento en la nube.
doc-type: article
solution: Experience Platform
exl-id: 1c80e71b-19a7-45e9-9961-d72b3f03ecae
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# Configuración del origen

## Cargar archivo de muestra

Debe cargar un archivo de datos de muestra en la zona de aterrizaje de datos a través del Explorador de almacenamiento de Azure para poder utilizarlo durante el laboratorio.  Para ello, haga lo siguiente:

1. Descargar los [archivos de ejemplo](../../sample-files.md)
1. Arrastre y suelte o cargue el archivo **Lab\_Customer\_Account.csv** en la zona de aterrizaje de datos que guardó desde el paso anterior.

Cuando se cargue, la pantalla debería parecerse a la captura de pantalla siguiente.

>[!WARNING]
>
>Asegúrese de no cargar el archivo en la carpeta *project*. Contiene datos precargados que no se utilizan en nuestros laboratorios.

![Explorador de archivos de zona de aterrizaje de datos que muestra el archivo Lab_Customer_Account.csv cargado, no la carpeta del proyecto](assets/setup-source-make-sure-you-do-not-upload-the-file.png)

## Navegar a orígenes

1. Vaya a Adobe Experience Platform y vaya a: **Orígenes** -> **Catálogo** -> **Almacenamiento en la nube**
1. Haz clic en **Configuración** / **Agregar datos** para la zona de aterrizaje de datos

![Configurar o agregar acción de datos para la fuente de almacenamiento en la nube de la zona de aterrizaje de datos](assets/setup-source-add-data-landing-zone-source.png "Acceder a la zona de aterrizaje de datos")

>[!NOTE]
>
>Si existe al menos una conexión para ese origen, verá **Agregar datos** como la acción predeterminada. Si no existen conexiones para ese origen, verá **Configuración** como la acción predeterminada

## Previsualización del archivo

1. Seleccione **Lab\_Customer\_Account.csv**

![Selección del archivo Lab_Customer_Account.csv para previsualizarlo en el Explorador de almacenamiento de Azure](assets/setup-source-select-lab-customer-account-csv.png "Acceso a los archivos del Explorador de almacenamiento de Azure en Adobe Experience Platform")

1. En el panel de vista previa, observe los siguientes atributos y lo siguiente:

- **sms\_optIn** es un campo de consentimiento con varios valores que faltan (se muestran en la vista previa como - )
- **account\_create\_date** no tiene el formato de fecha adecuado. Tiene valores de cadena junto con valores de fecha y hora en una cadena.
- **account\_end\_date** tiene el formato de fecha correcto.



![campo sms_optIn con varios valores que faltan en la vista previa del archivo](assets/setup-source-sms-optin-missing-values.png "sms_optin")



![campos account_create_date y account_end_date mostrados en la vista previa del archivo](assets/setup-source-account-create-date-account-end-date.png "account_create_date y account_end_date")

>[!NOTE]
>
>Más adelante en este laboratorio tendrá que lidiar con los valores, fechas y campos con formato incorrecto que faltan en los pasos de asignación

1. Haga clic en **Siguiente** en la esquina superior derecha de la pantalla para continuar con el paso siguiente



## Configuración del flujo de datos

1. En la pantalla Detalles del flujo de datos, elija **Nuevo conjunto de datos**.
1. Asigne un nombre al conjunto de datos de salida **Cuenta de cliente - \&lt;Sus iniciales>**
1. Seleccione el esquema **dep: Customer Account** de la lista desplegable.
1. Active la casilla de verificación **Conjunto de datos del perfil**.
(Si no lo activa, el Almacenamiento de perfiles no puede supervisar los nuevos datos que entran en este conjunto de datos y, por lo tanto, no ingiere estos datos en el Perfil)
1. Active **Habilitar la ingesta parcial**.
(Si no activa esta opción, la ingesta puede fallar si uno de los registros tiene errores).
1. Establezca el nombre del flujo de datos como **Ingesta por lotes de la cuenta del cliente - \&lt;Sus iniciales>**
1. Activar todas las alertas **Inicio/Éxito/Error del flujo de datos de origen**

![Pantalla de detalles de flujo de datos con nuevos ajustes de conjunto de datos, alternancia de perfil e ingesta parcial configurados](assets/setup-source-dataflow-detail-screen-settings.png "Detalles del flujo de datos")

>[!CAUTION]
>
> Asegúrese de que ha **habilitado el conjunto de datos** tanto para la ingesta de perfiles como para la ingesta parcial.

Haga clic en **Siguiente** en la esquina superior derecha de la pantalla para continuar con el paso siguiente.

>[!NOTE]
>
>**Habilitar la ingesta parcial** especifica el número de errores (**INGESTA** y **DCVS**) como un porcentaje del número total de registros que pueden fallar antes de que se declare un error en todo el flujo de datos.
