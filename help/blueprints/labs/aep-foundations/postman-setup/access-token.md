---
hold: true
title: Token de acceso
description: Genere un token de acceso de servidor a servidor OAuth en Postman y comprenda los encabezados necesarios para autenticar las llamadas a la API de AEP.
doc-type: article
solution: Experience Platform
exl-id: e38a1bd4-5a09-40c6-8303-c3770801c864
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# Token de acceso

## Información general de seguridad API



Para establecer una conexión API segura con un producto de Adobe, Adobe proporciona la creación de una credencial de servidor a servidor OAuth. Para ello, primero debe crear un proyecto de desarrollador dentro de Adobe Developer Console. Para tener acceso a Developer Console, se le deben haber asignado derechos de desarrollador en Adobe Admin Console. Una vez que tenga estos derechos, puede crear proyectos de desarrollador utilizando las distintas API relacionadas con productos de Adobe. Aquí es donde entra en juego la credencial de servidor a servidor OAuth. Para generar un token de acceso, debe pasar un determinado conjunto de notificaciones al servicio Identity Management de Adobe (IMS). Para las credenciales de servidor a servidor de OAuth, una llamada de ejemplo tendría este aspecto:

```curl
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3?client_id={CLIENT_ID}' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'client_secret={CLIENT_SECRET}&grant_type=client_credentials&scope={SCOPE}'
```

>[!NOTE]
>
>Puede obtener más información sobre el proceso e2e para crear el proyecto de desarrollador con las credenciales de servidor a servidor de OAuth [aquí](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/#generate-access-tokens). Para el bootcamp vamos a &quot;mover manualmente&quot; este paso del proceso 😄



## Adobe Experience Platform + Adobe IMS

Cada solicitud a cualquier servicio de Adobe debe incluir el token de acceso en el encabezado Autorización junto con el Secreto de cliente que se generó durante la creación del proyecto del desarrollador. Además, Experience Platform y sus aplicaciones asociadas requieren que haya otros dos parámetros de encabezado presentes en cada solicitud.

- `x-gw-ims-org-id`: este parámetro especifica `IMS Org` al que pertenece la solicitud y garantiza que el procesamiento de las solicitudes se resuelva en el entorno de SaaS adecuado
- `x-sandbox-name`: este parámetro especifica en qué zona protegida se procesará la solicitud dentro de Experience Platform

Ahora que comprende un poco sobre cómo Adobe protege sus API y qué se necesita para trabajar con ellas, utilícelas ahora.

>[!CAUTION]
>
>Si no se especifica el parámetro `x-sandbox-name`, la solicitud no se procesará de forma errónea como cabría esperar. En su lugar, establece de forma predeterminada la solicitud para procesarla en la zona protegida `default` que se aprovisiona automáticamente con cualquier entorno de Experience Platform

>[!NOTE]
>
>Como parte de este bootcamp creamos un proyecto de desarrollador y le proporcionamos un archivo de entorno de Postman con todos los valores necesarios para solicitar un `access_token`. Esto es lo que subió en los pasos anteriores del laboratorio

## Autenticar con Postman

1. Inicie Postman, vaya al directorio llamado `IMS Authenticate` y abra la solicitud haciendo clic en ella
1. A continuación, en la esquina superior derecha de Postman, verá una lista desplegable de entorno. Seleccione el entorno `AEP Bootcamp` de la lista desplegable
1. Ahora ejecute la llamada haciendo clic en el botón &quot;Enviar&quot;.

![Solicitud de Postman después de enviar la llamada de autenticación IMS para generar un token de acceso](assets/access-token-execute-ims-authenticate-request.png)

Una respuesta correcta debería tener este aspecto:

```none
200 OK Successful Authentication
```

Respuesta correcta

```json
{
    "token_type": "bearer",
    "access_token": "<value>",
    "expires_in": 86399979
}
```

`token_type` - siempre será de tipo portador

`access_token` - prueba la autorización y es necesario en el encabezado de autorización de todas las llamadas a la API

`expires_in`: milisegundos hasta que caduque el token de acceso (hoy, periodo de caducidad de 24 horas)

>[!TIP]
>
>¡Felicidades! Se ha autenticado correctamente y el access\_token se ha guardado en el archivo de entorno



## Errores comunes

### Token no válido

Esto ocurre cuando el `private_key` del archivo de entorno tiene un formato incorrecto o ya no es válido. Si lo ve, asegúrese de que ha copiado toda la clave, incluidos los saltos de línea

Ejemplo:

```none
-----BEGIN PRIVATE KEY----- 
some uber long varchar set is here
-----END PRIVATE KEY----- 
```

```none
400 invalid_token
```

>[!NOTE]
>
>Solo se aplica cuando se utiliza la autenticación basada en JWT

### IMS\_ORG no válido

Este error se produce cuando se olvida de configurar el entorno de Postman de la lista desplegable

![No se encontró IMS_ORG en el error de entorno activo cuando no se seleccionó ningún entorno de Postman](assets/access-token-forgot-to-select-postman-environment.png)

>[!NOTE]
>
>No olvide configurar su entorno de postman al ejecutar llamadas a la API
>
>![Selección del entorno de Bootcamp de AEP de la lista desplegable de entornos de Postman](assets/access-token-set-postman-environment.png)
