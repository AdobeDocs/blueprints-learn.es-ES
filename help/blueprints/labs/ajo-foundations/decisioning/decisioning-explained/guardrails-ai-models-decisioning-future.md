---
hold: true
title: Protecciones, modelos de IA y el futuro de la toma de decisiones
description: Conozca las protecciones clave de la toma de decisiones, cómo difieren los modelos de clasificación de IA de las fórmulas y cómo los componentes básicos de la toma de decisiones conectan de extremo a extremo.
doc-type: article
solution: Experience Platform
exl-id: 90902f6e-ba3c-4852-ab82-ad852698b227
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Protecciones, modelos de IA y el futuro de la toma de decisiones

## Objetivo de aprendizaje

Al final de esta lección, podrá hacer lo siguiente:

- Recuerde las dos barreras que se encuentran con más frecuencia en la práctica
- Diferenciación entre la optimización automática y los modelos de IA de optimización personalizados
- Explique cómo la toma de decisiones se extiende más allá del producto ODE heredado
- Resumir cómo los ocho bloques de construcción encajan de un extremo a otro

## Conferencia

El siguiente vídeo trata sobre las dos protecciones de toma de decisiones más comunes, cómo difieren los modelos de clasificación de IA de las fórmulas de clasificación manuales, cómo se extiende la toma de decisiones más allá del motor de Offer Decisioning heredado y un resumen de cómo se conectan de extremo a extremo los ocho componentes básicos.

>[!VIDEO](https://video.tv.adobe.com/v/3502212/)

## Puntos clave

- Las dos protecciones más visitadas: 10 000 elementos de decisión por organización de IMS (no por zona protegida) y 100 atributos personalizados por esquema; compruebe la documentación del producto para ver los números actuales, ya que están sujetos a cambios
- Los modelos de IA se pueden utilizar dentro de fórmulas de clasificación; la optimización automática no está personalizada y optimiza el rendimiento global, mientras que la optimización personalizada proporciona elementos hacia objetivos comerciales específicos por perfil
- Las puntuaciones de modelo calculadas fuera de AEP se pueden introducir como atributos de perfil y utilizar en reglas de idoneidad o fórmulas de clasificación
- La toma de decisiones va más allá del motor de Offer Decisioning heredado: utiliza XDM para la reutilización, envía JSON a aplicaciones sin encabezado y separa el elemento de decisión del tratamiento
- La toma de decisiones puede condicionar las rutas de recorrido y la prioridad de entrada a una respuesta de toma de decisiones
- Fin a fin: el XDM del elemento de decisión define atributos → la creación del elemento de decisión asigna valores y elegibilidad → colecciones elementos de grupo → fórmulas de clasificación ajustan la prioridad por perfil → estrategias de selección clasifican y filtran una colección → políticas de decisión aplican estrategias a un canal → paquetes de decisión activos en el centro o en el perímetro
