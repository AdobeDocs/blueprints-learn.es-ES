---
title: Emoción tras la compra
description: Obtenga información sobre cómo crear un recorrido posterior a la compra impulsado por eventos que almacene en déclencheur un correo electrónico de notificación de envío con detalles de seguimiento dinámico desde una API de terceros.
doc-type: overview-page
solution: Experience Platform
exl-id: 570dc378-e7a3-4895-8f14-89d420b6b340
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%
---

# Emoción tras la compra

## Requisitos previos

>[!WARNING]
>
>Los siguientes laboratorios deben haber sido completados antes de comenzar este laboratorio

- **Configuración de Postman** **—>** [Instalación de Postman](../../postman-setup/postman-installation.md)
- **Almacenes de datos — Almacén relacional en acción** **—>** [Dimension de destino de perfil](../../data-stores/relational-store-in-action/profile-target-dimension.md)
- **Almacenes de datos — Configurar canales de correo electrónico —>** [Configurar para perfil](../../data-stores/configure-email-channels/configure-for-profile.md)
  *(este paso tarda hasta tres horas en completarse)*

Si no lo ha hecho, complételo ahora

>[!CAUTION]
>
>Este laboratorio requiere un subdominio delegado a Adobe en su zona protegida. Consulta [Configuración](../../setup.md) si tienes ritmo personalizado y aún no lo tienes.

## Resumen de laboratorio

En este vídeo, aprenderá cómo se asigna el caso de uso de emoción posterior a la compra a un Recorrido, recorriendo las preguntas de pensamiento crítico y la arquitectura para enviar una notificación de envío personalizada una vez que se envía una solicitud.

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

- La confirmación de pedido inicial generalmente se implementa como un mensaje transaccional porque los clientes no desean esperar una confirmación después de realizar un pedido.
- La notificación de envío de pedidos también se puede implementar mediante mensajes transaccionales, pero se puede crear en un recorrido, lo que permite una acción personalizada para recuperar la información de envío y mejorar la comunicación con el cliente.

>[!NOTE]
>
>En este laboratorio, solo genera el mensaje de pedido enviado y omite el mensaje de confirmación de pedido.
