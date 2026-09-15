---
title: Configuración
description: Complete los pasos de implementación de zona protegida y configuración de Postman necesarios antes de iniciar AJO Foundations Labs.
doc-type: article

solution: Experience Platform
exl-id: 7c1a9e3d-5b8f-4a2e-9c6d-3f7b0e4a8c2d
source-git-commit: 8b3391d41cd4a3ea6cb52d5167e627b7f6bd2c6e
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%
---

# Configuración

Antes de iniciar los laboratorios de AJO Foundations, complete los pasos de configuración a continuación. Los pasos que necesita dependen de cómo esté tomando este bootcamp.

## Configuración de zona protegida

>[!NOTE]
>
>Si está en un curso o evento de formación en directo, su zona protegida ya se ha implementado para usted; omita esta sección y vaya directamente a la configuración de Postman, a continuación.

Si todavía no tiene una zona protegida en funcionamiento con los recursos de laboratorio implementados, complete los siguientes pasos:

- [Configuración de Developer Console](sandbox-setup/developer-console-setup.md)
- [Instrucciones de implementación](sandbox-setup/deployment-instructions.md)

## Configuración de Postman

Se requiere Postman para los laboratorios de este curso, independientemente de cómo se haya aprovisionado la zona protegida. Complete lo siguiente antes de continuar:

- [Instalación de Postman](postman-setup/postman-installation.md)
- [Importar archivo de entorno](postman-setup/import-environment-file.md)
- [Importar colección de API](postman-setup/import-api-collection.md)

## Preparación bajo demanda

Antes de iniciar los laboratorios, complete la configuración de Postman anterior. Los alumnos con ritmo personalizado también necesitan un subdominio delegado para los laboratorios que dependen del correo electrónico y las credenciales de SMS para el laboratorio de inicio telefónico de Flagship.

## Requisitos previos de canal

Dos laboratorios más adelante en este bootcamp dependen de cuentas externas que solo los alumnos con ritmo personalizado necesitan organizar — si estás en un curso o evento de entrenamiento en vivo, estas ya están aprovisionadas para ti.

### Subdominio delegado

El laboratorio de [Configuración de canales de correo electrónico](data-stores/configure-email-channels/overview.md), y todo lo que depende de él ([Envío de mensajes en acción](orchestrated-campaigns/message-delivery-in-action/overview.md), [emoción posterior a la compra](journeys/post-purchase-excitement/overview.md) y [Marcas de AJO](content-authoring-with-ai/overview.md)), requiere un subdominio delegado a Adobe para enviar correo electrónico. Si todavía no tiene un dominio, regístrelo en cualquier registrador de dominios (por ejemplo, Namecheap). A continuación, para delegar un subdominio del mismo (por ejemplo, `email.yourdomain.com`) a Adobe, siga las [instrucciones de delegación de subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/delegate-subdomains/delegate-subdomain) de Adobe.

>[!NOTE]
>
>La delegación de subdominios puede tardar un tiempo en propagarse. Inicie esta delegación mucho antes de que tenga previsto llegar al laboratorio Configurar canales de correo electrónico.

### Credenciales de SMS

El laboratorio [Flagship phone launch](orchestrated-campaigns/flagship-phone-launch/overview.md) configura un canal SMS a través de Twilio. No se envían mensajes, pero necesita credenciales de trabajo para completar la configuración. La opción más sencilla es una [cuenta de prueba Twilio](https://www.twilio.com/try-twilio) gratuita. Consulta la [guía de introducción](https://www.twilio.com/docs/usage/tutorials/how-to-use-your-free-trial-account) de Twilio para ver cómo registrarte y encontrar el SID de cuenta y el token de autenticación.
