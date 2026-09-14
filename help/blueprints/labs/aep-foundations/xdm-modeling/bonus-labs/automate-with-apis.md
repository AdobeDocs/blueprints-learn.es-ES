---
title: Automatización con API
description: Ejecute una colección Postman que automatice la creación de esquemas, grupos de campos, descriptores de identidad y relación y conjuntos de datos en una sola ejecución.
doc-type: article
solution: Experience Platform
exl-id: a490f93f-19da-4de3-81c8-4569c49c5354
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%
---

# Automatización con API

## Introducción

Para ver cómo puede automatizar las implementaciones mediante API, ejecute una carpeta de API que cree los siguientes objetos:

- Cuenta de cliente y esquema(s) \[Consulta] de plan
- Grupos de campos que componen los esquemas anteriores
- Descriptores de identidad necesarios para el perfil
- Descriptores de relación y referencia necesarios para crear las relaciones entre la cuenta del cliente y el plan \[Consulta]
- Dos conjuntos de datos que coinciden con cada esquema creado



## Ejecutar la carpeta

1. En Postman, vaya a la carpeta **Automatización con API** dentro de la carpeta **XDM Schema Lab**

   ![Automatización con carpeta API dentro de la carpeta XDM Schema Lab en Postman](assets/automate-with-apis-postman-automation-folder.png)



1. Haz clic en la carpeta **Automatización con API** y en el área de trabajo haz clic en el botón **Ejecutar**

   >[!NOTE]
   >
   >El botón de ejecución se encuentra en la parte superior derecha de su espacio de trabajo de Postman

   ![Botón Ejecutar en la parte superior derecha de Postman Workspace para la carpeta Automatización con API](assets/automate-with-apis-click-folder-run-button.png "Haga clic en la carpeta Ejecutar")



1. Aparece una nueva ventana que muestra todas las llamadas de API en la carpeta. Establece **Delay** en **500ms** y luego haz clic en el botón **Ejecutar**.

   ![Ejecutar cuadro de diálogo de automatización con Retraso establecido en 500 ms antes de hacer clic en Ejecutar](assets/automate-with-apis-execute-automation-dialog.png "Ejecutar automatización")



1. Verá que las llamadas de API comienzan a ejecutarse en orden y, cuando se completan, verá 32 pruebas aprobadas.

   ![Ejecución correcta de automatización con 32 pruebas superadas](assets/automate-with-apis-successful-automation-32-passed-tests.png "Automatización correcta")



1. Vaya a la interfaz de usuario de Experience Platform y verá dos esquemas y dos conjuntos de datos creados y habilitados para el perfil con el prefijo **postman:**

![Dos esquemas creados y habilitados para el perfil con el postman: prefix](assets/automate-with-apis-schemas-created-in-ui.png "Esquemas de automatización")



![Dos conjuntos de datos creados con el postman: el prefijo coincide con los esquemas automatizados](assets/automate-with-apis-datasets-created-in-ui.png "Conjuntos de datos de automatización")

>[!SUCCESS]
>
>¡Felicidades!  Ha automatizado la implementación de áreas de nombres de identidad, grupos de campos, esquemas, descriptores de identidad/relación y ha habilitado un esquema para el perfil y ha generado un conjunto de datos utilizando el esquema
