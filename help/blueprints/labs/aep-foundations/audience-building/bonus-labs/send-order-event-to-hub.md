---
title: Enviar evento de pedido a Hub
description: Obtenga información sobre cómo transmitir un evento de pedido al concentrador mediante API, crear un segmento de pedido de flujo continuo, activarlo en un destino y validar los resultados del perfil.
doc-type: article
solution: Experience Platform
exl-id: d5de39d7-7340-487a-86fa-504344daeab7
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---


# Enviar evento de pedido a Hub

## Transmisión a Hub o Edge

En el #1 de casos de uso, enviamos un evento a Edge.  Hay algunos casos de uso en los que podemos tener un sistema back-end que quiere transmitir en un evento, pero no necesita enviarlo a Edge.  Este laboratorio muestra cómo hacerlo transmitiendo un evento de pedido al concentrador.

## Crear un segmento de pedido (si no lo ha hecho)

Haga clic en Audiencia en el carril izquierdo y haga clic en el botón Crear audiencia en la parte superior derecha.

![Haga clic en Audiencia en el carril izquierdo y luego en Crear audiencia](assets/send-order-event-to-hub-click-create-audience-button.png)

Busque la tarjeta de tipo de evento Pedido realizado y arrástrela al lienzo.

![Arrastre la tarjeta de tipo de evento Pedido realizado al lienzo](assets/send-order-event-to-hub-drag-order-placed-event-onto-canvas.png)

## Actualización de reglas de eventos

Realice los siguientes cambios en las reglas de evento (puede que necesite expandir el evento para verlo)

1. En última instancia
1. 15
1. Minutes
1. Cambio en la evaluación de streaming

Guardar como **Solicitar flujo de eventos (en 15 minutos)**



![Guardar la audiencia como flujo de eventos de pedido (en 15 minutos) con evaluación de flujo](assets/send-order-event-to-hub-save-streaming-evaluation-rule.png)

## Activar en destino

Abra la audiencia que acaba de crear si está cerrada.

Haga clic en Activar en destino



![Haga clic en Activar en destino para la audiencia del pedido](assets/send-order-event-to-hub-click-activate-to-destination.png)

### Destino

Seleccione el destino de streaming que creó anteriormente (webhook de DEP de streaming)



![Seleccione el destino de webhook de Streaming DEP](assets/send-order-event-to-hub-select-streaming-destination.png)

### Asignación

Deje Mapping solo y haga clic en Next

![Deje la asignación sin cambios y haga clic en Siguiente](assets/send-order-event-to-hub-leave-mapping-click-next.png)

Haga clic en Finalizar

## Abrir Postman

Inicie postman en el equipo y vaya a la siguiente llamada de API:

1. **Barra lateral izquierda de Postman** —> `Collections`
1. **Colección** —> `AEP Foundations Bootcamps (labs)`
1. **Carpeta** —> laboratorio de perfiles
1. **Solicitud de API** —> `Create Order Event`

![Abrir la solicitud de API de evento Crear pedido en Postman](assets/send-order-event-to-hub-create-order-event-api-request.png)


## Modificar solicitud de API

Para crear la solicitud de API de ejemplo, debe rellenar los siguientes fragmentos en el cuerpo de la solicitud de API.

Comience por recopilar los siguientes valores:

## Buscar extremo de flujo continuo de cuenta

1. Vaya a **Orígenes** en el carril izquierdo y, a continuación, haga clic en **Cuentas** en la barra de navegación superior
1. Busque **dep: API HTTP \[raw]**, resalte la fila, copie y guarde el valor de **extremo de transmisión** en cualquier lugar al que pueda hacer referencia más adelante

 y copie su extremo de flujo continuo](assets/send-order-event-to-hub-http-api-raw-streaming-endpoint.png &quot;dep: HTTP API \[raw]&quot;)

## Buscar ID de flujo de datos

1. Busque el registro de **dep: Orders (stream)** y haga clic en el vínculo de flujos de datos
1. En el carril derecho, copie y guarde los valores de **ID de flujo de datos** en algún lugar al que pueda hacer referencia posteriormente

>[!NOTE]
>
>Haga clic en un espacio vacío de la fila.  NO haga clic en los enlaces azules!

![Copie el ID de flujo de datos para el flujo de datos dep: Orders (stream)](assets/send-order-event-to-hub-orders-stream-dataflow-id.png "Flujo de datos web e ID de conjuntos de datos")

## Crear solicitud de API final

Copie los valores guardados en los pasos anteriores en los lugares resaltados a continuación.

- **Rojo** —> `Streaming Endpoint URL`
- **Verde** —> `Dataflow ID`

La solicitud de API final debería tener un aspecto similar al siguiente cuando se complete

>[!CAUTION]
>
>NO EJECUTAR AÚN.

![Solicitud de API de evento de creación de pedido completada con extremo de flujo de datos e ID de flujo de datos completada](assets/send-order-event-to-hub-final-order-api-request.png)


## Ejecución de la API

1. Para guardar la llamada de API, haz clic en el botón **Guardar**
1. Ejecute la solicitud haciendo clic en el botón **Enviar**

Una llamada correcta debería dar la siguiente respuesta...

![Respuesta correcta de la API después de enviar el evento de pedido](assets/send-order-event-to-hub-successful-api-response.png)

## Validate

1. Vaya a su perfil y busque su perfil para ver que el evento se ha introducido en el perfil.  Debería aparecer en segundos.
   1. Buscar el perfil mediante el correo electrónico en el pedido
1. Valide que el perfil se haya clasificado para los segmentos (puede tardar unos minutos). Debería aparecer en segundos o minutos.
   1. Solicitar transmisión de eventos (en 15 minutos)
1. Compruebe su webhook para ver si el destino ha notificado al webhook que el segmento se ha &quot;realizado&quot;.  Debería aparecer en 5-10 minutos.
1. Después de 15-30 minutos, incluso puede comprobar el conjunto de datos con lo siguiente:
   1. Cambie el nombre de la tabla siguiente por el de su zona protegida.  Para encontrarlo, vaya a la lista de conjuntos de datos y filtre en &quot;`dest`&quot;, abra el conjunto de datos y copie el nombre de la tabla en el carril derecho.

```sql
SELECT * FROM profile_export_for_destination_merge_policy_xxx
WHERE extSourceSystemAudit.LASTREFERENCEDDATE >= CURRENT_DATE
AND identitymap['email'][0].ID in ('depche.mode@dep.com')
ORDER BY extSourceSystemAudit.LASTREFERENCEDDATE DESC
LIMIT 10
```
