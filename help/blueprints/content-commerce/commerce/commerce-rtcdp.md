---
title: 'Adobe Commerce: modelo RTCDP'
description: Integración de Adobe Experience Platform con Adobe Commerce para crear una única vista de clientes y personalizar de forma inteligente las experiencias en una tienda digital y en varios canales.
solution: Real-Time Customer Data Platform, Commerce
exl-id: e2fc5e1c-c865-4c24-9b82-861a34aba487
source-git-commit: 80a4716a7ed64ec30b9c60b3444affc5bd8984e4
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---

# ADOBE COMMERCE Y RTCDP

La extensión [!DNL Data Connection] ayuda a los clientes de Adobe Commerce a integrarse perfectamente con Adobe Experience Platform para enriquecer el perfil del cliente y personalizar experiencias en tiendas digitales y otros canales.

## Capacidades técnicas habilitadas

* Los datos de la tienda (del lado del cliente, como adición al carro de compras, abandonos del carro de compras, etc.) se recopilan y envían a cualquier producto de Adobe Experience Cloud.
* El estado de pedidos de gestiones internas de cualquier producto de Adobe Experience Cloud
* Los pedidos históricos de back office se pueden enviar a Adobe Experience Platform
* Uso compartido y personalización de audiencias de RTCDP con Adobe Commerce

## Requisitos previos

Para usar la extensión [!DNL Data Connection], debe tener lo siguiente:

* Adobe Commerce 2.4.4 o posterior
* Adobe ID e ID de organización
* Adobe Experience Platform/RTCDP
* [Capa de datos de cliente de Adobe (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html). La ACDL es necesaria para recopilar datos de evento de tienda.

## Pasos de incorporación

### Recopilación de datos de Adobe Commerce a Adobe Experience Platform

* [Instalar](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) la extensión [!DNL Data Connection].
* [Inicia sesión](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) en tu cuenta de Adobe y consulta para confirmar tu ID de organización. El ID de organización es el ID asociado con la empresa de Experience Cloud aprovisionada. Se trata de una cadena alfanumérica de 24 caracteres seguida de @AdobeOrg (que debe incluirse).
* [Cree o actualice](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) su esquema XDM con grupos de campos específicos de Commerce.
* [Crear un conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) basado en el esquema que creó o actualizó. Este conjunto de datos contendrá los datos de Commerce que envíe.
* [Cree una secuencia de datos](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) y seleccione el esquema XDM que contiene los grupos de campos específicos de Commerce.
* [Conectarse a los servicios de Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html).
* [Conectarse a Adobe Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).

### Conectarse al destino de Commerce desde Adobe Experience Platform para compartir audiencias

Para conectarse al destino de Adobe Commerce:

* En la [interfaz de Adobe Experience Platform](https://experience.adobe.com/platform/), vaya a Destinos > Catálogo.
* Seleccione Personalization.
* Seleccione el destino de Adobe Commerce para resaltarlo y, a continuación, seleccione Configurar.
* Siga los pasos descritos en el [tutorial de configuración de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html).

## Datos de fábrica

* Eventos de tienda (explorador/aplicación)
* Eventos de back office
* Datos históricos de pedidos

Para obtener una lista completa de los eventos admitidos, consulte [Eventos de Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html)

## Arquitectura

<img src="../commerce/assets/commerce_rtcdp.png" alt="Arquitectura RTCDP de Adobe Commerce" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Guías de implementación relacionadas

| Guía | Vínculo |
|:----|:----|
| Platform Connector | [Descripción general del conector de Experience Platform de Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html) |
| Destino de Commerce | [Conexión de Adobe Commerce en RTCDP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-commerce.html) |
| Edge Personalization | [Activar audiencias en destinos de personalización Edge](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations.html) |
