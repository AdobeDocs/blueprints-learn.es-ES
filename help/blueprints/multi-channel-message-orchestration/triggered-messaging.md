---
title: Caso de Mensajería activada y Adobe Experience Platform
description: Ejecute mensajes y experiencias activados con Adobe Experience Platform como concentrador central que transmite datos, perfiles de clientes y segmentación.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
translation-type: tm+mt
source-git-commit: df1e14631eddb0055f8e7a42db1e34d459667433
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 1%

---


# Caso de Mensajería activada y Adobe Experience Platform

Ejecute mensajes y experiencias activados con Adobe Experience Platform como concentrador central que transmite datos, perfiles de clientes y segmentación.

## Casos de uso

* Mensajes activados
* Confirmaciones de registro
* Abandonos del carro de compras y del formulario de solicitud
* Mensajes activados por ubicación

## Arquitectura

<img src="assets/triggered.svg" alt="Arquitectura de referencia para el escenario de Mensajería activada y Adobe Experience Platform" style="border:1px solid #4a4a4a" />

## Patrones de integración

* Adobe Experience Platform -> Journey Orchestration

## Requisitos previos

* Adobe Experience Platform
* Journey Orchestration

## Seguridad

### Journey Orchestration

* Consulte el enlace para [más detalles sobre las limitaciones](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en#starting-with-journeys)
* El límite está disponible a través de la configuración de la API para garantizar que el sistema de destino no esté saturado hasta el punto de error. Restricción significa que los mensajes que exceden el límite se descartan completamente y nunca se envían. La restricción aún no es compatible.
   * conexiones máximas: Número máximo de conexiones http/s que un destino puede gestionar
   * recuento máximo de llamadas: Número máximo de llamadas que se realizan en el parámetro periodInMs
   * periodInMs: Tiempo en milisegundos
* Los recorridos iniciados por la pertenencia a segmentos pueden funcionar en dos modos:
   * segmentos por lotes (se actualizan cada 24 horas)
   * Segmentos de transmisión (calificación de 5 minutos)
* Segmentos por lotes: Asegúrese de comprender el volumen diario de usuarios cualificados y de que el sistema de destino pueda gestionar el rendimiento por recorrido y en todos los recorridos
* Segmentos de flujo continuo: Asegúrese de que el arranque inicial de las cualificaciones de perfil se pueda gestionar junto con el volumen de clasificación de transmisión diaria por recorrido y en todos los recorridos
* El destino final debe admitir la API de REST y la carga útil JSON
* Actualmente no admite el Offer decisioning
* Consulte [protecciones de ingesta de datos y perfiles para el Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

### Campaign Standard

* Solo admite 14 tps (50 k por hora) en rendimiento
* No se admiten los recorridos iniciados por la pertenencia a segmentos
* El Journey Orchestration admite eventos de reacción a clics o aperturas de mensajes transaccionales.
* Los registros de mensajería transaccional no se sincronizan de forma nativa con el Experience Platform actualmente, lo que requiere una configuración manual. Se recomienda exportar registros como máximo cada cuatro horas.


## Pasos de la implementación

### Adobe Experience Platform

#### Esquema/Conjuntos de datos

1. Configure perfiles individuales, eventos de experiencia y esquemas de varias entidades en Experience Platform en función de los datos proporcionados por el cliente.
1. Cree esquemas de Campaign para lo siguiente: broadLog, trackingLog, direcciones no entregables y preferencias de perfil (opcional).
1. Agregue etiquetas de uso de datos al conjunto de datos para su administración.
1. Cree políticas para hacer cumplir la gobernanza en los destinos.

#### Perfil/identidad

1. Cree cualquier área de nombres específica del cliente.
1. Añadir identidades a esquemas.
1. Habilite esquemas y conjuntos de datos para el perfil.
1. Configure reglas de combinación para diferentes vistas del Perfil del cliente en tiempo real (opcional).
1. Cree segmentos para el uso de la campaña.

#### Fuentes/Destinos

1. Ingeste datos en el Experience Platform mediante API de flujo continuo y conectores de origen.
1. Configure el destino de almacenamiento del blob [!DNL Azure] para utilizarlo con Campaign.

#### Implementación de aplicación móvil

1. Implemente el SDK de Campaign para el SDK de Campaign Classic o Experience Platform para el Campaign Standard. Si el Experience Platform Launch está presente, se recomienda utilizar la extensión Campaign Classic/estándar con el SDK de Experience Platform.


### Journey Orchestration

1. Los datos de flujo utilizados para iniciar un recorrido de cliente deben configurarse primero en el Journey Orchestration para obtener un ID de organización. A continuación, este ID de organización se proporciona al desarrollador para que lo utilice con la ingesta.
1. Configure fuentes de datos externas.
1. Configure acciones personalizadas.

### Campaign Standard

1. Configure las plantillas de mensajería con los ajustes de personalización adecuados.
1. Configure los flujos de trabajo de exportación para exportar los registros de mensajería transaccional. La recomendación es que se ejecute como máximo cada cuatro horas.


## Documentación relacionada

* [Documentación de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [documentación del Journey Orchestration](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=en)
* [documentación del Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [documentación del Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [documentación del Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Documentación del SDK de Experience Platform Mobile](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
