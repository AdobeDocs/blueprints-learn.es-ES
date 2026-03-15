---
title: Activación de cuentas B2B en destinos de Advertising y destinos de archivos
description: Utilice la participación basada en cuentas para crear audiencias y segmentarlas mediante destinos.
solution: Real-Time Customer Data Platform
exl-id: 578c0019-6133-4508-ae9d-8a8a463376f0
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 4%

---

# Activación de cuentas B2B en destinos publicitarios y destinos de archivos

La participación basada en cuentas permite a los especialistas en marketing B2B crear audiencias de cuentas (es decir, listas de empresas) y segmentar dichas empresas a través de destinos como LinkedIn que aceptan listas de empresas como entrada o exportación a destinos de almacenamiento en la nube para la segmentación y el alcance de las ventas.

## Casos de uso

Mediante la participación basada en cuentas, los especialistas en marketing pueden desbloquear tres casos de uso clave:

* **Rellenar huecos de grupos de compras:** Un experto en marketing puede anunciarse en cuentas en las que aún no tenga contactos para los roles de CMO o CIO. Primero pueden crear una audiencia de cuentas sin un contacto con el título &quot;CMO&quot; o &quot;CIO&quot; y luego activar la audiencia en LinkedIn. Dentro del destino, LinkedIn, pueden lanzar una campaña dirigida a esa audiencia y a personas específicas con títulos de trabajo de &quot;CMO&quot; o &quot;CIO&quot; para llegar a estos nuevos contactos y destacar las ventajas de sus ofertas.
* **Ampliar ventas o realizar ventas cruzadas a otras divisiones de una compañía que ya sea cliente:** Un experto en marketing puede crear una audiencia de cuenta que compró el producto X entre 3 y 9 meses atrás, pero aún no es propietario del producto Y. Luego pueden activarse, destacando las ventajas del producto Y para ese público objetivo.
* **Compañías de Target que utilizan productos de la competencia:** Un experto en marketing puede comercializar cuentas para desplazar los productos de un competidor, incluso sin ningún contacto en esas cuentas. Pueden crear una audiencia de cuentas basada en datos de socios que muestren la propiedad o el uso del producto de un competidor y, a continuación, activarlas mediante LinkedIn para que los contactos de origen en las cuentas de destino se expandan.

## Aplicaciones

* Real-Time Customer Data Platform edición B2B

## Patrones de integración

* Fuentes de datos B2B (Marketo, Salesforce, etc.) -> Real-time Customer Data Platform B2B edition -> Destinos.
* Se pueden utilizar varias fuentes de datos B2B para asignar datos de cuenta, posible cliente, oportunidad y personas a B2B edition de Real-time Customer Data Platform.

## Arquitectura

![Arquitectura de referencia para modelo Audience Activation de cuenta B2B](assets/b2b-blueprint-account-audience-activation.png)

## Destinos de audiencia de cuenta

* (Compañías) Audiencias coincidentes de LinkedIn
* Destinos de almacenamiento en nube
   * Azure Data Lake
   * Data Landing Zone
   * SFTP
   * Azure Blob
   * AWS S3

## Guardas

* Limitado a 50 segmentos de cuenta por zona protegida.
* Evaluación de segmentación por lotes.
   * Se evalúa automáticamente cada 24 horas después de la finalización de los trabajos de exportación de perfiles y de ejecución de audiencias por lotes.
   * No se admite la evaluación de Edge, Streaming o Ad Hoc.
* Los atributos de cuenta están disponibles para la exportación.
* Eventos de personas.
   * Hasta 30 días de retrospectiva de eventos, sin orden de predicados de eventos.
   * Y / O son compatibles (por lo que puede decir &quot;A y B tienen que suceder,&quot;  pero no se puede decir &quot;A debe suceder 3 días antes de B&quot;).
* Para los destinos de almacenamiento en la nube, la programación de exportación admite la opción &quot;Después de la evaluación de segmentos&quot;.
* [Perfil B2B y protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails).

## Pasos de implementación de Real-time Customer Data Platform B2B edition, creación de audiencias de cuenta y activación

* Para ver los pasos de implementación de Real-time Customer Data Platform B2B edition, consulte la [Introducción a Real-Time Customer Data Platform B2B Edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial).
* Para ver los pasos de creación de audiencias de cuenta, consulte la documentación de [audiencias de cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences).
* Para ver los pasos de Account Audience Activation, consulte la documentación de [Activar audiencias de cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences).
   * Asignación requerida para [(Compañías) LinkedIn Destino de audiencias coincidentes](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences#required-mappings).

## Consideraciones sobre la implementación

Las audiencias coincidentes de LinkedIn tienen algunos requisitos, incluido el tamaño mínimo de audiencia de 300 miembros coincidentes. Si la audiencia de cuenta activada para el destino de audiencia coincidente vinculada de la empresa no cumple los requisitos, la definición de audiencia debe modificarse para aumentar el tamaño de la audiencia a fin de iniciar una campaña de LinkedIn.

## Documentación relacionada

* [B2B edition de Real-time Customer Data Platform](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
* [Tutorial en vídeo de Crear y activar audiencias de cuenta](https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/audiences/create-audiences-with-b2b-data)
* [Crear audiencias de cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences)
* [Activar audiencias de cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences)
* [Adobe Experience Platform - Conector de destino de LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
