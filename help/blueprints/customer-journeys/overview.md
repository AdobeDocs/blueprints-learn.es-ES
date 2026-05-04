---
title: Modelos de recorrido del cliente
description: Ofrezca experiencias de cliente individuales, puntuales y orquestadas en todas las pantallas.
solution: Journey Optimizer, Campaign, Experience Platform
exl-id: 273d024f-a220-4336-89f2-e3bffafcdc37
TQID: https://experienceleague.adobe.com/vJUJiLr7je-Pp2daoYoNYipfVBRyaEYNv-XCx9PrjzM
product_v2: id: cb954087-f4fc-4456-afb9-e939cabcdc79id: dfc56824-e8b9-499e-85d4-21aedb507314id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914id: d998adac-2f81-400b-a669-d07bb196e4ebid: daec7ead-f475-492a-a3b3-02ae08565d6fid: df64005d-8f9a-422e-ba4d-c6f6dc3454b4id: fe338112-e2ce-4876-8989-fc4d497613f1
subfeature_v2: id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5520579-b31f-4df7-9281-f0d9f91e2edcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: df401a2a-327d-468c-a5e4-b7b7ccd071a0id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: a99add31cc9f485db119ca00426798545e6a7316
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 13%

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