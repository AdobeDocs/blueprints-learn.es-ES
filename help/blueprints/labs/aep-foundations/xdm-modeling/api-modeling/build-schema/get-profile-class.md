---
title: Obtener clase de perfil
description: Llame a la API del Registro de esquemas globales para recuperar y guardar el $id de la clase XDM Individual Profile para utilizarlo en un esquema personalizado.
doc-type: article
solution: Experience Platform
exl-id: d87c21a2-dad4-4666-b917-cdf8e16058d4
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Obtener clase de perfil

## Ejecute el paso 3: Obtención de clase de perfil

1. Haga clic en la solicitud `Step 3 - Get Profile Class` en la carpeta `XDM API Lab -> Create Schema`
1. Ejecutar haciendo clic en el botón `Send`

![Paso 3: Obtener solicitud de API de clase de perfil](assets/get-profile-class-step-3-api-request.jpeg "Paso 3: Obtener solicitud de API de clase de perfil")

>[!NOTE]
>
>Observe que en la petición GET la ruta de acceso `global`: .../schemaregistry/**global**/classes. Recuerde que el uso de `global` indica al registro de esquemas que solo queremos devolver objetos XDM estándar de Adobe


## Busque y guarde la clase $id

Después de ejecutar la solicitud de API, realice los siguientes pasos para localizar y guardar `$id` para la clase de perfil individual de XDM.

1. Busque la clase `XDM Individual Profile` en la respuesta
1. Copie `$id` para la clase `XDM Individual Profile` y guárdelo en algún lugar al que pueda hacer referencia posteriormente.

![Clase de perfil individual XDM ubicada en la respuesta de API](assets/get-profile-class-xdm-individual-profile-class.png "Clase de perfil individual XDM")

>[!WARNING]
>
>No continúe hasta que haya guardado `$id` en algún lugar.  Se requerirá más adelante para crear el esquema de cuenta de cliente
