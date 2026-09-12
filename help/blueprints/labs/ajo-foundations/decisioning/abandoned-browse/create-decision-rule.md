---
title: Crear regla de decisión
description: Genere una regla de toma de decisiones que restrinja la elegibilidad para ofertas de teléfono premium a clientes con planes de nivel superior.
doc-type: article
solution: Experience Platform
exl-id: 1c1e2d82-ca09-4074-813d-3b29af77388b
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# Crear regla de decisión

## Objetivo

Dado que la idoneidad es uno de los componentes básicos clave de una oferta, el primer paso es crear las entidades necesarias para admitirla. En muchos casos, la pertenencia a audiencias es el factor decisivo, pero en este caso, utilizaremos Reglas de decisión. Con Connection 5G, los iPhone 17s de gama alta solo se pueden activar para usuarios con un plan de alto nivel. Como tal, usaremos una regla de decisión para garantizar que las ofertas para teléfonos de gama alta estén disponibles solo para aquellos con un plan lo suficientemente alto.

## Creación de la regla de decisión

1. Si es necesario, inicia sesión en Adobe Experience Cloud y navega a **Adobe Journey Optimizer.**
2. Expanda el elemento de menú **Decisioning** en el carril izquierdo si es necesario y haga clic en **Configuración de estrategia.**

   >[!WARNING]
   >
   >Asegúrese de que está en el menú Decisioning y NO en el menú Decision Management. Si se expande el menú Administración de decisiones, contráigalo para evitar confusiones de navegación durante este laboratorio.

3. Haga clic en **Reglas de decisión** en el menú &quot;Elegibilidad&quot;, seguido del botón **Crear regla** en la esquina superior derecha.

   ![Página Reglas de decisión con el botón Crear regla](assets/create-decision-rule-create-rule-button.png)

4. Se abrirá una pantalla similar a la interfaz de usuario del Generador de segmentos. Agregue el atributo de ID de plan al lienzo de reglas haciendo clic en **Perfil individual de XDM > DEP > Detalles del plan** y luego arrastrando el atributo **ID de plan** al lienzo.
5. Cambie el menú desplegable de igual a **contiene.**
6. Escriba el texto **2** en el cuadro, presione la tecla **Tab** para aceptar el valor 2 y, a continuación, escriba **3,** y presione **Tab** de nuevo para que la regla busque cualquier ID de plan que contenga un 2 o un 3
7. Utilice el cuadro de texto **Name** en el carril derecho para asignar un nombre a la regla de decisión **Planes de nivel superior**. Añada una descripción si lo desea. Cuando termine, la regla de decisión deberá tener este aspecto:

   ![Regla de decisión de planes de nivel superior completada con el identificador de plan que contiene 2 o 3](assets/create-decision-rule-upper-tier-plans-finished.png "Regla de decisión de planes de nivel superior completada con el identificador de plan que contiene 2 o 3")

8. Una vez que la regla sea correcta, haga clic en el botón azul **Crear** en la esquina superior derecha y volverá a la página Configuración de estrategia con la regla de decisión que acaba de crear enumerada como la única regla de decisión.

>[!NOTE]
>
>¿Por qué utilizar una regla de decisión en lugar de una audiencia? En la práctica, las razones principales serían que necesitaba criterios de idoneidad específicos para el paquete de decisiones o atributos de las ofertas en los criterios. Los atributos de oferta no están disponibles en el generador de audiencias.
>
>La regla de toma de decisiones de planes de nivel superior utilizada en este laboratorio probablemente sería una audiencia real en una implementación en la vida real, dada su probable reutilización fuera de Decisioning. Sin embargo, aquí se utilizó una regla de toma de decisiones con fines educativos y para mostrar su funcionalidad y las múltiples formas en que se puede aplicar la elegibilidad.

## Resumen

Ha creado una regla de decisión reutilizable, que utilizará para la idoneidad de la oferta.
