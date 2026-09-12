---
title: Crear un canal de experiencia basado en código
description: Configure un canal de experiencia basado en código en Adobe Journey Optimizer que devuelva datos de ofertas JSON a cualquier sistema web, móvil o de IoT que solicite una decisión.
doc-type: article
solution: Experience Platform
exl-id: c3353d3d-cd97-46b7-8ef8-c72fa9e7dfe5
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---


# Crear un canal de experiencia basado en código

## Objetivo

Recuerde que los requisitos comerciales son que cualquiera de los sistemas de Connection 5G debe poder devolver una oferta adecuada. Ya sea el equipo de un agente de cliente, un quiosco en la tienda, una aplicación móvil o el sitio web, el cliente debe recibir la misma experiencia de oferta. El único canal de AJO que puede hacerlo es una experiencia basada en código (CBE), uno de los canales de AJO entrantes. Aunque un CBE puede devolver HTML, su función principal es devolver información sobre qué oferta debe presentarse al sistema receptor, sabiendo ese sistema qué hacer con esa información de oferta. A diferencia del canal Web, los CBE no se representan ni registran automáticamente. Aunque es un poco más de trabajo manual para el cliente, ofrecen mucha flexibilidad, ya que se pueden configurar para devolver JSON que cualquier sistema móvil, web o IoT puede utilizar para ejecutar decisiones.

1. Si es necesario, expanda el elemento de menú **Administración** en el carril izquierdo (probablemente necesite desplazarse hacia abajo) y haga clic en **Canales**. Aterrizará en la página &quot;Configuraciones de canal&quot;.
2. Haga clic en el botón azul **Crear configuración de canal**
3. En la página &quot;Detalles de configuración del canal&quot;, asigne un nombre al canal **jsonOffer\_cbe**

   >[!NOTE]
   >
   >Dado que cualquier número de clientes puede llamar a un CBE en *N* número de plataformas, vamos a nombrar este CBE como algo genérico para la ubicación, pero específico para el hecho de que devuelve ofertas en formato JSON.

4. Establezca el menú desplegable **Seleccionar canal** en **Experiencia basada en código.**

   >[!WARNING]
   >
   >No estableceremos una acción de marketing en este laboratorio porque añada una complejidad innecesaria a nuestra demostración, pero como se puede acceder a los CBE desde varios sistemas, en un caso de uso real debe establecer todas las acciones de marketing posibles para este canal para que se apliquen las etiquetas DULE.

5. Marque la casilla **Web** en el área &quot;Configuración de experiencia basada en código&quot; y mantenga seleccionada la opción **Una sola página**.
6. En el cuadro de texto **Dirección URL de la página**, escriba el texto `https://connection5g.com/home`
7. En el cuadro de texto **Ubicación en la página**, escriba el texto **jsonOfferContainer**

   >[!NOTE]
   >
   >No todos los eventos de experiencia enviados a los déclencheur de Edge son solicitudes de ofertas personalizadas. Creará un Recorrido en la siguiente sección en el que se configurará este CBE con la estrategia de selección que acaba de configurar. La configuración &quot;Ubicación en la página&quot; es el nombre del parámetro que se pasa en los eventos de experiencia y que indica a Experience Edge que devuelva todas las ofertas asignadas a ese CBE. También se conoce a menudo como superficie. Ya sea una aplicación móvil, una página web o cualquier otro dispositivo de IoT, si el valor jsonOfferContainer se pasa a Edge, junto con el eventType correcto a través de un evento de experiencia, Edge ejecutará la lógica configurada hasta ahora en el laboratorio y devolverá la oferta adecuada.

8. Haga clic en el botón de opción **JSON** de la sección &#39;Formato&#39;. Cuando termine, la configuración del canal CBE debería tener este aspecto:

   ![Configuración de canal de experiencia basada en código completada con formato JSON seleccionado](assets/create-code-based-experience-channel-completed-config.png)

9. Una vez que todo parezca correcto, haga clic en el botón azul **Enviar** en la esquina superior derecha.

>[!TIP]
>
>Una vez guardado, se le redirigirá a la página de configuración del canal y verá el CBE recién creado.

## Resumen

En esta página, ha configurado un canal de experiencia basada en código (CBE) y un nuevo canal entrante que puede devolver decisiones de oferta en formato JSON para que sistemas externos (como páginas web, aplicaciones o quioscos) puedan solicitar y recibir las ofertas adecuadas en función de la estrategia de selección creada anteriormente.
