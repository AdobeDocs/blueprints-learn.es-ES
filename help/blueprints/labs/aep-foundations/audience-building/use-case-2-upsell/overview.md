---
hold: true
title: Caso de uso
description: Defina un caso de uso de ampliación de venta dirigido a clientes con un alto uso de datos sin un plan de teléfono definitivo, comparando los enfoques de agregación de audiencias para la activación.
doc-type: overview-page
solution: Experience Platform
exl-id: d0268de8-87eb-4dd9-b699-99d42716f20c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Caso de uso #2: ampliación de venta

## Información general

En este vídeo aprenderá a abordar el caso de uso de ampliación de venta, que se dirige a clientes con un alto uso de datos para su activación a través de canales de correo postal y de pago.

>[!VIDEO](https://video.tv.adobe.com/v/3459487/?quality=12&learn=on)



**Definición de caso de uso**

Encuentre todos los clientes que tengan un uso total de datos de facturación en los últimos 6 meses >140 GB, un promedio móvil de 6 meses. uso de datos mensual de >=20 GB y que no tengan un plan de teléfono definitivo.

Activar en los canales de Facebook / Google y correo directo.

Campos de personalización de correo postal:

- Nombre → se utiliza para el saludo
- Dirección de correo → se utiliza para el correo
- Nombre del plan → utiliza para la instrucción de correo (por ejemplo, &quot;Eric, ¡actualiza a un plan definitivo hoy!&quot;)



## Tareas de análisis

Analice lo anterior y anote:

1. ¿Qué campos cree que son necesarios para abordar este caso de uso?
1. ¿El método de evaluación debe ser de transmisión por secuencias?
1. ¿Qué hay que tener en cuenta con los datos de facturación?
1. ¿Qué otra información desea conocer?

Recuerde: cuando recibimos los requisitos de las partes interesadas de la empresa, tienden a ser incompletos, utilizan otra terminología y realizan suposiciones sin saberlo. Es su trabajo traer tanto de eso a la superficie y guiarlos a algo que se pueda hacer.



## Aproximación

Para este caso de uso, vamos a evaluar dos opciones:

- Opción #1 (usar Audience para agregar)
  - Esto hará que la audiencia realice la agregación
    - Suma de uso de datos de facturación > 140 GB (últimos 6 meses)
    - Uso de datos de facturación Promedio > 20 GB (últimos 6 meses)
    - Uso de datos de facturación alto, pero sin plan de Ultimate
- Opción #2 (utilizar preacumulados)
  - Esto utilizará la agregación realizada antes de colocar los datos en el perfil
    - Uso De Datos De Facturación Alto Pero Sin Plan De Ultimate (Agg)
