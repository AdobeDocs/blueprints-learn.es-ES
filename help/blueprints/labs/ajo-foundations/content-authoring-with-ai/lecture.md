---
title: Conferencia
description: Explore el modelo de anatomía de contenido de cuatro capas, los patrones de integración de contenido de AJO y AEM y el control de contenido asistido por IA para la personalización a escala.
doc-type: article
solution: Experience Platform
exl-id: 1ac39a70-51f8-426e-97cf-1ff08450d326
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# Conferencia

## Objetivos de aprendizaje

- Explicar por qué el contenido, no los datos ni los recorridos, es la restricción principal en los programas de personalización a escala
- Describa el modelo de anatomía de contenido de cuatro capas: recursos, fragmentos, plantillas y mensajes
- Diferenciar entre fragmentos de AJO y fragmentos de contenido de AEM, incluido cómo gestiona cada uno la propagación
- Asigne las fases del ciclo vital de contenido de creación, almacenamiento, administración, control, activación y medición
- Compare los tres patrones de integración de contenido: AJO independiente, AJO + AEM Assets y AJO + GenStudio for Performance Marketing
- Identificar las señales arquitectónicas que indican cuándo escalar de un patrón al siguiente
- Describa los tres niveles de capacidad de IA en la pila de Adobe: el asistente de contenido, los modelos personalizados de Firefly y el servicio de marca unificado
- Explicar el principio de supervisión en bucle en flujos de trabajo de contenido asistido por IA
- Distinguir la verdadera personalización de la inserción de nombre o la multiplicación de recursos

## Vídeo

En este vídeo aprenderá el modelo de anatomía de contenido de cuatro capas, los tres patrones de integración de contenido de AJO y cómo las capacidades de IA encajan en un sistema de contenido gobernado.

>[!VIDEO](https://video.tv.adobe.com/v/3491063/?quality=12&learn=on)

## Puntos clave

Personalization a escala depende de tres pilares: contenido, datos y recorridos. La mayoría de las empresas invierten mucho en datos y en la orquestación de recorridos, pero consideran el contenido como una idea tardía, por lo que el contenido es el lugar en el que los programas de personalización se rompen primero. Para un arquitecto de AJO, comprender cómo estructurar el contenido como un sistema gobernado, en lugar de una pila de recursos únicos, es lo que separa una implementación escalable de una que se colapsa bajo su propia expansión de plantillas.

**En esta lección ha explicado:**

- La tesis: la personalización no falla debido a los datos, falla porque el contenido no está diseñado como sistema
- La anatomía de contenido de cuatro capas: Assets (medios atómicos en DAM), Fragmentos (bloques visuales o de expresión reutilizables), Plantillas (zonas bloqueadas o editables) y Mensajes (la salida final ensamblada y lista para el canal)
- El ciclo de vida del contenido: crear, almacenar, administrar, gobernar, activar, medir y cómo los errores se producen en cascada de izquierda a derecha cuando se omite un paso
- Patrón 1, AJO independiente: mejor para un solo mercado, de un solo canal, con menos de 50 variantes, cuando la velocidad es la restricción principal; utiliza AEM Assets Essentials como DAM agrupado básico
- Los fragmentos de AJO se almacenan en AJO y se copian en plantillas como duplicados, sin actualizaciones automáticas y con un límite de 30 fragmentos/1 nivel de anidamiento
- Patrón 2, AJO + AEM: mejor para múltiples mercados, más de 50 variantes, cuando la gobernanza es la restricción principal; AEM se convierte en el sistema de registro, AJO el sistema de activación
- AJO hace referencia a los fragmentos de contenido de AEM (no se copian), por lo que las actualizaciones se propagan instantáneamente en todas las plantillas, recorridos y campañas de referencia
- Tres escenarios que rompen silenciosamente la propagación del fragmento: herencia dañada (fragmento desbloqueado), nuevos atributos de personalización añadidos a un fragmento publicado y restricciones de etiqueta de Control de acceso de nivel de objeto (OLAC)
- Patrón 3, AJO + GenStudio for Performance Marketing: mejor para la escala de producción y la generación de variantes de gran volumen; requiere la gobernanza del patrón 2 como requisito previo estricto
- Los cuatro pilares que mantienen la generación de IA en la marca: Unified Brand Service, Content Credentials, depuración en bucle e integración con AJO
- La matriz de decisiones arquitectónicas y el modelo de madurez de Content Supply chain (niveles 1 ad hoc a 5 autónomos) para diagnosticar dónde se encuentra un cliente hoy
- La personalización verdadera es la variación inteligente dentro de una sola plantilla controlada, no los campos de combinación de nombre ni las campañas independientes por segmento
