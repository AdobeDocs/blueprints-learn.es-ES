---
hold: true
title: Obtener grupos de campos estándar
description: Consulte la API del Registro de esquemas globales para buscar y guardar los $ids de grupos de campos XDM estándar necesarios para crear un esquema de perfil de cliente.
doc-type: article
solution: Experience Platform
exl-id: 62017ece-eef2-4785-afed-5c690c00ed02
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Obtener grupos de campos estándar

>[!NOTE]
>
>Anteriormente, se hacía referencia a **&quot;Grupo de campos&quot;** como **&quot;Mixin&quot;**, por lo que estos términos se pueden usar indistintamente en todas las solicitudes y guías de API.



## Solicitar grupos de campos estándar XDM

1. Haga clic en la llamada de API `Step 1 - Get XDM Standard Field Groups` en la carpeta `XDM Schema Lab -> Create Schema`
1. Ejecute la llamada haciendo clic en el botón `Send`



**Solicitud**

![Paso 1 - Obtener solicitud de API de grupos de campos estándar de XDM](assets/get-standard-field-groups-step-1-request.jpeg "Paso 1 - Solicitud")

>[!NOTE]
>
>Tenga en cuenta el uso del valor `global` en la siguiente dirección URL de solicitudes:
>
>https\://platform.adobe.io/data/foundation/schemaregistry/**global**/mixins
>
>`global` se usa para solicitar solo componentes estándar de XDM (grupo de campos/mezcla en este caso). Existen dos tipos de propietarios en el registro XDM de Experience Platform: Adobe e Inquilino (es decir, personalizado).
>
>- Los objetos creados por Adobe siempre utilizan la palabra `global` en cualquier solicitud de búsqueda o lista XDM
>- Los objetos creados por el inquilino (es decir, personalizados) siempre utilizan la palabra `tenant` en cualquier lista XDM o llamada de búsqueda



**Respuesta**

![Respuesta de API que enumera grupos de campos estándar XDM](assets/get-standard-field-groups-step-1-response.png "Respuesta del paso 1")


## Identificación de grupos de campos estándar XDM necesarios

Un esquema siempre está compuesto por uno o más grupos de campos y una clase.  Para el esquema Perfil individual de Connection 5G, busque los grupos de campos XDM estándar necesarios para el esquema.

- Datos demográficos
- Datos personales de contacto
- Detalles de consentimiento y preferencia



1. Busque el grupo de campos `Demographic Details` en la respuesta de la llamada
1. Copie el `$id` del grupo de campos y guárdelo en algún lugar para referencia futura
1. Repita los pasos 1 y 2 para los otros dos grupos de campos enumerados arriba

![Grupo de campos Detalles demográficos ubicado en la respuesta de API](assets/get-standard-field-groups-demographic-details-field-group.png)

>[!WARNING]
>
>No continúe hasta que haya guardado los tres (3) `$ids` en algún lugar.  Se necesitarán más adelante para crear el esquema de cuenta de cliente
