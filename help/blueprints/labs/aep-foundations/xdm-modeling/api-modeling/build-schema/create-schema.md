---
title: Crear esquema
description: Utilice la API del Registro de esquemas para ensamblar un esquema de cliente a partir de una clase de perfil y referencias de grupos de campos estándar y personalizados.
doc-type: article
solution: Experience Platform
exl-id: 78ebc5b8-d088-48e9-857f-87085a87a280
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# Crear esquema

## Modificación del cuerpo de la API

>[!CAUTION]
>
>**No ejecutar la llamada...aún**

1. Haga clic en la llamada de API `Step 4 - Create Customer Account Schema` en la carpeta `XDM Schema Lab -> Create Schema`.

   ![Paso 4: crear una llamada de API de esquema de cuenta de cliente en la colección de Postman](assets/create-schema-click-on-the-step-4-create-customer-account-schema.png)



2. Abra el cuerpo de la llamada y vea la estructura de cómo se define un esquema. Recuerde que un esquema siempre está compuesto por una sola (1) clase y uno o más grupos de campos.

3. Rellene los campos `title` y `description` del cuerpo del esquema con lo siguiente:

   - Título -> `Sample Customer Schema - <your sandbox number>`
   - Descripción -> `Sample Customer Schema - <your sandbox number>`

4. Rellene los campos de `$ref` con los `$ids` que guardó de las secciones de laboratorio anteriores que completó: [Crear grupos de campos personalizados](./create-custom-field-groups.md) y [Obtener clase de perfil](./get-profile-class.md). Debe tener $ids para cada uno de los elementos siguientes:

   - Clase -> Perfil individual XDM
   - Grupo de campos -> Detalles demográficos
   - Grupo de campos -> Datos de contacto personales
   - Grupo de campos -> Detalles de consentimiento y preferencia
   - Grupo de campos (personalizado) -> Detalles de cuenta de cliente

   ![Cuerpo de solicitud de esquema vacío antes de agregar referencias de clase y grupo de campos](assets/create-schema-empty-schema-api-body.png "Cuerpo de API de esquema vacío")



5. Revise el cuerpo final y asegúrese de que tenga un aspecto similar al siguiente

![Cuerpo de solicitud de esquema completado con título, descripción y todos los valores $ref rellenados](assets/create-schema-example-of-final-body-payload.png "Ejemplo de carga útil de cuerpo final")

>[!NOTE]
>
>El orden de `$refs` no importa ni la ubicación de `title` y `description` dentro del cuerpo.



## Ejecución de la API

1. Guarde las modificaciones realizadas en la solicitud de API antes de continuar.
1. Ejecute la API al hacer clic en el botón `Send`

Una respuesta correcta para crear el esquema debe generar un estado `201 Created` y debe parecerse a la imagen siguiente

>[!WARNING]
>
>No volver a ejecutar la solicitud si se ha realizado correctamente

![201 Se creó la respuesta después de crear correctamente el esquema mediante la API del paso 4](assets/create-schema-sample-response-from-executing-the-step-4-api.png "Respuesta de muestra al ejecutar la API del paso 4")


## Busque y guarde el esquema $id

1. Después de ejecutar la solicitud de API, copie `$id` y `$meta:altId` de la respuesta
1. Guarde los valores en algún lugar para poder reutilizarlos más adelante

>[!WARNING]
>
>No continúe hasta que haya guardado `$id` y `$meta:altId` en algún lugar.  Se requerirán en los pasos de laboratorio futuros

>[!TIP]
>
>**¡Felicitaciones! Acaba de crear un esquema usando solamente las API**
