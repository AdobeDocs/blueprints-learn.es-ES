---
title: Crear colección de ofertas
description: Agrupe los elementos de oferta relacionados en una colección mediante reglas basadas en atributos para que se puedan evaluar juntos mediante una estrategia de selección.
doc-type: article
solution: Experience Platform
exl-id: 0a54f4dc-2112-474a-8383-9dd1497c3c74
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Crear colección de ofertas

## Objetivo

Ahora que se han creado las ofertas, deben organizarse en una colección. Una colección tiene uno o más elementos de oferta, y un elemento de oferta puede estar en más de una colección.

## Creación de la colección de ofertas de iPhone

1. Si es necesario, expanda **Decisioning** en el carril izquierdo y luego haga clic en **Catálogos**. Verá las cuatro ofertas que creó en la sección anterior.
2. Haga clic en **Colecciones** que acaba de salir del nombre de la oferta

   ![Pestaña Colecciones en la página Catálogos](assets/create-offer-collection-collections-tab.png)

3. Haga clic en la colección azul **Crear colección** para crear la nueva colección.
4. Asigne un nombre a la colección **iPhone 17 Collection**
5. En la sección &quot;Reglas de recopilación&quot;, haga clic en el cuadro de texto que contiene el texto **_Haga clic para crear un elemento de decisión_**. Una vez que se haga clic en, aparecerán las opciones para crear la regla.

   ![Cuadro de texto de regla de recopilación abierto para crear un elemento de decisión](assets/create-offer-collection-create-decision-item.png)

6. Haga clic en el botón **Seleccionar atributo** y, a continuación, desplácese por el esquema del elemento de oferta haciendo clic en **Dispositivo > Crear**. Haga clic en **Guardar,** y verá que el atributo &#39;Hacer&#39; está ahora en la regla de decisión.

   Se agregó el atributo ![Device Make a la regla de recopilación](assets/create-offer-collection-select-make-attribute.png)

   >[!NOTE]
   >
   >Tenga en cuenta que las opciones disponibles son los mismos campos configurables que utilizó al crear los elementos de oferta. Dado que una colección es una agrupación de elementos de oferta, tiene sentido que las reglas para agruparlos dependan de sus atributos.

7. Deje el operador &quot;Es igual que&quot; en su lugar e introduzca el texto **iPhone** en el campo de valor, y verá que el número de elementos cambia a 4, lo que indica que todos los elementos de la oferta cumplen con ese criterio

   ![Regla de recopilación que muestra cuatro elementos de oferta que coinciden con los criterios de iPhone](assets/create-offer-collection-four-matching-offers.png)

   >[!NOTE]
   >
   >También puede hacer clic en el botón **Vista previa de la colección** y ver los elementos de oferta que cumplen los criterios.

8. Con los cuatro elementos de oferta seleccionados, haz clic en el botón azul **Crear**. Esto le lleva a una página que muestra la colección recién creada.

![Página de recopilación de iPhone 17 recién creada](assets/create-offer-collection-created-collection-page.png)

>[!NOTE]
>
>Una colección es más que un simple medio de organización. En los pasos siguientes, verá que en Decisioning, aplicamos lógica de selección a una colección de ofertas. Si pensamos en una implementación de tamaño empresarial, no es difícil imaginar cuántas ofertas se crearían con los años de uso. Con el fin de determinar qué ofertas debe aplicarse una estrategia de selección, saca a la luz lo importante que es una gestión adecuada de la colección.
>
>En este caso, una colección con solo &quot;iPhone&quot; como criterio incluiría demasiadas ofertas después de unos años de lanzamientos de iPhone. Podríamos haber utilizado criterios adicionales como &quot;Hacer igual a 17&quot; o haber utilizado etiquetas de AEP para etiquetar ofertas para una campaña específica. Pero para simplificar, estamos usando esta lógica simple para crear una colección.

## Resumen

Ahora ha creado una colección de ofertas que agrupa los elementos de ofertas creados anteriormente. Ha añadido todas las ofertas de iPhone 17 a una colección y ha definido una regla basada en atributos de oferta (como marca de dispositivo) para que solo las ofertas relevantes pertenezcan a esta colección.
