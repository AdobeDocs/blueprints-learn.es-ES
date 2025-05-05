---
title: Revisar y aprobar el modelo
description: 'Revisar y aprobar el modelo: Marketo Engage y modelo de integración de Workfront'
exl-id: a446faab-7db4-42a2-b4b9-395725c49c9f
source-git-commit: 3d6a2416cdb9956e59be4b2918ba19f88cd2150b
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 87%

---

# Revisar y aprobar el modelo {#review-and-approve-blueprint}

Garantizar que los activos y las campañas de marketing cumplan las expectativas y los estándares de una empresa va más allá de ofrecer el contenido y los mensajes adecuados al público indicado. Las organizaciones también tienen la responsabilidad de respetar las políticas internas, las normativas del sector e incluso los requisitos legales cuando se embarcan en nuevas iniciativas de marketing. Al incorporar pasos de revisión y aprobación en el proceso de desarrollo de campañas, los equipos de marketing pueden garantizar que el contenido y los mensajes sean precisos y estén en conformidad con las normas de su sector, especialmente en sectores como el financiero, el sanitario y el farmacéutico.

Con Workfront y Marketo Engage, los equipos de marketing pueden disponer de un sistema de marketing muy interconectado, con mensajes precisos y en conformidad.

## Desbloquee las revisiones y aprobaciones avanzadas para Marketo Engage con Workfront {#unlock-proofing-and-advanced-approvals}

En lo que respecta a la creación de campañas de marketing, debemos tener en cuenta que múltiples sistemas sean compatibles con los diferentes pasos implicados, entre los que se incluyen la planificación, la creación, la revisión, la retroalimentación, la aprobación y la ejecución. Con Workfront y Marketo Engage, los equipos disponen de todas las herramientas necesarias para guiarles a lo largo de todo el proceso de planificación y lanzamiento de una nueva campaña de marketing. Además, los equipos pueden agilizar aún más su proceso de revisión y aprobación para aumentar la velocidad de desarrollo de las campañas, y garantizar al mismo tiempo que la precisión y la conformidad se mantengan al más alto nivel.

### Revisar y aprobar casos de uso desbloqueados con Marketo Engage y Workfront {#review-and-approve-use-cases-unlocked-with-marketo-engage-and-workfront}

* Elimine los comentarios inconexos y aumente la colaboración en un lugar centralizado a través de las funcionalidades de anotación y comentarios de Workfront en los activos de Marketo Engage.

* Centralice sus aprobaciones al activarlas en Marketo Engage desde los flujos de trabajo de aprobación de Workfront.

* Dé soporte y agilice los complejos flujos de trabajo de aprobación de los activos de marketing gracias a las funcionalidades avanzadas de aprobación de Workfront con los activos de Marketo Engage.

* Democratice el acceso a los borradores de marketing al introducir de forma programática los activos de Marketo en Workfront para que múltiples responsables de departamento puedan revisarlos.

* Realice un seguimiento de los cambios y cree un registro en papel al centralizar todo el trabajo de revisión y comprobación de los activos de Marketo Engage en Workfront.

## Planificación del flujo de trabajo de pruebas y aprobaciones {#planning-your-proof-and-approval-workflow}

Tenga en cuenta los siguientes aspectos antes de configurar la integración de prueba y aprobación entre Marketo Engage y Workfront:

* ¿Qué activos deberán revisarse y aprobarse?
* ¿Quién deberá aprobarlos?
* ¿Tendrá que haber varios aprobadores antes de que un activo de marketing pueda ponerse en marcha?
* ¿En qué momento del proceso de desarrollo de la campaña se reunirán los activos de marketing y estarán listos para su revisión?

Responder a estas preguntas le ayudará a tener una idea de cómo será su flujo de aprobación y cómo empezar a pensar en la configuración de su instancia de Workfront.

## Creación de un flujo de trabajo de prueba y aprobación entre Marketo Engage y Workfront {#building-a-proof-and-approval-workflow}

Para agilizar el proceso de prueba y aprobación entre Workfront y Marketo Engage, puede integrar las dos soluciones con Workfront Fusion. Workfront Fusion proporciona una interfaz de flujo de trabajo para desencadenar acciones y pasar información entre sus instancias de Workfront y Marketo Engage.

Para ello, considere los siguientes pasos como parte del proceso para una experiencia integrada de revisión y aprobación.

1. Configure el proyecto de Workfront con una tarea Lista para revisión.
1. Active su correo electrónico de Marketo Engage para sincronizarlo con Workfront con un cambio de estado de tarea.
1. Convierta el archivo de correo electrónico de Marketo Engage en una prueba revisable en Workfront.
1. Utilice las pruebas de Workfront para colaborar mediante comentarios y anotaciones.
1. Apruebe la prueba de Workfront para activar la aprobación de activos en Marketo Engage y, a continuación, marque la tarea como completa.

### Configure un proyecto de Workfront con una tarea Lista para revisión {#configure-a-workfront-project-with-a-ready-for-review-task}

Use [plantillas de proyectos](https://experienceleague.adobe.com/docs/workfront/using/manage-work/projects/create-and-manage-project-templates/project-template-overview.html?lang=es){target="_blank"} para capturar la mayoría de los procesos repetibles, la información y los ajustes asociados a los proyectos de su organización. Puede definir tareas, temas de cola, crear formularios personalizados y adjuntar documentos en la plantilla.

Incluya tareas en la plantilla del proyecto en Workfront para revisar los activos que forman parte de la campaña de marketing. Además, puede añadir un proceso de aprobación para gestionar aprobaciones únicas u otras más complejas de varios niveles.

Si desea lanzar una nueva campaña por correo electrónico, debe contar con una plantilla de proyecto que incluya una tarea para revisar el correo electrónico, así como un proceso de aprobación para garantizar que los responsables de departamento pertinentes aprueben el correo electrónico antes de enviarlo.

![pantalla de tareas](assets/review-and-approve-blueprint-1.png){zoomable="yes"}

### Active su correo electrónico de Marketo Engage para sincronizarlo con Workfront con un cambio de estado de tarea {#trigger-your-marketo-engage-email-to-sync-to-workfront}

Como parte de su proceso de revisión, querrá poder sincronizar los correos electrónicos con su proyecto de Workfront una vez que estén listos para que su equipo de marketing los revise. Para ello, le recomendamos que configure una tarea Lista para revisión con un [estado de tarea](https://experienceleague.adobe.com/docs/workfront/using/manage-work/projects/update-work-on-a-project/update-task-status.html?lang=es){target="_blank"} que indique cuándo estará listo el correo electrónico para su revisión. En nuestro ejemplo, hemos añadido a la tarea un estado Revisar correo electrónico de Marketo que puede seleccionarse cuando el borrador del correo electrónico esté listo para que lo revisen los responsables de departamento.

Con este estado en el proyecto de Workfront, puede configurar el escenario de Workfront Fusion para que espere a que la tarea Listo para revisar se actualice a Revisar correo electrónico de Marketo. Una vez actualizado, el escenario puede recuperar el correo electrónico de Marketo Engage como un archivo HTML, comprimirlo y guardar una copia en los documentos del proyecto de Workfront para su revisión.

![listo para la pantalla de revisión](assets/review-and-approve-blueprint-2.png){zoomable="yes"}

### Convierta el correo electrónico de Marketo Engage en una prueba revisable en Workfront {#convert-your-marketo-engage-email-to-reviewable-proof-in-workfront}

Una vez que la tarea “Listo para revisión” pasa al estado “Revisar correo electrónico de Marketo” y el correo electrónico de Marketo Engage se guarda en Workfront, puede configurar el escenario Workfront Fusion para convertir el correo electrónico en una prueba de Workfront.

### Utilice las pruebas de Workfront para colaborar mediante comentarios y anotaciones {#use-workfront-proofing-to-collaborate}

Las funciones de [corrección de Workfront](https://experienceleague.adobe.com/docs/workfront/using/review-and-approve-work/proofing/proofing-overview/proofing-basics.html?lang=es){target="_blank"} permiten a su equipo de marketing tomar un nuevo recurso, como una imagen o un correo electrónico, y colaborar mediante comentarios y anotaciones. Una vez que una prueba está lista para ejecutarse, los responsables de la toma de decisiones pueden aprobarla desde la herramienta de prueba.

![convertir pantalla de correo electrónico](assets/review-and-approve-blueprint-3.png){zoomable="yes"}

### Aprobar Workfront Proof y déclencheur la aprobación de recursos en Marketo Engage, marcar la tarea como completada {#approve-workfront-proof-and-trigger-asset-approval-in-marketo-engage}

Workfront Fusion puede detectar cuándo las partes interesadas han aprobado el correo electrónico y enviar una solicitud al Marketo Engage para que apruebe el correo electrónico dentro de Marketo.

Con el correo electrónico revisado/aprobado por los miembros del equipo adecuados, el correo electrónico está listo para su publicación en Marketo Engage.

## Plantillas de escenario de Fusion {#fusion-scenario-templates}

Hemos creado Plantillas de Fusión que le ayudarán a comenzar con la integración para agilizar el desarrollo de flujos de trabajo de Revisión y Aprobación en su propia instancia de Workfront y Marketo Engage. Puede utilizar estas plantillas si busca “Marketo” en la sección de plantillas públicas de Fusion y las descarga en su instancia.

### Revisar una prueba de correo electrónico de su borrador de correo electrónico de Marketo Engage en Workfront {#review-an-email-proof-of-your-marketo-engage-email-draft-in-workfront}

El siguiente escenario de fusión le guiará a lo largo de la primera mitad del flujo de revisión y aprobación, en el que el borrador del correo electrónico puede extraerse de Marketo Engage y guardarse en Workfront como una Prueba. Una vez guardado como Prueba en los documentos del proyecto de Workfront, los responsables de departamento pueden revisarlo, comentarlo y anotarlo como parte del proceso de revisión.

![flujo de revisión y aprobación del escenario de fusión](assets/review-and-approve-blueprint-4.png){zoomable="yes"}

### Aprobar un correo electrónico en Workfront que desencadena la aprobación del activo en Marketo Engage {#approve-an-email-in-workfront-that-triggers-approval}

El siguiente escenario de fusión se puede utilizar para detectar cuándo una Prueba en Workfront se ha aprobado, y enrutar esa aprobación a Marketo Engage para actualizar el borrador de correo electrónico para que esté activo y listo para su uso en un programa de Marketo Engage.

![aprobación de revisión de escenario de fusión](assets/review-and-approve-blueprint-5.png){zoomable="yes"}

En conjunto, estos dos escenarios se pueden usar para crear una ruta bidireccional que extraiga activos de marketing desde Marketo Engage hacia flujos de trabajo robustos de revisión y aprobación de Workfront, y devuelva las aprobaciones a Marketo Engage desde Workfront.
