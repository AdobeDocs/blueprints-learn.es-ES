---
title: Prueba del correo electrónico
description: Obtenga información sobre cómo enviar y verificar correos electrónicos de prueba en Adobe Journey Optimizer para validar contenido personalizado y variantes condicionales antes de la activación.
doc-type: article
solution: Experience Platform
exl-id: 1abab39e-811c-4010-a4f5-a7adc9e4e0a4
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Prueba del correo electrónico

## Objetivos de aprendizaje

Al final de este módulo, deberá ser capaz de:

- Envíe correos electrónicos de prueba desde el editor de correo electrónico de Adobe Journey Optimizer.
- Valide contenido personalizado y variantes condicionales mediante correos electrónicos de prueba.
- Compruebe la entrega de prueba de correo electrónico en la bandeja de entrada, incluido el manejo de correo no deseado y mensajes recortados.
- Revise los registros de envío de pruebas, las marcas de tiempo y las variantes en Adobe Journey Optimizer.
- Confirme que el contenido del correo electrónico es preciso, personalizado y está listo para su activación.


## Enviar correos electrónicos de prueba (opcional, pero recomendada)

En este punto, ha aprendido que no solo podemos personalizar los atributos de perfil, sino que también podemos utilizar atributos para crear una lógica condicional que determine el contenido que desea mostrar. Adobe Journey Optimizer es extremadamente potente y ofrece a los especialistas en marketing mucha flexibilidad.

1. Haga clic en **Simular contenido**.
2. Seleccione **Simular variación de contenido**.

   ![Haciendo clic en Simular contenido y seleccionando Simular variación de contenido](assets/content-simulation-click-simulate-content-variation.png)

   Se abre un panel de simulación.

3. Haga clic en **Enviar revisión**.

   ![Botón Enviar prueba en el panel de simulación](assets/test-the-email-click-send-proof-button.png)

4. Añada su propia dirección de correo electrónico personal.

   >[!NOTE]
   >
   >Tenga en cuenta que, a veces, el correo electrónico corporativo bloqueará los correos electrónicos de la zona protegida. Le recomendaría que use su correo electrónico personal.



5. Seleccione ambas variantes.
6. Añadir prefijo de línea de asunto
   1. Variante 1: superior a 40
   2. Variante 2: por debajo de 40
7. Haga clic en **Enviar revisión**. Recibe un mensaje de confirmación verde &quot;**Pruebas enviadas correctamente**&quot;

![Mensaje de confirmación verde que muestra las pruebas enviadas correctamente](assets/test-the-email-proofs-sent-successfully-confirmation.png)

Compruebe que ambos correos electrónicos hayan llegado a la bandeja de entrada.

>[!NOTE]
>
>Los correos electrónicos de revisión pueden llegar a **Correo no deseado** según los filtros.



![Correo electrónico de prueba que aterrizó en la carpeta de correo no deseado](assets/test-the-email-proof-email-in-spam-folder.png)

Puede que experimente un mensaje recortado, pero está bien, ya que algunos de los vínculos de pie de página no son reales. Si hace clic en el vínculo, verá que han llegado ambos correos electrónicos con variantes.

![Correo electrónico de prueba recortado que muestra ambas variantes después de hacer clic en el vínculo](assets/test-the-email-clipped-proof-email-variants.png)

### Verificación del envío de pruebas en AJO

Por último, también puede ver la entrega de pruebas en Adobe Journey Optimizer.

1. Vuelva al editor de correo electrónico.
2. Vuelva a la pantalla de creación de correo electrónico y haga clic en **Ver revisión**.
3. Revise los registros de envío, las marcas de tiempo y las variantes enviadas.

![Botón Ver prueba en la pantalla de creación de correo electrónico](assets/test-the-email-click-view-proof-button.png)

Observará los detalles del correo electrónico de prueba.

![Registros de envío de correo electrónico de prueba, marcas de tiempo y variantes enviadas en AJO](assets/test-the-email-proof-email-delivery-details.png)


## Resumen

En este módulo ha realizado correctamente lo siguiente:

- Correos electrónicos de prueba enviados y verificados en AJO

Ahora ha completado el Recorrido completo de Conexión 5G AJO Lab y ha validado que su correo electrónico es preciso, personalizado y está listo para activarse.
