---
title: Caso de análisis de deformación de llamadas
description: Analice el comportamiento de los clientes antes de ponerse en contacto con el centro de llamadas.
solution: Experience Platform, Customer Journey Analytics
kt: 7209
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---


# Caso de análisis de Recorrido de la deformación de llamadas

Analice el comportamiento de un cliente en equipos de escritorio y móviles antes de ponerse en contacto con el centro de llamadas. Identifique oportunidades para mejorar el recorrido de los clientes al comprender qué acciones intentan completar sus clientes, qué contenido ven y qué términos buscan antes de ponerse en contacto con el servicio de atención al cliente. Determine el contenido y las herramientas de autoservicio que se pueden mejorar para ayudar a sus clientes a resolver problemas sin necesidad de llamar a .

## Casos de uso

* Analizar el comportamiento de los clientes antes de ponerse en contacto con el servicio de asistencia técnica
* Descubra oportunidades para mejorar las capacidades de autoservicio

## Aplicaciones

* Adobe Experience Platform
* Customer Journey Analytics

## Patrones de integración

* Adobe Experience Platform → Customer Journey Analytics

## Arquitectura

<img src="assets/CJA.svg" alt="Arquitectura de referencia para el modelo del Customer Journey Analytics" style="border:1px solid #4a4a4a" />

## Seguridad

Ingesta de datos en el Customer Journey Analytics:

* Ingesta de datos al lago: API ~ 7 GB/hora, conector de origen ~ 200 GB/hora, flujo a lago ~ 15 minutos, conector de origen de Analytics al lago ~ 45 minutos.
* Una vez publicados los datos en el lago de datos, puede tardar hasta 90 minutos en procesarse en Customer Journey Analytics.

## Pasos de la implementación

1. Configure conjuntos de datos y esquemas.
1. Ingeste datos en Platform.
Los datos deben ingerirse en Platform antes de ingerirlos en el Customer Journey Analytics.
1. Analizar conjuntos de datos de eventos de canales cruzados.
Los conjuntos de datos analizados en la unión deben tener un ID de área de nombres común o se deben volver a escribir a través de la capacidad de vinculación basada en campos de Customer Journey Analytics. 

   >[!NOTE]
   >
   >Actualmente, el Customer Journey Analytics no utiliza los servicios de Perfil del Experience Platform o de identidad para la vinculación.

1. Realice cualquier preparación de datos personalizada o use la vinculación de identidad basada en el campo en los datos para garantizar una clave común en los conjuntos de datos de series temporales que se incorporarán en el Customer Journey Analytics.
1. Proporcione un ID principal para los datos de búsqueda, que pueden unirse a un campo en los datos de evento. Cuenta como filas en licencias.
1. Establezca el mismo ID principal en los datos de perfil que el ID principal de los datos de evento.
1. Configure una conexión de datos para introducir datos de Experience Platform a Customer Journey Analytics. Una vez que los datos llegan al lago de datos, se procesan en Customer Journey Analytics en un plazo de 90 minutos.
1. Configure una vista de datos en la conexión para seleccionar las dimensiones y métricas específicas que se incluirán en la vista. La configuración de atribución y asignación también se configura en la vista de datos. Estos ajustes se calculan en el momento del informe.
1. Cree un proyecto para configurar tableros e informes en Analysis Workspace.

## Consideraciones sobre la implementación

### Consideraciones sobre la vinculación de identidad

* Los datos de series temporales que se van a unificar deben tener el mismo espacio de nombres de id en cada registro. Para conectar los datos del centro de llamadas a datos anónimos de dispositivos, el ID digital debe estar vinculado al ID que realiza la llamada. Esta vinculación puede producirse a través de varios mecanismos posibles:
   * El número de marcado es un número de marcado único para ese visitante durante ese tiempo, junto con una tabla de búsqueda para realizar un seguimiento de la relación.
   * Requerir que el usuario se autentique antes de solicitar asistencia técnica y enlazar esta autenticación con un identificador determinado por el agente de llamadas (por ejemplo, número de teléfono o correo electrónico).
   * Utilice un socio de integración para ayudar a escribir identificadores de dispositivo en línea con identificadores conocidos vinculados a la solicitud de asistencia.
* El proceso de unión de conjuntos de datos dispares requiere una clave persona/entidad principal común en todos los conjuntos de datos.
* Actualmente no se admiten uniones secundarias basadas en claves.
* El proceso de vinculación de identidad basado en el campo permite volver a incrustar identidades en filas basándose en registros de ID transitorios posteriores, como un ID de autenticación. Este proceso permite resolver registros dispares en un solo ID para su análisis por persona en lugar de en el dispositivo o la cookie.
* El ajuste se produce una vez a la semana, con reproducción después del punteado.

## Preguntas frecuentes

* ¿Cuál es el impacto descendente de los modelos de datos en Customer Journey Analytics?

   Los objetos y atributos del mismo campo XDM se combinan en una dimensión en el Customer Journey Analytics. Para combinar varios atributos de varios conjuntos de datos en la misma dimensión de CJA, los conjuntos de datos deben hacer referencia al mismo campo o esquema XDM.

## Documentación relacionada

* [Descripción del producto del Customer Journey Analytics](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [documentación del Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [tutoriales del Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)
