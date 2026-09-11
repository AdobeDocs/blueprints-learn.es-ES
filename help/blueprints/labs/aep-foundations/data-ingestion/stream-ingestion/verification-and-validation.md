---
hold: true
title: Verificación y validación
description: Obtenga una vista previa de un conjunto de datos transmitido en la IU y ejecute consultas SQL para verificar los registros ingeridos y los campos de esquema anidados.
doc-type: article
solution: Experience Platform
exl-id: fbdb0b6b-08b6-49b8-b6ab-d59d5941c678
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Verificación y validación

## Previsualización del conjunto de datos

1. Haga clic en **Conjuntos de datos**
1. **Busque** y **haga clic** en el nombre del conjunto de datos que ha creado.

![Acceso al conjunto de datos creado en el panel Conjuntos de datos](assets/verification-and-validation-access-the-dataset-in-the-datasets-pane.png "Acceso al conjunto de datos en el panel Conjuntos de datos")



1. Haga clic en **Vista previa del conjunto de datos** en la esquina superior derecha

![Botón Vista previa del conjunto de datos ubicado en la esquina superior derecha de la pantalla del conjunto de datos](assets/verification-and-validation-preview-dataset-button.png "Vista previa del conjunto de datos se encuentra en la esquina superior derecha ")



1. **Verificar** y **validar** los mismos registros que ha ingerido al hacer clic en el panel izquierdo que muestra la jerarquía de esquema.

![Comprobando y validando registros ingeridos mediante el panel de jerarquía de esquema](assets/verification-and-validation-verify-and-validate-the-dataset.png "Verificar y validar el conjunto de datos")

>[!NOTE]
>
>**Vista previa del conjunto de datos** solo mostrará las primeras filas del conjunto de datos. Los objetos de matriz no son visibles.



## Query dataset

1. **Cerrar** la vista previa
1. En la pantalla Conjunto de datos, haga clic en el icono Copiar de **Nombre de tabla**. En la pantalla de ejemplo siguiente, el nombre de tabla es `customer_account_sm`

![Copiando el nombre de tabla de la pantalla Conjunto de datos para utilizarlo en una consulta](assets/verification-and-validation-copy-the-table-name.png "Copie el nombre de tabla")



1. Vaya a la sección **Consultas**

1. Haz clic en **Crear consulta**

![Acceso al editor de consultas desde la sección Consultas](assets/verification-and-validation-access-the-query-editor.png "Acceso al editor de consultas")



1. Activar o desactivar **Editor de consultas mejorado**

![Interfaz del editor de consultas con la opción del Editor de consultas mejorado habilitada](assets/verification-and-validation-enhanced-query-editor-toggle.png "Interfaz del editor de consultas")



1. Copie y pegue la siguiente consulta SQL en **Editor**. Recuerde reemplazar `<table_name>` con el valor que obtuvo en el paso 2.

```sql
SELECT * FROM <table_name>
```



1. Presione el botón **Reproducir**.

1. **Vista previa** de los resultados.

1. Ejecute también la siguiente consulta SQL para recuperar el esquema XDM junto con los datos:

```sql
SELECT to_json(shippingAddress) FROM <table_name>
```



1. Para tener acceso a los datos del `postalCode` **nodo**, puede escribir:

```sql
SELECT shippingAddress.postalCode FROM <table_name>
```

>[!TIP]
>
>¡Felicidades!  Ha ingerido y creado correctamente un conjunto de muestras de perfiles de clientes en tiempo real
