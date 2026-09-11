---
hold: true
title: Envío de un evento web de Edge
description: Obtenga información sobre cómo enviar un evento web simulado a Adobe Edge Network a través de una llamada de API de Postman con el ID del conjunto de datos.
doc-type: article
solution: Experience Platform
exl-id: 0823bcf7-35d9-492e-ad8d-3e8327f77dd8
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Envío de un evento web de Edge

## Objetivo de aprendizaje

Envíe un evento web simulado a Adobe Edge Network mediante la API.

Para simular una página web que se carga y envía a AEP Edge, envía una llamada de Postman al conjunto de datos que ha creado.

Esto envía un evento sin token de OAuth.  Asegúrese de tener Postman abierto en el equipo para realizar este laboratorio.

>[!NOTE]
>
>Como no pasa un token autenticado, no se devuelve ningún atributo.

## Expectativas del laboratorio

1. Evento de experiencia para visitar Edge
1. Configuración de flujo de datos
1. Configuración de flujo de datos para utilizar el servicio AEP
   1. Audiencia de Edge para ejecutar
   2. Enviar evento al concentrador
1. Respuesta de Postman para incluir la audiencia de Edge (pero sin atributos)
1. Almacén de perfiles para recibir un evento y agregar un fragmento de perfil de evento
1. Almacén de identidades para agregar una relación
1. Conjunto de datos para recibir datos y almacenarlos en Data Lake



## Actualizar variable de entorno de Postman

Antes de poder ejecutar la solicitud de API, debe agregar el ID de la secuencia de datos al entorno de variables de Postman. Comience por recopilar los siguientes valores:

### Recopilación del ID de flujo de datos

1. Ya debería tener el **ID de secuencia de datos**

>[!NOTE]
>
>**Si perdió el ID de flujo de datos**
>
>1. En el carril izquierdo, haga clic en **Datastreams** (bajo el encabezado de Recopilación de datos)
>2. Seleccione su secuencia de datos y copie el valor **ID de secuencia de datos**
>
>![Lista de flujos de datos que muestra el ID de flujo de datos que se va a copiar](assets/send-an-edge-web-event-gather-datastream-id.png)



### Navegar hasta la llamada

1. **Barra lateral izquierda de Postman** -> `Collections`
1. **Colección** -> `AJO Bootcamp (Labs)`
1. **Carpeta** -> `Profile & Journey Labs`
1. **Solicitud de API** -> `Create Web Event`

![Barra lateral de Postman navegando a la solicitud Crear evento web](assets/send-an-edge-web-event-postman-create-web-event-request.png)

### Actualizar variable DATASTREAM\_CONFIG

1. Haga clic en **Variables en la solicitud** en la parte superior derecha

![Variables en la opción de solicitud en la barra de herramientas de Postman](assets/send-an-edge-web-event-click-variables-in-request.png)

&#x200B;2. Actualice **DATASTREAM_CONFIG** **Value** con **ID de secuencia de datos** desde el primer paso en la página.

![Variable DATASTREAM_CONFIG actualizada con el identificador de secuencia de datos](assets/send-an-edge-web-event-update-datastream-config-variable.png)

&#x200B;3. **Guardar** su actualización (Ctrl+S o Comando+S)
&#x200B;4. Haga clic en &#39;**X**&#39; en la esquina superior derecha de la barra lateral del entorno para cerrar la barra lateral

![Cerrando la barra lateral del entorno de Postman después de guardar](assets/send-an-edge-web-event-close-environment-sidebar.png)

&#x200B;5. La solicitud **Crear evento web** ya está lista para enviarse, ya que todas las variables aparecen ahora en azul y tienen un valor en el entorno.

![Crear solicitud de evento web con todas las variables rellenadas](assets/send-an-edge-web-event-request-ready-to-send.png)

## Ejecución de la API

Ejecute la solicitud haciendo clic en el botón **Enviar**.

La respuesta tiene este aspecto:

![Ejemplo 200 Respuesta correcta de la solicitud Crear evento web](assets/send-an-edge-web-event-api-response-example.png)

Lo que se ve que regresa en la respuesta son estas cosas centrales:

- Una respuesta 200 OK significa que Edge Network envió y aceptó correctamente los datos

## Resumen

El evento se ha enviado correctamente a Edge Network y lo ha aceptado
