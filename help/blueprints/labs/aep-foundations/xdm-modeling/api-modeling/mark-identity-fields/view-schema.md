---
hold: true
title: Ver esquema
description: Vea los descriptores de identidad de un esquema a través de la interfaz de usuario y la API, y compare las opciones de encabezado Aceptar para las respuestas de esquema resueltas frente a no resueltas.
doc-type: article
solution: Experience Platform
exl-id: 44eedb82-259f-4f7f-84fe-acc2b42376eb
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# Ver esquema

## Ver a través de la IU

1. Abra el explorador y vuelva a la sección `Schema -> Browse`.
1. Buscar el esquema **Cuenta de cliente**
1. Observe que las identidades se agregan al esquema

![Vista de exploración de esquemas que muestra identidades agregadas al esquema](assets/view-schema-schema-ui-with-identities.png "Vista de IU de esquemas con identidades")


## Ver mediante la API

1. Seleccione la API `Step 3 - Get Customer Account Schema and its descriptors` haciendo clic en ella.

![Paso 3 - Obtener esquema de cuenta de cliente con solicitud de API de descriptores](assets/view-schema-step-3-get-customer-account-schema-w-descriptors.png "Paso 3 - Obtener esquema de cuenta de cliente con descriptores")



1. En la dirección URL de la solicitud, reemplace `<replace me>` por el `$meta:altId` que guardó de la sección anterior (Crear el esquema) hasta el final de la llamada, como se muestra a continuación

![Solicitud del paso 5 final con altId anexado a la dirección URL](assets/view-schema-final-step-5-request.png "Solicitud del paso 5 final")



1. Guarde las ediciones que ha realizado en la solicitud

1. Ejecute la solicitud haciendo clic en el botón `Send`

Ahora debería ver una respuesta `200 OK` y poder examinar el esquema creado a través de la lente de la estructura JSON de XDM

![Cuerpo de respuesta de API que muestra la estructura JSON de XDM del esquema](assets/view-schema-body-of-the-api-response.png "Cuerpo de respuesta de API")



Vaya más abajo en la respuesta de la API para ver los descriptores de identidad que ha creado

![Descriptores de identidad mostrados en la respuesta de API](assets/view-schema-descriptors-displayed-in-api-response.png "Descriptores mostrados en la respuesta de API")


## Aceptar encabezados

Observe el encabezado **Accept** utilizado en la solicitud. Este encabezado indica al registro de esquemas XDM que devuelva `$refs` del esquema sin resolver (es decir, que muestre la cantidad mínima de información) junto con sus descriptores asociados en la respuesta de API.  Adobe proporciona otros **encabezados Accept** que puede usar para obtener diversos grados de detalle sobre el esquema.

![Aceptar campo de encabezado en el Paso 3 Obtener solicitud de esquema de cuenta de cliente](assets/view-schema-accept-header.png "Paso 3 - Obtener esquema de cuenta de cliente Aceptar encabezado")

>[!NOTE]
>
>Puede leer más sobre los distintos encabezados Aceptar aquí -> [Extremo de API de esquema de Experience League](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=es#lookup)



Para ver esto en acción, cambie el encabezado **Accept** para indicarle al registro de esquemas que responda con todos los `$ref` y `allOf` resueltos por completo (es decir, explotados) y cualquier descriptor asociado

1. Actualice el valor del encabezado `Accept` al siguiente:
   `application/vnd.adobe.xed-full-desc+json; version=1`
1. Guardar la solicitud utilizando el botón `Save`
1. Ejecute la solicitud utilizando el botón `Send`

Ahora debería ver una respuesta con este aspecto:

![Respuesta de esquema completamente explotada que muestra todas las propiedades resueltas](assets/view-schema-fully-exploded-schema-showing-all-properties.png "Esquema completamente explotado que muestra todas las propiedades")

>[!NOTE]
>
>Observe cómo todas las propiedades del esquema ahora se muestran completamente en la respuesta, mientras que en la llamada anterior solo se le mostraron los valores `$ref` del esquema (es decir, a qué grupos de campos se hacía referencia) y no se resolvió nada por completo en cada campo o propiedad individual.

>[!NOTE]
>
>Es importante comprender esto porque, al trabajar con API, no siempre necesita la respuesta completamente resuelta si lo único que hace es obtener `$id` del esquema o simplemente comprobar su composición
