---
title: Generar
description: Cree una audiencia de visitantes de la página de productos de iPhone 14 y combínela con otras audiencias mediante audiencias de audiencia de para habilitar la activación de streaming.
doc-type: article
solution: Experience Platform
exl-id: 999f9a20-1655-4eab-a796-a19d69a06879
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# Generar #3 de audiencia

## Objetivo del laboratorio

Crear una audiencia que haya visitado una página de producto de iPhone 14



## Tareas de análisis

Esta audiencia debe ser directa.  Es posible que tengamos varias páginas de productos, pero nada complicado aquí.



## Crear una audiencia (visitó cualquier página)

1. Busque el evento Vista de página en la pestaña Evento en Tipos de evento en el carril izquierdo y añada a la Audiencia

   ![Busque el evento Vista de página en Tipos de evento en el carril izquierdo](assets/build-audience-3-find-page-view-event.png)

   >[!NOTE]
   >
   >**Usando tipos de eventos**
   >
   >Con el evento de vista de página nos aseguramos de que la audiencia solo evalúe el nombre de la página en el contexto de una vista de página. Debería ser redundante, ya que el nombre de página solo existe en una vista de página, pero ofrece dos ventajas:
   >
   >- Proporciona documentación visual de alto nivel al usuario cuando busca en la interfaz de usuario
   >- Proporciona filtrado para garantizar que, a medida que se añaden nuevos eventos, no se incluyan cuando esa no era la intención
   >
   >Por este motivo, recomendamos que cada Esquema de evento que cree tenga mucho en cuenta los Tipos de evento que utilice. Son fundamentales para el filtrado y las guías visuales.



2. Proporcione una descripción y conviértala en Streaming.

3. Sobre el evento Colocado, cambie &quot;En cualquier momento&quot; a &quot;Hoy&quot;

   ![Cambiar el filtro de tiempo de evento de Cualquier hora a Hoy](assets/build-audience-1-change-any-time-to-today.png)

4. Guardar esta audiencia como &quot;*Visitó cualquier página*&quot;

5. Haga clic en el botón azul **Activar audiencia** al destino

6. Seleccione el destino **Streaming DEP Webhook** y haga clic en Siguiente

7. Haga clic en Next y Finish

## Crear una audiencia (visitó la página 14 de iPhone, pero no la posee ni la solicitó)

1. Crear una audiencia nueva y añadir el evento de vistas de página

   ![Crear una audiencia nueva y agregar el evento de vistas de página](assets/build-audience-3-create-a-new-audience-and-add-the-page-views-event.png)



2. Vaya a donde está Nombre de página y añada el campo Nombre de página al Evento para que podamos filtrar.

   - ExperienceEvent de XDM —> Web —> Detalles de página web —> Nombre

   ![Vaya a XDM ExperienceEvent > Web > Detalles de página web > Nombre](assets/build-audience-3-navigate-to-page-name-field.png)



3. Añadir contiene &quot;iPhone 14&quot;

   ![Agregar una condición contiene para &quot;iPhone 14&quot;](assets/build-audience-3-add-contains-iphone-14.png)

   >[!TIP]
   >
   >**Buscando &quot;Página&quot;**
   >
   >En lugar de navegar al campo, intente buscar &quot;Página&quot;
   >
   >Verá que Nombre de página no aparece. Esto se debe a su nombre:
   >
   >- ExperienceEvent de XDM > Web > Detalles de página web > Nombre
   >
   >Por lo tanto, la carpeta aparecerá, pero no el campo en sí. Cuando reúna las convenciones de nomenclatura, tenga en cuenta este y otros términos comunes que las personas pueden buscar e incorporarlos en su nomenclatura.
   >
   >La búsqueda no busca descripciones
   >
   >![Al buscar &quot;Página&quot;, no aparece el campo Nombre de página](assets/build-audience-3-searching-for-page-does-not-find-field.png)



4. Sobre el evento Colocado, cambie &quot;En cualquier momento&quot; a &quot;Hoy&quot;

   ![Cambiar el filtro de tiempo de evento de Cualquier hora a Hoy](assets/build-audience-1-change-any-time-to-today.png)

   >[!NOTE]
   >
   >Dado que la activamos en función de los eventos que se produjeron hoy, solo nos centramos en las vistas de página de hoy.



5. Valide que esto sea un flujo y proporcione una descripción.

6. Guardar audiencia como &quot;*Página visitada de iPhone 14*&quot;

   ![Guardar la audiencia como &quot;Página visitada de iPhone 14&quot;](assets/build-audience-3-save-audience-as-visited-iphone-14-page.png)



7. Haga clic en el botón azul **Activar audiencia** al destino

8. Seleccione el destino **Streaming DEP Webhook** y haga clic en Siguiente

9. Haga clic en Next y Finish



## Crear una audiencia de audiencias

1. Vaya a la pestaña Audiencias en la barra de navegación superior izquierda
1. Explorar en profundidad Experience Platform
1. Incorporar las otras tres audiencias que hemos creado anteriormente
1. Cambie Incluir a No incluye para Propietarios iPhone 14 y Pedido Realizado iPhone 14.

   ![Establecer iPhone 14 en propiedad y iPhone 14 con pedido realizado en No incluye en la audiencia de audiencias](assets/build-audience-3-audience-of-audiences-does-not-include.png)



&#x200B;5. Proporcione una descripción.

&#x200B;6. Cambio en streaming

&#x200B;7. Guardar como &quot;*Página de iPhone 14 visitada pero no perteneciente/solicitada*&quot;

&#x200B;8. Haga clic en el botón azul **Activar audiencia** al destino

&#x200B;9. Seleccione el destino **Streaming DEP Webhook** y haga clic en Siguiente

&#x200B;10. Haga clic en Next y Finish

>[!NOTE]
>
>**Filtro de tiempo**
>
>Los requisitos no tenían requisitos de tiempo, por lo que si alguien visitaba hace tres años, calificaría. Según nuestro caso de uso, eso puede funcionar o no. Vale la pena preguntar. Añadimos uno porque lo estamos activando en función de las personas que visitaron nuestro sitio web hoy.  Es posible que no funcione en todos los casos de uso.  Si añadimos un filtro de tiempo, ¿hasta dónde podemos retroceder antes de que una audiencia de Edge se convierta en streaming o incluso en lote?

>[!NOTE]
>
>**Consecuencias de romper esto**
>
>Hemos dividido lo que es un requisito simple en muchas audiencias por varias razones. El requisito es una transmisión, pero estos dos requisitos convierten nuestra audiencia en lote. Obtenga más información aquí sobre las reglas de elegibilidad de streaming aquí:
>
>[https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html?lang=es](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html?lang=es)

>[!NOTE]
>
>**Qué son las audiencias de streaming de audiencias**
>
>Nuestro blog *Echando un vistazo bajo el capó de la audiencia* (enlace abajo), habla un poco sobre esto a continuación. Muestra cómo se almacena el resultado de una audiencia en el perfil. Esto es importante, ya que, como los flujos de datos en ellos miran los resultados de una audiencia almacenada en el perfil, no se vuelve a ejecutar la audiencia en ese momento. Un simple matiz pero que vale la pena entender. La mayoría de los atributos de perfil se actualizan periódicamente, por lo que este enfoque tiene sentido.
>
>Debemos comprender que, cuando se utiliza una audiencia dentro de una audiencia, AEP intentará realizar la secuencia cuando sea posible. Hay casos extremos en los que esto no es posible, por ejemplo, Si se utiliza una Audiencia de audiencias, la descalificación de perfiles se producirá cada 24 horas.
>
>[https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-blogs/peeking-underneath-the-hood-of-segments-in-aep-adobe-experience/ba-p/453535?profile.language=es](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-blogs/peeking-underneath-the-hood-of-segments-in-aep-adobe-experience/ba-p/453535?profile.language=es)



## ¿Por qué crear varias audiencias?

Si hubiéramos creado todas estas audiencias en una audiencia en lugar de en cuatro, obtendríamos un método de evaluación por lotes aunque cada audiencia individualmente sea de streaming.

![Al crear una audiencia combinada se evalúa el lote en lugar de la transmisión](assets/build-audience-3-why-are-we-creating-multiple-audiences.png)



Al desglosar estas audiencias y usar una audiencia de audiencias, obtenemos este comportamiento.  Calificación en tiempo real de estas audiencias como flujos de datos en

- IPhone 14 solicitado
- Es propietario de iPhone 14
- Página de iPhone 14 visitada

>[!WARNING]
>
>Hoy en día hay una descalificación de audiencias de latencia diaria/de 24 horas



En resumen: negociamos una entrada más rápida en la Audiencia dividiéndola en partes con una latencia de 24 horas de que salieran de la Audiencia.

>[!TIP]
>
>**Laboratorio de desafío opcional**
>
>¿Terminaste temprano?
>
>Quiero apuntar a la gente con un correo electrónico si tienen un teléfono viejo.  Crear una audiencia de &quot;Tiene teléfono antiguo&quot;.  ¿Cómo podemos dirigirnos a ellos?
