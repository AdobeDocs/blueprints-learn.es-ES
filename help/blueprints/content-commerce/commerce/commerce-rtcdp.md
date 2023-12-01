---
title: 'Adobe Commerce: modelo RTCDP'
description: Integración de Adobe Experience Platform con Adobe Commerce para crear una única vista de clientes y personalizar de forma inteligente las experiencias en una tienda digital y en varios canales.
solution: Real-Time Customer Data Platform, Commerce
exl-id: e2fc5e1c-c865-4c24-9b82-861a34aba487
source-git-commit: 8a47b73065a5591673804301c61a73947346813c
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# ADOBE COMMERCE Y RTCDP

El [!DNL Data Connection] Esta extensión ayuda a los clientes de Adobe Commerce a integrarse perfectamente con Adobe Experience Platform para enriquecer el perfil del cliente y personalizar experiencias en tiendas digitales y otros canales.

## Capacidades técnicas habilitadas

* Los datos de la tienda (del lado del cliente, como adición al carro de compras, abandonos del carro de compras, etc.) se recopilan y envían a cualquier producto de Adobe Experience Cloud.
* El estado de pedidos de gestiones internas de cualquier producto de Adobe Experience Cloud
* Los pedidos históricos de back office se pueden enviar a Adobe Experience Platform
* Uso compartido y personalización de audiencias de RTCDP con Adobe Commerce

## Requisitos previos

Para usar la variable [!DNL Data Connection] Extensión, debe tener lo siguiente:

* Adobe Commerce 2.4.4 o posterior
* Adobe ID e ID de organización
* Adobe Experience Platform/RTCDP
* [Capa de datos del cliente de Adobe (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html). La ACDL es necesaria para recopilar datos de evento de tienda.

## Pasos de incorporación

### Recopilación de datos de Adobe Commerce a Adobe Experience Platform

* [Instalar](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) el [!DNL Data Connection] extensión.
* [Iniciar sesión](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) Vaya a la cuenta de Adobe y consulte para confirmar el ID de organización. El ID de organización es el ID asociado con la empresa de Experience Cloud aprovisionada. Se trata de una cadena alfanumérica de 24 caracteres seguida de @AdobeOrg (que debe incluirse).
* [Crear o actualizar](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) Cree su esquema XDM con grupos de campos específicos de Commerce.
* [Crear un conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) en función del esquema que haya creado o actualizado. Este conjunto de datos contendrá los datos de Commerce que envía.
* [Creación de una secuencia de datos](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) y seleccione el esquema XDM que contiene los grupos de campos específicos de Commerce.
* [Conectar con Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html).
* [Conectar con Adobe Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).

### Conéctese al destino de Commerce desde Adobe Experience Platform para compartir audiencias

Para conectarse al destino de Adobe Commerce:

* En el [Interfaz de Adobe Experience Platform](https://experience.adobe.com/platform/), vaya a Destinos > Catálogo.
* Seleccione Personalización.
* Seleccione el destino de Adobe Commerce para resaltarlo y, a continuación, seleccione Configurar.
* Siga los pasos descritos en la sección [tutorial de configuración de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html).

## Datos de fábrica

* Eventos de tienda (explorador/aplicación)
* Eventos de back office
* Datos históricos de pedidos

Para obtener una lista completa de los eventos admitidos, consulte [Eventos de Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html)

## Arquitectura

<img src="../commerce/assets/commerce_rtcdp.png" alt="Arquitectura RTCDP de Adobe Commerce" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Guías de implementación relacionadas

| Guía de  | Vínculo |
|:----|:----|
| Platform Connector | [Información general sobre el conector del Experience Platform Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html) |
| Destino comercial | [Conexión de Adobe Commerce en RTCDP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-commerce.html) |
| Personalización de Edge | [Activación de audiencias en destinos de personalización de Edge](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations.html) | |
