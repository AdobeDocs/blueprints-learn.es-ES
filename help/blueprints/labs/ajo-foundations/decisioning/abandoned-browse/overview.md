---
hold: true
title: Exploración abandonada
description: Aprenda a crear un flujo de trabajo de toma de decisiones de exploración abandonada de extremo a extremo que ofrezca ofertas telefónicas personalizadas según los requisitos en todos los canales.
doc-type: overview-page
solution: Experience Platform
exl-id: 37b8a0b3-2820-4303-81d2-19890a3c5782
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# Exploración abandonada

## Prerrequisitos

>[!WARNING]
>
>Los siguientes laboratorios deben haber sido completados antes de comenzar este laboratorio

- **Almacenes de datos — Perfil en acción** **—>** [Crear secuencia de datos](../../data-stores/profile-in-action/create-datastream.md)

Si no ha completado estos laboratorios, hágalo ahora antes de continuar.

## Resumen de laboratorio

En este vídeo aprenderá cómo la descripción del caso de uso de la exploración abandonada revela sus elementos de decisión y lo que construirá en este laboratorio para ofrecer una oferta telefónica personalizada, según los requisitos en tiempo real.

>[!VIDEO](https://video.tv.adobe.com/v/3491316/)

## Objetivos empresariales

El caso de uso comercial para este laboratorio es que Connection 5G quiere aumentar las ventas del nuevo teléfono insignia de Apple, el iPhone 17, dirigiéndose a los clientes que han navegado por la página de información general de iPhone 17 pero no han comprado. Los objetivos principales de la campaña son los siguientes:

- **Identifique a los clientes con intenciones altas** al detectar cuándo un usuario ve una página de teléfono insignia varias veces sin completar una compra.
- **Déclencheur una experiencia personalizada en tiempo real** en todas las superficies digitales de propiedad de Connection 5G cuando se produce este comportamiento.
- **Entregar ofertas contextuales** basadas en atributos clave del cliente, como la edad de **el titular de la cuenta** y su **plan móvil actual**.
- **Asegúrese de que se cumpla la elegibilidad para la oferta** para que los clientes solo vean ofertas telefónicas compatibles con su plan.
- **Ajuste dinámico del nivel de teléfono ofrecido** (por ejemplo, base, pro, ultra) según el compromiso del cliente o la respuesta a ofertas anteriores.
- **Proporcione una personalización coherente en todos los canales** mediante la lógica de toma de decisiones centralizada para determinar la mejor oferta en tiempo real.
- **Aumentar la probabilidad de conversión** al presentar la oferta de teléfono principal más relevante a cada cliente en el momento adecuado.

## Objetivos de aprendizaje del laboratorio

Para cumplir con los objetivos comerciales anteriores en este laboratorio, aprenderá a:

- **Amplíe el modelo de datos de oferta** agregando atributos personalizados al esquema de oferta para que se puedan usar en la lógica de toma de decisiones.
- **Cree reglas de elegibilidad** que determinen qué perfiles cumplen los requisitos para ofertas específicas según los atributos del perfil.
- **Genere y configure elementos de oferta**, lo que incluye establecer prioridades, definir condiciones de elegibilidad y aplicar límites de frecuencia.
- **Organice las ofertas en una colección** para que se pueda hacer referencia a ellas y evaluarlas fácilmente durante la actividad de toma de decisiones.
- **Cree una fórmula de clasificación** que ajuste dinámicamente la prioridad de ofertas según las características del perfil.
- **Configure una estrategia de selección** que combine colecciones de ofertas, reglas de elegibilidad y lógica de clasificación para determinar qué ofertas se tienen en cuenta y cómo se ordenan.
- **Configure un canal de experiencia basada en código (CBE)** para permitir que sistemas externos soliciten resultados de decisiones y reciban ofertas en formato JSON.
- **Pruebe el flujo de trabajo de toma de decisiones de extremo a extremo** enviando eventos de experiencia y solicitudes de decisión para validar la lógica de elegibilidad, el comportamiento de clasificación y el límite de frecuencia.

Al completar este laboratorio, obtendrá experiencia práctica en el diseño y validación de un flujo de trabajo de **offer decisioning completo en Adobe Journey Optimizer** para cumplir con el caso práctico comercial.
