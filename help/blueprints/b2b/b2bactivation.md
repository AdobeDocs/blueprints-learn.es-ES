---
title: Modelo de activación de audiencias y perfiles B2B
description: Ofrezca experiencias de cliente centradas en el perfil y audiencias basadas en la cuenta con Real-Time Customer Data Platform.
solution: Real-Time Customer Data Platform
kt: 9311
exl-id: 5215d077-b0a9-4417-ae9b-f4961d4a73fa
source-git-commit: 0509c5a8ce92c25040262130a5f583cdd7f08e59
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 52%

---

# Modelo de activación de audiencias y perfiles B2B

Utilice la información de cuentas, oportunidades y posibles clientes vinculada a un cliente individual para crear perfiles B2B procesables y, así, mejorar la personalización y la segmentación en todos los canales.

## Casos de uso

* Cree audiencias de personas para segmentación y personalización entre canales con datos B2B, incluidas cuentas, oportunidades y posibles clientes.
* Active audiencias en cualquier destino de Experience Platform para segmentación y personalización.
* Cree audiencias de cuentas (por ejemplo, listas de empresas) y diríjase a esas empresas a través de destinos como LinkedIn que acepten listas de empresas como entrada o exportación a destinos de almacenamiento en la nube para fines de segmentación y alcance de ventas.

## Aplicaciones

* Real-Time Customer Data Platform edición B2B

## Patrones de integración

* Fuentes de datos B2B (Marketo, Salesforce, etc.) -> Real-time Customer Data Platform B2B edition -> Destinos
* Se pueden utilizar varias fuentes de datos B2B para asignar datos de cuenta, posible cliente, oportunidad y personas a B2B edition de Real-time Customer Data Platform.

## Arquitectura

![Arquitectura de referencia para el modelo de activación B2B](assets/b2b-activation.png)

## Guardas

* Tenga en cuenta que los guardas y los pasos de implementación relacionados con Marketo Engage solo son relevantes cuando Marketo Engage se utiliza como origen o destino.

* Para obtener detalles y protecciones adicionales para el modelo de datos, el tamaño y la segmentación, consulte el [documento de protecciones de implementación](../experience-platform/guardrails.md)


### Admisión de varias instancias y organizaciones de IMS:

A continuación, se describen los patrones admitidos de asignación de instancias de Experience Platform y Marketo Engage.

#### Marketo como fuente de datos para Experience Platform:

* Se admiten varias instancias de Marketo Engage en una instancia de Experience Platform.
* No se admite una instancia de Marketo Engage en varias instancias de Experience Platform.
* Se admite una instancia de Marketo Engage en una instancia de Experience Platform y varias zonas protegidas.

#### Marketo como destino para Experience Platform:

* Se admite Experience Platform en varias instancias de Marketo Engage
* Se admiten varias instancias de Experience Platform en una instancia de Marketo Engage

#### Guardas de perfil y segmentación de Experience Platform:

* Consulte las guardas de perfil y segmentación en Experience Platform: [Guardas de perfil y segmentación](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=es)
* Los segmentos B2B que incluyen cuentas, posibles clientes y oportunidades utilizan relaciones de varias entidades que hace que la evaluación de segmentos se convierta en lote. La segmentación por flujo es compatible con segmentos que están limitados a personas y eventos.
* Incluya un segmento b2b por lotes como entrada para un segmento de streaming o Edge para admitir casos de uso de segmentos b2b de streaming. El abono de los segmentos por lotes se basa en el último resultado diario de evaluación de la segmentación por lotes.

#### Experience Platform - Conector de origen de Marketo Engage:

* El relleno histórico puede tardar hasta 7 días en completarse según el volumen de datos.
* Las actualizaciones y cambios de datos en curso de Marketo se envían a Experience Platform mediante una API de streaming que puede estar latente hasta unos 10 minutos en el perfil y puede tardar hasta 60 minutos en el lago de datos en función del volumen.

#### Experience Platform - Conector de destino de Marketo:

* El uso compartido de segmentos de streaming desde Real-time Customer Data Platform a Marketo Engage puede tardar hasta 15 minutos después de la evaluación del segmento. Los perfiles de relleno que ya existían en el segmento antes de la activación por primera vez pueden tardar hasta 24 horas.
* La segmentación por lotes se comparte una vez al día en función de la programación de segmentación de Experience Platform. Los segmentos B2B que utilizan relaciones de varias entidades, por ejemplo, los segmentos que utilizan datos en los objetos de cuenta y oportunidad, siempre se ejecutan en modo por lotes.

#### Guardas de Marketo Engage:

* Los contactos y posibles clientes deben ingerirse y definirse directamente en Marketo Engage para que la audiencia de Real-Time Customer Data Platform coincida con un posible cliente y un contacto de Marketo Engage.
* El destino de RTCDP Marketo puede, opcionalmente, crear nuevos posibles clientes en Marketo para los clientes que están en un segmento pero que no existen en Marketo.

#### Guardas de destino

* Consulte la documentación de destino para obtener instrucciones específicas sobre los destinos. [Guardas de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=es)


## Pasos de implementación

Para obtener información sobre cómo implementar y configurar la edición B2B de Real-Time Customer Data Platform, consulte la edición B2B de la documentación de Real-Time Customer Data Platform. [Edición B2B de Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=es)

Existen dos patrones de implementación posibles. Tanto la capacidad de ingerir datos y perfiles B2B de Marketo Engage como la capacidad de ingerir datos B2B de otras fuentes de datos de CRM.

## Consideraciones sobre la implementación

Directrices sobre consideraciones y configuraciones clave del modelo.

* Integración de CRM con y sin Marketo:
Si la implementación utiliza Marketo Engage como origen y Marketo Engage está conectado a CRM, los datos de CRM fluirán automáticamente a través de la misma conexión, lo que elimina la necesidad de conectar el CRM directamente a Platform a menos que haya objetos de datos de CRM adicionales que no se pasen a través de Marketo. Utilice el conector de origen de Experience Platform si es necesario introducir tablas adicionales. Si la implementación no va a utilizar Marketo Engage como origen, conecte el origen CRM directamente a Platform mediante el conector Experience Platform de origen CRM.
* El conector de destino de Marketo Engage para Platform, que envía las audiencias a Marketo Engage para su activación, comparte miembros de la audiencia en función de direcciones de correo electrónico y ECID coincidentes. Tiene la opción de crear un nuevo posible cliente si el contacto aún no existe. Al crear un nuevo posible cliente, se pueden asignar hasta 50 atributos de perfil (atributos que no sean de matriz o asignación) en Real-time Customer Data Platform a los campos Persona en Marketo.

## Documentación relacionada

* [Edición B2B de Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=es)
* [Introducción a Real-time Customer Data Platform B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial)
* [Protecciones para Real-time Customer Data Platform B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)
* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es)
* [Marketo Engage](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=es)
* [Adobe Experience Platform: Conector de origen de Marketo](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=es)
* [Adobe Experience Platform: Conector de destino de Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=es)
