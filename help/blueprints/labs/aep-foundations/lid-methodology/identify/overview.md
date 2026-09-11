---
title: Identificar
description: 'Conozca el paso de identificación de dos partes de la metodología LID: etiquetado de los tipos de tabla restantes e identificación de los campos de identidad clave.'
doc-type: overview-page
solution: Experience Platform
exl-id: 83657cf0-db35-4d4d-8cfb-1934ff40baca
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# Identificar

## Objetivos de aprendizaje

El paso **Identificar** dentro de la metodología LID se divide en dos partes distintas:

1. Parte 1: Tipos de tabla restantes -> identifique las tablas sin etiquetar restantes y etiquete el tipo de desnormalización
1. Parte 2: Campos clave -> identifique los campos clave de las entidades principal y de soporte



Le enseñará a identificar los siguientes elementos dentro de un modelo relacional que necesitará para diseñar el perfil del cliente en tiempo real:

- Tablas de Bridge (tablas que administran relaciones &quot;varios a varios&quot;)
- Tablas que requerirán desnormalización
- Identidades principales dentro del perfil del cliente en tiempo real
- Identidades basadas en personas dentro de las clases de entidad principal que se pueden utilizar para identificar a una persona de forma exclusiva
- Identificadores de relación entre tablas de Perfil individual/Evento de experiencia y tablas de búsqueda asociadas
- Campos obligatorios necesarios para los esquemas de Experience Event
- Campos recomendados para perfiles individuales y esquemas de búsqueda
