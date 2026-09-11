---
hold: true
title: Configuración del reenvío de eventos
description: Descubra cómo el reenvío de eventos utiliza propiedades, elementos de datos, reglas y flujos de datos para reenviar eventos Edge a un extremo de terceros.
doc-type: overview-page
solution: Experience Platform
exl-id: da3d1c7f-3642-4de7-a297-fc36d09e7336
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Configuración del reenvío de eventos

El reenvío de eventos se encuentra en Edge y nos permite crear un conjunto de reglas y transformaciones ligeras para enviar eventos a cualquier punto de conexión.

En este paso vamos a reenviar todos los eventos que enviamos a la Edge a un webhook. El webhook actuará como un proxy para un tercero y nos permitirá ver lo que está sucediendo.

Para configurar esto, se debe configurar lo siguiente:

- Propiedad que contiene todas las extensiones, elementos de datos y reglas necesarias para decidir qué se reenvía y dónde
  - Un elemento de datos para hacer referencia al evento entrante o analizarlo en varios componentes individuales si es necesario
  - Una regla para añadir cualquier condición sobre qué reenviar, transformar la carga útil y dónde enviarla
- Flujo de datos que configura qué servicios lo utilizarán (por ejemplo, Reenvío de eventos y AEP)
  - Los datos enviados a estas secuencias de datos pueden realizar acciones según el servicio configurado (por ejemplo, reenviar un evento y enviar datos a un conjunto de datos)
