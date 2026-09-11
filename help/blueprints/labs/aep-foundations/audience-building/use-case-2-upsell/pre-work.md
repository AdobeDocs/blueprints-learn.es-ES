---
title: Trabajo previo
description: Investigue los campos de esquema para el uso de la facturación y el nombre del plan, resaltando cómo las descripciones que faltan y los campos duplicados pueden confundir a los creadores de audiencias.
doc-type: article
solution: Experience Platform
exl-id: c26de19e-82da-4070-a918-2d2c8ef2c116
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Trabajo previo

Para este caso de uso, no hay mucho trabajo previo que hacer. Básicamente tenemos dos cosas que estamos buscando, 1) Uso, 2) Plan.  Encuentra dónde están.

## Uso de datos de facturación

1. Crear una audiencia nueva
1. Busque &quot;uso&quot; en Atributos. Haga clic en la &quot;i&quot; para revisar la descripción (no hay ninguna).

   ![Buscar uso en Atributos - no se muestra descripción](assets/pre-work-search-usage-in-attributes.png)



&#x200B;3. Busque &quot;uso&quot; en Eventos.  Haga clic en la &quot;i&quot; para revisar la descripción (no hay ninguna).

![Buscar uso en eventos - no se muestra descripción](assets/pre-work-search-usage-in-events.png)

>[!NOTE]
>
>Ninguno de estos tiene descripciones, por lo que el experto en marketing puede hacer algunas suposiciones y adivinar mal.
>
>Las descripciones son importantes.  Sin descripciones, ¿cómo sabrá el experto en marketing:
>
>- ¿Cuál utilizar?
>- ¿Latencia de datos?
>- ¿Recomendado/preferido en casos de uso específicos?
>
>Al proporcionar esta información en descripciones, podemos guiarlos mejor.

>[!NOTE]
>
>Intente buscar &quot;Facturación&quot;.  Observe que no aparece como un atributo de perfil.  Se muestra como una tarjeta de tipo de evento junto con el campo &quot;Uso de datos de facturación&quot;.
>
>También existen convenciones de nomenclatura para el experto en marketing.  Según en lo que busquen o si están buscando/esperando que esto sea un Evento o un Perfil, afecta a lo que encuentran y, finalmente, utilizan.

## Plan

Busque &quot;Plan&quot; en Atributos.  Tenga en cuenta que tenemos una serie de cosas para elegir.  Reducirlo a &quot;Nombre del plan&quot;.  Tenemos dos nombres de plan?!



![Se encontró el atributo Nombre del primer plan al buscar el plan](assets/pre-work-duplicate-plan-name-field.png)



![Se encontró el atributo Second Plan Name al buscar el plan](assets/pre-work-duplicate-plan-name-field--2.png)

El nombre del plan (nombre del plan) parece ser el que necesitamos en función de la descripción y al otro le falta una descripción.
