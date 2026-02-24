---
title: '[!DNL Journey Optimizer] - Modelo de Recorrido'
description: Ejecute mensajes y experiencias activadas con Adobe Experience Platform como sistema centralizado de transmisión de datos, perfiles de cliente y segmentación.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: 49251caac58cd8f62dff977f94ea6a716aa94250
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 15%

---

# [!DNL Journey Optimizer] modelos

Adobe [!DNL Journey Optimizer] es una aplicación nativa de la nube creada en Adobe Experience Platform que permite la organización en tiempo real y programada de los recorridos de los clientes en varios canales. Admite déclencheur impulsados por eventos, segmentación de audiencia y servicios de toma de decisiones para ofrecer experiencias personalizadas mediante correo electrónico, SMS, push, web y mensajería en la aplicación. Se integra con los sistemas entrantes y salientes, lo que permite una administración unificada del estado de la audiencia y una participación contextual en todo el ciclo de vida del cliente.

Este modelo describe las capacidades técnicas de la aplicación y proporciona una explicación detallada de los distintos componentes de arquitectura que conforman [!DNL Journey Optimizer].

<br>

## Casos de uso

>[!BEGINTABS]
>[!TAB Recorrido (Impulsado Por Eventos, En Tiempo Real)]

- **Recuperación de abandono:** Déclencheur mensajes personalizados cuando un usuario abandona un carro de compras, un formulario o una sesión por correo electrónico, push o en la aplicación.
- **Registro de nuevo usuario:** Capte a nuevos usuarios inmediatamente después de que se registren con nuevas preferencias de cuenta, promociones relevantes o beneficios
- **Mensajería transaccional:** Envíe confirmaciones, alertas o actualizaciones en tiempo real (por ejemplo, pedidos enviados, restablecimiento de contraseña) mediante déclencheur de evento.
- **Segmentación contextual:** Comuníquese con usuarios en el momento según sus señales y ubicación para guiar y dirigir su experiencia
- **Ampliación de venta/Venta cruzada contextual:** Entrega ofertas personalizadas basadas en atributos de perfil en tiempo real e interacciones recientes.

>[!TAB Orquestación de campaña (programada, iniciada con la marca)]

- **Campañas promocionales**: inicia campañas multicanal de varios pasos para lanzamientos de productos, ofertas de temporada o eventos de ventas.
- **Marketing durante el ciclo vital**: Automatice campañas recurrentes como mensajes de cumpleaños, recordatorios de renovación o hitos de lealtad.
- **Funnel basado en audiencias inserta**: Segmente y envíe audiencias a campañas estructuradas basadas en lógica empresarial o atributos CRM.
- **Boletín y distribución de contenido**: programa y entrega de contenido personalizado a audiencias de destino a través de correo electrónico y móviles.
- **Campañas de renovación de la participación**: identifique a los usuarios inactivos y vuelva a introducirlos en los flujos de participación según los umbrales de inactividad.

>[!ENDTABS]

<br>

## Arquitectura

<img src="images/ajo-architecture.svg" alt="Arquitectura de referencia Modelo de Adobe Journey Optimizer" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Escenarios de modelo

| Escenario | Descripción |
| :-- | :-- |
| [Recorridos](journey-optimizer-journeys.md) | Los Recorridos de AJO en Adobe Journey Optimizer son experiencias del cliente automatizadas y personalizadas activadas por eventos en tiempo real o segmentos de audiencia, lo que permite a los especialistas en marketing enviar mensajes relevantes a través de canales como correo electrónico, SMS y notificaciones push. |
| [Orquestación de campaña](journey-optimizer-campaigns.md) | AJO Campaign Orchestration permite a los especialistas en marketing diseñar y ejecutar campañas personalizadas en canales múltiples utilizando datos en tiempo real y perspectivas de audiencia. Admite direccionamiento dinámico, envío de mensajes y lógica de recorrido para optimizar la participación de los clientes en los canales de correo electrónico, SMS, push y personalizados. |

<br>

## Patrones de integración

| Integración | Descripción | Consideraciones técnicas |
| :-- | :-- | :-- |
| [Mensajería de terceros](3rd-party-messaging.md) | Muestra cómo Adobe [!DNL Journey Optimizer] se puede integrar con plataformas de mensajería de terceros para organizar y ofrecer comunicaciones personalizadas con los clientes. | <ul><li>El sistema de terceros debe admitir **autenticación de token de portador**</li><li>**No se admiten direcciones IP estáticas** debido a la arquitectura de varios inquilinos.</li><li>Tenga en cuenta los **límites de tasa de API** en sistemas de terceros; es posible que los clientes necesiten adquirir capacidad adicional para controlar el tráfico proveniente de **Adobe Journey Optimizer**.</li><li>**Administración de decisiones** no es compatible con las cargas útiles de mensajes o la lógica de envío.</li></ul> |
| [[!DNL Journey Optimizer] con Adobe Campaign v8](../campaign-v8/ajo-and-campaign-v8.md) | Muestra cómo Adobe [!DNL Journey Optimizer] se puede integrar con las capacidades de mensajería transaccional de Adobe Campaign v8 para ejecutar el envío final de mensajes. | <ul><li>No se restringen los mensajes. Límite de 4000 mensajes por 5 minutos.</li><li>Solo admite recorridos iniciados por eventos</li><li>Gestión de decisiones no es compatible con los mensajes enviados por Campaign</li></ul> |

<br>

## Prerrequisitos

Adobe [!DNL Experience Platform]:

- Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar [!DNL Journey Optimizer] orígenes de datos
- Para los esquemas basados en clases de eventos de experiencia XDM, añada el grupo de campos ID de evento de orquestación cuando desee tener un evento activado que no sea un evento basado en reglas
- Para los esquemas basados en clases de perfiles individuales de XDM, agregue el grupo de campos &quot;Detalles de la prueba de perfil&quot; para poder cargar perfiles de prueba para usarlos con [!DNL Journey Optimizer]

<br>

Correo electrónico:

- Debe tener un subdominio listo para utilizarse en el envío de mensajes
- El subdominio se puede delegar completamente a Adobe (recomendado) o se pueden usar CNAME para señalar a servidores DNS específicos de Adobe (personalizado)
- Se necesita el registro TXT de Google para cada subdominio para garantizar una buena entrega

<br>

Inserción móvil:

- El cliente debe tener un desarrollador móvil disponible para generar la aplicación
- SDK móvil de Adobe Experience Platform

<br>

## Guardas

[[!DNL Journey Optimizer] Vínculo de producto de protecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[Protecciones y guía de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=es)

## Documentación relacionada

- [[!DNL Experience Platform] documentación](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
- [[!DNL Experience Platform] Documentación de etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
- [[!DNL Experience Platform Mobile SDK] documentación](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
- [[!DNL Journey Optimizer] documentación](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es)
- [[!DNL Journey Optimizer] descripción del producto](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)