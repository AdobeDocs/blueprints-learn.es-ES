---
hold: true
title: Validar evento en el lago de datos
description: Obtenga información sobre cómo consultar el lago de datos para verificar que se escribió un evento web transmitido en el conjunto de datos correcto.
doc-type: article
solution: Experience Platform
exl-id: 14445089-aa3c-4cce-9d33-80032b6f9868
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# Validar evento en el lago de datos

## Objetivo de aprendizaje

Compruebe que el evento web se haya escrito en el lago de datos de Experience Platform.

## Validar evento

&#x200B;> [!NOTE]
>
>Finalmente, los datos aparecerán en el lago de datos.  **Esto puede tardar hasta 60 minutos**.  Sabemos que el conjunto de datos está habilitado para el perfil y, por lo tanto, el evento creará un fragmento de perfil.
>
>Puede buscar y consultar el conjunto de datos web.

1. Vaya a **Consultas** y **Crear consulta**

![Pantalla Crear consulta en la sección Consultas](assets/validate-event-on-data-lake-create-query.png)

&#x200B;2. Copie este SQL y péguelo en la consulta

```sql
SELECT identityMap['email'][0].id, * FROM dep_web
where identityMap['email'][0].id = 'henry.creel@emailsim.io'
```

&#x200B;3. **Ejecutar** Consulta

&#x200B;> [!NOTE]
>
>**Recordar**: Finalmente, los datos aparecerán en el lago de datos.  **Esto puede tardar hasta 60 minutos**.
>
>No es necesario esperar a que aparezca. No dude en volver a este paso y comprobarlo más tarde.



![Resultados de la consulta que muestran el evento web transmitido en el lago de datos](assets/validate-event-on-data-lake-query-results.png)

## Resumen

El registro de evento aparece en el conjunto de datos adecuado.
