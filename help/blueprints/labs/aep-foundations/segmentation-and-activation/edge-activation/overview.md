---
title: Edge Activation
description: Descubra cómo difieren las velocidades de activación por lotes, streaming y Edge, y previsualice los pasos de laboratorio para crear un segmento Edge y configurar el reenvío de eventos.
doc-type: overview-page
solution: Experience Platform
exl-id: 9ecadff9-3838-4cd4-93b1-7c23a232f84c
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Edge Activation

## Resumen de velocidad de activación

Adobe tiene tres velocidades de activación pensadas para satisfacer diferentes necesidades:

1. Edge
1. Transmisión
1. Lote

Se explicará cómo activar mediante Adobe Edge con reenvío de eventos, audiencias de Edge y Edge Personalization. A continuación, se muestra cómo utilizar destinos de streaming desde el concentrador a Edge y a un destino externo.

>[!NOTE]
>
>No cubriremos la activación por lotes en este laboratorio. La activación por lotes se puede programar a diferentes intervalos y el tiempo hace que sea difícil mostrarla en un entorno de laboratorio sin tener al menos 3-24 horas.



## Lo que cubrirá el laboratorio

- Crear segmento de Edge
- Configuración del reenvío de eventos
- Envío de un evento de Edge
- Estos déclencheur
  - Segmento de Edge para calificar
  - Reenvío de eventos en Edge para enviar al webhook
