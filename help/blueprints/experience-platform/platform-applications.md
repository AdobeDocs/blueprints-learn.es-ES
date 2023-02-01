---
title: Diagramas de arquitectura de Adobe Experience Platform & Applications
description: Este diagrama de arquitectura muestra cómo Adobe Experience Platform se relaciona con otras aplicaciones y servicios de aplicaciones de Adobe Experience Cloud.
solution: Experience Platform, Campaign, Analytics, Target, Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
kt: 7199
thumbnail: null
exl-id: 9b12cd7a-5e5f-443a-91a1-44273cdabc2d
source-git-commit: 8355a36a235d847a6faf2398f3fadbed28ccac37
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 64%

---

# Adobe Experience Platform y otras aplicaciones diagramas de arquitectura

## Diagrama de la arquitectura de Adobe Experience Platform y otras aplicaciones

Este diagrama de arquitectura muestra cómo Adobe Experience Platform se relaciona con las aplicaciones y los servicios de aplicaciones de Adobe Experience Cloud.

<img src="assets/aep+apps_vertical.svg" alt="Experience Platform y otras aplicaciones" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" />

## Diagrama detallado de la arquitectura de Adobe Experience Platform y otras aplicaciones

<img src="assets/aep-app-architecture.svg" alt="Experience Platform y otras aplicaciones" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" />

>[!VIDEO](https://video.tv.adobe.com/v/32456/?quality=12&learn=on)

## Integraciones de aplicaciones de Adobe Experience Platform y Experience Cloud

<table class="relative-table wrapped" style="width: 100%;">
<colgroup>
<col style="width: 16.0202%;" />
<col style="width: 29.3423%;" />
<col style="width: 33.5582%;" />
<col style="width: 21.0793%;" />
</colgroup>
<tbody>
<tr>
<th>Aplicación</th>
<th>De Experience Platform a la aplicación</th>
<th>De la aplicación a Experience Platform</th>
<th>Modelos relacionados</th>
</tr>
<tr>
<td colspan="1">Ad Cloud</td>
<td colspan="1">
<ul>
<li>Las audiencias definidas en Real-time Customer Data Platform se pueden compartir con Ad Cloud para segmentar mediante Audience Manager.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Actualmente, sin integración.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=es">Activación de audiencia anónima </a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=es">Activación de cliente conocida</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=es">Activación con Experience Platform y otras aplicaciones</a></li>
</ul>
</td>
</tr>
<tr>
<td>Analytics</td>
<td>
<ul>
<li>Los datos recopilados mediante el SDK web/móvil se pueden reenviar a Adobe Analytics.</li>
</ul>
</td>
<td>
<ul>
<li>Los datos que recopila Analytics se pueden enviar al repositorio de datos de Experience Platform y al almacén de perfiles. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=es">Analytics Data Connector</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-data-flow.html?lang=es">Flujos de datos de Experience Platform</a></li>
</ul>
</td>
</tr>
<tr>
<td>Audience Manager</td>
<td>
<ul>
<li>Las audiencias definidas en Real-time Customer Data Platform se pueden compartir con el Audience Manager para su activación en destinos de cookies de terceros.</li>
</ul>
</td>
<td>
<ul>
<li>Los datos recopilados y evaluados junto con las pertenencias a audiencias de Audience Manager se pueden compartir con el almacén de perfiles y el repositorio de datos de Experience Platform. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=es">Conector de origen de Audience Manager</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=es">Activación de audiencia anónima </a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=es">Activación de cliente conocida</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=es">Activación con Experience Platform y otras aplicaciones</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Campaign Classic</td>
<td colspan="1">
<ul>
<li>Las audiencias definidas en Real-time Customer Data Platform se pueden compartir con el Campaign Classic como audiencia para iniciar campañas.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Los datos de interacción y campaña recopilados por Campaign se pueden ingerir a Experience Platform como fuente de datos para su uso posterior en la creación de audiencias mediante Real-time Customer Data Platform y análisis mediante el servicio de consulta de Customer Journey Analytics y Experience Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/overview.html?lang=es">Recorridos del cliente</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Campaign Standard</td>
<td colspan="1">
<ul>
<li>Las audiencias definidas en Real-time Customer Data Platform se pueden compartir con el Campaign Standard como audiencia para iniciar campañas.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Los datos de interacción y campaña recopilados por Campaign se pueden ingerir a Experience Platform como fuente de datos para su uso posterior en la creación de audiencias mediante Real-time Customer Data Platform y análisis mediante el servicio de consulta de Customer Journey Analytics y Experience Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/overview.html?lang=es">Recorridos del cliente</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Customer Journey Analytics</td>
<td colspan="1">
<ul>
<li>Los datos recopilados e ingeridos en el repositorio de datos de Experience Platform quedan disponibles para ser procesados en Customer Journey Analytics. </li>
<li>Los datos de perfil y audiencia de Real-time Customer Data Platform se pueden ingerir en CJA. <a href="https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/ingest-aep-segments.html?lang=es">Integración de RTCDP con CJA</a>.
</li>
</ul>
</ul>
</td>
<td colspan="1">
<ul>
<li>Cree audiencias en Customer Recorrido Analytics y comparta los resultados de audiencia con Real-time Customer Data Platform. <a href="https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=es">Publicación de audiencias de CJA</a></li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journey-analytics/overview.html?lang=es">Customer Journey Analytics</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Experience Manager</td>
<td colspan="1">
<ul>
<li>Se puede acceder directamente al perfil del Experience Platform en el servidor para potenciar las experiencias personalizadas ofrecidas mediante Experience Manager. Tenga en cuenta que las actividades de personalización generalmente se realizan en Experience Manager a través de la integración de Target. </li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Ninguna integración actual, comportamientos ni interacciones realizadas en los sitios de Experience Manager se recopilan directamente mediante el SDK Web y Mobile de Experience Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=es">Activación de cliente conocida</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Journey Optimizer</td>
<td colspan="1">
<ul>
<li>Los eventos de datos y perfiles ingeridos en Experience Platform quedan disponibles para que Journey Optimizer inicie y active los recorridos en Journey Optimizer.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Los datos de interacción y campaña producidos por Journey Optimizer se recopilan en Experience Platform para su uso posterior en la creación de audiencias a través de Real-time Customer Data Platform y el análisis mediante el servicio de consulta de Experience Platform y Customer Journey Analytics.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=es">Journey Optimizer</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Adobe Commerce</td>
<td colspan="1">
<ul>
<li>Los perfiles y las audiencias creados en Real-time Customer Data Platform pueden estar disponibles para la personalización en Adobe Commerce. </li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Los datos nativos de Adobe Commerce se pueden enviar a Experience Platform a través de un conector de origen de Adobe Commerce. </li>
</ul>
</td>
<td colspan="1">Actualmente, sin integración.</td>
</tr>
<tr>
<td colspan="1">Marketo</td>
<td colspan="1">
<ul>
<li>Las audiencias definidas en Real-time Customer Data Platform se pueden compartir con Marketo como audiencia para iniciar campañas de Marketo y actualizar objetos de Marketo.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Las cuentas, los contactos y los datos de oportunidad de Marketo, junto con los datos de interacción y campaña que genera Marketo, se ingieren en Experience Platform para su uso posterior en la creación de audiencias mediante B2B-CDP y en el análisis a través de Customer Journey Analytics y Experience Platform Query Service. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=es">Conector de Marketo Engage</a></li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=es">Modelo de activación B2B</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Real-Time CDP</td>
<td colspan="1">
<ul>
<li>Los datos introducidos y recopilados en el Experience Platform son la fuente de datos para ensamblar perfiles de clientes en tiempo real que alimentan el Real-time Customer Data Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Las métricas de audiencia y perfil se envían al repositorio de datos de Experience Platform para alimentar los paneles de creación de informes de datos de perfiles.</li>
<li>Los datos de audiencia y perfil del repositorio de datos se pueden usar para obtener más información mediante Query Service y Customer Journey Analytics.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=es">Activación de cliente conocida</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=es">Activación con Experience Platform y otras aplicaciones</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Target</td>
<td colspan="1">
<ul>
<li>Las audiencias y los atributos de perfil definidos en Real-time Customer Data Platform se pueden compartir con Target y usar en las experiencias de personalización y segmentación que Target proporcione.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Los datos recopilados para las experiencias e interacciones de Target se pueden recoger en Experience Platform mediante el SDK web o móvil de Experience Platform. Estos datos se pueden utilizar en la creación de audiencias a través de Real-time Customer Data Platform y para su análisis mediante el Customer Journey Analytics y el servicio de consulta Experience Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=es">Activación de cliente conocida</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=es">Activación con Experience Platform y otras aplicaciones</a></li>
</ul>
</td>
</tr>
</tbody>
</table>