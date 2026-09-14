---
title: Crear identidad principal
description: Utilice la API del Registro de esquemas para crear un descriptor de identidad customerID principal para el esquema de cuenta de cliente.
doc-type: article
solution: Experience Platform
exl-id: db690081-e857-4875-8bb9-7ac197d73cab
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%
---

# Crear identidad principal

1. Haga clic en la solicitud de API `Step 1 - Create Primary Identity for Customer Account Schema` en la carpeta `XDM Schema Lab -> Create Identity Descriptors`

   ![Paso 1 - Crear identidad principal para la solicitud Postman del esquema de cuenta de cliente](assets/create-primary-identity-step-1-postman-request.jpeg "Paso 1 - Crear identidad principal para el esquema de cuenta de cliente")

   >[!CAUTION]
   >
   >Aún no ejecute la solicitud



1. Actualice el valor `xdm:sourceSchema` en el cuerpo de la solicitud utilizando el `$id` que guardó desde el paso de laboratorio [Crear esquema](../build-schema/create-schema.md)

1. Actualizar el valor `xdm:isPrimary` en el cuerpo de la solicitud a `true`

   SOLO EJEMPLO

   ```json
   {
     "@type": "xdm:descriptorIdentity",
     "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
     "xdm:sourceVersion": 1,
     "xdm:sourceProperty": "/_devbc/customerID",
     "xdm:namespace": "customerID",
     "xdm:property": "xdm:code",
     "xdm:isPrimary": true
   }
   ```

   >[!NOTE]
   >
   >Recuerde actualizar el nombre de inquilino anterior (\_devbc) con el suyo propio



1. Guarde la solicitud antes de seguir utilizando el botón `Save`

1. Ejecute la API al hacer clic en el botón `Send`. Ahora verá una respuesta `201 Created` como se muestra a continuación

![201 Se creó la respuesta después de crear correctamente el descriptor de identidad principal](assets/create-primary-identity-201-created-response.png "Se creó correctamente el descriptor de identidad principal")

>[!SUCCESS]
>
>¡Felicidades!  Ha creado un descriptor de identidad principal en el esquema
