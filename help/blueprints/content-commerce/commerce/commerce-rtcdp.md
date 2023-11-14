---
title: 'Adobe Commerce: modelo RTCDP'
description: Integración de Adobe Experience Platform con Adobe Commerce para crear una única vista de clientes y personalizar de forma inteligente las experiencias en una tienda digital y en varios canales.
solution: Real-Time Customer Data Platform, Commerce
source-git-commit: abb946358ceeee1af427c5b362ed2f48f733a6c9
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# ADOBE COMMERCE Y RTCDP

Esta experiencia integrada ayuda a los clientes de Adobe Commerce a integrarse perfectamente con Adobe Experience Platform para enriquecer el perfil del cliente y personalizar experiencias en tiendas digitales y otros canales.

## Capacidades técnicas habilitadas

* Datos de la tienda (lado del cliente) recopilados y enviados a cualquier producto de Adobe Experience Cloud. (añadir al carro de compras, abandonos del carro de compras, etc.)
* El estado de pedidos de gestiones internas de cualquier producto de Adobe Experience Cloud
* Los pedidos históricos de back office se pueden enviar a Adobe Experience Platform
* Uso compartido y personalización de audiencias de RTCDP con Adobe Commerce

## Requisitos previos

Para utilizar el conector del Experience Platform, debe tener lo siguiente:

* Adobe Commerce 2.4.4 o posterior
* Adobe ID e ID de organización
* Adobe Experience Platform/RTCDP
* [Capa de datos del cliente de Adobe (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html?lang=en). La ACDL es necesaria para recopilar datos de evento de tienda.

## Pasos de incorporación

### Recopilación de datos de Adobe Commerce a Adobe Experience Platform

* [Instalar](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/install.html?lang=en) la extensión del conector del Experience Platform.
* [Iniciar sesión](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) Vaya a la cuenta de Adobe y consulte para confirmar el ID de organización. El ID de organización es el ID asociado con la empresa de Experience Cloud aprovisionada. Se trata de una cadena alfanumérica de 24 caracteres seguida de @AdobeOrg (que debe incluirse).
* [Crear o actualizar](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html?lang=en) Cree su esquema XDM con grupos de campos específicos de Commerce.
* [Crear un conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=en#create-a-dataset) en función del esquema que haya creado o actualizado. Este conjunto de datos contendrá los datos de Commerce que envía.
* [Creación de una secuencia de datos](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html?lang=en) y seleccione el esquema XDM que contiene los grupos de campos específicos de Commerce.
* [Conectar con Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html?lang=en).
* [Conectar con Adobe Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/connect-data.html?lang=en).

### Conéctese al destino de Commerce desde Adobe Experience Platform para compartir audiencias

Para conectarse al destino de Adobe Commerce:

* En el [Interfaz de Adobe Experience Platform](https://experience.adobe.com/platform/), vaya a Destinos > Catálogo.
* Seleccione Personalización.
* Seleccione el destino de Adobe Commerce para resaltarlo y, a continuación, seleccione Configurar.
* Siga los pasos descritos en la sección [tutorial de configuración de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en).

## Datos de fábrica

* Eventos de Storefront (Browser/App)
* Eventos de back office
* Datos históricos de pedidos

Para obtener una lista completa de los eventos admitidos, consulte [Eventos de Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/event-forwarding/events.html?lang=en)

## Arquitectura

<img src="../commerce/assets/commerce_rtcdp.png" alt="Arquitectura RTCDP de Adobe Commerce" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Guías de implementación relacionadas

| Guía  | Vínculo |
|:----|:----|
| Platform Connector | [Información general sobre el conector del Experience Platform Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/overview.html?lang=en) |
| Destino comercial | [Conexión de Adobe Commerce en RTCDP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-commerce.html?lang=en) |
| Personalización de Edge | [Activación de audiencias en destinos de personalización de Edge](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations.html?lang=en) | |
