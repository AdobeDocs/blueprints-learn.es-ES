---
hold: true
title: Instrucciones de implementación
description: Utilice la CLI de DEP para implementar los esquemas, conjuntos de datos, flujos de datos y datos de perfil de muestra del paquete de laboratorio de AEP Foundations en su zona protegida.
doc-type: article
solution: Experience Platform
exl-id: 9f2b6d4a-8e1c-4b7a-a3d5-6c9f0e2a4b8d
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 1%

---


# Instrucciones de implementación

> [!NOTE]
>
>Esto solo es necesario si está trabajando en los laboratorios a su propio ritmo. Si está en un curso o evento de formación en directo, su zona protegida ya se ha implementado para usted.

El paquete de laboratorio de AEP Foundations se implementa en el entorno limitado mediante la CLI de DEP, una herramienta de línea de comandos que crea los esquemas, conjuntos de datos, flujos de datos y datos de muestra que se utilizarán en todos los laboratorios.

## Qué se implementa

- 4 áreas de nombres de identidad
- 1 clase de esquema, 13 grupos de campos, 10 esquemas
- 12 descriptores de identidad, 6 descriptores de relación/referencia, 3 descriptores de nombres descriptivos
- 10 conjuntos de datos de catálogo
- 1 conexión de origen HTTP API y 10 flujos de datos
- Datos de perfil: un solo perfil de modo Depeche (3 conjuntos de datos de rasgos, 7 conjuntos de datos de evento) más 3 conjuntos de datos de búsqueda
- 2 políticas de combinación de perfiles y 1 audiencia (cualquier flujo de eventos, dentro de la hora)

>[!NOTE]
>
>La implementación de extremo a extremo tarda aproximadamente 2 horas y 24 minutos, la mayoría de los cuales son tiempos de espera desatendidos entre pasos. La CLI impone estas esperas automáticamente, por lo que no necesita programar nada usted mismo.

## Prerrequisitos

- **Derechos de licencia.** Privilegios administrativos para una organización de IMS con Real-Time CDP (con segmentación por streaming)
- **Derechos de acceso.** Una función de Adobe Experience Platform con todos los permisos en la zona protegida de Target, incluida la credencial de API que creó a partir de la [configuración de Developer Console](developer-console-setup.md).
- **Credenciales de Developer Console.** Proyecto que incluye las API de Adobe Experience Platform. Si aún no lo tiene, siga primero [Configuración de Developer Console](developer-console-setup.md)
- **Zona protegida.** Vacío, de tipo `dev` y en estado &quot;Listo&quot; durante al menos 60 minutos antes de iniciar la implementación
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
2. Abra el archivo y rellene los campos siguientes con los valores de [Configuración de Developer Console](developer-console-setup.md):

| **Campo** | **Valor** |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `API_KEY` | ID de cliente |
| `CLIENT_SECRET` | Secreto del cliente |
| `IMS_ORG` | ID de organización |
| `SCOPES` | Debe incluir ámbitos de API de Experience Platform (openid, session, AdobeID, read_groups, additional_info.projectProductContext) |
| `SANDBOX_NAME` | La zona protegida a la que está dirigiendo debe estar vacía y ser del tipo `dev` |

3. Guarde y cierre el archivo

>[!NOTE]
>
>Se le pedirá el nombre de este archivo cada vez que ejecute un comando CLI, para que pueda reutilizarlo en todos los pasos siguientes.

## &#x200B;3. Ejecutar el menú Fundamentos de AEP

En el menú principal, seleccione **AEP foundation**. Hay tres pasos, y tienen que correr en orden.

>[!WARNING]
>
>La zona protegida debe haber estado en estado &quot;Listo&quot; durante al menos 60 minutos antes de ejecutar el paso 1.

| **Paso** | **Qué hace** | **Antes de ejecutarlo** |
| ----------------------- | ------------------------------------------------------------------------------------------ | ------------------------------- |
| &#x200B;1. Crear base de perfil | Implementa áreas de nombres de identidad, esquemas, conjuntos de datos, políticas de combinación y audiencias | Espacio aislado &quot;listo&quot; durante más de 60 minutos |
| &#x200B;2. Carga de datos de perfil | Crea flujos de datos y flujos de datos de perfil y búsqueda | Espere más de 60 minutos después del paso 1 |
| &#x200B;3. Comprobar estado del perfil | Valida que todos los datos se hayan cargado correctamente | Espere más de 15 minutos después del paso 2 |

El paso 1 tarda unos 2 minutos en ejecutarse, el paso 2, unos 6 minutos, y el paso 3 es una validación rápida sin esperar por sí solo. Los intervalos de 60 y 15 minutos entre pasos son para que AEP termine de propagar los datos entre bastidores; esa es la mayor parte de su cronología de 2 horas.

> [!NOTE]
>
>La CLI comprueba automáticamente estos tiempos de espera. Si ejecuta un paso demasiado pronto, se bloquea y le informa de cuántos minutos quedan; no necesita rastrear el reloj usted mismo.

>[!NOTE]
>
>El paso 2 se puede volver a ejecutar con seguridad si algo sale mal. Sobrescribe los registros de rasgos existentes y omite los eventos duplicados.

## Resolución de problemas

>[!WARNING]
>
>**La comprobación de estado falla y faltan eventos**. Algunos datos de perfil aún no se han terminado de propagar. Espere otros 15 minutos y vuelva a ejecutar Comprobar el estado del perfil. Si sigue fallando, vuelva a ejecutar Cargar datos de perfil, espere 15 minutos y vuelva a comprobarlo.

**Algo más se ve mal.** Como último recurso, puede restablecer la zona protegida desde el menú de administración de la zona protegida de CLI y volver a implementar desde el paso 1.

>[!CAUTION]
>
>El restablecimiento de una zona protegida es destructivo. La CLI le pide que escriba el nombre de la zona protegida para confirmarlo antes de continuar.
