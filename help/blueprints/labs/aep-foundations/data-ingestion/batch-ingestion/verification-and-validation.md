---
title: Verificación y validación
description: Obtenga una vista previa de un conjunto de datos ingerido en la interfaz de usuario y ejecute consultas SQL para verificar registros ingeridos por lotes y campos de esquema anidados.
doc-type: article
solution: Experience Platform
exl-id: 7e7cd43d-cc24-4a40-a175-2c651436ab79
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Verificación y validación

## Previsualización del conjunto de datos

1. Haga clic en **Conjuntos de datos**
1. **Busque** y **haga clic** en el nombre del conjunto de datos que ha creado.

   ![Localizar y hacer clic en el nombre del conjunto de datos en el panel Conjuntos de datos](assets/verification-and-validation-access-dataset-in-datasets-pane.png "Obtener acceso al conjunto de datos en el panel Conjuntos de datos")



1. Haga clic en **Vista previa del conjunto de datos** en la esquina superior derecha

   ![Ubicación del botón Vista previa del conjunto de datos en la esquina superior derecha de la pantalla del conjunto de datos](assets/verification-and-validation-preview-dataset-button-location.png "Vista previa del conjunto de datos en la esquina superior derecha")



1. **Verificar** y **validar** los mismos registros que ha ingerido al hacer clic en el panel izquierdo que muestra la jerarquía de esquema.

![Vista previa de conjunto de datos con panel de jerarquía de esquema que muestra registros ingeridos](assets/verification-and-validation-verify-and-validate-the-dataset.png)

>[!NOTE]
>
>**Previsualizar conjunto de datos** muestra el lote exitoso más reciente en este conjunto de datos. No puede ver los lotes anteriores. Además, los datos complejos, como matrices y mapas, no se pueden ver hoy en día y aparecen como columnas vacías. ¡No te asustes! Para obtener una vista más completa, debe utilizar SQL para explorar el conjunto de datos como se explica a continuación.



## Query dataset

1. **Cerrar** la vista previa
1. En la pantalla Conjunto de datos, haga clic en el icono Copiar de **Nombre de tabla**. En la pantalla de ejemplo siguiente, el nombre de tabla es `customer_account_sm`

   ![Icono de copiar junto al nombre de tabla en la pantalla Conjunto de datos](assets/verification-and-validation-copy-table-name.png "Copie el nombre de tabla")



1. Vaya a la sección **Consultas**

1. Haz clic en **Crear consulta**

   ![Botón Crear consulta en la sección Consultas](assets/verification-and-validation-access-the-query-editor.png)



1. Copie y pegue la siguiente consulta SQL en **Editor**. Recuerde reemplazar `<table_name>` con el valor que obtuvo en el paso 6.

   ```sql
   SELECT * FROM <table_name>
   ```



1. Presione el botón **Reproducir**.

   ![Interfaz del editor de consultas con consulta SQL y botón Reproducir](assets/verification-and-validation-query-editor-interface.png "Interfaz del editor de consultas")



1. **Vista previa** de los resultados

1. Ejecute también la siguiente consulta SQL para recuperar el esquema XDM junto con los datos:

```sql
SELECT to_json(shippingAddress) FROM <table_name>
```

Para tener acceso a los datos del `postalCode` **nodo**, puede escribir:

```sql
SELECT shippingAddress.postalCode FROM <table_name>
```

>[!TIP]
>
>¡Felicidades!  Ha ingerido y creado correctamente un conjunto de muestras de perfiles de clientes en tiempo real
