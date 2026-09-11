---
title: Ingesta por lotes
description: Cargue los datos de la cuenta del cliente mediante la ingesta por lotes en el lago de datos y el perfil, al tiempo que corrige los errores de asignación y calidad de datos.
doc-type: overview-page
solution: Experience Platform
exl-id: 76830e79-8fc0-4fda-98b1-2c1de19e8158
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Ingesta por lotes

## Objetivos de aprendizaje

En este ejercicio, cargará los datos de la cuenta del cliente desde un conector de origen basado en archivos a AEP Data Lake y, a continuación, a Profile. Aprenderá lo siguiente:

1. Explicación de las asignaciones de paso a través
1. Corrección de asignaciones de paso a través generadas por ML
1. Uso de la previsualización de datos de origen para comprobar cualquier problema de calidad de datos
1. Programación de una ejecución de flujo de datos
1. Tratamiento de errores derivados de valores faltantes en campos obligatorios
1. Tratamiento de errores derivados de errores de no coincidencia de tipos de datos
1. Tratamiento de errores de ingesta de datos y recuperación de dichos errores
1. Uso iterativo de datos de prueba para generar un conjunto de asignaciones completo.

>[!NOTE]
>
>Si no completó la creación del esquema de cuenta de cliente en los laboratorios anteriores, puede examinar el catálogo de esquemas y utilizar **dep: Cuenta de cliente** en su lugar
