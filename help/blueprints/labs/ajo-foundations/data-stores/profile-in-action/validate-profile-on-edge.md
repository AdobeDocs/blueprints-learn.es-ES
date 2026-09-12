---
title: Validar perfil en Edge
description: Obtenga información sobre cómo comprobar el almacén de perfiles de Edge y la pestaña Pertenencia a audiencias para confirmar el estado de un perfil en la red de Edge.
doc-type: article
solution: Experience Platform
exl-id: f82ceba7-6916-49ff-8776-2d0238560df8
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---


# Validar perfil en Edge

## Objetivo de aprendizaje

Confirme que el perfil no existe en el almacén de perfiles de red de Edge.

## Compruebe el perfil de Edge

1. Haga clic en la ficha **Atributos** y en el botón de opción **Edge** para ver el perfil de Edge

   ![Perfil de Edge mostrado en la ficha Atributos](assets/validate-profile-on-edge-attributes-tab.png)

   >[!NOTE]
   >
   >Es posible que vea una versión &quot;depurada&quot; del perfil que consista únicamente en las identidades, dependiendo de cuánto tiempo haya pasado.



2. Haga clic en la pestaña Pertenencia a audiencias.  Estará **en blanco**.

![Pestaña Pertenencia a audiencia vacía en el perfil de Edge](assets/validate-profile-on-edge-empty-audience-membership-tab.png)

>[!NOTE]
>
>**¿Por qué no hay pertenencia a Edge?**
>
>¿No deberíamos haber visto **dep: Cualquier evento Edge (dentro de la hora)** califica?
>
>A pesar de que tenemos una audiencia que tiene una evaluación de Edge, esa audiencia no existe en Edge porque no tenemos razón para ello ahí fuera... todavía.
>
>Si se utilizara esa audiencia (por ejemplo, Decisioning o Destinations), las reglas de audiencia se insertan en Edge y la próxima vez que un evento se transmita a Edge, se evaluará esa audiencia.
>
>Además, no activamos los servicios de segmentación de Edge.



## Resumen

El perfil no existe en Edge (todavía)
