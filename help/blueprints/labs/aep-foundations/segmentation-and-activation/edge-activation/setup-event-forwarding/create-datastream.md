---
title: Crear flujo de datos
description: Cree y configure una secuencia de datos con los servicios Reenvío de eventos y Adobe Experience Platform para enrutar eventos perimetrales entrantes.
doc-type: article
solution: Experience Platform
exl-id: f7ada451-2f87-48f4-8673-7bfa0df9d0d3
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---


# Crear flujo de datos

Un flujo de datos define qué servicios lo utilizarán.

- Al enviar datos a Edge, debe especificar qué secuencia de datos utilizar
- Los datos enviados a estas secuencias de datos pueden realizar acciones según el servicio configurado
  - Reenvío de eventos
  - Adobe Experience Platform

## Crear una nueva secuencia de datos

1. En el carril izquierdo bajo **Recopilación de datos**, haga clic en **Flujos de datos**
1. A continuación, haga clic en **Nueva secuencia de datos** para crear una

![Lista de flujos de datos con el botón Nuevo flujo de datos resaltado](assets/create-datastream-new-datastream-button.png)

## Configurar flujo de datos

Configure la secuencia de datos con la siguiente información:

1. Nombre -> **Datastream SB + \&lt;sandbox name> (es decir Datastream SB01)**
1. Esquema de eventos -> **dep: Web**
1. Alternar **en** todas las opciones bajo **Búsqueda por geolocalización y red**
1. Haz clic en el botón **Guardar** cuando termines

>[!WARNING]
>
>No haga clic en Guardar y agregar asignación.  Si se cancela accidentalmente

![Formulario de configuración de secuencia de datos con nombre, esquema de evento y opciones de búsqueda de geolocalización establecidas](assets/create-datastream-configure-datastream-form.png "Configurar la secuencia de datos")



Después de guardar la secuencia de datos, verá la siguiente pantalla:

![Se muestra la pantalla de confirmación inmediatamente después de guardar la nueva secuencia de datos](assets/create-datastream-created-confirmation-screen.png "Pantalla final creada por la secuencia de datos")

## Añadir servicio de reenvío de eventos

Esto le permite utilizar el reenvío de eventos para los datos recibidos por esta secuencia de datos.



1. Haz clic en **Agregar servicio**

   ![Página de detalles de secuencia de datos con el botón Agregar servicio resaltado](assets/create-datastream-add-service-button.png "Agregar servicio")

1. Configure los siguientes elementos:

   - Servicio -> Reenvío de eventos
   - Propiedad -> Seleccione la propiedad que creó en el paso anterior.  Debe llamarse de esta manera: Propiedad de reenvío de eventos SB + \&lt;su número de zona protegida>
   - Entorno -> Desarrollo

1. Cuando termine, haga clic en **Guardar**

![Configuración del servicio de reenvío de eventos con la propiedad y el entorno de desarrollo seleccionados](assets/create-datastream-event-forwarding-service-config.png "Pantalla de configuración del reenvío de eventos")



## Añadir servicio de Adobe Experience Platform

Esto le permite enviar datos al concentrador y aterrizar en un conjunto de datos para los datos recibidos por este conjunto de datos.



1. Haz clic en **Agregar servicio**

   ![Página de detalles de secuencia de datos con el botón Agregar servicio resaltado para agregar el servicio Adobe Experience Platform](assets/create-datastream-add-second-service-button.png "Agregar un nuevo servicio")

1. Configure los siguientes elementos:

   - Servicio -> Adobe Experience Platform
   - Conjunto de datos de evento -> dep: Web
   - Conjunto de datos del perfil -> dep: Cuenta de cliente
   - Seleccione La Casilla De Verificación -> Segmentación De Edge.
   - Seleccione La Casilla -> Destino De Personalization.

   ![Configuración del servicio Adobe Experience Platform con el conjunto de datos de evento, el conjunto de datos de perfil y las casillas de verificación de segmentación establecidas](assets/create-datastream-aep-service-config.png "Configurar el servicio")

1. Cuando termine, haga clic en **Guardar**.

1. La pantalla final debe ser la siguiente con dos servicios presentes. **Copie** y **guarde** el **ID de secuencia de datos** en el equipo local (lo utilizará más adelante en Postman)

![Configuración final de secuencia de datos con los servicios de reenvío de eventos y Adobe Experience Platform enumerados](assets/create-datastream-final-configuration-both-services.png "Configuración final de secuencia de datos")
