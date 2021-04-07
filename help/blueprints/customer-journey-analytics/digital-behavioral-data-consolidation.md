---
title: Modelo de consolidación de datos de comportamiento digital
description: Analice y extraiga perspectivas de las interacciones de los clientes en todo el recorrido de clientes.
solution: Experience Platform, Customer Journey Analytics, Data Collection
kt: 7208
exl-id: b042909c-d323-40d5-8b35-f3e5e3e26694
translation-type: tm+mt
source-git-commit: 844fff1cefe367575beb5c03aa0f0d026eb9f39b
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Modelo de consolidación de datos de comportamiento digital

Disponer de una sola vista consolidada del comportamiento de los clientes en varios canales mediante la unificación de datos de varias propiedades web, móviles y sin conexión.

## Casos de uso

* Analice las interacciones de los clientes en equipos de escritorio y dispositivos móviles para comprender el comportamiento de los clientes y extraer perspectivas para optimizar las experiencias de los clientes digitales.
* Analice las interacciones de los clientes entre canales, incluidos los canales digitales y sin conexión, como las interacciones de soporte y las compras en tiendas, para comprender y optimizar mejor el recorrido de los clientes. 

## Aplicaciones

* Adobe Experience Platform
* Customer Journey Analytics
* Adobe Analytics (opcional)

## Patrones de integración

* Adobe Experience Platform → Customer Journey Analytics
* Adobe Analytics → Adobe Experience Platform → Customer Journey Analytics

## Arquitectura

<img src="assets/CJA.svg" alt="Arquitectura de referencia para el modelo del Customer Journey Analytics" style="border:1px solid #4a4a4a" />

## Seguridad

Ingesta de datos en el Customer Journey Analytics:

* Ingesta de datos al lago: API ~ 7 GB/hora, conector de origen ~ 200 GB/hora, flujo a lago ~ 15 minutos, conector de origen Adobe Analytics al lago ~ 45 minutos.
* Una vez publicados los datos en el lago de datos, puede tardar hasta 90 minutos en procesarse en Customer Journey Analytics.

## Pasos de la implementación

1. Configure conjuntos de datos y esquemas.
1. Ingeste datos en Platform.
Los datos deben ingerirse en Platform antes de procesarse en Customer Journey Analytics.
1. Analice los conjuntos de datos de eventos de canales cruzados para analizarlos en una unión a fin de asegurarse de que tengan un ID de área de nombres común o de que se redefinan mediante la capacidad de vinculación basada en el campo de Customer Journey Analytics. 

   >[!NOTE]
   >
   >Actualmente, el Customer Journey Analytics no utiliza los servicios de Perfil del Experience Platform o de identidad para la vinculación.

1. Realice cualquier preparación de datos personalizada o use la vinculación de identidad basada en el campo en los datos para garantizar una clave común en los conjuntos de datos de series temporales que se incorporarán en el Customer Journey Analytics.
1. Asigne un ID principal a los datos de búsqueda que pueda unirse a un campo en los datos de evento. Cuenta como filas en licencias.
1. Establezca el mismo ID principal para los datos de perfil que el ID principal de los datos de evento.
1. Configure una conexión de datos para introducir datos de Experience Platform a Customer Journey Analytics. Una vez que los datos llegan al lago de datos, se procesan en Customer Journey Analytics en un plazo de 90 minutos.
1. Configure una vista de datos en la conexión para seleccionar las dimensiones y métricas específicas que se incluirán en la vista. La configuración de atribución y asignación también se configura en la vista de datos. Estos ajustes se calculan en el momento del informe.
1. Cree un proyecto para configurar tableros e informes en Analysis Workspace.

## Consideraciones sobre la implementación

### Consideraciones sobre la vinculación de identidad

* Los datos de series temporales que se van a unificar deben tener el mismo espacio de nombres de ID en cada registro.
* El proceso de unión de conjuntos de datos dispares requiere una clave persona/entidad principal común en todos los conjuntos de datos.
* Actualmente no se admiten uniones secundarias basadas en claves.
* El proceso de vinculación de identidad basado en el campo permite volver a incrustar identidades en filas basándose en registros de ID transitorios posteriores, como un ID de autenticación. Esto permite resolver registros dispares en un único ID para su análisis en el nivel de la persona, en lugar de en el nivel de dispositivo o cookie.
* El ajuste se produce una vez a la semana, con reproducción después del punteado.

## Preguntas frecuentes

* ¿Cuál es el impacto descendente de los modelos de datos en Customer Journey Analytics?

   Los objetos y atributos del mismo campo XDM se combinan en una dimensión en el Customer Journey Analytics. Hasta  combinar varios atributos de varios conjuntos de datos en la misma dimensión de Customer Journey Analytics, los conjuntos de datos deben hacer referencia al mismo campo o esquema XDM.

## Documentación relacionada

* [Descripción del producto del Customer Journey Analytics](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [documentación del Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [tutoriales del Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)
