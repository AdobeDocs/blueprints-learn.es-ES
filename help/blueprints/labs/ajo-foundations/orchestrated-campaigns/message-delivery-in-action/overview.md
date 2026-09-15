---
title: Envío de mensajes en acción
description: Obtenga información general sobre la creación de una campaña orquestada dirigida a miembros del plan básico y compare el comportamiento de entrega entre los canales de correo electrónico de esquema relacional y perfil de AEP.
doc-type: overview-page
solution: Experience Platform
exl-id: 84b16fff-f733-439a-9a93-726811e543ce
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%
---

# Envío de mensajes en acción

## Requisitos previos

>[!WARNING]
>
>Los siguientes laboratorios deben haber sido completados antes de comenzar este laboratorio

- **Almacenes de datos — Almacén relacional en acción** **—>** [Dimension de destino de perfil](../../data-stores/relational-store-in-action/profile-target-dimension.md)
- **Almacenes de datos —>** [Configurar canales de correo electrónico](../../data-stores/configure-email-channels/overview.md) *(este paso de configuración tarda tres horas en completarse)*

Si no ha completado estos laboratorios, hágalo ahora antes de continuar.

>[!CAUTION]
>
>Este laboratorio requiere un subdominio delegado a Adobe en su zona protegida. Consulta [Configuración](../../setup.md) si tienes ritmo personalizado y aún no lo tienes.

## Resumen de laboratorio

En este vídeo aprenderá a crear la campaña orquestada para este laboratorio, lo que incluye crear y ramificar una audiencia de miembros de un plan básico y comparar los resultados de envío entre los canales de correo electrónico Perfil y Relacional.

>[!VIDEO](https://video.tv.adobe.com/v/3486541/)

## Objetivos de aprendizaje

- Creación de una campaña organizada mediante varias actividades de flujo de trabajo
- Crear una audiencia con la actividad Generar audiencia
- Ramifique la audiencia para crear dos ramas y utilice los canales de correo electrónico, creados en el laboratorio anterior, para enviar mensajes
- Pruebe la campaña y comprenda la diferencia de comportamiento entre los canales de correo electrónico

Para dirigirse a los miembros del plan &quot;Básico&quot;, cree una campaña en este laboratorio y explore cómo las distintas configuraciones de Campaña orquestada afectan a las configuraciones del canal de correo electrónico.
