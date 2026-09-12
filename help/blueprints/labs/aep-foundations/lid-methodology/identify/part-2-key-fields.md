---
title: 'Parte 2: Campos clave'
description: Identifique los campos de identidad principal, de persona y de relación, además de los campos de Evento de experiencia requeridos, en las tablas etiquetadas como ERD.
doc-type: article
solution: Experience Platform
exl-id: 24b6fdbd-0d59-4fe7-828e-c4bc7036db90
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 0%

---


# Parte 2: Campos clave

## Conferencia

En este vídeo aprenderá a identificar la identidad principal, las identidades de persona y las identidades de relación en cada tabla, además de los campos requeridos _id, marca de tiempo y tipo de evento para los eventos de experiencia.

>[!VIDEO](https://video.tv.adobe.com/v/3459085/?quality=12&learn=on)



## Detalles del laboratorio

### Campos de identidad

- **Identidad de persona**: se usa para identificar a una persona de forma exclusiva. Solo se utilizan en tablas de entidad principal. Debe haber al menos uno de ellos, pero puede haber más de uno.
- **Identidad de relación (es decir, no persona)**: se usa para describir relaciones desde las tablas de entidad principal del perfil del cliente en tiempo real a una clase de entidad auxiliar asociada (es decir, búsquedas).
- **Identidad principal**: puede ser una identidad de persona o una identidad de relación (no persona) que se esté usando como clave de almacenamiento y que se requiera para cualquier esquema que esté usando el perfil del cliente en tiempo real. En las tablas de entidad principal, la identidad también identifica de forma exclusiva a una persona. Cuando se especifica para esquemas de perfil XDM y esquemas de búsqueda, este campo determina si se crea un registro nuevo o se actualiza uno existente. Debe haber exactamente uno de estos.

### Campos obligatorios (solo evento de experiencia XDM)

- **\_id**: utilizado por el perfil del cliente en tiempo real junto con la identidad principal para crear una clave de almacenamiento única para el evento. Necesario para evitar la duplicación accidental de datos de evento dentro del servicio de perfil
- **Marca de tiempo**: todos los eventos se producen a una hora específica y, por lo tanto, todos los eventos requieren una marca de tiempo

No es necesario, pero se recomienda encarecidamente:

- **Tipo de evento**: describe el comportamiento de alto nivel de los datos de evento (es decir, compras, reservas, etc.)

### Reglas generales

1. #2 de reglas de tablas de Bridge: en situaciones en las que existe una tabla puente entre un elemento principal &quot;**P**&quot; o &quot;**E**&quot; (es decir, una tabla principal) y una tabla &quot;**L**&quot;, la tabla puente se considera parte de la tabla principal
1. Valide siempre que las identidades sean únicas para una persona **soltera** en este momento para evitar que se repita el trabajo durante la ingesta de datos
1. Para esquemas de Experience Event, la identidad principal es la que identifica de forma exclusiva ese comportamiento para una sola persona.
1. En las tablas de búsqueda, la clave principal (PK) del modelo relacional siempre será la identidad principal no personal

Para cada tabla del ERD de Connection 5G Warehouse y del ERD de flujo continuo que haya etiquetado como **&quot;P&quot;, &quot;E&quot; o &quot;L&quot;,** ahora debe realizar los pasos siguientes para identificar las identidades principales, las identidades de persona, las identidades de relación y cualquier campo requerido para las clases de esquema dadas.

>[!NOTE]
>
>Consulte el diagrama siguiente durante los laboratorios para etiquetar identidades en esquemas
>
>![Diagrama que muestra ejemplos de etiquetas de identidad principal, identidad de persona e identidad de relación aplicadas a tablas ERD](assets/part-2-key-fields-identity-labeling-diagram.png)



## Paso 1: Etiquetado de campos clave en las tablas de Perfil individual de XDM

Realice los siguientes pasos para identificar los campos clave dentro de la tabla Cuenta de cliente:

- Identifique el campo que se usará como identidad principal y etiquete con un `PI`
- Identifique todas las demás identidades de personas y etiquételas con un `I`
- Identifique cualquier Identidad de relación y etiquétela con un `R`



## Paso 2: Etiquetado de campos clave en las tablas de Evento de experiencia XDM

Realice el mismo conjunto de tareas que hizo en el paso 1, pero ahora para las tablas de Evento de experiencia XDM:

- Identifique el campo de cada tabla que será la identidad principal y etiquete con un `PI`
- Identifique todas las demás identidades de persona en cada tabla y etiquételas con un `I`
- Identifique todas las identidades de relación y etiquételas con un `R`

Además de las etiquetas anteriores, etiquete también lo siguiente:

- Identifique o cree el ID de evento único para cada tabla de evento de experiencia XDM y etiquete con un `_id`
- Identifique la marca de tiempo del evento para cada tabla y etiquete con un `T`
- Identifique o cree el Tipo de evento para cada tabla y etiquete con un `ET`



## Paso 3: Etiquetado de campos clave en las tablas de búsqueda

Identifique en cada tabla de búsqueda el campo que será Identidad principal y etiquete con un `PI`



## Revisar

El siguiente vídeo revisa los campos clave identificados en las tablas de Connection 5G, incluida la razón por la que se necesitaba un campo concatenado como ID de evento único para los registros de pedidos mutables.

>[!VIDEO](https://video.tv.adobe.com/v/3459088/?quality=12&learn=on)
