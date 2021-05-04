---
title: Análisis de Recorridos en todos los canales
description: Analizar y extraer información de interacciones del cliente mediante su recorrido.
solution: Experience Platform, Customer Journey Analytics, Data Collection
kt: 7208
exl-id: b042909c-d323-40d5-8b35-f3e5e3e26694
translation-type: tm+mt
source-git-commit: 58368eb06b9bbd6c332424bdcfa2789dde7d4c2f
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 98%

---

# Modelo de análisis de Recorrido en todos los canales

Obtenga una sola vista consolidada con el comportamiento del cliente para todos los diferentes canales, unificando los datos de distintas propiedades web, móvil y sin conexión.

## Casos de uso

* Analizar la interacción del cliente en el ordenador y en el móvil para entender su comportamiento y extraer datos que optimicen su experiencia.
* Analizar la interacción del cliente en todos los canales, incluyendo los digitales y sin conexión, como interacciones con la asistencia y las compras en tienda, para entender mejor y optimizar el recorrido del cliente. 

## Aplicaciones

* Adobe Experience Platform
* Customer Journey Analytics
* Adobe Analytics (opcional)

## Patrones de integración

* Adobe Experience Platform → Customer Journey Analytics
* Adobe Analytics → Adobe Experience Platform → Customer Journey Analytics

## Arquitectura

<img src="assets/CJA.svg" alt="Arquitectura de referencia para el modelo de Customer Journey Analytics" style="border:1px solid #4a4a4a" />

## Pasos de implementación

1. Configurar conjunto de datos y esquemas.
1. Ingerir datos en Platform.
Los datos deben enviarse a Platform antes de que se procesen en Customer Journey Analytics.
1. Analizar conjuntos de datos de eventos multicanal para que se estudien juntos, asegurando que tengan el mismo ID de área de nombres o se reescriban a través de la capacidad de combinación basada en campos de Customer Journey Analytics. 

   >[!NOTE]
   >
   >Actualmente, Customer Journey Analytics no utiliza el servicio de perfil ni identidad de Experience Platform para la combinación.

1. Realizar cualquier preparación de datos del cliente o emplear en ellos la combinación de identidades basada en campos para mantener una clave común a través de los conjuntos de datos de series temporales para que se ingieran en Customer Journey Analytics.
1. Asignar a los datos de búsqueda un ID principal que se puede unir a un campo en los datos de evento. Cuenta como líneas en la licencia.
1. Establecer el mismo ID principal para los datos del perfil y del evento.
1. Configurar una conexión de datos para ingerirlos de Experience Platform a Customer Journey Analytics. Cuando los datos llegan al repositorio, se procesan en Customer Journey Analytics en un periodo de 90 minutos.
1. Configurar una vista de datos de la conexión para seleccionar las dimensiones y métricas específicas que se incluirán en la vista. La configuración de atribución y asignación también se configura en la vista de datos. Estas configuraciones se computan en el momento del informe.
1. Crear un proyecto para configurar paneles e informes dentro de Analysis Workspace.

## Consideraciones sobre la implementación

### Consideraciones sobre la combinación de identidad

* Los datos de serie temporal que se unan deben tener el mismo ID de área de nombres en todos los registros.
* El proceso de unificación de los conjunto de datos dispares requiere mantener una clave común principal por persona/entidad en todos ellos.
* Actualmente, las unificaciones secundarias basadas en claves no son compatibles.
* El proceso de combinación de identidades basadas en campos permite renombrar las identidades en filas según los registros de ID temporales subsecuentes, como en un ID de autenticación. Esto permite convertir registros dispares en un ID único para que se analice como persona en lugar de dispositivo o cookie.
* La combinación ocurre una vez a la semana, con repetición tras la combinación.

## Preguntas frecuentes

* ¿Cuáles son las consecuencias que se derivan de los modelos de datos en Customer Journey Analytics?

   Los objetos y los atributos del mismo campo XDM se fusionan en una única dimensión en Customer Journey Analytics. Para fusionar varios atributos de varios conjuntos de datos en la misma dimensión de Customer Journey Analytics, los conjuntos de datos deben hacer referencia el mismo campo XDM o esquema.

## Documentación relacionada

* [Descripción del producto Customer Journey Analytics](https://helpx.adobe.com/es/legal/product-descriptions/customer-journey-analytics.html)
* [Documentación de Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html?lang=es)
* [Tutoriales de Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html?lang=es)
