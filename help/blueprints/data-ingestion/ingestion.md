---
title: Modelo de preparación e ingesta de datos
description: Este modelo muestra todos los métodos por los cuales se puede realizar la ingesta y preparación de datos en Adobe Experience Platform.
solution: Data Collection
kt: 7204
thumbnail: null
exl-id: 21f8a73e-6be7-448e-8cd3-ebee9fc848e1
source-git-commit: f22ff4ac15b21592226f6645ab28f30473996776
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# Modelo de preparación e ingesta de datos

El modelo de preparación e ingesta de datos engloba todos los métodos por los cuales se puede realizar la ingesta y preparación de datos en Adobe Experience Platform.

La preparación de datos incluye mapear los datos de origen en el esquema del Modelo de datos de experiencia (XDM). También incluye realizar transformaciones de datos, como dar formato a las fechas, unir/concatenar/convertir campos o unir/fusionar/reescribir registros. La preparación de datos ayuda a unificar la información del cliente, lo que ofrece un análisis agregado/filtrado, incluyendo la creación de informes o la preparación de datos para el ensamblaje/ciencia de datos/activación de perfiles de los clientes.

## Arquitectura

<img src="../experience-platform/assets/aep_data_flow.svg" alt="Arquitectura de referencia para el modelo de preparación e ingesta de datos" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" class="modal-image" />

## Guardas de ingesta de datos

El diagrama siguiente ilustra la latencia y los guardas de rendimiento promedio para la ingesta de datos en Adobe Experience Platform.

<img src="../experience-platform/assets/aep_data_flow_guardrails.svg" alt="Flujo de datos de Experience Platform" style="border:1px solid #4a4a4a; margin-bottom: 15px;" width="90%" class="modal-image" />

## Métodos de ingesta de datos

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1123px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:31px; vertical-align:top; width:1123px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Orígenes de flujo</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Método</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:401px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Casos de uso comunes</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protocolos</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:282px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Consideraciones</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es" style="color:#0563c1; text-decoration:underline">SDK web/móvil de Adobe</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Recopilación de datos de sitios web y aplicaciones móviles.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Método preferido para la recopilación del lado del cliente.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, HTTP, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Implemente varias aplicaciones de Adobe utilizando un único SDK.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=es" style="color:#0563c1; text-decoration:underline">Conector de API HTTP</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Recopilación a partir de orígenes de flujo, transacciones, eventos relevantes del cliente y señales</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, API de REST, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Los datos se transmiten directamente al hub, por lo que no hay segmentación en tiempo real de Edge ni reenvío de eventos.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=es" style="color:#0563c1; text-decoration:underline">API de Edge Network</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Recopilación a partir de orígenes de flujo, transacciones, eventos relevantes del cliente y señales de Edge Network distribuida globalmente</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, API de REST, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Los datos se transmiten a través de Edge Network. Es compatible con la segmentación en tiempo real en Edge. </span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=es" style="color:#0563c1; text-decoration:underline">Aplicaciones de Adobe</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Implementación previa de Adobe Analytics, Marketo, Campaign, Target, AAM</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, conectores de origen y API</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">El enfoque recomendado es la migración al SDK web/móvil en lugar de los SDK de aplicaciones tradicionales.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=es" style="color:#0563c1; text-decoration:underline">Conectores de origen de streaming</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingesta de un flujo de eventos empresariales, que normalmente se utiliza para compartir datos empresariales en varias aplicaciones de flujo descendente. </span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, API de REST, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Se debe transmitir en formato XDM.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">SDK de orígenes de flujo</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Al igual que el conector de API HTTP, permite la tarjeta de configuración de autoservicio de un flujo de datos externo.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, API HTTP, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Edge Network</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1105px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:37px; vertical-align:top; width:1105px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Orígenes por lote</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Método</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:397px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Casos de uso comunes</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protocolos</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:277px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Consideraciones</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=es" style="color:#0563c1; text-decoration:underline">API de ingesta por lotes</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingesta de una empresa administrada. Limpieza y transformación de datos antes de su ingesta.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, JSON o Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Debe administrar lotes y archivos para la ingesta</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/cloud-storage/blob-s3.html?lang=es" style="color:#0563c1; text-decoration:underline">Conectores de origen por lotes</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Enfoque común para la ingesta de archivos desde ubicaciones de almacenamiento en la nube.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Conectores para aplicaciones comunes de CRM y marketing.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ideal para la ingesta de grandes cantidades de datos históricos.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">No está siempre activado, ingesta inmediata. </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">La frecuencia recurrente comprueba la ingesta de archivos delta cada 15 minutos como mínimo.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/cloud-storage/data-landing-zone.html?lang=es" style="color:#0563c1; text-decoration:underline">Data Landing Zone</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ubicación de almacenamiento de archivos aprovisionada por Adobe a la que enviar los archivos para su ingesta.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">- Se proporcionan archivos TTL de 7 días</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/sdk/overview.html?lang=es" style="color:#0563c1; text-decoration:underline">SDK de orígenes por lote</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Permite la tarjeta de configuración de autoservicio de una fuente de datos externa.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ideal para conectores de socios o para una experiencia de flujo de trabajo adaptada para configurar un conector de empresa.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Archivos de pull, API de REST, CSV o JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Frecuencia mínima de 15 minutos</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ejemplos: MailChimp, One Trust, Zendesk</span></span></span></li>
</ul>

<p> </p>
</td>
</tr>
</tbody>
</table>



| Métodos de ingesta | Descripción |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SDK web/móvil | Latencia:<ul><li>Tiempo real, misma colección de páginas que Edge Network.</li><li>Ingesta de flujo al perfil ~1 minuto.</li><li>Ingesta de flujo al repositorio de datos (lote pequeño ~15 minutos).</ul>Documentación: <ul><li>[SDK Web](https://experienceleague.adobe.com/docs/web-sdk.html?lang=es)</li><li>[Tutorial de implementación de Adobe Experience Cloud con SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es)</li><li>[SDK móvil](https://experienceleague.adobe.com/docs/mobile.html?lang=es)</li><li>[Tutorial sobre implementación de Adobe Experience Cloud en aplicaciones móviles](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=es)</li></ul> |
| Orígenes de flujo | [Orígenes de flujo](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=es#connectors)<br>Latencia:<ul><li>Tiempo real, misma colección de páginas que Edge Network.</li><li>Ingesta de flujo al perfil ~1 minuto.</li><li>Ingesta de flujo al repositorio de datos (lote pequeño ~15 minutos).</li></ul> |
| API de flujo | [API del servidor de Edge Network (preferida)](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=es): admite los servicios de Edge, incluida la segmentación de Edge y <br>[API Data Collection Core Service](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/streaming/http.html?lang=es): no admite los servicios de Edge, dirige directamente al hub.<br>Latencia:<ul><li>Tiempo real, misma colección de páginas que Edge Network.</li><li>Ingesta de flujo al perfil ~1 minuto.</li><li>Ingesta de flujo al repositorio de datos (lote pequeño ~15 minutos).</li><li>7 GB/hora</li></ul>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=es#what-can-you-do-with-streaming-ingestion%3F) |
| Herramientas ETL | Utiliza herramientas ETL para modificar y transformar datos empresariales antes de su ingesta en Experience Platform.<br><br>Latencia:<ul><li>El tiempo depende de la programación de la herramienta ETL externa. A continuación, se aplican guardas estándar de ingesta según el método de ingesta utilizado.</li></ul> |
| Orígenes por lote | Extracción programada desde origen<br>Latencia: ~ 200 GB/hora.<br><br>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=es#connectors)<br>[Tutoriales en vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html?lang=es) |
| API por lote | Latencia:<ul><li>Ingesta por lotes a perfiles condicionados por tamaño y carga de tráfico ~45 minutos.</li><li>Ingesta por lotes a repositorios de datos condicionados por tamaño y carga de tráfico.</li></ul>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=es#batch) |
| Conectores de aplicaciones Adobe | Realizan la ingesta de datos procedentes de las aplicaciones de Adobe Experience Cloud automáticamente.<ul><li>Adobe Analytics: [documentación](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=es#connectors) y [tutorial en vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=es)</li><li>Audience Manager: [documentación](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=es#connectors) y [tutorial en vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html?lang=es)</li></ul> |


## Métodos de preparación de datos

| Métodos de preparación de datos | Descripción |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Herramienta ETL externa ([!DNL Snaplogic], [!DNL Mulesoft], [!DNL Informatica], etc.) | Realizar transformaciones complejas en herramientas ETL y utilizar las API o los conectores de origen estándar de [!UICONTROL Flow Service] de Experience Platform para la ingesta de datos resultantes. |
| [!UICONTROL Servicio de consultas]: preparación de datos | Une, divide, fusiona, transforma, consulta y filtra datos en un nuevo conjunto de datos. <br>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=es#sql) sobre el uso de Create Table as Select (CTAS) |
| Funciones del mapeador XDM y preparación de datos (flujo y lotes) | Mapear atributos de origen en formato CSV o JSON en atributos XDM durante la ingesta de Experience Platform.<br>Computa funciones de datos mientras se realiza la ingesta; esto es, les da formato, los divide, los concatena, etc.<br>[Documentación](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=es) |

## Entradas relacionadas en el blog

* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page-------------------------------------)
* [[!DNL High Throughput Ingestion with Iceberg]](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page-------------------------------------)
* [[!DNL Query Service Tricks in Adobe Experience Platform (Writing Queries and Storing Derived Datasets)]](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page-------------------------------------)
* [[!DNL Digging into Adobe Experience Platform's Experience Data Model to More Fully Understand the Power of Real-time Customer Profile]](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page-------------------------------------)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page-------------------------------------)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page-------------------------------------)
