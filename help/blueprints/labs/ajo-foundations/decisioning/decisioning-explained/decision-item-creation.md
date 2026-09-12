---
title: Creación de elemento de decisión
description: Descubra cómo difieren los atributos de los elementos de decisión de la configuración de idoneidad, además de la protección a nivel de organización sobre los elementos de decisión y las impresiones en comparación con los eventos de decisión.
doc-type: article
solution: Experience Platform
exl-id: 28752ac1-118c-41d9-af6a-9907f854df1e
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Creación de elemento de decisión

## Objetivo de aprendizaje

Al final de esta lección, podrá hacer lo siguiente:

- Diferenciación entre los atributos de un elemento de decisión y su configuración de aceptación
- Indique la protección en los elementos de decisión por organización de IMS y por qué es de nivel de organización, no de zona protegida
- Distinguir una impresión de un evento de decisión
- Diferenciación entre las reglas de decisión y las audiencias por ámbito, momento y datos a los que cada una puede acceder

## Materiales necesarios

- 12 cartas (Jack, Reina, Rey de cada palo)
- 12 notas adhesivas, con nombres de atributos ya escritos en ellos de la lección anterior

## Conferencia

Esta es la lección más práctica hasta el momento: adjuntará una nota adhesiva a cada tarjeta y, a continuación, hará una pausa varias veces para escribir los valores de nivel, capacidad, visualización, cámara, prioridad e idoneidad a medida que se introduce cada concepto.

>[!VIDEO](https://video.tv.adobe.com/v/3502207/)

## Puntos clave

- Un elemento de decisión tiene dos mitades: atributos (nombre, descripción, atributos personalizados, etiquetas, prioridad) y elegibilidad (fechas, inclusión de regla de decisión, inclusión de audiencia, límite)
- Un cliente puede tener hasta 10 000 elementos de decisión; ese límite es por organización de IMS, no por zona protegida
- Las puntuaciones de prioridad más altas se devuelven primero
- Una regla de decisión es un ámbito condicional if/true para una sola campaña o recorrido, se evalúa en el momento de la decisión y puede utilizar atributos del elemento de decisión; una audiencia es un grupo más amplio de perfiles, se evalúa a la velocidad por lotes/flujo/Edge y no puede acceder a los atributos del elemento de decisión
- Utilice una regla de decisión en lugar de una audiencia cuando la idoneidad dependa de los atributos del propio elemento de decisión
- Un elemento de decisión puede transportar más de un déclencheur de límite (impresiones, clics, eventos de decisión, eventos personalizados) a la vez
- Una impresión cuenta cuando el elemento se visualiza realmente en el perímetro; un evento de decisión cuenta cada vez que la toma de decisiones evalúa y devuelve una respuesta, vista o no
- El límite se restablece diariamente, semanalmente o mensualmente a medianoche (GMT), no en la hora local
