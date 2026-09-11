---
hold: true
title: Corregir asignaciones de paso a través
description: Identifique y corrija asignaciones de paso A través de AI/ML incorrectas, como asignaciones de campo de destino duplicadas o no coincidentes, antes de validarlas.
doc-type: article
solution: Experience Platform
exl-id: b06cc091-661e-4ff4-b6e5-f16bc5128b6b
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# Corregir asignaciones de paso a través

## Colocar asignaciones específicas

Algunos de los datos de origen que tiene que gestionarse mediante campos calculados.  Para solucionarlos, suéltelos en las asignaciones y vuelva a validar las asignaciones.

1. Suelte los siguientes datos de origen de las asignaciones:
   - fecha_nacimiento
   - origen
   - sms\_optIn
1. Vuelva a validar las asignaciones haciendo clic en el botón Validar

![Botón Validar utilizado para volver a validar asignaciones después de soltar campos](assets/fix-passthrough-mappings-re-validate-mappings-using-validate-button.png "Volver a validar asignaciones con el botón Validar")

>[!NOTE]
>
>Después de hacer clic en Validar, es posible que aún tenga errores



## Ejemplos de asignación incorrectos

Aunque las recomendaciones de IA/ML son útiles, a veces son erróneas.  Si inspecciona las recomendaciones, es posible que encuentre este tipo de errores que debe corregir

>[!NOTE]
>
>A continuación se muestran algunos ejemplos de asignaciones no válidas que puede ver en su propia zona protegida. También puede ver otros errores.

## Duplicar asignaciones

En este escenario, verá que el recomendador de AI/ML asignó dos campos de origen diferentes al mismo campo de destino **person.name.lastName**



![Dos campos de origen diferentes asignados al mismo campo de destino person.name.lastName](assets/fix-passthrough-mappings-person-lastname-mapped-twice.png "person.name.lastName se asignan dos veces en esta asignación")

![Ejemplo de asignación de paso a través duplicado que implica el campo nombre_plan](assets/fix-passthrough-mappings-plan-name-duplicate-mapping.png)



## Asignaciones incorrectas

Esta asignación parece correcta, pero tras una inspección más detallada **email** no es lo mismo que **emailFormat**

![La asignación en la que el correo electrónico está asignado incorrectamente en lugar de emailFormat](assets/fix-passthrough-mappings-email-mapped-incorrectly.png "parece estar asignada correctamente, pero es incorrecta según los requisitos")

Y en este otro en el que **email\_optIn** se asigna incorrectamente al objeto de consentimiento incorrecto

![email_optIn asignado incorrectamente al objeto de consentimiento incorrecto](assets/fix-passthrough-mappings-email-optin-wrong-consent-object.png "email_optIn parece estar asignado correctamente, pero es incorrecto según los requisitos")



## Corrección de asignaciones de paso a través

Para corregir asignaciones de paso a través que apuntan incorrectamente al campo de destino incorrecto, realice los siguientes pasos.

### Ejemplo

1. Comience con una asignación no válida y haga clic en el cuadro de campo de destino. Por ejemplo, en la asignación siguiente, el campo **person.name.lastName** no está asignado correctamente y está asignado a **planName**
1. En el panel de esquema de destino que se abre a la derecha, elija el campo de destino adecuado y seleccione **\_devbc.plan.name**
1. El campo de destino debe actualizarse ahora en el cuadro de campo de destino
1. Después de corregir cada error de este tipo, debe presionar el botón **Validar** para asegurarse de reducir este tipo de errores y de no introducir nuevos errores.



![Revisando la lista de asignaciones para corregir cada error de asignación](assets/fix-passthrough-mappings-work-through-mapping-errors.png "Supere y corrija los errores de asignación")



![Panel de esquema de destino para seleccionar el campo correcto para corregir una asignación de paso a través](assets/fix-passthrough-mappings-choose-correct-target-field.png "Elija el campo de destino correcto y compruebe que coincide con los requisitos de paso a través")

>[!WARNING]
>
>No continúe con el siguiente paso hasta que haya resuelto todos los errores de asignación
