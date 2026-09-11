---
hold: true
title: Etiqueta
description: Etiquete tablas de Data Warehouse relacionales como clases de Perfil individual, Evento de experiencia o Búsqueda de XDM como parte de la metodología de LID.
doc-type: article
solution: Experience Platform
exl-id: 332ead7a-ca6e-4e30-bb35-8419c060c596
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Etiqueta

## Conferencia

En este vídeo, aprenderá a etiquetar tablas relacionales como una tabla de Perfil individual (P), Evento de experiencia (E) o Búsqueda (L) de XDM utilizando la Conexión 5G ERD como ejemplo.

>[!VIDEO](https://video.tv.adobe.com/v/3459087/?quality=12&learn=on)



## Detalles del laboratorio

Etiquete las tablas del ERD del almacén de datos de Connection 5G y del ERD de streaming con la etiqueta de clase XDM adecuada para las tablas de Perfil individual, Evento de experiencia y Búsqueda.

Tenga en cuenta lo siguiente al realizar el laboratorio:

- **Perfil individual (características) -** describe de forma exclusiva las características de una persona (por ejemplo: nombre, correo electrónico, dirección, preferencias, etc.)
- **Evento de experiencia (comportamientos):** describe las interacciones y los puntos de contacto que una persona tiene con una marca o compañía (por ejemplo, visitas a páginas web, compras, interacciones con centros de llamadas, envíos de aplicaciones, etc.)
- **Búsquedas (compatibles) -** proporcionan información contextual adicional para admitir el perfil individual o el evento de experiencia



## Paso 1. Etiquetado de tablas de perfil individuales de XDM

1. Identifique todas las tablas de origen que representan a una persona individual tanto en el ERD del almacén de datos del cliente como en el ERD de flujo del cliente.
1. Marque cada tabla con un &quot;**P**&quot; que indique que forma parte de la clase de perfil individual de XDM

>[!NOTE]
>
>Marcar solo las tablas que representan de forma exclusiva los rasgos de una persona individual



## Paso 2. Etiquetado de tablas de eventos de experiencia XDM

1. Identifique todas las tablas de origen que representan el comportamiento de una persona individual tanto en el ERD del almacén de datos de Connection 5G como en el ERD de streaming.
1. Marque cada tabla con un &quot;**E**&quot; que indique que forma parte de la clase de evento de experiencia XDM.

>[!NOTE]
>
>Marcar solo las tablas que representan de forma exclusiva el comportamiento de una persona individual



## Paso 3. Etiquetar tablas compatibles con XDM

1. Identifique todas las tablas de origen que representan datos de búsqueda y están directamente relacionadas con una tabla **&quot;P&quot;** o **&quot;E&quot;** que haya marcado en el ERD del almacén de datos de Connection 5G y en el ERD de streaming.
1. Marque cada tabla con **&quot;L&quot;**, lo que significa que forma parte de una clase XDM personalizada que no es de persona.

>[!NOTE]
>
>Las tablas de búsqueda solo pueden estar a 1 nivel de combinación o &quot;salto&quot; de una tabla con las etiquetas &quot;P&quot; o &quot;E&quot;



## Revisar

El siguiente vídeo revisa las etiquetas correctas para el almacén de Connection 5G y los ERD de flujo continuo, y explica por qué las tablas de cuenta de cliente, pedidos y extractos de facturación se etiquetaron tal cual.

>[!VIDEO](https://video.tv.adobe.com/v/3459081/?quality=12&learn=on)
