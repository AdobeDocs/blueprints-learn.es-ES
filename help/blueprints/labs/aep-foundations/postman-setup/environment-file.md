---
title: Archivo de entorno
description: Importe el archivo de entorno de Postman y rellene las variables de proyecto de desarrollador y de zona protegida necesarias para las llamadas de API de bootcamp.
doc-type: article
solution: Experience Platform
exl-id: 1461fac5-0714-44d4-b5c8-949df6bcff83
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# Archivo de entorno

## Archivo de entorno de Postman

Descargar archivo: [AEP Bootcamp.postman_environment.json](assets/aep-bootcamp.postman_environment.json)



## Importar archivo de entorno

1. Abra `Environment File` desde arriba en el explorador haciendo clic en el archivo
1. Copie la dirección URL del archivo en el portapapeles
1. Inicie Postman en el equipo local y haga clic en el botón `Import` del área de trabajo
1. Pegue la dirección URL de `Environment File` en el cuadro de texto modal de importación de la superposición.  Esto debería almacenar en déclencheur una importación automática

![Haciendo clic en el botón Importar del área de trabajo de Postman para importar el archivo de entorno](assets/environment-file-click-import-button.png "Botón Importar")



![Pegando la dirección URL del archivo de entorno en el cuadro de texto modal de importación de Postman](assets/environment-file-import-modal-paste-url.png "Superposición del botón de importación")



Una vez importado, puede validar que el archivo de entorno existe haciendo clic en la pestaña `Environments` en la barra lateral izquierda.  Debería ver algo similar a lo siguiente.

![El entorno de Bootcamp de AEP aparece en la ficha Entornos de Postman después de importar](assets/environment-file-aep-bootcamp-environment-listed.png "El entorno de Bootcamp de AEP")



## Variables de entorno

Antes de poder realizar cualquier llamada de API, debe actualizar algunas de las variables del archivo de entorno que acaba de importar.  Se hace referencia a estas variables en las llamadas de API, por lo que debe asegurarse de que se rellenan correctamente.  Las variables se dividen en dos grupos:

- **Valores de proyecto de desarrollador** -> estas son las variables predeterminadas generadas a partir del proyecto de desarrollador que se crearon en Adobe Developer Console
- **Otros valores** -> son variables creadas a medida que un usuario suele crear para trabajar con las distintas API de Experience Platform

>[!NOTE]
>
>Estos valores provienen de la credencial de servidor a servidor OAuth que creó en [programa de instalación de Developer Console](../sandbox-setup/developer-console-setup.md#collect-your-values)



### Actualizar valores de proyectos de desarrollador

1. Haga clic en la ficha `Environments` en la barra lateral izquierda de Postman
1. Siguiente clic en el archivo de entorno `AEP Bootcamp`
1. Actualice `current values` para las siguientes variables:
   - CLIENT\_SECRET
   - CLIENT\_ID (también denominada CLAVE API)
   - TÉCNICO\_ACCOUNT\_ID
   - IMS\_ORG

Cuando termine, el archivo de entorno debería tener un aspecto similar al siguiente:

![Archivo de entorno después de actualizar los valores de CLIENT_SECRET, CLIENT_ID, TECHNICAL_ACCOUNT_ID e IMS_ORG](assets/environment-file-with-developer-project-values.png "Archivo de entorno con valores de proyecto para desarrolladores")

### Actualizar otros valores

Los únicos otros valores que deben actualizarse son la variable `SANDBOX_NAME` y la variable `TENANT_NAME`.

- `SANDBOX_NAME`: indica a Adobe Experience Platform en qué zona protegida se debe ejecutar
- `TENANT_NAME`: se usa para rellenar previamente el nombre del inquilino en llamadas XDM específicas

>[!NOTE]
>
>Si está trabajando en estos laboratorios a su propio ritmo (en lugar de un evento de formación en directo con un sandbox-assignment.pdf), puede encontrar ambos valores mientras está conectado a su zona protegida desde la URL de la interfaz de usuario de Adobe Experience Platform, por ejemplo:
>
>`https://experience.adobe.com/#/@dep/sname:prod/platform/home`
>
>- `SANDBOX_NAME` es el valor después de `sname:` — en este ejemplo, `prod`
>- `TENANT_NAME` es el valor después del símbolo `@`, con el prefijo guion bajo; en este ejemplo, `_dep`

1. Actualice `current values` para las siguientes variables:
   - SANDBOX\_NAME
   - TENANT\_NAME
1. Para guardar las actualizaciones, haga clic en el botón `Save` en la parte superior derecha del área de trabajo de entorno

Cuando haya terminado, el archivo de entorno debería tener este aspecto:

![Archivo de entorno después de actualizar los valores SANDBOX_NAME y TENANT_NAME](assets/environment-file-with-sandbox-name-and-tenant-name.png "Archivo de entorno con SANDBOX_NAME")

>[!TIP]
>
>¡Felicidades! Ha completado la configuración del entorno de Postman
