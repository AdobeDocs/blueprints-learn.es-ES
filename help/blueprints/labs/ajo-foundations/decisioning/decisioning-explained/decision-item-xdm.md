---
hold: true
title: XDM del elemento de decisión
description: Conozca el esquema XDM generado previamente que comparte cada elemento de decisión y cómo los atributos personalizados están anidados en un área de nombres de inquilino.
doc-type: article
solution: Experience Platform
exl-id: c42503a2-24e7-4a5d-98bf-38c16fe69733
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# XDM del elemento de decisión

## Objetivo de aprendizaje

Al final de esta lección, podrá hacer lo siguiente:

- Identifique el esquema XDM creado previamente y utilizado para cada elemento de decisión
- Explique dónde residen los atributos personalizados dentro del esquema y el límite que se les aplica
- Reconocer cómo la anidación de atributos en un objeto principal admite la reutilización

## Materiales necesarios

- bloc de al menos 12 notas adhesivas (más en caso de que cometas errores)

## Conferencia

A lo largo del vídeo, hará una pausa para escribir cuatro nombres de atributos en la parte superior de las 12 notas adhesivas; rellenará los valores reales en la siguiente lección.

>[!VIDEO](https://video.tv.adobe.com/v/3502206/)

## Puntos clave

- Cada elemento de decisión utiliza el mismo esquema generado previamente: elementos de oferta personalizados: experience decisioning
- Todo lo que hay bajo el nodo \_experience es obligatorio para el sistema y no se puede editar
- Los atributos personalizados se encuentran en el área de nombres de inquilino de su organización y tienen un límite de 100 por esquema
- Solo hay un esquema para cada elemento de decisión: sin duplicados ni versiones alternativas
