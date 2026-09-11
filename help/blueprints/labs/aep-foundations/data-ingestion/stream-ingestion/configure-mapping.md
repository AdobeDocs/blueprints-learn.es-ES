---
hold: true
title: Configurar asignación
description: Importe el conjunto de asignaciones desde el laboratorio de ingesta por lotes y actualice los campos de fecha calculada para que coincidan con el formato de fecha del origen de flujo.
doc-type: article
solution: Experience Platform
exl-id: c05792af-5eab-4e62-a26e-a54478a988a8
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Configurar asignación

> [!NOTE]
>
>Siga esta sección únicamente si ha completado correctamente el laboratorio de ingesta por lotes.  De lo contrario, siga los [datos de asignación](../batch-ingestion/mapping-data/overview.md) pasos que se encontraron en el laboratorio de ingesta por lotes.

## Importar conjunto de asignaciones

Si ha completado el laboratorio de ingesta por lotes, puede volver a utilizar el conjunto de asignaciones que creó allí 😄🎉

Siga estos pasos:

1. Haga clic en el botón **Importar asignación** de la pantalla de asignación

![Botón Importar asignación en la pantalla de asignación](assets/configure-mapping-import-mapping-button.png)



1. Elija el flujo de datos que ha creado en la sección Ingesta por lotes y selecciónelo.  Debe tener un nombre como **Lote de cuenta de cliente v2 - \&lt;sus iniciales>.**

![Elección del flujo de datos de ingesta por lotes para importar su conjunto de asignaciones de](assets/configure-mapping-choose-batch-ingestion-dataflow.png)



Después de la importación, verá que aparecen errores.  Esto se debe a que el formato de fecha utilizado para el campo birth\_Date en el archivo de muestra ha cambiado.

- Archivo de muestra por lotes utilizado -> mm/dd/aaaa
- Transmitir archivo de muestra utilizado -> aaaa-mm-dd

Los campos calculados que usan las funciones **date** deberán actualizarse para tener en cuenta el cambio en el formato de fecha usado.

![Errores de asignación mostrados después de importar el conjunto de asignaciones de ingesta por lotes](assets/configure-mapping-mapping-after-the-import.png)



## Actualizar campos calculados

Actualice cada campo calculado simplemente haciendo clic en el icono de flecha situado junto a cada campo calculado y, a continuación, valide las asignaciones

![Icono de flecha donde hacer clic para editar la fórmula de un campo calculado](assets/configure-mapping-arrow-to-edit-calculated-field-formula.png)

| Campo de destino | Nuevo campo calculado |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| person.birthYear | date\_part(&quot;yyyy&quot;,date(birth\_Date,&quot;yyyy-M-d&quot;)) |
| person.birthDayAndMonth | concat(fecha\_part(&quot;mm&quot;, fecha(nacimiento\_Fecha, &quot;aaaa-M-d&quot;)).toString(), &quot;-&quot;, fecha\_part(&quot;dd&quot;, fecha(nacimiento\_Fecha, &quot;aaaa-M-d&quot;)).toString()) |
