---
title: Modelo de Campaign v8
description: Adobe Campaign v8 es la herramienta de campañas de próxima generación diseñada para canales de marketing tradicionales como correo electrónico y correo postal. Proporciona sólidas capacidades de ETL y administración de datos para ayudar a diseñar y depurar la campaña perfecta. Su motor de orquestación proporciona programas de marketing multitáctil enriquecidos con un enfoque central en los recorridos impulsados por lotes.  También viene acompañado de un servidor de mensajería en tiempo real escalable que permite a los equipos de marketing enviar mensajes predefinidos basados en una carga útil inclusiva de cualquier sistema de TI para cosas como restablecimiento de contraseña, confirmación de pedido, recepción electrónica y mucho más.
solution: Campaign v8
hidefromtoc: true
exl-id: f754d099-6842-4759-8e27-6a06d5d8c2e9
source-git-commit: 13f750c0ff820ab01ed4fc615aba864bc2dc7b75
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 3%

---

# Modelo de Campaign v8

Adobe Campaign v8 es la herramienta de campañas de próxima generación diseñada para canales de marketing tradicionales como correo electrónico y correo postal. Proporciona sólidas capacidades de ETL y administración de datos para ayudar a diseñar y depurar la campaña perfecta. Su motor de orquestación proporciona programas de marketing multitáctil enriquecidos con un enfoque central en los recorridos impulsados por lotes.  También viene acompañado de un servidor de mensajería en tiempo real escalable que permite a los equipos de marketing enviar mensajes predefinidos basados en una carga útil inclusiva de cualquier sistema de TI para cosas como restablecimiento de contraseña, confirmación de pedido, recepción electrónica y mucho más.

<br>

## Casos de uso

* Programas de mensajería basados en lotes muy complejos
* Campañas de incorporación y remarketing
* Campañas de publicidad, folletos y revistas de Direct Mail
* Mensajería transaccional simple (es decir, restablecimiento de contraseña, recibos de correo electrónico, confirmaciones de pedidos, etc.)

<br>

## Arquitectura

<img src="assets/campaign-v8-architecture.svg" alt="Arquitectura de referencia para Campaign v8 Blueprint" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Escenarios de modelo

| Escenario | Descripción | Competencias |
| :-- | :--- | :--- |
| [Journey Optimizer con Adobe Campaign](ajo-and-campaign.md) | Muestra cómo puede utilizar Adobe Journey Optimizer para orquestar experiencias 1:1 utilizando el Perfil del cliente en tiempo real y aprovechar el sistema de mensajería transaccional nativo de Adobe Campaign para enviar el mensaje | Aproveche el perfil de cliente en tiempo real y la potencia de Journey Optimizer para orquestar en el momento las experiencias mientras utiliza las capacidades nativas de mensajería en tiempo real de Adobe Campaign para realizar la comunicación de última milla<br><br>Consideraciones:<br><ul><li>Pueden enviar hasta 1 M mensajes por hora a través del servidor de mensajes en tiempo real<li>No se realiza ninguna limitación desde Journey Optimizer, por lo que debe asegurarse de que un arquitecto de empresa de pre-ventas realice una comprobación técnica</li><li>El offer decisioning no se admite en cargas útiles a Campaign v8</li></ul> |

<br>

## Prerrequisitos


### Servidor de aplicaciones y servidor de mensajería en tiempo real

* La consola de cliente de Adobe Campaign es necesaria para interactuar y utilizar el software de Campaign v8. Es un cliente basado en Windows y utiliza protocolos de Internet estándar (SOAP, HTTP, etc.). Asegúrese de que tiene los permisos necesarios activados en la organización para distribuir, instalar y ejecutar software

* Listado de direcciones IP permitidas
   * Identificar los rangos de IP que todos los usuarios aprovecharán durante el acceso a la consola del cliente
   * Identificar qué sistemas empresariales podrán hablar con el servidor de mensajería en tiempo real y asegurarse de que tienen una IP o un rango asignado estáticamente que se puede lista de permitidos
   * Esto se puede configurar y controlar mediante el Panel de control de Campaign de Campaign
* Administración de claves sFTP
   * Tenga a disposición claves públicas SSH para su uso con el SFTP proporcionado por la campaña. Esto se puede configurar y controlar mediante el Panel de control de Campaign de Campaign.

### Correo electrónico

* Tener un subdominio listo para utilizarse para el envío de mensajes
* El subdominio se puede delegar completamente a Adobe (recomendado) o se pueden usar CNAME para señalar a servidores DNS específicos de Adobe (personalizado)
* Se necesita el registro TXT de Google para cada subdominio para garantizar una buena entrega

### Push móvil

* Tenga a un desarrollador móvil disponible para implementar, configurar y crear la aplicación móvil
* Adobe solo proporciona un SDK para recopilar la información necesaria de FCM (Android) y APNS (iOS) para enviar cargas de mensajes a sus servidores. La responsabilidad del cliente es cómo debe codificarse, implementarse, administrarse y depurarse la aplicación móvil

### Aplicaciones web (opcional)

* Puede delegar un subdominio adicional para las páginas de aterrizaje y cancelación de suscripción alojadas en Campaign
* Se recomienda encarecidamente el certificado SSL

<br>

## Guardas

### Tamaño del servidor de aplicaciones

* El almacenamiento se puede ampliar a 200 millones de perfiles con capacidad para escalar hasta perfiles 1B
* Configuración y control del acceso de los usuarios mediante Adobe Admin Console
* Se espera que la carga de datos en Campaign se realice mediante archivos por lotes
   * La compatibilidad con la carga de datos de API se utiliza principalmente para administrar perfiles u objetos simples dentro de la base de datos (es decir, crear y actualizar). No se pretende utilizar para cargar grandes volúmenes de datos u operaciones similares a lotes.
   * No se admite el uso de API para leer datos con fines de aplicación personalizados
   * Los datos cargados mediante API se almacenan en la base de datos de la aplicación y, a continuación, se replican cada hora en la base de datos de Cloud
* Las llamadas de API están limitadas a 15 por segundo o a 150 k por día a escala

### Tamaño del servidor de mensajería por lotes

* Se puede escalar para gestionar hasta 20 millones de mensajes por hora

### Tamaño del servidor de mensajería en tiempo real

* Pueden enviar hasta 1 millón de mensajes por hora
* De forma predeterminada, solo se aprovisiona un (1) servidor de mensajería en tiempo real. Esto sirve para garantizar que cualquier comunicación con el servidor se realice mediante un token de sesión que caduque en 24 horas
* De forma opcional, puede implementar hasta ocho (8) servidores de mensajería en tiempo real, pero la autenticación solo es compatible con user/pass
* El método recomendado siempre es utilizar un servidor de mensajería en tiempo real para aprovechar la autenticación basada en token de sesión siempre que sea posible

### Configuración de SMS

* Campaign ofrece la capacidad de integrarse con un proveedor de SMS. El cliente adquiere el proveedor y lo integra con la campaña para enviar mensajes basados en SMS
* La compatibilidad se realiza a través del protocolo SMPP
* Hay tres (3) tipos diferentes de SMS que el Adobe puede soportar:
   * SMS MT (móvil finalizado): un SMS emitido por Adobe Campaign hacia los teléfonos móviles a través del proveedor SMPP.
   * SMS MO (móvil originado): un SMS que un móvil envía a Adobe Campaign a través del proveedor SMPP.
   * SMS SR (informe de estado), DR o DLR (recibo de envío): un recibo devuelto enviado por el móvil a Adobe Campaign a través del proveedor SMPP que indica que el SMS se ha recibido correctamente. Adobe Campaign también puede recibir SR para indicar que el mensaje no se ha podido entregar, a menudo con una descripción del error.

### Configuración push móvil

* Solo se admite el SDK de Campaign para Campaign v8. Póngase en contacto con el Servicio de atención al cliente de Adobe para obtener acceso
* Siga las [Documentación del SDK de Campaign](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=en) para aprender a instalar y configurar el SDK

   >[!IMPORTANT]
   >Otras aplicaciones de Experience Cloud requerirán el uso del SDK móvil de Experience Platform para la recopilación de datos. Se trata de un SDK diferente y deberá instalarse junto al SDK de Campaign

<br>

## Pasos de implementación

Consulte la guía de introducción para [Implementación de Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=en)


## Documentación relacionada

* [Documentación de Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=en)
* [Descripción del producto Campaign v8](https://helpx.adobe.com/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/launch.html?lang=es)
* [Documentación del SDK Experience Platform Mobile](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
