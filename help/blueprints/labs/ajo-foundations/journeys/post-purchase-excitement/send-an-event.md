---
title: Enviar un evento
description: Utilice Postman para transmitir un evento de pedido enviado simulado directamente al concentrador para almacenar en déclencheur el recorrido, en lugar de enviarlo al Edge.
doc-type: article
solution: Experience Platform
exl-id: a0f75f5a-e3b3-42a2-8547-f075a7661a22
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---


# Enviar un evento

## Objetivo de aprendizaje

Envíe un evento simulado de envío de pedidos para almacenar en déclencheur el recorrido mediante Postman

## Transmisión a Hub o Edge

Anteriormente, se enviaba un evento al Edge.  Hay algunos casos de uso en los que puede ser que tengamos un sistema back-end que quiera transmitir en un evento, pero no necesita enviarlo a Edge.  Este laboratorio muestra cómo hacerlo al **transmitir un evento de envío de pedidos al concentrador** (también conocido como servidor a servidor, por ejemplo, Commerce Server a AEP indicando que se ha enviado un pedido).

## El evento de validación no está en el perfil

1. Vaya a sus **perfiles** y busque el perfil.
   - **Área de nombres de identidad** -> `email`
   - **Valor de identidad** -> `henry.creel@emailsim.io`
1. Haga clic en la ficha **Eventos**.
   - No debe haber **ningún** `orders.shipped` eventos

## Modificar solicitud de API

Para crear la solicitud de API, debe rellenar las siguientes partes en el cuerpo de la solicitud de API.

Comience por recopilar los siguientes valores:

### Buscar extremo de flujo continuo de cuenta

1. Vaya a **Orígenes** en el carril izquierdo y, a continuación, haga clic en **Cuentas** en la barra de navegación superior
1. Busque **dep: API HTTP \[raw]**, resalte la fila, copie y guarde el valor de **extremo de transmisión** en cualquier lugar al que pueda hacer referencia más adelante

![dep: API HTTP [raw] fila de cuenta resaltada con valor de extremo de transmisión](assets/send-an-event-streaming-endpoint-account-row.png "dep: API HTTP \[raw]")


### Buscar ID de flujo de datos

1. Haga clic en **dep: API HTTP \[raw]**
1. Busque el registro de **dep: Orders (stream)** haga clic en el vínculo de flujos de datos
1. En el carril derecho, copie y guarde los valores de **ID de flujo de datos** en algún lugar al que pueda hacer referencia posteriormente

>[!WARNING]
>
>Haga clic en un espacio vacío de la fila.  NO haga clic en los enlaces azules!

![Valores de ID de flujo de datos mostrados en el carril derecho](assets/send-an-event-dataflow-id-in-right-rail.png "ID de conjunto de datos y flujo de datos web")



### Abrir Postman

Inicie Postman en el equipo y vaya a la siguiente llamada de API:

- **Barra lateral izquierda de Postman** —> `Collections`
- **Colección** —> `AJO Bootcamp (Labs)`
- **Carpeta** —> `Profile & Journey Labs`
- **Solicitud de API** —> `Ship Order Event`

![Solicitud de evento de pedido de envío ubicada en la colección Postman](assets/send-an-event-open-ship-order-event-postman.png)



### Crear solicitud de API final

1. Copie los valores guardados en los pasos anteriores en los lugares resaltados a continuación.
1. Haga clic en **Encabezados** y pegue estos valores (elimine los espacios finales):
   - **Rojo** —> `Streaming Endpoint URL`
   - **Verde** —> `Dataflow ID`
     - El valor tiene el aspecto de un GUID (no comienza con http)

>[!CAUTION]
>
>NO EJECUTAR AÚN.

![URL de extremo de transmisión e ID de flujo de datos pegados en los encabezados de Postman](assets/send-an-event-paste-headers-in-postman.png)

## Ejecución de la API

1. Para guardar la llamada de API, haz clic en el botón **Guardar**
1. Ejecute la solicitud haciendo clic en el botón **Enviar**

Una llamada correcta debería dar la siguiente respuesta...

![Respuesta correcta después de enviar el evento web](assets/send-an-event-successful-web-event-send.png)

## Resumen

Se ha enviado correctamente un evento de orden de envío a la plataforma
