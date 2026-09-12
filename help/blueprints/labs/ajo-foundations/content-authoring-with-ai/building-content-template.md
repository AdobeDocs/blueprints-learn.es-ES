---
title: Creación de plantilla de contenido
description: Obtenga información sobre cómo crear una plantilla de correo electrónico reutilizable en Adobe Journey Optimizer importando HTML e insertando un fragmento de encabezado creado anteriormente.
doc-type: article
solution: Experience Platform
exl-id: e73f06b1-be8a-4096-949c-900db13db9f8
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---


# Creación de plantilla de contenido

## Creación de contenido con plantillas y fragmentos

**Objetivo:** Aprenda a crear plantillas reutilizables en Adobe Journey Optimizer

## Objetivos de aprendizaje

Al final de este módulo, deberá ser capaz de:

1. Cree una plantilla de correo electrónico completa con fragmentos y HTML importados.

## Por qué importan las plantillas

Las plantillas le permiten crear contenido coherente y alineado con la marca que se puede reutilizar en correos electrónicos, campañas y recorridos.

### Plantillas

Planes que estructuran:

- Ubicación del encabezado
- Área de contenido del cuerpo
- Área del pie
- Estilo de diseño estándar

Las plantillas garantizan la coherencia de la marca en todos los equipos y ahorran un tiempo de creación significativo.


## Creación de una nueva plantilla con fragmentos

Las plantillas ayudan a los usuarios a reutilizar diseños completos en todas las campañas. Las plantillas de contenido de Adobe Journey Optimizer son potentes herramientas diseñadas para simplificar y optimizar la forma de crear contenido reutilizable para campañas y recorridos. Tanto si está creando un mensaje de correo electrónico como un mensaje SMS o una notificación push, las plantillas le ayudan a ahorrar tiempo, ya que proporcionan estructuras prediseñadas que se pueden personalizar y compartir fácilmente entre los proyectos.

Para un proceso de diseño acelerado y mejorado, cree plantillas independientes para reutilizar fácilmente el contenido personalizado en las campañas y recorridos de Journey Optimizer.

Esta funcionalidad permite a los usuarios orientados a contenido trabajar en plantillas fuera de campañas o recorridos. Los usuarios de marketing pueden reutilizar y adaptar estas plantillas de contenido independientes dentro de sus propios recorridos o campañas.

## Crear plantilla

1. Vaya a **Administración de contenido → Plantillas de contenido**.

   ![Navegando a Administración de contenido y luego a Plantillas de contenido](assets/building-content-template-navigate-content-templates.png)

2. Haga clic en **Crear plantilla** y, a continuación, complete lo siguiente:
   - **Nombre:** `Promotional Template`
   - **Descripción:** `Promotional Template for phone products`
   - **Canal:** `Email`

   ![Crear formulario de plantilla con nombre, descripción y canal de correo electrónico](assets/building-content-template-create-template-form-fields.png)

3. Haga clic en **Crear**.

![Botón Crear para terminar de crear la plantilla promocional](assets/building-content-template-click-create-button.png)


## Añadir línea de asunto y abrir el diseñador de correo electrónico

1. Agregue la línea de asunto: `Promotional Template` y haga clic en **en el cuerpo del correo electrónico** para abrirlo y editarlo

   ![Agregando la línea de asunto y abriendo el cuerpo del correo electrónico para editar](assets/building-content-template-add-subject-line-open-editor.png)

2. Verá tres opciones:
   1. Diseñe desde cero
   2. Codifique su propio código
   3. Importar HTML

Seleccione la tercera opción. Haga clic en **Importar HTML**



![Seleccionar la opción Importar HTML entre las tres opciones de diseño](assets/building-content-template-select-import-html-option.png)

## Importar la plantilla de HTML proporcionada



1. Cargar el archivo html de plantilla de la carpeta del kit de herramientas `promotional-template-final.html`

   ![Cargando promotional-template-final.html desde la carpeta del kit de herramientas](assets/building-content-template-upload-html-template-file.png)

2. Haga clic en el botón Importar para **importar** la plantilla.

   ![Botón Importar para importar la plantilla de HTML cargada](assets/building-content-template-click-import-button.png)

3. Espere a que se procese el diseño. Observará problemas como vínculos de imagen rotos y falta de personalización de marca. (Este es el comportamiento esperado, ya que tenemos recursos de marcador de posición)

![Plantilla procesada que muestra vínculos de imagen rotos y marcadores de posición que faltan](assets/building-content-template-rendered-template-broken-images.png)


## Explorar estructura de plantillas

### Panel izquierdo

Los componentes &quot;**Structures**&quot; y &quot;**Contents**&quot; de Adobe Journey Optimizer (AJO) son elementos esenciales utilizados al diseñar correos electrónicos, páginas de aterrizaje y fragmentos de contenido. Las estructuras definen el marco de diseño, mientras que el Contenido proporciona los bloques de creación reales colocados dentro de esos diseños.

La sección del cuerpo de Adobe Journey Optimizer es el contenedor principal del contenido del correo electrónico o de la página. Sirve como raíz del espacio de diseño visual, donde todos los componentes de estructura (columnas, diseños) y los componentes de contenido (texto, imágenes, botones, etc.) están anidadas.

### Panel derecho

Las opciones &quot;**Settings**&quot; y &quot;**Style**&quot; de la sección del cuerpo de Adobe Journey Optimizer le permiten definir el aspecto y el diseño básicos del correo electrónico o la página. Estos controles afectan a todo el diseño, ya que el cuerpo es el elemento principal de todos los componentes.

![Opciones de configuración y estilo en el panel derecho de la sección del cuerpo](assets/building-content-template-body-settings-style-panel.png)


En la barra del carril izquierdo encontrará secciones para:

- Fragmentos
- Archivos
- Estructura del cuerpo
- URL seguidas

Verá que el fragmento de encabezado que creó en el ejercicio anterior aparece aquí como se muestra a continuación. Asegúrese de que el fragmento de encabezado se muestre como activo con un punto azul y no como borrador. Dedique tiempo a comprobar el resto de las secciones.

![Fragmento de encabezado mostrado activo con un punto azul en la barra lateral izquierda](assets/building-content-template-header-fragment-live-sidebar.png)

>[!NOTE]
>
>Si no ve el fragmento aquí, significa que no lo ha guardado correctamente y que debe volver a cargarlo.



## Insertar fragmentos de encabezado

Ahora, mejore la plantilla. Ya ha creado el encabezado y pie de página.

1. Arrastre una columna **1:1** sobre el contenido existente.

   ![Arrastrando una columna 1:1 sobre el contenido de la plantilla existente](assets/building-content-template-drag-1-1-column-above-content.png)

   Ves algo como esto.

   ![Diseño de plantilla después de agregar la nueva columna sobre el contenido](assets/building-content-template-column-added-above-content.png)

2. El fondo utiliza el color de fondo de la plantilla, que actualmente es negro. Establece su color de fondo **en blanco. Haga clic en** en la ficha Estilo del carril derecho y utilice el color blanco del selector de color.

   ![Estableciendo el color de fondo de la columna en blanco mediante el selector de color](assets/building-content-template-set-background-color-white.png)

3. Abra **Fragmentos** y arrastre su fragmento **Encabezado**.

   ![Arrastrando el fragmento de encabezado a la plantilla desde el panel Fragmentos](assets/building-content-template-drag-header-fragment-into-template.png)

4. Observe que el fragmento de encabezado está perfectamente alineado con la plantilla, como se muestra a continuación.

   ![Fragmento de encabezado perfectamente alineado dentro de la plantilla](assets/building-content-template-header-fragment-aligned-template.png)

5. Haga clic en el botón **Guardar** para guardar la plantilla y luego haga clic en **Atrás**.

![Botón Guardar para guardar la plantilla antes de hacer clic en Atrás](assets/building-content-template-click-save-button-template.png)

>[!NOTE]
>
>Tenga en cuenta que puede ver algunas imágenes rotas. Lo arreglaremos más tarde.


## Resumen

En este módulo ha realizado correctamente lo siguiente:

- HTML importado para crear una plantilla promocional completa

Ya está listo para pasar al siguiente módulo: **Creación del correo electrónico**
