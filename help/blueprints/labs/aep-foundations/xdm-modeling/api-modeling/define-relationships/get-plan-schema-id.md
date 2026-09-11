---
title: Obtener ID de esquema de plan
description: Consulte la API del Registro del esquema de inquilinos para buscar y guardar el $id del esquema de búsqueda de Plan para utilizarlo en un descriptor de relación.
doc-type: article
solution: Experience Platform
exl-id: f66e0483-b5b3-4493-b752-c4e00211a8bd
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# Obtener ID de esquema de plan

## Enumerar todos los esquemas de inquilino

1. Haga clic en la solicitud de API `Step 1 - Get Lookup Schemas` en la carpeta `XDM Schema Lab -> Create Relationship Descriptors`
1. Ejecute la API al hacer clic en el botón `Send`

![Paso 1 - Obtener solicitud de API de esquemas de búsqueda](assets/get-plan-schema-id-step-1-get-lookup-schemas.jpeg "Paso 1 - Obtener esquemas de búsqueda")

>[!NOTE]
>
>Esta llamada de GET obtiene todos los esquemas que existen dentro de la parte de &quot;inquilino&quot; del registro de esquemas (es decir, esquemas creados personalizados). Solo necesitamos buscar el esquema **Plan** para poder relacionarlo con el esquema de cuenta de cliente.



## Identificación del esquema de plan

1. Busque el esquema `dep: Plan [Lookup] ` en la respuesta de llamadas
1. Copie el `$id` del esquema y guárdelo en algún lugar para referencia futura

![El dep: Esquema de búsqueda de plan $id ubicado en la respuesta de API](assets/get-plan-schema-id-dep-lookup-plan-schema-sid.png "dep: Esquema de plan de búsqueda $id")

>[!NOTE]
>
>Este esquema ya debe estar implementado previamente en su zona protegida

>[!WARNING]
>
>No continúe hasta que haya guardado `$id` del esquema en algún lugar.  Se requerirá más adelante para crear el Descriptor de relación
