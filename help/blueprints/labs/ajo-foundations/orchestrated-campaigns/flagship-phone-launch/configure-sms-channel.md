---
hold: true
title: Configuración del canal SMS
description: Aprenda a configurar un canal de SMS basado en Twilio y sus dimensiones de ejecución para utilizarlo en campañas orquestadas.
doc-type: article
solution: Experience Platform
exl-id: 63c994f2-4b6b-42e9-aa82-cb6697390a08
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Configuración del canal SMS

## Objetivo

En el siguiente conjunto de pasos configurará el canal SMS. Esto es necesario para poder enviar mensajes a los titulares de línea individuales más adelante cuando esté creando la campaña.



## Navegar a canales

1. En Adobe Journey Optimizer, vaya al menú **Administración** -> **Canales**.
1. Seleccione **Configuración de SMS** → **credenciales de API**.
1. Haga clic en **Crear credencial de API**.

![Vaya a Configuración de SMS y credenciales de API en el menú Canales de administración &quot;Vaya a Configuración de SMS&quot;](assets/configure-sms-channel-navigate-to-sms-settings.png "Vaya a Configuración de SMS")



## Defina las credenciales de la API de SMS

Empezará creando el conector de API que AJO utilizará para enviar solicitudes de SMS salientes.

1. En Proveedor de SMS, elija **Twilio**.
1. Escriba los siguientes detalles de credenciales de API, usando su propia [cuenta de prueba de Twilio](https://www.twilio.com/try-twilio):
   - **Nombre:** `DEP SMS`
   - **SID de cuenta:** encontrado en su tablero de la consola Twilio
   - **Se encontró el token de autenticación:** en el panel de la consola Twilio (haz clic en **Ver** para mostrarlo)
1. Haga clic en **Enviar** para registrar la credencial de la API

>[!NOTE]
>
>Necesitarás una cuenta de prueba gratuita de Twilio con un número de teléfono verificado antes de comenzar este paso. Regístrese en [twilio.com/try-twilio](https://www.twilio.com/try-twilio) y busque el SID de cuenta y el token de autenticación en el panel de la consola de Twilio.

![Campos de credencial de API de SMS para el proveedor Twilio](assets/configure-sms-channel-enter-api-credentials.png)



## Creación de configuración de canal SMS

Ahora asignará esta credencial de API a una configuración de canal que puedan utilizar los recorridos y las campañas.

1. Vaya a **Canales** → **Configuración general** → **Configuraciones de canal**.

![Vaya a las configuraciones de canal en Configuración general](assets/configure-sms-channel-navigate-channel-configurations.png)



&#x200B;2. Haga clic en **Crear configuración de canal**.

![Botón Crear configuración de canal](assets/configure-sms-channel-click-create-configuration.png)



&#x200B;3. Complete los Ajustes de configuración de canal SMS con los siguientes valores:
   - **Nombre:** `Relational-SMS-Multi-Entity`
   - **Canal:** `Mobile Message`
   - **Acción de marketing:** `SMS Targeting`

&#x200B;> [!NOTE]
>
>Si aparece un error que indica que el usuario no tiene permiso, ignórelo y continúe.

## Configuración de SMS

Al seleccionar Canal como Mensaje móvil, aparece una nueva sección llamada Configuración de SMS. Rellénelo con los siguientes detalles:

- **Tipo de mensaje móvil:** `Marketing`
- **Configuración de mensaje móvil:** `DEP SMS`
- **Número de remitente:** `01234567890`
- **Subdominio:** `leave blank`
- **Número de exclusión:** `leave blank`

![Configuración de SMS con número de remitente y tipo de mensaje móvil](assets/configure-sms-channel-sms-settings-fields.png)



## Detalles de ejecución

1. En Detalles de ejecución, haga clic en la ficha **Campaña organizada**

![Ficha de campaña orquestada en Detalles de ejecución](assets/configure-sms-channel-execution-details-tab.png)



&#x200B;2. Asegúrese de que la casilla de verificación **Habilitado** esté marcada

![Casilla de verificación habilitada para campañas orquestadas](assets/configure-sms-channel-enabled-checkbox.png)



&#x200B;3. A continuación, en la subsección **Dimensión de ejecución**, asegúrese de que las siguientes opciones estén configuradas de la siguiente manera:
   - **Enviar mensaje por:** `Target + Secondary Dimension`
   - **Dimension de destino de perfil:** `dep-rel: Customer Account - customer_id`
   - **Dimension secundario:** `Customer Line`

![Configuración de la dimensión de ejecución con el destino y la dimensión secundaria](assets/configure-sms-channel-execution-dimension-setup.png)

![Dimension secundario establecido en Línea de cliente en la configuración de la dimensión de ejecución &quot;Dimension secundario&quot;](assets/configure-sms-channel-secondary-dimension-detail.png "Dimension secundario")

>[!NOTE]
>
>Esto le indica a las campañas orquestadas que cuando envía mensajes, debe enviar un mensaje por registro que coincida con el Dimension de destinatario del perfil.



&#x200B;4. Bajo el encabezado Dirección de ejecución, asegúrese de seleccionar el botón de opción de **Dimension secundario** y, a continuación, haga clic en el botón de edición en el **Campo de ejecución de SMS**

![Dirección de ejecución establecida en Dimension secundario con campo de edición](assets/configure-sms-channel-execution-address-selection.png)



&#x200B;5. En el elemento emergente, haga clic en el esquema **dep-rel: Customer Line** y seleccione **Teléfono móvil**.

![Ventana emergente de esquema para el elemento dep-rel: Esquema de línea del cliente](assets/configure-sms-channel-customer-line-schema-popup.png)

![Campo de teléfono móvil seleccionado del rel profundo: Esquema de línea del cliente &quot;Campo de teléfono móvil&quot;](assets/configure-sms-channel-mobile-phone-field-selected.png "Campo de teléfono móvil")



&#x200B;6. Confirme las coincidencias de la sección Detalles de ejecución final a continuación

![La configuración de los detalles de la ejecución final coincide con la configuración requerida](assets/configure-sms-channel-final-execution-details.png)



## Enviar y revisar

1. Puede hacer clic en el botón **Enviar** para completar la configuración y ver cómo aparece un mensaje de éxito

![Mensaje de éxito después de enviar la configuración del canal](assets/configure-sms-channel-submit-success-message.png)



&#x200B;2. En la página de inventario de configuraciones de canal, asegúrese de que el estado se muestre como **Activo** antes de continuar

![Estado de configuración del canal mostrado como Activo](assets/configure-sms-channel-active-status.png)

>[!CAUTION]
>
>Espere hasta que el estado se convierta en **Activo**; de lo contrario, los pasos de laboratorio futuros fallarán miserablemente para usted



&#x200B;3. Cuando el estado se active, estará completo.

>[!TIP]
>
>🚀 ¡Booyah! Su canal SMS ya está activo y listo para la acción.



## Resumen

Ya ha visto cómo configurar correctamente un canal SMS.  Tenga en cuenta que este es un SMS basado en API, por lo que según el proveedor pueden utilizar métodos alternativos para la autenticación.

Puede leer más [aquí](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration) si está interesado.
