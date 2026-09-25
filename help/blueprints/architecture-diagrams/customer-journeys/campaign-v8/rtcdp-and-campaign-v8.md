---
title: Patrón de integración de Real-Time CDP con Adobe Campaign v8
description: Muestra cómo se puede utilizar Adobe Experience Platform, su funcionalidad Real-Time Customer Profile y la herramienta de segmentación centralizada con Adobe Campaign v8 para ofrecer conversaciones personalizadas.
solution: Real-Time Customer Data Platform, Campaign
exl-id: d0291088-02ed-4e7e-b538-018ea40e38c6
TQID: https://experienceleague.adobe.com/LANKBKui1B5RfyNI8ufsgjrC98TXpAf74IB-alwDTnk
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
    internal-label: Real-Time Customer Data Platform
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 79738031788419872e32b8f754febacbfd18cc06
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 72%
---
# [!DNL Real-Time CDP] con el patrón de integración de Adobe [!DNL Campaign] v8

Muestra cómo Adobe [!DNL Experience Platform] y su herramienta de segmentación centralizada y el Perfil del cliente en tiempo real se pueden utilizar con Adobe Campaign para ofrecer conversaciones personalizadas.

## Aplicaciones

* Adobe[!DNL Experience Platform Real-Time CDP]
* Adobe [!DNL Campaign] v8

## Arquitectura

![Arquitectura de referencia para el patrón de integración de Adobe Experience Platform y mensajería por lotes](images/campaign-v8-with-rtcdp.png){width="1000" zoomable="yes"}

<br>

## Prerrequisitos

* El cliente debe poder acceder a Experience Cloud con una organización IMS válida
* Se recomienda aprovisionar Adobe Experience Platform y [!DNL Campaign] en la misma organización de IMS para una sola URL de inicio de sesión
* El cliente debe tener la instancia V8 aprovisionada de [!DNL Campaign]
* El cliente debe ser elegible y tener acceso a RTCDP, orígenes y destinos.
* El contexto del producto Adobe [!DNL Campaign] debe existir

<br>

## Pasos de implementación

Consulte la siguiente documentación sobre la configuración del conector de origen de Campaign v8 en Adobe Experience Platform y el conector de destino de Real-Time Customer Data Platform en Campaign v8.
[Conectores de Campaign y AEP](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=es)

## Guardas

### Adobe Campaign

* Consulte la documentación del conector de origen de Campaign: [conector de origen de Campaign](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/campaign.html?lang=es)
* Solamente compatible con la implementación de entidades organizativas únicas de Adobe Campaign


### Uso compartido de segmentos en Real-Time Customer Data Platform de Experience Platform

* Consulte el conector de destino de RTCDP Campaign: [conexión de RTCDP Campaign](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=es)

* Consulte las guardas de ingesta de datos y perfiles para AEP: [vínculo](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
