---
title: Crear otras identidades
description: Utilice la API del Registro de esquemas para crear un descriptor de identidad de dirección de correo electrónico no principal para el esquema de cuenta de cliente.
doc-type: article
solution: Experience Platform
exl-id: 22c40299-fb93-4d41-a23b-f8629df3e7b9
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Crear otras identidades

1. Haga clic en la llamada de API `Step 2 - Create Email Address Identity for Customer Account Schema` en la carpeta `XDM Schema Lab -> Create Identity Descriptors`

   >[!CAUTION]
   >
   >No ejecutar la solicitud...aún

   ![Paso 2 - Crear una identidad de dirección de correo electrónico para la solicitud Postman de esquema de cuenta de cliente](assets/create-other-identities-step-2-postman-request.jpeg "Paso 2 - Crear un descriptor de identidad de dirección de correo electrónico")



1. Actualice el valor `xdm:sourceSchema` en el cuerpo de la solicitud utilizando el `$id` que guardó desde el paso de laboratorio [Crear esquema](../build-schema/create-schema.md)

1. Actualizar el valor `xdm:isPrimary` en el cuerpo de la solicitud a `false`

   SOLO EJEMPLO

   ```json
   {
     "@type": "xdm:descriptorIdentity",
     "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
     "xdm:sourceVersion": 1,
     "xdm:sourceProperty": "/personalEmail/address",
     "xdm:namespace": "Email",
     "xdm:property": "xdm:code",
     "xdm:isPrimary": false
   }
   ```

   >[!NOTE]
   >
   >Recuerde actualizar el nombre de inquilino anterior (\_devbc) con el suyo propio



1. Guarde la solicitud antes de seguir utilizando el botón `Save`

1. Ejecute la API al hacer clic en el botón `Send`. Ahora debería ver una respuesta de `201 Created` como la siguiente

![201 Se creó la respuesta después de crear correctamente el descriptor de identidad de la dirección de correo electrónico](assets/create-other-identities-201-created-response.png "Descriptor de identidad correcto para la dirección de correo electrónico")
