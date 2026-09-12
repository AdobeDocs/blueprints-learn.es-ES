---
title: Emoción tras la compra
description: Obtenga información sobre cómo crear un recorrido posterior a la compra impulsado por eventos que almacene en déclencheur un correo electrónico de notificación de envío con detalles de seguimiento dinámico desde una API de terceros.
doc-type: overview-page
solution: Experience Platform
exl-id: 570dc378-e7a3-4895-8f14-89d420b6b340
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Emoción tras la compra

## Requisitos previos

>[!WARNING]
>
>Los siguientes laboratorios deben haber sido completados antes de comenzar este laboratorio

Estos laboratorios deben haber sido completados antes de comenzar este laboratorio:

- **Almacenes de datos — Almacén relacional en acción** **—>** [Dimension de destino de perfil](../../data-stores/relational-store-in-action/profile-target-dimension.md)
- **Almacenes de datos — Configurar canales de correo electrónico —>** [Configurar para perfil](../../data-stores/configure-email-channels/configure-for-profile.md)
  *(esto puede tardar hasta tres horas en completarse)*

Si no lo ha hecho, complételo ahora

## Resumen de laboratorio

En este vídeo, aprenderá cómo se asigna el caso de uso de emoción posterior a la compra a un recorrido, recorriendo las preguntas de pensamiento crítico y la arquitectura para enviar una notificación de envío personalizada una vez que se envía una solicitud.

>[!VIDEO](https://video.tv.adobe.com/v/3491146/)

## Objetivos de aprendizaje

- Crear un Recorrido que comience con un evento unitario
- Configure una acción personalizada para llamar a un sistema de terceros y devolver información utilizada en un Recorrido
- Ejecución de un recorrido mediante streaming en una carga útil de evento
- Prueba y depuración de perfiles y Recorridos
- Validar la experiencia deseada mediante informes y registros
- Configure la personalización en un correo electrónico simple y véala en acción



## Descripción del caso de uso

Cuando un cliente realiza un pedido, desea enviar un mensaje de confirmación con los detalles del pedido.  Una vez enviado el pedido, desea almacenar en déclencheur un segundo mensaje con información de seguimiento recuperada dinámicamente de una API de terceros.

**Llamadas clave:**

- El pedido inicial realizado se suele implementar como mensaje transaccional, ya que las personas no desean esperar una confirmación cuando simplemente solicitan algo.
- La notificación de envío de pedidos también se puede implementar mediante mensajes transaccionales, pero se puede crear en un recorrido, lo que permite una acción personalizada para recuperar la información de envío y mejorar la comunicación con el cliente.

>[!NOTE]
>
>En este laboratorio solo generará el mensaje de envío de pedido y omitirá el mensaje de confirmación de pedido.
