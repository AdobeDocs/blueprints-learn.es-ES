---
hold: true
title: Simulación de contenido
description: Aprenda a utilizar la herramienta de simulación de Adobe Journey Optimizer con datos de perfil de muestra para validar campos personalizados, variantes de contenido y comportamientos de reserva.
doc-type: article
solution: Experience Platform
exl-id: 3e2b064f-5680-461c-a49e-2a61514e146f
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '443'
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

En este módulo final, probará su correo electrónico con **dos variantes condicionales** usando la herramienta de simulación en Adobe Journey Optimizer.
Esto le permite obtener una vista previa de cómo los distintos clientes experimentarán el mensaje personalizado, lo que garantiza la precisión antes de iniciar la campaña.

Utilizará el archivo de perfil de prueba de muestra **sample.csv** de su conjunto de herramientas.

![Ejemplo de archivo de perfil de prueba sample.csv del kit de herramientas](assets/content-simulation-sample-csv-toolkit-file.png)

## Abra la herramienta de simulación

1. Abra el correo electrónico completado.
1. Haga clic en **Simular contenido**.
1. Seleccione **Simular variación de contenido**.

![Haciendo clic en Simular contenido y seleccionando Simular variación de contenido](assets/content-simulation-click-simulate-content-variation.png)

Después de unos segundos, se abre un panel de simulación.

## Carga de los datos del perfil de prueba

1. Abra **sample.csv** desde la carpeta del kit de herramientas.
   - **Alex** → de más de 40 años
   - **Jason** → menor de 40 años
2. Haga clic en **Cargar datos de entrada**.

![Botón Cargar datos de entrada en el panel de simulación](assets/content-simulation-click-upload-input-data.png)

&#x200B;3. Elija **sample.csv** y haga clic en **Continuar**.

![Eligiendo sample.csv y haciendo clic en Continuar](assets/content-simulation-choose-sample-csv-continue.png)

AJO procesa el archivo y prepara las vistas previas.


## Revisar representación de variante

AJO muestra ambas variantes una al lado de la otra en función de los perfiles cargados.

**Resultados esperados:**

- **Alex** → Ve **Variante 1** (Edad superior a 40)

![Perfil Alex procesando Variante 1 para mayores de 40](assets/content-simulation-variant-1-age-above-40.png)

Si se desplaza hacia arriba, también verá campos personalizados con el nombre ahora, como puede ver a continuación.

![Campo de nombre personalizado mostrado para Alex en la variante 1](assets/content-simulation-personalized-name-field-variant-1.png)

- **Jason** → Ve **Variante 2** (Edad inferior a 40)

![Jason representa el perfil Variant 2 para menores de 40](assets/content-simulation-variant-2-age-below-40.png) años

Con el nombre completo de Jason también. ¡Qué guay es eso!

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
