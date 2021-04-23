---
title: Mensajería por lotes y modelo de Adobe Experience Platform
description: Ejecute campañas de mensajería programadas por lotes con Adobe Experience Platform como repositorio central de los perfiles de clientes y segmentación.
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
translation-type: tm+mt
source-git-commit: 37416aafc997838888edec2658d2621d20839f94
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 59%

---

# Mensajería por lotes y modelo de Adobe Experience Platform

Ejecute campañas de mensajería programadas por lotes con Adobe Experience Platform como repositorio central de los perfiles de clientes y segmentación.

## Casos de uso

* Campañas programadas de email
* Campañas de incorporación y remarketing

## Aplicaciones

* Adobe Experience Platform
* Adobe Campaign Classic o Standard

## Patrones de integración

* Adobe Experience Platform → Adobe Campaign Classic
* Adobe Experience Platform → Adobe Campaign Standard

## Arquitectura

<img src="assets/aepbatch.svg" alt="Arquitectura de referencia para la mensajería por lotes y el modelo de Adobe Experience Platform" style="border:1px solid #4a4a4a" />

## Guardas

* Solo admite implementaciones de unidades organizativas únicas de Adobe Campaign
* Adobe Campaign es la fuente de la verdad para todos los perfiles activos, lo que significa que los perfiles deben existir en Adobe Campaign y que los perfiles nuevos no deben crearse en función de los segmentos del Experience Platform.
* La generación de pertenencia a segmento desde Experience Platform está implícita tanto en lotes (1 al día) como flujo (5 minutos).

**[!UICONTROL Uso compartido de segmentos en tiempo real de la ] plataforma de datos del cliente en Adobe Campaign:**

* Recomendación: máximo de 20 segmentos.
* La activación se limita a cada 24 horas.
* Solo los atributos de esquemas de unión están disponibles para la activación (no es compatible con eventos array/maps/experience).
* Recomendación: máximo de 20 atributos por segmento.
* Un archivo por segmento de todos los perfiles con el abono de segmento “realized” O si el abono de segmento se añade como atributo en el archivo como perfiles “realized” y “exited” a la vez.
* Compatible con la exportación de segmentos incrementales o completos.
* No es compatible con la criptografía de archivos.
* Los flujos de trabajo de exportación de Adobe Campaign se ejecutan como máximo cada 4 horas
* Consulte [los guardas de perfil e ingesta de datos de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)

## Pasos de implementación

### Adobe Experience Platform

#### Esquemas/conjuntos de datos

1. Configurar perfil individual, evento de experiencia y esquemas de identidad múltiple según los datos ofrecidos por los clientes en Experience Platform.
1. Cree esquemas de Adobe Campaign para broadLog, trackingLog, direcciones no entregables y preferencias de perfil (opcional).
1. Añadir etiquetas de uso de datos al conjunto de datos para la gobernanza.
1. Crear políticas que refuercen la gobernanza en los destinos.

#### Perfil/identidad

1. Crear áreas de nombres específicas para los clientes.
1. Añadir identidades a los esquemas.
1. Activar esquemas y conjuntos de datos del perfil.
1. Configure reglas de combinación para diferentes vistas de [!UICONTROL Perfil del cliente en tiempo real] (opcional).
1. Cree segmentos para el uso de Adobe Campaign.

#### Origen/destino

1. Realizar la ingesta de datos en Experience Platform mediante API de flujo y conectores de origen.
1. Configure el [!DNL Azure] destino de almacenamiento del blob para utilizarlo con Adobe Campaign.

#### Implementación de aplicaciones móviles

1. Implemente el SDK de Adobe Campaign para Adobe Campaign Classic o el SDK de Experience Platform para Adobe Campaign Standard. Si el Experience Platform Launch está presente, se recomienda utilizar la extensión de Adobe Campaign Classic o Adobe Campaign Standard con el SDK de Experience Platform.

#### Adobe Campaign

1. Configurar esquemas de perfil, datos de búsqueda y otros datos relevantes de personalización de entrega.

>[!IMPORTANT]
>
>En este momento es fundamental comprender qué es el modelo de datos en Experience Platform de los datos de perfil y evento, de modo que pueda saber qué datos se necesitarán en Adobe Campaign.

#### Importar flujos de trabajo

1. Cargue e incorpore datos de perfil simplificados en Adobe Campaign SFTP.
1. Cargue e incorpore datos de organización y personalización de mensajería en el SFTP de Adobe Campaign.
1. Ingerir segmentos de Experience Platform desde los blobs (objetos binarios grandes) de [!DNL Azure] a través de flujos de trabajo.

#### Exportar flujos de trabajo

1. Vuelva a enviar los registros de Adobe Campaign al Experience Platform mediante flujos de trabajo cada cuatro horas (broadLog, trackingLog, direcciones que no se pueden enviar).
1. Enviar preferencias de perfil de vuelta a Experience Platform a través de flujos de trabajo generados por consulta a cada 4 horas (opcional).


## Documentación relacionada

* [Documentación de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Documentación de Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=es)
* [Documentación de Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=es)
* [Documentación de Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=es)
* [Documentación del SDK móvil de Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=es)
