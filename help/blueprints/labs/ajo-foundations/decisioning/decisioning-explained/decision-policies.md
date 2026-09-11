---
hold: true
title: Políticas de decisión
description: Descubra cómo las políticas de decisión aplican estrategias de selección a un canal de entrega y cómo los métodos de combinación individuales frente a agrupados cambian el orden de la oferta.
doc-type: article
solution: Experience Platform
exl-id: 21dc67fd-76ac-4b82-ae78-be024c7bfc55
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Políticas de decisión

## Objetivo de aprendizaje

Al final de esta lección, podrá hacer lo siguiente:

- Explicar qué configura una política de decisión y dónde se aplica
- Definir un paquete de decisión y lo que incluye
- Diferenciación de los métodos individuales y agrupados de combinación de múltiples estrategias de selección
- Explique cómo interactúa la restricción de frecuencia con el número de elementos de decisión que devuelve una directiva

## Materiales necesarios

- 12 cartas (Jack, Reina, Rey de cada palo)
- 13 notas adhesivas
  - 12 rellenadas con nombre de atributo y valores de lecciones anteriores
  - Una nueva nota adhesiva para rastrear las solicitudes

## Conferencia

Esta es la simulación más larga e involucrada en el curso. Simulará el comportamiento de la política de decisiones en vivo: hacer &quot;solicitudes&quot; repetidas, rastrear impresiones con límites de frecuencia y ver cómo las tarjetas abandonan y son reemplazadas. Luego, aplicará todo a un escenario comercial real comparando combinaciones de estrategia de selección individuales frente a agrupadas.

>[!VIDEO](https://video.tv.adobe.com/v/3502211/)

## Puntos clave

- Una directiva de decisión aplica estrategias de selección a un canal de entrega de AJO real, configurado en un nodo de canal de un recorrido o en la sección de canal de una campaña
- Una directiva puede utilizar ninguna, una o varias estrategias de selección; con ninguna, devuelve elementos por su puntuación de prioridad original, filtrados por los requisitos de nivel de elemento
- Una política de decisión más su canal de entrega juntos se denominan paquete de decisión: la configuración que se encuentra en el concentrador o perímetro
- Con una combinación individual, la colección de cada estrategia se ordena por separado y, a continuación, las listas se apilan; con agrupadas, todos los elementos se ordenan juntos en una lista y los duplicados utilizan la mayor de sus dos puntuaciones
- Las mismas entradas pueden producir pedidos finales muy diferentes en función de cada individuo o grupo
- El límite de frecuencia limita directamente la cantidad de elementos disponibles para devolver, por lo que debe planificar suficientes elementos de reserva sin límite para llenar cada ranura
