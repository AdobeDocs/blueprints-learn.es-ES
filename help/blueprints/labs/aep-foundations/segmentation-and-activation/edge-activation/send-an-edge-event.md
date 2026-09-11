---
hold: true
title: Enviar un evento de Edge
description: Envíe un evento web no autenticado a Edge mediante Postman y verifique que fluye a través del reenvío de eventos, la ingesta de perfiles y la calificación de audiencias Edge.
doc-type: article
solution: Experience Platform
exl-id: 8d6e9552-1fa0-4f12-928c-03f836c1652e
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---


# Enviar un evento de Edge

Ahora que todo está configurado, envíe un evento a Edge para ver cómo funciona todo.

Para ello, utilice Postman para enviar un evento web al conjunto de datos que ha creado.

Esto envía un evento **sin token de OAuth** para simular una vista de página que llega de la web a Edge.  Asegúrese de tener Postman abierto en el equipo para realizar este laboratorio.

>[!NOTE]
>
>Como no pasa un token autenticado, no se devuelve ningún atributo.

## Expectativas del laboratorio

1. Evento de experiencia para visitar Edge
1. Configuración de flujo de datos para utilizar el servicio de reenvío de eventos
1. Reenvío de eventos para enviar el evento al webhook
1. Configuración de flujo de datos para utilizar el servicio AEP
   1. Audiencia de Edge para ejecutar
   1. Enviar evento al concentrador
1. Respuesta de Postman para incluir la audiencia de Edge (pero sin atributos)
1. Almacén de perfiles para recibir un evento y agregar un fragmento de perfil de evento
1. Almacén de identidades para agregar una relación
1. Conjunto de datos para recibir datos y almacenarlos en Data Lake



## Navegar hasta la llamada

1. **Barra lateral izquierda de Postman** -> Colecciones
1. **Colección** -> Bootcamp de AEP Foundations (Labs)
1. **Carpeta** -> laboratorio de perfiles
1. **Solicitud de API** -> Crear Edge de evento web (sin autenticación)

![Navegación de la barra lateral de Postman a la solicitud de API Crear Edge de evento web (sin autenticación) en la carpeta del laboratorio de perfiles](assets/send-an-edge-event-navigate-to-the-postman-call.png)

## Modificar solicitud de API

Antes de poder ejecutar la solicitud de API, debe añadir información adicional a la solicitud. Comience por recopilar los siguientes valores:

## Recopile el ID de secuencia de datos

1. En el carril izquierdo, haga clic en **Datastreams** (bajo el encabezado de Recopilación de datos)
1. Seleccione su secuencia de datos y copie el valor **ID de secuencia de datos**

![Lista de flujos de datos con el valor de ID de flujo de datos resaltado para copiar](assets/send-an-edge-event-gather-datastream-id.png)

## Actualizar parámetro de consulta de Postman

1. En la propia solicitud, haga clic en **Params**
1. Actualice **Value** con el ID de secuencia de datos del paso anterior
1. Haga clic en el botón **Guardar** para guardar la actualización

![Pestaña Parámetros de Postman con el valor de ID de secuencia de datos pegado en el campo Valor](assets/send-an-edge-event-update-datastream-id-param.png "Actualizar dataStreamId")



Cambiar el correo electrónico a su correo electrónico

![Cuerpo de solicitud de Postman que muestra el valor de correo electrónico actualizado a la propia dirección de correo electrónico del evaluador](assets/send-an-edge-event-change-email-param.png "Cambiar correo electrónico a su correo electrónico")

## Ejecución de la API

Ejecute la solicitud haciendo clic en el botón **Enviar**.

Se está haciendo clic en el botón ![Enviar de Postman para ejecutar la solicitud Crear evento web de Edge](assets/send-an-edge-event-execute-request.png)

Lo que debería ver que regresa en la respuesta es esto central:

- Una respuesta 200 OK significa que Edge Network envió y aceptó correctamente los datos

>[!NOTE]
>
>Los segmentos por lotes y de flujo continuo no se mostrarán hasta que se evalúen primero en el concentrador

## Validar el reenvío de eventos

En webhook.site debe ver inmediatamente el mismo cuerpo de carga útil que envió a través de su solicitud de Postman.

![Webhook.site muestra la carga de evento reenviada recibida desde el reenvío de eventos](assets/send-an-edge-event-webhook-payload.png)

>[!NOTE]
>
>Observe que la carga útil ha agregado la información de búsqueda geográfica que solicitó al configurar el conjunto de datos que utilizó en la configuración de Edge

## Búsqueda del perfil

En Adobe Experience Platform, busque el perfil que acaba de enviar desde el evento que acaba de enviar a Edge Network. Vaya a Perfiles -> Examinar para realizar la búsqueda con la siguiente información:

- Política de combinación -> Basada en tiempo predeterminado
- Área de nombres de identidad -> Correo electrónico
- Valor de identidad -> edge-email\@dep.com
  - Nota: cambie esto para que coincida con el correo electrónico que utilizó en el paso *Actualizar parámetro de consulta de Postman* anterior

1. Haga clic en **Ver** para buscar el perfil
1. Haga clic en **ID de perfil** para abrir el perfil

![Perfil Examine los resultados de búsqueda con el vínculo Ver para abrir el perfil coincidente](assets/send-an-edge-event-lookup-profile.png "Perfil de búsqueda")

1. Haz clic en **Eventos** en la barra de navegación superior y podrás ver el evento que acabas de enviar

![Pestaña Eventos de perfil que muestra el evento de experiencia que se acaba de enviar a Edge](assets/send-an-edge-event-view-profile-event.png "Ver el evento de perfil")

1. Valide que el perfil se haya clasificado para las audiencias mediante la revisión de la pestaña Pertenencia a la audiencia en la barra de navegación superior. Debería ver lo siguiente:

- Cualquier evento de Edge (en 15 minutos)
- dep: cualquier flujo de eventos (en una hora)

![Pestaña Pertenencia a audiencia que muestra la calificación para cualquier evento Edge y dep: Cualquier evento Transmitiendo audiencias](assets/send-an-edge-event-any-event-streaming-within-the-last-hour.png)

## Interpretación de las comprobaciones

1. Compruebe si hay respuestas de 200 en Postman (carga útil con formato correcto)
1. Compruebe si el webhook tiene el evento (reenvío de eventos configurado correctamente)
1. Compruebe si el perfil tiene los eventos (servicio de AEP correctamente configurado, evento recibido y procesado en el concentrador)
1. Compruebe si el perfil tiene dos identidades (el gráfico de identidad se ha vinculado en el concentrador) después de unos minutos
1. Compruebe si el perfil cumple los requisitos para las audiencias (audiencia definida correctamente)
1. Compruebe si Data Lake tiene el evento.
