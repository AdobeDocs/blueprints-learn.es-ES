---
hold: true
title: Desnormalizar
description: Aplique las reglas de desnormalización de la metodología LID para plegar las tablas puente y dependientes de un ERD de nuevo en su perfil principal, evento y tablas de consulta.
doc-type: article
solution: Experience Platform
exl-id: c98c9f58-03bc-4b28-becb-f84f3de04300
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# Desnormalizar

## Conferencia

En este vídeo aprenderá las tres reglas de desnormalización para volver a plegar las tablas de búsqueda y de puente en sus tablas principales, además de cómo los requisitos de personalización y segmentación de streaming afectan a esas decisiones.

>[!VIDEO](https://video.tv.adobe.com/v/3459083/?quality=12&learn=on)



## Detalles del laboratorio

>[!NOTE]
>
>Este laboratorio se centra únicamente en el almacén de conexión 5G ERD

## Reglas de desnormalización:

1. Cualquier tabla del modelo relacional etiquetada como &quot;**D**&quot; con una cardinalidad 1\:M o etiquetada como &quot;**B**&quot; se definirá como una matriz de objetos o un mapa en la tabla principal
1. Activado por el #1 de reglas, antes de desnormalizar las tablas &quot;**D**&quot; o &quot;**B**&quot; que actúan como matrices o mapas, debe interrogarlas para determinar la mejor manera de desnormalizarlas de nuevo en su tabla principal
1. Cualquier tabla del modelo relacional etiquetada como &quot;**D**&quot; con una cardinalidad de M:1 actuará como objeto o como lista de campos en su tabla principal

## Desnormalización de reglas de personalización:

Recuerde siempre revisar los casos de uso del cliente al crear el modelo de datos.  Tenga en cuenta lo siguiente:

- La segmentación de streaming no tiene acceso a las tablas de búsqueda en el momento de la evaluación
- Solo se puede acceder a los rasgos y las suscripciones a segmentos de un perfil para personalizar el contenido

![Casos de uso de Connection 5G considerados al aplicar la desnormalización para la personalización](assets/denormalize-connection-5g-use-cases.png "Casos de uso de Connection 5G")

>[!NOTE]
>
>¡Recuerde hacer referencia al Scenario.pdf de entrenamiento de Connection 5G durante este laboratorio!



## Paso 1: Rellene la tabla de perfil individual

1. Escriba en los campos que deben volver a desnormalizarse en la tabla Cuenta de cliente desde cualquier esquema &quot;**B**&quot; o &quot;**D**&quot; relacionado
1. Revisando los casos de uso anteriores, ¿qué campos adicionales se requieren para admitir la segmentación de flujo continuo y/o personalización? Agregue esos campos a la tabla



## Paso 2: Rellenado de las tablas de Evento de experiencia

1. Escriba en los campos que deben volver a desnormalizarse en las tablas Facturación y Pedidos desde cualquier tabla relacionada &quot;**B**&quot; o &quot;**D**&quot;
1. Revisando los casos de uso anteriores, ¿qué campos adicionales se requieren para admitir la segmentación de flujo continuo y/o personalización? Agregue esos campos a la tabla



## Paso 3: Rellenado de las tablas de búsqueda

1. Escriba en los campos que deben volver a desnormalizarse en la tabla de búsqueda de productos desde cualquier tabla relacionada de &quot;**B**&quot; o &quot;**D**&quot;
1. Revisando los casos de uso anteriores, ¿qué campos adicionales se requieren para admitir la segmentación de flujo continuo y/o personalización? Agregue esos campos a la tabla




## Revisar

El siguiente vídeo revisa cómo se desnormalizaron las tablas de Connection 5G en matrices y objetos, y cómo los casos de uso de adquisición y ampliación de venta requirieron volver a traer campos adicionales a las tablas principales de perfiles y eventos.

>[!VIDEO](https://video.tv.adobe.com/v/3459086/?quality=12&learn=on)
