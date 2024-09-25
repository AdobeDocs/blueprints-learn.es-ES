---
title: Customer Journey Analytics con modelo de Real-time Customer Data Platform
description: Unifique y analice los datos y los comportamientos de los clientes desde todo el recorrido del cliente en Customer Journey Analytics y publique la audiencia de CJA a RTCDP
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
source-git-commit: 9fe44d93dcc05711c77ce1325b6549bb6c27a860
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 94%

---

# Customer Journey Analytics con modelo de Real-time Customer Data Platform

Cree y publique audiencias identificadas en Customer Journey Analytics (CJA) en Real-Time Customer Profile en Adobe Experience Platform para la segmentación y personalización de clientes. Ideal para crear audiencias que utilicen datos históricos o audiencias más refinadas a partir de filtros granulares y campos calculados en Customer Journey Analytics.

## Guía de publicación de audiencias de Customer Journey Analytics

Consulte la siguiente documentación para obtener instrucciones sobre la implementación y configuración de la publicación de audiencias de Customer Journey Analytics en Real-Time Customer Data Platform. [Documentación](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=es)

## Modelos de arquitectura de Customer Journey Analytics

![Diagrama de arquitectura](assets/CJA.svg){zoomable="yes"}

## Diagrama de guardas para los modelos de Customer Journey Analytics

* Para obtener más información sobre los mecanismos de protección y las latencias de extremo a extremo, consulte el [documento de mecanismos de protección de implementación](../experience-platform/deployment/guardrails.md)

![Diagrama de guardas](../experience-platform/deployment/assets/CJA_guardrails.svg){zoomable="yes"}

## Preguntas frecuentes

* Si en RTCDP no existe un perfil correspondiente al enviado por CJA, ¿se creará un nuevo perfil o las audiencias solo se registrarán desde CJA para perfiles que ya están presentes? Sí, se creará un nuevo perfil. Como resultado, si la implementación de RTCDP es solo para clientes conocidos, las reglas de audiencia de CJA deben escribirse para que filtren solo perfiles con identidades conocidas. Esto garantizará que el recuento de perfiles en RTCDP no aumente a partir de perfiles anónimos si no se desea.

* ¿Qué identidades envía CJA? CJA envía cualquier identidad configurada como “ID de persona” durante la configuración de CJA.

* ¿Qué se establece como identidad principal? Cualquiera que sea la identidad que el usuario seleccionó cuando configuró CJA como ID de “persona” principal.

* ¿El servicio de identidad también procesa los mensajes de CJA? Es decir, ¿puede CJA añadir identidades a un gráfico de identidad de perfil mediante el uso compartido de audiencias? No, el servicio de identidad no procesa los mensajes de CJA.