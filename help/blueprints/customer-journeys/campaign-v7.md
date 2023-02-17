---
title: Modelo de Campaign v7
description: Adobe Campaign v7 es una herramienta de campaña diseñada para canales de marketing tradicionales, como correo electrónico y correo directo. Proporciona sólidas capacidades de ETL y administración de datos para ayudar a diseñar y depurar la campaña perfecta. Su motor de orquestación proporciona programas de marketing multitáctil enriquecidos con un enfoque central en los recorridos impulsados por lotes. También viene acompañado de un servidor de mensajería en tiempo real que permite a los equipos de marketing enviar mensajes predefinidos basados en una carga útil inclusiva de cualquier sistema de TI para cosas como restablecimiento de contraseña, confirmación de pedido, recepción electrónica y mucho más.
solution: Campaign,Campaign Classic v7
exl-id: 71c808f5-59e6-4f49-a6ba-581ed508bc04
source-git-commit: 5110ee2a7a079945475055cbcfdabf7cdcaa0ab5
workflow-type: ht
source-wordcount: '1195'
ht-degree: 100%

---

# Modelo de Campaign v7

Adobe Campaign v7 es una herramienta de campaña diseñada para canales de marketing tradicionales, como correo electrónico y correo directo. Proporciona sólidas capacidades de ETL y administración de datos para ayudar a diseñar y depurar la campaña perfecta. Su motor de orquestación proporciona programas de marketing multitáctil enriquecidos con un enfoque central en los recorridos impulsados por lotes. También viene acompañado de un servidor de mensajería en tiempo real que permite a los equipos de marketing enviar mensajes predefinidos basados en una carga útil inclusiva de cualquier sistema de TI para cosas como restablecimiento de contraseña, confirmación de pedido, recepción electrónica y mucho más.

<br>

## Casos de uso

* Programas de mensajería por lotes
* Campañas de incorporación y remarketing
* Campañas de publicidad, folletos y revistas del correo directo
* Mensajes transaccionales simples de bajo volumen (es decir, restablecimiento de contraseña, recibos de correo electrónico, confirmaciones de pedidos, etc.)

<br>

## Arquitectura

<img src="assets/campaign-v7-architecture.svg" alt="Arquitectura de referencia para el modelo de Campaign v7" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Patrones de integración

| Escenario | Descripción | Competencias |
| :-- | :--- | :--- |
| [Real-Time CDP con Adobe Campaign](rtcdp-and-campaign.md) | Muestra cómo se puede utilizar el Real-Time CDP de Adobe Experience Platform y su herramienta de segmentación centralizada con Adobe Campaign para ofrecer conversaciones personalizadas | <ul><li>Uso compartido de perfiles y audiencias de Real-Time CDP con Adobe Campaign mediante el uso del intercambio de archivos de almacenamiento en la nube y los flujos de trabajo de ingesta de Adobe Campaign </li><li>Comparta fácilmente los datos de entrega e interacción de las conversaciones de los clientes con Real-Time CDP desde Adobe Campaign para mejorar el perfil del cliente en tiempo real y proporcionar informes multicanal en campañas de mensajería</li></ul> |
| [Journey Optimizer con Adobe Campaign](ajo-and-campaign.md) | Muestra cómo puede utilizar Adobe Journey Optimizer para orquestar experiencias 1:1 utilizando el perfil del cliente en tiempo real y aprovechar el sistema de mensajería transaccional nativo de Adobe Campaign para enviar el mensaje | Aproveche Real-Time Customer Profile y la potencia de Journey Optimizer para orquestar en el momento las experiencias mientras utiliza las capacidades nativas de mensajería en tiempo real de Adobe Campaign para realizar la comunicación de último momento<br><br>Consideraciones:<br><ul><li>Se pueden enviar hasta 50 000 mensajes por hora a través del servidor de mensajes en tiempo real<li>No se establece ninguna limitación desde Journey Optimizer, por lo que debe asegurarse de que un arquitecto empresarial de preventas realice una comprobación técnica</li><li>Gestión de decisiones no se admite en cargas al servidor de mensajería en tiempo real de Campaign v7</li></ul> |

<br>

## Prerrequisitos

### Servidor de aplicaciones y servidor de mensajería en tiempo real

* La consola de cliente de Adobe Campaign es necesaria para interactuar y utilizar el software de Campaign v8. Es un cliente basado en Windows y utiliza protocolos de Internet estándar (SOAP, HTTP, etc.). Asegúrese de que tiene los permisos necesarios activados en la organización para distribuir, instalar y ejecutar software

* Listado de direcciones IP permitidas
   * Identifique los rangos de IP que todos los usuarios aprovecharán durante el acceso a la consola del cliente
   * Identifique qué sistemas empresariales podrán hablar con el servidor de mensajería en tiempo real y asegúrese de que tienen una IP o un rango asignado estáticamente que pueda realizar la lista de permitidos
   * Esto se puede configurar y controlar mediante el panel de control de Campaign
* Administración de claves sFTP
   * Tenga a disposición claves públicas SSH para su uso con el sFTP proporcionado por Campaign. Esto se puede configurar y controlar mediante el panel de control de Campaign.

### Correo electrónico

* Debe tener un subdominio listo para utilizarse en el envío de mensajes
* El subdominio se puede delegar completamente a Adobe (recomendado) o se pueden usar CNAME para señalar a servidores DNS específicos de Adobe (personalizado)
* Se necesita el registro TXT de Google para cada subdominio para garantizar una buena entrega

### Push móvil

* Debe tener un desarrollador móvil disponible para implementar, configurar y crear la aplicación móvil
* Adobe solo proporciona un SDK para recopilar la información necesaria de FCM (Android) y APNS (iOS) para enviar cargas de mensajes a sus servidores. Es responsabilidad del cliente saber cómo debe codificarse, implementarse, administrarse y depurarse la aplicación móvil

### Aplicaciones web (opcional)

* Puede delegar un subdominio adicional para las páginas de aterrizaje y cancelación de suscripción alojadas en Campaign
* Se recomienda encarecidamente el certificado SSL

<br>

## Guardas

### Tamaño del servidor de aplicaciones

* El almacenamiento se puede ampliar a 100 millones de perfiles
* Configure y controle el acceso de los usuarios a través de Adobe Admin Console (recomendado) o localmente en la propia aplicación
* Se espera que la carga de datos en Campaign se realice mediante archivos por lotes
   * La compatibilidad con la carga de datos de API se utiliza principalmente para administrar perfiles u objetos simples dentro de la base de datos (es decir, crear y actualizar). No se pretende utilizar para cargar grandes volúmenes de datos u operaciones similares a lotes.
   * No se admite el uso de API para leer datos con fines de aplicación personalizados
* Las llamadas de API están limitadas a 15 por segundo o a 150 000 por día a escala

### Tamaño del servidor de mensajería por lotes

* Se puede escalar para gestionar hasta 2,5 millones de mensajes por hora

### Tamaño del servidor de mensajería en tiempo real

* Se pueden enviar hasta 50 000 mensajes por hora
* De forma predeterminada, se aprovisionan dos servidores de mensajería en tiempo real. Capacidad para ampliar hasta ocho servidores de mensajería en tiempo real.

### Configuración de SMS

* Campaign ofrece la capacidad de integrarse con un proveedor de SMS. El cliente adquiere el proveedor y lo integra con la campaña para enviar mensajes basados en SMS
* La compatibilidad se realiza a través del protocolo SMPP
* Hay tres (3) tipos diferentes de SMS que puede soportar Adobe:
   * SMS MT (móvil finalizado): un SMS emitido por Adobe Campaign a los teléfonos móviles a través del proveedor SMPP.
   * SMS MO (móvil originado): un SMS que un móvil envía a Adobe Campaign a través del proveedor SMPP.
   * SMS SR (informe de estado), DR o DLR (recibo de envío): un recibo devuelto enviado por el móvil a Adobe Campaign a través del proveedor SMPP que indica que el SMS se ha recibido correctamente. Adobe Campaign también puede recibir SR para indicar que el mensaje no se ha podido entregar, a menudo con una descripción del error.

### Configuración push móvil

* Dos enfoques compatibles para la integración con dispositivos móviles para notificaciones push:
   * SDK móvil de Experience Platform (recomendado)
   * SDK móvil de Campaign
* Ruta del SDK móvil de Experience Platform:
   * Aproveche las etiquetas de Adobe y la extensión de Campaign Classic para configurar la integración con el SDK móvil de Experience Platform
   * Se necesita un conocimiento práctico de las etiquetas de Adobe y la recopilación de datos
   * Se necesita experiencia de desarrollo móvil con notificaciones push en Android y iOS para implementar el SDK, integrarse con FCM (Android) y APNS (iOS) para obtener un token push, configurar la aplicación para recibir notificaciones push y gestionar interacciones push
* SDK móvil de Campaign
   * Póngase en contacto con el Servicio de atención al cliente de Adobe para obtener acceso
   * Siga la [Documentación del SDK de Campaign](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=es) para aprender a instalar y configurar el SDK

   >[!IMPORTANT]
   >Si implementa el SDK de Campaign y trabaja con otras aplicaciones de Experience Cloud, será necesario utilizar el SDK móvil de Experience Platform para la recopilación de datos. Se trata de un SDK diferente y deberá instalarse junto al SDK de Campaign

<br>

## Pasos de implementación

Consulte la [Guía de introducción](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=es) para implementar Adobe Campaign v7


## Documentación relacionada

* [Documentación de Campaign v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=es)
* [Descripción del producto Campaign v7](https://helpx.adobe.com/es/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/launch.html?lang=es)
* [Documentación del SDK móvil de Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
