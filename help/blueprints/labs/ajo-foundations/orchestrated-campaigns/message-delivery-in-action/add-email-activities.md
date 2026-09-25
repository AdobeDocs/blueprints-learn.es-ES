---
title: Añadir actividades de correo electrónico
description: Aprenda a añadir y configurar dos actividades de correo electrónico en ramas de ramificación independientes mediante diferentes configuraciones de canal de correo electrónico en una campaña orquestada.
doc-type: article
solution: Experience Platform
exl-id: e911a251-9f9f-484c-a2de-101b0fc2c417
source-git-commit: 96308d5726def849ef22540a5d13618017c40cc3
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%
---

# Añadir actividades de correo electrónico

## Objetivo

En el siguiente conjunto de pasos, se basará en la campaña para agregar dos actividades Email a las dos ramas de actividad Fork. Configurará las dos actividades de correo electrónico para utilizar los canales de correo electrónico creados anteriormente. Finalmente, también agregará la configuración básica de correo electrónico (asunto y cuerpo) a cada una de estas actividades de correo electrónico.

>[!CAUTION]
>
>Antes de continuar, debe asegurarse de que las dos configuraciones de canal de correo electrónico se muestren activas en su estado.
>
>![Ambas configuraciones de canal de correo electrónico muestran el estado activo](assets/add-email-activities-email-channel-configs-active.png "Configuraciones de canal de correo electrónico")



## Añadir actividad de correo electrónico de rama superior

1. Haga clic en **+** del flujo superior y seleccione **Correo electrónico** de las **actividades de canal**

   ![Agregar actividad de correo electrónico](assets/add-email-activities-select-email-activity.png)

   Se abre el panel de detalles de **Correo electrónico**

   ![Panel de detalles de correo electrónico](assets/add-email-activities-email-details-pane.png)

2. Cambie el nombre de la etiqueta a **Correo electrónico con el atributo de perfil** para la actividad **Correo electrónico** y haga clic en **Editar correo electrónico**. Tenga en cuenta que la creación del cuerpo del correo electrónico solo se realiza con fines de prueba

   ![Cambie el nombre de la etiqueta de actividad Correo electrónico y haga clic en Editar correo electrónico](assets/add-email-activities-rename-and-edit-email.png)

3. Seleccione la ficha **Acciones** y, en la lista desplegable, seleccione la configuración de canal **Perfil-Correo electrónico**

   ![Seleccione la configuración de canal de correo electrónico-perfil en la pestaña Acciones](assets/add-email-activities-select-profile-email-channel.png)

4. A continuación, haga clic en **Editar contenido** para agregar contenido de prueba

   ![Haga clic en Editar contenido para agregar contenido de prueba](assets/add-email-activities-edit-content.png)

5. Proporcione una **Línea de asunto** (&quot;Oferta de actualización para miembros del plan básico&quot;) y haga clic en el botón **Editar cuerpo del correo electrónico**

   ![Agregar línea de asunto y editar cuerpo del correo electrónico](assets/add-email-activities-subject-line-edit-body.png)

6. Hay muchas opciones, para esta prueba, elige **Codifique su propia opción** de HTML

   ![Elija una opción de HTML para codificar](assets/add-email-activities-code-your-own-html.png)

7. En **Enviar correo electrónico a Designer**, inserte una línea de prueba &quot;Oferta de actualización disponible&quot;. justo antes de las etiquetas `</body></html>` tal y como se muestra y haz clic en **Guardar**

   ![Inserte una línea de prueba en el correo electrónico Designer y haga clic en Guardar](assets/add-email-activities-email-designer-save.png)

8. Espere a que el mensaje de confirmación aparezca en la esquina inferior derecha

   ![Aparece un mensaje de confirmación](assets/add-email-activities-confirmation-message.png)

9. Haga clic en la **flecha izquierda** junto al **Designer de correo electrónico** para salir

   ![Haga clic en la flecha izquierda para salir del correo electrónico Designer](assets/add-email-activities-exit-email-designer.png)

10. Aparece un cuadro de diálogo de confirmación, haga clic en el botón **Guardar y cerrar**

![Cuadro de diálogo de confirmación con el botón Guardar y cerrar](assets/add-email-activities-save-and-close-dialog.png)

1. Revise las propiedades y acciones de correo electrónico, incluido el texto agregado al cuerpo del correo electrónico. Haga clic en la **flecha izquierda** para regresar al lienzo de la campaña

![Volver al lienzo de Campaign](assets/add-email-activities-back-to-campaign-canvas.png)

## Añadir actividad de correo electrónico de rama inferior

De nuevo en el lienzo de la campaña, haz clic en **+** del flujo inferior y selecciona **Correo electrónico** de las **actividades del canal**. Siga los mismos pasos que se indican arriba (pasos 2 a 11), excepto los siguientes:

- Cambie el nombre de la etiqueta a **Correo electrónico con Dimension de Target** para la actividad **Correo electrónico**
- En la configuración de correo electrónico, elija la configuración de canal de correo electrónico **Correo electrónico relacional**

![Segunda actividad de correo electrónico configurada con el canal de correo electrónico relacional](assets/add-email-activities-bottom-branch-relational-email.png "Agregar la segunda actividad de correo electrónico")

## Resumen

Ahora ha visto cómo configurar las actividades de correo electrónico con los canales de correo electrónico. Cada actividad se configuró con un asunto y un cuerpo de correo electrónico muy básicos. La próxima vez se probará toda la campaña.
