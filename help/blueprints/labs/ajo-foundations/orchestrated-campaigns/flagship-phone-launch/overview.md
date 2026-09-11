---
title: Lanzamiento de teléfono insignia
description: Obtenga información general sobre la creación de una campaña orquestada dirigida a titulares de cuentas y líneas individuales con una oferta de actualización de SMS después del lanzamiento de un teléfono insignia.
doc-type: overview-page
solution: Experience Platform
exl-id: 04c509f1-aa10-4d29-aa59-5e627b79e498
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Lanzamiento de teléfono insignia

## Prerrequisitos

>[!WARNING]
>
>Los siguientes laboratorios deben haber sido completados antes de comenzar este laboratorio

- **Almacenes de datos — Almacén relacional en acción** **—>** [Dimension de destino de perfil](../../data-stores/relational-store-in-action/profile-target-dimension.md)
- **Almacenes de datos — Configurar canales de correo electrónico —>** [Configurar para relacionales](../../data-stores/configure-email-channels/configure-for-relational.md)
  *(este paso de configuración tarda hasta tres horas en completarse)*

Si no ha completado estos laboratorios, hágalo ahora antes de continuar.

## Resumen de laboratorio

En este vídeo, aprenderá cómo el caso de uso del lanzamiento del teléfono insignia se asigna a las campañas orquestadas, recapitulando las preguntas de pensamiento crítico y la arquitectura antes de crear los titulares de cuentas de direccionamiento de campaña y las líneas individuales.

>[!VIDEO](https://video.tv.adobe.com/v/3486217/)

## Objetivos de aprendizaje

- Creación de una campaña organizada mediante diversas actividades de flujo de trabajo
- Crear una audiencia con una actividad de Crear audiencia
- Obtenga información sobre cómo configurar un canal SMS
- Guardar una audiencia en el portal de audiencias
- Dirija la cuenta del cliente y las líneas individuales con mensajes de correo electrónico y SMS



## Descripción del caso de uso

Inmediatamente después del lanzamiento del último dispositivo insignia de un fabricante, envíe un mensaje dirigido a los titulares de cuentas y a los usuarios de la línea con modelos más antiguos, invitándolos a actualizar y experimentar el futuro de la tecnología móvil.

**Llamadas clave:**

- Guarde la audiencia de todas las líneas del cliente en Audience Portal
- Dirigirse a líneas individuales y titulares de cuenta con un mensaje (utilizará SMS)

>[!NOTE]
>
>Este escenario simula una **campaña de actualización de contratos de telecomunicaciones**, en la que las líneas secundarias (dependientes) reciben mensajes de actualización dirigidos.
