---
title: Importar archivo de entorno
description: Importe el archivo de entorno de Postman y establezca las variables globales como EDGE_REGION necesarias para las llamadas de API en todo el bootcamp.
doc-type: article
solution: Experience Platform
exl-id: a5d45656-e3f5-4207-823c-ad33d4ef26a4
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%
---

# Importar archivo de entorno

## Objetivo

En esta página, se importa el archivo de entorno de Postman.  Este archivo contiene una serie de variables globales que se utilizan en varias llamadas API que realiza durante otros laboratorios en el bootcamp.

## Importar archivo de entorno

1. Descargar el archivo **AJO Bootcamp.postman\_environment.json**:

   Descargar archivo: [AJO Bootcamp.postman_environment.json](assets/ajo-bootcamp.postman_environment.json)

2. Inicie Postman en el equipo local.
3. Si es necesario, cambie a la Workspace que está usando para estos laboratorios y haga clic en el botón **Importar**.

   ![Postman comienza a importar](assets/import-environment-file-click-import-button.png)

4. Pegue la URL local del archivo **AJO Bootcamp.postman\_environment.json** en el cuadro de texto modal de importación o suéltelo en el cuadro de diálogo de importación.  Esta acción déclencheur una importación automática

   ![Cuadro de diálogo de importación de Postman que muestra la opción para pegar una URL de archivo](assets/import-environment-file-import-button-overlay.png "Importación de Postman a través de la URL")

   ![cuadro de diálogo de importación de Postman que acepta un archivo colocado mediante arrastrar y soltar](assets/import-environment-file-drag-and-drop-import.png "Importación de Postman mediante arrastrar y soltar")

5. Una vez importado, compruebe que el entorno existe haciendo clic en la ficha **Entornos** en la barra lateral izquierda. Verá que el entorno de Bootcamp de AJO ya está disponible.

![Validar importación de entorno](assets/import-environment-file-validate-environment-imported.png)

## Establecer variables de entorno

Postman se ha diseñado para probar e interactuar con las API. Sin embargo, este laboratorio lo utiliza para simular las visitas de AEP Web SDK desde un explorador o para las llamadas de recopilación de datos en tiempo real del lado del servidor. Aunque técnicamente estas solicitudes son llamadas de API, no son llamadas de API típicas que requieren cosas como tokens de autorización en el encabezado. Las variables de entorno de estos laboratorios se utilizan principalmente para variables en rutas URL (y se utiliza una en un encabezado).

1. Si es necesario, haga clic en la pestaña **Entornos** en la barra lateral izquierda de Postman
2. Haga clic en el archivo de entorno **AJO Bootcamp**. Verá algunos valores que debe rellenar

   ![Variables de entorno de Postman con valores vacíos que deben rellenarse](assets/import-environment-file-values-need-filling-in.png "Compruebe las variables de Postman en los entornos")

3. Omita el valor DATASTREAM\_CONFIG por ahora. Puede crear una configuración de secuencia de datos en un laboratorio posterior.
4. Actualice el campo **EDGE\_REGION** con el código de región que esté más cerca de donde se encuentra físicamente para este campo de arranque, utilizando la tabla siguiente como búsqueda.

   | **Región** | **Código de región** |
   | ---------- | --------------- |
   | Oeste de Estados Unidos | o2 |
   | Este de Estados Unidos | va6 |
   | Europa | irl1 |
   | Australia | aus3 |
   | Japón | jpn3 |
   | Asia | spg3 |

   Cuando termine, el archivo de entorno tendrá un aspecto similar al siguiente:



   ![Verificar variable de región Postman](assets/import-environment-file-region-variable-set.png)

5. Ahora debe guardar las variables de entorno; sin embargo, no hay ningún botón Guardar en la interfaz de usuario de Postman. Utilice las teclas de acceso rápido de Windows o Mac para guardar (Ctrl+S en Windows, por ejemplo). Sabe que sus cambios se han guardado cuando ve un mensaje de **Cambios guardados** en la esquina inferior derecha de la interfaz de usuario de Postman:

![Verificar cambios guardados](assets/import-environment-file-changes-saved-confirmation.png)

>[!SUCCESS]
>
>¡Felicidades! Ha completado el archivo de entorno de Postman
