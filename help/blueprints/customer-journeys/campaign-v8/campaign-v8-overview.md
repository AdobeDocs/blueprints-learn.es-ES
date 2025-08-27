---
title: Modelo, Campaign y plataforma de Campaign v8
description: Obtenga información acerca del modelo para Campaign v8.
solution: Campaign,Campaign v8
version: Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: 0a3ebcbc6029df46bd988cb8f15ecf838f80c3c9
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 31%

---

# Modelo de Campaign v8

Adobe Campaign v8 es una plataforma de administración de campañas de próxima generación diseñada para canales de marketing tradicionales como correo electrónico y correo directo. Ofrece sólidas capacidades de ETL y administración de datos para admitir segmentación compleja y segmentación de audiencias, además de un potente motor de orquestación para crear programas de marketing multitáctil y por lotes.

También incluye un servidor de mensajería en tiempo real escalable que permite las comunicaciones transaccionales (como restablecimientos de contraseña, confirmaciones de pedidos y recibos electrónicos) mediante la aceptación de cargas útiles completas de sistemas externos para su entrega inmediata.

## Casos de uso

>[!BEGINTABS]

>[!TAB Ejecución de campañas por lotes]

- Diseñe y entregue campañas de marketing programadas a gran escala a través de correo electrónico, SMS y correo directo.
- Ideal para promociones, boletines informativos y ofertas de temporada con segmentación y direccionamiento complejos.

>[!TAB Orquestación multitáctil]

- Cree programas de varios pasos y canales que guíen a los clientes a través de un recorrido de marketing predefinido.
- Admite la reentrada de audiencias, lógica condicional y transiciones basadas en el tiempo.

>[!TAB Administración de datos y ETL]

- Ingeste, transforme y administre datos de clientes de varias fuentes para admitir un direccionamiento preciso.
- Permite la creación de esquemas personalizados, campos calculados y definiciones de audiencia.

>[!TAB Mensajería transaccional]

- Envíe mensajes predefinidos en tiempo real activados por sistemas externos (por ejemplo, restablecimientos de contraseña, confirmaciones de pedidos, recibos electrónicos).
- Utiliza un servidor de mensajería escalable que acepta cargas útiles completas de sistemas informáticos para su entrega inmediata.

>[!ENDTABS]

<br>

## Diagramas de arquitectura

Obtenga más información acerca de [modelos de implementación de Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/config/architecture/architecture.html#ac-deployment){target="_blank"}.

### Implementación empresarial de Campaign (FDAC)

<img src="images/campaign-v8-ffda.svg" alt="Arquitectura de referencia para el modelo de implementación de Campaign v8 (FDAC)" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

### Implementación de FDA de Campaign v8

<img src="images/campaign-v8-fda.svg" alt="Arquitectura de referencia para el modelo de Campaign v8 (FDA)" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Patrones de integración

| Escenario | Descripción | Consideraciones técnicas |
| :-- | :--- | :--- |
| [[!DNL Real-time Customer Data Platform] con Adobe [!DNL Campaign]](rtcdp-and-campaign-v8.md) | Muestra cómo Adobe Experience Platform y su herramienta de segmentación centralizada y el Perfil del cliente en tiempo real se pueden utilizar con Adobe [!DNL Campaign] para ofrecer conversaciones personalizadas | <ul><li>Uso compartido de perfiles y audiencias de [!DNL Real-Time CDP] en Adobe [!DNL Campaign] mediante el uso del intercambio de archivos de almacenamiento en la nube y los flujos de trabajo de ingesta de Adobe [!DNL Campaign] </li><li>Comparta fácilmente datos de interacción y envío de las conversaciones con los clientes en [!DNL Real-Time CDP] desde Adobe [!DNL Campaign] para mejorar tanto el perfil del cliente en tiempo real como para proporcionar informes multicanal sobre las campañas de mensajería</li></ul> |
| [[!DNL Journey Optimizer] con Adobe [!DNL Campaign]](ajo-and-campaign-v8.md) | Muestra cómo puede usar Adobe Journey Optimizer para orquestar experiencias de 1:1 mediante el Perfil del cliente en tiempo real y aprovechar el sistema nativo de mensajería transaccional de Adobe [!DNL Campaign] para enviar el mensaje | <ul><li>Se pueden enviar hasta 1 millón de mensajes por hora a través del servidor de mensajes en tiempo real<li>No se realiza ninguna restricción desde [!DNL Journey Optimizer]. Asegúrese de que un arquitecto de empresa de preventa realice un examen técnico</li><li>Gestión de decisiones no se admite en cargas útiles a Campaign v8</li></ul> |

<br>

## Prerrequisitos

Los siguientes requisitos previos existen para este modelo.

### Servidor de aplicaciones y servidor de mensajería en tiempo real

- La consola del cliente de Adobe [!DNL Campaign] es necesaria para interactuar y utilizar el software [!DNL Campaign] v8. Es un cliente basado en Windows y utiliza protocolos de Internet estándar (SOAP, HTTP, etc.). Asegúrese de que tiene los permisos necesarios activados en la organización para distribuir, instalar y ejecutar software

- Lista de direcciones IP permitidas:
   - Identifique los rangos IP que todos los usuarios aprovechan durante el acceso a la consola del cliente.
   - Identifique qué sistemas empresariales pueden comunicarse con el servidor de mensajería en tiempo real y asegúrese de que tengan una IP o un intervalo asignado estáticamente que pueda incluir en la lista de permitidos.
   - Esto se puede configurar y controlar mediante el panel de control de Campaign.
- Administración de claves sFTP:
   - Tenga a disposición claves públicas SSH para su uso con el sFTP proporcionado por Campaign. Esto se puede configurar y controlar mediante el panel de control de Campaign.

### Correo electrónico

- Tenga un subdominio listo para utilizarlo para el envío de mensajes.
- El subdominio se puede delegar completamente a Adobe (recomendado) o se pueden utilizar CNAME para señalar a servidores DNS específicos de Adobe (personalizados).
- Se necesita el registro TXT de Google para cada subdominio a fin de garantizar una buena entrega.

### Push móvil

- Pida a un desarrollador móvil disponible para implementar, configurar y crear la aplicación móvil.
- Adobe solo proporciona un SDK para recopilar la información necesaria de FCM (Android) y APNS (iOS) para enviar cargas de mensajes a sus servidores. La manera en que la aplicación móvil debe codificarse, implementarse, administrarse y depurarse es responsabilidad del cliente.

### Aplicaciones web (opcional)

- Puede delegar un subdominio adicional para las páginas de cancelación de suscripción y aterrizaje alojadas en Campaign.
- Se recomienda encarecidamente el certificado SSL.

<br>

## Guardas

### Tamaño del servidor de aplicaciones

- El almacenamiento se puede ampliar a hasta 200 millones de perfiles con potencial de ampliación a perfiles 1B.
- Configure y controle el acceso de usuarios a través de Adobe [!DNL Admin Console].
- Se espera que la carga de datos en [!DNL Campaign] se realice mediante archivos por lotes:
   - La compatibilidad con la carga de datos de API se utiliza principalmente para administrar perfiles u objetos simples dentro de la base de datos (es decir, crear y actualizar). No se pretende utilizar para cargar grandes volúmenes de datos u operaciones similares a lotes.
   - No se admite el uso de API para leer datos con fines de aplicación personalizados
   - Los datos cargados mediante API se almacenan en la base de datos de la aplicación y, a continuación, se replican cada hora en la base de datos de Cloud
- Se aplican límites a las llamadas API. Obtenga más información en la [Descripción del producto de Adobe Campaign](https://helpx.adobe.com/es/legal/product-descriptions/adobe-campaign-managed-cloud-services.html){target="_blank"}.

### Tamaño del servidor de mensajería por lotes

- Se puede escalar para gestionar hasta 20 millones de mensajes por hora

### Tamaño del servidor de mensajería en tiempo real

- Se pueden enviar hasta 1 millón de mensajes por hora
- De forma predeterminada, se aprovisionan dos servidores de mensajería en tiempo real. Capacidad para ampliar hasta ocho servidores de mensajería en tiempo real.

### Configuración de SMS

- Campaign ofrece la capacidad de integrarse con un proveedor de SMS. El proveedor es adquirido por el cliente e integrado con la campaña para enviar mensajes SMS.
- La compatibilidad se realiza mediante el protocolo SMPP.
- Hay tres (3) tipos diferentes de SMS que puede soportar Adobe:
   - SMS MT (móvil finalizado): un SMS emitido por Adobe [!DNL Campaign] hacia los teléfonos móviles a través del proveedor de SMPP.
   - SMS MO (móvil original): un SMS enviado por un móvil a Adobe [!DNL Campaign] a través del proveedor de SMPP.
   - SMS SR (informe de estado) o DR o DLR (recibo de envío): un recibo de devolución enviado por el móvil a Adobe [!DNL Campaign] a través del proveedor de SMPP que indica que el SMS se ha recibido correctamente. Adobe [!DNL Campaign] también puede recibir SR indicando que el mensaje no se pudo entregar, a menudo con una descripción del error.

<br>

## Pasos de implementación

Consulte la guía de introducción para la [Implementación de Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html)

## Documentación relacionada

- [Documentación de Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html)
- [Descripción del producto Campaign v8](https://helpx.adobe.com/es/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
- [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/launch.html)
- [Documentación del SDK móvil de Experience Platform](https://experienceleague.adobe.com/docs/mobile.html)