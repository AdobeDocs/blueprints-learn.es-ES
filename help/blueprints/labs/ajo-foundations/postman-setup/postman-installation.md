---
title: Instalación de Postman
description: Instale Postman y familiarícese con sus colecciones, entornos e interfaz de espacio de trabajo antes de realizar llamadas de API en laboratorios posteriores.
doc-type: article
solution: Experience Platform
exl-id: c277edb5-f758-4955-bcd7-b15a9b9ab949
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Instalación de Postman

## Objetivo

Al final de este laboratorio, podrá instalar Postman, configurar un espacio de trabajo y un entorno básicos para poder realizar las llamadas de API posteriores que necesiten los futuros laboratorios.

>[!IMPORTANT]
>
>Se requiere Postman para varios laboratorios en este curso.  Incluso si ya ha instalado Postman, deberá completar este laboratorio para asegurarse de que ha instalado y configurado correctamente los archivos de entorno y la colección de API.



## Instalación de Postman

Vaya al sitio web de Postman y descargue la aplicación de Postman o utilice la versión web —> [https://www.postman.com/download/](https://www.postman.com/download/)

![Página de descarga de Postman en el sitio web de Postman](assets/postman-installation-postman-download.png)

## Crear un espacio de trabajo de Postman (opcional)

Si eres *nuevo en Postman* y esta es tu primera instalación, entonces no necesitas crear un nuevo espacio de trabajo. En el primer inicio, elija continuar sin iniciar sesión y utilizará el cliente ligero que no requiera espacio de trabajo.

Si *ya está familiarizado con Postman* y lo tiene instalado, es probable que ya haya iniciado sesión y tenga varios espacios de trabajo. En ese caso, le recomendamos que cree un nuevo espacio de trabajo para *este bootcamp*. Encontrará instrucciones en el [sitio web de Postman.](https://learning.postman.com/docs/collaborating-in-postman/using-workspaces/create-workspaces/)

## Interfaz de Postman

Abra Postman y familiarícese rápidamente con algunas áreas de la aplicación. Para trabajar con Experience Platform, solo necesitamos centrarnos en unas pocas áreas clave de la aplicación.

![Información general sobre la interfaz de Postman con la barra lateral, el encabezado y el área de trabajo principal denominada](assets/postman-installation-interface-overview.png "Interfaz de Postman")

## Barra lateral

La barra lateral es lo que le permite navegar rápidamente por los diferentes elementos de Postman. Durante los laboratorios, solo utilizará los dos elementos siguientes:

**Colecciones**: grupos de solicitudes guardadas que se pueden importar desde una ubicación externa o crear por su cuenta.

**Entornos**: un conjunto de variables a las que puede hacer referencia en sus solicitudes de Postman. En Experience Platform, puede considerar los entornos de Postman como sinónimos de los entornos limitados de Adobe dentro de una organización de IMS. Utilizaremos la función del Entorno en Postman



## Header

Espacios de trabajo: permiten organizar el trabajo en varias agrupaciones (es decir, proyectos, equipos, etc.)



## Área de trabajo principal

El área de trabajo principal es donde realizará la mayor parte del trabajo cuando trabaje en Postman. Todas las solicitudes de API se exponen en una pestaña específica dentro del área de trabajo principal.

**Barra lateral derecha**: proporciona acceso adicional a las herramientas según la ficha seleccionada actualmente. Algunos ejemplos son la documentación de la solicitud, los comentarios y los fragmentos de código, por nombrar algunas funciones.

**Selector de entorno**: le permite cambiar rápidamente entre diferentes entornos para acceder a variables preconfiguradas al trabajar con API. Al trabajar con Experience Platform, aprovechará esto al trabajar con una zona protegida de AEP específica dentro de la organización de IMS asignada.



## Pie

En la parte inferior de la aplicación de Postman, encontrará un conjunto de funciones que le permiten ver rápidamente los registros de las llamadas que realizó, el acceso rápido para buscar y reemplazar, y varias otras funciones.



## Resumen

Ahora debería tener Postman instalado y comprender algunos conceptos básicos de la interfaz de usuario
