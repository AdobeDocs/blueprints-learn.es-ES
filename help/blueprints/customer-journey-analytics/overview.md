---
title: Customer Journey Analytics
description: Unifique y analice datos y comportamiento de los clientes en todo su recorrido
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 3bb2dada-f4cd-43f7-a0d0-f276510ad224
source-git-commit: 6059edc6a6b65e87ed1c06a072feea45703e9103
workflow-type: ht
source-wordcount: '413'
ht-degree: 100%

---

# Customer Journey Analytics

Customer Journey Analytics muestra cómo las marcas pueden unificar datos y comportamientos del cliente de varios canales y fuentes de interacción para crear una vista basada en el recorrido de todas las interacciones del cliente. La creación de informes y el análisis se pueden realizar en el servicio de la aplicación Customer Journey Analytics para evaluar y obtener datos sobre la interacción del cliente y sus patrones de comportamiento.

Puede encontrar una lista completa de los casos de uso de Customer Journey Analytics en la documentación de Customer Journey Analytics aquí.

## [Vínculo a casos de uso de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cja-usecases.html?lang=es)

Los casos de uso comunes incluyen:

* Crear y publicar audiencias en Real-time Customer Data Platform
* Rutas de conversión arriba/abajo
* Participación y conversión del canal
* Contenido más visto
* Categorías y productos principales
* Qué campañas resultaron en conversión y más participación
* Análisis de uso de herramientas para optimizar las experiencias de autoservicio

## Arquitectura para el Customer Journey Analytics

![Diagrama de arquitectura](assets/CJA.svg)

Algunos ejemplos de casos de uso principales son los siguientes:
| Modelo | Descripción | Aplicaciones de Experience Cloud |
|---|---|---|
| **[Cross Channel Journey Analysis](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cross-channel.html?lang=es)**  | <ul><li>Obtenga una sola vista consolidada con el comportamiento del cliente para todos los diferentes canales unificando los datos de distintas propiedades web, móvil y sin conexión.</li></ul> | <ul><li>Adobe Experience Platform</li><li>Customer Journey Analytics</li><li>Adobe Analytics (opcional)</li></ul>|
| **[Publicar audiencias en Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=es)** | <ul><li>Cree y publique audiencias identificadas en Customer Journey Analytics (CJA) en Real-time Customer Profile en Adobe Experience Platform para la segmentación y personalización de clientes. Ideal para crear audiencias que utilicen datos históricos o audiencias más refinadas a partir de filtros granulares y campos calculados en Customer Journey Analytics.</li></ul> | <ul><li>Real-time Customer Data Platform</li><li>Customer Journey Analytics</li> |
| **[Análisis del recorrido de desvío de llamadas](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/call-center.html?lang=es)** | <ul><li>Determine qué comportamientos tienen más posibilidades de resultar en una llamada atendida por un agente, uniendo los datos del centro de llamadas con otros derivados de la web, móvil u otras interacciones.</li><li>Esta información se puede utilizar para optimizar la experiencia del cliente y reducir la ruta a interacciones atendidas por agentes gracias al contenido y a las herramientas optimizadas para el autoservicio.  </li></ul> | <ul><li>Adobe Experience Platform</li><li>Customer Journey Analytics</li> |

## Diagrama de guardas para los modelos de Customer Journey Analytics

* Para obtener más información sobre las guardas y las latencias de extremo a extremo, consulte el [documento de guardas de implementación](../experience-platform/deployment/guardrails.md)

![Diagrama de guardas](../experience-platform/assets/CJA_guardrails.svg)

## Entradas relacionadas en el blog

* [[!DNL Blueprint for Multi-Channel Orchestration in Adobe Experience Platform]](https://medium.com/adobetech/blueprint-for-multi-channel-orchestration-in-adobe-experience-platform-c68317e94184){target=&quot;_blank&quot;}
* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17){target=&quot;_blank&quot;}
* [[!DNL Event-Based Triggering on Adobe Experience Platform Orchestration Service using Apache Airflow]](https://medium.com/adobetech/event-based-triggering-on-adobe-experience-platform-orchestration-service-using-apache-airflow-8607b28251f1){target=&quot;_blank&quot;}
* [[!DNL Adobe Campaign Classic Integration with Journey Orchestration]](https://medium.com/adobetech/adobe-campaign-classic-integration-with-journey-orchestration-ae577653281){target=&quot;_blank&quot;}
* [[!DNL Demonstrating the Power of Adobe’s New Journey Orchestration Service to Build Personalized Omnichannel Experiences in Real-Time]](https://medium.com/adobetech/demonstrating-the-power-of-adobes-new-journey-orchestration-service-to-build-personalized-aa60d88cd34){target=&quot;_blank&quot;}
* [[!DNL Journey Orchestration in an Omnichannel World]](https://medium.com/adobetech/journey-orchestration-in-an-omnichannel-world-3a2d32d556d9){target=&quot;_blank&quot;}
