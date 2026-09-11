---
hold: true
title: Marcar campos de identidad
description: Descubra cómo los descriptores de identidad marcan los campos de esquema como identidades principales o no principales mediante la API del Registro de esquemas XDM.
doc-type: overview-page
solution: Experience Platform
exl-id: f6498584-0f4d-4baf-86b5-b00cc78e2ba7
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Marcar campos de identidad

## Descriptores de identidad

Para marcar un campo como identidad, debe crear un descriptor de identidad en el registro de esquemas. Un cuerpo del descriptor de esquema de ejemplo tiene el siguiente aspecto:

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

- **@type** -> siempre se establece en `xdm:descriptorIdentity`
- **xdm\:sourceSchema** -> `$id` del esquema donde existe el campo
- **xdm\:sourceVersion** -> siempre 1
- **xdm\:sourceProperty** -> ruta del campo dentro del esquema
- **xdm\:namespace** -> el código del área de nombres de identidad donde se debe almacenar el campo
- **xdm\:property** -> siempre `xdm:code`
- **xdm\:isPrimary** -> si es una identidad principal, entonces `true` si no es `false`


## Su objetivo

Cree identidades principales y no principales para el esquema de cuentas de cliente. Después de realizar los pasos en la siguiente sección, el esquema debe tener el aspecto siguiente.

![Esquema de cuenta de cliente después de crear descriptores de identidad principales y no principales](assets/overview-schema-with-primary-and-non-primary-identities.png)
