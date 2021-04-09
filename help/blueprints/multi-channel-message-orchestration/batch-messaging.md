---
title: Mensajería por lotes y modelo de Adobe Experience Platform
description: Ejecute campañas de mensajería programadas y por lotes utilizando Adobe Experience Platform como concentrador central para perfiles y segmentación de clientes.
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
translation-type: tm+mt
source-git-commit: 37416aafc997838888edec2658d2621d20839f94
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Mensajería por lotes y modelo de Adobe Experience Platform

Ejecute campañas de mensajería programadas y por lotes utilizando Adobe Experience Platform como concentrador central para perfiles y segmentación de clientes.

## Casos de uso

* Campañas de correo electrónico programadas
* Incorporación y remarketing de campañas

## Aplicaciones

* Adobe Experience Platform
* Adobe Campaign Classic o Standard

## Patrones de integración

* Adobe Experience Platform → Adobe Campaign Classic
* Adobe Experience Platform → Adobe Campaign Standard

## Arquitectura

<img src="assets/aepbatch.svg" alt="Arquitectura de referencia para la mensajería por lotes y el modelo de Adobe Experience Platform" style="border:1px solid #4a4a4a" />

## Seguridad

* Solo admite implementaciones de unidades organizativas únicas de Adobe Campaign
* Adobe Campaign es la fuente de la verdad para todos los perfiles activos, lo que significa que los perfiles deben existir en Adobe Campaign y que los perfiles nuevos no deben crearse en función de los segmentos del Experience Platform.
* La realización de la pertenencia al segmento desde el Experience Platform está latente tanto para el lote (1 por día) como para la transmisión (unos 5 minutos)

**[!UICONTROL Uso compartido de segmentos en tiempo real de la ] plataforma de datos del cliente en Adobe Campaign:**

* Recomendación del límite de 20 segmentos
* La activación está limitada a cada 24 horas
* Solo los atributos de esquema de unión están disponibles para la activación (no se admiten los eventos de matriz/mapas/experiencia).
* Recomendación de no más de 20 atributos por segmento
* Un archivo por segmento de todos los perfiles con pertenencia a segmentos &quot;realizada&quot; O si la pertenencia a segmentos se agrega como atributo en el archivo tanto perfiles &quot;realizados&quot; como perfiles &quot;salidos&quot;
* Se admiten las exportaciones de segmentos incrementales o completos
* No se admite el cifrado de archivos
* Los flujos de trabajo de exportación de Adobe Campaign se ejecutan como máximo cada 4 horas
* Consulte [protecciones de ingesta de datos y perfiles para el Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Pasos de la implementación

### Adobe Experience Platform

#### Esquema/Conjuntos de datos

1. Configure perfiles individuales, eventos de experiencia y esquemas de varias entidades en Experience Platform, según los datos proporcionados por el cliente.
1. Cree esquemas de Adobe Campaign para broadLog, trackingLog, direcciones no entregables y preferencias de perfil (opcional).
1. Agregue etiquetas de uso de datos al conjunto de datos para su administración.
1. Cree políticas que hagan cumplir la gobernanza en los destinos.

#### Perfil/identidad

1. Cree cualquier área de nombres específica del cliente.
1. Añadir identidades a esquemas.
1. Habilite esquemas y conjuntos de datos para el perfil.
1. Configure reglas de combinación para diferentes vistas de [!UICONTROL Perfil del cliente en tiempo real] (opcional).
1. Cree segmentos para el uso de Adobe Campaign.

#### Fuentes/Destinos

1. Ingeste datos en el Experience Platform mediante API de flujo continuo y conectores de origen.
1. Configure el [!DNL Azure] destino de almacenamiento del blob para utilizarlo con Adobe Campaign.

#### Implementación de aplicación móvil

1. Implemente el SDK de Adobe Campaign para Adobe Campaign Classic o el SDK de Experience Platform para Adobe Campaign Standard. Si el Experience Platform Launch está presente, se recomienda utilizar la extensión de Adobe Campaign Classic o Adobe Campaign Standard con el SDK de Experience Platform.

#### Adobe Campaign

1. Configure esquemas para perfiles, datos de búsqueda y datos de personalización de envíos relevantes.

>[!IMPORTANT]
>
>En este momento es fundamental comprender qué es el modelo de datos en Experience Platform de los datos de perfil y evento, de modo que pueda saber qué datos se necesitarán en Adobe Campaign.

#### Importación de flujos de trabajo

1. Cargue e incorpore datos de perfil simplificados en Adobe Campaign SFTP.
1. Cargue e incorpore datos de organización y personalización de mensajería en el SFTP de Adobe Campaign.
1. Ingeste segmentos de Experience Platform del blob [!DNL Azure] mediante flujos de trabajo.

#### Exportación de flujos de trabajo

1. Vuelva a enviar los registros de Adobe Campaign al Experience Platform mediante flujos de trabajo cada cuatro horas (broadLog, trackingLog, direcciones que no se pueden enviar).
1. Vuelva a enviar las preferencias de perfil al Experience Platform mediante flujos de trabajo creados por consultoría cada cuatro horas (opcional).


## Documentación relacionada

* [Documentación de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [documentación del Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [documentación del Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [documentación del Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Documentación del SDK de Experience Platform Mobile](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
