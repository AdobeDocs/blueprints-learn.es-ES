---
hold: true
title: Prueba de la campaña
description: Obtenga información sobre cómo ejecutar una campaña orquestada en modo de prueba e interpretar por qué un canal de correo electrónico basado en un perfil de AEP produce errores de entrega que un canal basado en una relación evita.
doc-type: article
solution: Experience Platform
exl-id: e77ae8ab-f18f-4683-8fdd-ba4f4629d96c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---


# Prueba de la campaña

## Objetivo

En el siguiente conjunto de pasos, ejecute la campaña en modo de prueba para confirmar las funciones de campaña según lo esperado antes de publicar la campaña. En este caso, el modo de prueba no envía correos electrónicos, pero ayuda a verificar todo el flujo e identificar los problemas de forma temprana.

## Inicio del flujo de trabajo

1. Una vez configurados los dos flujos de correo electrónico, la campaña tiene el siguiente aspecto. Haga clic en el botón **Iniciar** para ejecutar la campaña en **Modo de prueba**

![Haga clic en Iniciar para ejecutar la campaña en modo de prueba](assets/test-the-campaign-click-start-test-mode.png)

>[!NOTE]
>
>Como se mencionó en el laboratorio anterior, el modo de prueba permite validar la ejecución de la campaña y los resultados de las distintas actividades. Cada actividad se ejecuta secuencialmente hasta que se llega al final del flujo.



&#x200B;2. Se inicia la ejecución de prueba de todas las actividades de campaña y se verifican los resultados

![Ejecución de prueba de actividades de campaña en curso](assets/test-the-campaign-verify-execution-results.png)



## #1 de informe de correo electrónico

1. Para probar la entrega de correo electrónico, haga clic en el **correo electrónico con la actividad de atributo del perfil** y en el panel derecho, haga clic en **Ejecutar prueba**

![Ejecutar prueba para correo electrónico mediante la actividad de atributo de perfil](assets/test-the-campaign-run-test-profile-attribute.png)

&#x200B;2. Espere el mensaje de confirmación y haga clic en **Ver informe** para ver los detalles de la prueba de correo electrónico

![Haga clic en Ver informe para ver los detalles de la prueba de correo electrónico](assets/test-the-campaign-view-report-1.png)

&#x200B;3. La página Informe de correo electrónico se presenta con las estadísticas de Campaign y el estado de ejecución. La prueba de correo electrónico es una verificación de la actividad para asegurarse de que no haya errores y no envía correos electrónicos. Normalmente tarda unos \~**5** minutos en completarse.

![Página de informe de correo electrónico con estadísticas de Campaign](assets/test-the-campaign-campaign-statistics-1.png)

>[!NOTE]
>
>Es posible que tenga que actualizar la página varias veces para ver el resultado final de la prueba.



&#x200B;4. Una vez finalizada la prueba de correo electrónico, se presentan los resultados. Hay cierto porcentaje de errores; haga clic en **Ver más** para conocer el motivo.

![Tasa de error con el vínculo Ver más](assets/test-the-campaign-error-rate-view-more.png)

&#x200B;5. Los estados de razón `Email address not found in profile`

![Motivo: no se encontró la dirección de correo electrónico en el perfil](assets/test-the-campaign-email-not-found-reason.png)

>[!NOTE]
>
>Dado que la **dirección de envío** configurada para la actividad de correo electrónico, **correo electrónico con atributo de perfil**, se configuró para usar el atributo de perfil `personalEmail.address`, se creó una dependencia en el **perfil de AEP**.
>
>De los **38** ID de cliente calificados del esquema relacional, el sistema solo pudo encontrar **7** perfiles de AEP correspondientes. Para los restantes **31** de ellos, los perfiles de AEP no existían, lo que resultó en el mensaje de error `Email address not found in profile`.
>
>Es importante recordar que los datos del lago de datos y del almacén relacional se mantienen **consistentes** al usar atributos de perfil de AEP en campañas orquestadas.



## #2 de informe de correo electrónico

1. Repita el mismo proceso para el **correo electrónico con la actividad Dimension** de Target

![Ejecutar prueba para correo electrónico mediante la actividad de Dimension de Target](assets/test-the-campaign-run-test-target-dimension.png)

&#x200B;2. Espere el mensaje de confirmación y haga clic en **Ver informe** para ver los detalles de la prueba de correo electrónico

![Haga clic en Ver informe para ver los detalles de la prueba de correo electrónico](assets/test-the-campaign-view-report-2.png)

&#x200B;3. Una vez finalizada la prueba de correo electrónico, se presentan los resultados. En este caso, no habrá errores

![Estadísticas de campaña sin errores](assets/test-the-campaign-campaign-statistics-2.png)

>[!NOTE]
>
>Dado que la **dirección de envío** para la actividad de correo electrónico **Correo electrónico con Target Dimension**, se configuró para usar `dep_rel_customer_account.email`, desde el esquema relacional, no había dependencia en los perfiles de AEP ni en sus atributos.
>
>Se encontró que todos los **38** ID de cliente calificados tenían los correos electrónicos correspondientes en el almacén relacional y se pudieron segmentar correctamente sin errores.



## Detener el flujo de trabajo

Haga clic en el botón **Detener** para detener el **modo de prueba** de la campaña

>[!TIP]
>
>Ambas configuraciones de canal de correo electrónico se probaron dentro de la misma campaña y se observaron diferencias entre el uso de un atributo de perfil de AEP y el uso de la Dimension de Target en la configuración de canal de correo electrónico.
>
>Felicidades, esto concluye el laboratorio de entrega de mensajes.

## Resumen

Ahora ha visto cómo probar la campaña creada para comprender el flujo y el comportamiento. Aquí los matices de usar las diferentes configuraciones de configuración del canal de correo electrónico se entendieron bien durante la ejecución del flujo de prueba.

Puede leer más sobre el modo de prueba de la campaña [aquí](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/launch/start-monitor-campaigns), si está interesado.
