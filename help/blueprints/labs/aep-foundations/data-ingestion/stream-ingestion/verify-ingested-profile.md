---
title: Verificar perfil introducido
description: Busque un perfil transmitido en el explorador de perfiles utilizando su área de nombres de identidad principal para confirmar que la ingesta se ha realizado correctamente.
doc-type: article
solution: Experience Platform
exl-id: d45d6baf-9597-4419-b838-03156ce8cc83
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Verificar perfil introducido

## Validación de streaming

La validación de los datos de flujo continuo dentro de Adobe Experience Platform requiere algunos pasos diferentes.  Recuerde que los datos de flujo continuo pueden escribir en varias bases de datos según la configuración del conjunto de datos.

| Almacenamiento | Latencia | Descripción |
| -------------- | -------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| Lago de datos | \~hasta 60 minutos | El lugar de descanso final para todos los datos de streaming |
| Almacenamiento de perfiles | \~1 min de media pero hasta \~15min | Solo procesa los datos cuando el conjunto de datos subyacente está habilitado para el perfil |
| Almacén de identidad | \~1 min promedio \~10 minutos de microlotes para nuevas relaciones de identidad | Solo procesa los datos cuando el conjunto de datos subyacente está habilitado para el perfil |

Según lo que esté intentando validar, es posible que tenga que ir a varios lugares diferentes, como puede ver arriba.  En esta situación, escribió los datos en el perfil (tal como había habilitado el conjunto de datos para el perfil), por lo que compruebe el Almacenamiento de perfiles para ver si el perfil está allí.



## Búsqueda del perfil

1. En la interfaz de usuario, vaya a **Perfiles -> Examinar**
1. Introduzca los siguientes valores en los cuadros de entrada Área de nombres de identidad y Valor de identidad:
   - **Área de nombres de identidad** -> `customerID`
   - **Valor de identidad** -> `202208240125`
1. Haz clic en el botón **Ver** para buscar tu perfil
1. Haga clic en el vínculo **ID de perfil** de la fila devuelta para ver su perfil

![Pantalla Examinar perfil que muestra la fila de perfil devuelta después de buscar por customerID](assets/verify-ingested-profile-browse-profile-screen.png "Pantalla Examinar perfil")

Eche un vistazo a su perfil y compruebe que coincide con el que ha transmitido. ¡Bastante genial!

![Vista de detalles del perfil que coincide con el registro de cuenta de cliente transmitido](assets/verify-ingested-profile-profile-detail-view.png)

>[!NOTE]
>
>Dada la latencia de \~10 minutos en la vinculación de nueva relación de identidad, si hubiera intentado buscar su perfil utilizando el área de nombres de correo electrónico no habría visto una respuesta.
>
>El uso del área de nombres customerID (que es la identidad principal) garantizó que pudiera buscar el perfil inmediatamente.
>
>Recuerde que el perfil solo conoce las identidades principales 😄
