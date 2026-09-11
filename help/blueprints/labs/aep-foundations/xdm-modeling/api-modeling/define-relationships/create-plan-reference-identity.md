---
hold: true
title: Crear identidad de referencia del plan
description: Utilice la API del Registro de esquemas para crear un descriptor de identidad de referencia en el esquema de búsqueda para que se pueda utilizar en la segmentación por lotes.
doc-type: article
solution: Experience Platform
exl-id: b3b8f480-af3b-4bf8-b74e-3842f59691b6
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Crear identidad de referencia del plan

1. Haga clic en la solicitud de API `Step 3 - Reference Descriptor for Plan` en la carpeta `XDM Schema Lab -> Create Relationship Descriptors`

>[!CAUTION]
>
>No ejecutar la solicitud...aún

![Paso 3: descriptor de referencia para la solicitud de API de esquema de plan](assets/create-plan-reference-identity-step-3-descriptor-request.jpeg "Paso 3: descriptor de referencia para el esquema de plan")



2. Actualice las siguientes propiedades en el cuerpo de la llamada de API.

- Actualice el valor de la propiedad `xdm:sourceSchema` al `$id` del esquema `Customer Account` que guardó desde el paso [Crear esquema](../build-schema/create-schema.md)
- Actualizar el valor de `xdm:sourceProperty` a la ruta de acceso del campo `planID` desde el esquema `Customer Account`

>[!NOTE]
>
>Utilice el valor de notación de puntos del campo `planId` del esquema `dep: Lookup Plan` y reemplace `.` por `/`
>
>No olvide el/la `/` inicial ni 😄

SOLO EJEMPLO

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:identityNamespace": "planID"
}
```

>[!NOTE]
>
>Recuerde actualizar el nombre de inquilino anterior (\_devbc) con el suyo propio



3. Guarde la solicitud antes de seguir utilizando el botón `Save`

4. Ejecute la API al hacer clic en el botón `Send`

Ahora debería ver una respuesta de `201 Created` como la siguiente

![201 Se creó la respuesta después de crear el descriptor de identidad dep: Referencia de búsqueda de plan](assets/create-plan-reference-identity-dep-plan-descriptor-result.png "dep: Referencia de búsqueda de plan ")

>[!NOTE]
>
>Siempre se define un descriptor de identidad de referencia en el esquema de búsqueda (es decir, sourceSchema)

>[!NOTE]
>
>Los descriptores de identidad de referencia se crean automáticamente en el servidor al crear relaciones desde la interfaz de usuario del esquema. **Solo necesita crearlos explícitamente al utilizar las API para crear esquemas**

>[!TIP]
>
>¡Fantástico! Acaba de crear todos los descriptores necesarios para relacionar el esquema `dep: Lookup Plan` con el esquema `Customer Account` y permitir que se haga referencia a él durante la segmentación por lotes
