---
title: Creación de fragmentos de contenido
description: Aprenda a dividir un diseño de correo electrónico en fragmentos reutilizables, como un bloque de encabezado, que sean coherentes en todas las plantillas de Adobe Journey Optimizer.
doc-type: article
solution: Experience Platform
exl-id: 253a9332-dc08-420d-ac11-2bf342f0dc38
source-git-commit: d935e9a5179579e35c6aa5fe9e495f5bba1a1b03
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%
---

# Creación de fragmentos de contenido

## Creación de contenido con plantillas y fragmentos

**Propósito:** Aprenda a crear fragmentos reutilizables en Adobe Journey Optimizer y, a continuación, aplíquelos dentro de un correo electrónico real dentro de un recorrido.

## Objetivos de aprendizaje

Al final de este módulo, deberá ser capaz de:

1. Desglose los diseños de correo electrónico en fragmentos reutilizables.
1. Cree fragmentos de encabezado, pie de página, banner, cuerpo y CTA.

## Por qué importan los fragmentos

Los fragmentos le permiten crear contenido coherente y alineado con la marca que se puede reutilizar en correos electrónicos, campañas y recorridos.

### Fragmentos

Componentes básicos reutilizables como:

- Encabezados
- Pies de página
- CTA
- Titulares
- Descargo de responsabilidad legal

Cada vez que se actualiza un fragmento, todos los correos electrónicos que lo utilicen se actualizarán automáticamente.

## Cómo encaja esto en la creación de correo electrónico

- **Crear fragmentos** para elementos que cambian con poca frecuencia.
- **Cree una plantilla** que use esos fragmentos.
- **Usa la plantilla** en el correo electrónico de tu campaña y personaliza su contenido.

A continuación se muestra el correo electrónico final que creará a partir de este laboratorio.

![Diseño final de correo electrónico que usted creó en este laboratorio](assets/building-content-fragments-final-email-preview.png)

Sin embargo, el equipo de diseño normalmente le proporciona plantillas como esta:

![Plantilla de diseño genérica proporcionada por el equipo de diseño](assets/building-content-fragments-generic-design-template.png)


## Paso 1: Crear fragmentos de contenido

La siguiente plantilla es una plantilla de diseño genérica y nuestro objetivo es desglosarla en bloques de contenido repetibles. En Adobe recorrido Optimizer, esto se denomina **Fragmentos**.

El primer paso es identificar cuántos fragmentos necesitamos crear. En esta plantilla tiene sentido utilizar 5 fragmentos como se muestra a continuación.



![Plantilla desglosada en cinco fragmentos identificados](assets/building-content-fragments-five-fragments-identified.png)

Hemos identificado las plantillas que requieren 5 fragmentos como se indica a continuación.

- Header
- Titular
- CTA
- Cuerpo
- Pie

>[!NOTE]
>
>Para este ejercicio, cree solo un fragmento de encabezado para ahorrar tiempo.



Cree un fragmento de encabezado para empezar. Sin embargo, antes de crear el fragmento, configure una carpeta de recursos ya que el entorno de recursos es compartido. Para ello, primero cree su propia carpeta.

1. En el panel de navegación izquierdo, localice la sección **Administración de contenido** y haga clic en **Assets**.

   ![Sección de administración de contenido con opción de Assets en la navegación izquierda](assets/building-content-fragments-content-management-assets-nav.png)

2. Haga clic en **Assets** en la sección Administración de Assets.

   ![Opción de Assets en la sección de administración de Assets](assets/building-content-fragments-assets-under-assets-management.png)

3. Cree una carpeta haciendo clic en el botón **&quot;Crear carpeta&quot;**.

   ![Botón Crear carpeta en el área de Assets](assets/building-content-fragments-click-create-folder-button.png)

4. Dé un nombre como su nombre y apellido. p. ej. Nish\_Pithia\_LabAssets (Algo que puede recordar)

   ![Nombrar la nueva carpeta de recursos con su nombre y apellidos](assets/building-content-fragments-name-asset-folder.png)

5. Haz doble clic en la carpeta recién creada para **abrirla**. Luego haz clic en **Agregar Assets** y busca o suelta todas las imágenes .png y .jpg de la carpeta del kit de herramientas. Luego haga clic en **Cargar**

   ![Haga clic en Agregar recursos y cargue archivos de imagen](assets/building-content-fragments-add-assets-and-upload-image-files.png)

   ![Haga clic en Cargar](assets/building-content-fragments-click-upload.png)

6. **Crear un nuevo fragmento:** En Administración de contenido, haga clic en **Fragmentos** y cree un nuevo fragmento.

   ![Opción Fragmentos en Administración de contenido para crear un nuevo fragmento](assets/building-content-fragments-click-fragments-create-new.png)

   Asigne un nombre descriptivo como se muestra a continuación. Añada todos los detalles como se indica a continuación:

   **Nombre:** encabezado

   **Descripción:** encabezado de fragmento para la plantilla

   **Tipo:** Seleccionar fragmento visual

   ![Nombre del fragmento de encabezado, descripción y campos de tipo de fragmento visual](assets/building-content-fragments-fragment-name-type-details.png)

7. Haz clic en **Crear botón** en la parte superior derecha.

   ![Botón Crear en la parte superior derecha del nuevo cuadro de diálogo de fragmento](assets/building-content-fragments-click-create-button-top-right.png)

   Se abrirá una pantalla en blanco del creador de fragmentos.

8. Vaya a la ficha **Componentes** en la columna izquierda. A continuación, haga clic en la columna **1:1** debajo de Estructuras y arrastre en el lienzo como se muestra a continuación. (Haga clic en la imagen siguiente para ver un gráfico animado)

   ![Arrastrando una estructura de columnas 1:1 al lienzo del fragmento](assets/building-content-fragments-drag-1-1-columns-structure.png)

9. A continuación, arrastre &quot;**image**&quot; a la fila 1:1 que acabamos de agregar

   ![Arrastrando un componente de imagen a la fila 1:1](assets/building-content-fragments-drag-image-onto-row.png)

10. Haga clic en **&quot;Examinar&quot;** para seleccionar la imagen del logotipo que le han proporcionado y que ya ha subido a Assets.

![Haga clic en el botón Examinar para seleccionar la imagen del logotipo](assets/building-content-fragments-click-browse-button.png)

11. Vaya a la carpeta, haga clic en la imagen del logotipo (*C5G-Logo.png*) y haga clic en **Seleccionar**.

![Seleccionar C5G-Logo.png de la carpeta Assets](assets/building-content-fragments-select-logo-from-assets.png)

12. El logotipo está colocado correctamente, pero es demasiado grande y debe cambiarse de tamaño. Para cambiar el tamaño del logotipo, actualice sus propiedades. Haga clic en la ficha **Estilos** de la columna derecha y establezca el ancho en 40% arrastrando el control deslizante, como se muestra a continuación.

>[!NOTE]
>
>Tenga en cuenta que cuando el botón de alternancia está activado, el número 40 representa % y no píxeles. Si desea un valor absoluto de píxel perfecto, cambie el botón a píxeles.



![El control deslizante de anchura de la ficha Estilo se ha establecido en 40 por ciento para cambiar el tamaño del logotipo](assets/building-content-fragments-resize-logo-width-slider.png)

13. Haga clic en **&quot;Guardar&quot;** y se guardará el fragmento. Recibe una notificación de barra verde en la confirmación.

![Barra de confirmación verde después de guardar el fragmento](assets/building-content-fragments-save-fragment-confirmation.png)

14. El fragmento guardado está en modo de borrador. Antes de usarlo, debe publicarlo. Haga clic en el botón **atrás**.

![Botón Atrás para dejar el fragmento de borrador antes de publicar](assets/building-content-fragments-click-back-button-draft.png)

15. Haga clic en el botón &quot;**Publicar**&quot;. Verá el mensaje &quot;Publicando fragmento, esto puede tardar. Notificaremos una vez hecho&quot;. en la confirmación. El fragmento está listo para utilizarse para la creación de plantillas.

![Botón Publicar y mensaje de confirmación de fragmento de publicación](assets/building-content-fragments-click-publish-fragment-button.png)

Verá el cambio de estado a **&quot;Activo&quot;**. En este punto, ha completado la creación de un fragmento de encabezado, que se utilizará en el siguiente paso.

![Se cambió el estado del fragmento de encabezado a Activo](assets/building-content-fragments-fragment-status-live.png)

>[!NOTE]
>
>Tenga en cuenta que en este ejercicio solo ha creado un fragmento. En la práctica, los arquitectos pueden elegir crear varios fragmentos, como encabezados, pies de página u otros componentes reutilizables.

## Resumen

En este módulo ha realizado correctamente lo siguiente:

- Desglose de un correo electrónico en un fragmento de encabezado reutilizable
- Bloques de contenido de encabezado creados

Ya está listo para pasar al siguiente módulo: **Creación de una plantilla de contenido**, donde usará el fragmento que creó para generar una nueva plantilla.
