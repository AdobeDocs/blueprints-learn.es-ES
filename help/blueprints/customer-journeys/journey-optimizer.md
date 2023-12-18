---
title: Journey Optimizer - Modelo de mensajería activada y Adobe Experience Platform
description: Ejecute mensajes y experiencias activadas con Adobe Experience Platform como sistema centralizado de transmisión de datos, perfiles de cliente y segmentación.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: 5f9384abe7f29ec764428af33c6dd1f0a43f5a89
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 97%

---

# modelos de Journey Optimizer

Adobe Journey Optimizer es un sistema diseñado específicamente para que los equipos de marketing reaccionen en tiempo real a los comportamientos de los clientes y se dirijan a ellos dondequiera que estén. Las funcionalidades de gestión de datos se han trasladado a Adobe Experience Platform, lo que permite a los equipos de marketing centrarse en lo mejor saben: generar conversaciones personalizadas y de recorrido del cliente de primera clase. Este modelo describe las capacidades técnicas de la aplicación y proporciona información detallada de los distintos componentes arquitectónicos que forman Adobe Journey Optimizer.

<br>

## Casos de uso

* Mensajes activados
* Confirmaciones de bienvenida y registro
* Abandonos del carro de compras y formulario de solicitud
* Mensajería activada por localización
* Experiencias en el estadio
* Experiencias de viaje y hospitalidad antes de la llegada y estancia

<br>

## Arquitectura

<img src="assets/ajo-architecture.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Escenarios de modelo

| Escenario | Descripción | Competencias |
| :-- | :--- | :--- |
| [Mensajería de terceros](3rd-party-messaging.md) | Muestra cómo se puede utilizar Adobe Journey Optimizer con sistemas de mensajería de terceros para organizar y enviar comunicaciones personalizadas | Entregue comunicaciones personalizadas 1:1 en el momento a los clientes a medida que interactúan con su marca o empresa<br><br>Consideraciones:<br><ul><li>El sistema de terceros debe admitir tokens de portador para la autenticación</li><li>No hay compatibilidad con IP estáticas debido a la arquitectura de varios inquilinos</li><li>Tenga en cuenta las limitaciones arquitectónicas del sistema de terceros cuando se trata de llamadas API por segundo. Puede ser necesario que el cliente compre un volumen adicional del proveedor de terceros para admitir el volumen proveniente de Journey Optimizer</li><li>No admite Gestión de decisiones en mensajes o cargas útiles</li></ul> |

<br>

## Patrones de integración

| Integración | Descripción | Competencias |
| :-- | :--- | :--- |
| [Journey Optimizer con Adobe Campaign](ajo-and-campaign.md) | Muestra cómo puede utilizar Adobe Journey Optimizer para orquestar experiencias 1:1 utilizando el perfil del cliente en tiempo real y aprovechar el sistema de mensajería transaccional nativo de Adobe Campaign para enviar el mensaje | Aproveche Real-Time Customer Profile y la potencia de Journey Optimizer para orquestar en el momento las experiencias mientras utiliza las capacidades nativas de mensajería en tiempo real de Adobe Campaign para realizar la comunicación de último momento<br><br>Consideraciones:<br><ul><li>La aplicación Campaign debe estar en la v7 >21.1 o v8</li><li>Rendimiento de mensajería</li><ul><li>Campaign v7: hasta 50 000 por hora</li><li>Campaign v8: hasta 1 millón por hora</li><li>Campaign Standard: hasta 50 000 por hora</li></ul><li>No se establece ninguna limitación, por lo que los casos de uso necesitan una revisión técnica de un arquitecto empresarial</li><li>No se admite la utilización de Gestión de decisiones en el mensaje enviado por Campaign</li></ul> |

<br>

## Prerrequisitos

Adobe Experience Platform

* Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar las fuentes de datos de Journey Optimizer
* Para los esquemas basados en clases de eventos de experiencia, agregue el grupo de campos &#39;ID de evento de orquestación&#39; cuando desee que se active un evento que no sea un evento basado en reglas
* Para los esquemas basados en clases de perfil individual, agregue el grupo de campos &#39;Detalles de prueba de perfil&#39; para poder cargar perfiles de prueba para utilizarlos con Journey Optimizer

Correo electrónico

* Debe tener un subdominio listo para utilizarse en el envío de mensajes
* El subdominio se puede delegar completamente a Adobe (recomendado) o se pueden usar CNAME para señalar a servidores DNS específicos de Adobe (personalizado)
* Se necesita el registro TXT de Google para cada subdominio para garantizar una buena entrega

Push móvil

* El cliente debe tener un desarrollador móvil disponible para generar la aplicación
* SDK móvil de Adobe Experience Platform

<br>

## Guardas

[Vínculo del producto de guardas de Journey Optimizer](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html)

[Protecciones y guía de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## Documentación relacionada

* [Documentación de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Documentación de las etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
* [Documentación del SDK móvil de Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
* [Documentación de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es)
* [Descripción del producto Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
