---
title: Definir relaciones
description: Descubra cómo los descriptores de relación vinculan un esquema de cliente a un esquema de búsqueda en el registro de esquemas XDM a través de la API.
doc-type: overview-page
solution: Experience Platform
exl-id: be672c84-09ac-4941-b40e-da7bd3fd6704
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Definir relaciones

## Descriptores de relaciones

Para crear una relación de un esquema a otro, debe crear un Descriptor de relación en el Registro de esquemas. Un cuerpo del descriptor de esquema de ejemplo tiene el siguiente aspecto:

Descriptor uno a uno

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:destinationSchema": "https://ns.adobe.com/devbc/schemas/6470f71181cf87aa39c2c2c43824eaa15f523652f7f88ff7",
  "xdm:destinationVersion": 1
}
```

Descriptor de identidad de referencia

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/6470f71181cf87aa39c2c2c43824eaa15f523652f7f88ff7",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:identityNamespace": "planID"
}
```

## Su objetivo

Crear identidades de relación para el esquema de cuenta de cliente. Después de realizar los pasos en la siguiente sección, el esquema debe tener el aspecto siguiente.

![Esquema de cuenta de cliente que muestra la relación y los descriptores de identidad de referencia](assets/overview-schema-with-relationship-identities.png)
