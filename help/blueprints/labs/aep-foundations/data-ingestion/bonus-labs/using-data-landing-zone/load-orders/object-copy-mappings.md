---
title: Asignaciones de copia de objeto
description: Configure las asignaciones de copia de objetos para una matriz de productos y, a continuación, agregue y elimine las invalidaciones de nivel de campo encima de la copia predeterminada.
doc-type: article
solution: Experience Platform
exl-id: 762d0e19-ed1c-4f4d-91ec-a962bd6277a7
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# Asignaciones de copia de objeto

En esta sección, agregará las asignaciones de copia de objetos y creará algunas invalidaciones.

## Asignaciones de paso a través

Agregue las siguientes asignaciones de paso a través con **productos\[\*]** y **productos\[\*].productID** haciendo clic en Nuevo tipo de campo y agregue un nuevo campo para cada fila aquí. Es posible que algunos ya estén presentes debido a las recomendaciones ML.

| Columna Source | Columna XDM |
| ----------------------- | ------------------------- |
| orderStatus | eventType |
| lastOrderStatusUpdate | timestamp |
| productos\[\*] | productListItems\[\*] |
| products\[\*].productID | productListItems\[\*].SKU |

>[!NOTE]
>
>Tenga en cuenta que **products\[\*]** está realizando una asignación de campo 1-1 entre los campos de objeto y la asignación de campo explícita **products\[\*].productID** está anulando la copia predeterminada.

>[!NOTE]
>
>**products\[\*].productID** también está asignado a **productListItems\[\*].SKU** además de a **productListItems\[\*].\_id**. Este es un ejemplo de campo de entrada único que se asigna a varios campos de salida en el esquema XDM. Mantenga la asignación tal cual.

1. Mantener la asignación de **productos\[\*].price** a **productListItems\[\*].priceTotal**

## Agregar invalidaciones en determinados campos

1. Omitir las asignaciones de copia de objetos por
   1. Asignando **productos\[\*].make** a **productListItems\[\*].\_devbc.make**
   2. Asignando **productos\[\*].model** a **productListItems\[\*].\_devbc.model**

## Eliminar invalidaciones en determinados campos

1. Observe que **productListItems.currencyCode** y **productListItems.quantity** se rellenan automáticamente.
1. Elimine las asignaciones **productListItems\[\*].quantity** y **productListItems\[\*].currencyCode**.
1. Las anulaciones no se producen y la copia del objeto se hace cargo cuando los campos de acceso directo pasan por ellas.


## Resumen de asignaciones, anulaciones y eliminaciones de copias de objetos

| Columna Source | Columna XDM | Acción |
| -------------------------- | ----------------------------------- | -------------------------------------- |
| productos\[\*] | productListItems\[\*] | `Add` |
| products\[\*].productID | productListItems\[\*].SKU | `Add` |
| products\[\*].productID | productListItems\[\*].\_id | `No change` |
| products\[\*].make | productListItems\[\*].\_devbc.make | `Change` |
| products\[\*].model | productListItems\[\*].\_devbc.model | `Change` |
| products\[\*].price | productListItems\[\*].priceTotal | `No change` |
| products\[\*].quantity | productListItems\[\*].quantity | `Remove` |
| products\[\*].currencyCode | productListItems\[\*].currencyCode | `Remove` |

## Verificar asignaciones

Debe comprobar dos conjuntos de asignaciones. En total, debe tener 6 asignaciones después de la eliminación de 2.



![Las asignaciones resultantes para productListItems después de agregar las invalidaciones de copia de objeto](assets/object-copy-mappings-resultant-mappings-for-productlistitems.png "Las asignaciones resultantes para ProductListItems\[*] deben tener este aspecto")

![Segunda vista de las asignaciones resultantes para productListItems después de invalidar la copia de objeto](assets/object-copy-mappings-resultant-mappings-for-productlistitems--2.png)
