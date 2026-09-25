---
title: Crear relación de esquema
description: Utilice la API del Registro de esquemas para crear un descriptor de relación uno a uno que vincule el esquema de cuenta de cliente a un esquema de plan de búsqueda.
doc-type: article
solution: Experience Platform
exl-id: c9079585-fff1-4ee1-8992-93825fcde759
source-git-commit: 96308d5726def849ef22540a5d13618017c40cc3
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%
---

# Crear relación de esquema

1. Haga clic en la solicitud de API `Step 2 - Relationship Descriptor Customer Account To Plan` en la carpeta `XDM Schema Lab -> Create Relationship Descriptors`

   >[!CAUTION]
   >
   >No ejecutar la solicitud...aún

   ![Paso 2 - Cuenta de cliente del descriptor de relación para planificar la solicitud de API](assets/create-schema-relationship-step-2-descriptor-request.png "Paso 2 - Cuenta de cliente del descriptor de relación para planificar")



2. Actualice las siguientes propiedades en el cuerpo de la llamada de API.

- Establezca el valor de la propiedad `xdm:sourceSchema` en `$id` del esquema de cuenta de cliente que guardó desde el paso de laboratorio [Crear esquema](../build-schema/create-schema.md)
- Establezca el valor de `xdm:sourceProperty` en la ruta de acceso del campo `planID` desde el Esquema de cuenta de cliente.
- Establezca el valor de la propiedad `xdm:destinationSchema` en el esquema `$id` de `dep: Lookup Plan` que guardó en el primer paso

>[!NOTE]
>
>Utilice el valor de notación de puntos del campo planId del esquema de cuenta de cliente y reemplace `.` por `/`
>
>
>No olvide el/la `/` inicial ni 😄

SOLO EJEMPLO

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:destinationSchema": "https://ns.adobe.com/devbc/schemas/6470f71181cf87aa39c2c2c43824eaa15f523652f7f88ff7"
,
  "xdm:destinationVersion": 1
}
```

>[!NOTE]
>
>Recuerde actualizar el nombre de inquilino anterior (\_devbc) con el suyo propio



1. Guarde la solicitud antes de seguir utilizando el botón `Save`

1. Ejecute la API al hacer clic en el botón `Send`

Ahora debería ver una respuesta de `201 Created` como la siguiente

![201 Se creó la respuesta después de crear la cuenta de cliente para el descriptor de relación del plan](assets/create-schema-relationship-customer-account-plan-descriptor.png "Cuenta de cliente - Descriptor de relación del plan")

>[!NOTE]
>
>Recuerde que el perfil del cliente en tiempo real (y todo Experience Platform) solo admite lo que llamamos una **unión de un (1) salto** desde el perfil individual de XDM o los esquemas de evento de experiencia de XDM (es decir, solo puede crear una (1) relación de búsqueda de nivel)

>[!NOTE]
>
>¿Se ha dado cuenta de que el descriptor de relación `@type` está establecido en un valor de `OneToOne`? ¿La relación entre la cuenta de cliente y la tabla de plan del XDM ERD en papel no es 1\:N?  ¿Qué está pasando?
>
>
>El perfil del cliente en tiempo real se ha creado para describir los rasgos y comportamientos de una persona individual.  Por lo tanto, desde el punto de vista de una persona individual, una tabla de búsqueda se define como **solo** **siempre** como una relación 1:1 durante la segmentación.
>
>Está bien si te duele el cerebro...
