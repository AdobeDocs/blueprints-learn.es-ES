---
hold: true
title: Comprobar conjunto final de asignaciones
description: Compare las asignaciones de campos simples y calculadas para el esquema de cuenta del cliente con el conjunto de asignaciones final esperado.
doc-type: article
solution: Experience Platform
exl-id: d1521d08-1ccb-405f-b728-a2777598cb9f
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# Comprobar conjunto final de asignaciones

&#x200B;> [!NOTE]
>
>Si viene del laboratorio de ingesta de transmisión, haga clic en el siguiente enlace para continuar con el siguiente paso en ese laboratorio:
>
>[Laboratorio De Ingesta De Transmisión - Comprobar El Conjunto Final De Asignaciones](../../stream-ingestion/check-final-mapping-set.md)



## Asignaciones simples

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

&#x200B;> [!NOTE]
>
>Asegúrese de que la asignación final coincida con lo que se muestra a continuación antes de continuar.



## Asignaciones calculadas

| Campos calculados | Campo XDM |
| ------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| iif(sms\_optIn == null o sms\_optIn == &quot;&quot;, &#39;n&#39;, sms\_optIn) | conents.marketing.sms.val |
| concat(date\_part(&quot;month&quot;, date(birth\_Date,&quot;M/d/yyyy&quot;)).toString(), &quot;-&quot;, date\_part(&quot;day&quot;, date(birth\_Date,&quot;M/d/yyyy&quot;)).toString()) | person.birthDayAndMonth |
| date\_part(&quot;yyyy&quot;,date(birth\_Date,&quot;M/d/yyyy&quot;)) | person.birthYear |

&#x200B;> [!NOTE]
>
>Asegúrese de que la asignación final coincida con lo que se muestra a continuación antes de continuar
