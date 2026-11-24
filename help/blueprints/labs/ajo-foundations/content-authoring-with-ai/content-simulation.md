---
title: Simulación de contenido
description: Aprenda a utilizar la herramienta de simulación de Adobe Journey Optimizer con datos de perfil de muestra para validar campos personalizados, variantes de contenido y comportamientos de reserva.
doc-type: article
solution: Experience Platform
exl-id: 3e2b064f-5680-461c-a49e-2a61514e146f
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: c0adb1eab9b0a1315e2041c1f2cb89a4bfdae4b2
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%
---

# Simulación de contenido

**Propósito:** Valide variantes de personalización, lógica condicional y contenido usando las herramientas de Adobe Journey Optimizer Simulation y Proof.

## Objetivos de aprendizaje

Al final de este módulo, deberá ser capaz de:

1. Cargue y utilice datos de perfil de prueba para la simulación.
1. Valide campos personalizados y lógica de variante.
1. Pruebe el comportamiento de reserva para los datos que faltan o no coinciden.

## Introducción

En este módulo, probará el correo electrónico con **dos variantes condicionales** mediante la herramienta de simulación de Adobe Journey Optimizer.
Esto le permite obtener una vista previa de cómo los distintos clientes experimentarán el mensaje personalizado, lo que garantiza la precisión antes de iniciar la campaña.

Utilizará el archivo de perfil de prueba de muestra **sample.csv** de su conjunto de herramientas.

![Ejemplo de archivo de perfil de prueba sample.csv del kit de herramientas](assets/content-simulation-sample-csv-toolkit-file.png)

## Abra la herramienta de simulación

1. Abra el correo electrónico completado.
2. En el correo electrónico, haga clic en **Simular contenido**.

![Haciendo clic en Simular contenido y seleccionando Simular variación de contenido](assets/content-simulation-click-simulate-content-variation.png)

Después de unos segundos, se abre un panel de simulación.

## Carga de los datos del perfil de prueba

1. Haga clic en **Cargar** en la parte inferior para cargar los datos de entrada.

   ![Botón de carga de datos de entrada en el panel de simulación](assets/content-simulation-click-upload-input-data.png)

&#x200B;3. Elija **sample.csv** y haga clic en **Continuar**.

   ![Seleccionando sample.csv y haciendo clic en Abrir](assets/content-simulation-choose-sample-csv-continue.png)

AJO procesa el archivo y, a tiempo, prepara las vistas previas.
![Vistas previas de variación](assets/content-simulation-variation-previews.png)


## Revisar representación de variante

Al hacer clic en Simular contenido en el correo electrónico, AJO muestra variantes en paralelo en función de los perfiles cargados.

**Resultados esperados:**

- **Alex** → Ve **Variante 1** (Edad superior a 40)
Haga clic en el icono de lápiz sobre la primera variante para **Mostrar detalles de la variante**

![Haga clic en el icono de lápiz para ver los detalles de la variante](assets/content-simulation-click-pencil-icon.png)

La tarjeta cambiará para mostrar los detalles en los que se basa la personalización
![Perfil Alex procesando Variante 1 para mayores de 40](assets/content-simulation-variant-1-age-above-40.png)

- **Jason** → Ve **Variante 2** (Edad inferior a 40)
Haga clic en el icono de lápiz sobre la segunda variante para **Mostrar detalles de la variante**

![Haga clic en el icono de lápiz para ver los detalles de la variante](assets/content-simulation-click-pencil-icon-for-second-variant.png)

Cambie la vista de Lado a lado a **Apilada verticalmente** para ver los detalles y la personalización de Jason en paralelo

![Jason representa el perfil Variant 2 para menores de 40](assets/content-simulation-swap-view-to-vertically-stacked.png) años

Al desplazarse por el contenido del correo electrónico, podemos ver el nombre completo de Jason, así como la imagen de contenido condicional que elegimos. ¡Qué guay es eso!

![Campo de nombre completo personalizado mostrado para Jason en la variante 2](assets/content-simulation-personalized-name-field-variant-2.png)



## Validar comportamiento de reserva

**Inconvenientes y valores predeterminados:** Compruebe que su correo electrónico gestiona correctamente los datos que faltan o los escenarios en los que no coinciden. Por ejemplo, simule un perfil con un campo vacío de año de nacimiento o uno que no cumpla los requisitos de ninguna oferta segmentada. La vista previa debe mostrar un bloque de contenido predeterminado o un marcador de posición adecuado en lugar de contenido roto o vacío. Si la simulación muestra una sección vacía en la que el contenido debe estar vacío, eso indica que puede que necesite configurar una oferta de reserva o un texto predeterminado en el diseño.


## Resumen

En este módulo ha realizado correctamente lo siguiente:

- Simulación de contenido personalizado mediante perfiles de muestra
- Lógica de cambio de variante validada
- Los campos personalizados confirmados se rellenan correctamente

Ya está listo para el siguiente módulo: **Alineación de marca**,
donde evaluará su correo electrónico con las directrices de marca de Connection 5G mediante IA.
