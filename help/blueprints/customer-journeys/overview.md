---
title: Modelos de recorrido del cliente
description: Ofrezca experiencias de cliente individuales, puntuales y orquestadas en todas las pantallas.
solution: Journey Optimizer, Campaign, Experience Platform
exl-id: 273d024f-a220-4336-89f2-e3bffafcdc37
source-git-commit: 49251caac58cd8f62dff977f94ea6a716aa94250
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 14%

---

# Modelos de recorrido del cliente

Los equipos de marketing modernos requieren plataformas que puedan admitir la participación reactiva (que responda a los comportamientos de los clientes individuales) y la divulgación proactiva (que inicie campañas que guíen a las audiencias hacia canales de conversión). Estos casos de uso abarcan canales como correo electrónico, SMS, push y, cada vez más, experiencias web y en la aplicación.

Adobe Journey Optimizer y Adobe Campaign v8 admiten dos modelos fundamentales para la participación del cliente:

- Recorridos activados por el cliente: orquestación en tiempo real basada en comportamientos y señales individuales.
- Campañas iniciadas por marcas: Inserciones programadas estratégicamente que introducen audiencias en canales de participación basados en la segmentación o la lógica empresarial.

Ambas soluciones permiten la comunicación saliente entre canales tradicionales y digitales. AJO también admite la integración con canales entrantes (por ejemplo, aplicaciones web y móviles) mediante servicios de decisiones y uso compartido de estados de audiencia, lo que permite una personalización unificada entre canales.

La selección entre estas herramientas depende de consideraciones arquitectónicas como la tolerancia de latencia, los requisitos de canal, la estrategia de integración de datos y la escalabilidad.

<br>

| Modelo | Descripción | Arquitectura |
|---|---|:---:|
| **[Adobe Journey Optimizer](journey-optimizer/journey-optimizer-overview.md)** | Combina organización de perfiles 1:1 basada en eventos con comunicaciones de marca basadas en audiencias en varios canales, como correo electrónico, sms, web, push, mensajería en la aplicación, escritorio, etc. | <img src="journey-optimizer/images/ajo-architecture.svg" alt="Arquitectura de referencia para el modelo de Journey Optimizer" style="width:75%; border:1px solid #4a4a4a" class="modal-image" /> |
| **[Adobe [!DNL Campaign] v8](campaign-v8/campaign-v8-overview.md)** | Se centra en la administración de campañas multicanal por lotes, ideal para canales de marketing tradicionales como correo electrónico, SMS y correo directo. | <img src="campaign-v8/images/campaign-v8-architecture.svg" alt="Arquitectura de referencia para el modelo de Campaign v8" style="width:75%; border:1px solid #4a4a4a" class="modal-image" /> |

<br>

## Modelos obsoletos

| Modelo | Arquitectura |
|---|:---:|
| **[Adobe [!DNL Campaign] v7](campaign-v7/campaign-v7-overview.md)** | <img src="campaign-v7/images/campaign-v7-architecture.svg" alt="Arquitectura de referencia para el modelo de Campaign v7" style="width:50%; border:1px solid #4a4a4a" class="modal-image" /> |