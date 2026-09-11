---
hold: true
title: Creación de atributos de oferta
description: Añada atributos de dispositivo personalizados como marca, modelo y nivel al esquema XDM de oferta estándar para su uso en reglas de clasificación y elegibilidad.
doc-type: article
solution: Experience Platform
exl-id: 00326a7c-8139-46f5-85bd-5ea1f63f29cf
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---


# Creación de atributos de oferta

## Objetivo

En esta sección, agregará campos XDM personalizados al esquema XDM de oferta estándar. Estos campos personalizados se pueden utilizar en la clasificación, la ordenación y los criterios de idoneidad. También pueden ser datos que se devuelven al dispositivo solicitante.

## Crear objeto principal de dispositivo personalizado

1. Expanda el elemento de menú **Decisioning** en el carril izquierdo si es necesario y haga clic en **Catálogos.**
2. De forma predeterminada, se muestra la página &quot;Ofertas&quot;. Haga clic en el botón **Editar esquema** en la esquina superior derecha.

![Editar botón de esquema en la página del catálogo de ofertas](assets/create-offer-attributes-edit-schema-button.png)

>[!TIP]
>
>La página resultante es el editor de esquemas XDM estándar. Del mismo modo que se utiliza XDM para definir la estructura de datos de los conjuntos de datos, aquí se utiliza XDM para definir los atributos de una oferta.

>[!NOTE]
>
>El esquema &quot;Elementos de oferta personalizados: Experience Decisioning&quot; es un esquema estándar generado por el sistema que se aplica a todas las ofertas. Sin embargo, se puede agregar a este esquema para satisfacer necesidades comerciales únicas, que es lo que hará en esta sección.
>
>Además, navegar por la página de ofertas es un método abreviado para llegar a este esquema. También puede navegar a él a través del menú Esquema en el carril izquierdo.

&#x200B;3. Haga clic en el icono **+** a la derecha del nivel raíz del esquema y, con el menú &quot;Propiedades del campo&quot; ahora visible en el carril derecho, rellene los campos siguientes con los valores proporcionados:
   - Nombre de campo: **dispositivo**
   - Nombre para mostrar: **Dispositivo**
   - Lista desplegable de tipos: **Objeto**
   - Asignar a grupo de campos (escriba este valor en): **Detalles de la oferta**

>[!NOTE]
>
>La opción Asignar a grupo de campos parece ser un menú desplegable, pero también acepta la entrada de texto directo; por lo tanto, introduzca el texto &quot;Detalles de la oferta&quot;. Al escribirlo, también verá un elemento &quot;Detalles de la oferta (nueva)&quot;. Cualquier atributo nuevo debe asignarse a un grupo de campos, por lo que en este paso creará un nuevo grupo de campos llamado Detalles de la oferta.

&#x200B;4. Asegúrese de que todas las propiedades se hayan rellenado como se muestra en la siguiente captura de pantalla:

![Propiedades de campo para el nuevo objeto Device rellenado](assets/create-offer-attributes-device-object-field-properties.png)

&#x200B;5. Una vez que haya verificado que todos los campos son correctos, haga clic en el botón azul **Aplicar** en la parte inferior del menú &#39;Propiedades del campo&#39; (carril derecho) para ver los cambios aplicados al esquema:

![Grupo de campos de dispositivo aplicado al esquema de oferta](assets/create-offer-attributes-device-object-applied.png)

>[!TIP]
>
>Al igual que el XDM normal, los atributos personalizados se agrupan en un área de nombres específica de la organización IMS, concretamente el ID de inquilino imsorg o &quot;dep&quot; en este caso. También verá que el nuevo grupo de campos &quot;Detalles de la oferta&quot; ahora aparece en el panel &quot;Composición&quot;, a la izquierda del esquema.

>[!WARNING]
>
>Tenga en cuenta que estos cambios NO se guardan. Simplemente son &quot;Aplicadas&quot;. Si tuviera que salir de la página sin guardar, perdería su trabajo. Complete los pasos de esta sección antes de salir.

## Crear atributos de dispositivo personalizados

Ahora que se ha creado el objeto XDM de dispositivo, puede pasar a la creación de campos específicos del dispositivo.

1. Haga clic en el icono **+** a la derecha del nuevo objeto **device** que acaba de crear y, con el menú &quot;Propiedades del campo&quot; en el carril derecho, rellene los campos siguientes con los valores proporcionados:
   - Nombre de campo: **make**
   - Nombre para mostrar: **Make**
   - Lista desplegable de tipos: **Cadena**
   - Asignar a grupo de campos: **Detalles de la oferta** (ya debería estar seleccionado)
   - Una vez que haya verificado que todos los campos son correctos, haga clic en el botón azul **Aplicar** para ver los cambios aplicados al esquema
2. Repita los pasos anteriores para agregar dos atributos adicionales para **Modelo** y **Nivel**. Utilice el mismo patrón de nomenclatura, tipo y grupo de campos. Cuando termine, el esquema debería tener este aspecto:

![Esquema de oferta que muestra los campos de marca, modelo y nivel completados](assets/create-offer-attributes-make-model-tier-fields.png)

&#x200B;3. Con todos los campos/atributos XDM nuevos creados, haz clic en **Guardar** en la esquina superior derecha y recibirás el mensaje verde &quot;Esquema guardado correctamente&quot; en la parte inferior de la pantalla. Ahora ha completado los pasos de esta sección.

>[!WARNING]
>
>El esquema que acaba de actualizar se aplica a TODAS las ofertas, incluidas todas las ofertas futuras. Se debe tener mucho cuidado al añadir atributos a este esquema. En nuestro ejemplo de caso de uso de una empresa de telecomunicaciones que vende teléfonos móviles, la marca del dispositivo, el modelo y los atributos de nivel probablemente se utilicen ampliamente para muchas ofertas y en los próximos años, por lo que tiene sentido añadirlos. Cuando piense en qué atributos son necesarios para una oferta, evite añadir atributos que sean únicos para una campaña específica. Con el paso de los meses o años, este esquema puede sobrecargarse y causar problemas al crear ofertas. Verá cómo se aplica en la sección en la que creará ofertas.

## Resumen

Ha actualizado correctamente el esquema de ofertas estándar con campos personalizados reutilizables que se aprovecharán en partes posteriores del laboratorio al crear y evaluar ofertas.
