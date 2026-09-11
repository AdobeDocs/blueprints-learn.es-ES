---
hold: true
title: Automatización con API
description: Ejecute una colección Postman que automatice la creación de esquemas, grupos de campos, descriptores de identidad y relación y conjuntos de datos de una sola vez.
doc-type: article
solution: Experience Platform
exl-id: a490f93f-19da-4de3-81c8-4569c49c5354
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '306'
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



1. Debe aparecer una nueva ventana que muestre todas las llamadas de API en la carpeta. Establece **Delay** en **500ms** y luego haz clic en el botón **Ejecutar**.

![Ejecutar cuadro de diálogo de automatización con Retraso establecido en 500 ms antes de hacer clic en Ejecutar](assets/automate-with-apis-execute-automation-dialog.png "Ejecutar automatización")



1. Verá que las llamadas de API comienzan a ejecutarse en orden y, cuando se completen, verá 32 pruebas superadas.

![Ejecución correcta de automatización con 32 pruebas superadas](assets/automate-with-apis-successful-automation-32-passed-tests.png "Automatización correcta")



1. Vaya a la interfaz de usuario de Experience Platform y debería ver dos esquemas y dos conjuntos de datos creados y habilitados para el perfil con el prefijo **postman:**

![Dos esquemas creados y habilitados para el perfil con el postman: prefix](assets/automate-with-apis-schemas-created-in-ui.png "Esquemas de automatización")



![Dos conjuntos de datos creados con el postman: el prefijo coincide con los esquemas automatizados](assets/automate-with-apis-datasets-created-in-ui.png "Conjuntos de datos de automatización")

&#x200B;> [!TIP]
>
>¡Felicidades!  Acaba de automatizar la implementación de áreas de nombres de identidad, grupos de campos, esquemas, descriptores de identidad/relación y de habilitar un esquema para el perfil y generar un conjunto de datos utilizando el esquema
