---
title: Activación de cuenta B2B en Advertising y destinos de archivo
description: Utilice la participación basada en cuentas para crear audiencias de cuenta y activarlas en destinos de publicidad y almacenamiento en la nube.
solution: Real-Time Customer Data Platform
exl-id: 578c0019-6133-4508-ae9d-8a8a463376f0
source-git-commit: 7f0b624616480cf563142c08eb0598d1dd55d551
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 1%
---

# Activación de cuentas B2B en destinos publicitarios y destinos de archivos

La participación basada en cuentas permite a los especialistas en marketing B2B crear audiencias de cuentas (listas de empresas) en **Real-Time Customer Data Platform B2B edition** y activar esas audiencias de cuenta en destinos publicitarios como LinkedIn Matched Audiences, Bombora y Demandbase, así como en destinos de almacenamiento en la nube. Estas audiencias de cuenta pueden utilizarse para direccionamiento, alcance de ventas y análisis descendente.

## Casos de uso

Mediante la participación basada en cuentas, los especialistas en marketing pueden desbloquear tres casos de uso clave:

- **Rellenar huecos de grupos de compras:** Un experto en marketing puede anunciarse en cuentas en las que aún no tenga contactos para los roles de CMO o CIO. Primero pueden crear una audiencia de cuentas sin un contacto con el título &quot;CMO&quot; o &quot;CIO&quot; y luego activar la audiencia en Audiencias coincidentes de LinkedIn u otros destinos de publicidad admitidos. Dentro del destino, pueden lanzar una campaña dirigida a esa audiencia y a personas específicas con puestos de trabajo de &quot;CMO&quot; o &quot;CIO&quot; para llegar a estos nuevos contactos y destacar las ventajas de sus ofertas.
- **Ampliar ventas o realizar ventas cruzadas a otras divisiones de una compañía que ya sea cliente:** Un experto en marketing puede crear una audiencia de cuenta que compró el producto X entre 3 y 9 meses atrás, pero aún no es propietario del producto Y. Luego pueden activar esta audiencia de cuenta, resaltando los beneficios del producto Y para esa audiencia objetivo a través de Audiencias coincidentes de LinkedIn, otras plataformas de publicidad o exportaciones de almacenamiento en la nube para el alcance de ventas y marketing.
- **Compañías de Target que utilizan productos de la competencia:** Un experto en marketing puede comercializar cuentas para desplazar los productos de un competidor, incluso sin contactos en esas cuentas. Pueden crear una audiencia de cuentas basadas en datos de socios o de intención que muestren la propiedad o el uso del producto de un competidor y, a continuación, activarlas mediante Audiencias coincidentes de LinkedIn u otros destinos de publicidad admitidos para obtener contactos en cuentas de destino para su expansión.

## Aplicaciones

- Real-Time Customer Data Platform B2B edition
- (Opcional) Customer Journey Analytics B2B edition

## Patrones de integración

Los patrones de integración habituales para este modelo incluyen:

- **Fuentes de participación y CRM B2B → audiencias de cuenta de → de RTCDP B2B edition → destinos**

  La participación B2B y los sistemas CRM como Marketo Engage, Salesforce y Microsoft Dynamics envían posibles clientes/contactos, cuentas y oportunidades a **Real-Time CDP B2B edition** mediante los esquemas y relaciones B2B estándar. Las audiencias de cuenta se crean sobre este modelo de datos unificado B2B y se activan para los destinos de publicidad y archivos.

- **Fuentes de intención y evento B2B → audiencias de cuenta de → de RTCDP B2B edition → destinos**

  Las fuentes de intención y evento B2B, como Bombora Intent y Demandbase Intent, envían eventos de intención y participación a Experience Platform. Estos conjuntos de datos se asignan a los esquemas B2B estándar, lo que permite a los especialistas en marketing crear audiencias de cuenta (por ejemplo, cuentas que surgen en temas de la competencia) y activarlas en destinos de publicidad y almacenamiento en la nube. Las audiencias de cuenta se pueden activar a socios publicitarios como Bombora y Demandbase donde sea compatible.

## Arquitectura

<img src="assets/b2b-account-activation.png" alt="Arquitectura de referencia para el modelo de activación de cuenta B2B" style="border:1px solid #4a4a4a"  width="100%" />

## Destinos de audiencia de cuenta

- **Audiencias coincidentes de LinkedIn**
- **Bombora**
- **Demandbase**
- **Destinos de almacenamiento en la nube**
  - Almacenamiento de Azure Data Lake Gen2
  - Data Landing Zone
  - SFTP
  - Azure Blob
  - AWS S3

Consulte la documentación de destino para obtener la lista más reciente de destinos compatibles con las audiencias de cuenta.

## Guardas

Consulte las siguientes protecciones al diseñar y activar audiencias de cuenta:

- [Protecciones para Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [Audiencias de cuenta](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/account-audiences?lang=en)
- [Activar audiencias de cuenta](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en)
- [Protecciones de perfil y segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- [Actualización de criterios de idoneidad de segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/eligibility-criteria-update)

## Pasos de implementación de Real-Time Customer Data Platform B2B edition, creación de audiencias de cuenta y activación

- Para ver los pasos de implementación de Real-Time Customer Data Platform B2B edition, consulte la siguiente documentación: [Introducción a Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial?lang=en).
- Para ver los pasos de creación de audiencias de cuenta, consulte la documentación de [audiencias de cuenta](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/account-audiences?lang=en).
- Para ver los pasos de activación de Audiencia de cuenta, consulte la documentación de [Activar audiencias de cuenta](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en):

  - Asignación requerida para [destino de audiencias coincidentes de LinkedIn](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en#required-mappings).

## Consideraciones sobre la implementación

Las audiencias coincidentes de LinkedIn tienen un requisito mínimo de tamaño de audiencia (por ejemplo, 300 miembros coincidentes). Si la audiencia de la cuenta activada en Audiencias coincidentes de LinkedIn no cumple este requisito, es posible que tenga que ampliar la definición de audiencia para aumentar el tamaño de audiencia coincidente antes de lanzar una campaña.

## Documentación relacionada

- [Modelo de activación de audiencia y perfil B2B](b2bactivation.md): modelo principal que cubre la activación B2B a nivel de persona y de cuenta.
- [B2B edition de Real-Time Customer Data Platform](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview?lang=en)
- [Creación y activación de una audiencia de cuenta: tutorial en vídeo](https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/audiences/create-audiences-with-b2b-data?lang=en)
- [Crear audiencias de cuenta](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/account-audiences?lang=en)
- [Activar audiencias de cuenta](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en)
- [Adobe Experience Platform - Conector de destino de LinkedIn](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/social/linkedin?lang=en)
- [Esquemas en Real-Time CDP B2B edition](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/schemas/b2b)
- [Actualizaciones de arquitectura a Real-Time CDP B2B edition](https://experienceleague.adobe.com/es/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade)
- [Guardas de destino](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/guardrails)
