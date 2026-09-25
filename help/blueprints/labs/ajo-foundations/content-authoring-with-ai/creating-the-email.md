---
title: Creación del correo electrónico
description: Aprenda a aplicar una plantilla de contenido de marca a un correo electrónico de campaña en Adobe Journey Optimizer y a reemplazar imágenes de productos y héroes.
doc-type: article
solution: Experience Platform
exl-id: bf823714-7298-48fc-a18b-9bf2462ae52e
source-git-commit: 96308d5726def849ef22540a5d13618017c40cc3
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%
---

# Creación del correo electrónico

## Creación de contenido con plantillas

**Objetivo:** Aprenda a crear plantillas reutilizables en Adobe Journey Optimizer y, a continuación, aplíquelas en un correo electrónico real dentro de una campaña.

## Objetivos de aprendizaje

Al final de este módulo, deberá ser capaz de:

1. Cree una nueva campaña y utilice la nueva plantilla de marca.
1. Actualice las imágenes principales, las imágenes de producto, los botones y el estilo del diseño.

## Creación y actualización del correo electrónico en una campaña

### Objetivo

En este ejercicio, aprenderemos a aplicar la plantilla que ha creado a un correo electrónico dentro de un recorrido. En un escenario ideal, puede utilizar cualquier recorrido o campaña existente y reemplazar su contenido de correo electrónico con una plantilla estandarizada para garantizar la coherencia de la marca y una ejecución más rápida.

Este paso muestra cómo se pueden reutilizar las plantillas en todos los recorridos, lo que permite a los equipos actualizar los diseños sin volver a crear los correos electrónicos desde cero.

## Crear nueva campaña de correo electrónico

1. Vuelva a la pantalla principal y haga clic en **Administración de Recorridos → Campañas**.
2. Haz clic en **Crear campaña**

   ![Botón Crear campaña en Administración de Recorridos](assets/creating-the-email-click-create-campaign-button.png)

3. Seleccione &quot;**Orquestación - Marketing**&quot; y haga clic en **confirmar**

   ![Seleccionar orquestación - Marketing y hacer clic en confirmar](assets/creating-the-email-select-orchestration-marketing.png)

4. Asigne un nombre a la campaña `Flagship Phone Launch Branded`. Presione el botón **Guardar**.

   ![Poner nombre a la campaña y hacer clic en Guardar](assets/creating-the-email-name-campaign-save.png) en el lanzamiento de Flagship Phone

5. Haga clic en el signo **+** y seleccione la actividad **Leer audiencia**

   ![Más el signo para seleccionar la actividad Leer audiencia](assets/creating-the-email-click-plus-read-audience.png)

6. El siguiente paso es seleccionar el cuadro **&quot;Leer audiencia&quot;** y hacer clic en el **icono de la carpeta Audiencia**

   ![Icono de Leer cuadro de audiencia y carpeta de audiencia](assets/creating-the-email-read-audience-folder-icon.png)

7. Seleccione la audiencia **dep: interesado en iPhone 17** y haga clic en el botón &quot;**Agregar audiencia**&quot;

   ![Seleccionar la audiencia de iPhone 17 que le interesa y hacer clic en Agregar audiencia](assets/creating-the-email-select-audience-add-button.png)

8. Seleccione Entidad - **dep-rel: Cuenta de cliente - customer\_id** (o cualquier, ya que no importa para esta parte)
9. Agregue la **actividad de correo electrónico** haciendo clic en **+ signo** y, a continuación, seleccione **Correo electrónico** de las actividades del canal.

   ![Agregando la actividad de correo electrónico desde actividades del canal](assets/creating-the-email-add-email-channel-activity.png)

10. Haz clic en **Editar correo electrónico**.

![Editar opción de correo electrónico para la actividad de correo electrónico de la campaña](assets/creating-the-email-click-edit-email.png)

1. Haz clic en la pestaña **Acción** y selecciona **tu** configuración de correo electrónico. Su zona protegida puede mostrarla como un correo electrónico relacional. (Seleccione cualquiera)

   ![Ficha de acción con la configuración de correo electrónico seleccionada](assets/creating-the-email-action-tab-email-configuration.png)

1. Haz clic en **pestaña Contenido**

   ![Pestaña Contenido en el editor de correo electrónico](assets/creating-the-email-click-content-tab.png)

1. Haga clic en **Aplicar plantilla de contenido**

   ![Aplicar plantilla de contenido en el editor de correo electrónico](assets/creating-the-email-click-apply-content-template.png)

1. Seleccione la plantilla **&quot;Plantilla promocional&quot;** que creó y haga clic en **Confirmar**

   ![Seleccionando la plantilla promocional y haciendo clic en Confirmar](assets/creating-the-email-select-promotional-template-confirm.png)

1. Haz clic en **Editar cuerpo del correo electrónico**

   ![Editar opción de cuerpo del correo electrónico después de aplicar la plantilla](assets/creating-the-email-click-edit-email-body.png)

1. Confirme que el nuevo encabezado, la imagen a pantalla completa, el pie de página y los bloques de contenido aparecen correctamente.

![Los bloques de encabezado, imagen a pantalla completa, pie de página y contenido aparecen correctamente en el correo electrónico](assets/creating-the-email-header-hero-footer-blocks-confirmed.png)


## Reemplazar imagen a pantalla completa e imágenes de producto

Cambiar las imágenes de héroe y teléfono. Debe cargar contenido en los recursos desde la carpeta del kit de herramientas. Actualmente, la imagen del titular a pantalla completa del producto es un marcador de posición.

1. Haga clic en la imagen del titular de héroe roto.

   ![Haciendo clic en la imagen de titular de marcador de posición a pantalla completa](assets/creating-the-email-click-broken-hero-banner-image.png)

2. Elimine la URL de origen temporal.

   ![Quitando la dirección URL de origen temporal de la imagen](assets/creating-the-email-remove-temporary-source-url.png)

3. Haz clic en **Importar medios**

   ![Botón Importar medios para la imagen a pantalla completa](assets/creating-the-email-click-import-media.png)

4. Cargue `hero.png` de su kit de herramientas. (Puede arrastrar el archivo)

   ![Cargando hero.png desde la carpeta del kit de herramientas](assets/creating-the-email-upload-hero-png-file.png)

5. Haga clic en **Siguiente,** Seleccione **su carpeta para los recursos** y presione **importar**

   ![Seleccionando la carpeta de recursos y haciendo clic en importar para la imagen a pantalla completa](assets/creating-the-email-select-folder-import-hero.png)

6. Su plantilla de correo electrónico está saliendo bien. Aparece de la siguiente manera. Haga clic en **&quot;Guardar&quot;** para guardar el trabajo.

![Se ha actualizado la plantilla de correo electrónico con la nueva imagen a pantalla completa antes de guardar](assets/creating-the-email-save-updated-email-template.png)


## Ejercicio opcional

### Reemplazar imágenes de productos

Continúe, actualice todas las imágenes de producto (imágenes proporcionadas en la carpeta del kit de herramientas) y añada un borde redondeado a su gusto. Su correo electrónico se ve mejor sin ningún vínculo roto, como se muestra a continuación. Repita el proceso para todas las tarjetas de producto.

![Correo electrónico con todas las imágenes de productos actualizadas y sin vínculos rotos](assets/creating-the-email-product-images-updated-no-broken-links.png)

## Resumen

En este módulo ha realizado correctamente lo siguiente:

- Se ha creado una nueva campaña con correo electrónico utilizando la plantilla con marca.
- Imágenes actualizadas de productos y héroes
- Estilo mejorado

Ya está listo para pasar al siguiente módulo: **asistente de IA y personalización de contenido**, donde utilizará IA para refinar el texto y generar imágenes automáticamente.
