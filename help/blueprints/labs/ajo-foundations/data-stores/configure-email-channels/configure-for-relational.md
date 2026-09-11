---
hold: true
title: Configurar para relacional
description: Aprenda a configurar un canal de correo electrónico con el atributo de correo electrónico de un esquema relacional solo para campañas orquestadas.
doc-type: article
solution: Experience Platform
exl-id: 6f299942-79a6-42c2-8a5b-dd4bccd6aad4
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 10%

---


# Configurar para relacional

## Objetivo

En el siguiente conjunto de pasos creará una configuración de canal de correo electrónico para usarla solo con campañas orquestadas, usando el atributo `email` del esquema relacional `dep-rel: Customer Account`

## Crear configuración de canal

1. Vaya a **Configuraciones de canal** que se encuentran en el menú **Administración → Canales → Configuración general**
2. Haga clic en el botón **Crear configuración**

![Crear configuración de canal](assets/configure-for-profile-create-configuration-button.png)

3. En el asistente Crear establezca los siguientes valores:
   - **Nombre:** `Relational-Email`
   - **Canal:** `Email`
   - **Acción de marketing:** `Email Targeting`

![Detalles de configuración del canal](assets/configure-for-relational-channel-configuration-name-values.png)

>[!NOTE]
>
>Al seleccionar Correo electrónico como canal, aparece una nueva sección Configuración de correo electrónico.





## Configurar tipo de correo electrónico

Definir **Tipo de correo electrónico** en **Marketing**

![Configuración de correo electrónico](assets/configure-for-profile-set-email-type-marketing.png)

## Configurar subdominio

En el menú desplegable **Subdominio**, seleccione **email.dep-labs.com**

![Menú desplegable de subdominios con email.dep-labs.com seleccionado](assets/configure-for-profile-select-email-subdomain.png "Configurar subdominio")

## Configurar detalles del grupo de IP

En el menú desplegable **grupo de IP**, seleccione **marketing**

![Menú desplegable de grupo de IP con marketing seleccionado](assets/configure-for-profile-select-marketing-ip-pool.png "Configurar detalles del grupo de IP")

## Configurar cancelación de suscripción a lista

1. Asegúrese de que la opción esté **habilitada** para cancelar la suscripción a una lista
1. En el área de preferencias de cancelación de suscripción a lista, asegúrese de que todas las casillas de verificación estén **marcadas**
1. En Administración de vínculos, asegúrese de que **Adobe managed** está seleccionado
1. Para el nivel de consentimiento, asegúrese de que esté establecido en **Canal**

![Configurar cancelación de suscripción a lista](assets/configure-for-profile-configure-list-unsubscribe-settings.png)

## Configurar parámetros de encabezado

1. Defina los campos siguientes como se indica a continuación:
   - **Nombre desde:** `DEP Labs`
   - **Del prefijo de correo electrónico:** `dep`
   - **Responder al nombre:** `DEP Labs Support`
   - **Responder al correo electrónico:** `reply@email.dep-labs.com`
   - **Prefijo de correo electrónico con error:** `error`

![Parámetros de encabezado](assets/configure-for-profile-email-header-parameters.png)

## Configurar correo electrónico CCO

Deje esto en blanco

>[!NOTE]
>
>Puede conservar una copia de los correos electrónicos enviados enviándolos a una bandeja de entrada CCO. Escriba la dirección de correo electrónico que desee para que cada correo electrónico enviado se copie de forma oculta a esta dirección de CCO. Tenga en cuenta que el dominio de la dirección CCO debe ser diferente de cualquier subdominio delegado a Adobe. Esta funcionalidad es opcional. *Cómo usar CCO para correos electrónicos*

## Configurar parámetros de reintento de correo electrónico

Déjelo con la configuración predeterminada de **Horas** establecida en **84**

## Configurar parámetros de seguimiento de URL

Mantener la configuración predeterminada

## Detalles de ejecución

1. En la ficha Campaña orquestada y **marque** la casilla de verificación Habilitado.

![Configurar campaña orquestada](assets/configure-for-profile-enable-orchestrated-campaign-tab.png)

2. En Dimensión de ejecución, configure lo siguiente:
   - **Enviar un mensaje por:** `Target Dimension `
   - **Dimension de destino de perfil:** `dep-rel: Customer Account - customer_id`

![Dimensión de ejecución](assets/configure-for-relational-execution-dimension-target-settings.png)

3. En Dirección de ejecución, configure lo siguiente:
   - **Source:** `Target Dimension`
   - **Dirección de envío:** `click on the Edit button`

![Dimension de destino](assets/configure-for-relational-execution-address-source-target-dimension.png)

4. En la ventana emergente, haga clic en la carpeta **dep-rel: Customer Account**

![Configurar dirección de entrega](assets/configure-for-relational-customer-account-folder.png)

5. Seleccione **Correo electrónico** y haga clic en el botón **Seleccionar**

![Correo electrónico como dirección de envío](assets/configure-for-relational-select-email-as-delivery-address.png)

6. Cuando termine, los detalles de ejecución finales se parecerán a la captura de pantalla siguiente

![Dimensión de ejecución configurada](assets/configure-for-relational-execution-details-final-result.png)

>[!NOTE]
>
>Para las campañas organizadas, se dirige a la cuenta del cliente con un correo electrónico, por lo que solo necesita enviar un mensaje por cada Dimension de Target.  La dirección de ejecución que usa proviene del propio Dimension de Target (es decir, lo que se almacena en la tabla **dep-rel: Customer Account** para la dirección **email**)


## Revisar y guardar

1. Revise todos los detalles de nuevo para asegurarse de que coinciden.
1. Desplácese hacia arriba y haga clic en **Enviar**.
1. Cuando haya terminado, verá dos configuraciones de canal de correo electrónico, ambas probablemente en estado de &quot;procesamiento&quot;.

>[!WARNING]
>
>Se ha observado que el procesamiento de la configuración del canal de correo electrónico tarda hasta dos horas.

## Resumen

Ahora ha visto cómo crear una configuración de canal de correo electrónico para utilizar el atributo de esquema relacional para campañas orquestadas.
