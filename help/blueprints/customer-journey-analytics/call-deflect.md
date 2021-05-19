---
title: Modelo de análisis del desvío de llamadas
description: Analice el comportamiento de los clientes antes de que contacten con el centro de llamadas.
solution: Experience Platform, Customer Journey Analytics
kt: 7209
exl-id: 13593c1c-4c58-4b8a-aa6c-7530fd679a14
translation-type: ht
source-git-commit: 9fe9d67c5f97b633e45155bd54e2006f1b797332
workflow-type: ht
source-wordcount: '639'
ht-degree: 100%

---

# Modelo de análisis del recorrido de desvío de llamadas

Analice el comportamiento de los clientes en el ordenador y en el móvil antes de que ellos contacten con el centro de llamadas. Identifique oportunidades de mejora en el recorrido del cliente entendiendo qué acciones intenta concluir, qué contenido quiere ver y qué términos busca antes de contactar con Atención al cliente. Determine el contenido y las herramientas de autoservicio que se pueden mejorar para ayudar al cliente a resolver sus incidencias sin necesidad de contactarnos.

## Casos de uso

* Analizar el comportamiento del cliente antes de que contacte con el servicio de asistencia.
* Descubrir oportunidades de mejora en las capacidades de autoservicio

## Aplicaciones

* Adobe Experience Platform
* Customer Journey Analytics

## Patrones de integración

* Adobe Experience Platform → Customer Journey Analytics

## Arquitectura

<img src="assets/CJA.svg" alt="Arquitectura de referencia para el modelo de Customer Journey Analytics" style="border:1px solid #4a4a4a" />

## Pasos de implementación

1. [Crear esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html?lang=es) para la ingesta de datos.
1. [Crear conjuntos de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) para la ingesta de datos.
1. [Ingesta de datos](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=es) a Experience Platform.
Los datos se deben ingerir en Platform antes de que se procesen en Customer Journey Analytics.
1. Analizar los conjuntos de datos de eventos multicanal.
Los conjuntos de datos analizados juntos deben tener un ID de área de nombres común o ser renombrados a través de la capacidad de combinación basada en campos o Customer Journey Analytics. 

   >[!NOTE]
   >
   >Actualmente, Customer Journey Analytics no utiliza el servicio de perfil ni identidad de Experience Platform para la combinación.

1. Realizar cualquier preparación de datos del cliente o emplear en ellos la combinación de identidades basada en campos para mantener una clave común a través de los conjuntos de datos de series temporales para que se ingieran en Customer Journey Analytics.
1. Estipular in ID principal para los datos de búsqueda, que puede unirse a un campo en los datos de evento. Cuenta como líneas en la licencia.
1. Establecer el mismo ID principal a los datos del perfil y a los del evento.
1. Configurar una conexión de datos para su ingesta de Experience Platform a Customer Journey Analytics. Cuando los datos llegan al repositorio, se procesan en Customer Journey Analytics en un periodo de 90 minutos.
1. Configurar una vista de datos de la conexión para seleccionar las dimensiones y métricas específicas que se incluirán en la vista. La configuración de atribución y asignación también se configura en la vista de datos. Estas configuraciones se computan en el momento del informe.
1. Crear un proyecto para configurar paneles e informes dentro de Analysis Workspace.

## Consideraciones sobre la implementación

### Consideraciones sobre la combinación de identidad

* Los datos de serie temporal que se unan deben tener el mismo ID de área de nombres en todos los registros. Para conectar los datos del centro de llamadas con los del dispositivo anónimo, el ID digital debe estar enlazado con el ID de la llamada. Ese enlace se puede dar con diversos mecanismos:
   * El número marcado debe ser único para ese visitante en ese momento, junto con una tabla de búsqueda para rastrear el vínculo;
   * Requiere que el usuario esté autenticado antes de que solicite la asistencia y enlazar esa autenticación con un identificador determinado por el agente de la llamada (por ejemplo, el número de teléfono o email).
   * Utilice un socio de incorporación para ayudar a introducir identificadores de dispositivos en línea con identificadores conocidos enlazados a la solicitud de asistencia.
* El proceso de unificación de los conjunto de datos dispares requiere mantener una clave común principal por persona/entidad en todos ellos.
* Actualmente, las unificaciones secundarias basadas en claves no son compatibles.
* El proceso de combinación de identidades basadas en campos permite renombrar las identidades en filas según los registros de ID temporales subsecuentes, como en un ID de autenticación. Este proceso permite convertir registros dispares en un ID único para que sea analizado como persona en lugar de dispositivo o cookie.
* La combinación ocurre una vez a la semana, con repetición tras la combinación.

## Preguntas frecuentes

* ¿Cuáles son las consecuencias que se derivan de los modelos de datos en Customer Journey Analytics?

   Los objetos y los atributos del mismo campo XDM se fusionan en una única dimensión en Customer Journey Analytics. Para fusionar varios atributos de varios conjuntos de datos en la misma dimensión de CJA, los conjuntos de datos deben hacer referencia el mismo campo XDM o esquema.

## Documentación relacionada

* [Descripción del producto Customer Journey Analytics](https://helpx.adobe.com/es/legal/product-descriptions/customer-journey-analytics.html)
* [Documentación de Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html?lang=es)
* [Tutoriales de Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html?lang=es)
