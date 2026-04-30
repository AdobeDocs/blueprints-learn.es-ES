---
title: '[!DNL Journey Optimizer]: mensaje activado y modelo de Adobe Experience Platform'
description: Ejecute mensajes y experiencias activadas con Adobe Experience Platform como sistema centralizado de transmisión de datos, perfiles de cliente y segmentación.
solution: Journey Optimizer
exl-id: 70573eb9-cd69-4fe6-b2ae-dae81665a308
TQID: https://experienceleague.adobe.com/MuodOvJ52G9lmUAmsuj06q1aTXkRg7W0Bj6nxLp96N8
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
feature_v2:
  - id: a653cc2e-bc85-4353-a306-399e5b247978
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
  - id: fe338112-e2ce-4876-8989-fc4d497613f1
  - id: fe96aceb-8194-4a8a-a6b0-75302d02804d
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 357
ht-degree: 12%

---

# [!DNL Journey Optimizer] - Modelo de Recorrido

>[!TIP]
>Este modelo también está disponible como [patrón de caso de uso](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) en Administración y orquestación de campañas.

Los Recorridos de Adobe Journey Optimizer son flujos de trabajo en tiempo real impulsados por eventos que ofrecen experiencias personalizadas de varios pasos basadas en los comportamientos individuales de los clientes. Admiten una amplia gama de canales, incluidos correo electrónico, SMS, notificaciones push, mensajería en la aplicación, experiencias basadas en código e integraciones personalizadas basadas en API que permiten a las marcas interactuar con los clientes de forma contextual en sus puntos de contacto preferidos.

<br>

## Arquitectura

<img src="images/ajo-journeys-architecture.svg" alt="Arquitectura de referencia Adobe Journey Optimizer: modelo para Recorridos" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Consideraciones arquitectónicas para los Recorridos

- **Actualización de perfil**: los Recorridos de AJO dependen de las actualizaciones en tiempo real del perfil del cliente. Asegúrese de que las fuentes de datos que se alimentan de Adobe Experience Platform (AEP) estén configuradas para una ingesta de baja latencia a fin de mantener la precisión del perfil.
- **Procesamiento de eventos escalable:** Asegúrese de que la infraestructura pueda gestionar grandes volúmenes de déclencheur de recorrido y envío de mensajes.
- **Integración modular:** Diseñe API y acciones personalizadas para conectar AJO con sistemas externos para una personalización dinámica.
- **Resolución de identidad**: La vinculación precisa de las identidades de los clientes entre dispositivos y canales es fundamental. Las identidades mal alineadas pueden provocar recorridos rotos o mal dirigidos.
- **Tiempo de calificación de segmentos**: los recorridos basados en audiencias dependen del abono a segmentos. Comprenda con qué frecuencia se evalúan los segmentos y cómo ese tiempo afecta a la entrada y personalización de recorridos.
- **Condiciones de entrada de Recorrido**: los perfiles deben cumplir unas condiciones específicas para poder introducir un recorrido. Estas condiciones deben diseñarse cuidadosamente para evitar exclusiones o superposiciones no deseadas.
- **Evaluación de audiencias y latencia**: Los pasos para leer audiencias dependen de las evaluaciones de segmentos realizadas en Adobe Experience Platform, lo que puede no ocurrir en tiempo real. Los arquitectos tienen recorridos con conocimiento de la frecuencia y latencia de la evaluación para evitar retrasos en la calificación de audiencias y garantizar una personalización oportuna.

<br>

## Guardas

[Vínculo del producto de protecciones [!DNL Journey Optimizer]](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[Protecciones y guía de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

<br>

## Documentación relacionada

- [Documentación de [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
- [Documentación de etiquetas [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
- [Documentación de [!DNL Experience Platform Mobile SDK]](https://experienceleague.adobe.com/docs/mobile.html)
- [Documentación de [!DNL Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
- [[!DNL Journey Optimizer] descripción del producto](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)
