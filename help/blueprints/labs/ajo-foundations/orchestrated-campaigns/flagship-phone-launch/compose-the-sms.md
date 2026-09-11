---
title: Componga el SMS
description: Aprenda a componer y personalizar un mensaje SMS en campañas orquestadas utilizando la marca del teléfono y los atributos del modelo de la tienda relacional.
doc-type: article
solution: Experience Platform
exl-id: 3deb822b-8374-4537-a260-f4f6f4d67569
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Componga el SMS

## Objetivo

En los siguientes pasos va a redactar un mensaje SMS MUY simple.  Verá cómo puede añadir fácilmente contenido a un nivel EXTREMADAMENTE básico y personalizar el mensaje en función de los datos del almacén relacional.



## Navegar al contenido

Haga clic en el botón **Editar contenido** o vaya directamente a la pestaña **Contenido**

![Editar botón de contenido y navegación de la pestaña de contenido &quot;Editar contenido&quot;](assets/compose-the-sms-navigate-to-content-tab.png "Editar contenido")



## Creación del mensaje

1. Haz clic en el botón **Personalization** para crear tu mensaje.

   ![Botón Personalization para crear el mensaje SMS](assets/compose-the-sms-click-personalization-button.png)

   >[!NOTE]
   >
   >La opción &quot;varita mágica&quot; utiliza IA para ayudarle a escribir un mensaje. Compruébalo si quieres, pero no vamos a estar cubriéndolo en este laboratorio.



2. Copie y pegue el texto siguiente en el cuerpo del mensaje SMS.

   ```none
   Hi from Connection 5G! Your phone_make phone_model is eligible for a free upgrade to one of the new iPhone 17 models. Shop online or come into a store today to take advantage of this offer.
   ```

   >[!NOTE]
   >
   >Asegúrese de activar el ajuste de línea en **Activado** en el editor de mensajes.  Se encuentra en el panel inferior derecho de la ventana.



3. Actualice los dos campos del mensaje **phone\_make** y **phone\_model** más abajo con la opción **Atributos de destino** en el carril izquierdo.  Cuando termine, el mensaje debe coincidir con la captura de pantalla.

   ![Mensaje SMS final con marca y modelo de teléfono personalizados](assets/compose-the-sms-final-message-text.png)

   >[!NOTE]
   >
   >¿Por qué haces esto?  Bueno, desea personalizar el mensaje con la marca y el modelo del teléfono de los clientes y esta información se encuentra en la tabla Línea del cliente de la tienda relacional.  Esto muestra cómo se pueden utilizar datos de campañas orquestadas para personalizar mensajes.



4. Haga clic en **Validar** en el editor, compruebe que no haya errores de validación y, si es correcto, haga clic en el botón **Guardar**

   ![Botones Validar y Guardar en el editor de mensajes](assets/compose-the-sms-validate-and-save.png)



5. Haga clic en la **flecha hacia atrás (\&lt;-)** cuando haya terminado para volver al lienzo del flujo de trabajo

![Flecha hacia atrás para volver al lienzo del flujo de trabajo](assets/compose-the-sms-return-to-canvas.png)



## Resumen

Acaba de crear un mensaje y, con suerte, ahora está un poco más familiarizado con el funcionamiento del editor de mensajes.  Recuerde que puede personalizar con datos de la Tienda relacional, pero también puede personalizar con datos del Perfil del cliente en tiempo real.

>[!NOTE]
>
>Si utiliza los atributos de Perfil del cliente en tiempo real para personalizar mensajes en campañas orquestadas, solo recuerde que se está extrayendo del conjunto de datos de instantáneas de perfil en el lago de datos, por lo que los atributos pueden tener hasta 24 horas de antigüedad. La instantánea de perfil solo se actualiza una vez al día después del trabajo diario de segmentación por lotes.
