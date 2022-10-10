---
title: Modelo de Journey Optimizer con Adobe Campaign
description: Muestra cómo se puede utilizar Adobe Journey Optimizer con Adobe Campaign para enviar mensajes de forma nativa utilizando el servidor de mensajería en tiempo real en Campaign
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: 076446a9-dfb9-464c-a04f-6864b8cb7b48
source-git-commit: 6901596cbb661ffa8cf57c6ae958db1978bf1520
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 92%

---

# Journey Optimizer con Adobe Campaign

Muestra cómo se puede utilizar Adobe Journey Optimizer con Adobe Campaign para enviar mensajes de forma nativa utilizando el servidor de mensajería en tiempo real en Campaign.

<br>

## Arquitectura

<img src="assets/ajo-campaign-architecture.svg" alt="Arquitectura de referencia del modelo de Journey Optimizer" style="width:100%; border:1px solid #4a4a4a" />

>[!IMPORTANT]
>El uso de Journey Optimizer y Campaign para enviar mensajes de forma independiente entre sí es posible, pero tiene algunas consideraciones técnicas que se deben tener en cuenta. Si desea seguir esta ruta, póngase en contacto con su arquitecto empresarial de preventa para asegurarse de que comprende lo que se necesitará para admitir la implementación.

<br>

## Prerrequisitos

### Adobe Experience Platform

* Los esquemas y conjuntos de datos deben configurarse en el sistema para poder configurar las fuentes de datos de Journey Optimizer
* Para los esquemas basados en clases de eventos de experiencia, agregue el grupo de campos &#39;ID de evento de orquestación&#39; cuando desee que se active un evento que no sea un evento basado en reglas
* Para los esquemas basados en clases de perfil individual, agregue el grupo de campos &#39;Detalles de prueba de perfil&#39; para poder cargar perfiles de prueba para utilizarlos con Journey Optimizer
* Journey Optimizer y Campaign se aprovisionan en la misma organización de IMS

### Campaign v7/v8 o Campaign Standard

* La instancia de ejecución del servicio de mensajería en tiempo real (es decir, el Centro de mensajes) debe estar alojada por Adobe Managed Cloud Services
* Toda la creación de mensajes se realiza dentro de la propia instancia de Campaign

<br>

## Guardas

[Vínculo del producto de guardas de Journey Optimizer](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=es)

### Guardas adicionales de Journey Optimizer

* Es posible configurar la limitación a través de la API para asegurar que el sistema de destino no se sature hasta el punto que dé errores. Esto significa que los mensajes que excedan el tope se descartarán completamente y no se enviarán jamás. No se admite establecer limitaciones.
   * Número máximo de conexiones: número máximo de conexiones de http/s que admite el destino.
   * Recuento máximo de llamadas: número máximo de llamadas que se pueden realizar en el parámetro periodInMs.
   * periodInMs: tiempo en milisegundos.
* Los recorridos iniciados por pertenencia a segmentos pueden funcionar de dos modos:
   * Segmentos por lotes (actualizados cada 24 horas)
   * Segmentos por flujo (calificación &lt;5 minutos)
* Segmentos por lotes: debe conocer el volumen diario de usuarios adecuados y garantizar que el sistema de destino pueda soportar el pico de rendimiento por recorrido y durante todos los recorridos.
* Segmentos por flujo: debe asegurarse de que el pico inicial de calificaciones de perfil pueda gestionarse junto con el volumen de calificación de flujo diario por recorrido y durante todos los recorridos.
* Gestión de decisiones no es compatible
* No se admiten los eventos comerciales
* Integraciones salientes a sistemas de terceros
   * No es compatible con una sola IP estática, ya que nuestra infraestructura es de varios inquilinos (debe realizar la lista de permitidos de todas las IP del centro de datos)
   * Solo se admiten métodos de PUT y POST para acciones personalizadas
   * Compatibilidad con autenticación: token | contraseña | OAuth2
* No es posible empaquetar y mover componentes individuales de Adobe Experience Platform o Journey Optimizer entre varios entornos limitados. Debe volver a implementarse en nuevos entornos

<br>

### Integraciones de Campaign

Para obtener instrucciones sobre la integración con su versión específica de Adobe Campaign y Adobe Journey Optimizer, consulte la guía correspondiente para cada versión de Adobe Campaign.

* [Adobe Journey Optimizer y Campaign v7](ajo-and-campaign-v7.md)
* [Adobe Journey Optimizer y Campaign v8](ajo-and-campaign-v8.md)