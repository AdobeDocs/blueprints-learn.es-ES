---
title: Crear propiedad
description: Cree una propiedad de reenvío de eventos con un elemento de datos y una regla que reenvíe eventos de experiencia entrantes a un extremo de gancho web.
doc-type: article
solution: Experience Platform
exl-id: eabd5f75-7706-4c96-982e-2512509bdc55
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---


# Crear propiedad

Normalmente, queremos reenviar un evento de experiencia a un tercero (aunque no tiene por qué serlo). Esto se utiliza generalmente cuando se necesita una copia de un evento en tiempo real para notificar a un tercero en circunstancias específicas (por ejemplo, notificar a Google, Meta o TikTok una compra).

>[!NOTE]
>
>Recordatorio: una propiedad contiene todas las extensiones, elementos de datos y reglas necesarias para decidir qué se reenvía y hacia dónde

1. En el carril izquierdo, haga clic en Reenvío de eventos
2. A continuación, haga clic en Nueva propiedad

   ![Sección de reenvío de eventos con el botón Nueva propiedad resaltado](assets/create-property-new-property-button.png "Cree una nueva propiedad de reenvío de eventos")

3. Actualice el nombre de la propiedad mediante la fórmula siguiente: `Event Forward Property SB + [sandbox number]`. El nombre final tendría este aspecto: **Propiedad de reenvío de eventos SB01**

4. Haga clic en **Guardar** cuando haya terminado

![El campo Nombre de propiedad de reenvío de eventos se completó con el botón Guardar resaltado](assets/create-property-name-property-form.png)

## Instalar extensión

1. Haga clic en la propiedad de reenvío de eventos que acaba de crear

   ![Lista de propiedades de reenvío de eventos con la propiedad recién creada resaltada](assets/create-property-open-new-property.png "Abra la propiedad de eventos")



2. Debería ver una pantalla como la siguiente.  Haz clic en **Extensiones**.

   ![Pantalla de información general sobre la propiedad de reenvío de eventos con la pestaña Extensiones resaltada](assets/create-property-click-extensions-tab.png)



3. Instale la extensión Adobe Cloud Connector haciendo lo siguiente:

4. Haz clic en **Catálogo** en la barra de navegación superior
5. Haga clic en la tarjeta **Conector de Adobe Cloud**
6. En el carril derecho, haga clic en el botón **Instalar**

![Catálogo de extensiones con la tarjeta Adobe Cloud Connector y el botón de instalación resaltados](assets/create-property-install-cloud-connector-extension.png)



Después de hacer clic en Instalar, debe ver la extensión debajo de Extensiones instaladas para su propiedad, como se muestra a continuación

![Lista de extensiones instaladas que muestra la extensión del conector de Adobe Cloud instalada correctamente](assets/create-property-extension-installed-confirmation.png "Extensión totalmente instalada")

## Crear elemento de datos

>[!NOTE]
>
>Un elemento de datos hace referencia al evento entrante y puede analizarlo en varios componentes individuales si es necesario

1. En el carril izquierdo, haga clic en **Elementos de datos**



   ![Navegación del carril izquierdo con el vínculo Elementos de datos resaltado](assets/create-property-navigate-to-data-elements.png "Vaya a los elementos de datos")



2. Haga clic en el botón **Crear nuevo elemento de datos**

   ![Página de elementos de datos con el botón Crear nuevo elemento de datos resaltado](assets/create-property-create-new-data-element-button.png "Crear nuevo elemento de datos")



3. Configure el nuevo elemento de datos con la siguiente información:

   | Tipo de elemento | Valor para configurar |
   | ----------------- | ------------------ |
   | Nombre | Objeto de datos |
   | Extensión | Núcleo |
   | Tipo de elemento de datos | Código personalizado |

   ![Configuración del elemento de datos con los campos Nombre, Extensión y Tipo de elemento de datos establecidos](assets/create-property-data-element-config-step-1.png "Paso 1 de la configuración del elemento de datos")



4. Haga clic en el botón **Abrir editor** para agregar el siguiente código personalizado:

   ![Configuración del elemento de datos con el botón Abrir editor resaltado para el código personalizado](assets/create-property-open-custom-code-editor.png "Abrir el editor")



5. Agregue código personalizado al editor como tal y guárdelo

   ```none
   var xdm = arc?.event || '';
   return xdm;
   ```

   ![Editor de código personalizado que muestra el script que devuelve el objeto de evento XDM entrante](assets/create-property-custom-code-added.png "Código personalizado")

   >[!NOTE]
   >
   >Esto captura todo el objeto xdm sin hacer ninguna traducción a la carga útil.  Si es necesario, podríamos analizar cada fragmento individual dentro del objeto XDM (por ejemplo, nombre de página, cantidad de compra) en un elemento de datos por campo.  La razón para hacerlo podría ser si hay una transformación de la estructura a una estructura diferente





6. Haga clic en el botón **Guardar** para guardar el elemento de datos.

![Editor de elementos de datos con el botón Guardar resaltado](assets/create-property-save-data-element-button.png)



Cuando haya terminado, debería ver la siguiente pantalla que confirma que se ha agregado el elemento de datos:

![Lista de elementos de datos que muestra el elemento de datos recién guardado que se agregó a la propiedad](assets/create-property-data-element-saved-confirmation.png)


## Creación de reglas

>[!NOTE]
>
>Una regla contiene:
>
>1. Condiciones sobre qué reenviar
>2. Acciones que pueden transformar la carga útil y definir adónde enviarla



1. En el carril izquierdo, haga clic en **Reglas**

   ![Navegación del carril izquierdo con el vínculo Reglas resaltado](assets/create-property-navigate-to-rules.png)



2. Luego haz clic en **Crear nueva regla**

   ![Página de reglas con el botón Crear nueva regla resaltado](assets/create-property-new-rule-button.png)



3. Actualice el nombre de la regla con la fórmula siguiente: `"EF Rule SB" + [your sandbox number]` (es decir, la regla EF SB01). Puede encontrar el número de la zona protegida en la parte superior derecha de la ventana del explorador, como se muestra a continuación\...

   ![Esquina superior derecha de la ventana del explorador que muestra el número de zona protegida utilizado en el nombre de regla](assets/create-property-sandbox-number-location.png)

4. Haga clic en **Guardar** cuando haya terminado

   >[!NOTE]
   >
   >Asegúrese de que el nombre de la regla sigue el patrón de fórmula de `"EF Rule SB" + [sandbox number]`

   ![Campo de nombre de regla completado con el patrón de nomenclatura de la zona protegida de reglas EF](assets/create-property-add-rule-name.png "Agregar nombre a la regla")



5. Añada una acción a la regla haciendo clic en el signo (+) para añadir una nueva acción

![Editor de reglas con el icono más resaltado para agregar una nueva acción](assets/create-property-add-action-button.png "Agregar una acción")

## Obtener URL del webhook (para usar en acción)

>[!NOTE]
>
>Este laboratorio utiliza un webhook para que puedas ver si los datos han llegado al destino al que los estás enviando. En un escenario del mundo real, debería iniciar sesión en ese destino y utilizar sus herramientas para ver lo que ha llegado.



1. Abra el siguiente vínculo en una nueva pestaña del explorador -> [https://webhook.site](https://webhook.site/)
2. Copie la dirección URL única que ve y guárdela en un lugar seguro

   ![Página webhook.site con la dirección URL única resaltada para copiar](assets/create-property-webhooksite-copy-url.png)



3. Configure la acción con la siguiente información:

| Configuración | Valor |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Extensión | Conector de Adobe Cloud |
| Tipo de acción | Hacer llamada de recuperación |
| Método | Publicar |
| URL | Utilice la misma URL de webhook que utilizó al configurar el destino de streaming. Puede encontrarlo abriendo una nueva pestaña en el navegador y navegando hasta Destinos -> Examinar |
| Cuerpo | Raw |
| Datos del cuerpo | \{ &quot;data&quot;: \{ &quot;event&quot;: &quot;\{\{Data Object\}\}&quot; } } |

>[!NOTE]
>
>Aquí se hace referencia al \{\{Data Object\}\} que es el elemento de datos que ha creado anteriormente. En este caso, el requisito del sistema descendente era que deseara envolver el evento en un objeto de datos con un objeto de evento. Puede poner cualquier formato aquí.
>
>Si hubiéramos dividido \{\{Data Object\}\} en varios campos (por ejemplo, nombre de página, compra, etc.), podríamos transformar la estructura JSON colocando cada campo en el lugar deseado, lo que nos daría más control sobre la coincidencia del destino.





Cuando termine, valide la pantalla que se parece a la que se muestra a continuación y haga clic en **Conservar cambios**

![Acción de regla configurada con el conector de Adobe Cloud para realizar la configuración de llamada de recuperación y la URL del gancho web](assets/create-property-configure-action-settings.png "Configurar la acción")



&#x200B;4. Cuando termine, debería ver la acción agregada a la regla. Haga clic en **Guardar** para continuar.

![Editor de reglas que muestra la acción configurada con el botón Guardar resaltado](assets/create-property-save-rule-button.png "Guarde la regla")

>[!WARNING]
>
>Al enviar un evento de experiencia, está enviando el evento, no el perfil, ni ninguno de sus atributos, incluidas las cualificaciones de audiencia (aunque se trate de una audiencia de Edge).
>
>Esto sucede por motivos de velocidad.



## Publicación de los cambios

1. En el carril izquierdo, haga clic en **Flujo de publicación**

   ![Navegación del carril izquierdo con el vínculo Flujo de publicación resaltado](assets/create-property-navigate-to-publishing-flow.png "Vaya al Flujo de publicación")



2. Haga clic en el botón **Agregar biblioteca**

   ![Página de flujo de publicación con el botón Agregar biblioteca resaltado](assets/create-property-add-library-button.png "Agregar biblioteca")



3. Configure la biblioteca con la siguiente información:

   - Nombre -> **Biblioteca EF**
   - Entorno -> **Desarrollo**
   - Haz clic en **Añadir todos los recursos modificados**


   Cuando termine, la pantalla debería ser similar a la de abajo.  Si todo parece correcto, haga clic en el botón **Guardar y generar en desarrollo**

   ![Configuración de la biblioteca con nombre, entorno de desarrollo y botón Guardar y generar en desarrollo](assets/create-property-configure-library-save-and-build.png)



4. Luego debería ver que la compilación de desarrollo se vuelve verde indicando que está lista para usarse

![Flujo de publicación que muestra el estado de compilación de desarrollo cambiado a verde y listo para usar](assets/create-property-development-build-ready.png)
