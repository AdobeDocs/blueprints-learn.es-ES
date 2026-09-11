---
title: Importar colección de API
description: Importe la colección de API de Postman de bootcamp y compruebe que las variables de entorno se resuelven correctamente en su zona protegida.
doc-type: article
solution: Experience Platform
exl-id: 7562c7f1-0d60-4a3a-8bce-fa42bda08962
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---


# Importar colección de API

## Objetivo

En este paso va a importar la colección de API que contiene todas las distintas solicitudes que va a necesitar para realizar a lo largo del bootcamp.  Estas solicitudes de API dependen del archivo de entorno que acaba de importar.



## Importar colección de solicitudes

1. Descargue el archivo **AJO Bootcamp (Labs).postman\_collection.json**:

   Descargar archivo: [AJO Bootcamp (Labs).postman_collection.json](assets/ajo-bootcamp-labs.postman_collection.json)

2. Como antes, haz clic en el botón **Importar**.
3. Pegue la URL local del archivo **AJO Bootcamp (Labs).postman\_collection.json** en el cuadro de texto modal de importación o suéltelo en el cuadro de diálogo de importación.  Esto déclencheur una importación automática.
4. Una vez completado el proceso de importación, haga clic en **Colecciones** en la barra de navegación izquierda, expanda la carpeta **AJO Bootcamp (Labs)** y verá la colección recién importada

![comprobar importación de colección de postman](assets/import-api-collection-verify-collection-imported.png)

>[!TIP]
>
>¡Felicidades!  Ha importado correctamente la colección Postman del campamento de arranque



## Validar variables de entorno

La colección que importó contiene todas las llamadas de API necesarias que necesitará para los laboratorios en todo el bootcamp.  Cada laboratorio está organizado en una carpeta específica con su propio conjunto de solicitudes.

A continuación, se encuentran los detalles de cada carpeta:

- **Laboratorios de perfil y Recorrido**: contiene un conjunto de solicitudes para enviar un evento web y un evento que simula una confirmación de envío.
- **Decisioning Labs**: contiene solicitudes para 3 visitantes que imitan las llamadas a las páginas superior e inferior que normalmente se encontrarían en un sitio etiquetado con AEP Web SDK.

Para asegurarse de que el entorno y la colección funcionan correctamente juntos, siga estos pasos.

1. Si es necesario, haga clic en **Colecciones** en el carril izquierdo y, a continuación, expanda la carpeta **Profile &amp; Recorrido Labs**.
2. Haga clic en la solicitud **Crear evento web** y verá que las variables de entorno son **rojas**

   ![Solicitud de Postman que muestra las variables de entorno resaltadas en rojo porque no se seleccionó ningún entorno](assets/import-api-collection-environment-variables-shown-red.png "Compruebe que las variables de entorno de Postman estén en rojo")

3. Haga clic en el menú desplegable **Entorno** en la esquina superior derecha y elija el entorno **AJO Bootcamp**.

   ![Seleccionar el entorno de Postman correcto](assets/import-api-collection-select-postman-environment.png)

4. Con el entorno adecuado seleccionado, verá que la variable EDGE\_REGION ahora se vuelve de color azul más claro. Esto indica que la variable ahora tiene un valor para el entorno seleccionado. La variable DATASTREAM\_CONFIG permanece en rojo porque aún no ha creado el conjunto de datos, por lo que no tiene un valor para esa variable de entorno. Al pasar el ratón por encima de EDGE\_REGION, verá cuál es el valor del entorno.

![La variable EDGE_REGION de Postman ahora está rellenada y ya no se muestra en rojo](assets/import-api-collection-environment-works-with-collection.png "Compruebe que el entorno de Postman funciona con la colección")

## Resumen

Ahora tiene importados los archivos de entorno y colección y sabe cómo utilizarlos.
