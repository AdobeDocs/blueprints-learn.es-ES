---
title: 'Parte 1: Tipos de tablas restantes'
description: Identifique y etiquete tablas y tablas puente que requieran desnormalización en el Perfil individual, el Evento de experiencia y los ERD de búsqueda.
doc-type: article
solution: Experience Platform
exl-id: 742b58fa-3feb-4275-ab45-eb8d3aade22c
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---


# Parte 1: Tipos de tablas restantes

## Conferencia

En este vídeo aprenderá a etiquetar las tablas sin etiquetar restantes con un tipo de desnormalización de D o B, incluido cómo Bridge Table Rule #1 convierte el lado varios a uno de una tabla puente en una búsqueda.

>[!VIDEO](https://video.tv.adobe.com/v/3459082/?quality=12&learn=on)



## Detalles del laboratorio

Identificar y etiquetar tablas en el almacén de Connection 5G y transmitir los ERD que se ajustan a una de las categorías siguientes

- Tabla de Bridge (etiquetada como &quot;**B**&quot;)
- Nuevas tablas de búsqueda que existen debido a las tablas de puente
- Tablas que requerirán desnormalización (etiquetadas como &quot;**D**&quot;)

>[!CAUTION]
>
>El orden es muy importante aquí! Asegúrese de seguir los pasos en orden, ya que cada paso depende del anterior



## Paso 1: Identificar y etiquetar tablas de perfil individuales de XDM

1. Identifique todas las tablas directamente relacionadas con (a un salto de) las tablas de perfil individuales de XDM que aún no tengan una etiqueta. Márquelas con una estrella &quot;**\***&quot;.
1. Al mirar solo los esquemas que acaba de etiquetar con una estrella, realice las siguientes tareas:
   1. **Agregue una etiqueta &quot;B&quot; para la tabla puente**: una tabla se considera una tabla puente cuando dos o más tablas están relacionadas con ella con el lado varios de la relación de ambas tablas que apuntan a la tabla puente
   2. **Agregue una etiqueta &quot;D&quot; para que las tablas se desnormalicen**: cualquier entidad que tenga una cardinalidad 1\:M o M:1 con la tabla etiquetada Perfil individual XDM y que aún no esté marcada

>[!NOTE]
>
>Recuerde #1 de reglas de tablas de Bridge.
>
>Al encontrar una tabla puente directamente relacionada con una &quot;P&quot; o &quot;E&quot;, la relación M:1 actúa como una consulta. De lo contrario, siga las reglas de desnormalización estándar.



## Paso 2: Identificar y etiquetar tablas de eventos de experiencia XDM

1. Identifique todas las tablas directamente relacionadas con (a un salto de) el evento de experiencia etiquetado como tablas que aún no tienen una etiqueta. Márquelas con una estrella.
1. Al mirar solo las tablas que acaba de etiquetar con una estrella, realice las siguientes tareas:
   1. **Agregue una etiqueta &quot;B&quot; para las tablas puente**: una tabla se considera una tabla puente cuando dos o más tablas están relacionadas con ella con el lado varios de la relación que señala a la tabla puente
   2. **Agregue una etiqueta &quot;D&quot; para que las tablas se desnormalicen**: cualquier tabla que tenga una cardinalidad 1\:M o M:1 con el evento de experiencia XDM etiquetado como tabla y que aún no esté marcada

>[!NOTE]
>
>Recuerde #1 de reglas de tablas de Bridge.
>
>Al encontrar una tabla puente directamente relacionada con una &quot;P&quot; o &quot;E&quot;, la relación M:1 actúa como una consulta. De lo contrario, siga las reglas de desnormalización estándar.



## Paso 3: Identificar y etiquetar tablas de búsqueda

1. Identifique todas las tablas relacionadas con cualquiera de las tablas etiquetadas de búsqueda que aún no tengan una etiqueta (no importa cuántos saltos realice). Márquelas con una estrella &quot;**\***&quot;.
1. Al mirar solo las tablas que acaba de etiquetar con una estrella, realice las siguientes tareas:
   1. Agregue una etiqueta &quot;**B**&quot; para las tablas puente: una tabla se considera una tabla puente cuando dos o más tablas están relacionadas con ella con el lado varios de la relación que señala a la tabla puente
   2. Agregue una etiqueta &quot;**D**&quot; para que las tablas se desnormalicen: cualquier tabla que tenga una cardinalidad 1\:M o M:1 con una tabla de búsqueda o una tabla puente relacionada con una búsqueda

>[!NOTE]
>
>Recuerde #1 de reglas de tablas de Bridge.
>
>Al encontrar una tabla puente directamente relacionada con una &quot;P&quot; o &quot;E&quot;, la relación M:1 actúa como una consulta. De lo contrario, siga las reglas de desnormalización estándar **(hint, hint)**



## Revisar

El siguiente vídeo revisa las etiquetas D y B correctas para el almacén de Connection 5G y los ERD de flujo continuo, incluyendo por qué el tipo de producto es una tabla desnormalizada en lugar de una búsqueda.

>[!VIDEO](https://video.tv.adobe.com/v/3459064/?quality=12&learn=on)
