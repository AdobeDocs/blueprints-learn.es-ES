---
title: Colección de API
description: Descargue e importe la colección de API de Postman de bootcamp que contiene las solicitudes utilizadas en los laboratorios de AEP Foundations.
doc-type: article
solution: Experience Platform
exl-id: 18d820c5-56ad-46b8-a9cf-f725555d2db3
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Colección de API

## Archivo de recopilación de API de Postman

Descargar archivo: [AEP Foundations Bootcamp (Labs).postman_collection.json](assets/aep-foundations-bootcamp-labs.postman_collection.json)



## Importar colección de API

1. Abra `Postman API Collection File` desde arriba en el explorador haciendo clic en el archivo
1. Copie la dirección URL del archivo en el portapapeles
1. Inicie Postman en el equipo local y haga clic en el botón `Import` del área de trabajo
1. Pegue la dirección URL de `Postman API Collection File` en el cuadro de texto modal de importación de la superposición.  Esto debería almacenar en déclencheur una importación automática

![Haciendo clic en el botón Importar del área de trabajo de Postman para importar la colección de API](assets/api-collection-click-import-button.png "Botón Importar")



![Pegando la dirección URL del archivo de recopilación de API en el cuadro de texto modal de importación de Postman](assets/api-collection-import-modal-paste-url.png "Cuadro de texto modal del botón de importación")

Ahora debería ver una colección que se rellena bajo la ficha `Collections` de la barra lateral izquierda llamada `AEP Foundations Bootcamp`



![Colección de Bootcamp de AEP Foundations completada en la ficha de la barra lateral de Postman Collections](assets/api-collection-imported-collection-in-sidebar.png)

## Resumen de la colección Bootcamp de AEP Foundations

La colección de API que importó contiene todas las llamadas de API necesarias que necesitará para los laboratorios durante todo el bootcamp.  Cada laboratorio está organizado en una carpeta específica con su propio conjunto de API.  Tenga esto en cuenta a medida que trabaje en los laboratorios esta semana.

A continuación, se encuentran los detalles de cada carpeta:

- **Autenticar IMS**: contiene una única solicitud para generar un access\_token, que es necesario al trabajar con cualquiera de las API de Adobe Experience Platform
- **Laboratorio de esquemas XDM**: contiene un conjunto de solicitudes para crear los componentes XDM necesarios para crear y configurar un esquema para el perfil del cliente en tiempo real
- **Laboratorio de ingesta de datos**: contiene un conjunto de solicitudes de transmisión de datos a Experience Platform
- **Laboratorio de perfiles**: contiene un conjunto de solicitudes para ver los rasgos y comportamientos del Perfil del cliente en tiempo real

>[!TIP]
>
>¡Felicidades!  Ha importado correctamente la colección Postman del campamento de arranque
