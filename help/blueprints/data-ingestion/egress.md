---
title: Modelo de acceso y exportación de datos
description: Obtenga información sobre los métodos mediante los cuales se puede acceder a los datos y exportarlos desde Adobe Experience Platform y aplicaciones.
product: adobe experience platform
solution: Experience Platform, Journey Optimizer, Real-Time Customer Data Platform, Data Collection
exl-id: 2ca51a29-2db2-468f-8688-fc8bc061b47b
source-git-commit: 9fe44d93dcc05711c77ce1325b6549bb6c27a860
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 90%

---

# Acceso a datos y modelo de exportación

El modelo de acceso a datos y exportación describe todos los métodos posibles mediante los cuales se puede acceder a datos o exportarlos desde [!DNL Experience Platform] y aplicaciones.

El modelo se divide en dos categorías para el acceso a los datos desde [!DNL Experience Platform] y las aplicaciones.

El primero incluye enfoques para la salida de datos de [!DNL Experience Platform] y aplicaciones. Esto se consideraría un método de tipo _push_ de salida de datos.

El segundo incluye enfoques para acceder a datos de [!DNL Experience Platform] y aplicaciones. Esto se consideraría un método de tipo _pull_ de acceso a datos.

Enfoques de acceso a datos:

* [API de acceso al perfil del cliente en tiempo real](#rtcp-profile-access-api)
* [API de acceso a datos](#data-access-api)
* [Servicio de consultas](#query-service)

Enfoques de exportación de datos:

* [Etiquetas del lado del cliente](#client-side-tags-extensions)
* [Reenvío de eventos](#event-forwarding)
* [Destinos de Real-Time Customer Data Platform](#RTCDP-destinations)
* [Acciones personalizadas de Journey Optimizer](#jo-custom-actions)

## Arquitectura de información general de acceso a datos y exportación

<img src="../experience-platform/assets/aep_data_flow.svg" alt="Arquitectura de referencia para el modelo de preparación e ingesta de datos" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" class="modal-image" />

## Métodos de acceso a datos y exportación

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1133px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:39px; vertical-align:top; width:1133px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Destinos de streaming</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Método</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Casos de uso comunes</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protocolos</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Consideraciones</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=es" style="color:#0563c1; text-decoration:underline">Reenvío de eventos</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Reenvío de datos sin procesar recopilados de los SDK de Adobe para su análisis y recopilación en sistemas empresariales</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Etiquetado ligero para recopilación de datos de 3<sup>os</sup> a través de extensiones</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">API de REST</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Eventos sin procesar de bajo nivel</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">No se ha añadido ningún agregado ni contexto de registro anterior</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=es#:~:text=containing%20profile%20exports.-,Streaming%20segment%20export%20destinations,-Segment%20export%20destinations" style="color:#0563c1; text-decoration:underline">RTCDP: exportaciones de segmentos por streaming</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Active audiencias desde RTCDP para marketing y publicidad, sistemas...</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">API de REST</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Datos agregados que representan la suscripción a la audiencia</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">No se activan los datos de eventos de experiencias sin procesar</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=es#:~:text=file%2Dbased)%20destinations-,Streaming%20profile%20export%20destinations%20(enterprise%20destinations),-IMPORTANT" style="color:#0563c1; text-decoration:underline">RTCDP: destinos de exportación de perfil</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Aproveche los perfiles y audiencias de comportamiento enriquecidos de RTCDP para mejorar las experiencias de los consumidores y el marketing.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Active audiencias y atributos de perfil de RTCDP para marketing y publicidad, sistemas que funcionan con audiencias y atributos de perfil. </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Active los perfiles de AEP en los proveedores de servicios de correo electrónico, la alimentación de posibles clientes y los sistemas CRM.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">API de REST</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Datos agregados que representan la suscripción a la audiencia y los atributos de registro de perfil</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">No se activan los datos de eventos de experiencias sin procesar</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=es" style="color:#0563c1; text-decoration:underline">RTCDP: destinos de personalización</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Acceda a Real-time Customer Profile en experiencias del explorador y del lado del cliente para enriquecer la personalización del lado del cliente. </span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Requiere la implementación de WebSDK</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-sdk/overview.html?lang=es" style="color:#0563c1; text-decoration:underline">RTCDP: Destination SDK</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Configure una tarjeta de destino personalizada en los destinos RTCDP.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Es compatible con destinos de tipo archivo y streaming</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">CSV</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Permite a socios y marcas configurar tarjetas de destino personalizadas</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=es" style="color:#0563c1; text-decoration:underline">RTCDP: API de Profile Lookup Hub</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Acceda al perfil para enriquecer las experiencias de los consumidores para experiencias asistidas por agentes, como las interacciones con el agente de ventas o la asistencia.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">API de REST</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Búsqueda de hub ideal para casos de uso solo de &gt;500 ms</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">RTCDP: búsqueda de perfiles API de Edge</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Acceda al perfil en Edge para enriquecer las experiencias de los consumidores para experiencias de &lt;200 ms en tiempo real, como la personalización o las decisiones de oferta en web y móvil.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">API de REST</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Para experiencias en tiempo real e integraciones de servidor a servidor</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=es" style="color:#0563c1; text-decoration:underline">Acciones personalizadas de Journey Optimizer</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Activación de eventos de recorrido 1:1 y activadores para notificar a un sistema externo. Abandonos del carro de compras, abandonos de aplicaciones, registros.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">API de REST</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Activación de un solo evento para un perfil determinado. No es para el agregado ni operaciones masivas</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>

<p> </p>

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1132px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:39px; vertical-align:top; width:1132px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Destinos por lote</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Método</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Casos de uso comunes</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protocolos</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Consideraciones</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/data-access/api.html?lang=es" style="color:#0563c1; text-decoration:underline">API de acceso a datos</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Acceso a datos sin procesar para la ciencia de datos y flujos de trabajo ML fuera de Experience Platform.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">API de REST</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Archivos de Parquet</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Requiere procesos de desarrollo para acceder y procesar archivos de Parquet en conjuntos de datos utilizables</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=es" style="color:#0563c1; text-decoration:underline">Servicio de consultas</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Conserve los resultados de consultas de conjuntos de datos para obtener información agregada y crear informes. </span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">PostgreSQL </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Cliente SQL</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Solo datos agregados. Límite de consulta de 10 minutos.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-datasets.html?lang=es" style="color:#0563c1; text-decoration:underline">Exportación de conjuntos de datos</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Exporte datos de eventos de Experience Platform para acceder a las herramientas externas de creación de informes, análisis y ciencia de datos. </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Exporte datos de perfil y suscripciones a la audiencia agregados para herramientas externas de creación de informes, análisis y ciencia de datos. </span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">API de REST </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">CSV</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Se admite un subconjunto de conjuntos de datos como se describe en la documentación del producto.</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>



## Enfoques para el acceso a datos

### API de acceso al perfil del cliente en tiempo real {#rtcp-profile-access-api}

Los clientes pueden acceder a perfiles unificados individuales desde el almacén de perfiles del cliente en tiempo real, que incluye todas las identidades de perfil, las pertenencias a audiencias, los atributos y los eventos de experiencia mediante la API de acceso al perfil del cliente en tiempo real.

Consulte la documentación de la [API de acceso al perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=es) para obtener más información.

#### Casos de uso

* Busque un perfil individual para agregar contexto a la interacción entre cliente y agente, como interacciones de soporte a través de chat y centro de llamadas o bien una interacción de venta en el punto de venta.
* Permite añadir contexto a una descripción de personalización realizada por un sistema externo, como un sistema de personalización web o un sistema de decisión de ofertas.

#### Consideraciones

* Se aplican las [guardas](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es) del perfil del cliente en tiempo real.
* Diseñado para la búsqueda de un solo perfil a la vez. No se utiliza para acceder a perfiles por lotes ni para descargar toda la población de perfiles para el uso de análisis o ciencia de datos.
* El tiempo de respuesta de búsqueda de perfiles se vincula a las guardas de perfil. Requisitos de latencia baja en tiempo real: por ejemplo, para los requisitos de personalización de la misma página, debe utilizar el perfil de Edge desde [Conexión de Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=es) o desde la [Conexión de personalización](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=es) para acceder a perfiles en tiempo real en el navegador y en la personalización de la aplicación.

### API de acceso a datos {#data-access-api}

Con la API de acceso a datos, los clientes pueden acceder directamente a los archivos de conjuntos de datos sin procesar almacenados en el repositorio de datos de Experience Platform.

* Para obtener más información sobre el uso de la API de acceso a datos, consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=es).

#### Casos de uso

* Extraiga archivos de datos tanto sin procesar como procesados de Experience Platform para almacenarlos y evaluarlos en entornos empresariales.

#### Consideraciones

* Como se accede a los datos de forma asíncrona y por lotes, el acceso a los datos estará inherentemente latente en comparación con los enfoques de salida de datos de flujo continuo, como la utilización de etiquetas, el reenvío de eventos o los destinos RTCDP.
* Los archivos de datos procesados en Experience Platform se almacenan como colecciones de archivos en lotes y se comprimen y almacenan en formato de parquet. De esta forma, al acceder y descargar los archivos en un entorno diferente, se debe acceder sistemáticamente a ellos por lote y archivo (a diferencia de como se haría con todo un conjunto de datos), y cualquier operación en los datos debe tener en cuenta los archivos comprimidos en formato de parquet.

### Servicio de consultas {#query-service}

Con el uso del servicio de consultas de Experience Platform, los clientes pueden consultar conjuntos de datos dentro de Experience Platform y mantener los resultados de la consulta. Se puede usar un cliente SQL para consultar y mantener la respuesta de consulta en el destino de almacenamiento deseado que el cliente SQL pueda soportar. La interfaz de usuario del servicio de consulta se puede utilizar para almacenar el resultado de SQL en un conjunto de datos de destino en Experience Platform o bien se puede guardar en el equipo local.

* Para obtener más información sobre la conexión con clientes SQL para mantener los resultados de SQL del servicio de consulta de Experience Platform, consulte la siguiente [documentación](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=es).

#### Casos de uso

* Consulte los datos sin procesar de los conjuntos de datos de Experience Platform y mantenga los resultados de la consulta.
* Consulte el conjunto de datos de instantánea de perfil para extraer perspectivas sobre el perfil del cliente en tiempo real. [Documentación](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=es#profile-attribute-datasets).
* Almacene los resultados de una consulta en un conjunto de datos independiente para acceder a ellos o bien en un conjunto de datos con capacidades de perfil que luego se pueda registrar a través de RTCDP y otras aplicaciones de Experience Cloud que accedan al perfil del cliente en tiempo real.

#### Consideraciones

* Como los datos se consultan de forma asíncrona y por lotes, el acceso a los datos estará inherentemente latente en comparación con los enfoques de salida de datos de flujo continuo, como la utilización de etiquetas, el reenvío de eventos o los destinos RTCDP.
* Solo se pueden consultar los datos disponibles en el repositorio de datos de Experience Platform mediante el servicio de consulta. El almacén de Real-Time Customer Profile, el gráfico de identidad y el Customer Journey Analytics no se pueden consultar directamente mediante el servicio de consulta. Solo cuando se exportan conjuntos de datos al repositorio de datos se pueden consultar estos conjuntos de datos, como en el ejemplo del conjunto de datos de instantánea de perfil.
* Tenga en cuenta que las guardas relativas al número de resultados de una consulta y el tiempo de espera de la consulta se aplican tal como se describe en la documentación [Guardas de los servicios de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=es).

## Enfoques para la exportación de datos

### Extensiones de etiquetas del lado del cliente {#client-side-tags-extensions}

Las extensiones se pueden implementar mediante la solución de etiquetas de Adobe. Una vez implementada la extensión, las solicitudes de datos se implementan directamente en un explorador o aplicación cliente y se puede invocar una solicitud para enviar datos y solicitudes al destino deseado.

Consulte la documentación [Información general sobre etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es) para obtener más información.

#### Casos de uso

* Recopile información de flujo sin procesar directamente desde entornos del lado del cliente mediante el etiquetado.

#### Consideraciones

* No hay acceso directo a ninguna información del lado del servidor, como el perfil del cliente en tiempo real de Experience Platform y las pertenencias a audiencias.
* La adición de etiquetas adicionales de recopilación de datos a la página puede aumentar los tiempos de carga de las páginas.
* Posibilidad de configurar reglas para que solo soliciten datos cuando se cumplan determinados criterios.
* Los datos se recopilan directamente del cliente, lo que limita los tipos de transformaciones y enriquecimiento que se pueden realizar antes de recopilar los datos.

### Reenvío de eventos {#event-forwarding}

Las solicitudes de recopilación de datos se recopilan directamente en el Adobe [!DNL Edge Network]. Desde [!DNL Edge Network] solicitudes a extremos RESTful externos se pueden configurar para reenviar estas solicitudes al destino externo.

Consulte la documentación siguiente [Reenvío de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=es) para obtener más información.

#### Casos de uso

* Recopile información de flujo sin procesar directamente desde entornos del lado del cliente a un extremo empresarial mediante el reenvío de eventos del lado del servidor de Adobe.

#### Consideraciones

* Para utilizar el reenvío de eventos, los datos deben enviarse a [!DNL Edge Network] mediante el SDK web o el SDK móvil.
* El método de reenvío de eventos reduce el tiempo y el peso de la carga de la página porque se agregan etiquetas adicionales a la página.
* Actualmente no se admite ningún enriquecimiento del perfil de Edge u otras fuentes de datos.
* Los filtrados de datos limitados y las transformaciones de asignación sencillas son compatibles.

### Destinos de Real-Time Customer Data Platform {#RTCDP-destinations}

Los datos de atributos de perfil y de pertenencia a audiencias se pueden activar en destinos empresariales y publicitarios. Esto significa que los datos registrados deben introducirse en el perfil del cliente en tiempo real de Experience Platform.

Consulte la documentación [Destinos de Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=es) para obtener más información.

#### Casos de uso

* Active la información de atributos de perfil, como los abonos a audiencias en un almacén de datos empresarial, herramientas de análisis, sistemas de correo electrónico o sistemas de asistencia.
* Active las pertenencias a audiencias del perfil a un anunciante externo para acotar y personalizar el contenido del perfil.

#### Consideraciones

* Se pueden activar los atributos de perfil y las pertenencias a audiencias. Actualmente, los eventos de experiencia sin procesar no se pueden activar como parte de destinos RTCDP.
* Las activaciones se producen en flujo continuo o por lotes según la naturaleza de la evaluación del segmento y la naturaleza del protocolo de ingesta que acepte el destino.

### Acciones personalizadas de Journey Optimizer {#jo-custom-actions}

Con el uso de Journey Optimizer, los clientes pueden invocar una acción personalizada desde el lienzo de recorrido para enviar una carga útil o un mensaje a un extremo de API externo configurado. Se puede configurar una acción para cualquier servicio de cualquier proveedor al que se pueda llamar mediante una API de REST con una carga útil de formato JSON. Esta carga útil puede incluir información de evento, atributos de perfil y datos de evento anteriores, transformaciones y enriquecimientos configurados en el recorrido.

Consulte la documentación [Acciones personalizadas de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=es) para obtener más información.

#### Casos de uso

* Eventos de activación de Experience Platform y Journey Optimizer que incluyan información adicional del perfil del cliente en tiempo real.
* Notificar a sistemas externos cuando un cliente haya alcanzado un punto específico de un recorrido.

#### Consideraciones

* Protección del rendimiento permitido por [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=es) y enriquecimientos admitidos por el [perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es).
* Las acciones personalizadas se pueden llevar a cabo de una en una de forma continua para cada evento o perfil de un recorrido. No se pueden realizar operaciones masivas ni flujos masivos de datos en forma de archivos o solicitudes agregadas entre recorridos de clientes.
* Acceso de flujo continuo a los atributos de perfil del cliente en tiempo real y a los eventos de experiencia que se pueden incluir en la carga útil de activación.
* Los datos de evento se pueden filtrar y se pueden aplicar transformaciones de asignación sencillas antes de enviar eventos a destinos externos.
