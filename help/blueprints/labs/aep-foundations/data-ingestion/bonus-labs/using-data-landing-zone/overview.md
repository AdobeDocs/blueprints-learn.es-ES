---
hold: true
title: Uso de la zona de aterrizaje de datos
description: Instale y configure el Explorador de almacenamiento de Azure con una URL SAS para conectarse a la zona de aterrizaje de datos de Adobe Experience Platform.
doc-type: overview-page
solution: Experience Platform
exl-id: d61bef25-7039-450d-a8e7-01bb12e8df7c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Uso de la zona de aterrizaje de datos

## Prerrequisitos

Si no ha descargado el Explorador de almacenamiento de Azure, hágalo ahora, ya que es un requisito para este laboratorio.  Puede encontrar la descarga en el siguiente enlace:

[Descargar el Explorador de almacenamiento de Azure](https://azure.microsoft.com/en-us/blog/microsoft-azure-data-lake-storage-adls-in-storage-explorer-public-preview/)

1. Instalación de la aplicación
1. Al iniciar por primera vez, acepte el Contrato de licencia de usuario final

![Pantalla del Contrato de licencia para el usuario final en Azure Storage Explorer](assets/overview-end-user-license-agreement-screen.png "Pantalla del Contrato de licencia para el usuario final")


## Configuración del Explorador de almacenamiento de Azure con Experience Platform

1. Abra el Explorador de almacenamiento de Azure, haga clic en el **icono Seleccionar recurso** y, a continuación, seleccione **Contenedor o directorio ADLS Gen 2**

![Seleccionar el contenedor o directorio ADLS Gen2 como recurso en el Explorador de almacenamiento de Azure](assets/overview-choose-the-resource-as-shown-above.png)



1. Seleccione **URL de firma de acceso compartido (SAS)** y haga clic en **Siguiente**

![Elegir la opción de URL SAS como modo de conexión](assets/overview-choose-the-sas-url-option-as-the-mode-of-connection.png "Elija la opción de URL SAS como modo de conexión")



1. Escriba el nombre para mostrar como **Zona de aterrizaje de datos**

>[!NOTE]
>
>No puede continuar en este paso hasta que proporcione la dirección URL de SAS.  Esto se obtiene de Experience Platform, que se ve en el siguiente paso.

![Nombrar la zona de aterrizaje de datos de la conexión](assets/overview-name-the-connection.png "Nombrar la conexión")



1. Vaya a Adobe Experience Platform y desplácese hasta la zona de aterrizaje de datos haciendo lo siguiente:

- Vaya a **Orígenes -> Catálogo**
- Seleccione **Almacenamiento en la nube** en los orígenes
- A continuación, busque la tarjeta **Zona de aterrizaje de datos**
- Haga clic en la tarjeta de la zona de aterrizaje de datos y, a continuación, haga clic en **Ver credenciales** en el carril derecho

![Tarjeta de origen de zona de aterrizaje de datos con la opción Ver credenciales en Adobe Experience Platform](assets/overview-data-landing-zone-view-credentials.png "Acceder a la tarjeta Source de zona de aterrizaje de datos en Adobe Experience Platform")



1. Copie **SASUri** del modal que se muestra.

Vuelva al Explorador de almacenamiento de Azure y pegue el valor **SASUri** en el **contenedor de blobs o en la URL de SAS de directorio** que dejó en blanco en el paso anterior

![Copiando el valor SASUri de Experience Platform en el Explorador de almacenamiento de Azure](assets/overview-copy-sas-uri-into-azure-storage-explorer.png "Copie las credenciales de la URL SAS de Adobe Experience Platform y cópielo en el Explorador de almacenamiento de Azure")



1. Haga clic en **Siguiente** para continuar

![Copiando credenciales de URL SAS en la sección de URL SAS de la información de conexión](assets/overview-copy-sas-url-into-connection-info.png "Copie las credenciales de URL SAS en la sección de URL SAS de la información de conexión")



1. En la pantalla Resumen, haz clic en **Conectar**

![Pantalla de resumen con el botón Conectar](assets/overview-connect-screen.png "Pantalla de conexión")



Ahora debería ver una pantalla similar a la siguiente

![Explorador de almacenamiento de Azure que muestra la cuenta de la zona de aterrizaje de datos conectada correctamente](assets/overview-successfully-connected-account.png)

> [!TIP]
>
>¡Felicidades!  Ha configurado correctamente el Explorador de almacenamiento de Azure
