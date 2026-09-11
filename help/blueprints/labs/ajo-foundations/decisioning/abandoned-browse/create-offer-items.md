---
title: Creación de elementos de oferta
description: Cree elementos de ofertas de iPhone por niveles con prioridades, reglas de elegibilidad y límites de frecuencia para usarlos en un paquete de decisiones.
doc-type: article
solution: Experience Platform
exl-id: 76214d87-5107-4829-9d6e-91073e1008ca
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---


# Creación de elementos de oferta

## Objetivo

En esta sección, creará los elementos de oferta reales que la experiencia basada en código (CBE) devolverá al cliente solicitante. Algunos de los elementos de la oferta tendrán requisitos de idoneidad y límite de frecuencia, mientras que otros no.

## Información general del escenario

Sin embargo, antes de crear los elementos de oferta, he aquí algunos recordatorios rápidos sobre nuestro escenario. En primer lugar, hay 3 niveles de iPhone 17 en nuestro escenario: Ultra, Pro y Base. Puede crear 4 ofertas totales, 1 para cada nivel, además de una oferta de reserva genérica que el sistema receptor puede utilizar para mostrar información general acerca de iPhone 17 en todos los niveles.

En segundo lugar, solo los clientes con un ID de plan de 2 o 3 son elegibles para los teléfonos de nivel Ultra y Pro.

A continuación, la empresa ha solicitado que cada oferta se muestre solo tres veces al día antes de que se presente el siguiente teléfono de nivel inferior.

Por último, en igualdad de condiciones, Connection 5G preferiría vender el Ultra tier, seguido del Pro, y luego el modelo base. De este modo, verá que estas prioridades aparecen cuando asigne una puntuación de prioridad a cada elemento de oferta.

## Crear elemento de oferta predeterminado/de reserva

El primer y más fácil elemento de oferta que crea es la oferta de reserva, que cualquier persona puede ver durante un período ilimitado.

1. Si es necesario, expanda **Decisioning** en el carril izquierdo y haga clic en **Catálogos**
2. Se muestra una página de ofertas vacía:

   ![Vacíe la página del catálogo de ofertas antes de crear cualquier elemento de oferta](assets/create-offer-items-empty-offers-page.png)

3. Haga clic en el botón azul **Crear elemento**. Se abrirá la página &quot;Crear elemento de oferta&quot;.
4. En el campo &quot;Nombre de oferta&quot;, escriba el texto **iphone:17\:generic**. Escriba una descripción si lo desea.

   >[!NOTE]
   >
   >La convención de nombres en minúsculas y separados por dos puntos es solo uno de nuestros propios diseños que podría servir como uno a seguir para un cliente real. En la práctica, puede desarrollar una estrategia de nomenclatura diferente para los elementos de oferta. Asegúrese de que esté documentado y sea coherente antes de crear elementos de oferta. Esto garantizará que los elementos de oferta sean fáciles de encontrar y agrupar en colecciones. Más información más adelante.

5. Dado que este es el elemento de oferta de prioridad más baja/predeterminado, deje la prioridad predeterminada en 1.

   >[!NOTE]
   >
   >En Decisioning, cuanto menor sea el número, menor será la prioridad. Por ejemplo, se muestra un elemento de oferta con una prioridad de 100 antes de un elemento de oferta con una prioridad de 1

6. Expanda el elemento **Dispositivo** en el área &#39;Atributos personalizados&#39; y, a continuación, escriba la siguiente información en los cuadros de texto:
   - Nivel: **Genérico**
   - Modelo: **17**
   - Marca: **iPhone**

   Estos son los valores de texto reales que describen la oferta y lo que se puede utilizar en la ordenación, la clasificación y los criterios de idoneidad. También son los valores de texto que se pueden devolver al dispositivo solicitante.

   ![Atributos del dispositivo para la oferta genérica establecida en Nivel genérico, Modelo 17, Convertir en iPhone](assets/create-offer-items-generic-device-attributes.png)

   >[!NOTE]
   >
   >El área de Dispositivo que ha expandido es el mismo objeto principal &quot;Dispositivo&quot; que se creó cuando el esquema &quot;Elementos de oferta personalizados: Experience Decisioning&quot; se actualizó con atributos personalizados en la sección anterior. Los campos Nivel, Modelo y Crear son los atributos individuales que se agregaron:
   >
   >![Objeto principal del dispositivo que muestra los campos de nivel, modelo y atributo Make](assets/create-offer-items-device-attribute-fields.png)

   >[!WARNING]
   >
   >En la sección anterior se mencionó la necesidad de tener mucho cuidado al añadir atributos personalizados al esquema generado por el sistema &quot;Elementos de oferta personalizados: Experience Decisioning&quot;. Cada nodo personalizado adicional aparecerá como un campo posible para cada elemento de oferta en adelante. La creación de atributos innecesarios o específicos de la campaña saturará la interfaz de usuario de creación de elementos de oferta y puede causar confusión.

7. Haga clic en el botón **Siguiente** azul en la esquina superior derecha para pasar al siguiente paso.
8. Esta oferta debe estar disponible para todos/Todos los visitantes y no tener ningún límite de frecuencia, por lo que no es necesario realizar cambios en las secciones &quot;Elegibilidad&quot; o &quot;Límite&quot;. Vuelva a hacer clic en el botón azul **Siguiente** para continuar con el último paso.
9. En el paso &quot;Revisar&quot;, compruebe que todos los datos son correctos:

   ![Revise el paso que confirma los detalles del elemento de oferta genérico antes de guardar](assets/create-offer-items-generic-offer-review-step.png "Revise el paso que confirma los detalles del elemento de oferta genérico antes de guardar")

10. Realice los cambios necesarios. Cuando esté listo, haga clic en el botón azul **Guardar**.
11. Una vez guardado, aparece un botón blanco &quot;Aprobar&quot; donde solía estar el botón &quot;Guardar&quot;. Haga clic en el botón **Aprobar** en blanco para aprobar este elemento de oferta. Verá un indicador verde &quot;Aprobado&quot; debajo del título del elemento de oferta:

![Indicador de aprobación verde en el elemento de oferta genérico](assets/create-offer-items-generic-offer-approved.png)

>[!NOTE]
>
>En la práctica, y con ofertas más complejas, debe existir un proceso de aprobación adecuado para garantizar que los elementos de la oferta se hayan creado correctamente. Para ahorrar tiempo en este laboratorio, solo tiene que aprobar cada elemento de oferta que cree.

12. Haga clic en la **flecha izquierda** junto al título del elemento de oferta para volver a la página &quot;Ofertas&quot; y verá su oferta iphone:17\:generic en la lista.

## Crear elemento de oferta del modelo base

Ahora que se ha creado el elemento de oferta genérico, puede crear el siguiente elemento de oferta prioritario para el modelo base de iPhone 17.

1. Vuelva a hacer clic en el botón azul **Crear elemento** y asigne un nombre a la oferta **iphone:17\:base**
2. Dado que este es el siguiente elemento de oferta de prioridad más baja, aumente el campo **Prioridad** a **2**
3. Expanda el área **Dispositivo** y proporcione a los campos estos valores:
   - Nivel: **Base**
   - Modelo: **17**
   - Marca: **iPhone**

   Cuando termine, el elemento de oferta tendrá este aspecto (se agrega el cuadro rojo para garantizar que la prioridad sea correcta):

   ![Elemento de oferta del modelo base que muestra la prioridad establecida en 2](assets/create-offer-items-base-offer-priority.png)

   Cuando todo esté correcto, haga clic en el botón azul **Siguiente** para continuar con el paso siguiente.

4. Este artículo de oferta debe estar disponible para todos, por lo que no hay requisito de elegibilidad; sin embargo, debe estar limitado a 3 impresiones por día. Haga clic en el botón &#39;**+ Crear límite&#39;**.
5. En la nueva regla de límite, cambie **Elegir evento de límite** a **Impresión.**
6. Cambie **Capping event count** a **3**. Una vez finalizada, la regla de límite tiene este aspecto:

   ![Regla de límite para la oferta base establecida en 3 impresiones](assets/create-offer-items-base-offer-capping-rule.png)

   Una vez que sea correcto, haga clic en el botón azul **Crear** para guardar la regla de límite.

   >[!NOTE]
   >
   >Observe cómo podría crear una regla de límite adicional. En la práctica, es posible que desee agregar más de una regla. En este caso, podríamos haber agregado una regla para limitar esto si se viera un evento específico, como un evento de compra. Este laboratorio lo mantiene simple con una sola regla de límite.
   >
   >![Ejemplo de una regla de límite adicional basada en un evento de compra](assets/create-offer-items-additional-capping-rule-example.png)

   >[!NOTE]
   >
   >Los &quot;días&quot; mencionados en las reglas de límite de frecuencia se refieren a días en la zona horaria GMT.  El límite de frecuencia con días en la lógica se restablece a medianoche (GMT).

7. Haga clic en **Siguiente** para continuar con el paso de revisión.
8. Asegúrese de que todo aparece según lo esperado y haga clic en el botón **Guardar**. Una vez guardado, haga clic en **Aprobar.**
9. Una vez aprobada, haga clic en la flecha izquierda junto al título y vuelva a la página de ofertas. Ahora verá dos ofertas, cada una con la prioridad adecuada.

![La página de ofertas enumera los artículos de ofertas genéricos y base con sus prioridades](assets/create-offer-items-first-two-offers-priority.png)

## Crear elementos de oferta del modelo de nivel superior

Ahora que se han creado las ofertas del modelo genérico y base, puede pasar a los elementos de oferta para los modelos pro y ultra. Estos elementos de oferta también deben incluir un elemento de idoneidad, ya que solamente los miembros con un determinado nivel de plan deben ver estas ofertas.

1. Siguiendo los mismos pasos y patrones de nomenclatura descritos en las secciones anteriores, cree una nueva oferta llamada **iphone:17\:pro** y establezca su prioridad en **3.**
2. Establece el atributo **Tier** en **Pro** y los demás atributos personalizados como lo hiciste en las otras ofertas.
3. En el paso &quot;Elegibilidad&quot;, seleccione el botón de opción **Por regla**.
4. El carril izquierdo muestra solo una regla de Decisión, la creada anteriormente denominada &quot;Planes de nivel superior&quot;. Haga clic en el icono **+** junto a esa regla para agregarla al lienzo.
5. Como se mencionó anteriormente, el negocio ha declarado que las ofertas de no reserva deben tener un límite de frecuencia de 3 pantallas (o impresiones) por día. Siga los pasos de la sección anterior para crear una regla de límite para 3 impresiones al día. Cuando termine, la página tendrá este aspecto:

   ![Pro ofrece elegibilidad para el artículo y configuración de límite para 3 impresiones por día](assets/create-offer-items-pro-offer-eligibility-capping.png)

6. Una vez que hayas verificado que todo es correcto, haz clic en **Siguiente**. La configuración final del elemento de oferta tiene este aspecto:

   ![Configuración completada para el elemento de oferta de nivel Pro](assets/create-offer-items-pro-offer-final-config.png)

7. Una vez que todo parezca correcto, **guarda** y **aprueba** el elemento de oferta.
8. Vuelva a la página de ofertas y compruebe que las 3 ofertas están presentes y que cada una tiene la prioridad adecuada.
9. Cree el elemento de oferta final y asígnele el nombre **iphone:17\:ultra,**. Asígnele una prioridad de **4,** y establezca los demás atributos personalizados con los mismos valores que las otras ofertas.
10. Al igual que con el último elemento de oferta, establezca la idoneidad para la regla de decisión &quot;Planes de nivel superior&quot; y establezca un límite de frecuencia de 3 impresiones al día. Cuando finalice, el elemento de oferta tendrá este aspecto:

![Configuración completada para el elemento de oferta de nivel Ultra](assets/create-offer-items-ultra-offer-final-config.png)

11. Una vez que haya comprobado que todas las configuraciones son correctas, guarde y apruebe este elemento de oferta. Ahora verá los cuatro elementos de oferta, cada uno con una prioridad única.

![La página de ofertas enumera los cuatro artículos de oferta con prioridades únicas](assets/create-offer-items-all-four-offers-priority.png)

>[!NOTE]
>
>Las instrucciones de este laboratorio son enfáticas en cuanto a garantizar que las prioridades sean diferentes para cada elemento de oferta. En este caso de uso sencillo, es importante, pero no hay nada en la interfaz de usuario que le obligue a dar a cada elemento de oferta una prioridad única. Con el tiempo, es probable que tenga varias ofertas de artículos con la misma prioridad. Verá por qué es importante comprender esto en secciones posteriores.

## Resumen

Ha definido varias ofertas para los diferentes niveles de iPhone 17, incluida una oferta de reserva genérica y ofertas específicas de los niveles (base, pro y ultra). También ha aprobado los cuatro elementos de oferta con las prioridades, los requisitos y la configuración de límite de impresión correctos para que estén listos para su uso en el paquete de decisiones.
