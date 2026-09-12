---
title: Instrucciones de implementación
description: Utilice la CLI de DEP para implementar los esquemas, conjuntos de datos, flujos de datos y datos de muestra del paquete de laboratorio de AJO Architectural Foundations en su zona protegida.
doc-type: article
solution: Experience Platform
exl-id: 3d6e9a1c-7b2f-4e8a-9d0c-1f5a8b6c2e3d
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 1%

---


# Instrucciones de implementación

>[!WARNING]
>
>Esto solo es necesario si está trabajando en los laboratorios a su propio ritmo. Si está en un curso o evento de formación en directo, su zona protegida ya se ha implementado para usted.

El paquete de laboratorio de AJO Architectural Foundations se implementa en su zona protegida mediante la CLI de DEP, una herramienta de línea de comandos que crea los esquemas, conjuntos de datos, flujos de datos y datos de muestra que utilizará en todos los laboratorios, abarcando tanto el almacén de perfiles como el almacén relacional de AJO utilizado para las campañas orquestadas.

## Qué se implementa

**Seguimiento de perfiles**

- Áreas de nombres de identidad (customerID, planID, productID)
- Grupos de campos XDM estándar, descriptores y esquemas habilitados para el perfil
- Conjuntos de datos de catálogo habilitados para perfil
- Políticas de combinación y audiencias
- Datos de perfil para tres conjuntos de datos de muestra: Depeche Mode (características + eventos), Stranger Things (características) y Decisioning (características)

**Pista relacional**

- El área de nombres de identidad customerID
- 11 esquemas XDM relacionales con descriptores de clave principal, clave externa y versión
- 11 conjuntos de datos habilitados para campañas orquestadas de AJO
- 11 flujos de datos cargando datos desde la zona de aterrizaje de datos

>[!NOTE]
>
>La implementación de extremo a extremo tarda unas 2 horas y 23 minutos. El perfil y las pistas relacionales se ejecutan en paralelo, y la mayoría de las veces es tiempo de espera desatendido que la CLI aplica automáticamente.

## Prerrequisitos

- **Derechos de licencia.** Privilegios administrativos para una organización de IMS con Real-Time CDP (con segmentación de streaming) y Adobe Journey Optimizer (con campañas organizadas)
- **Derechos de acceso.** Una función de Experience Platform con todos los permisos en la zona protegida de Target, incluida la credencial de API que creó desde la [configuración de Developer Console](developer-console-setup.md).
- **Credenciales de Developer Console.** Proyecto que incluye API de Adobe Experience Platform y API de Adobe Journey Optimizer. Si aún no lo tiene, siga primero la [configuración de Developer Console](developer-console-setup.md)
- **Zona protegida.** Vacío, de tipo `dev` y en estado &quot;Listo&quot; durante al menos 120 minutos antes de iniciar la implementación
- **Nodo.js.** Cualquier versión reciente de LTS, en Windows o Mac

## &#x200B;1. Instale la CLI

1. Clonar o descargar el [repositorio dep-cli](https://github.com/adobe/dep-cli)
1. Desde el directorio `dep-cli`, ejecute `npm install`
1. Iniciar la CLI con `npm start`

>[!NOTE]
>
>Se requiere Node.js antes de ejecutar los comandos anteriores. Si todavía no tiene instalado Node.js, vea primero la página de configuración [Node.js](https://github.com/adobe/dep-cli/wiki/Nodejs-Setup)de la wiki. Para obtener información detallada sobre la instalación, incluidas capturas de pantalla y cómo actualizar una instalación existente, consulta la página wiki [Instalación](https://github.com/adobe/dep-cli/wiki/Installation)

## &#x200B;2. Configurar el archivo de entorno

La CLI se implementa en cualquier zona protegida a la que apunte el archivo de entorno, por lo que esto debe configurarse correctamente antes de ejecutar cualquier cosa.

1. Copie `envFiles/sample-env.json` y asígnele un nombre nuevo, p. ej. `my-env.json`
2. Abra el archivo y rellene los campos siguientes con los valores de [Developer Console setup](developer-console-setup.md):

   | **Campo** | **Valor** |
   | ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
   | `API_KEY` | ID de cliente |
   | `CLIENT_SECRET` | Secreto del cliente |
   | `IMS_ORG` | ID de organización |
   | `SCOPES` | Debe incluir ámbitos de API de Experience Platform y API de Adobe Journey Optimizer <br />*(por ejemplo: cjm.suppression\_service.client.delete, cjm.suppression\_service.client.all, openid, session, AdobeID, read\_groups, additional\_info.projectProductContext)* |
   | `SANDBOX_NAME` | La zona protegida a la que está dirigiendo debe estar vacía y ser del tipo `dev` |

3. Guarde y cierre el archivo

>[!NOTE]
>
>Se le pedirá el nombre de este archivo cada vez que ejecute un comando CLI, para que pueda reutilizarlo en todos los pasos siguientes.

## &#x200B;3. Ejecute el menú Fundamentos arquitectónicos de AJO

En el menú principal, seleccione **Fundamentos de arco de AJO**. Hay seis pasos divididos en dos vías.

### Seguimiento de perfil (ejecutar en orden)

>[!WARNING]
>
>La zona protegida debe haber estado en estado &quot;Listo&quot; durante al menos 60 minutos antes de ejecutar el paso 1.

| **Paso** | **Qué hace** | **Antes de ejecutarlo** |
| ------------------------ | ------------------------------------------------------------------------------------------- | ---------------------------------- |
| &#x200B;1. Crear base de perfil | Implementa áreas de nombres de identidad, esquemas, conjuntos de datos, políticas de combinación y audiencias | Espacio aislado &quot;listo&quot; durante más de 60 minutos |
| &#x200B;2. Carga de datos de perfil | Crea flujos de datos y flujos de datos de perfil de Depeche Mode, Stranger Things y Decisioning | Espere más de 60 minutos después del paso 1 |
| &#x200B;3. Comprobar estado del perfil | Valida que todos los datos de perfil se hayan cargado correctamente | Espere más de 15 minutos después del paso 2 |

El paso 1 dura unos 2 minutos, el paso 2 unos 6 minutos.

>[!NOTE]
>
>El paso 2 se puede volver a ejecutar con seguridad si algo falla: sobrescribe los rasgos existentes y omite los eventos duplicados.

### Seguimiento relacional

>[!WARNING]
>
>La zona protegida debe haber estado en estado &quot;Listo&quot; durante al menos 120 minutos antes de ejecutar el paso 4 o el paso 6.

| **Paso** | **Qué hace** | **Antes de ejecutarlo** |
| ----------------------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------- |
| &#x200B;4. Crear base relacional | Crea el área de nombres customerID y esquemas/descriptores/conjuntos de datos relacionales | Espacio aislado &quot;listo&quot; durante más de 120 minutos |
| &#x200B;5. Carga de datos relacionales | Carga 11 archivos CSV y crea los flujos de datos que los cargan | Se ejecuta justo después del paso 4: no se necesita una espera manual |
| &#x200B;6. Implementación de bases y datos relacionales | Combina los pasos 4 y 5 en una sola ejecución de ~5 minutos | Espacio aislado &quot;listo&quot; durante más de 120 minutos |

>[!NOTE]
>
>Utilice el paso 6 en lugar de ejecutar los pasos 4 y 5 por separado; hace lo mismo en una pasada con la espera de propagación gestionada por usted.

>[!NOTE]
>
>La CLI comprueba automáticamente todos los tiempos de espera anteriores. Si ejecuta un paso demasiado pronto, se bloquea y le indica cuánto tiempo debe esperar.

## Resolución de problemas

>[!WARNING]
>
>**La comprobación de estado del perfil falla y faltan eventos.** Algunos datos de perfil aún no se han terminado de propagar. Espere otros 15 minutos y vuelva a ejecutar Comprobar el estado del perfil. Si sigue fallando, vuelva a ejecutar Cargar datos de perfil, espere 15 minutos y vuelva a comprobarlo.

>[!WARNING]
>
>**La carga de datos relacionales produce un error parcial.** Cada llamada de API se reintenta hasta 3 veces. Si sigue fallando, la limpieza elimina las conexiones de origen, las conexiones de destino y los flujos de datos que ha creado para que pueda volver a ejecutar el paso 5 (o el paso 6) sin problemas. Los conjuntos de asignaciones no se pueden eliminar a través de la API y pueden quedarse atrás, esto no afecta a la reimplementación.

**Algo más se ve mal.** Como último recurso, puede restablecer la zona protegida desde el menú de administración de la zona protegida de CLI y volver a implementar desde el paso 1.

>[!CAUTION]
>
>El restablecimiento de una zona protegida es destructivo. La CLI le pide que escriba el nombre de la zona protegida para confirmarlo antes de continuar.
