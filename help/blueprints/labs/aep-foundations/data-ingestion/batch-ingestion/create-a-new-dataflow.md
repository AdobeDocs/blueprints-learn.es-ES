---
hold: true
title: Crear un nuevo flujo de datos
description: Cree un flujo de datos de origen por lotes con un conjunto de datos existente e importe asignaciones de un flujo de datos anterior para acelerar la configuración.
doc-type: article
solution: Experience Platform
exl-id: 6f26f742-27e8-445a-8005-21d4e59dc3d0
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Crear un nuevo flujo de datos

## Navegar a orígenes

1. En la interfaz de usuario de Adobe Experience Platform, vaya a la siguiente ubicación:\
   **Fuentes** -> **Catálogo** -> **Sistema local**
1. Siguiente clic en el botón **Agregar datos** para la tarjeta **Carga de archivos locales**

![Botón Agregar datos para la tarjeta de carga de archivos locales en el catálogo de fuentes](assets/create-a-new-dataflow-local-file-upload-add-data.png "Acceso a la zona de aterrizaje de datos")



## Configuración del flujo de datos

1. En la pantalla de detalles de flujo de datos, elija **Conjunto de datos existente**.
1. Utilice el conjunto de datos que creó anteriormente con el nombre **Cuenta de cliente - \&lt;Sus iniciales>**
1. Asegúrese de tener activada la opción **Conjunto de datos del perfil**.
(Si no lo activa, el Almacenamiento de perfiles no podrá supervisar los nuevos datos que entren en este conjunto de datos y, por lo tanto, no ingerirá estos datos en el Perfil)
1. Asegúrese de que tiene activada la opción **Habilitar ingesta parcial**
(Si no activa esta opción, puede producirse un error en toda la ingesta si solo uno de los registros contiene un error).
1. Establezca el nombre del flujo de datos como **Lote de cuenta de cliente v2 - \&lt;Sus iniciales>**
1. Activar todas las alertas **Inicio/Éxito/Error del flujo de datos de origen**
1. Si todo parece correcto, haga clic en el botón **Siguiente** en la esquina superior derecha de la pantalla para continuar con el siguiente paso.

![Pantalla de detalles de flujo de datos configurada con el conjunto de datos existente para el segundo flujo de datos](assets/create-a-new-dataflow-existing-dataset-flow-details.png "Detalles de flujo de datos")



## Cargar archivo de muestra

1. Arrastre y suelte o cargue el archivo **Lab\_Customer\_Account.csv** en la interfaz de usuario.  Cuando termine, la pantalla debería tener el aspecto siguiente.

![Vista previa del archivo CSV de la cuenta de cliente cargado para el segundo flujo de datos](assets/create-a-new-dataflow-uploaded-csv-preview.png "Acceso a los archivos del Explorador de almacenamiento de Azure en Adobe Experience Platform")



## Importar asignaciones

En la pantalla de asignación, en lugar de volver a configurar todas las asignaciones, puede importar las que haya creado anteriormente.

1. Haz clic en el botón **Importar asignación**
1. Seleccione el flujo de datos que tiene la asignación creada anteriormente



![Botón de asignación de importación en la pantalla de asignación](assets/create-a-new-dataflow-import-mapping-button.png "Botón de asignación de importación")



![Cuadro de diálogo para seleccionar el flujo de datos para importar la asignación de](assets/create-a-new-dataflow-select-dataflow-to-import-mapping-from.png "Seleccione el flujo de datos para importar la asignación de")

>[!NOTE]
>
>La importación de asignaciones es una forma útil de reutilizar asignaciones de otros flujos de datos y reducir la cantidad de trabajo de asignación que debe realizar
