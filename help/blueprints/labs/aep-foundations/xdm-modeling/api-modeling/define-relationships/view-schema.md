---
hold: true
title: Ver esquema
description: Vea la relación de búsqueda del esquema de cuenta de cliente con el esquema de planificación a través de la interfaz de usuario del esquema y la API de obtención de esquema.
doc-type: article
solution: Experience Platform
exl-id: dae48ef4-f762-4173-8564-c1ad40c0109b
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Ver esquema

## Ver a través de la IU

1. Abra el explorador y vuelva a la sección `Schema -> Browse`.
1. Buscar el esquema `Sample Customer Schema - <your sandbox number>`
1. Observe que la relación con `dep: Plan [Lookup]` está definida

![Esquema de cliente de muestra en la interfaz de usuario de Experience Platform que muestra la relación profunda: búsqueda de plan](assets/view-schema-relationship-to-plan-lookup-schema.png)


## Ver mediante la API

1. Seleccione la API `Step 4 - Get Customer Account Schema and its descriptors` haciendo clic en ella

![Paso 4: obtención del esquema de cuenta de cliente y sus descriptores Llamada de API](assets/view-schema-step-4-get-schema-and-descriptors.png "Paso 4: obtención del esquema de cuenta de cliente y sus descriptores")



2. En la dirección URL de la solicitud reemplace `<replace me>` por el `$meta:altId` que guardó de la sección anterior [Crear esquema](../build-schema/create-schema.md), como se muestra a continuación

![Solicitud del paso 4 con el meta:altId anexado a la dirección URL](assets/view-schema-final-step-4-request.png "Solicitud del último paso 4")



3. Guardar la solicitud utilizando el botón `Save`

4. Ejecute la solicitud haciendo clic en el botón `Send`

Ahora debería ver una respuesta `200 OK` y poder navegar hasta el final del esquema que creó para ver la identidad a través de la lente de la estructura JSON de XDM



![Descriptor de relación visible en el esquema de cuenta de cliente JSON](assets/view-schema-relationship-descriptor.png "Descriptor de relación")



![Descriptor de identidad de referencia visible en el esquema de cuenta de cliente JSON](assets/view-schema-reference-identity-descriptor.png "Descriptor de identidad de referencia")
