---
hold: true
title: Configuración de Developer Console
description: Cree un proyecto de Adobe Developer Console con credenciales de servidor a servidor OAuth para las API de Experience Platform y Journey Optimizer utilizadas por la CLI de DEP.
doc-type: article
solution: Experience Platform
exl-id: 8b8f2a3e-2f4a-4b0e-9c5a-6e0c2b7a1d4f
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Configuración de Developer Console

>[!WARNING]
>
>Esto solo es necesario si está trabajando en los laboratorios a su propio ritmo. Si está en un curso o evento de formación en directo, su zona protegida ya se ha implementado para usted.

La CLI de DEP se autentica en la zona protegida utilizando las credenciales de servidor a servidor de OAuth de un proyecto de Adobe Developer Console. Esta página muestra cómo crear ese proyecto. Solo debe hacerlo una vez; las mismas credenciales funcionan en las pistas de AEP Foundations y AJO Architectural Foundations, siempre y cuando añada ambas API que se describen a continuación.

>[!NOTE]
>
>Si ya tiene un proyecto de Developer Console con credenciales para Adobe Experience Platform (y, si es necesario, Adobe Journey Optimizer), omita esta sección y vaya directamente a [Instrucciones de implementación](deployment-instructions.md).

## Prerrequisitos

- Una Adobe ID con acceso de desarrollador a su organización
- Una zona protegida de Adobe Experience Platform que esté vacía y del tipo `dev`
- Una función de Adobe Experience Platform con todos los permisos concedidos para esa zona protegida (pregunte al administrador del sistema si no está seguro)

## Creación del proyecto

1. Vaya a [Adobe Developer Console](https://developer.adobe.com/console) e inicie sesión
1. Si tiene acceso a más de una organización, utilice el conmutador de organización en la parte superior derecha para seleccionar la correcta
1. Seleccione **Crear nuevo proyecto**
1. Cambie el nombre del proyecto a algo que reconozca más adelante (por ejemplo, `DEP Sandbox`)

## Añadir API de Experience Platform

1. En la descripción general del proyecto, seleccione **Agregar API**
1. Elija el icono de producto **Adobe Experience Platform** y, a continuación, seleccione **API de Adobe Experience Platform**
1. Seleccionar **Siguiente**
1. Elija **Servidor a servidor OAuth** como tipo de autenticación y seleccione **Siguiente**
1. Asigne un nombre a la credencial y seleccione **Siguiente**
1. Seleccione el perfil de producto que coincida con la zona protegida que está utilizando y, a continuación, seleccione **Guardar la API configurada**

## Añadir API de Adobe Journey Optimizer

1. En la descripción general del proyecto, seleccione **Agregar API**
1. Elija el icono de producto **Adobe Journey Optimizer** y seleccione la API correspondiente
1. Seleccionar **servidor a servidor OAuth**
1. Seleccione el mismo perfil de producto y seleccione **Guardar la API configurada**

>[!NOTE]
>
>Reutilice la credencial que creó anteriormente en lugar de crear una nueva: la CLI solo necesita un único conjunto de credenciales, con ámbitos combinados.



## Recopile sus valores

Abra la página de información general de **OAuth Server-to-Server** de sus credenciales. Necesitará cuatro valores para el archivo de entorno de la CLI:

| **Valor de la consola de desarrollo** | **Campo de archivo envolvente** |
| --------------------- | ------------------------------- |
| ID de cliente | `API_KEY` |
| Secreto del cliente | `CLIENT_SECRET` |
| ID de organización | `IMS_ORG` (termina en `@AdobeOrg`) |
| Ámbitos | `SCOPES` |

>[!NOTE]
>
>Copie los ámbitos predeterminados que se muestran en la página de credenciales; no es necesario agregar nada manualmente. Si ha agregado ambas API, la lista de ámbitos incluirá ambas automáticamente.

Mantenga esta página abierta o copie estos cuatro valores en un lugar seguro. Las pegará en el archivo de entorno de la CLI en el siguiente paso de la guía de configuración de la pista.
