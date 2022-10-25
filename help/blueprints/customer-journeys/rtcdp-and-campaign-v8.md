---
title: Patrón de integración de Real-Time CDP con Adobe Campaign v8
description: Muestra cómo se puede utilizar Adobe Experience Platform, su funcionalidad Real-Time Customer Profile y la herramienta de segmentación centralizada con Adobe Campaign v8 para ofrecer conversaciones personalizadas.
solution: Real-time Customer Data Platform, Campaign
source-git-commit: f8116387105cf1fe0adfc148562529d62ca90cfc
workflow-type: ht
source-wordcount: '385'
ht-degree: 100%

---

# Patrón de integración de Real-Time CDP con Adobe Campaign v8

Muestra cómo se puede utilizar el perfil del cliente en tiempo real de Adobe Experience Platform y su herramienta de segmentación centralizada con Adobe Campaign para ofrecer conversaciones personalizadas.

<br>

## Aplicaciones

* Adobe Experience Platform Real-Time CDP
* Adobe Campaign v8

<br>

## Arquitectura

<img src="assets/rtcdp-campaignv8-architecture.svg" alt="Arquitectura de referencia del patrón de integración de Adobe Experience Platform y mensajería por lotes" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Prerrequisitos

* El cliente debe poder acceder a Experience Cloud con una organización IMS válida
* Se recomienda aprovisionar Adobe Experience Platform y Campaign en la misma organización IMS para la URL de inicio de sesión único
* El cliente debe estar aprovisionado con la instancia v8 de Campaign
* El cliente debe ser elegible y tener acceso a RTCDP, orígenes y destinos.
* Debe existir el contexto del producto de Adobe Campaign

<br>

## Pasos de implementación

Consulte la siguiente documentación sobre la configuración del conector de origen de Campaign v8 en Adobe Experience Platform y el conector de destino de Real-time Customer Data Platform en Campaign v8.
[Conectores de Campaign y AEP](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=es)

## Guardas

### Adobe Campaign

* Consulte la documentación del conector de origen de Campaign: [conector de origen de Campaign](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/campaign.html?lang=es)
* Solamente compatible con la implementación de entidades organizativas únicas de Adobe Campaign
* Adobe Campaign es la fuente de información verídica de todos los perfiles activos, esto es, que los perfiles deben existir en Adobe Campaign y los nuevos no deben crearse según los segmentos de Experience Platform.


### Uso compartido de segmentos en Real-time Customer Data Platform de Experience Platform

* Consulte el conector de destino de RTCDP Campaign: [conexión de RTCDP Campaign](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=es)
* Recomendación: máximo de 50 segmentos.
* Tenga en cuenta que la realización de la pertenencia a segmentos desde AEP está latente tanto para el lote (1 por día) como para la transmisión (~5 min) y se basa en el programa de evaluación de segmentos.
* La latencia de activación es de 3 horas como mínimo
* Solo los atributos de esquemas de unión están disponibles para la activación (no es compatible con eventos array/maps/experience)
* Recomendación: máximo de 20 atributos por segmento.
* Un archivo por segmento de todos los perfiles con la pertenencia a segmento “realized” O si la pertenencia a segmento se añade como atributo en el archivo como perfiles “realized” y “exited” a la vez.
* Compatible con la exportación de segmentos incrementales y completos.
* No es compatible con la criptografía de archivos.
* Consulte las guardas de ingesta de datos y perfiles para AEP: [vínculo](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)