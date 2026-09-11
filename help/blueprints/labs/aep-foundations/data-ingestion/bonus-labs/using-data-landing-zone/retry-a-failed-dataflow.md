---
title: Reintento de un flujo de datos fallido
description: Vuelva a intentar una ejecución de flujo de datos fallida para que los datos de origen se vuelvan a procesar con reglas de asignación actualizadas en un nuevo flujo de datos.
doc-type: article
solution: Experience Platform
exl-id: 83ecf037-e524-4887-b833-5ed96af40419
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# Reintento de un flujo de datos fallido

Para reintentar un flujo de trabajo, haga lo siguiente:

1. Vaya a **Fuentes -> Flujos de datos -> \[Nombre del flujo de datos] -> \[Error al ejecutar]**
1. Resalte la ejecución del flujo de datos que no haya podido mostrar el carril derecho.
1. Haz clic en **Reintentar**. El reintento realizará la copia de los datos asociados con la ejecución fallida y ahora le aplicará las nuevas reglas de asignación

![Reintentando una ejecución de flujo de datos fallida desde el carril derecho](assets/retry-a-failed-dataflow.png)

>[!NOTE]
>
>Tenga en cuenta que cuando vuelve a intentar un flujo de datos fallido, se crea y ejecuta un nuevo flujo de datos. Aparecerá en la parte superior de la lista de flujos de datos
