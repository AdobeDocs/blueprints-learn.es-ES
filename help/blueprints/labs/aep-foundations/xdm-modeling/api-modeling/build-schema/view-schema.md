---
hold: true
title: Ver esquema
description: Vea un esquema del cliente recién creado en la interfaz de usuario de Experience Platform y mediante una llamada a la API de obtención de esquema.
doc-type: article
solution: Experience Platform
exl-id: 29302546-46dc-4c97-8fd8-deab6977635c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Ver esquema

## Ver a través de la IU

1. Abra el explorador y vuelva a la sección `Schema -> Browse`.

>[!NOTE]
>
>Actualice la interfaz de usuario para verla, ya que acaba de crearla y debe volver a consultar el registro de esquema

2. Buscar el esquema `Sample Customer Schema - <your sandbox number>`

3. Observe que la clase requerida y los grupos de campos asociados se agregan al esquema

![Esquema de cliente de ejemplo mostrado en la interfaz de usuario de Experience Platform con sus grupos de clases y campos](assets/view-schema-ui-view-of-sample-customer-schema.png "Vista de interfaz de usuario del Esquema de cliente de ejemplo")


## Ver mediante la API

1. Seleccione la API `Step 5 - Get Customer Account Schema` haciendo clic en ella.
1. En la dirección URL de la solicitud, reemplace `<replace me>` por el `$meta:altId` que guardó de la sección anterior (Crear el esquema) hasta el final de la llamada, como se muestra a continuación
1. Guarde las ediciones que ha realizado en la solicitud
1. Ejecute la solicitud haciendo clic en el botón `Send`

![Paso 5 - Obtener llamada de API de esquema de cuenta de cliente](assets/view-schema-step-5-get-customer-account-schema.jpeg "Paso 5 - Obtener esquema de cuenta de cliente")



Ejemplo de su solicitud final después de agregar `$meta:altId`

![Solicitud del paso 5 con el meta:altId anexado a la dirección URL](assets/view-schema-final-step-5-request.png "Solicitud del paso 5 final")



Si ha recibido una respuesta `200 OK`, debería poder examinar el esquema que ha creado a través de la vista de la estructura JSON de XDM

![Respuesta correcta de 200 que muestra el esquema completo de cuenta de cliente de muestra JSON](assets/view-schema-sample-customer-account-schema.png "Esquema de cuenta de cliente de muestra")
