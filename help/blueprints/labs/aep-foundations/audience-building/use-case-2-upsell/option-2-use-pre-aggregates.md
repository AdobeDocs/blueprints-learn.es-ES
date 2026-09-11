---
hold: true
title: Opción
description: Cree una audiencia de flujo completo usando atributos de uso preagregados calculados en sentido ascendente en lugar de agregar eventos dentro de la regla de audiencia.
doc-type: article
solution: Experience Platform
exl-id: fe6ee041-814f-41c1-91cf-c3473cbca0c2
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Opción #2: usar preacumulados

El desafío de los agregados de nuestra audiencia es que nuestra audiencia (mientras transmite) se basa en acumulaciones realizadas dentro de audiencias que son audiencias por lotes. Dado que Marketing ha determinado que se necesita un enfoque más a tiempo real, hemos hecho tres cosas para incorporar esto al diseño:

- Calcule los agregados antes de transmitir los datos en

>[!NOTE]
>
>Esto es poco común, ya que la mayoría de los datos transmitidos se diseñan en torno a un solo evento o a un acumulado

- Uso del Nombre de Plan Desnormalizado
- Transmitir los datos en

## Crear la audiencia

Cree una audiencia de todos los perfiles cuyo uso de datos de facturación sea alto, pero que actualmente no tengan un plan de teléfono definitivo.

1. Crear una audiencia nueva
1. Busque &quot;Agg&quot; en la pestaña Atributos no evento y arrastre los dos agregados al lienzo. Establezca los operadores y valores adecuados para cada uno.

![Establezca los operadores y valores apropiados para cada agregado](assets/option-2-use-pre-aggregates-set-operators-and-values.png)



3. Busque el nombre del plan en el perfil y añádalo (XDM Individual Profile > Devbc > Detalles del plan > Nombre del plan). Seleccione No es igual a &quot;Ultimate&quot;

![Seleccionar Nombre De Plan No Es Igual A Ultimate](assets/option-2-use-pre-aggregates-select-does-not-equal-ultimate.png)



4. Proporcione una descripción.  El método de evaluación Validate es Streaming.

5. Guardar la audiencia como &quot;*Uso de datos de facturación alto pero sin plan de Ultimate (Agg)*&quot;

>[!NOTE]
>
>Recuerde, cambiamos la lógica agregada a nuestra capa de ETL de flujo ascendente.
>
>Esta opción es un equilibrio entre tener una audiencia por lotes en la que el experto en marketing controle la lógica y una audiencia de flujo, pero empujando la definición y el control a la capa de ETL en la que el departamento de ingeniería debe participar.

>[!TIP]
>
>**Laboratorio de desafío opcional**
>
>¿Terminaste temprano?
>
>Nos gustaría ponernos en contacto con nuestros VIP en tiempo real con un mensaje especial cuando compren.  Cree una audiencia de &quot;VIP&quot;.  Un VIP es alguien que compró más de 1.000 dólares en el último mes.
