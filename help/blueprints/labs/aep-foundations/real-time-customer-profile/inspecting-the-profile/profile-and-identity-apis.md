---
title: API de perfil e identidad
description: Utilice la API de entidad de perfil y la API de clúster de servicio de identidad en Postman para buscar atributos de perfil, eventos e identidades vinculadas.
doc-type: article
solution: Experience Platform
exl-id: 1db55c5b-fdf8-4c63-b435-477626bb0450
source-git-commit: 8b3391d41cd4a3ea6cb52d5167e627b7f6bd2c6e
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 1%
---

# API de perfil e identidad

>[!IMPORTANT]
>
>Complete [Configuración de Postman](../../setup.md) antes de iniciar los ejercicios de API de perfil e identidad.

## API de entidad de perfil

Saber cómo utilizar las API de perfil es fundamental a la hora de trabajar con el perfil del cliente en tiempo real. Desbloquea la capacidad de triaje y depuración rápidos, al tiempo que le expone a muchas posibles integraciones del sistema, desde centros de llamadas hasta quioscos.

Una de las API más importantes es la API de entidad de perfil. Esta API le permite buscar un perfil individual, como ha visto en la interfaz de usuario. Utiliza parámetros para dictar si desea ver los atributos o eventos del perfil.

A continuación se muestra toda la especificación del método GET para la API de entidad de perfil


## Resumen de API

A continuación se proporciona la información mínima necesaria para llamar a la API de entidad de perfil.

`GET https://platform.adobe.io/data/core/ups/access/entities`

### Parámetro de consulta requerido

Envíe este parámetro con cada solicitud. Su valor depende de si está buscando los atributos de un perfil o sus eventos:

| Parámetro | Tipo | Descripción | Ejemplo |
| ------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| `schema.name` | cadena | Nombre de clase de esquema XDM de la entidad que está buscando. | `_xdm.context.profile` |
| `schema.name` | cadena | Utilice este valor en su lugar para buscar los eventos de un perfil. Emparejarlo con `relatedSchema.name=_xdm.context.profile` para asignar el ámbito de los eventos a un perfil. | `_xdm.context.experienceevent` |

### Identificación de la entidad que se va a buscar

La mayoría de las solicitudes utilizan `entityId` y `entityIdNS` para identificar la entidad por cualquier valor de identidad conocido, como una dirección de correo electrónico, un ID de CRM o un ID de fidelidad, en lugar de requerir que ya sepa su XID. Un XID es un identificador codificado en Base64 que el servicio de identidad genera y asigna internamente para representar una identidad, consolidando su área de nombres y valor de ID en un solo token compacto (consulte [XID nativo](https://experienceleague.adobe.com/docs/experience-platform/identity/api/list-native-id.html?lang=es) para obtener detalles):

| Parámetro | Tipo | Descripción | Ejemplo |
| ------------ | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `entityId` | cadena | El valor del identificador que se va a buscar. Si ya conoce el XID de la entidad, utilícelo aquí solo y omita `entityIdNS`. | `depeche.mode@dep.com` |
| `entityIdNS` | cadena | Código del área de nombres de identidad al que pertenece `entityId` (por ejemplo, `email`, `crmid`, `ECID`). Se requiere siempre que `entityId` no sea un XID. | `email` |

>[!NOTE]
>
>Las solicitudes Postman de este laboratorio buscan el perfil Depeche Mode por su dirección de correo electrónico (`entityIdNS=email`, `entityId=depeche.mode@dep.com`) en lugar de su XID.

### Encabezados obligatorios

Cada solicitud también necesita estos encabezados:

| Header | Tipo | Descripción | Ejemplo |
| ----------------- | ------ | ---------------------------------------------- | --------------------- |
| `x-gw-ims-org-id` | cadena | ID de la organización IMS. | `<your IMS org>` |
| `x-api-key` | cadena | Clave de API del proyecto o credencial registrado. | `<your API key>` |
| `Authorization` | cadena | Token de portador para la solicitud. | `Bearer <your token>` |

>[!NOTE]
>
>Consulte la [Referencia de API de entidades de perfil](https://developer.adobe.com/experience-platform-apis/references/profile#tag/Entities) para obtener una lista completa de los parámetros de consulta, incluidas las opciones de búsqueda de identidad adicionales, el filtrado de eventos (`startTime`, `endTime`, `property`, `orderby`, `limit`), la selección de campos y las invalidaciones de las políticas de combinación.

>[!WARNING]
>
>Recuerde que todas las solicitudes de API son específicas de la zona protegida, por lo que es importante que, al trabajar con las API, se asegure de que el parámetro de encabezado de cada solicitud denominada `x-sandbox-name` se establezca correctamente en la zona protegida adecuada.
>
>Para este laboratorio ya tiene el `x-sandbox-name` establecido en el archivo de entorno

## Búsqueda de entidades (atributos)

Para obtener una idea de la API de búsqueda de entidad, utilice el perfil Depeche Mode del laboratorio anterior.

1. Abra **Postman** y vaya a la carpeta **Profile Lab**
1. Haga clic en la solicitud **Consulta de entidad (atributos)** para abrirla
1. Ejecute la llamada haciendo clic en el botón **Enviar**

   ![Panel de solicitud de Postman para la llamada de búsqueda de entidad (atributos) antes de enviar](assets/profile-and-identity-apis-entity-lookup-attributes-request.png "API de búsqueda de entidad de perfil (atributos)")

   Una solicitud correcta debe responder con `200 OK` y debería ver un resultado que contenga todos los atributos del perfil Modo profundo.

   ![Respuesta correcta de 200 que contiene todos los atributos para el perfil de modo Depeche](assets/profile-and-identity-apis-successful-attributes-api-response.png "Respuesta correcta de API de entidad de perfil (atributos)")

   >[!NOTE]
   >
   >De forma predeterminada, si no se especifica ninguna política de combinación en una solicitud de entidad de perfil, se utiliza la política de combinación predeterminada en la zona protegida

   Con la API de entidad, utilice los parámetros de consulta para cambiar lo que se devuelve en respuesta.

1. En la solicitud de búsqueda de entidad (atributos), haga clic en la opción **Params** de la solicitud
1. Marque la casilla junto a **Clave** con nombre **campos**
1. Ejecute la solicitud haciendo clic en el botón **Enviar**

![Solicitud de búsqueda de entidad (atributos) con el parámetro de campos habilitado para filtrar la respuesta](assets/profile-and-identity-apis-entity-lookup-attributes-with-filter-enabled.png)

>[!NOTE]
>
>Observe que también hay un parámetro para especificar `mergePolicyId`. Para encontrar el valor de, utilice otras API o busque el ID con la interfaz de usuario.

Una solicitud correcta debe responder con un `200 OK` y solo debe ver los campos especificados en el filtro de parámetro que acaba de habilitar: Nombre, Apellidos y una matriz de productos activos.

![Se ha filtrado una respuesta 200 OK que muestra solo los campos Nombre, Apellido y Productos activos](assets/profile-and-identity-apis-successful-filtered-attributes-response.png "Respuesta de API de búsqueda de entidad de perfil (atributos) correcta con el filtro habilitado")

>[!SUCCESS]
>
>¡Felicidades!  Ha buscado correctamente los atributos de un perfil utilizando la API de entidad de perfil

## Búsqueda de entidades (eventos)

Para buscar los eventos de un perfil, se utiliza exactamente la misma API de entidad de perfil.  La única diferencia es que debe indicar al servicio de perfil que desea cambiar qué tipo de clase utilizar en la respuesta.

1. Haga clic en la solicitud **Entity Lookup (events)** para abrirla
1. Ejecute la llamada haciendo clic en el botón **Enviar**

![Panel de solicitud de Postman para la llamada de búsqueda de entidad (eventos) antes de enviar](assets/profile-and-identity-apis-entity-lookup-events-request.png)

Una solicitud correcta debe responder con un `200 OK` y debería ver un resultado que contenga todos los eventos del perfil Depeche Mode.



![Respuesta correcta de 200 que contiene todos los eventos para el perfil de modo Depeche](assets/profile-and-identity-apis-successful-events-api-response.png "Respuesta correcta de API de búsqueda de entidad de perfil (eventos)")

Cuando busca atributos de perfil, la API de entidad tiene incluso más parámetros de consulta que cambian lo que se devuelve en respuesta.

Pruebe con algunos de ellos activándolos en la sección Parámetros y ejecutando la solicitud. ¡Mira cómo funciona!

![Solicitud de búsqueda de entidad (eventos) con parámetros de consulta adicionales habilitados en la sección Parámetros](assets/profile-and-identity-apis-entity-lookup-events-query-params.png "Búsqueda de entidad de perfil para eventos de experiencia")

**Definiciones de parámetro de consulta de muestra**

| Clave | Valor | Descripción |
| ------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------- |
| mergePolicyId | \&lt;blank> | Cambia la política de combinación utilizada para la búsqueda. Si se deja en blanco se utiliza la política de combinación predeterminada de la zona protegida |
| campos | eventType,timestamp,identityMap | Muestra únicamente estos campos de cada evento, tengan o no un valor |
| propiedad | eventType=&quot;order.placement&quot; | Filtra los eventos solo a los del tipo especificado |
| orderby | +marca de tiempo | Ordena los eventos en orden ascendente |
| límite | 5 | Muestra solo 5 eventos en la respuesta |

>[!NOTE]
>
>Obtenga más información acerca de todas las opciones del parámetro de consulta aquí -> [https://developer.adobe.com/experience-platform-apis/references/profile/#tag/Entities/operation/retrieveEntity](https://developer.adobe.com/experience-platform-apis/references/profile/#tag/Entities/operation/retrieveEntity)



## API de clúster de servicio de identidad

En algún momento, es posible que tenga una pregunta acerca de qué identidades forman parte del clúster de identidad de un perfil específico dentro del gráfico de identidades.  Esta API le permite pasar un único área de nombres o valor de identidad y, como respuesta, recibe el clúster de identidad completo para ese perfil.

Pruébelo usted mismo:

1. Haga clic en la solicitud **Identidades vinculadas de lista** para abrirla
1. Ejecute la llamada haciendo clic en el botón **Enviar**

>[!NOTE]
>
>Tenga en cuenta que los parámetros de la solicitud son el área de nombres de identidad y el ID (es decir, el valor)



![Panel de solicitud de Postman para la llamada de lista de identidades vinculadas antes de enviar](assets/profile-and-identity-apis-list-linked-identities-request.png "API de lista de identidades vinculadas")

Una respuesta correcta debería parecerse a la captura de pantalla siguiente



![Respuesta de identidades vinculadas de lista correcta que muestra todas las identidades del perfil de modo Depeche](assets/profile-and-identity-apis-successful-list-linked-identities-response.png)

>[!NOTE]
>
>Verá que la respuesta contiene todas las identidades del perfil Modo profundo
