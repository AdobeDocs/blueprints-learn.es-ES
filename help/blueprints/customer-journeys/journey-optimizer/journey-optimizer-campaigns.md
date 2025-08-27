---
title: '[!DNL Journey Optimizer] - Orquestación de campaña'
description: Permite a los especialistas en marketing coordinar comunicaciones de marketing programadas, basadas en audiencias y de varios pasos entre canales de mensajería salientes.
solution: Journey Optimizer
source-git-commit: 0a3ebcbc6029df46bd988cb8f15ecf838f80c3c9
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 2%

---

# [!DNL Journey Optimizer] - Modelo de orquestación de campaña

AJO Campaign Orchestration permite a los especialistas en marketing diseñar y ejecutar comunicaciones programadas, basadas en audiencias y de varios pasos en canales salientes como correo electrónico, SMS, push y correo directo. A diferencia de los Recorridos de AJO, que reaccionan a los comportamientos individuales de los clientes utilizando datos en tiempo real del Perfil del cliente en tiempo real, las campañas son esfuerzos de marketing coordinados que se dirigen a audiencias a intervalos planificados. Juntas, las campañas y los recorridos ofrecen enfoques complementarios: las campañas impulsan las estrategias de participación de la marca, mientras que los recorridos ofrecen experiencias personalizadas y adaptables.

<br>

## Arquitectura

<img src="images/ajo-campaigns-architecture.svg" alt="Arquitectura de referencia Modelo de orquestación de Adobe Journey Optimizer Campaign" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

### Arquitectura de ejecución de mensajes

<img src="images/ajo-campaigns-message-sending-architecture.png" alt="Arquitectura de referencia Modelo de orquestación de Adobe Journey Optimizer Campaign" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

### Almacenamiento relacional: latencia de ingesta de datos

<img src="images/ajo-campaigns-data-ingestion-architecture.png" alt="Arquitectura de referencia Modelo de orquestación de Adobe Journey Optimizer Campaign" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Consideraciones arquitectónicas para los Recorridos

- **Arquitectura de datos**: AJO Campaign Orchestration utiliza una base de datos relacional para la creación y organización de audiencias
- **Integración de Audience Portal**: integrado de forma nativa con Audience Portal dentro del Perfil del cliente en tiempo real para leer audiencias existentes y guardar nuevas audiencias en al crear campañas
- **Creación de audiencias a petición**: cree, evalúe y ejecute una audiencia inmediatamente para casos de uso de marketing urgentes
- **Integración de perfil del cliente en tiempo real:** fuente fiable para el historial de consentimientos y comunicaciones; admite el diseño de &#39;perfil delgado&#39; para la personalización
- **Envío de mensajes de varias entidades:** capacidad para enviar varios mensajes por perfil en una sola entrega (por ejemplo, enviar un mensaje por reserva a la dirección de correo electrónico del cliente)
- **Segmentación de varias entidades**: empiece a crear una audiencia a partir de cualquier entidad del almacén relacional (es decir, producto, inventario, plan, etc.)

<br>

## Guardas

[Vínculo de producto de campañas orquestadas](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/guardrails)

[Protecciones y guía de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails)

<br>

## Documentación relacionada

- [[!DNL Journey Optimizer] Campañas orquestadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/orchestrated-campaigns-landing-page.html)
- [[!DNL Experience Platform] documentación](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
- [[!DNL Experience Platform] Documentación de etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
- [[!DNL Experience Platform Mobile SDK] documentación](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
- [[!DNL Journey Optimizer] documentación](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es)
- [[!DNL Journey Optimizer] descripción del producto](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)