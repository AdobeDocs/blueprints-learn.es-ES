---
title: Monitorice su evento
description: Utilice Adobe Experience Platform Assurance para crear una sesión de depuración, enviar un evento validado a través de Postman e inspeccionar los registros de procesamiento de eventos Edge.
doc-type: article
solution: Experience Platform
exl-id: 94b200c0-6714-4996-a266-119cc8f7f4e2
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---


# Monitorice su evento

## Navegar a Assurance

[Adobe Experience Platform Assurance](https://experienceleague.adobe.com/es/docs/experience-platform/assurance/home) es un producto de Adobe Experience Cloud que le ayudará a inspeccionar, probar, simular y validar la forma en que recopila datos en Adobe Experience Platform Edge.

1. Vaya a Adobe Experience Platform -> Assurance -> Crear sesión

   ![Vaya a Adobe Experience Platform Assurance y cree una sesión](assets/monitor-your-event-navigate-to-assurance-create-session.png)



2. Haz clic en el botón **Iniciar**

![Haga clic en el botón Inicio para comenzar a configurar la sesión de Assurance](assets/monitor-your-event-click-start-button.png)



## Configuración de una sesión

1. Nombre —> \[Espacio aislado] Sesión de Edge
1. URL —> https\://www\.adobe.com
   - Tenga en cuenta que esta dirección URL se reemplazará con el sitio real del cliente
1. Haga clic en el botón Next

   ![Haga clic en Siguiente después de escribir el nombre de la sesión y la dirección URL](assets/monitor-your-event-click-next-button.png)

4. Copie el vínculo en un lugar al que pueda hacer referencia posteriormente

5. Haga clic en el botón **Listo**

   ![Copie el vínculo de la sesión de Assurance y haga clic en Listo](assets/monitor-your-event-copy-link.png)



6. Vaya a **Configuración**

   ![Vaya a la pestaña Configuración en la sesión de Assurance](assets/monitor-your-event-navigate-to-settings.png "Haga clic en la configuración")



7. Habilite **Transacciones de eventos** y **Edge Delivery** haciendo clic en el botón **+**, luego **Listo**

![Habilitar transacciones de eventos y Edge Delivery y, a continuación, haga clic en Listo](assets/monitor-your-event-enable-event-transactions-and-edge-delivery.png)


## Abrir Postman

Vaya a Postman -> Crear Edge de eventos web (sin autenticación) -> Encabezados

1. Agregue **x-adobe-aep-validation-token** a los encabezados con el vínculo copiado desde Assurance. Coja **solo el valor ID** después de = en el vínculo que copió de Assurance. p. ej. [https://www.adobe.com/?adb\_validation\_sessionid=](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0)[`efa4a9ed-02d8-4647-80fa-f01a5be273d0`](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0)
1. Solo usaríamos el valor [`efa4a9ed-02d8-4647-80fa-f01a5be273d0`](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0), no la dirección URL completa

   ![Agregue el encabezado x-adobe-aep-validation-token con el ID de sesión de Assurance en Postman](assets/monitor-your-event-populate-the-x-adobe-aep-validation-token.png)



3. En Postman, guarde y ejecute la solicitud **Crear Edge de eventos web (sin autenticación)**



## Ver registros de Assurance

Vuelva a Assurance y verá que se muestran muchos eventos. Filtre solo a tipos de eventos relevantes colocando el ID de flujo de datos en la búsqueda

![Filtre eventos de Assurance buscando su ID de secuencia de datos](assets/monitor-your-event-filter-using-search.png)



Seleccione un evento y abra cualquier mensaje si es necesario en el carril derecho.

![Seleccione un evento y expanda sus mensajes en el carril derecho](assets/monitor-your-event-expand-messages.png)

Tipos de eventos que buscar:

- hitReceived (muestra la carga útil recibida por Edge)
- Regla de evaluación (si configura SSF, muestra las reglas que se evalúan)
- fireDestinations (a qué destinos se envió esto)
- segmentsDiscovered (cumple los requisitos para cualquier segmento de Edge)
- com.adobe.experience\_platform.edge\_segmentation/response (con qué segmentos respondió)

![Seleccione cada tipo de evento para ver cómo lo interpreta Assurance](assets/monitor-your-event-select-each-event.png)

Explore estos y vea cómo Assurance interpreta cada paso.
