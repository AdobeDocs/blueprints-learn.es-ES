---
title: Recomendación de comportamiento
description: Obtenga información sobre cómo generar recomendaciones de elementos y contenido mediante estrategias de selección y modelos de clasificación.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '7626'
ht-degree: 2%

---


# Recomendación de comportamiento

Esta guía explica cómo implementar recomendaciones de contenido y productos de comportamiento mediante [!DNL Adobe Journey Optimizer] (AJO) Decisioning, [!DNL Real-Time Customer Data Platform] (RT-CDP) y [!DNL Adobe Experience Platform] (AEP). Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesitan ofrecer experiencias de recomendación personalizadas en canales web, de aplicaciones móviles y de correo electrónico.

Presenta todas las opciones de implementación viables, consideraciones de decisión en cada fase y vínculos a la documentación de [!DNL Adobe Experience League]. Behavioral Recommendations genera recomendaciones de nivel de elemento o de nivel de contenido mediante señales de comportamiento (vistas de producto, compras, interacciones de contenido, consultas de búsqueda) combinadas con estrategias de selección y modelos de clasificación de AJO Decisioning. A diferencia de Offer Decisioning, que selecciona entre un conjunto seleccionado de ofertas de marketing utilizando reglas de elegibilidad explícitas, este patrón funciona en catálogos de artículos grandes (productos, artículos, vídeos) y utiliza señales de afinidad de comportamiento y clasificación basada en ML para mostrar los artículos más relevantes para cada visitante.

## Resumen del caso de uso

Las organizaciones con catálogos de productos, bibliotecas de contenido o bibliotecas de medios deben mostrar los elementos más relevantes para cada visitante en función de su historial de comportamiento y de la actividad de la sesión. Ya sea un carrusel &quot;recomendado para usted&quot; en una página de inicio, un widget de venta cruzada en una página de detalles del producto o las recomendaciones de productos incrustadas en una campaña de correo electrónico, el desafío subyacente es el mismo: combine el perfil de comportamiento de cada visitante con los artículos más relevantes de un catálogo y, a continuación, envíe esas recomendaciones en el canal correcto en el momento adecuado.

Este patrón aborda ese desafío mediante la ingesta de señales de comportamiento en tiempo real mediante [!DNL Web SDK] o [!DNL Mobile SDK], el procesamiento mediante estrategias de selección de AJO Decisioning que combinan atributos de elemento con contexto de comportamiento y la entrega de los elementos recomendados a través de canales web, en la aplicación o de correo electrónico. Los modelos de clasificación pueden basarse en fórmulas (por ejemplo, ordenar por puntuación de afinidad de categoría) o en una clasificación de IA (por ejemplo, modelo de recomendación personalizado). El patrón también gestiona escenarios de inicio en frío para nuevos visitantes sin historial de comportamiento configurando recomendaciones de reserva.

La audiencia a la que se dirige este patrón incluye equipos de comercialización de comercio electrónico, equipos de personalización de contenido y equipos de experiencia digital que buscan mejorar la participación, la conversión y el valor promedio de los pedidos a través de recomendaciones personalizadas impulsadas por el comportamiento real del usuario.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### [Aumentar los ingresos de ventas cruzadas y ventas adicionales](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)

Promocione productos o servicios complementarios y de primera calidad a los clientes existentes en función del comportamiento y el historial de compras.

| KPI | Descripción |
| --- | --- |
| Porcentaje de ampliación de venta/venta cruzada | Porcentaje de clientes que compran artículos complementarios o premium recomendados |
| Ingresos incrementales | Ingresos adicionales atribuibles a compras impulsadas por recomendaciones |
| Valor de duración del cliente | Aumento de valor a largo plazo gracias a una mayor participación del producto |

### [Aumentar las tasas de conversión](../../business-objectives/revenue-monetization/increase-conversion-rates.md)

Mejore el porcentaje de visitantes y clientes potenciales que completan las acciones deseadas, como compras, suscripciones o envíos de formularios.

| KPI | Descripción |
| --- | --- |
| Tasas de conversión | Porcentaje de visitantes que realizan la conversión después de interactuar con las recomendaciones |
| Conversión de cliente potencial | Velocidad a la que los visitantes comprometidos con la recomendación se convierten en clientes |
| Coste por posible cliente | Reducción del coste de adquisición mediante la participación en recomendaciones orgánicas |

### [Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo de vida individuales.

| KPI | Descripción |
| --- | --- |
| Participación | Frecuencia de interacción con superficies de recomendación (clics, vistas, complementos al carro de compras) |
| Tasas de conversión | Alza en las tasas de conversión para visitantes comprometidos con la recomendación frente a control |
| Satisfacción del cliente (CSAT) | Mejora de la satisfacción del cliente gracias a experiencias relevantes y personalizadas |

## Casos de uso tácticos de ejemplo

Las siguientes son implementaciones tácticas comunes de este patrón:

- Widget de venta cruzada de productos en la página de detalles del producto (&quot;los clientes también compraron&quot;)
- Carrusel &quot;Recomendado para usted&quot; en la página principal en función del historial del explorador
- Recomendaciones de contenido en sitios multimedia según el comportamiento de lectura
- Widget de &quot;Artículos vistos recientemente&quot; combinado con elementos similares
- Recomendaciones de productos complementarios posteriores a la compra
- Enviar por correo electrónico recomendaciones de productos basadas en afinidad de comportamiento
- Recomendaciones específicas por categoría basadas en el comportamiento de exploración dentro de la sesión
- Volver a clasificar los resultados de búsqueda según las señales de comportamiento

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir la eficacia de las implementaciones de recomendaciones de comportamiento.

| KPI | Método de medición |
| --- | --- |
| Tasa de clics en recomendaciones (CTR) | Clics en artículos recomendados divididos por impresiones de recomendación |
| Tasa de conversión de recomendaciones | Compras o acciones deseadas desde clics en recomendaciones divididas por el total de clics en recomendaciones |
| Ingresos influidos por Recommendations | Ingresos totales de pedidos que incluyeron al menos un producto basado en recomendaciones |
| Alza del valor de pedido promedio (AOV) | Aumento en AOV para sesiones que se comprometieron con recomendaciones en comparación con sesiones sin recomendaciones |
| Artículos por pedido | Número de artículos por pedido para las sesiones dedicadas a recomendaciones |
| Cobertura de recomendación | Porcentaje de vistas de página o sesiones aptas que recibieron recomendaciones personalizadas (no de reserva) |
| Tasa de reserva de inicio en frío | Porcentaje de solicitudes de recomendación atendidas por lógica de reserva debido a un historial de comportamiento insuficiente |

## Patrón de caso de uso

**Recomendación de comportamiento**

Genere recomendaciones de nivel de elemento o de nivel de contenido basadas en señales de comportamiento, utilizando estrategias de selección de AJO Decisioning y modelos de clasificación para servir contenido contextual.

**Cadena de funciones:** Ingesta de señal de comportamiento > Evaluación de estrategia de toma de decisiones > Entrega de recomendaciones > Informes

Consulte la sección Composición del patrón en Consideraciones de implementación para obtener instrucciones sobre cómo combinar patrones.

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Adobe Journey Optimizer] (AJO) Decisioning**: Estrategias de selección, modelos de clasificación, catálogos de elementos y políticas de decisión que evalúan las señales de comportamiento y devuelven los elementos más relevantes para cada visitante
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)**: acumulación de datos de perfil de comportamiento, evaluación de audiencia para ámbitos de recomendación y atributos calculados para puntuación de afinidad de comportamiento
- **[!DNL Adobe Experience Platform] (AEP)** — Ingesta de evento de comportamiento a través de [!DNL Web SDK] y [!DNL Mobile SDK], procesamiento de [!DNL Edge Network], administración de esquema XDM para datos de catálogo y evento

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Se asume en contexto | Zona protegida de AJO con permisos de Decisioning habilitados. Funciones de usuario aprovisionadas con acceso a la administración del catálogo de elementos, la configuración de la estrategia de selección y la administración de superficies de canal. | [Resumen de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home), [Resumen de control de acceso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | Esquema de Experience Event que captura señales de comportamiento (vistas de productos, complementos al carro de compras, compras, interacciones de contenido) con identificadores de artículo/producto. Esquema del catálogo de artículos (atributos de producto, categorías, imágenes, precios) para el conjunto de artículos de recomendación. Esquema de perfil con campos de identidad. Todos los esquemas habilitados para [!DNL Real-Time Customer Profile]. | [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [Conceptos básicos de composición de esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition), [Crear un conjunto de datos](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/create) |
| Fuentes de datos y recopilación | Requerido | La transmisión de eventos de comportamiento en tiempo real a través de [!DNL Web SDK] o [!DNL Mobile SDK] es crítica; la calidad de la recomendación depende de nuevas señales de comportamiento. Los datos del catálogo de artículos deben ingerirse (por lotes o streaming). Flujos de datos configurados con el servicio AJO habilitado para Edge Decisioning. | [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Información general de Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview), [Configurar flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Configuración de identidad y perfil | Requerido | Las señales de comportamiento deben asociarse con una identidad (conocida o anónima a través de ECID) para crear perfiles de comportamiento. Para las recomendaciones de visitantes conocidos, se debe configurar una identidad autenticada (ID de CRM, correo electrónico). Política de combinación activa en Edge para la entrega de recomendaciones en tiempo real. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Introducción a las políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Definición de audiencia y segmentación | Recomendado | Las audiencias pueden utilizarse para aplicar recomendaciones (por ejemplo, recomendar solo productos Premium a los miembros Premium) o para filtrar. No es estrictamente necesario si las recomendaciones son puramente de comportamiento. Necesario para que las recomendaciones basadas en correo electrónico (Opción C) definan la audiencia de destino. | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Guía de la interfaz de usuario del generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Los atributos calculados, como las puntuaciones de afinidad de la categoría, la frecuencia de interacción del producto, la actualización de la compra y el gasto total, mejoran la calidad de la clasificación de recomendaciones. [!DNL Customer AI] las puntuaciones de tendencia pueden mejorar aún más la relevancia al predecir la probabilidad de compra. | [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Resumen de inteligencia artificial aplicada al cliente](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Administración del ciclo de datos | Recomendado | Los datos de evento de comportamiento deben tener políticas de caducidad adecuadas; la relevancia de la recomendación se degrada con datos antiguos. La configuración de directivas de caducidad de conjuntos de datos en conjuntos de datos de evento de comportamiento garantiza la actualización y administra el almacenamiento. La aplicación del consentimiento garantiza el uso compatible de los datos de comportamiento. | [Caducidad de conjuntos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration), [información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Etiquetado y aplicación del uso de datos | Recomendado | Las etiquetas de gobernanza en los datos de comportamiento garantizan el uso compatible del historial de interacciones para las recomendaciones. Especialmente importante cuando los datos de comportamiento incluyen patrones de navegación, historial de compras o señales de interés de productos financieros/de salud. | [Resumen de control de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Resumen de etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview) |
| Monitorización y observabilidad | Recomendado | Se debe monitorizar la latencia de entrega de Recommendations, las tasas de reserva y el estado de ingesta del catálogo de artículos. Las alertas sobre errores de ingesta de eventos de comportamiento y errores de toma de decisiones ayudan a mantener la calidad de la recomendación. | [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home), [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview) |
| Informes y análisis | Incluido | Los informes de rendimiento de recomendaciones forman parte del paso 4 de la cadena de funciones. [!DNL Customer Journey Analytics] el análisis de la eficacia de las recomendaciones, el impacto en los ingresos y el rendimiento de nivel de elemento en todas las superficies y segmentos proporciona perspectivas de optimización. | [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del Catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Journey Optimizer] (AJO)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Decisioning | Configuración de estrategia de selección y catálogo de elementos | Configure catálogos de elementos (elementos de decisión), estrategias de selección con modelos de clasificación de comportamiento, reglas de filtrado y recomendaciones de reserva |
| Configuración de canal | Configuración de canales y superficies | Configure las superficies de envío para los canales web (experiencias basadas en código), en la aplicación, de tarjeta de contenido o de correo electrónico en los que se procesarán las recomendaciones |
| Creación de mensajes | Configuración de contenido y envío | Diseñar plantillas de renderización de recomendaciones, diseños de visualización de elementos y expresiones de personalización para artículos recomendados |
| Informes y análisis de rendimiento | Informes y optimización | Monitorice las métricas de clics, conversiones e ingresos de recomendaciones mediante los informes nativos de AJO y la integración de [!DNL Customer Journey Analytics] |

### [!DNL Real-Time CDP] (RT-CDP)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Evaluación de audiencia | Ámbito de audiencia (opción C) | Evaluar los segmentos de audiencia utilizados para definir el ámbito de las recomendaciones o la población objetivo para las campañas de recomendaciones por correo electrónico |
| Enriquecimiento de perfiles | Enriquecimiento de señal de comportamiento | Enriquezca los perfiles con atributos calculados (puntuaciones de afinidad de la categoría, frecuencia de interacción) que mejoren la clasificación de las recomendaciones |

## Prerrequisitos

Complete lo siguiente antes de comenzar la implementación:

- AJO Decisioning está aprovisionado y habilitado en la zona protegida de Target
- [!DNL Web SDK] o [!DNL Mobile SDK] está implementado y recopilando eventos de comportamiento con identificadores de producto/contenido
- Los datos del catálogo de productos o de contenido están disponibles para su ingesta (nombre del producto, categoría, precio, URL de imagen, disponibilidad)
- Los esquemas de eventos de comportamiento incluyen identificadores de artículo/producto que se vinculan a elementos de catálogo
- La secuencia de datos está configurada con el servicio [!DNL Adobe Journey Optimizer] habilitado (requerido para Edge Decisioning)
- Se ha configurado la política de combinación con `isActiveOnEdge: true` (necesaria para las recomendaciones de aplicaciones/web en tiempo real)
- Para recomendaciones de correo electrónico (Opción C): la superficie de canal de correo electrónico se configura y valida
- Para recomendaciones por correo electrónico (Opción C): la audiencia de destino se define y evalúa

## Opciones de implementación

Las siguientes opciones describen diferentes enfoques para implementar recomendaciones de comportamiento. Elija la opción que mejor se adapte a sus requisitos de canal y restricciones técnicas.

### Opción A: recomendaciones en tiempo real para web

**Ideal para:** Recomendaciones de productos o contenido en páginas web: widgets de venta cruzada de páginas de detalles de productos, carruseles de recomendaciones de páginas de inicio, listados personalizados de páginas de categorías y personalización de resultados de búsqueda.

**Cómo funciona:**

Las señales de comportamiento se recopilan en tiempo real mediante [!DNL Web SDK] a medida que los visitantes navegan por el sitio. Cada vista de página, interacción de producto o consulta de búsqueda se transmite a AEP y se asocia con el perfil del visitante (a través de ECID para visitantes anónimos o identidad autenticada para visitantes conocidos). Cuando se carga una página que contiene una superficie de recomendación, [!DNL Web SDK] solicita una evaluación de toma de decisiones de AJO a través de [!DNL Edge Network]. El motor de decisión evalúa el perfil de comportamiento del visitante con respecto a la estrategia de selección, aplica la lógica de clasificación, filtra los elementos no aptos (ya adquiridos, sin existencias) y devuelve los elementos recomendados.

Las recomendaciones se representan en la página a través de experiencias basadas en código o superficies de canales web. La renderización puede ser un carrusel, una cuadrícula, un widget de un solo elemento o cualquier diseño personalizado definido en la plantilla de recomendación. Los eventos de impresión y clics se rastrean automáticamente en AEP para la creación de informes de rendimiento.

**Consideraciones clave:**

- Edge Decisioning requiere que la política de combinación esté activa en Edge
- La latencia de la recomendación depende del tiempo de respuesta de [!DNL Edge Network] (SLA inferior a 500 ms para solicitudes de un solo ámbito)
- Los visitantes anónimos reciben recomendaciones basadas en el comportamiento de la sesión; los visitantes conocidos se benefician del historial de comportamiento entre sesiones
- Los visitantes de inicio en frío sin historial de comportamiento reciben recomendaciones de reserva

**Ventajas:**

- Personalización en tiempo real basada en el comportamiento en la sesión
- Envío de recomendación de subsegundo a través de [!DNL Edge Network]
- Funciona tanto para visitantes anónimos como conocidos
- Impresión automática y rastreo de clics
- No se requiere volver a cargar la página para recomendaciones nuevas

**Limitaciones:**

- El almacén de perfiles de Edge contiene un subconjunto de atributos de perfil completos
- Los modelos de clasificación complejos con muchos atributos de perfil pueden requerir una evaluación en el centro
- Requiere implementación [!DNL Web SDK] con seguimiento de eventos de comportamiento

**Experience League:**

- [Entrega de ofertas mediante la API de Edge Decisioning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)

### Opción B: recomendaciones de aplicaciones móviles

**Ideal para:** recomendaciones de productos en la aplicación, fuentes de contenido personalizadas, recomendaciones basadas en notificaciones y experiencias de comercio móvil.

**Cómo funciona:**

Las señales de comportamiento se recopilan a través de [!DNL Mobile SDK] a medida que los usuarios interactúan con la aplicación. Las vistas de productos, las interacciones de contenido, las búsquedas y las compras se transmiten a AEP. Cuando se carga una pantalla que contiene una superficie de recomendación, [!DNL Mobile SDK] solicita una evaluación de toma de decisiones. Las recomendaciones se entregan mediante mensajes en la aplicación, tarjetas de contenido o experiencias basadas en código dentro de la aplicación móvil.

Las tarjetas de contenido son especialmente adecuadas para casos de uso de recomendaciones en aplicaciones móviles, ya que persisten en una experiencia similar a una fuente que los usuarios pueden examinar según les convenga. Los mensajes en la aplicación se pueden utilizar para recomendaciones contextuales activadas por comportamientos específicos (por ejemplo, mostrar productos complementarios después de agregar un elemento al carro de compras).

**Consideraciones clave:**

- [!DNL Mobile SDK] debe configurarse con el seguimiento de eventos de comportamiento para las interacciones relevantes
- Las tarjetas de contenido proporcionan una superficie de recomendación persistente; los mensajes en la aplicación son efímeros
- El seguimiento de comportamiento sin conexión requiere la administración de colas de SDK para el envío de eventos diferidos
- Los ciclos de actualización de la tienda de aplicaciones afectan a la rapidez con la que se pueden implementar cambios de procesamiento de recomendaciones

**Ventajas:**

- Experiencia móvil nativa con procesamiento de recomendaciones suave integrado en la aplicación
- Las tarjetas de contenido proporcionan una fuente de recomendaciones persistente y explorable
- Los mensajes en la aplicación permiten recomendaciones contextuales y activadas por el comportamiento
- Aprovecha las señales a nivel de dispositivo (ubicación, patrones de uso de la aplicación) para lograr una relevancia mejorada

**Limitaciones:**

- Requiere integración de [!DNL Mobile SDK] y recursos de desarrollo de aplicaciones
- Los cambios de procesamiento requieren actualizaciones de la aplicación (a menos que se utilicen experiencias basadas en código con diseños impulsados por el servidor)
- Los periodos sin conexión crean lagunas en la recopilación de señales de comportamiento

**Experience League:**

- [Información general de Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Opción C: recomendaciones de comportamiento por correo electrónico

**Recomendado para:** Recomendaciones de productos en campañas de correo electrónico: correos electrónicos de navegación abandonados con recomendaciones de productos vistos, correos electrónicos de venta cruzada posteriores a la compra, resúmenes periódicos de &quot;selecciones para ti&quot; y correos electrónicos de renovación de participación con sugerencias de productos personalizadas.

**Cómo funciona:**

Los datos de perfil de comportamiento acumulados de sesiones anteriores informan la selección de recomendaciones en el momento de envío del correo electrónico o en el momento de procesamiento. Una audiencia se define para dirigirse a los destinatarios adecuados (por ejemplo, visitantes que navegaron pero no compraron, clientes que realizaron una compra reciente). Se configura una campaña o un recorrido para enviar un correo electrónico que incluya ubicaciones de recomendaciones. En el momento del envío, AJO Decisioning evalúa el perfil de comportamiento de cada destinatario con respecto a la estrategia de selección e inserta los elementos recomendados en el contenido del correo electrónico.

Esta opción se basa en el historial de comportamiento acumulado en lugar de en las señales de la sesión. Los atributos calculados (puntuaciones de afinidad de la categoría, vistas recientes del producto, frecuencia de compra) mejoran significativamente la calidad de las recomendaciones por correo electrónico, ya que destilan el historial de comportamiento en señales de nivel de perfil que la estrategia de selección puede evaluar de forma eficaz.

**Consideraciones clave:**

- Las recomendaciones de correo electrónico se evalúan en el momento de la entrega, no en el momento de la apertura (el estado del perfil de comportamiento en el momento de la entrega determina las recomendaciones)
- Se recomiendan los atributos calculados para mejorar la calidad de la clasificación
- Las limitaciones de procesamiento de correo electrónico (sin JavaScript y CSS limitado) limitan los formatos de visualización de recomendaciones
- Requiere una superficie de canal de correo electrónico configurada y validada

**Ventajas:**

- Aprovecha el historial de comportamiento completo en todas las sesiones para conseguir una personalización más profunda
- Se integra con los flujos de trabajo de campaña y recorrido existentes
- Efectivo para escenarios de renovación de participación y recuperación en los que los puntos de contacto web/aplicación no están disponibles
- Puede incluir varias ubicaciones de recomendaciones en un solo correo electrónico

**Limitaciones:**

- Las recomendaciones son estáticas en el momento del envío y no se actualizan cuando se abre el correo electrónico
- Las restricciones de procesamiento de correo electrónico limitan los formatos de visualización de recomendaciones
- Requiere evaluación de audiencia e infraestructura de orquestación de campaña/recorrido
- Mayor complejidad de la implementación debido a dependencias adicionales (configuración del canal, definición de audiencia, ejecución de campañas)

**Experience League:**

- [Crear un correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Comparación de opciones

En la tabla siguiente se resumen las principales diferencias entre las opciones de implementación.

| Criterios | Opción A: Tiempo real web | Opción B: aplicación móvil | Opción C: comportamiento del correo electrónico |
| --- | --- | --- | --- |
| Mejor para | Recomendaciones de página web (PDP, página principal, categoría) | Recomendaciones en la aplicación y fuentes de contenido | Campañas de correo electrónico con recomendaciones de productos |
| Fuente de señal de comportamiento | En la sesión + entre sesiones ([!DNL Web SDK]) | Interacciones en la aplicación ([!DNL Mobile SDK]) | Antecedentes de comportamiento acumulados (perfil) |
| Latencia de recomendación | Subsegundo ([!DNL Edge Network]) | Subsegundo ([!DNL Edge Network]) | En el momento del envío (evaluación del lado del concentrador) |
| Tipo de visitante | Anónimo y conocido | Conocidos (usuarios de la aplicación) | Conocidos (destinatarios de correo electrónico) |
| Complejidad | Medio | Medium-High | Alta |
| Dependencia del canal | [!DNL Web SDK], superficie de experiencia basada en código | [!DNL Mobile SDK], superficie de la tarjeta de contenido/en la aplicación | Superficie del canal de correo electrónico, audiencia, campaña o recorrido |
| Requiere | implementación [!DNL Web SDK], política de combinación de Edge | implementación [!DNL Mobile SDK], política de combinación de Edge | Superficie del correo electrónico, definición de audiencia, configuración de campaña |

### Elija la opción correcta

Siga estas instrucciones para seleccionar la mejor opción para su situación:

- **Comience con la opción A** si su objetivo principal son las recomendaciones de productos en tiempo real en su sitio web. Este es el punto de partida más común y proporciona un valor inmediato con la complejidad de implementación más baja.
- **Elija la opción B** si su aplicación móvil es un canal de participación principal y las recomendaciones en la aplicación podrían impulsar un aumento significativo de la conversión. La opción B se puede ejecutar en paralelo con la opción A utilizando las mismas estrategias de selección y catálogos de artículos.
- **Agregue la opción C** cuando desee ampliar las recomendaciones de comportamiento a las campañas de correo electrónico. Normalmente, se coloca por encima de la opción A o B, utilizando los mismos catálogos de elementos y estrategias de selección, pero con plantillas de renderización específicas del correo electrónico y segmentación basada en la audiencia.
- **Combine las opciones A + C** para un patrón común: recomendaciones web en tiempo real para visitantes activos, además de recomendaciones de navegación abandonada o correo electrónico posterior a la compra para visitantes que se van sin convertir.

## Fases de implementación

Las siguientes fases le guían a través de la implementación integral de recomendaciones de comportamiento.

### Fase 1: Configurar el esquema de evento de comportamiento y la recopilación de datos

**Función de la aplicación:** AEP: Modelado y preparación de datos (F2), AEP: Fuentes de datos y recopilación (F3)

Esta fase establece los esquemas XDM, los conjuntos de datos y los mecanismos de recopilación de datos que capturan señales de comportamiento y datos del catálogo de elementos. Esta base de datos es de lo que depende toda la lógica de recomendación.

#### Decisión: diseño de esquema de evento de comportamiento

¿Qué señales de comportamiento deben impulsar las recomendaciones?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo vistas de producto | Recomendaciones sencillas de venta cruzada/ampliación de ventas | Menor esfuerzo de implementación; profundidad de señal limitada |
| Vistas de productos + compras | Recomendaciones con exclusión de compras y lógica de venta cruzada | Moderar esfuerzo; habilita el filtrado &quot;excluir ya comprado&quot; |
| Grupo de comportamiento completo (vistas, compras, complemento al carro, búsquedas, interacciones de contenido) | Recomendaciones sofisticadas con clasificación de varias señales | Máxima calidad de señal; requiere instrumentación [!DNL Web SDK]/[!DNL Mobile SDK] completa |

#### Decisión: método de ingesta del catálogo de artículos

¿Cómo se incorporará el producto o el catálogo de contenido en AEP?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Ingesta por lotes mediante el conector de origen | Las actualizaciones de catálogo son periódicas (diarias/semanales) | Configuración más sencilla; los cambios del catálogo no se reflejan en tiempo real |
| Ingesta por streaming | El catálogo requiere actualizaciones casi en tiempo real (cambios de precio, disponibilidad) | Más complejo; garantiza que las recomendaciones reflejen el inventario actual |
| Carga manual/API | Catálogo pequeño con cambios poco frecuentes | Configuración más sencilla; no escalable para catálogos grandes o dinámicos |

**Navegación de la interfaz de usuario:** Administración de datos > Esquemas > Crear esquema; Recopilación de datos > Flujos de datos > Nuevo flujo de datos

**Detalles de configuración de clave:**

- El esquema de Experience Event debe incluir identificadores de producto/elemento (SKU, ID de producto, ID de contenido) en la carga útil de evento
- El esquema del catálogo de artículos debe incluir atributos utilizados para el filtrado y la clasificación: categoría, precio, URL de imagen, estado de disponibilidad, etiquetas
- La secuencia de datos debe tener el servicio [!DNL Adobe Journey Optimizer] habilitado para Edge Decisioning
- [!DNL Web SDK] `sendEvent` llamadas deben incluir datos de interacción del producto asignados a campos de comercio XDM

**Documentación de Experience League:**

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Definición de una relación entre dos esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-api)

### Fase 2: Configuración de la identidad y el perfil

**Función de aplicación:** AEP: Configuración de identidad y perfil (F4)

Esta fase configura áreas de nombres de identidad, designaciones de identidad principales y políticas de combinación que garantizan que las señales de comportamiento se asocien correctamente a los perfiles de los visitantes y estén disponibles para la entrega de recomendaciones en tiempo real.

#### Decisión: Política de combinación para la toma de decisiones en Edge

¿Requiere el caso de uso de la recomendación una evaluación de Edge en tiempo real?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Activo en la política de combinación de Edge | Opciones A y B (recomendaciones web y móviles en tiempo real) | Necesario para la entrega de recomendaciones por debajo de segundo; solo una política de combinación de Edge por zona protegida |
| Política de combinación estándar (no en Edge) | Solo opción C (recomendaciones de correo electrónico evaluadas en el momento del envío) | Suficiente para la evaluación del lado del concentrador; no consume la ranura de política de combinación de Edge |

#### Decisión: identidad anónima frente a identidad conocida del visitante

¿Cómo se deben gestionar las señales de comportamiento de los visitantes anónimos?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo ECID (anónimo) | Recomendaciones principalmente para visitantes anónimos en función del comportamiento de la sesión | Configuración más sencilla; no hay continuidad entre sesiones a menos que el visitante se autentique |
| ECID + identidad autenticada (ID de CRM, correo electrónico) | Recomendaciones entre sesiones para visitantes conocidos con vinculación de identidad | Perfiles de comportamiento más completos; requiere flujo de autenticación |
| Ambos con vinculación de gráfico de identidad | Recorrido completo de anónimo a conocido con vinculación de identidad | El más completo; requiere la configuración de reglas de vinculación de identidad |

**Navegación de la interfaz de usuario:** Identidades > Áreas de nombres de identidad; Perfiles > Políticas de combinación

**Detalles de configuración de clave:**

- El espacio de nombres ECID está preconfigurado y [!DNL Web SDK] y [!DNL Mobile SDK] lo utilizan automáticamente
- Deben crearse áreas de nombres de identidad personalizadas (ID de CRM, ID de fidelidad) para la identidad autenticada
- La identidad principal en el esquema de Experience Event debe ser ECID para los eventos de comportamiento web/móvil
- La política de combinación debe utilizar Private Device Graph para la vinculación de identidad entre dispositivos

**Documentación de Experience League:**

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Reglas de vinculación de gráficos de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)

### Fase 3: Configurar el catálogo de artículos y la estrategia de selección

**Función de aplicación:** AJO: Decisioning

Esta fase configura el catálogo de elementos (elementos de decisión), las estrategias de selección que combinan señales de comportamiento con atributos de elemento para la clasificación, las reglas de filtrado para excluir elementos no aptos y las recomendaciones de reserva para perfiles de inicio en frío.

#### Decisión: ámbito del catálogo de elementos

¿Qué artículos están disponibles para la recomendación?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Catálogo de productos (comercio electrónico) | Recomendación de productos físicos o digitales para la compra | Los atributos del artículo incluyen precio, categoría, disponibilidad e imágenes |
| Catálogo de contenido (medios/publicación) | Recomendar artículos, vídeos o contenido educativo | Los atributos del elemento incluyen tema, autor, fecha de publicación y tipo de contenido |
| Catálogo híbrido | Recomendación de productos y contenido | Requiere un esquema de elemento unificado que se ajuste a ambos tipos |

#### Decisión: enfoque de clasificación

¿Cómo se deben clasificar los artículos aptos para determinar las mejores recomendaciones?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Clasificación basada en fórmulas | Borrar la lógica empresarial para la clasificación (por ejemplo, ordenar por puntuación de afinidad de categoría multiplicada por la popularidad del artículo) | Clasificación transparente y auditable; requiere una fórmula de clasificación definida |
| Clasificación de IA (optimización automática) | El aprendizaje automático debe determinar la clasificación óptima en función de los datos de conversión | Requiere un mínimo de 1000 eventos de conversión para la formación de modelos; menos transparente |
| Basado en prioridades (manual) | Pedidos de recomendaciones simples y depurados manualmente | Es más fácil de configurar; no se adapta al comportamiento individual |

#### Decisión: Reglas de filtrado

¿Qué artículos deben excluirse de las recomendaciones?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Excluir artículos ya adquiridos | Recomendaciones de venta cruzada y descubrimiento | Requiere historial de compras en perfil de comportamiento |
| Excluir artículos sin existencias | Comercio electrónico con inventario dinámico | Requiere actualizaciones de catálogo en tiempo real o casi en tiempo real |
| Excluir elementos descartados anteriormente | Recomendaciones de contenido en las que los usuarios pueden rechazar sugerencias | Requiere un seguimiento de despido en eventos de comportamiento |
| Filtrado con alcance de categoría | Recomendaciones limitadas a categorías específicas | Utiliza atributos de elemento para filtrar |

#### Decisión: Estrategia de inicio en frío

¿Qué se debe mostrar para los nuevos visitantes sin historial de comportamiento?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Artículos populares (más vendidos en todo el mundo) | Reserva de uso general | Fácil de mantener; no personalizado |
| Elementos populares específicos de la categoría | El visitante ha llegado a una página de categoría | Reserva relevante para el contexto; requiere contexto de página |
| Selección editorial seleccionada | Brand quiere control editorial sobre la experiencia de arranque en frío | Requiere revisión y actualizaciones manuales |
| Elementos de tendencia (popularidad ponderada en el tiempo) | Reserva dinámica que refleja las tendencias actuales | Requiere cálculo de señal de tendencia |

**Navegación de la interfaz de usuario:** [!DNL Journey Optimizer] > Componentes > Administración de decisiones > Decisiones; [!DNL Journey Optimizer] > Componentes > Administración de decisiones > Ofertas; [!DNL Journey Optimizer] > Componentes > Administración de decisiones > Ubicaciones

**Detalles de configuración de clave:**

- Cree elementos de decisión que representen cada producto o elemento de contenido del catálogo, con atributos (categoría, precio, URL de imagen, etiquetas)
- Defina estrategias de selección que combinen el filtrado del catálogo de elementos con la lógica de clasificación de comportamiento
- Configurar modelos de clasificación: las expresiones basadas en fórmulas pueden hacer referencia a atributos de perfil (por ejemplo, puntuaciones de afinidad de categoría de atributos calculados)
- Crear ofertas o elementos de reserva que sirvan como recomendaciones predeterminadas para perfiles de inicio en frío
- Organizar elementos en colecciones utilizando calificadores de colección (etiquetas) para la agrupación lógica
- Configurar reglas de filtrado dentro de las estrategias de selección para aplicar reglas empresariales (excluir compradas, solo en stock)

**Documentación de Experience League:**

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fase 4: Configuración de canal y superficie

**Función de aplicación:** AJO: Configuración de canal

Esta fase configura las superficies de envío en las que se procesarán las recomendaciones. La configuración varía significativamente según la opción de implementación.

#### Decisión: Tipo de superficie de entrega

¿Dónde se mostrarán las recomendaciones?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Experiencia basada en código (web) | Widget de recomendaciones en páginas web con procesamiento personalizado | Máxima flexibilidad de procesamiento; requiere desarrollo front-end |
| Superficie del canal web | Superficie de personalización web estándar | Utiliza el diseñador web de AJO; es menos flexible que la función basada en código |
| Mensaje en la aplicación | Recomendaciones contextuales activadas por el comportamiento de la aplicación | Efímero; desaparece después de la interacción o el despido |
| Tarjeta de contenido (móvil) | Fuente de recomendaciones persistentes en aplicaciones móviles | Persiste hasta que el usuario actúa; experiencia de fuente explorable |
| Correo electrónico | Recomendaciones de productos incrustadas en campañas de correo electrónico | Estático en el momento del envío; sujeto a restricciones de procesamiento de correo electrónico |

**Donde las opciones difieren:**

**Para La Opción A (Recomendaciones En Tiempo Real Web):**
Configure una superficie de experiencia basada en código o una superficie de canal web. Las experiencias basadas en código proporcionan la mayor flexibilidad para la representación de recomendaciones personalizadas (carruseles, cuadrículas y tarjetas de elementos). El URI de superficie identifica dónde aparecen las recomendaciones en la página.

**Para Opción B (Recomendaciones De Aplicaciones Móviles):**
Configure las superficies de mensajes en la aplicación o de tarjetas de contenido. Se recomiendan las tarjetas de contenido para las fuentes de recomendaciones persistentes. Los mensajes en la aplicación funcionan bien para recomendaciones contextuales activadas por el comportamiento.

**Para La Opción C (Recomendaciones De Comportamiento De Correo Electrónico):**
Configure una superficie de canal de correo electrónico con delegación de subdominios, asignación de grupos de IP y configuración de remitente. Asegúrese de que la superficie esté validada para la entrega.

**Navegación de interfaz de usuario:** Administración > Canales > Superficies de canal > Crear superficie

**Documentación de Experience League:**

- [Configuración de superficies de canal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fase 5: Configuración de contenido y envío

**Función de aplicación:** AJO: Creación de mensajes

Esta fase define las plantillas de renderización de recomendaciones que controlan cómo se muestran los artículos recomendados al visitante. Esto incluye el diseño del artículo, expresiones de personalización que extraen atributos del artículo (nombre, imagen, precio, vínculo) y el diseño general de la experiencia de recomendación.

#### Decisión: formato de visualización de recomendación

¿Cómo se deben representar los elementos recomendados?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Carrusel (desplazamiento horizontal) | Página de inicio o página de categoría con espacio vertical limitado | Patrón de UX familiar; muestra varios elementos en un espacio compacto. |
| Cuadrícula (varias filas) | Sección de recomendaciones dedicada con amplio espacio | Muestra más elementos a la vez; funciona bien para las secciones &quot;recomendado para usted&quot; |
| Widget de un solo elemento | Recomendación contextual en una ubicación de página específica (por ejemplo, barra lateral) | Espacio mínimo; ubicación de alto impacto |
| Bloque de correo electrónico en línea | Recomendaciones incrustadas en el cuerpo del correo electrónico | Sujeto a restricciones de HTML/CSS de correo electrónico; normalmente, de 2 a 4 elementos |

#### Decisión: número de recomendaciones que se mostrarán

¿Cuántos elementos debe devolver la decisión por ubicación?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| 3 a 4 elementos | Widget de recomendación estándar | Equilibra relevancia con densidad visual |
| 6 a 8 elementos | Carrusel con desplazamiento o diseño de cuadrícula | Más opciones para el visitante; requiere suficiente profundidad de catálogo |
| 1 elemento | Recomendación contextual de un solo producto | Impacto de mayor relevancia; procesamiento más sencillo |
| Más de 10 elementos | Experiencia de recomendación de estilo de fuente | Casos de uso con contenido elevado (medios, publicación) |

**Donde las opciones difieren:**

**Para La Opción A (Recomendaciones En Tiempo Real Web):**
Diseñe el procesamiento de recomendaciones utilizando plantillas de experiencia basadas en código. Utilice HTML/CSS/JavaScript para crear el diseño de carrusel, cuadrícula o widget. Las expresiones de Personalization hacen referencia a los atributos de respuesta de decisión (nombre del artículo, dirección URL de imagen, precio, dirección URL del producto). La impresión y el rastreo de clics son administrados automáticamente por [!DNL Web SDK].

**Para Opción B (Recomendaciones De Aplicaciones Móviles):**
Configure la tarjeta de contenido o las plantillas de mensajes en la aplicación con la lógica de visualización de elementos. Utilice estructuras de contenido basadas en JSON que la aplicación móvil procese de forma nativa. Incluya vínculos profundos para cada elemento recomendado.

**Para La Opción C (Recomendaciones De Comportamiento De Correo Electrónico):**
Diseño del contenido del correo electrónico con Email Designer. Inserte ubicaciones de recomendaciones utilizando bloques de contenido basados en decisiones. Configure expresiones de personalización para atributos de elemento dentro de la plantilla de correo electrónico. La personalización de la línea de asunto puede hacer referencia a los elementos principales recomendados.

**Navegación de la interfaz de usuario:** Administración de contenido > Plantillas de contenido; Campaña/Recorrido > Editar contenido > Enviar correo electrónico a Designer

**Detalles de configuración de clave:**

- Cada ubicación de recomendación debe hacer referencia a la decisión creada en la Fase 3
- Las expresiones de Personalization utilizan la sintaxis Handlebars para procesar atributos de elemento
- Para la web: configure la experiencia basada en código para llamar a la decisión y procesar la respuesta
- Para el correo electrónico: incrusta la decisión en la acción de correo electrónico dentro de la campaña o el recorrido
- Previsualización de recomendaciones mediante perfiles de prueba con historial de comportamiento conocido

**Documentación de Experience League:**

- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### Fase 6: Configurar el ámbito de audiencia y la campaña/recorrido (solo opción C)

**Función de aplicación:** RT-CDP: Evaluación de audiencia, AJO: Ejecución de campaña o Journey Orchestration

Para las recomendaciones basadas en correo electrónico (Opción C), esta fase define la audiencia objetivo y configura la campaña o el recorrido que envía el correo electrónico de recomendación. Las opciones A y B omiten esta fase porque las recomendaciones se entregan en tiempo real al cargar la página o la pantalla.

#### Decisión: método de evaluación de audiencia

¿Cómo se debe evaluar la audiencia de destino de los correos electrónicos de recomendación?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Evaluación por lotes | Campañas de correo electrónico de recomendaciones programadas (resumen diario y semanal) | Tiempo de envío predecible; audiencia evaluada antes del envío |
| Evaluación de streaming | Correos electrónicos de recomendación activados por eventos (navegador abandonado, posterior a la compra) | Calificación de audiencias casi en tiempo real; se vincula con la orquestación de recorrido |

#### Decisión: Mecanismo de entrega

¿Debe entregarse el correo electrónico a través de una campaña o un recorrido?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Campaña programada | El correo electrónico de recomendación única o recurrente se envía a una audiencia definida | Configuración más sencilla; evaluación de audiencias por lotes y envío |
| Recorrido con la entrada de audiencia | Correos electrónicos de recomendación en curso activados por la calificación de audiencia | Habilita flujos de varios pasos (por ejemplo, correo electrónico de recomendación seguido de recordatorio) |
| Recorrido activado por evento | Correo electrónico de recomendación activado por un evento específico (navegación, abandono, compra) | Activación en tiempo real; requiere la entrada de recorrido basada en eventos |

**Navegación de la interfaz de usuario:** Cliente > Audiencias > Crear audiencia > Generar regla; Campañas > Crear campaña; Recorridos > Crear recorrido

**Detalles de configuración de clave:**

- Defina la audiencia de destino mediante expresiones de regla de segmento que hagan referencia al historial de comportamiento (por ejemplo, &quot;productos vistos en los últimos 7 días pero no comprados&quot;)
- Configure la campaña o el recorrido con la acción de correo electrónico que hace referencia a la superficie de canal desde la fase 4
- Incrustar la decisión de la fase 3 en el contenido del correo electrónico
- Establezca reglas de programación y frecuencia para evitar mensajes excesivos

**Documentación de Experience League:**

- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Informe en vivo de la campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)

### Fase 7: Configuración de informes y optimización

**Función de la aplicación:** AJO: Reporting &amp; Performance Analysis, S5: Reporting &amp; Analysis

Esta fase establece la monitorización del rendimiento para las métricas de clics, conversiones e ingresos de recomendaciones. Crea la infraestructura de creación de informes para medir la eficacia de las recomendaciones e identificar las oportunidades de optimización.

#### Decisión: profundidad del informe

¿Qué nivel de análisis de creación de informes se necesita?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo informes nativos de AJO | Monitorización del rendimiento de recomendaciones básicas | Configuración rápida; limitada a métricas con seguimiento de AJO |
| Integración de AJO + [!DNL Customer Journey Analytics] | Análisis de impacto de recomendaciones en canales múltiples y atribución de ingresos | Requiere conexión y vista de datos de [!DNL Customer Journey Analytics]; proporciona información más detallada |
| Espacio de trabajo [!DNL Customer Journey Analytics] completo con paneles personalizados | Programa de optimización en curso con análisis de nivel de elemento, nivel de segmento y nivel de superficie | El más completo; requiere experiencia y configuración de [!DNL Customer Journey Analytics] |

**Navegación de la interfaz de usuario:** Campañas > Seleccionar campaña > Informe de todo el tiempo; Recorrido > Seleccionar recorrido > Informe de todo el tiempo; [!DNL Customer Journey Analytics] > Proyectos > Crear nuevo proyecto

**Detalles de configuración de clave:**

- Revise los informes de campaña y recorrido de AJO para ver las métricas de entrega y participación
- Para la integración de [!DNL Customer Journey Analytics], cree una conexión que incluya conjuntos de datos de evento de experiencia de AJO (comentarios de mensajes, seguimiento de correo electrónico, toma de decisiones)
- Crear una vista de datos [!DNL Customer Journey Analytics] con dimensiones específicas de la recomendación (nombre del elemento, categoría del elemento, superficie de recomendación) y métricas (impresiones, clics, conversiones, ingresos)
- Cree métricas calculadas para el CTR de recomendación, la tasa de conversión y los ingresos por impresión
- Crear [!DNL Customer Journey Analytics] paneles de Workspace comparando el rendimiento de las recomendaciones en superficies, segmentos y periodos de tiempo

**Documentación de Experience League:**

- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Crear o editar una conexión](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Creación o edición de una vista de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Resumen de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

## Consideraciones sobre la implementación

Revise las siguientes barreras, escollos, prácticas recomendadas y compensaciones antes y durante la implementación.

### Protecciones y límites

- Máximo de 10 000 ofertas personalizadas aprobadas (elementos de decisión) por zona protegida: [protecciones de administración de decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 30 colocaciones por decisión
- Máximo de 30 ámbitos de recopilación por solicitud de decisión
- Tiempo de respuesta de entrega de la oferta SLA: menos de 500 ms a P95 para solicitudes de Edge de un solo ámbito
- Los modelos de clasificación de IA requieren un mínimo de 1000 eventos de conversión para la formación.
- Los contadores de límite de oferta pueden tener un retraso de hasta unos segundos en escenarios de alto rendimiento
- Las decisiones de Edge se limitan a atributos de perfil disponibles en el almacén de perfiles Edge
- Solo puede haber una política de combinación activa en Edge por zona protegida — [Protecciones de perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Máximo de 25 atributos calculados activos por zona protegida: [Controles de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- Máximo de 4000 definiciones de segmento por zona protegida — [Protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Ingesta de transmisión: máximo de 20 000 registros por segundo por conexión HTTP — [Protecciones de ingesta](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### Peligros comunes

- **La decisión solo devuelve elementos de reserva:** Compruebe que los elementos de decisión personalizados estén aprobados, dentro de su intervalo de fechas de validez, y que las reglas de elegibilidad coincidan con los atributos de perfil del visitante. Compruebe que no se han alcanzado los límites.
- **La entrega de Edge devuelve la personalización vacía:** Asegúrese de que la secuencia de datos esté configurada con el servicio [!DNL Adobe Journey Optimizer] habilitado y de que el ámbito de decisión tenga el formato correcto en la solicitud [!DNL Web SDK].
- **Fórmula de clasificación no aplicada:** Compruebe que la fórmula es sintácticamente válida y hace referencia a atributos de perfil accesibles. Los errores de fórmula vuelven silenciosamente a la clasificación basada en prioridades.
- **Recomendaciones antiguas:** Si los datos de eventos de comportamiento no fluyen en tiempo real, las recomendaciones se basarán en perfiles de comportamiento obsoletos. Verifique que [!DNL Web SDK] o [!DNL Mobile SDK] estén transmitiendo eventos de forma activa.
- **La tasa de reserva de inicio en frío es demasiado alta:** Si un gran porcentaje de visitantes recibe recomendaciones de reserva, considere enriquecer la estrategia de inicio en frío con señales contextuales (categoría de página actual, origen de referencia) en lugar de depender únicamente del historial de comportamiento.
- **Las recomendaciones no se representan en la página:** Compruebe que el URI de superficie de experiencia basado en código coincide con el patrón de URL de página y que [!DNL Web SDK] solicita y procesa correctamente la respuesta de decisión.
- Faltan **elementos de catálogo en las recomendaciones:** Asegúrese de que todos los elementos de catálogo se hayan ingerido como elementos de decisión, se hayan etiquetado con los calificadores de colección correctos y se hayan incluido en las colecciones adecuadas a las que hace referencia la estrategia de selección.

### Prácticas recomendadas

- Comience con un modelo de clasificación basado en fórmulas que utilice atributos calculados (afinidad de la categoría, actualización de la interacción) antes de invertir en modelos con clasificación de IA. Los modelos basados en fórmulas son transparentes, auditables y proporcionan una línea de base sólida para la comparación.
- Implemente el rastreo de clics y impresiones desde el primer día. Sin datos de interacción, los modelos de clasificación de IA no pueden entrenarse y no se puede medir la efectividad de las recomendaciones.
- Cree estrategias de selección independientes para diferentes superficies de recomendación (página principal, PDP, correo electrónico) en lugar de reutilizar una sola estrategia en todas partes. Las diferentes superficies sirven para diferentes intenciones del usuario.
- Utilice atributos calculados para destilar el historial de comportamiento en señales de clasificación. Los datos de evento sin procesar son demasiado granulares para una clasificación efectiva basada en fórmulas; las señales agregadas como &quot;puntuación de afinidad de categoría&quot; y &quot;días desde la última compra&quot; son más efectivas.
- Pruebe recomendaciones de reserva por separado de recomendaciones personalizadas. Asegúrese de que los elementos de reserva sean valores predeterminados de alta calidad y apropiados para la marca que proporcionen una buena experiencia a los nuevos visitantes.
- Monitorice la tasa de reserva de inicio en frío como métrica de estado clave. Una tasa de respuesta descendente con el tiempo indica una creciente cobertura del comportamiento.
- Para las recomendaciones por correo electrónico, la programación envía a las horas en las que el perfil de comportamiento es más completo (por ejemplo, después de las horas de mayor navegación, no durante ellas).

### Decisiones de compensación

Las siguientes compensaciones deben evaluarse en función de sus necesidades específicas.

#### Señales en tiempo real frente a historial acumulado

Las señales de comportamiento en la sesión proporcionan relevancia inmediata, pero una profundidad limitada. Los antecedentes de comportamiento acumulados proporcionan profundidad, pero pueden ser antiguos. El equilibrio entre estas fuentes afecta a la calidad de las recomendaciones.

- **Favores de la opción A:** Señales en tiempo real para una relevancia inmediata, complementadas por el historial acumulado de visitantes conocidos
- **Opción C favorece:** El historial acumulado es exclusivo, ya que los mensajes de correo electrónico se envían de forma asincrónica
- **Recomendación:** Para la web y el móvil (opciones A y B), combine las señales de la sesión con atributos calculados derivados del comportamiento histórico. Para el correo electrónico (Opción C), realice una fuerte inversión en atributos calculados que resuman el historial de comportamiento en señales procesables a nivel de perfil.

#### Modelos basados en fórmulas o clasificados por IA

La clasificación basada en fórmulas es transparente e inmediata. Los modelos con clasificación de IA se adaptan automáticamente, pero requieren datos de formación y ofrecen menos visibilidad en las decisiones de clasificación.

- **Favoritos basados en fórmulas:** Transparencia, auditabilidad, implementación inmediata y control empresarial preciso de la lógica de clasificación
- **Favoritos de clasificación de IA:** Optimización automatizada, descubrimiento de patrones no obvios y menor esfuerzo de ajuste manual
- **Recomendación:** Comience con la clasificación basada en fórmulas para establecer una línea de base de rendimiento y acumular datos de conversión. Realice la transición a modelos con clasificación de IA una vez que tenga datos de formación suficientes (más de 1000 eventos de conversión) y desee optimizar más allá de lo que puede lograr el ajuste manual de la fórmula.

#### Cobertura de la recomendación frente a relevancia

Ampliar el catálogo de artículos y relajar las reglas de filtrado aumenta el porcentaje de solicitudes que reciben recomendaciones personalizadas, pero puede reducir la relevancia por recomendación.

- **Favoritos de alta cobertura:** Maximizar el número de visitantes que ven recomendaciones personalizadas; útil cuando el objetivo principal es la participación
- **Favoritos de alta relevancia:** mostrar solo elementos de alta relevancia, incluso si significa que más visitantes verán recomendaciones de reserva; útil cuando el objetivo principal es la conversión
- **Recomendación:** Comience con un filtrado moderado (excluya los artículos comprados y los que no tengan existencias) y supervise tanto la tasa de reserva como la tasa de conversión. Apriete las reglas de filtrado solo si los datos de conversión lo admiten.

#### Profundidad de Personalization frente a complejidad de la implementación

Las señales de comportamiento más enriquecidas y los modelos de clasificación más sofisticados mejoran la calidad de la recomendación, pero aumentan la complejidad de la implementación y la carga de mantenimiento.

- **Una implementación más sencilla favorece:** Un tiempo de respuesta más rápido, menor mantenimiento, más fácil de depurar e iterar
- **Favoritos de personalización más profundos:** mayor alza de conversión, mejor experiencia de cliente y diferenciación competitiva
- **Recomendación:** implementación por fases. Comience con las señales de vista del producto y la clasificación basada en fórmulas (Fase 1). Agregar atributos calculados para el enriquecimiento conductual (Fase 2). Evalúe los modelos con clasificación de IA una vez que la base esté madura y haya disponibles datos de formación suficientes (Fase 3).

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las tecnologías y capacidades utilizadas en este patrón.

### Administración de decisiones

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear calificadores de colección](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Entrega de ofertas mediante la API de Edge Decisioning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)

### Recopilación de datos y SDK web/móvil

- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Instalación de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [Información general de Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Información general sobre API de Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### XDM y modelado de datos

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Crear un conjunto de datos](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/create)
- [Definición de una relación entre dos esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-api)

### Identidad y perfil

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Resumen del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Atributos calculados y enriquecimiento de perfiles

- [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Guía de IU de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Información general sobre Customer AI](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configuración de superficies de canal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)

### Creación y personalización de mensajes

- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### Informes y análisis

- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Resumen de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

### Gobernanza de datos y ciclo vital

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Información general sobre Advanced Data Lifecycle Management](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [Caducidad de conjuntos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration)

### Monitorización y observabilidad

- [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
- [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones de ingesta](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [Protecciones del servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)

### Tutoriales y guías

- [Resumen de orígenes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Información general sobre etiquetas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
- [Grupo de campos de consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
