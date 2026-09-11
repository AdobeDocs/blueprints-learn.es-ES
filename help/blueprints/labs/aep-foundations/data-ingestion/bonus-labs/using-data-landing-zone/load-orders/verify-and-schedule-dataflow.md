---
hold: true
title: Verificación y programación del flujo de datos
description: Compruebe el conjunto completo de asignaciones de pedidos, obtenga una vista previa de la salida y programe el flujo de datos para que se ejecute cada 15 minutos.
doc-type: article
solution: Experience Platform
exl-id: b7f0c43b-092c-45ba-b95b-27cb4a49d110
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 7%

---


# Verificación y programación del flujo de datos

## Comprobar doble conjunto de asignaciones

| # | Columna Source | Columna XDM |
| -- | ------------------------------------------- | -------------------------------------------------------- |
| 1 | orderStatus | eventType |
| 2 | lastOrderStatusUpdate | timestamp |
| 3 | orderID | order.orderID |
| 4 | orderDate | order.orderDate |
| 5 | orderTotal | order.priceTotal |
| 6 | paymentType | order.payment.paymentType |
| 7 | paymentAmount | order.payment.paymentAmount |
| 8 | paymentCurrencyCode | order.payment.currencyCode |
| 9 | paymentTransactionID | order.payment.transactionID |
| 10 | plan.ID | order.\_devbc.plan.planID |
| 11 | customerID | \_devbc.customerID |
| 12 | personalEmail | \_devbc.personalEmail |
| 13 | storeID | store.storeID |
| 14 | shippingStreetAddress | shipping.address.street1 |
| 15 | shippingCity | shipping.address.city |
| 16 | shippingState | shipping.address.state |
| 17 | shippingZip | shipping.address.postalCode |
| 18 | shippingMethod | shipping.shippingMethod |
| 19 | shippingAmount | shipping.shippingAmount |
| 20 | shippingDestination | shipping.shippingDestination |
| 21 | billingStreetAddress | billing.address.street1 |
| 22 | billingCity | billing.address.city |
| 23 | billingState | billing.address.state |
| 24 | billingZip | billing.address.postalCode |
| 25 | productos\[\*] | productListItems\[\*] |
| 26 | products\[\*].productID | - productListItems\[\*].\_id - productListItems\[\*].SKU |
| 27 | products\[\*].make | productListItems\[\*].\_devbc.make |
| 28 | products\[\*].model | productListItems\[\*].\_devbc.model |
| 29 | products\[\*].price | productListItems\[\*].priceTotal |
| 30 | concat(orderID, &quot;-&quot;, lastOrderStatusUpdate) | \_id |
| 31 | &quot;inStore&quot; | order.\_devbc.acqSource |



## Previsualización de la salida de asignación

1. Previsualice la salida de asignación. Desplácese por todos los atributos para asegurarse de que no haya ninguna exclamación roja junto a ninguno de los atributos del lado derecho.

![Vista previa de la pantalla de asignación sin errores en ningún atributo asignado](assets/verify-and-schedule-dataflow-preview-mapping-screen.png "La vista previa de la pantalla de asignación tendrá este aspecto")

1. En la navegación del lado izquierdo de la vista previa, seleccione la matriz de objetos **productListItems**. El lado derecho se actualiza para mostrar solo los atributos de esa matriz de objetos.

>[!NOTE]
>
>Observe que **productListItems.currencyCode** y **productListItems.quantity** se rellenan automáticamente (incluso después de quitar las asignaciones). Esto sucede porque **productListItems** está asignado como objeto principal.

![Se completó la pantalla de asignación de productListItems después de quitar las invalidaciones duplicadas](assets/verify-and-schedule-dataflow-completed-mapping-screenshot.png "La asignación completada tendrá un aspecto similar al de la siguiente captura de pantalla")

## Programar la ejecución

1. Establezca la programación para que se ejecute **cada 15 minutos**; para ello, establezca la frecuencia en Minuto y el intervalo en 15. Revise el flujo y haga clic en Finish.

>[!CAUTION]
>
>Asegúrese de que la programación esté configurada en 15 minutos. Si programa la ejecución como **Ejecutar una vez**, no podrá volver a ejecutarla aunque realice cambios en la asignación más adelante.

1. La ejecución del flujo de datos no comienza inmediatamente y tarda unos minutos. Por lo tanto, el último estado de ejecución del flujo de datos está establecido en &quot;*Sin ejecuciones*&quot;.

1. Después de unos minutos, el flujo de datos se ha realizado correctamente. Observe el **último estado de ejecución del flujo de datos** y la **última fecha de ejecución del flujo de datos**.

1. Haga clic en el nombre del flujo de datos para obtener una lista de las ejecuciones del flujo de datos. Se deben ingerir 10 registros.

1. Haga clic en la hora de inicio de la ejecución del flujo de datos para ver los detalles del diagnóstico de errores.

1. En la barra de navegación izquierda, vaya a Conjuntos de datos en Platform y haga clic en **Pedidos - YourNameHere**

1. Haga clic en **Vista previa del conjunto de datos.**
