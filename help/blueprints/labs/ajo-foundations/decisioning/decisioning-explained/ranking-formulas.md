---
hold: true
title: Clasificar fórmulas
description: Aprenda cómo las fórmulas de clasificación ajustan dinámicamente la puntuación de prioridad de un elemento de decisión por perfil mediante expresiones matemáticas condicionales.
doc-type: article
solution: Experience Platform
exl-id: 08183f1a-8db6-43c5-8b2e-05fa3d9c0f8d
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Clasificar fórmulas

## Objetivo de aprendizaje

Al final de esta lección, podrá hacer lo siguiente:

- Defina una fórmula de clasificación y explique lo que ajusta
- Explicar la estructura if/then de una regla de fórmula de clasificación
- Explique por qué cada configuración de fórmula de clasificación requiere una fórmula predeterminada
- Determinar el resultado cuando dos elementos de decisión aterrizan en la misma puntuación de prioridad ajustada

## Materiales necesarios

- 12 cartas (Jack, Reina, Rey de cada palo)
- 12 notas adhesivas, rellenas con el nombre del atributo y los valores de lecciones anteriores

## Conferencia

Esta lección incluye varias rondas de reordenación manual de las tarjetas, primero por prioridad original y después por dos fórmulas de clasificación diferentes aplicadas a perfiles de muestra diferentes, para que pueda ver cómo se reorganiza el mismo conjunto de elementos según quién lo pregunte.

>[!VIDEO](https://video.tv.adobe.com/v/3502209/)

## Puntos clave

- Una fórmula de clasificación ajusta dinámicamente la puntuación de prioridad de un elemento de decisión en función de cada perfil, según los atributos del perfil o el evento de experiencia de activación
- Las fórmulas admiten matemáticas básicas (sumar, restar, multiplicar, dividir) y pueden hacer referencia a la puntuación de prioridad original del elemento de decisión como variable
- La lógica de regla: si una condición sobre el perfil o la visita es verdadera, ajusta la prioridad de los elementos de decisión que cumplen determinados criterios de elemento
- Cada configuración de fórmula de clasificación necesita una fórmula predeterminada para los elementos de decisión que no afectan a ninguna regla de ajuste
- Cuando dos elementos de decisión se colocan en la misma puntuación de prioridad ajustada, la toma de decisiones los ordena aleatoriamente
