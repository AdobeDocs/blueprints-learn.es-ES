---
title: Corregir errores de MAPPER para CreateDate
description: Solucione y resuelva un error de MAPPER causado por un valor createDate con formato incorrecto que se estaba transformando en un campo vacío.
doc-type: article
solution: Experience Platform
exl-id: e3f7ef23-6fd1-4f7a-8dc7-db82445322b0
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%
---

# Corregir errores de MAPPER para CreateDate

En este ejercicio, tendrá que averiguar cómo eliminar el error de MAPPER que vimos en el laboratorio de ingesta por lotes. El error debe corregirse porque, aunque createDate no es un campo obligatorio, los registros se siguen introduciendo porque la fecha con formato incorrecto se transforma en un campo vacío.

![valor createDate con un formato no válido que causa el error MAPPER](assets/fix-mapper-errors-for-createdate-invalid-format-mapper-error.png)
