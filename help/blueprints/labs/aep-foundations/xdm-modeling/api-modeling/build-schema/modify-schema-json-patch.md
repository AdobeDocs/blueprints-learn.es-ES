---
title: 'Modificar esquema: parche de JSON'
description: Utilice una llamada a la API de PATCH de JSON para agregar un nuevo campo a un grupo de campos de inquilino existente y ver el cambio reflejado en el esquema.
doc-type: article
solution: Experience Platform
exl-id: c0313594-d998-4525-a0a4-d9d844bed5ef
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%
---

# Modificar esquema: parche de JSON

## Información general

Supongamos que después de crear el esquema, necesita agregar un campo adicional al objeto `plan` llamado `planDescription`. Esta necesidad puede surgir porque se olvidó de agregarlo cuando creó el esquema o porque fue una solicitud que se produjo meses después. Para realizar esta tarea, ejecute una operación `PATCH` que actualice el esquema con el nuevo campo.

Obtenga más información acerca de JSON PATCH en los siguientes vínculos. Para este laboratorio, supongamos que tiene una comprensión general de cómo funciona.

- [https://jsonpatch.com/](https://jsonpatch.com/)
- [Aspectos básicos de API Experience League](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-fundamentals.html?lang=en#json-patch)

![Diagrama de aplicación de parches a un campo planDescription que falta en un esquema existente](assets/modify-schema-json-patch-patching-missing-plan-description-field.png "Aplicación de parches a un campo que falta Descripción del plan")

>[!NOTE]
>
>Recuerde los siguientes puntos:
>
>- Un esquema está compuesto por una clase y uno o más grupos de campos
>- Debe agregar nuevos campos a un grupo de campos antes de agregarlos a un esquema. Esta restricción garantiza la reutilización de un campo en cualquier esquema que utilice ese grupo de campos.



Para agregar un nuevo campo a un esquema, debe realizar las siguientes operaciones en orden. Este proceso es lo que se hace en los siguientes pasos del laboratorio.

- Identifique el grupo de campos al que desee agregar la nueva propiedad
- Construya una llamada de PATCH JSON para actualizar el grupo de campos
- Ejecute la llamada PATCH de JSON para actualizar el grupo de campos (que hereda el esquema)



## Busque e identifique el grupo de campos que desea actualizar

1. Seleccione la llamada API `Step 1 - Get Tenant Field groups` ubicada en la carpeta `XDM Schema Lab -> Customize Schema`
1. Ejecute la solicitud haciendo clic en el botón `Send`

   ![Paso 1 - Obtener solicitud de API de grupos de campos de inquilino](assets/modify-schema-json-patch-step-1-get-tenant-field-groups.png "Paso 1 - Obtener grupos de campos de inquilino")

   >[!NOTE]
   >
   >Recuerde que creó el objeto `plan` dentro de un grupo de campos personalizados. Los objetos creados a medida en el registro de esquema XDM se denominan &quot;tenant&quot;, de ahí que la llamada API utilice la ruta `/schemaregistry/tenant/mixins/`.



1. En la respuesta, busque el ID de esquema para el grupo de campos personalizados que creó anteriormente con el título `Customer Account Details - Sandbox <your number here> `

1. Copie `$meta:altId` y guárdelo en un lugar seguro, ya que lo necesita para el siguiente paso

![Localizando el grupo de campos Detalles de cuenta de cliente personalizada en la respuesta de API](assets/modify-schema-json-patch-search-field-group-response.jpeg "Busque la respuesta correspondiente al grupo de campos Detalles de cuenta de cliente")

>[!CAUTION]
>
>Asegúrese de seleccionar el grupo de campos correcto que desea copiar. No utilice el grupo de campos con nombre similar denominado `dep: Customer Account Details`

>[!WARNING]
>
>Necesita `$meta:altId` para realizar los pasos de laboratorio futuros, así que guárdelo en algún lugar antes de continuar



## Buscar el grupo de campos por $meta\:altId

1. Seleccione la llamada API `Step 2 - Fetch path for the object to be modified` en la carpeta `XDM Schema Lab -> Customize Schema`
1. En la dirección URL de la solicitud, reemplace `<replace me>` por el `$meta:altId` que guardó desde el paso de sección anterior hasta el final de la llamada, como se muestra a continuación
1. Guarde las ediciones que ha realizado en la solicitud
1. Ejecute la solicitud haciendo clic en el botón `Send`

![Paso 2 - Ruta de acceso de búsqueda para la llamada API al objeto que se va a modificar](assets/modify-schema-json-patch-step-2-fetch-object-path.jpeg "Paso 2 - Ruta de acceso de búsqueda para los pasos del objeto que se va a modificar")



Revise la respuesta y observe que la ruta del puntero JSON para el objeto **plan** se construye utilizando cada una de las propiedades resaltadas a continuación.

![Propiedades resaltadas que componen la ruta del puntero JSON al objeto de plan](assets/modify-schema-json-patch-customer-account-details-path-to-the-plan-object.png "Ruta de detalles de cuenta del cliente al objeto de plan")



La ruta totalmente compuesta tiene el aspecto que se muestra a continuación.  Copie esta ruta y guarde en algún lugar para referencia

```none
/definitions/customFields/properties/_devbc/properties/plan/properties
```

>[!NOTE]
>
>Recuerde actualizar el nombre de inquilino anterior (\_devbc) con el suyo propio



## PATCH en el grupo de campos

### Muestra del cuerpo de la API de PATCH JSON

```none
[
    {
        "op": "",
        "path": "",
        "value": {
            "title": "",
            "type": "",
            "description": ""
        }
    }
]
```

- **op (Operación)** -> proporciona instrucciones sobre qué acción debe realizar PATCH
- **Ruta** -> esta es la ruta que desea crear, actualizar o eliminar (es decir, el puntero JSON a la ubicación del nuevo campo)
- **Valor** -> este es un campo opcional y solo se usa al crear o reemplazar un campo existente



### Ejecución de la solicitud de API

1. Haga clic en la llamada de API `Step 3 - Modify Tenant Field group` en la carpeta `XDM Schema Lab -> Customize Schema`

   ![Paso 3 - Modificar llamada de API del grupo de campos de inquilino](assets/modify-schema-json-patch-step-3-modify-tenant-field-group.png "Paso 3 - Modificar grupo de campos de inquilino")



2. Actualice el cuerpo de la solicitud con la siguiente información

   - **op** ->` add`
   - **ruta** -> `path from previous step +`` the new field name`
   - **valor** ->
     - **título** -> `Plan Description`
     - **tipo** -> `string`
     - **descripción** -> `High-level details about the plan`

   Cuando haya terminado, la solicitud de API debería tener un aspecto similar al siguiente

   ![Cuerpo de solicitud JSON PATCH completado que agrega el campo planDescription](assets/modify-schema-json-patch-step-3-final-call-example.png "Paso 3 - Ejemplo de llamada final")

   >[!WARNING]
   >
   >Asegúrese de incluir el nuevo nombre de campo **planDescription** en la ruta de acceso



3. Si todo se ve bien `Save`, su llamada

4. `Execute` llamó a para realizar el PATCH

Verá una respuesta `200 OK` y el campo `planDescription` en el grupo de campos, de esta manera:

![200 OK respuesta después de aplicar correctamente parches al grupo de campos con planDescription](assets/modify-schema-json-patch-step-3-200-ok-successful-patch.png "Paso 3 - 200 OK Correcto PATCH")

>[!SUCCESS]
>
>¡Felicidades! Ha actualizado correctamente un grupo/esquema de campos mediante JSON PATCH



## Vea el cambio en la interfaz de usuario

Examine el esquema a través de la interfaz de usuario y vea el campo recién agregado.

![Campo de descripción del plan visible en el esquema después del parche JSON en la interfaz de usuario de Experience Platform](assets/modify-schema-json-patch-plan-description-added-to-field-group.png "Descripción del plan agregada al grupo de campos Detalles de cuenta de cliente - Zona protegida \&lt;su número>. Modificar el esquema JSON")
