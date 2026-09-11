---
hold: true
title: Crear secuencia de datos
description: Obtenga información sobre cómo crear y configurar un flujo de datos con los servicios de Adobe Experience Platform, Offer Decisioning y Journey Optimizer para habilitar el procesamiento de eventos de Edge.
doc-type: article
solution: Experience Platform
exl-id: 37873340-476a-4303-886d-de4835bba8df
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# Crear secuencia de datos

## Objetivo de aprendizaje

Cree y configure una secuencia de datos con los servicios necesarios para habilitar el procesamiento de eventos de Edge.

Un flujo de datos define qué servicios lo utilizarán.

- Al enviar datos a Edge, debe especificar qué secuencia de datos utilizar
- Los datos enviados a estas secuencias de datos pueden realizar acciones según el servicio configurado
  - Adobe Experience Platform

## Crear una nueva secuencia de datos

1. En el carril izquierdo bajo **Recopilación de datos**, haga clic en **Flujos de datos**
1. A continuación, haga clic en **Nueva secuencia de datos** para crear una

![Lista de flujos de datos con el botón Nuevo flujo de datos resaltado](assets/create-datastream-new-datastream-button.png)

## Configurar flujo de datos

Configure la secuencia de datos con la siguiente información:

1. Nombre -> **Datastream SB + \&lt;sandbox name> (es decir Datastream SB01)**
1. Esquema de asignación -> **dep: Web**
1. Cambie **on** todas las opciones en **Geolocalización y Búsqueda de red** si desea capturar esta información.
1. Haz clic en el botón **Guardar** cuando termines

>[!WARNING]
>
>No haga clic en Guardar y agregar asignación.  Si lo hace accidentalmente, simplemente cancele la suscripción

![Formulario de configuración de secuencia de datos con campos de nombre y esquema de asignación](assets/create-datastream-configure-datastream-form.png "Configurar la secuencia de datos")



Después de guardar la secuencia de datos, verá la siguiente pantalla:

![Pantalla de confirmación después de guardar la nueva secuencia de datos](assets/create-datastream-created-confirmation.png "Pantalla final creada por la secuencia de datos")

## Añadir servicio de Adobe Experience Platform

Esto le permite enviar datos al concentrador y aterrizar en un conjunto de datos para los datos recibidos por este conjunto de datos.

1. Haga clic en el botón azul **Agregar servicio** que se encuentra en medio de la pantalla

![Botón Agregar servicio en la pantalla de configuración de la secuencia de datos](assets/create-datastream-add-service-button.png)

&#x200B;2. Configure los siguientes elementos:
   - **Servicio** -> `Adobe Experience Platform`
   - **Conjunto de datos de evento** -> `dep: Web`
   - **Conjunto de datos del perfil** -> `dep: Customer Account`
   - **Seleccionar casilla de verificación** -> `Offer Decisioning`
   - **Seleccionar casilla de verificación** -> `Adobe Journey Optimizer`
&#x200B;3. Cuando termine, haga clic en **Guardar**

![Cuadro de diálogo de configuración del servicio Adobe Experience Platform con campos de evento y conjunto de datos de perfil](assets/create-datastream-configure-aep-service.png)

Verá el servicio ahora agregado a su secuencia de datos

Se agregó el servicio ![Adobe Experience Platform al conjunto de datos](assets/create-datastream-aep-service-added.png "Servicio Adobe Experience Platform agregado al conjunto de datos")

**Copie** y **guarde** la **ID de secuencia de datos** en el equipo local (la usaremos más adelante en Postman)

![Campo de ID de secuencia de datos que copiar y guardar para su uso posterior](assets/create-datastream-copy-datastream-id.png)

## Resumen

Debe tener un flujo de datos que funcione con el servicio Adobe Experience Platform configurado.
