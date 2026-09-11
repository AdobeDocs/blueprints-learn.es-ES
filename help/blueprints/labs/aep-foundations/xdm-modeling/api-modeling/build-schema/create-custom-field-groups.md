---
hold: true
title: Crear grupos de campos personalizados
description: Utilice la API del registro de esquema para crear un grupo de campos Detalles de cuenta del cliente personalizado y guardar su $id para utilizarlo en un esquema posterior.
doc-type: article
solution: Experience Platform
exl-id: d3262db9-7c0b-476a-843f-1a2c224ee792
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Crear grupos de campos personalizados

## Estructura del grupo de campos

Un grupo de campos siempre está compuesto por los siguientes campos. Esto se ve en la solicitud de en el siguiente paso.

| Valores requeridos | Descripción |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| title | El nombre del grupo de campos que desea crear en el registro de esquema. Observe que el nombre DEBE SER ÚNICO. |
| description | Breve descripción sobre el propósito del grupo de campos |
| type | Siempre es un objeto |
| meta\:intendedToExtend | Define con qué clases se puede utilizar el grupo de campos. Siempre se hace referencia a las clases por su valor `$id` |
| allOf | Describe los recursos que se pueden incluir en el grupo de campos. Para los campos definidos personalizados la ruta siempre es `#/definitions/customFields` |
| definitions.customFields... | Esta es la estructura de esquema JSON predeterminada necesaria para crear grupos de campos personalizados. Debe coincidir con el `allOf` de arriba |
| \&lt;TENANT\_NAME> | El nombre del inquilino (es decir, un nombre único) se crea durante el proceso de aprovisionamiento. Esto garantiza que las personalizaciones realizadas no entren en conflicto con los cambios existentes o futuros del Registro del esquema de Adobe |



## Crear grupo de campos Detalles de cuenta de cliente

1. Haga clic en la llamada de API `Step 2 - Create Customer Account Details Field Group` de la solicitud en la carpeta `XDM Schema Lab -> Create Schema`



![Paso 2 - Crear solicitud de API del grupo de campos Detalles de cuenta de cliente](assets/create-custom-field-groups-step-2-field-group-request.png "Paso 2 - Crear grupo de campos Detalles de cuenta de cliente")



Revise el cuerpo de la solicitud antes de ejecutarla. Tenga en cuenta que los campos obligatorios mencionados en la sección Estructura del grupo de campos aparecen así:

![Campos requeridos de un grupo de campos personalizados como se muestra en el cuerpo de la solicitud](assets/create-custom-field-groups-field-group-structure.png "Estructura del grupo de campos")



![La propiedad allOf que hace referencia a la ruta de definiciones de campo personalizado](assets/create-custom-field-groups-field-group-structure-allof.png "Estructura de grupo de campos allOf")

>[!NOTE]
>
>Observe cómo en la imagen de la derecha encima de `allOf` se hace referencia a la ruta de &quot;/definitions/customFields&quot;.  Debe coincidir con la estructura definida en el esquema (imagen de la izquierda), ya que indica al sistema XDM dónde localizar los objetos creados personalizados.
>
>![Comparación que resalta cómo la ruta allOf debe coincidir con la ruta de definiciones de campo personalizado](assets/create-custom-field-groups-allof-path-highlighted.png)



Observe también cómo cada campo específico de la hoja de asignación se corrobora dentro de la estructura JSON de XDM.



![Asignación de notación de puntos de plan de hoja convertida a estructura JSON de XDM](assets/create-custom-field-groups-plan-dot-notation-to-xdm-json.png "Planificación de notación de puntos a JSON de XDM")



![Asignación de notación de puntos de cuenta de hoja y de ID de cliente convertida a XDM](assets/create-custom-field-groups-account-customer-id-dot-notation-to-xdm.png "Notación de puntos de ID de cuenta y cliente a XDM")



2. Actualice `title` y `description` para el grupo de campos con el siguiente formato: `Customer Account Details - Sandbox <your number here>`



![Ejemplo de título y descripción rellenados para el grupo de campos personalizados](assets/create-custom-field-groups-field-group-title-description-example.png "Ejemplo de título y descripción del grupo de campos")



3. Ejecute haciendo clic en el botón `Send`.  Debería ver una respuesta similar a la captura de pantalla siguiente.

4. Copie el valor `$id` del grupo de campos Detalles de cuenta de cliente recién creado.

![Respuesta correcta de la API después de crear el grupo de campos personalizados](assets/create-custom-field-groups-step-2-create-custom-field-group-success.png "Paso 2 - Éxito al crear un grupo de campos personalizados")

>[!WARNING]
>
>No continúe hasta que haya guardado `$id` en algún lugar.  Se requerirá más adelante para crear el esquema de cuenta de cliente
>
>
