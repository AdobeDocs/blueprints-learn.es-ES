---
title: Personalization de aplicación/web de visitante conocido
description: Aprenda a ofrecer contenido, ofertas o promociones personalizadas a visitantes identificados en función del perfil en tiempo real y la pertenencia a segmentos.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 585adc0e-f528-4a09-b931-ef6b45fa8ec8
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7968'
ht-degree: 2%

---

# Personalización web/aplicación de visitante conocido

Este plan de referencia proporciona una guía de implementación completa para ofrecer contenido personalizado a visitantes identificados en superficies digitales mediante [!DNL Adobe Journey Optimizer] (AJO) y [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP). Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesitan comprender todos los enfoques de implementación viables, las decisiones que se deben tomar en cada fase y la documentación de Experience League que admite la configuración.

La personalización de aplicaciones/web de visitante conocido es el patrón de personalización principal para experiencias digitales autenticadas. A diferencia de la personalización de visitantes anónimos, que se basa únicamente en señales de comportamiento en la sesión, este patrón aprovecha el perfil unificado completo: datos de comportamiento históricos, pertenencia a segmentos, nivel de lealtad, historial de compras, fase del ciclo vital, atributos calculados y puntuaciones de tendencia. Admite la personalización en varias páginas web (a través del canal web de AJO), mensajes móviles en la aplicación y tarjetas de contenido.

Esta guía presenta todas las opciones de implementación viables (basadas en segmentos, en decisiones y de varias superficies) con compensaciones, orientación para la toma de decisiones y referencias a la documentación de [!DNL Adobe Experience League].

## Resumen del caso de uso

Las organizaciones con propiedades digitales autenticadas (sitios de comercio electrónico, portales bancarios, servicios de suscripción, programas de fidelidad y aplicaciones móviles) deben ofrecer experiencias personalizadas que reflejen la relación de cada cliente con la marca. Cuando un visitante inicia sesión o se reconoce mediante la resolución de identidades, la plataforma puede acceder a su perfil unificado completo y ofrecer contenido adaptado a sus atributos, comportamientos y preferencias específicos.

Este patrón aborda el escenario en el que un visitante identificado llega a una propiedad web o abre una aplicación móvil, y el sistema debe determinar el contenido, la oferta o la promoción óptimos para mostrar en función de los datos de perfil en tiempo real y la pertenencia a audiencias. La decisión de personalización se produce en el extremo en milisegundos, lo que permite la entrega de contenido por subsegundo sin latencia perceptible.

El patrón admite la personalización determinística (donde el contenido específico se asigna a segmentos de audiencia específicos) y la toma de decisiones dinámica (donde AJO Decisioning evalúa las reglas de elegibilidad y las estrategias de clasificación para seleccionar el contenido óptimo por perfil). Abarca varias superficies digitales (páginas web, mensajes móviles en la aplicación y tarjetas de contenido) y permite una personalización coherente en todo el recorrido digital del cliente.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Ofrezca experiencias de cliente personalizadas

Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo de vida individuales. Para obtener más información, consulte [Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md).

**KPI:** participación, tasas de conversión, satisfacción del cliente (CSAT)

### Aumentar la participación en el sitio web

Mejore el tiempo en el sitio, las páginas por sesión y la interacción con el contenido web mediante experiencias relevantes. Para obtener más información, consulte [Aumentar la participación en el sitio web](../../business-objectives/acquisition-growth/increase-website-engagement.md).

**KPI:** tiempo en la página (web), participación, tasas de conversión

### Aumentar la participación en aplicaciones móviles

Impulse el uso activo diario, la adopción de funciones y las conversiones en la aplicación a través de experiencias personalizadas en la aplicación.

**KPI:** participación, retención, tasas de conversión

## Casos de uso tácticos de ejemplo

Las siguientes son implementaciones tácticas comunes de este patrón:

- Personalización de la página principal como héroe por nivel de lealtad o etapa del ciclo vital: muestre diferentes titulares a pantalla completa en función de si el cliente es nuevo, está activo, está en riesgo o es VIP
- Carrusel de recomendaciones de productos basado en el historial de compras: muestre sugerencias de productos relevantes utilizando datos de compras anteriores y puntuaciones de afinidad de productos
- Titular promocional personalizado por segmento de cliente: muestra diferentes promociones para segmentos de clientes nuevos, de alto valor y en riesgo.
- Mensaje en la aplicación para usuarios móviles basado en la adopción de funciones: guíe a los usuarios a funciones infrautilizadas según sus patrones de uso
- Tarjeta de contenido con oferta personalizada en el panel de cuentas: ofertas persistentes y descartables adaptadas al perfil del cliente
- Visualización personalizada de precios o descuentos según el nivel del cliente: mostrar precios específicos del nivel o descuentos exclusivos a los miembros del programa de fidelidad.
- Widget de recomendaciones de venta cruzada basado en productos propios: sugerir productos o servicios complementarios basados en la cartera actual
- Navegación personalizada u orden de contenido basado en intereses: vuelva a ordenar los módulos de contenido o los elementos de navegación según las preferencias demostradas.

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir la eficacia de este patrón de caso de uso.

| KPI | Método de medición | Guía de referencia |
| --- | --- | --- |
| Tasa de participación de Personalization | Clics e interacciones con elementos de contenido personalizados divididos por impresiones | El contenido personalizado debe superar el contenido predeterminado en un 20-50 % |
| Alza de tasa de conversión | Tasa de conversión para experiencias personalizadas en comparación con experiencias de control/predeterminadas | Opte a un alza del 10 al 30 % con respecto a las experiencias no personalizadas |
| Tasa de clics (CTR) | Clics en CTA, ofertas y recomendaciones personalizadas divididas por impresiones | Monitor por superficie (web, en la aplicación, tarjeta de contenido) y por segmento |
| Ingresos por visita | Ingresos atribuidos a sesiones con experiencias personalizadas | Comparación de cohortes de visitantes personalizadas y no personalizadas |
| Tasa de interacción de tarjeta de contenido | Clics y descartes en la tarjeta de contenido en relación con impresiones | Seguimiento por tipo de tarjeta y segmento de audiencia |
| Participación en mensajes en la aplicación | Interacciones de mensajes en la aplicación (clics de CTA, rechazos) relativas a impresiones | Comparar entre segmentos de audiencia y tipos de mensajes |
| Tiempo en la página | Tiempo promedio empleado en páginas con contenido personalizado en comparación con el valor predeterminado | Las páginas personalizadas deben mostrar un mayor tiempo de permanencia |
| Tasa de aceptación de ofertas | Porcentaje de ofertas seleccionadas para la toma de decisiones que resultan en un evento de conversión | Seguimiento de cada oferta, ubicación y estrategia de clasificación |

## Patrón de caso de uso

En esta sección se describe el patrón principal y su cadena de funciones.

**Personalización web/aplicación de visitante conocido**

Ofrezca contenido, ofertas o promociones personalizados a un visitante identificado en función de la pertenencia a perfiles y segmentos en tiempo real en la web, aplicaciones móviles y superficies de tarjetas de contenido.

**Cadena de funciones:** Evaluación de audiencias > Personalization Decisioning > Configuración de superficie/canal > Entrega de contenido > Seguimiento de impresiones > Informes

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Adobe Journey Optimizer] (AJO)**: configuración del canal web, configuración del canal en la aplicación, configuración del canal de la tarjeta de contenido, toma de decisiones (selección de ofertas y clasificación), creación de mensajes (creación de contenido personalizado), ejecución de campañas, experimentación de contenido y creación de informes
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Evaluación de audiencias (Edge, streaming y por lotes), búsqueda de perfiles en tiempo real mediante Edge Network, enriquecimiento de perfiles con atributos calculados y puntuaciones de tendencia
- **[!DNL Adobe Experience Platform] (AEP)**: almacén de perfiles, servicio de identidad, Web SDK, Mobile SDK, configuración de secuencia de datos, entrega de red perimetral

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Se asume en contexto | Entorno de pruebas de AJO con permisos de canal web, canal en la aplicación y toma de decisiones configurados. Usuarios aprovisionados con funciones de experto en marketing y autor de contenido. | [Resumen de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home), [Resumen de control de acceso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | El esquema de perfil debe incluir atributos utilizados para la personalización y segmentación (por ejemplo, nivel de lealtad, historial de compras, intereses de productos, fase de ciclo vital). Esquema de evento de experiencia para eventos de conversión y seguimiento de interacción web/aplicación. Conjuntos de datos habilitados para [!DNL Real-Time Customer Profile]. | [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [Conceptos básicos de composición de esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Fuentes de datos y recopilación | Requerido | Web SDK implementado en propiedades web para la entrega de experiencias y el seguimiento de impresiones. SDK móvil implementado en aplicaciones móviles para la entrega en la aplicación y con tarjeta de contenido. Flujo de datos configurado con el servicio AJO habilitado para la personalización Edge. Datos de perfil en tiempo real disponibles en el perímetro de para una personalización por debajo de segundo. | [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Información general de Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview), [Configurar flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Configuración de identidad y perfil | Requerido | Áreas de nombres de identidad conocidas (ID de CRM, correo electrónico, ID de usuario autenticado) configuradas. La vinculación de identidad entre sesiones anónimas y autenticadas funciona para una transición sin problemas de la personalización anónima a la de visitante conocido. Política de combinación de Edge configurada con `isActiveOnEdge: true` para resolver el perfil autenticado en el perímetro de. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Introducción a las políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Definición de audiencia y segmentación | Requerido | Audiencias definidas mediante atributos de perfil, datos de comportamiento y atributos calculados. Evaluación de Edge o streaming habilitada para la calificación de personalización en tiempo real. Las audiencias utilizadas para la personalización basada en segmentos deben cumplir los requisitos para la evaluación de Edge. | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Los atributos calculados (por ejemplo, puntuaciones de tendencia de [!DNL Customer AI], valor de duración, puntuación de participación, afinidad del producto, días desde la última compra) mejoran significativamente la calidad de la personalización al proporcionar señales más completas para la definición de audiencias y la selección de contenido. | [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Resumen de inteligencia artificial aplicada al cliente](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Administración del ciclo de datos | Recomendado | Las políticas de retención de datos de perfil y evento garantizan que los datos nuevos y relevantes alimenten las decisiones de personalización. La aplicación del consentimiento garantiza que la personalización respete las preferencias del usuario. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted) |
| Etiquetado y aplicación del uso de datos | Recomendado | Las etiquetas de gobernanza en los atributos de perfil utilizados para la personalización (especialmente los atributos adyacentes a PII como el historial de compras, la ubicación y los datos financieros) garantizan el cumplimiento de las políticas de uso de datos. | [Resumen de control de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Resumen de etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview) |
| Monitorización y observabilidad | Recomendado | La monitorización del rendimiento de la personalización y la entrega de Edge ayuda a detectar problemas de latencia, fallos de entrega o problemas de actualización de datos que degradan la experiencia personalizada. | [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home), [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview) |
| Informes y análisis | Incluido | Los informes de rendimiento de Personalization forman parte del paso 6 de la cadena de funciones. [!DNL Customer Journey Analytics] analysis permite una investigación profunda del impacto de la personalización en la conversión, la participación y los ingresos entre segmentos de visitantes. | [descripción general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del Catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Journey Optimizer] (AJO)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Configuración de canal | Configuración de superficie y canal | Configuración de superficies de canal web, en la aplicación y de tarjetas de contenido para la entrega de personalización |
| Creación de mensajes | Creación de contenido | Cree variantes de contenido personalizadas con contenido dinámico, expresiones de personalización y bloques condicionales para cada superficie |
| Ejecución de campaña | Configuración y activación de Campaign | Cree y active campañas web (programadas o activadas por API) que enlacen audiencias, superficies y contenido |
| Decisioning | Configuración de decisiones (opción B/C) | Configure las políticas de decisión con reglas de idoneidad, estrategias de clasificación y elementos de oferta/contenido para la personalización dinámica |
| Experimentación de contenido | Optimización (opcional) | Ejecute pruebas A/B en variantes de contenido personalizadas para optimizar el rendimiento |
| Frecuencia y reglas comerciales | Configuración y activación de Campaign | Aplicar límites de frecuencia de impresión para evitar la fatiga por sobrepersonalización |
| Informes y análisis de rendimiento | Informes y optimización | Monitorización de métricas de entrega de personalización, participación y conversión por superficie y segmento |

### [!DNL Real-Time CDP] (RT-CDP)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Evaluación de audiencia | Definición y evaluación de audiencias | Defina y evalúe audiencias mediante atributos de perfil, datos de comportamiento y atributos calculados con evaluación de Edge o streaming |
| Búsqueda de perfiles en tiempo real | Entrega de contenido (tiempo de ejecución) | Acceda a atributos de perfil en tiempo real y suscripciones a segmentos a través de Edge Network para decisiones de personalización por debajo del segundo |
| Enriquecimiento de perfiles | Preimplementación (compatibilidad) | Enriquezca los perfiles con atributos calculados, puntuaciones de [!DNL Customer AI] y señales de comportamiento agregadas que mejoren la calidad de la personalización |

## Prerrequisitos

Antes de implementar este patrón de caso de uso, asegúrese de que se cumplan las siguientes condiciones:

- [ ] Web SDK implementado en las propiedades web de destino con `alloy("sendEvent")` configurado para vistas de página y seguimiento de interacciones
- [ ] SDK móvil implementado en aplicaciones móviles de destino (si se utilizan superficies de aplicación o de tarjeta de contenido)
- [ Flujo de datos ] configurado con el servicio [!DNL Adobe Journey Optimizer] habilitado
- [ ] El esquema de perfil incluye atributos utilizados para la personalización (nivel de lealtad, historial de compras, intereses de productos, fase de ciclo de vida)
- [ ] esquema de evento de experiencia configurado para el seguimiento de impresiones y conversiones
- [ ] áreas de nombres de identidad conocidas creadas y la vinculación de identidad operativa entre identidades anónimas (ECID) y autenticadas
- [ ] política de combinación de Edge configurada con `isActiveOnEdge: true`
- [ ] audiencias definidas con evaluación apta para Edge para personalización en tiempo real
- [ ] recursos de contenido (imágenes, copias, CTA) preparados para cada variante de personalización
- [ ]: estrategia de Personalization documentada: qué atributos determinan qué contenido, para qué superficies

## Opciones de implementación

En esta sección se describen los enfoques de implementación disponibles para este patrón de caso de uso.

### Opción A: personalización web basada en segmentos

**Mejor para:** Personalización determinística en la que variantes de contenido específicas se asignan directamente a segmentos de audiencia: banners de pantalla completa específicos del nivel de lealtad, mensajes de la fase de ciclo vital, contenido promocional del segmento del cliente. Ideal cuando la asignación de contenido a segmento está bien definida y no requiere optimización ni clasificación dinámica.

**Cómo funciona:**

La personalización basada en segmentos asigna las variantes de contenido directamente a los segmentos de audiencia. Cuando se evalúa el perfil de un visitante conocido frente a audiencias aptas para Edge al cargar la página, el sistema determina a qué segmentos pertenece el visitante y muestra la variante de contenido correspondiente. La selección se basa en la prioridad de abono del segmento: si un visitante cumple los requisitos para varios segmentos, se muestra el contenido del segmento con la prioridad más alta.

Este método utiliza campañas de canal web de AJO (o campañas en la aplicación/con tarjeta de contenido) con reglas de contenido condicional o configuraciones de segmentación de varios tratamientos. Cada segmento de audiencia está asociado con una experiencia de contenido específica. No hay ningún motor de decisión involucrado: la lógica de selección de contenido está totalmente basada en segmentos.

El contenido se crea mediante la interfaz de creación de mensajes de AJO con bloques de contenido dinámico que representan contenido diferente en función de la pertenencia a audiencias o los atributos de perfil. Web SDK o Mobile SDK ofrece la experiencia personalizada en tiempo real a través de Edge Network.

**Consideraciones clave:**

- Las variantes de contenido deben haber sido creadas previamente para cada segmento
- Las definiciones de segmentos deben cumplir los requisitos de Edge para la calificación en tiempo real
- Añadir nuevos segmentos o variantes de contenido requiere actualizar la configuración de la campaña
- La selección de contenido es determinista: el mismo segmento siempre ve el mismo contenido

**Ventajas:**

- Fácil de implementar y mantener con una asignación clara de contenido a segmento
- Es fácil de entender y explicar la lógica de personalización a las partes interesadas
- Sin sobrecarga de decisiones: resolución de contenido más rápida
- Control total sobre el contenido que recibe cada segmento

**Limitaciones:**

- Flexibilidad limitada cuando aumenta el número de segmentos y variantes de contenido
- No se puede optimizar dinámicamente la selección de contenido en función de las señales de nivel de perfil más allá del abono a segmentos
- La adición de nuevas variantes de contenido requiere actualizaciones manuales de la campaña
- No admite escenarios de mejor oferta siguiente en los que varias ofertas compitan por la misma ubicación

**Experience League:**

- [Introducción al canal web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Creación de experiencias web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### Opción B: personalización basada en decisiones

**Mejor opción para:** Personalización dinámica en la que se debe seleccionar el contenido u oferta óptimos para cada perfil mediante reglas de elegibilidad y estrategias de clasificación: oferta de la siguiente mejor oferta en la página principal, recomendaciones de productos personalizadas y selección dinámica de banners promocionales. Ideal cuando varias ofertas o artículos de contenido compiten por la misma ubicación y el sistema debe elegir la mejor.

**Cómo funciona:**

La personalización basada en decisiones utiliza AJO Decisioning para evaluar el perfil de cada visitante con respecto a un catálogo de artículos de contenido u ofertas, aplicar reglas de aceptación para determinar qué artículos cumplen los requisitos y, a continuación, aplicar una estrategia de clasificación (basada en prioridades, basada en fórmulas o en AI) para seleccionar el artículo óptimo para cada ubicación.

La implementación implica crear ubicaciones (donde aparece el contenido), definir ofertas con reglas de idoneidad y representaciones de contenido, organizar ofertas en colecciones y crear políticas de decisión que vinculen ubicaciones a colecciones con estrategias de clasificación. En tiempo de ejecución, cuando un visitante carga una página, Edge Network evalúa la política de decisión en relación con el perfil del visitante y devuelve el contenido de oferta seleccionado.

Este enfoque admite escenarios de personalización sofisticados, incluidas ofertas de próxima mejor oferta, promociones personalizadas con límite y selección de contenido optimizado para IA. Las ofertas pueden tener límites de límite globales y por perfil, intervalos de fechas de validez y criterios de idoneidad complejos que combinen atributos de perfil y pertenencia a audiencias.

**Consideraciones clave:**

- Requiere una configuración más inicial (ubicaciones, ofertas, reglas de elegibilidad, colecciones y decisiones)
- Las estrategias de clasificación pueden basarse en prioridades (manual), en fórmulas (expresión personalizada) o en IA (optimización automática)
- La clasificación de IA requiere un mínimo de 1000 eventos de conversión para la formación de modelos
- Los contadores de límite de oferta pueden tener un ligero retraso en escenarios de alto rendimiento
- Se debe configurar una oferta de reserva para los casos en los que no se cumpla ninguna oferta personalizada

**Ventajas:**

- Selección de contenido dinámica por perfil sin asignación de segmento a contenido codificada
- Admite criterios de idoneidad complejos y lógica de clasificación
- La opción de clasificación de IA permite la optimización automática sin intervención manual
- La restricción de oferta evita la sobreexposición de contenido específico
- Administración centralizada de ofertas: las ofertas se pueden reutilizar en campañas y canales

**Limitaciones:**

- Mayor complejidad de la implementación que la personalización basada en segmentos
- La clasificación de IA requiere un volumen de evento de conversión suficiente para la formación
- La evaluación de decisiones añade latencia marginal en comparación con la entrega de contenido directa basada en segmentos
- La clasificación basada en fórmulas requiere un diseño cuidadoso para evitar la priorización no deseada

**Experience League:**

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

**En qué se diferencia de la opción B de Offer Decisioning:**

La infraestructura es idéntica: ambos utilizan AJO Decisioning en el perímetro con Web SDK y una política de combinación activa para el perímetro. La diferencia es lo que se está seleccionando. Esta opción administra los elementos de contenido en los que el criterio de selección es el ajuste personalizado (pertenencia a segmento, clasificación de comportamiento). [Offer Decisioning](offer-decisioning.md): la opción B administra un catálogo de ofertas gobernadas donde las reglas de elegibilidad, los límites de límite y las ventanas de validez son requisitos comerciales. Si el conjunto de artículos requiere un límite de impresiones por perfil, restricciones de elegibilidad regulatorias o administración del ciclo de vida de la oferta, utilice la Opción B de Offer Decisioning en su lugar.

### Opción C: personalización de varias superficies (web + en la aplicación + tarjeta de contenido)

**Ideal para:** Personalización coherente en varias superficies digitales: ofrece experiencias personalizadas coordinadas en páginas web, mensajes móviles en la aplicación y tarjetas de contenido. Ideal cuando la organización tiene propiedades de aplicaciones web y móviles y desea una lógica de personalización unificada en todos los puntos de contacto digitales.

**Cómo funciona:**

La personalización de varias superficies amplía la opción A (basada en segmentos) o la opción B (basada en decisiones) para ofrecer contenido personalizado en varios tipos de superficies de AJO. Cada tipo de superficie (web, en la aplicación, tarjeta de contenido) puede tener diferentes formatos de contenido y mecanismos de envío, pero la lógica de personalización subyacente (pertenencia a audiencia o toma de decisiones) se comparte.

La implementación implica la configuración de superficies de canal para cada tipo de superficie, la creación de contenido específico de la superficie (HTML/CSS web para superficies web, mensajes estructurados para aplicaciones, diseños de tarjeta para tarjetas de contenido) y la creación de campañas dirigidas a la superficie adecuada. Web SDK gestiona la entrega desde la superficie web, mientras que Mobile SDK gestiona la entrega desde la aplicación y desde la tarjeta de contenido.

Las tarjetas de contenido son especialmente valiosas para mensajes personalizados persistentes y descartables en los paneles de la cuenta o en las pantallas de inicio de la aplicación. Los mensajes en la aplicación son ideales para comunicaciones contextuales y específicas de la sesión. La personalización web gestiona banners de pantalla completa, widgets de recomendación y contenido promocional.

**Consideraciones clave:**

- Cada tipo de superficie requiere su propia configuración de superficie de canal y creación de contenido
- Web SDK y Mobile SDK deben implementarse y configurarse a la vez
- El contenido debe diseñarse para cada formato de superficie (diferentes dimensiones, diseños, patrones de interacción)
- Las audiencias compartidas y la lógica de toma de decisiones garantizan la coherencia entre superficies
- Las pruebas deben cubrir todos los tipos de superficie entre dispositivos

**Ventajas:**

- Experiencia de personalización coherente en todos los puntos de contacto digitales
- La lógica compartida de audiencia y toma de decisiones reduce la duplicación
- Las tarjetas de contenido proporcionan una superficie de personalización persistente y no intrusiva
- Los mensajes en la aplicación permiten la personalización contextual y específica de la sesión en dispositivos móviles

**Limitaciones:**

- Mayor complejidad de implementación: requiere configuración para cada tipo de superficie
- Requiere implementación de Web SDK y Mobile SDK
- El contenido debe diseñarse y mantenerse para cada formato de superficie
- El alcance de las pruebas aumenta con cada tipo de superficie adicional

**Experience League:**

- [Información general sobre el canal en la aplicación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [Canal de tarjeta de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [Introducción al canal web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)

### Comparación de opciones

La siguiente tabla compara las tres opciones de implementación.

| Criterios | Opción A: Basada En Segmentos | Opción B: Basada En La Toma De Decisiones | Opción C: multisuperficie |
| --- | --- | --- | --- |
| Mejor para | Asignación de segmento a contenido conocida | Selección dinámica de contenido por perfil | Personalización coherente en la web y dispositivos móviles |
| Complejidad | Baja | Medium-High | Alto (se basa en A o B) |
| Latencia | El más rápido (resolución directa de segmentos) | Ligeramente superior (evaluación de toma de decisiones) | Depende de la opción subyacente (A o B) |
| Flexibilidad | Limitado a pares de contenido-segmento predefinidos | Alto: clasificación dinámica e idoneidad | Máximo: varias superficies con lógica compartida |
| Gestión de contenidos | Asignación manual de segmento a contenido | Biblioteca de ofertas centralizada con reglas de aceptación | Contenido por superficie con lógica de personalización compartida |
| Optimización | Pruebas A/B manuales | Optimización automática con clasificación de IA disponible | Optimización por superficie |
| Requiere | audiencias aptas para Edge, Web SDK | Ubicaciones, ofertas, reglas de idoneidad y decisiones | Web SDK + Mobile SDK, varias configuraciones de superficie |
| Superficies admitidas | Web (principal) | Web (principal) | Web + En la aplicación + Tarjeta de contenido |

### Elija la opción correcta

Comience con estas preguntas para seleccionar el método de implementación adecuado:

1. **¿Cuántas superficies?** Si necesita personalizar en la aplicación web y móvil, elija la opción C (que se basa en A o B para la lógica subyacente). Si es solo web, elija entre A y B.

2. **¿Cuán dinámica es su selección de contenido?** Si tiene una asignación bien definida de segmentos a variantes de contenido (por ejemplo, de 3 a 5 niveles de lealtad, cada uno con un banner a pantalla completa específico), elija Opción A. Si necesita seleccionar entre un catálogo de ofertas con elegibilidad y clasificación complejas, elija la Opción B.

3. **¿Necesita una selección optimizada para IA?** Si desea que el sistema aprenda y optimice automáticamente qué contenido tiene el mejor rendimiento para cada perfil, elija la Opción B con toma de decisiones clasificadas por IA.

4. **¿Cuántas variantes de contenido?** Si tiene menos de 10 variantes de contenido con asignaciones de segmentos claras, la opción A es más sencilla. Si tiene docenas de ofertas que necesitan filtrado y clasificación de elegibilidad, la Opción B se escala mejor.

5. **¿Planea ampliar a otros canales?** Si la lógica de toma de decisiones debe servir finalmente ofertas en canales de correo electrónico, web y otros, la opción B proporciona la base de toma de decisiones centralizada que amplía la toma de decisiones de oferta en canales múltiples.

## Fases de implementación

Esta sección muestra en detalle cada fase de la implementación.

### Fase 1: Definir audiencias y configurar la evaluación

**Función de aplicación:** RT-CDP: Evaluación de audiencia

**Lo que configurará:** Defina las audiencias que impulsan la selección de contenido de personalización. Estas audiencias representan los segmentos del visitante que recibirán experiencias personalizadas: niveles de fidelidad, etapas del ciclo vital, cohortes de comportamiento o grupos de afinidad del producto.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: método de evaluación de audiencia**
>
>¿Con qué rapidez se debe resolver la pertenencia a audiencias para la personalización? Esto afecta directamente a si la personalización puede producirse al cargar la página o requiere un retraso.
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Evaluación de Edge | Personalización web/aplicación en tiempo real que requiere una calificación de menos de un segundo | Se limita a simples comprobaciones de atributos de perfil y a la pertenencia a segmentos. No hay consultas de series temporales ni agregaciones complejas. Necesario para la personalización de visitantes conocidos. |
>| Evaluación de streaming | Calificación casi en tiempo real cuando los perfiles entran o salen de audiencias en función de eventos de comportamiento | Admite consultas de ventana de tiempo limitado y de evento único. Cambios de audiencia reflejados en minutos. Adecuado para superficies de tarjetas de contenido y aplicaciones en las que se admite un ligero retraso. |
>| Evaluación por lotes | Actualizaciones diarias de la audiencia para segmentos en función de agregaciones complejas o patrones históricos | Compatibilidad total con la función de regla de segmento. No es adecuado para la personalización en tiempo real, pero puede complementar las audiencias de Edge con segmentos precalculados complejos. |

>[!NOTE]
>**Decisión: atributos de Personalization**
>
>¿Qué atributos de perfil deben impulsar la definición de audiencia y la selección de contenido?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Atributos de perfil (nivel de fidelidad, fase del ciclo vital) | Personalización determinista basada en propiedades de cliente conocidas | Atributos estables y bien definidos. Fácil de asignar a variantes de contenido. Disponible en el perímetro si el perfil está configurado correctamente. |
>| Señales de comportamiento (historial de compras, patrones de navegación) | Personalization basado en comportamientos recientes y patrones de participación | Requiere atributos calculados o segmentos de flujo continuo. Más dinámico, pero más complejo de mantener. |
>| Puntuaciones de tendencia ([!DNL Customer AI]) | Personalización predictiva basada en la probabilidad de conversión, pérdida o compra | Requiere atributos calculados. Permite una personalización sofisticada, pero requiere datos de formación del modelo XML. |
>| Enfoque combinado | La mayoría de implementaciones de producción | Utiliza atributos de perfil para la segmentación primaria con señales de comportamiento y puntuaciones de tendencia para el refinamiento. |

**Navegación de la interfaz de usuario:** Cliente > Audiencias > Crear audiencia > Generar regla

**Detalles de configuración de clave:**

- Defina audiencias mediante el Generador de segmentos con expresiones de reglas de segmentos que hagan referencia a atributos de perfil
- Asegúrese de que las expresiones de reglas de segmentos cumplen los requisitos para la evaluación de Edge (comprobaciones de atributos simples, pertenencia a segmentos)
- Configure audiencias aptas para Edge para casos de uso de personalización en tiempo real
- Considere las audiencias de supresión para excluir a los visitantes convertidos recientemente o excluidos

**Documentación de Experience League:**

- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Fase 2: Configurar la toma de decisiones (solo para las opciones B y C)

**Función de aplicación:** AJO: Decisioning

**Lo que configurará:** Configure la infraestructura de decisiones que selecciona dinámicamente el contenido u oferta óptimos para cada visitante. Esto incluye ubicaciones (donde aparecen las ofertas), ofertas (qué contenido está disponible), reglas de elegibilidad (quién califica), estrategias de clasificación (cómo elegir el mejor) y políticas de decisión (cómo se conecta todo).

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: estrategia de clasificación**
>
>¿Cómo se deben clasificar las ofertas aptas para seleccionar la mejor para cada visitante?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Basado en prioridades (manual) | Casos de uso simples con una jerarquía de ofertas clara | Cada oferta tiene un valor de prioridad manual. La oferta elegible de mayor prioridad gana. Fácil de entender y controlar. |
>| Basado en fórmulas (expresión personalizada) | Cuándo la clasificación debe tener en cuenta los atributos de perfil | Las fórmulas de clasificación personalizadas hacen referencia a datos de perfil (por ejemplo, puntuación por nivel de lealtad + actualización). Flexible, pero requiere diseño y pruebas de fórmula. |
>| Clasificación de IA (optimización automática) | Cuando desee que el sistema optimice automáticamente la selección de ofertas | El modelo XML aprende qué ofertas funcionan mejor para qué perfiles. Requiere un mínimo de 1000 eventos de conversión para formación. Es ideal para ubicaciones de alto tráfico. |

>[!NOTE]
>**Decisión: límite de oferta**
>
>¿Debería haber límites en la cantidad de veces que se muestra una oferta a un visitante o entre todos los visitantes?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Límite por perfil | Evite que la fatiga vea la misma oferta repetidamente | Limita las impresiones por visitante durante un periodo de tiempo. Garantiza variedad en la experiencia personalizada. |
>| Límite global | Limitar el total de impresiones de una promoción u oferta de disponibilidad limitada | Limita las impresiones totales de todos los visitantes. Útil para promociones de cantidad limitada. |
>| Sin límite | Contenido permanente u ofertas siempre relevantes | Sin límites de impresión. Adecuado para contenido persistente como banners de nivel de fidelidad. |

**Navegación de la interfaz de usuario:** [!DNL Journey Optimizer] > Componentes > Administración de decisiones

**Detalles de configuración de clave:**

- Cree ubicaciones para cada superficie donde aparecerán las ofertas (banner web, área de mensaje en la aplicación, ranura de tarjeta de contenido)
- Defina las reglas de aceptación utilizando expresiones de reglas de segmentos que hagan referencia a atributos de perfil y pertenencia a audiencias
- Cree ofertas personalizadas con representaciones de contenido para cada ubicación
- Cree una oferta de reserva que cubra todas las ubicaciones (que se muestra cuando no se califica ninguna oferta personalizada)
- Organizar ofertas con calificadores de colección (etiquetas) y agrupar en colecciones
- Cree una política de decisión enlazando ubicaciones a colecciones con la estrategia de clasificación seleccionada

**Documentación de Experience League:**

- [Creación de ubicaciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fase 3: Configuración de superficies y canales

**Función de aplicación:** AJO: Configuración de canal

**Lo que configurará:** Configure las superficies de canal que definen dónde se enviará el contenido personalizado. Cada tipo de superficie (web, en la aplicación, tarjeta de contenido) requiere su propia configuración, en la que se especifica el URI de superficie, el formato de contenido y los parámetros de envío.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: superficies de destino**
>
>¿Qué superficies digitales recibirán contenido personalizado?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Solo canal web | Personalization centrado en las propiedades web | Requiere Web SDK. La implementación más sencilla. Cubre banners de pantalla completa, áreas promocionales y widgets de recomendaciones. |
>| Solo canal en la aplicación | Personalization se centró en las experiencias de aplicaciones móviles | Requiere Mobile SDK. Abarca mensajes contextuales y específicos de la sesión dentro de la aplicación. |
>| Solo canal de tarjeta de contenido | Mensajes personalizados persistentes y no permisibles | Requiere Mobile SDK o Web SDK. Las cartas persisten hasta que se descartan. Ideal para paneles y pantallas de inicio. |
>| Varias superficies (opción C) | Personalización coherente en la web y dispositivos móviles | Requiere Web SDK y Mobile SDK. Cada superficie necesita una configuración y un contenido independientes. |

>[!NOTE]
>**Decisión: enfoque de configuración de la superficie web**
>
>¿Cómo se debe configurar la superficie web para la entrega de contenido?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Aplicación de una sola página (SPA) | Aplicaciones web modernas con enrutamiento del lado del cliente | Usar `renderDecisions: true` en llamadas a Web SDK `sendEvent`. Contenido procesado automáticamente por SDK. |
>| Aplicación de varias páginas (MPA) | Páginas web tradicionales procesadas por el servidor | Contenido entregado al cargar la página mediante la respuesta de Edge Network. Puede requerir la configuración de URI de superficie de nivel de página. |

**Navegación de la interfaz de usuario:** [!DNL Journey Optimizer] > Administración > Canales > Superficies de canal

**Detalles de configuración de clave:**

- Para superficies web: configure el URI de la superficie web que coincida con las páginas de destino
- Para superficies en la aplicación: configure la superficie de la aplicación móvil con el ID de la aplicación y el tipo de superficie
- Para superficies de tarjeta de contenido: configure la superficie de tarjeta de contenido con ID de aplicación o contexto web
- Asegúrese de que la secuencia de datos tenga el servicio AJO habilitado para la entrega de personalización Edge

**Documentación de Experience League:**

- [Introducción al canal web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Configuración del canal web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)
- [Requisitos previos del canal en la aplicación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [Configuración de tarjeta de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)

### Fase 4: Creación de contenido

**Función de aplicación:** AJO: Creación de mensajes

**Lo que configurará:** Cree las variantes de contenido personalizadas para cada superficie y segmento u oferta. Esto incluye el diseño del diseño visual, la adición de expresiones de personalización que hacen referencia a atributos de perfil, la configuración de bloques de contenido condicional y la creación de fragmentos de contenido reutilizables.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: enfoque de contenido**
>
>¿Cómo se debe estructurar el contenido personalizado para este caso de uso?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Bloques de contenido condicionales | Las distintas secciones de contenido dentro del mismo diseño varían según la audiencia | Recurso de contenido único con reglas condicionales. Eficiente para variaciones menores (titular, texto de CTA, intercambio de imágenes). |
>| Separar variantes de contenido por tratamiento | Diseños diferentes por audiencia | Varios recursos de contenido completos. Más flexible pero más para mantener. Necesario para la experimentación de contenido. |
>| Contenido orientado a la toma de decisiones | Contenido seleccionado dinámicamente desde un catálogo de ofertas | Las representaciones de ofertas definen el contenido. La administración de contenido está centralizada en la biblioteca de ofertas. |

>[!NOTE]
>**Decisión: profundidad de Personalization**
>
>¿Qué parte del contenido se debe personalizar?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Personalización a nivel de superficie | Solo se personalizan elementos específicos (imagen a pantalla completa, CTA, banner de oferta) | Menor complejidad. Personalización centrada en áreas de alto impacto. Punto de partida más común. |
>| Personalización de toda la página | El diseño de página completo o el orden del contenido están personalizados | Mayor complejidad. Requiere una creación de contenido extensa. Ofrece la experiencia más adaptada. |
>| Personalización a nivel de token | Tokens de personalización en línea (nombre, nivel, saldo de puntos) | La forma más simple. Inserta valores de atributo de perfil en contenido estático. |

**Navegación por la interfaz de usuario:** [!DNL Journey Optimizer] > Campañas > Crear campaña > Editar contenido

**Donde las opciones difieren:**

**Para la opción A (basada en segmentos):**

- Cree variantes de contenido para cada segmento de audiencia mediante el diseñador web o el editor de código
- Uso de bloques de contenido dinámico con condiciones basadas en la pertenencia a audiencias
- Configure expresiones de personalización que hagan referencia a atributos de perfil (por ejemplo, `{{profile.person.name.firstName}}`, `{{profile.loyalty.tier}}`)
- Configure reglas condicionales para mostrar contenido diferente según la pertenencia a un segmento

**Para la opción B (basada en la toma de decisiones):**

- El autor ofrece representaciones de contenido para cada ubicación definida en la Fase 2
- Cada oferta tiene una o más representaciones (HTML, imagen, JSON) coincidentes con las ubicaciones
- Integrar la salida de decisiones en la página web o la aplicación incrustando ubicaciones de decisión
- El contenido se selecciona dinámicamente durante la ejecución: la creación se centra en elementos de oferta individuales

**Para la opción C (multisuperficie):**

- Crear contenido específico de la superficie para cada superficie de destino (HTML/CSS web, mensaje estructurado en la aplicación, diseño de tarjeta de contenido)
- Mantenga una lógica de personalización uniforme entre las superficies mientras se adapta a las restricciones de formato de cada superficie
- Prueba de representación de contenido en cada tipo de superficie

**Documentación de Experience League:**

- [Creación de experiencias web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Funciones de ayuda](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Creación de mensajes en la aplicación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [Crear tarjetas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/create-content-card)

### Fase 5: Configuración y activación de campañas

**Función de aplicación:** AJO: Campaign Execution

**Lo que configurará:** Cree y active la campaña de AJO que vincula la audiencia, la superficie y el contenido para su envío. Para la personalización web, las campañas suelen configurarse para su activación inmediata o continua en lugar de envíos programados una sola vez.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: tipo de campaña**
>
>¿Cómo se debe activar la campaña de personalización?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Campaña programada (siempre activada) | Personalización en curso que se ejecuta continuamente para todos los visitantes aptos | Establezca la fecha de inicio en inmediata y sin fecha de finalización. Campaign permanece activo hasta que se detiene manualmente. Más común en la personalización web. |
>| Campaña programada (con límite de tiempo) | Personalization vinculado a un periodo de promoción específico | Establecer las fechas de inicio y finalización. La campaña se detiene automáticamente después de la fecha de finalización. Adecuado para promociones de temporada u ofertas por tiempo limitado. |
>| Campaña activada por API | Personalization activado por un evento de aplicación específico | Se activa mediante programación. Resulta útil cuando la personalización solo debe aparecer como respuesta a eventos del sistema específicos. |

>[!NOTE]
>**Decisión: límite de frecuencia**
>
>¿Debe limitarse la frecuencia de impresión para esta personalización?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Aplicación de reglas de frecuencia | Personalización promocional u basada en ofertas que podría agotar a los visitantes | Evita que la misma personalización aparezca demasiadas veces. Configurado mediante reglas comerciales de AJO. |
>| Sin límite de frecuencia | Personalización de contenido permanente (banner de nivel de lealtad, contenido de panel) | Contenido siempre relevante que no cause fatiga. No se necesitan límites de impresión. |

**Navegación por la interfaz de usuario:** [!DNL Journey Optimizer] > Campañas > Crear campaña

**Detalles de configuración de clave:**

- Seleccione el canal web, en la aplicación o de la tarjeta de contenido y la superficie configurada en la fase 3
- Vincular la audiencia de destino definida en la fase 1
- Vincular el contenido creado en la fase 4
- Configure la programación de campaña (inmediata, con intervalo de fechas o activada por API)
- Revisión y activación de la campaña
- Para la experimentación de contenido: habilite la opción del experimento, defina los tratamientos, establezca la asignación del tráfico y las métricas de éxito antes de la activación

**Documentación de Experience League:**

- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introducción a las campañas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Reglas de frecuencia](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Introducción al experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### Fase 6: Seguimiento de impresiones y recopilación de datos

**Función de aplicación:** AEP: fuentes de datos y colección

**Lo que configurará:** Asegúrese de que las impresiones, interacciones y conversiones de experiencias personalizadas se rastrean hasta la plataforma para la creación de informes, la reevaluación de audiencias y la optimización de decisiones.

**Detalles de configuración de clave:**

- Verificar que Web SDK envíe `decisioning.propositionDisplay` eventos cuando se represente contenido personalizado
- Comprobar que Web SDK envía `decisioning.propositionInteract` eventos cuando los visitantes interactúan con contenido personalizado (clics, rechazos)
- Para Mobile SDK: compruebe que se capturan los eventos de interacción de mensajes en la aplicación y tarjetas de contenido
- Configure el seguimiento de eventos de conversión para las métricas de éxito descendentes (compras, suscripciones, adopción de funciones)
- Asegúrese de que los eventos incluyan el ID de la propuesta para la atribución a decisiones de personalización específicas

**Documentación de Experience League:**

- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Seguimiento de eventos con Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview)
- [Información general de Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)

### Fase 7: informar y optimizar

**Función de aplicación:** AJO: Reporting &amp; Performance Analysis, Reporting &amp; Analysis

**Lo que configurará:** Configure la supervisión y el análisis del rendimiento para medir la eficacia de la personalización en superficies, segmentos y variantes de contenido. Use los informes nativos de AJO para las métricas operativas y [!DNL Customer Journey Analytics] para el análisis del impacto comercial en canales múltiples.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: ámbito de informe**
>
>¿Qué nivel de análisis se necesita para este caso de uso de personalización?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Solo informes nativos de AJO | Monitorización operativa de las métricas de entrega y participación | Informes de campaña integrados con datos de impresión, clics y conversión. Configuración más rápida. |
>| Análisis en canales múltiples de CJA | Análisis profundo del impacto de la personalización en los resultados empresariales | Requiere conexión CJA y vista de datos. Habilita el análisis de funnel, las comparaciones de cohortes y el modelado de atribución en todos los canales. |
>| Tanto AJO como CJA | Visibilidad operativa y analítica completa | Utilice AJO para la monitorización diaria y CJA para el análisis estratégico. Recomendado para implementaciones de producción. |

**Navegación por la interfaz de usuario:**

- Informes de AJO: Campañas > Seleccionar campaña > Ver informe
- CJA: Proyectos > Crear nuevo proyecto

**Detalles de configuración de clave:**

- Acceso a informes en directo de campañas durante la entrega de personalización activa
- Revisar informes históricos para campañas completadas o análisis periódicos
- Para CJA: configure una conexión que incluya conjuntos de datos de evento de experiencia de AJO y cree una vista de datos con métricas de personalización
- Cree paneles que rastreen la tasa de participación de personalización, el alza de conversión, la tasa de aceptación de ofertas y los ingresos por visita
- Para la personalización basada en decisiones (Opción B): monitorice el rendimiento de las ofertas según la ubicación y la eficacia de la estrategia de clasificación

**Documentación de Experience League:**

- [Informe en vivo de la campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Consideraciones sobre la implementación

Esta sección cubre las barreras, los escollos comunes, las prácticas recomendadas y las decisiones de compensación relevantes para este patrón de caso de uso.

### Protecciones y límites

- Las búsquedas de Edge Network tienen un tiempo de respuesta SLA inferior a 200 ms para segmentos evaluados por Edge: [protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Máximo de 4000 definiciones de segmento por zona protegida — [Protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Los segmentos de Edge se limitan a simples comprobaciones de atributos y consultas de pertenencia a segmentos (sin consultas de series temporales): [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- Solo puede haber una política de combinación activa en Edge por zona protegida: [Políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- Máximo de 10 000 ofertas personalizadas aprobadas por espacio aislado: [protecciones de administración de decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 30 ubicaciones por decisión: [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Los modelos de clasificación de IA requieren un mínimo de 1000 eventos de conversión para la formación.
- Offer Tiempo de respuesta de entrega SLA es inferior a 500 ms en P95 para solicitudes de un solo ámbito
- Máximo de 500 campañas activas por zona protegida: [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 25 atributos calculados activos por zona protegida: [Controles de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)

### Peligros comunes

- **No se ha configurado la política de combinación de Edge:** Sin una política de combinación activa para Edge, Edge Network no puede resolver el perfil autenticado, lo que provoca que la personalización falle o vuelva a un comportamiento anónimo. Asegúrese de que exactamente una política de combinación tenga `isActiveOnEdge: true` en la zona protegida.
- **La audiencia no cumple los requisitos para Edge:** Si las expresiones de reglas de segmentos de audiencia utilizan consultas de series temporales, agregaciones complejas o referencias de `inSegment()` a segmentos solo por lotes, no calificarán para la evaluación de Edge y no podrán activar la personalización en tiempo real. Valide la idoneidad del perímetro durante la definición de audiencia.
- **Intervalo de vinculación de identidad durante la autenticación:** Cuando un visitante pasa de anónimo a autenticado, puede haber un breve momento en el que el perfil aún no se haya resuelto. Asegúrese de que la vinculación de identidad esté configurada correctamente y que Web SDK envíe la identidad autenticada mediante `identityMap` inmediatamente al iniciar sesión.
- **Falta oferta de reserva en la toma de decisiones:** Si no se configura ninguna oferta de reserva y no se personaliza ninguna oferta para un visitante, la decisión devuelve contenido vacío, lo que crea una experiencia rota. Configure siempre una oferta de reserva que cubra todas las ubicaciones.
- **Web SDK no envía eventos de visualización de propuesta:** Si `renderDecisions` se establece en `true` pero los eventos de visualización no se envían, el informe no reflejará las impresiones reales. Compruebe el seguimiento de eventos inspeccionando las solicitudes de red en las herramientas para desarrolladores del explorador.
- **Parpadeo del contenido al cargar la página:** Si el contenido personalizado no se oculta previamente durante la llamada de toma de decisiones, es posible que los visitantes vean el contenido predeterminado brevemente antes de que se reemplace. Utilice el fragmento de ocultamiento previo o la ocultación previa basada en CSS para eliminar el parpadeo.

### Prácticas recomendadas

- Comience con la personalización basada en segmentos (Opción A) para la implementación inicial y, a continuación, evolucione a basada en decisiones (Opción B) a medida que crezca el catálogo de ofertas y aumenten las necesidades de optimización
- Utilice audiencias evaluadas por Edge siempre que sea posible para la personalización en tiempo real; reserve audiencias de streaming y por lotes para casos de uso complementarios
- Implemente experimentación de contenido en experiencias personalizadas para validar que la personalización genera un aumento mensurable del contenido predeterminado
- Diseñar una personalización con una estrategia de degradación correcta: si el perfil no se puede resolver en el perímetro, muestre contenido predeterminado bien diseñado en lugar de una experiencia rota
- Utilice atributos calculados para crear señales de personalización de alto valor como la puntuación de participación, la afinidad del producto y los días transcurridos desde la última compra, que mejoran la calidad de la personalización basada en segmentos y en decisiones
- Mantenga un proceso de control de contenido para garantizar que el contenido personalizado esté actualizado, no utilice marca y sea compatible en todas las superficies
- Monitorice el rendimiento de la personalización por segmento para identificar qué audiencias se benefician más de la personalización y dónde es más fuerte el alza

### Decisiones de compensación

>[!NOTE]
>**Compensación: granularidad de Personalization vs. complejidad de administración de contenido**
>
>Una personalización más granular (más segmentos, más variantes de contenido, más superficies) ofrece experiencias cada vez más adaptadas, pero requiere proporcionalmente más esfuerzo de creación, mantenimiento y gobernanza del contenido.
>
>- **Favoritos de mayor granularidad:** Mejor experiencia del cliente, mayor participación, mayor alza de conversión
>- **Favoritos de menor granularidad:** implementación más rápida, menor carga de mantenimiento de contenido y administración más sencilla
>- **Recomendación:** Comience con 3-5 segmentos de alto impacto (por ejemplo, niveles de lealtad o etapas del ciclo vital) con una clara diferenciación de contenido. Amplíe la granularidad en función del aumento de rendimiento medido. Utilice la toma de decisiones (Opción B) para escalar la granularidad sin crecimiento proporcional de la administración de contenido.

>[!NOTE]
>**Compensación: toma de decisiones en tiempo real vs. control de contenido determinístico**
>
>La personalización basada en decisiones (Opción B) proporciona optimización dinámica, pero reduce el control directo sobre el contenido que ve cada visitante. La personalización basada en segmentos (Opción A) proporciona un control determinista completo, pero limita la optimización dinámica.
>
>- **Favoritos de decisión:** Escalabilidad, optimización automática, escenarios de elegibilidad complejos
>- **Favoritos basados en segmentos:** Previsibilidad, control de cumplimiento, transparencia de partes interesadas
>- **Recomendación:** Utilice la personalización basada en segmentos para el contenido sensible al cumplimiento (mensajería reglamentaria, precios específicos del nivel) donde se requiera un control exacto. Utilice la toma de decisiones para contenido promocional, ofertas y recomendaciones en los que la optimización dinámica añada valor.

>[!NOTE]
>**Compensación: disponibilidad de datos de Edge frente a riqueza de personalización**
>
>La personalización evaluada por Edge se limita a los atributos disponibles en el almacén de perfiles Edge. Las señales de personalización más completas (historial de comportamiento completo, atributos calculados complejos) pueden requerir una búsqueda en el lado del servidor o un cálculo previo.
>
>- **Favoritos solo de Edge:** Latencia de subsegundo, arquitectura más sencilla
>- **Favoritos de enriquecimiento precalculados:** Señales de personalización más ricas, definiciones de audiencia más sofisticadas
>- **Recomendación:** Use atributos calculados para preagregar señales de comportamiento enriquecidas en atributos de perfil disponibles para el perímetro. Esto proporciona la riqueza de datos de comportamiento con la velocidad de la evaluación de Edge.

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las tecnologías y configuraciones a las que se hace referencia en esta guía.

### Personalización del canal web

- [Introducción al canal web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Creación de experiencias web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Configuración del canal web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)

### Canales de tarjeta de contenido y en la aplicación

- [Información general sobre el canal en la aplicación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [Requisitos previos del canal en la aplicación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [Creación de mensajes en la aplicación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [Canal de tarjeta de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [Configuración de tarjeta de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)
- [Crear tarjetas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/create-content-card)

### Administración de decisiones

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Personalization y contenido

- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funciones de ayuda](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Identidad y perfil

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Reglas de vinculación de gráficos de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Resumen del perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Recopilación de datos y SDK

- [Información general de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Instalación de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [Información general de Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Información general sobre API de Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### Campañas y experimentación

- [Introducción a las campañas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introducción al experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### Atributos calculados y enriquecimiento

- [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Guía de IU de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Información general sobre Customer AI](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Informes y análisis

- [Informe en vivo de la campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Guía de integración de AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### Gobernanza y privacidad

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Información general sobre Advanced Data Lifecycle Management](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones del servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
