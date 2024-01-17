---
title: Modelo de Campaign v8, Campaign y Platform
description: Adobe Campaign v8 es la herramienta de campañas de próxima generación diseñada para canales de marketing tradicionales como correo electrónico y correo directo. Proporciona sólidas capacidades de ETL y administración de datos para ayudar a diseñar y depurar la campaña perfecta. Su motor de orquestación proporciona programas de marketing multitáctil enriquecidos con un enfoque central en los recorridos impulsados por lotes. También viene acompañado de un servidor de mensajería en tiempo real escalable que permite a los equipos de marketing enviar mensajes predefinidos basados en una carga útil inclusiva de cualquier sistema de TI para cosas como restablecimiento de contraseña, confirmación de pedido, recepción electrónica y mucho más.
solution: Campaign,Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: ac6e27e88854f5a05a7ff7428cd4375b3532f632
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 95%

---

# Modelo de Campaign v8

Adobe Campaign v8 es la herramienta de campañas de próxima generación diseñada para canales de marketing tradicionales como correo electrónico y correo directo. Proporciona sólidas capacidades de ETL y administración de datos para ayudar a diseñar y depurar la campaña perfecta. Su motor de orquestación proporciona programas de marketing multitáctil enriquecidos con un enfoque central en los recorridos impulsados por lotes. También viene acompañado de un servidor de mensajería en tiempo real escalable que permite a los equipos de marketing enviar mensajes predefinidos basados en una carga útil inclusiva de cualquier sistema de TI para cosas como restablecimiento de contraseña, confirmación de pedido, recepción electrónica y mucho más.

<br>

## Casos de uso

* Programas de mensajería basados en lotes muy complejos
* Campañas de incorporación y remarketing
* Campañas de publicidad, folletos y revistas del correo directo
* Mensajes transaccionales simples (es decir, restablecimiento de contraseña, recibos de correo electrónico, confirmaciones de pedidos, etc.)
* Integración de datos de Campaign en Adobe Experience Platform para análisis y creación de perfiles
* Uso compartido de audiencias de Real-Time Customer Data Platform con Campaign.

<br>

## Diagramas de arquitectura

Obtenga más información acerca de los modelos de implementación de Campaign v8 en [esta página](https://experienceleague.adobe.com/docs/campaign/campaign-v8/config/architecture/architecture.html#ac-deployment){target="_blank"}.

### Implementación de Campaign Enterprise (FDAC)

<img src="assets/P4-architecture.png" alt="Arquitectura de referencia para el modelo de Campaign v8 (P4)" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />


### Implementación de FDA de Campaign v8

<img src="assets/P1-P3-architecture.png" alt="Arquitectura de referencia para el modelo de Campaign v8 (P1-P3)" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Patrones de integración

| Escenario | Descripción | Competencias |
| :-- | :--- | :--- |
| [Real-Time Customer Data Platform con Adobe Campaign](rtcdp-and-campaign-v8.md) | Muestra cómo se puede utilizar el perfil del cliente en tiempo real de Adobe Experience Platform y su herramienta de segmentación centralizada con Adobe Campaign para ofrecer conversaciones personalizadas | <ul><li>Uso compartido de perfiles y audiencias de Real-Time CDP con Adobe Campaign mediante el uso del intercambio de archivos de almacenamiento en la nube y los flujos de trabajo de ingesta de Adobe Campaign </li><li>Comparta fácilmente los datos de entrega e interacción de las conversaciones de los clientes con Real-Time CDP desde Adobe Campaign para mejorar el perfil del cliente en tiempo real y proporcionar informes multicanal en campañas de mensajería</li></ul> |
| [Journey Optimizer con Adobe Campaign](ajo-and-campaign.md) | Muestra cómo puede utilizar Adobe Journey Optimizer para orquestar experiencias 1:1 utilizando el perfil del cliente en tiempo real y aprovechar el sistema de mensajería transaccional nativo de Adobe Campaign para enviar el mensaje | Aproveche Real-Time Customer Profile y la potencia de Journey Optimizer para orquestar en el momento las experiencias mientras utiliza las capacidades nativas de mensajería en tiempo real de Adobe Campaign para realizar la comunicación de último momento<br><br>Consideraciones:<br><ul><li>Se pueden enviar hasta 1 millón de mensajes por hora a través del servidor de mensajes en tiempo real<li>No se establece ninguna limitación desde Journey Optimizer, por lo que debe asegurarse de que un arquitecto empresarial de preventas realice una comprobación técnica</li><li>Gestión de decisiones no se admite en cargas útiles a Campaign v8</li></ul> |

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

* El almacenamiento se puede ampliar a 200 millones de perfiles con capacidad para escalar hasta perfiles 1B
* Configuración y control del acceso de los usuarios mediante Adobe Admin Console
* Se espera que la carga de datos en Campaign se realice mediante archivos por lotes
   * La compatibilidad con la carga de datos de API se utiliza principalmente para administrar perfiles u objetos simples dentro de la base de datos (es decir, crear y actualizar). No se pretende utilizar para cargar grandes volúmenes de datos u operaciones similares a lotes.
   * No se admite el uso de API para leer datos con fines de aplicación personalizados
   * Los datos cargados mediante API se almacenan en la base de datos de la aplicación y, a continuación, se replican cada hora en la base de datos de Cloud
* Se aplican límites a las llamadas API. Obtenga más información en la [Descripción del producto de Adobe Campaign](https://helpx.adobe.com/es/legal/product-descriptions/adobe-campaign-managed-cloud-services.html){target="_blank"}.

### Tamaño del servidor de mensajería por lotes

* Se puede escalar para gestionar hasta 20 millones de mensajes por hora

### Tamaño del servidor de mensajería en tiempo real

* Se pueden enviar hasta 1 millón de mensajes por hora
* De forma predeterminada, se aprovisionan dos servidores de mensajería en tiempo real. Capacidad para ampliar hasta ocho servidores de mensajería en tiempo real.

### Configuración de SMS

* Campaign ofrece la capacidad de integrarse con un proveedor de SMS. El cliente adquiere el proveedor y lo integra con la campaña para enviar mensajes basados en SMS
* La compatibilidad se realiza a través del protocolo SMPP
* Hay tres (3) tipos diferentes de SMS que puede soportar Adobe:
   * SMS MT (móvil finalizado): un SMS emitido por Adobe Campaign a los teléfonos móviles a través del proveedor SMPP.
   * SMS MO (móvil originado): un SMS que un móvil envía a Adobe Campaign a través del proveedor SMPP.
   * SMS SR (informe de estado), DR o DLR (recibo de envío): un recibo devuelto enviado por el móvil a Adobe Campaign a través del proveedor SMPP que indica que el SMS se ha recibido correctamente. Adobe Campaign también puede recibir SR para indicar que el mensaje no se ha podido entregar, a menudo con una descripción del error.

## Pasos de implementación

Consulte la guía de introducción para la [Implementación de Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=es)


## Documentación relacionada

* [Documentación de Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html)
* [Descripción del producto Campaign v8](https://helpx.adobe.com/es/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/launch.html)
* [Documentación del SDK móvil de Experience Platform](https://experienceleague.adobe.com/docs/mobile.html)
