---
title: Modelo de Campaign v8, Campaign y Platform
description: Obtenga información acerca del modelo para Campaign v8.
solution: Campaign,Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: 16b233c7ea9077566ebf12238f0a87beec1c61ce
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 41%

---

# Modelo de Campaign v8

Adobe Campaign v8 es la herramienta de campañas de próxima generación diseñada para canales de marketing tradicionales como correo electrónico y correo directo. Proporciona sólidas capacidades de ETL y administración de datos para ayudar a diseñar y depurar la campaña perfecta. Su motor de orquestación proporciona programas de marketing multitáctil enriquecidos con un enfoque central en los recorridos impulsados por lotes.

También viene acompañado de un servidor de mensajería en tiempo real escalable que permite a los equipos de marketing enviar mensajes predefinidos basados en una carga útil inclusiva de cualquier sistema de TI para cosas como restablecimiento de contraseña, confirmación de pedido, recepción electrónica y mucho más.

## Casos de uso

* Programas de mensajería basados en lotes muy complejos.
* Campañas de incorporación y remarketing.
* Campañas de publicidad, folletos y revistas del correo directo
* Mensajería transaccional sencilla (como restablecimiento de contraseña, recibos de correo electrónico, confirmaciones de pedidos, etc.).
* Integración de datos de Campaign en Adobe Experience Platform para análisis y generación de perfiles.
* Uso compartido de audiencias de Real-Time Customer Data Platform con Campaign.

## Diagramas de arquitectura

Más información sobre [Modelos de implementación de Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/config/architecture/architecture.html#ac-deployment){target="_blank"}.

### Implementación empresarial de Campaign (FDAC)

<img src="assets/P4-architecture.png" alt="Arquitectura de referencia para el modelo de Campaign v8 (P4)" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

### Implementación de FDA de Campaign v8

<img src="assets/P1-P3-architecture.png" alt="Arquitectura de referencia para el modelo de Campaign v8 (P1-P3)" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Patrones de integración

| Escenario | Descripción | Competencias |
| :-- | :--- | :--- |
| [[!DNL Real-time Customer Data Platform] con Adobe [!DNL Campaign]](rtcdp-and-campaign-v8.md) | Muestra cómo Adobe Experience Platform y su herramienta de segmentación centralizada y el Perfil del cliente en tiempo real se pueden utilizar con Adobe [!DNL Campaign] para ofrecer conversaciones personalizadas | <ul><li>Uso compartido de perfiles y audiencias de [!DNL Real-Time CDP] al Adobe [!DNL Campaign] mediante el uso del intercambio y el Adobe de archivos de almacenamiento en la nube [!DNL Campaign] flujos de trabajo de ingesta </li><li>Compartir fácilmente datos de interacción y envío de las conversaciones con los clientes en [!DNL Real-Time CDP] desde el Adobe [!DNL Campaign] para mejorar el Perfil del cliente en tiempo real y proporcionar informes en canales múltiples sobre campañas de mensajería</li></ul> |
| [[!DNL Journey Optimizer] con Adobe [!DNL Campaign]](ajo-and-campaign.md) | Muestra cómo puede utilizar Adobe Journey Optimizer para orquestar experiencias 1:1 utilizando el Perfil del cliente en tiempo real y aprovechar el Adobe nativo [!DNL Campaign] sistema de mensajería transaccional para enviar el mensaje | Aproveche el perfil del cliente en tiempo real y la potencia de [!DNL Journey Optimizer] para orquestar experiencias en el momento mientras se utilizan las capacidades nativas de mensajería en tiempo real de Adobe [!DNL Campaign] para realizar la comunicación de la última milla<br><br>Consideraciones:<br><ul><li>Se pueden enviar hasta 1 millón de mensajes por hora a través del servidor de mensajes en tiempo real<li>No se realiza ninguna restricción desde [!DNL Journey Optimizer] por lo tanto, asegúrese de que un arquitecto de Pre-Sales Enterprise realice el estudio técnico</li><li>Gestión de decisiones no se admite en cargas útiles a Campaign v8</li></ul> |

## Prerrequisitos

Los siguientes requisitos previos existen para este modelo.

### Servidor de aplicaciones y servidor de mensajería en tiempo real

* El Adobe [!DNL Campaign] La consola de cliente es necesaria para interactuar y utilizar [!DNL Campaign] software v8. Es un cliente basado en Windows y utiliza protocolos de Internet estándar (SOAP, HTTP, etc.). Asegúrese de que tiene los permisos necesarios activados en la organización para distribuir, instalar y ejecutar software

* Lista de direcciones IP permitidas:
   * Identifique los rangos IP que todos los usuarios aprovechan durante el acceso a la consola del cliente.
   * Identifique qué sistemas empresariales pueden comunicarse con el servidor de mensajería en tiempo real y asegúrese de que tengan una IP o un intervalo asignado estáticamente que pueda incluir en la lista de permitidos.
   * Esto se puede configurar y controlar mediante el panel de control de Campaign.
* Administración de claves sFTP:
   * Tenga a disposición claves públicas SSH para su uso con el sFTP proporcionado por Campaign. Esto se puede configurar y controlar mediante el panel de control de Campaign.

### Correo electrónico

* Tenga un subdominio listo para utilizarlo para el envío de mensajes.
* El subdominio se puede delegar completamente al Adobe (recomendado) o se pueden utilizar CNAME para señalar a servidores DNS específicos del Adobe (personalizados).
* Se necesita el registro TXT de Google para cada subdominio a fin de garantizar una buena entrega.

### Push móvil

* Pida a un desarrollador móvil disponible para implementar, configurar y crear la aplicación móvil.
* Adobe solo proporciona un SDK para recopilar la información necesaria de FCM (Android) y APNS (iOS) para enviar cargas de mensajes a sus servidores. La manera en que la aplicación móvil debe codificarse, implementarse, administrarse y depurarse es responsabilidad del cliente.

### Aplicaciones web (opcional)

* Puede delegar un subdominio adicional para las páginas de cancelación de suscripción y aterrizaje alojadas en Campaign.
* Se recomienda encarecidamente el certificado SSL.

## Guardas

Las barreras se describen a continuación.

### Tamaño del servidor de aplicaciones

* El almacenamiento se puede ampliar a hasta 200 millones de perfiles con potencial de ampliación a perfiles 1B.
* Configuración y control del acceso de los usuarios mediante el Adobe [!DNL Admin Console].
* Carga de datos en [!DNL Campaign] se espera realizar mediante archivos por lotes:
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

* Campaign ofrece la capacidad de integrarse con un proveedor de SMS. El proveedor es adquirido por el cliente e integrado con la campaña para enviar mensajes SMS.
* La compatibilidad se realiza mediante el protocolo SMPP.
* Hay tres (3) tipos diferentes de SMS que puede soportar Adobe:
   * SMS MT (móvil finalizado): un SMS emitido por el Adobe [!DNL Campaign] hacia teléfonos móviles a través del proveedor SMPP.
   * SMS MO (móvil original): un SMS que un móvil envía al Adobe [!DNL Campaign] a través del proveedor SMPP.
   * SMS SR (informe de estado) o DR o DLR (recibo de envío): un recibo de devolución enviado por el móvil al Adobe [!DNL Campaign] a través del proveedor SMPP, lo que indica que el SMS se ha recibido correctamente. Adobe [!DNL Campaign] También pueden recibir SR indicando que el mensaje no se pudo entregar, a menudo con una descripción del error.

## Pasos de implementación

Consulte la guía de introducción para la [Implementación de Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=es)

## Documentación relacionada

* [Documentación de Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html)
* [Descripción del producto Campaign v8](https://helpx.adobe.com/es/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/launch.html)
* [Documentación del SDK móvil de Experience Platform](https://experienceleague.adobe.com/docs/mobile.html)
