---
title: Comprobar conjunto final de asignaciones
description: Compare sus asignaciones de ingesta de flujo continuo con el paso final esperado y el conjunto de asignación de campo calculado.
doc-type: article
solution: Experience Platform
exl-id: 8802aaca-f566-4972-8bd6-41aca9fae9bf
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# Comprobar conjunto final de asignaciones

## Asignaciones de paso a través

>[!NOTE]
>
>Asegúrese de que la asignación final coincida con lo que se muestra a continuación antes de continuar.

>[!NOTE]
>
>Reemplace \&lt;tenant-name> con el valor de la zona protegida

| Campo de Source | Campo de destino |
| ------------------------- | --------------------------------- |
| account\_create\_date | \&lt;tenant-name>.account.createDate |
| account\_end\_date | \&lt;tenant-name>.account.endDate |
| customer\_id | \&lt;tenant-name>.customerID |
| plan\_name | \&lt;tenant-name>.plan.name |
| plan\_id | \&lt;tenant-name>.plan.planID |
| billing\_city | billingAddress.city |
| billing\_zip\_code | billingAddress.postalCode |
| billing\_state | billingAddress.state |
| billing\_street\_address | billingAddress.street1 |
| email\_optIn | conents.marketing.email.val |
| mobile\_phone | mobilePhone.number |
| firstName | person.name.firstName |
| lastName | person.name.lastName |
| email | personalEmail.address |
| createDate | repo.createDate |
| modifyDate | repo.modifyDate |
| shipping\_city | shippingAddress.city |
| shipping\_zip\_code | shippingAddress.postalCode |
| shipping\_state | shippingAddress.state |
| shipping\_street\_address | shippingAddress.street1 |



## Asignaciones calculadas

>[!NOTE]
>
>Tenga en cuenta que las asignaciones de `birth_Date` son diferentes de las asignaciones del laboratorio de ingesta por lotes debido al formato de la fecha.  El lote está usando barras `/` mientras que la transmisión está usando guiones `-`

| Campos calculados | Campo XDM |
| ----------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| iif(sms\_optIn == null o sms\_optIn == &quot;&quot;, &#39;n&#39;, sms\_optIn) | conents.marketing.sms.val |
| concat(fecha\_part(&quot;mm&quot;, fecha(nacimiento\_Fecha, &quot;aaaa-M-d&quot;)).toString(), &quot;-&quot;, fecha\_part(&quot;dd&quot;, fecha(nacimiento\_Fecha, &quot;aaaa-M-d&quot;)).toString()) | person.birthDayAndMonth |
| date\_part(&quot;yyyy&quot;,date(birth\_Date,&quot;yyyy-M-d&quot;)) | person.birthYear |

>[!NOTE]
>
>Asegúrese de que la asignación final coincida con lo que se muestra a continuación antes de continuar



## Finalizar flujo de datos

Cuando termine, haga clic en el botón **Siguiente** y, a continuación, haga clic en el botón Finalizar para actualizar el flujo de datos con la nueva lógica de asignación.

![Revisando los detalles del flujo de datos antes de hacer clic en Finalizar para guardarlo](assets/check-final-mapping-set-review-and-finish-dataflow.png)



Ahora debería ver una pantalla que muestra la cuenta de la API HTTP que ha creado con todos los flujos de datos asociados que utilizan esa cuenta. El flujo de datos que ha creado también debe mostrarse.
