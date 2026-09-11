---
title: Acceso a zona protegida
description: Compruebe que el entorno de Postman puede recuperar correctamente la zona protegida de Experience Platform asignada antes de iniciar los laboratorios.
doc-type: article
solution: Experience Platform
exl-id: c841e497-a695-4d3f-85e6-d653478cad1e
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# Acceso a zona protegida

Antes de continuar, compruebe que su acceso sea legítimo. Siga estos pasos:

1. Abra la carpeta `Check Sandbox Access` y haga clic en la llamada `Retrieve Your Sandbox`
1. A continuación, en la esquina superior derecha de Postman, verá un cuadro desplegable Entorno.  Asegúrese de seleccionar el entorno `AEP Bootcamp`
1. Ejecute la llamada haciendo clic en el botón `Send`

![Panel de solicitud de Postman para la llamada a Recuperar la zona protegida antes de enviar](assets/sandbox-access-check-sandbox-request.png "Recupere la llamada a la API de la zona protegida")



Una respuesta correcta tiene este aspecto:

![200 Respuesta correcta que confirma la recuperación correcta de la zona protegida asignada](assets/sandbox-access-successful-response.png "200 Correcta Solicitud correcta de zona protegida")

>[!NOTE]
>
>El valor **name** debe coincidir con la variable sandbox\_name de su entorno de Postman

>[!TIP]
>
>¡Felicidades!  Está listo para empezar a usar las API de Experience Platform
