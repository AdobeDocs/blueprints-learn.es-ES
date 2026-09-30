---
title: Ingesta de flujo
description: Cargue los datos de la cuenta del cliente mediante una fuente de flujo continuo en el lago de datos y el perfil utilizando una entrada de flujo y la API de REST.
doc-type: overview-page
solution: Experience Platform
exl-id: 973a9cac-dc9d-4c5f-87c3-16a55efd1314
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%
---

# Ingesta de flujo

## Objetivos de aprendizaje

En este ejercicio, cargaremos los datos de la cuenta del cliente desde una fuente de flujo continuo al lago de datos y al perfil de Adobe Experience Platform. ¿Con qué te vas después de tomar este laboratorio?

- Creación de una entrada de flujo
- Importando conjunto de asignaciones desde otro flujo de datos
- Obtención de ID de flujo de datos e ID de conjunto de datos desde la IU
- Uso de la API de REST para introducir un evento

>[!IMPORTANT]
>
>Complete la [configuración de Postman](../../setup.md) antes de iniciar este laboratorio.

>[!NOTE]
>
>Si no completó la creación del esquema Cuentas de cliente en los laboratorios anteriores, puede examinar el catálogo de esquemas y utilizar **dep: Cuenta de cliente** en su lugar
