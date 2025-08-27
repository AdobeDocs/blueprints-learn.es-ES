---
title: '[!DNL Journey Optimizer]: mensaje activado y modelo de Adobe Experience Platform'
description: Ejecute mensajes y experiencias activadas con Adobe Experience Platform como sistema centralizado de transmisión de datos, perfiles de cliente y segmentación.
solution: Journey Optimizer
source-git-commit: 0a3ebcbc6029df46bd988cb8f15ecf838f80c3c9
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 9%

---

# [!DNL Journey Optimizer] - Modelo de Recorrido

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

[[!DNL Journey Optimizer] Vínculo de producto de protecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[Protecciones y guía de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

<br>

## Documentación relacionada

- [[!DNL Experience Platform] documentación](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
- [[!DNL Experience Platform] Documentación de etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
- [[!DNL Experience Platform Mobile SDK] documentación](https://experienceleague.adobe.com/docs/mobile.html)
- [[!DNL Journey Optimizer] documentación](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
- [[!DNL Journey Optimizer] descripción del producto](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html)