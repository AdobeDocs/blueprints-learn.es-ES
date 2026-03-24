---
title: Offer Decisioning
description: Aprenda a utilizar la lógica de decisión centralizada para seleccionar la mejor oferta o el contenido más próximo para un perfil en todos los canales.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 8fd511b3-0200-41bf-aff1-e3f2a00a578e
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8026'
ht-degree: 2%

---

# Offer Decisioning

Esta guía proporciona una referencia de implementación completa para Offer Decisioning mediante [!DNL Adobe Journey Optimizer] (AJO) Decisioning y [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP). Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesitan implementar una lógica de selección de ofertas centralizada que determine la mejor oferta de próxima generación para cada perfil de cliente en todos los canales.

Utilice esta guía para comprender qué se debe configurar, dónde existen las opciones y qué compensaciones se aplican a cada decisión.

El patrón desvincula la decisión &quot;qué mostrar&quot; de la lógica del canal &quot;dónde mostrarlo&quot;, lo que permite una selección de ofertas coherente y optimizada en el correo electrónico, la web, la aplicación móvil y cualquier otro punto de contacto. AJO Decisioning administra todo el ciclo de vida de la oferta: creación de ofertas y administración del catálogo, reglas de elegibilidad (que pueden ver cada oferta), estrategias de clasificación (cómo seleccionar entre ofertas aptas), ubicaciones (donde aparecen las ofertas) y políticas de decisión (que unen todo).

## Resumen del caso de uso

Las organizaciones suelen tener que presentar la oferta, la promoción o el incentivo más relevantes a cada cliente en el momento de la interacción. Tanto si la interacción se produce en una campaña de correo electrónico, en una página de inicio de un sitio web, en una aplicación móvil o en un punto de decisión dentro de un recorrido de varios pasos, el desafío es el mismo: seleccionar la oferta óptima de un catálogo de opciones disponibles en función de quién es el cliente, para qué cumplen los requisitos y qué oferta es la que tiene más probabilidades de impulsar el resultado deseado.

Offer Decisioning soluciona esto centralizando toda la lógica de selección de ofertas en el motor de gestión de decisiones de AJO. En lugar de codificar las asignaciones de ofertas en campañas o canales individuales, el motor de decisión evalúa los atributos de cada perfil, la pertenencia a audiencias y las señales contextuales para determinar la mejor oferta en tiempo real. Esta centralización garantiza que el mismo cliente reciba ofertas coherentes y optimizadas independientemente del canal al que acceda.

Este patrón difiere del ámbito de la personalización de aplicaciones/web de visitantes conocidos: Offer Decisioning no depende del canal y está centralizado, mientras que la personalización de visitantes conocidos se centra en la personalización de superficies digitales. Difiere de la recomendación de comportamiento en el modelo de catálogo: utilice Offer Decisioning cuando el conjunto de artículos elegibles esté regido por reglas comerciales, restricciones de elegibilidad o requisitos regulatorios (promociones, productos financieros, incentivos). Utilice recomendaciones de comportamiento cuando el conjunto de elementos sea grande, cambie continuamente y la selección esté impulsada por señales de similitud o afinidad de comportamiento (catálogos de productos, bibliotecas de contenido).

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

**[Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo de vida individuales.
**KPI:** participación, tasas de conversión, satisfacción del cliente (CSAT)

**[Aumentar los ingresos de ventas cruzadas y ventas adicionales](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
Promocione productos o servicios complementarios y de primera calidad a los clientes existentes en función del comportamiento y el historial de compras.
**KPI:**, porcentaje de ampliación de venta/venta cruzada, ingresos incrementales, valor de duración del cliente

**[Aumentar la lealtad del cliente y el valor de duración](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
Profundice las relaciones con los clientes y maximice el valor a largo plazo mediante programas de fidelidad, recompensas y participación personalizada.
**KPI:** valor de duración del cliente, retención, aumento de venta/venta cruzada %

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran cómo se puede aplicar la toma de decisiones de oferta en la práctica.

- La siguiente mejor oferta en campañas de correo electrónico: seleccione la promoción más relevante por destinatario en el momento de la entrega
- Titular promocional en tiempo real en el sitio web: al tomar decisiones, se selecciona la oferta al cargar la página en función del perfil del visitante
- Tarjeta personalizada en la aplicación con el mejor incentivo para la fase de ciclo vital del usuario
- Coherencia de ofertas en canales múltiples: la misma lógica de toma de decisiones sirve para el correo electrónico, la web y la notificación push para que el cliente vea una experiencia de oferta unificada
- Selección dinámica de cupones o descuentos basada en el nivel de valor del cliente (por ejemplo, los clientes de alto valor reciben una oferta premium)
- Selección de ofertas de ampliación o actualización de productos según el nivel de suscripción actual
- Personalización de ofertas de recompensas de fidelización en función del nivel y el historial de actividades

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir la eficacia de una implementación de Offer Decisioning.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de aceptación de ofertas | Porcentaje de ofertas enviadas que resultan en un clic, canje o conversión | Clics o reembolsos de ofertas / Ofertas totales entregadas |
| Distribución de selección de oferta | Proporción de cada oferta seleccionada en todas las decisiones | Recuento por oferta/Decisiones totales procesadas |
| Tasa de reserva | Porcentaje de decisiones en las que no se cualificó ninguna oferta personalizada y se proporcionó la reserva | Impresiones de reserva/Decisiones totales |
| Tasa de conversión | Porcentaje de destinatarios de la oferta que completaron la acción deseada (compra, registro, canje) | Conversiones / Impresiones de la oferta |
| Ingresos incrementales | Ingresos atribuibles a ofertas seleccionadas para la toma de decisiones en comparación con un grupo de control o reserva | Ingresos de ofertas personalizadas: ingresos de reserva/control |
| Puntuación de coherencia entre canales | Porcentaje de perfiles que reciben la misma oferta en varios canales dentro de una ventana definida | Ofertas coherentes/Impresiones multicanal totales |
| Tasa de clics en ofertas | Porcentaje de impresiones de oferta que resultan en un clic | Clics de ofertas / Impresiones de ofertas |

## Patrón de caso de uso

Esta sección describe la cadena de funciones y la definición de patrones para Offer Decisioning.

**Offer Decisioning**

Utilice la lógica de decisión centralizada para seleccionar la mejor oferta o el contenido siguiente para un perfil entre canales.

**Cadena de funciones:** Evaluación de audiencias > Idoneidad de la oferta > Estrategia de clasificación > Ejecución de decisiones > Entrega > Informes

Consulte la sección [Opciones de implementación](#implementation-options) para ver cómo se manifiesta cada composición.

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones de Adobe.

- **[!DNL Adobe Journey Optimizer] (AJO)**: motor de administración de decisiones para la creación de ofertas, reglas de elegibilidad, estrategias de clasificación, ubicaciones y políticas de decisión; configuración de canal y creación de mensajes para la entrega de ofertas; ejecución de campañas y recorridos
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Evaluación de audiencia para segmentos de elegibilidad de ofertas; datos de perfil y atributos calculados utilizados en la elegibilidad y la clasificación
- **[!DNL Adobe Experience Platform] (AEP)**: almacén de perfiles unificado, resolución de identidades y base de datos compatible con AJO y RT-CDP

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Se asume en contexto | Zona protegida de AJO con permisos de Decisioning habilitados. Funciones de administración de ofertas (administrador de decisiones, aprobador de ofertas) asignadas al equipo de implementación. | [Resumen de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home), [Resumen de control de acceso](https://experienceleague.adobe.com/es/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | El esquema de perfil debe incluir atributos utilizados para las reglas de idoneidad para la oferta (por ejemplo, nivel de lealtad, historial de compras, tipo de suscripción). Debe existir un esquema de respuesta/interacción de oferta para el seguimiento de impresiones, clics y conversiones de ofertas. | [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home), [Conceptos básicos de composición de esquemas](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/composition) |
| Fuentes de datos y recopilación | Se asume en contexto | Los atributos de perfil utilizados en las reglas de idoneidad deben ser actuales. Para la entrega web (Opción B), Web SDK debe implementarse con el servicio AJO habilitado en el conjunto de datos. Para la entrega por correo electrónico, los atributos de perfil deben poder resolverse en el momento de la entrega. | [Información general de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home), [Configurar flujos de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure) |
| Configuración de identidad y perfil | Se asume en contexto | Los perfiles deben poder resolverse en todos los canales en los que se envíen ofertas. Para la coherencia de la oferta en canales múltiples, la identidad unificada es crítica: el mismo perfil debe reconocerse en los contextos de correo electrónico, web y móvil. Se requiere una política de combinación activa para la entrega de aplicaciones/web en tiempo real. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home), [Introducción a las políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview) |
| Definición de audiencia y segmentación | Requerido | Las audiencias utilizadas como criterios de idoneidad para la oferta deben definirse y evaluarse (por ejemplo, &quot;clientes de alto valor&quot;, &quot;usuarios de prueba&quot;, &quot;nivel oro de fidelidad&quot;). El método de evaluación debe coincidir con la latencia de entrega (evaluación de Edge) para web/aplicación en tiempo real, por lotes o streaming para campañas de correo electrónico. | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home), [Guía de la interfaz de usuario del generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Las puntuaciones de tendencia de la inteligencia artificial aplicada al cliente, los cálculos de valor de duración y las métricas de participación mejoran significativamente la eficacia de la estrategia de clasificación. Los atributos calculados como &quot;días desde la última compra&quot; o &quot;gasto total en 90 días&quot; permiten reglas de elegibilidad y clasificación basadas en fórmulas más precisas. | [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview), [Resumen de inteligencia artificial aplicada al cliente](https://experienceleague.adobe.com/es/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Administración del ciclo de datos | Recomendado | El historial de ofertas y los datos del evento de decisión se acumulan con el tiempo. Las políticas de retención (caducidad) deben configurarse para los conjuntos de datos de evento de interacción de ofertas para administrar el almacenamiento y cumplir con los requisitos de retención de datos. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/home), [Caducidad de conjuntos de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| Etiquetado y aplicación del uso de datos | Recomendado | Las etiquetas de gobernanza garantizan que las ofertas con criterios de segmentación confidenciales (por ejemplo, estado financiero, condiciones de salud) cumplan con las políticas de uso de datos. Las etiquetas de los campos utilizados en las reglas de idoneidad impiden la segmentación de ofertas no compatible. | [Resumen de control de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home), [Resumen de etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview) |
| Monitorización y observabilidad | Recomendado | Se debe monitorizar el rendimiento del motor de decisión, las tasas de reserva y el estado de la entrega de las ofertas. Las alertas para tasas de reserva altas pueden indicar una configuración incorrecta de la regla de elegibilidad o problemas de actualización de datos. | [Resumen de alertas](https://experienceleague.adobe.com/es/docs/experience-platform/observability/alerts/overview), [Resumen de Observability Insights](https://experienceleague.adobe.com/es/docs/experience-platform/observability/home) |
| Informes y análisis | Incluido | La creación de informes de rendimiento de las ofertas forma parte de la cadena de funciones (Fase 7). El análisis de CJA permite medir la efectividad de ofertas en canales múltiples, la atribución del impacto en los ingresos y la identificación de oportunidades de optimización. | [Información general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview), [Información general de Analysis Workspace](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/home) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del Catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Journey Optimizer] (AJO)

En la tabla siguiente se enumeran las funciones de AJO y las fases de implementación en las que están configuradas.

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Decisioning | Fase 3: Configuración de decisiones | Cree elementos de oferta, defina reglas de elegibilidad, configure estrategias de clasificación, cree ofertas de reserva, defina ubicaciones y cree políticas de decisión |
| Configuración de canal | Fase 4: Configuración de canal y superficie | Configure las superficies de canal por correo electrónico, web, en la aplicación o basadas en código para la entrega de ofertas |
| Creación de mensajes | Fase 5: Configuración de contenido y envío | Diseñar plantillas de mensajes con zonas de colocación de ofertas; configurar experiencias basadas en código para la entrega web/aplicación |
| Ejecución de campaña | Fase 5: Configuración de contenido y envío | Ejecutar campañas programadas o activadas por API que invoquen directivas de decisión (Opción A) |
| Experimentación de contenido | Fase 5: Configuración de contenido y envío | Opcionalmente, la prueba A/B permite utilizar diferentes estrategias de clasificación u ofrecer variantes creativas |
| Informes y análisis de rendimiento | Fase 7: Informes y monitorización del rendimiento | Monitorice la distribución de la selección de ofertas, las tasas de aceptación, las tasas de reserva y el rendimiento a nivel de canal |

### [!DNL Real-Time CDP] (RT-CDP)

En la tabla siguiente se enumeran las funciones RT-CDP y las fases de implementación en las que están configuradas.

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Evaluación de audiencia | Fase 2: Evaluación de audiencias | Defina y evalúe las audiencias utilizadas para las reglas de idoneidad para la oferta; seleccione el método de evaluación adecuado (por lotes, streaming o Edge) |
| Enriquecimiento de perfiles | Fase 1 (compatibilidad): Atributos calculados | Enriquezca los perfiles con atributos calculados y puntuaciones de tendencia que mejoren la eficacia de la estrategia de clasificación |

## Prerrequisitos

Complete los siguientes requisitos previos antes de comenzar la implementación.

- [ ] zona protegida de AJO con capacidades de Administración de decisiones habilitadas
- [ ] funciones de usuario con permisos de Administración de decisiones (crear/editar ofertas, ubicaciones, decisiones)
- [ ]: el esquema de perfil incluye los atributos necesarios para la idoneidad de la oferta (por ejemplo: nivel de lealtad, segmento de cliente o nivel de suscripción)
- [ ] Los datos del perfil están actuales y se han ingerido activamente para mantener actualizados los atributos de elegibilidad
- [ ] para opción A (correo electrónico): superficie de canal de correo electrónico configurada con subdominio verificado y grupo de IP calentadas
- [ ] para Opción B (web/aplicación): Web SDK implementado con el servicio AJO habilitado en el conjunto de datos; directiva de combinación activa para Edge configurada
- [ ] para Opción C (Recorrido): permisos de lienzo de Recorrido y al menos un evento de entrada de recorrido o una audiencia configurada
- [ ] recursos creativos de ofertas (imágenes, copias, CTA) preparados para cada combinación de oferta y ubicación
- [ ] contenido de oferta de reserva preparado para cada ubicación
- [ ] audiencias para reglas de elegibilidad de ofertas definidas y evaluadas en RT-CDP

## Opciones de implementación

Esta sección describe las opciones de implementación disponibles para Offer Decisioning. Cada opción ofrece un canal de entrega y un contexto de caso de uso diferentes.

### Opción A: Offer Decisioning de correo electrónico

Esta opción es perfecta para seleccionar la mejor oferta que se debe incluir en las campañas de correo electrónico salientes: correos electrónicos promocionales, personalización de boletines informativos y correos electrónicos del ciclo vital con contenido de oferta dinámica. La decisión se toma en el momento de procesar el mensaje para cada destinatario.

#### Cómo funciona

Las políticas de decisión se invocan durante el procesamiento del mensaje de correo electrónico para seleccionar la mejor oferta para cada destinatario. La plantilla de correo electrónico incluye una zona de colocación de ofertas en la que el motor de decisión inserta la representación de contenido de la oferta seleccionada (imagen, HTML o texto). En el momento de la entrega, el motor evalúa el perfil de cada destinatario con las reglas de idoneidad para la oferta, aplica la estrategia de clasificación e incrusta el contenido de la oferta ganadora en el correo electrónico.

Este método funciona tanto con campañas programadas (evaluadas en el momento de la ejecución de la campaña) como con correos electrónicos incrustados en el recorrido (evaluados cuando el perfil llega al nodo de acción del mensaje). El contenido de la oferta (imagen, titular, texto independiente y CTA) se personaliza por destinatario en función del resultado de la decisión.

#### Consideraciones clave

- La idoneidad de la oferta se evalúa en el momento de la entrega mediante el estado actual del perfil
- La evaluación de audiencias por lotes es suficiente, ya que las decisiones se toman durante el procesamiento de mensajes
- Cada oferta necesita una representación de contenido de imagen o HTML para la ubicación del correo electrónico
- La oferta de reserva debe tener contenido para cada ubicación de correo electrónico utilizada

#### Ventajas

- Ruta de implementación más sencilla: utiliza la entrega de correo electrónico de recorrido o campaña estándar
- No hay requisitos de SDK del lado del cliente
- Funciona con infraestructuras de correo electrónico y superficies de canal existentes
- Admite grandes volúmenes de audiencia mediante la ejecución de campañas por lotes

#### Limitaciones

- La decisión se toma en el momento del envío; no se puede adaptar al comportamiento posterior al envío
- El contenido de la oferta es estático una vez enviado el correo electrónico (sin actualizaciones en tiempo real)
- Limitado a los atributos de perfil disponibles en el almacén de perfiles de hub (no de edge)

#### Recursos de Experience League

- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

### Opción B: Web/aplicación de decisiones de oferta en tiempo real

Esta opción es perfecta para la selección de ofertas en tiempo real en páginas web o aplicaciones móviles: titulares promocionales de página de inicio, widgets de oferta del tablero de cuentas, tarjetas de oferta en la aplicación o cualquier superficie digital en la que la oferta deba seleccionarse en el momento en que se carga la página o se procesa la pantalla.

#### Cómo funciona

Las políticas de decisión se invocan al cargar la página o al procesar la pantalla de la aplicación a través de la red de Edge Decisioning o mediante experiencias basadas en código. Cuando un visitante carga una página, Web SDK envía una solicitud a Edge Network, que evalúa el perfil de Edge del visitante frente a las reglas de elegibilidad de las ofertas y las estrategias de clasificación. La oferta seleccionada se devuelve en la respuesta y se procesa en la ubicación configurada en la superficie digital.

En el caso de las experiencias basadas en código, la aplicación recupera la respuesta de decisión y procesa el contenido de la oferta mediante una lógica front-end personalizada. Para las experiencias de canal web, el canal web de AJO puede insertar el contenido de la oferta directamente en la página mediante la creación visual o basada en código.

#### Consideraciones clave

- Requiere la implementación de Web SDK o Mobile SDK con el servicio de AJO habilitado en el conjunto de datos
- Se requiere una política de combinación activa para Edge para las búsquedas de perfiles en tiempo real
- Las audiencias utilizadas para los requisitos deben admitir la evaluación de Edge (comprobaciones de atributos simples y pertenencia a segmentos)
- Las representaciones de contenido de las ofertas deben utilizar formatos JSON o URL de imagen para el procesamiento en el lado del cliente
- El seguimiento de impresiones debe implementarse para capturar las vistas de ofertas y los clics

#### Ventajas

- Selección de ofertas en tiempo real dentro de la sesión en función del estado del perfil actual del visitante
- Latencia de decisión subsegunda a través de Edge Network
- Las ofertas se adaptan a los datos de perfil más actuales disponibles en Edge
- Admite pruebas A/B de estrategias de oferta mediante experimentación de contenido

#### Limitaciones

- Requiere implementación de SDK del lado del cliente (Web SDK o Mobile SDK)
- El perfil de Edge tiene un subconjunto de atributos de perfil hub completos; es posible que las reglas de idoneidad complejas no se evalúen correctamente
- Los segmentos de Edge tienen restricciones de complejidad de reglas de segmentos (sin consultas de series temporales)
- Requiere desarrollo front-end para procesamiento personalizado en experiencias basadas en código

#### Recursos de Experience League

- [Entrega de ofertas mediante la API de Edge Decisioning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Canal de experiencia basado en código](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/code-based-experience/get-started-code-based)

**En qué se diferencia de la opción B de personalización de aplicaciones/web de visitantes conocidos:**

La infraestructura es idéntica: ambos utilizan AJO Decisioning en el perímetro con Web SDK y una política de combinación activa para el perímetro. La diferencia es el modelo de gobernanza del catálogo. Esta opción rige un catálogo de ofertas limitado con reglas de idoneidad, contadores de límite y fechas de validez. Utilícela cuando las restricciones comerciales o regulatorias determinen qué ofertas se pueden mostrar y con qué frecuencia. [Personalización web/aplicación de visitante conocido](known-visitor-web-app-personalization.md) La opción B selecciona elementos de contenido mediante la pertenencia a segmentos o estrategias de clasificación sin la administración del ciclo de vida de ofertas. Si el conjunto de artículos es grande, cambia continuamente y no requiere límite ni control de elegibilidad, use la Opción B de visitante conocido en su lugar.

### Opción C: nodo de decisión de Recorrido

Esta opción es mejor para la selección de ofertas dentro de un recorrido de varios pasos: seleccionar la mejor oferta en un punto de decisión en un recorrido de clientes y, a continuación, entregarla a través del siguiente nodo de acción. Utilícelo cuando la decisión de oferta forme parte de un flujo de orquestación más amplio con esperas, condiciones y varias acciones de mensaje.

#### Cómo funciona

Las políticas de decisión se invocan desde un nodo de decisión dentro de un lienzo de recorrido de AJO. Cuando un perfil llega al nodo de decisión, el motor evalúa la idoneidad y la clasificación de la oferta para seleccionar la oferta óptima. La oferta seleccionada informa de la siguiente acción de mensaje: qué contenido de oferta se va a incluir, qué canal se va a utilizar o qué rama de recorrido se va a tomar en función del resultado de la oferta.

Este método permite recorridos adaptables en los que la decisión de oferta influye en los pasos de recorrido siguientes. Por ejemplo: un recorrido puede seleccionar la mejor oferta, enviarla por correo electrónico, esperar a la participación y, a continuación, enviar una notificación push si la oferta no se ha abierto.

#### Consideraciones clave

- El recorrido debe diseñarse con un nodo de decisión seguido de uno o más nodos de acción de mensaje
- La idoneidad de la oferta se evalúa mediante el estado del perfil en el momento en que este alcanza el nodo de decisión
- Los pasos de espera de recorrido entre la decisión y la entrega pueden hacer que el estado del perfil cambie
- Se puede combinar con la bifurcación de recorridos para seguir diferentes rutas en función de la oferta seleccionada

#### Ventajas

- Integra la selección de ofertas en flujos de orquestación de varios pasos
- Habilita recorridos adaptables en los que la opción de oferta influye en los pasos siguientes
- Admite entrega en canales múltiples dentro del mismo recorrido (correo electrónico, push, SMS)
- Se puede combinar con condiciones de recorrido para el seguimiento de la participación posterior a la oferta

#### Limitaciones

- Es más complejo de configurar que la toma de decisiones de campaña independiente
- Se aplican límites de rendimiento de recorrido (tasa de entrada de 5000 perfiles por segundo)
- La decisión está vinculada al contexto del recorrido: los cambios requieren el control de versiones del recorrido
- El recorrido debe volver a publicarse para que las actualizaciones del catálogo de ofertas o de la directiva de decisiones surtan efecto

#### Recursos de Experience League

- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Introducción a recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/journey)

### Comparación de opciones

En la tabla siguiente se comparan las tres opciones de implementación en función de criterios clave.

| Criterios | Opción A: toma de decisiones por correo electrónico | Opción B: web/aplicación en tiempo real | Opción C: nodo de decisión de Recorrido |
| --- | --- | --- | --- |
| Mejor para | Agrupar campañas por correo electrónico con selección de ofertas por destinatario | Banners de ofertas en tiempo real en superficies web/aplicaciones | Selección de ofertas dentro de recorridos organizados de varios pasos |
| Latencia de decisión | En el momento del envío (segundos por destinatario durante el procesamiento por lotes) | Subsegundo (Edge Network) | En la ejecución del nodo de recorrido (segundos) |
| Canal | Correo electrónico | Superficies basadas en código, aplicaciones móviles y web | Cualquier canal (correo electrónico, push, SMS) dentro del recorrido |
| Se requiere SDK | No | Sí (Web SDK o Mobile SDK) | No (para correo electrónico/push); Sí (si el canal web es una acción de recorrido) |
| Evaluación de audiencia | Lote o flujo continuo | Edge | Lote, flujo o borde (según la entrada de recorrido) |
| Ámbito de datos del perfil | Perfil de concentrador completo | Perfil de Edge (subconjunto) | Perfil de concentrador completo |
| Complejidad | Baja | Medium-High | Medio |
| Rendimiento | Alto (volúmenes de campaña por lotes) | Alta (escala Edge Network) | Medium (se aplican límites de rendimiento de recorrido) |

### Elija la opción correcta

Siga estas directrices para seleccionar la mejor opción de implementación para su caso de uso.

- **Elija la opción A** si el caso de uso principal es seleccionar la mejor oferta por destinatario en campañas de correo electrónico salientes y no hay ninguna SDK del lado del cliente disponible. Esta es la ruta de implementación más sencilla y funciona bien para correos electrónicos promocionales, boletines informativos y campañas del ciclo vital.
- **Elija la opción B** si las ofertas deben seleccionarse en tiempo real en el momento en que un visitante carga una página web o abre una aplicación móvil. Esto requiere Web SDK o Mobile SDK y una política de combinación activa para Edge, pero ofrece la selección de ofertas más rápida y contextual.
- **Elija la opción C** si la decisión de oferta es parte de un recorrido del cliente más amplio con varios pasos, esperas y ramificación condicional. Esta es la opción correcta cuando la oferta seleccionada debe influir en las acciones de recorrido descendentes o cuando se necesita un seguimiento de varios canales basado en la participación en la oferta.
- **Combine opciones** cuando las ofertas deban entregarse de manera consistente entre canales. Utilice la misma política de decisión en las tres opciones para asegurarse de que el cliente vea la misma oferta en el correo electrónico (opción A), en el sitio web (opción B) y dentro de un seguimiento del recorrido (opción C).

## Fases de implementación

Las siguientes fases describen la secuencia de implementación de extremo a extremo para Offer Decisioning.

### Fase 1: Validar los requisitos previos básicos

**Función de la aplicación:** AEP: Modelado y preparación de datos, AEP: Configuración de identidad y perfil

Esta fase valida que la capa de datos fundacional admite Offer Decisioning. Los esquemas de perfil deben incluir los atributos utilizados en las reglas de aceptación de ofertas y la configuración de identidad debe habilitar la resolución de perfiles en canales múltiples.

#### Decisión: Atributos de perfil para la elegibilidad

Determine qué atributos de perfil se utilizarán en las reglas de aceptación de ofertas.

>[!NOTE]
>La elección de los atributos de perfil afecta tanto al diseño de las reglas de aceptación como a la eficacia de la estrategia de clasificación. Considere los atributos calculados y las puntuaciones de tendencia para mejorar la calidad de la decisión.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Atributos de perfil estándar (nivel de lealtad, historial de compras) | Los atributos ya existen en el esquema de perfil | No se necesitan cambios de esquema; compruebe la actualización de los datos |
| Atributos calculados (valor de duración, puntuación de participación) | La idoneidad o la clasificación dependen de los datos de comportamiento agregados | Requiere la configuración de S1; agrega una dependencia en la cadencia de actualización de atributos calculada |
| Puntuaciones de tendencia de Customer AI | La clasificación debe aprovechar las predicciones basadas en ML | Requiere datos de formación suficientes (más de 10 000 perfiles con evento de destinatario); tiempo de formación del modelo |

#### Detalles de configuración clave

- Compruebe que el esquema de perfil incluye campos a los que se hace referencia en las reglas de idoneidad (por ejemplo, `_tenantId.loyaltyTier`, `_tenantId.subscriptionType`)
- Confirme que existe el esquema de seguimiento de interacción de la oferta para los eventos de impresión, clics y conversión
- Para la opción B: Compruebe que la política de combinación activa en el perímetro está configurada y que el flujo de datos de Web SDK tiene habilitado el servicio AJO

#### Documentación de Experience League

- [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home)
- [Habilitar un esquema para perfil](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview)

### Fase 2: Configurar la evaluación de audiencias

**Función de aplicación:** RT-CDP: Evaluación de audiencia

Esta fase define y evalúa las audiencias utilizadas como criterios de idoneidad para la oferta. Estas audiencias determinan qué segmentos de clientes cumplen los requisitos para ofertas específicas (por ejemplo, &quot;clientes de alto valor&quot; cumplen los requisitos para ofertas Premium, &quot;usuarios de prueba&quot; para ofertas de conversión).

#### Decisión: método de evaluación de audiencia

Determine la rapidez con la que el abono a audiencia debe actualizarse para poder optar a la oferta.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Evaluación por lotes | Opción A (campañas por correo electrónico) en la que la idoneidad se evalúa en el momento del envío | El más sencillo; se admiten todas las expresiones de reglas de segmentos; actualización diaria o bajo demanda |
| Evaluación de streaming | Opción A o C cuando se necesitan actualizaciones de audiencia casi en tiempo real entre lotes | Automático para segmentos aptos; compatibilidad limitada con reglas de segmentos (eventos únicos, comparaciones de atributos) |
| Evaluación de Edge | Opción B (web/aplicación en tiempo real) donde la idoneidad debe evaluarse al cargar la página | Subsegundo; necesario para ofertas web/aplicación en tiempo real; limitado a simples comprobaciones de atributos y abono a segmentos |

**Navegación de la interfaz de usuario:** Cliente > Audiencias > Crear audiencia > Generar regla

#### Detalles de configuración clave

- Defina audiencias de segmentación para los requisitos de oferta (por ejemplo, &quot;Nivel Gold de fidelidad&quot;, &quot;Clientes de alto valor&quot;, &quot;Usuarios de prueba&quot;)
- Defina audiencias de supresión si es necesario (por ejemplo, &quot;Oferta X recibida recientemente&quot;)
- Para la opción B: compruebe que las audiencias de idoneidad cumplen los requisitos para la evaluación de extremos; evite consultas de series temporales y agregaciones complejas en las expresiones de reglas de segmentos

#### Dónde divergen las opciones

**Para La Opción A (Toma De Decisiones Por Correo Electrónico):**
La evaluación por lotes o de flujo continuo es suficiente. Las audiencias se evalúan antes o durante la ejecución de la campaña. Las expresiones de reglas de segmentos complejos, incluidas las condiciones basadas en el tiempo y las agregaciones de eventos, son totalmente compatibles.

**Para Opción B (Web/Aplicación En Tiempo Real):**
Se requiere la evaluación de Edge. Las audiencias deben utilizar comprobaciones de atributos sencillas o condiciones de pertenencia a segmentos. Pruebe la idoneidad del perímetro comprobando que la expresión de regla del segmento cumple los requisitos para la segmentación de perímetros.

**Para Opción C (Nodo De Decisión De Recorrido):**
Cualquier método de evaluación funciona según los criterios de entrada de recorrido. Si el recorrido utiliza entradas basadas en audiencias, el método de evaluación de audiencias coincide con los requisitos del recorrido.

#### Documentación de Experience League

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)

### Fase 3: Configuración de la toma de decisiones

**Función de aplicación:** AJO: Decisioning

Esta es la fase principal en la que se crean el catálogo de ofertas, las reglas de elegibilidad, las estrategias de clasificación y las políticas de decisión. Esta fase crea la configuración del motor de decisión que comparten todas las opciones de entrega (A, B, C).

#### Decisión: Canal de ubicación y formato de contenido

Determine dónde aparecerán las ofertas y en qué formato.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Correo electrónico (HTML) | Opción A: ofrecer contenido procesado como HTML dentro del cuerpo del correo electrónico | Admite formato enriquecido; debe ser compatible con clientes de correo electrónico |
| Correo electrónico (URL de imagen) | Opción A: oferta representada como imagen alojada en el correo electrónico | Más sencillo; la imagen debe estar alojada y ser accesible; no hay texto dinámico |
| Web (HTML) | Opción B — oferta representada como HTML en una página web | Control de diseño completo; admite elementos interactivos |
| Web/móvil (JSON) | Opción B: datos de oferta devueltos como JSON para un procesamiento personalizado | Máxima flexibilidad; requiere desarrollo front-end para procesar |
| Basado en código (JSON) | Opción B: datos de ofertas para superficies de experiencias basadas en código | La aplicación controla la renderización; lo más flexible |

#### Decisión: Estrategia de clasificación

Determine cómo se debe seleccionar la mejor oferta entre las ofertas aptas.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Basado en prioridades (manual) | Catálogos de ofertas pequeñas; reglas comerciales explícitas para la ordenación de ofertas | Más fácil de configurar; asignar manualmente el valor de prioridad por oferta; determinístico |
| Basado en fórmulas (expresión personalizada) | La clasificación debe tener en cuenta los atributos del perfil (por ejemplo, nivel de lealtad, actualización) | Flexible; utiliza datos de perfil para calcular una puntuación de clasificación; requiere el diseño de la expresión de regla de segmento |
| Clasificación de IA (optimización automática) | Catálogos de ofertas grandes; desea que ML optimice la selección con el tiempo | Requiere un mínimo de 1000 eventos de conversión para la formación de modelos; aprende de los datos de rendimiento de las ofertas |

#### Decisión: Límite de oferta

Determine si debe haber límites en cuanto a la cantidad de veces que se muestra una oferta.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Límite por perfil | Evitar que la misma oferta se muestre demasiadas veces a un cliente | Evita la fatiga de la oferta; retraso del contador de unos segundos en escenarios de alto rendimiento |
| Límite global | Limitar las impresiones totales de una oferta en todos los perfiles (por ejemplo, inventario limitado) | Controla el suministro de ofertas; una vez alcanzado el límite, la oferta se excluye de las decisiones |
| Sin límite | Las ofertas tienen disponibilidad ilimitada | Lo más sencillo; adecuado para promociones continuas |

**Navegación de la interfaz de usuario:** Componentes > Administración de decisiones > Ubicaciones / Reglas / Ofertas / Decisiones

#### Detalles de configuración clave

1. **Crear ubicaciones**: defina dónde aparecen las ofertas especificando el tipo de canal y el formato de contenido para cada ubicación.
   - IU: Componentes > Administración de decisiones > Ubicaciones
   - Cree una ubicación por combinación de canal y formato (por ejemplo, &quot;Email Hero Banner - HTML&quot;, &quot;Web Homepage - JSON&quot;, &quot;Mobile App Card - JSON&quot;)

2. **Definir reglas de elegibilidad**: cree reglas utilizando expresiones de reglas de segmentos que hagan referencia a atributos de perfil o a pertenencia a audiencias.
   - IU: Componentes > Administración de decisiones > Reglas
   - Las reglas pueden hacer referencia a miembros de audiencias, atributos de perfil (nivel de lealtad, tipo de suscripción), restricciones de fecha o datos contextuales

3. **Crear ofertas personalizadas**: cree cada oferta con representaciones de contenido para cada ubicación, asigne reglas de elegibilidad, establezca prioridad y configure un límite opcional.
   - IU: Componentes > Administración de decisiones > Ofertas > Crear oferta
   - Cada oferta necesita una representación de contenido por ubicación (por ejemplo, HTML para correo electrónico, JSON para web)
   - Asigne reglas de aceptación para controlar qué perfiles pueden ver cada oferta
   - Definición de fechas de validez de la oferta (inicio/final) y límite de frecuencia opcional
   - Apruebe cada oferta para que sea apta para la toma de decisiones

4. **Crear ofertas de reserva**: cree una oferta predeterminada para cada ubicación que se muestre cuando no se califique ninguna oferta personalizada.
   - IU: Componentes > Administración de decisiones > Ofertas > Crear oferta de reserva
   - La reserva debe tener representaciones para cada ubicación utilizada en la decisión

5. **Crear calificadores y colecciones**: organice ofertas en colecciones con etiquetas de calificador.
   - IU: Componentes > Administración de decisiones > Cualificadores de recopilación
   - Ofertas relacionadas con el grupo (por ejemplo, &quot;Promociones de verano&quot;, &quot;Recompensas de fidelidad&quot;) para su uso en ámbitos de decisión

6. **Crear directivas de decisión**: vincule ubicaciones, colecciones, estrategias de clasificación y ofertas de reserva a decisiones ejecutables.
   - IU: Componentes > Administración de decisiones > Decisiones > Crear decisión
   - Cada ámbito de decisión vincula una ubicación a una colección y especifica el método de clasificación

#### Documentación de Experience League

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear calificadores de colección](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fase 4: Configuración de canal y superficie

**Función de aplicación:** AJO: Configuración de canal

Esta fase configura las superficies de canal a través de las cuales se enviarán las ofertas. La configuración depende de las opciones de implementación que se utilicen.

#### Decisión: Tipo de canal

Determine qué canal de mensajería requiere el caso de uso.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Correo electrónico | Opción A o Opción C con envío de correo electrónico | Requiere delegación de subdominios, grupo de IP y configuración del remitente |
| Web | Opción B para entrega en superficie web | Requiere Web SDK y configuración de secuencia de datos |
| En la aplicación | Opción B para la entrega de aplicaciones móviles | Requiere SDK móvil y credenciales push |
| Experiencia basada en código | Opción B para superficies de renderización personalizadas | Más flexible; la aplicación gestiona el procesamiento |

#### Dónde divergen las opciones

**Para La Opción A (Toma De Decisiones Por Correo Electrónico):**
- IU: Administración > Canales > Superficies de canal > Crear superficie (correo electrónico)
- Configuración de subdominio, grupo de IP, nombre/correo electrónico del remitente, respuesta, cancelación de suscripción
- Compruebe los registros SPF, DKIM y DMARC del subdominio de envío

**Para Opción B (Web/Aplicación En Tiempo Real):**
- IU: Administración > Canales > Superficies de canal > Crear superficie (web o en la aplicación)
- Para la web: configure el patrón de URL de la superficie web
- Para experiencias basadas en código: Defina el URI de superficie para la aplicación
- Compruebe que el flujo de datos tiene habilitado el servicio AJO

**Para Opción C (Nodo De Decisión De Recorrido):**
- Configure las superficies de canal para cada canal utilizado en el recorrido (correo electrónico, push, SMS o web)
- Cada acción de mensaje de recorrido requiere una superficie de canal activa correspondiente

#### Documentación de Experience League

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configuración de superficie de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fase 5: Configuración de contenido y envío

**Función de la aplicación:** AJO: Creación de mensajes, AJO: Ejecución de campañas

En esta fase se diseñan las plantillas de mensaje o las superficies de experiencia que muestran la oferta seleccionada y, a continuación, se configura el mecanismo de entrega (campaña, recorrido o experiencia basada en código).

#### Decisión: enfoque del contenido para la representación de ofertas

Determine cómo se debe integrar el contenido de la oferta en el mensaje o la experiencia.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Componente de decisión de oferta en Email Designer | Opción A: incrustar ubicación de oferta en la plantilla de correo electrónico | Arrastrar y soltar; el contenido de la oferta se procesa automáticamente según el resultado de la decisión |
| Experiencia basada en código con política de decisión | Opción B: la aplicación recupera y procesa los datos de ofertas | Control máximo sobre el procesamiento; requiere desarrollo front-end |
| Acción de mensaje de recorrido con decisión incrustada | Opción C: las fuentes de los nodos de decisión ofrecen contenido al mensaje de recorrido | La selección y la entrega de ofertas se organizan dentro del flujo de recorrido |

#### Decisión: Tipo de campaña (solo opción A)

Determine si se trata de una campaña de marketing programada o de una campaña activada por una API.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Campaña programada | Envíos por lotes únicos o recurrentes a una audiencia definida | Audiencia evaluada en el momento de la ejecución; establecer fecha/hora o periodicidad |
| Campaña activada por API | Envíos impulsados por eventos o activados por el sistema a perfiles especificados | Perfiles especificados en la carga útil de déclencheur; admite hasta 20 destinatarios por solicitud |

#### Dónde divergen las opciones

**Para La Opción A (Toma De Decisiones Por Correo Electrónico):**

1. Crear el mensaje de correo electrónico con el Designer de correo electrónico
   - IU: Campañas > Crear campaña > Seleccionar correo electrónico > Editar contenido
   - Inserte un componente de decisión de oferta en el diseño de correo electrónico para definir la zona de colocación
   - Añadir tokens de personalización para el contenido de nivel de perfil (nombre, nivel de lealtad)
   - Configuración de la línea de asunto y el preencabezado con personalización opcional
2. Creación y configuración de la campaña
   - IU: Campañas > Crear campaña > Programado o activado por API
   - Enlace la audiencia de destinatario y seleccione la superficie de canal
   - Establecer la programación de ejecución o la configuración del déclencheur de API
   - Revisión y activación de la campaña

**Para Opción B (Web/Aplicación En Tiempo Real):**

1. Configurar la experiencia basada en código o el canal web
   - IU: Campañas > Crear campaña > Experiencia basada en código (o web)
   - Vinculación de la política de decisión a la superficie de experiencia
   - Defina el formato de renderización (respuesta JSON para código basado; editor visual para canal web)
2. Implementar el procesamiento del lado del cliente
   - Usar la respuesta de Web SDK `sendEvent` para recuperar la oferta seleccionada
   - Procesar el contenido de la oferta en la ubicación designada en la página
   - Implementación del rastreo de clics y impresiones

**Para Opción C (Nodo De Decisión De Recorrido):**

1. Diseño del recorrido con un nodo de decisión
   - IU: Recorrido > Crear Recorrido > Agregar nodo de decisión
   - Configure el nodo de decisión para invocar la directiva de decisión desde la fase 3
2. Añadir nodos de acción de mensaje después de la decisión
   - Configurar acciones de correo electrónico, push o SMS que hagan referencia a la oferta seleccionada
   - Agregar pasos de espera, condiciones o ramas en función de la participación en la oferta
3. Publicación del recorrido

#### Documentación de Experience League

- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introducción a recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Fase 6: Prueba y validación

**Función de la aplicación:** AJO: Decisioning, AJO: Message Authoring

Esta fase valida que el motor de decisión devuelve las ofertas correctas para los perfiles de prueba y que el contenido de la oferta se procesa correctamente en cada canal de entrega.

#### Lógica de toma de decisiones de prueba

Utilice perfiles de prueba con atributos conocidos para comprobar que se han seleccionado las ofertas correctas en función de la idoneidad y la clasificación.

- Cree perfiles de prueba que coincidan con diferentes criterios de idoneidad (por ejemplo, nivel Gold, nivel Silver, usuario de prueba)
- Verifique que cada perfil de prueba reciba la oferta esperada
- Compruebe que los perfiles que no coinciden con ninguna regla de idoneidad reciben la oferta de reserva

#### Prueba de representación de contenido

Previsualice el contenido de la oferta en cada canal de entrega.

- Para la opción A: utilice la previsualización de correo electrónico con perfiles de prueba para verificar que el contenido de la oferta se procese correctamente
- Para la opción B: Probar la respuesta de Edge Decisioning en un entorno de ensayo
- Para la opción C: utilice el modo de prueba recorrido para comprobar que el nodo de decisión se selecciona correctamente

#### Validar el seguimiento de impresiones

Confirme que se está realizando un seguimiento de las impresiones, los clics y las conversiones de la oferta.

- Verificar que los eventos de interacción de ofertas aparezcan en los conjuntos de datos de seguimiento
- Confirmar atribución entre impresiones de oferta y conversiones descendentes

#### Documentación de Experience League

- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Envío de pruebas de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/proofs)

### Fase 7: Configurar la creación de informes y la monitorización del rendimiento

**Función de aplicación:** AJO: Informes y análisis de rendimiento

Esta fase configura los informes para rastrear la distribución de selección de ofertas, las tasas de aceptación, el impacto de conversión y las tasas de reserva. Esta fase abarca tanto los informes nativos de AJO como el análisis entre canales basado en CJA.

#### Decisión: método de creación de informes

Determine qué herramientas de creación de informes se necesitan para el análisis del rendimiento de las ofertas.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo informes nativos de AJO | Supervisión operativa de campañas o recorridos individuales | Acceso rápido; métricas de entrega y participación integradas; análisis limitado entre entidades |
| Análisis de CJA Workspace | Eficacia de ofertas en canales múltiples, atribución de ingresos, análisis de funnel | Requiere conexión y vista de datos de CJA; funciones analíticas más profundas |
| Tanto AJO como CJA | Cobertura operacional y analítica completa | Recomendado para implementaciones de producción; AJO para monitorización en tiempo real, CJA para análisis estratégicos |

#### Detalles de configuración clave

1. **Creación de informes nativos de AJO**: supervise el rendimiento de la campaña o del recorrido mediante informes integrados.
   - IU: Campañas > Seleccionar campaña > Informe de todos los tiempos (o Informe en vivo)
   - Revise las métricas específicas de la oferta: impresiones por oferta, tasa de pulsaciones por oferta, tasa de reserva
   - Monitorización de la entrega funnel: Objetivos > Enviado > Entregado > Aperturas > Clics

2. **Análisis de CJA (recomendado)**: genere paneles de rendimiento de ofertas en canales múltiples.
   - Configuración de una conexión CJA que incluya conjuntos de datos de interacción de ofertas AJO
   - Cree una vista de datos con dimensiones específicas de la oferta (nombre de la oferta, ubicación, decisión) y métricas (impresiones, clics, conversiones)
   - Cree un análisis del espacio de trabajo para: distribución de la selección de ofertas, tasa de aceptación por segmento, impacto en los ingresos, coherencia de la oferta en canales múltiples

#### Documentación de Experience League

- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/home)

## Consideraciones sobre la implementación

Esta sección cubre las barreras, los escollos comunes, las prácticas recomendadas y las decisiones de compensación para las implementaciones de Offer Decisioning.

### Protecciones y límites

Tenga en cuenta las siguientes limitaciones y protecciones de la plataforma al planificar la implementación.

- Máximo de 10 000 ofertas personalizadas aprobadas por espacio aislado: [protecciones de administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 30 colocaciones por decisión
- Máximo de 30 ámbitos de recopilación por solicitud de decisión
- Los modelos de clasificación de IA requieren un mínimo de 1000 eventos de conversión para la formación.
- Los contadores de límite de oferta pueden tener un retraso de hasta unos segundos en escenarios de alto rendimiento
- Las decisiones de Edge se limitan a atributos de perfil disponibles en el almacén de perfiles Edge
- Máximo de 4000 definiciones de segmento por zona protegida — [Protecciones de plataforma](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- Solo puede haber una política de combinación activa en Edge por zona protegida
- Máximo de 500 campañas activas por zona protegida
- Límite de tasa de entrada de recorrido: 5000 perfiles por segundo
- Máximo de 10 superficies de canal por tipo de canal y zona protegida

### Peligros comunes

Evite estos problemas que se producen con frecuencia durante la implementación.

- **La decisión siempre devuelve la oferta de reserva:** Esto generalmente significa que las ofertas personalizadas no están aprobadas, están fuera de su intervalo de fechas de validez o las reglas de elegibilidad no coinciden con los atributos del perfil de prueba. Compruebe cada condición: estado de aprobación, intervalo de fechas y precisión de expresión de regla de segmento. Compruebe también que no se han alcanzado los límites.
- **La oferta no aparece en la colección:** Asegúrese de que la oferta se haya etiquetado con el calificador de colección correcto y de que el filtro de colección coincida. Las ofertas deben estar etiquetadas y aprobadas para aparecer en ámbitos de decisión basados en colecciones.
- **Fórmula de clasificación no aplicada:** Compruebe que la fórmula es sintácticamente válida y hace referencia a atributos de perfil accesibles. Los errores de fórmula vuelven silenciosamente a la clasificación basada en prioridades sin ningún error visible.
- **La entrega de Edge devuelve la personalización vacía:** Asegúrese de que la secuencia de datos esté configurada con el servicio [!DNL Adobe Journey Optimizer] habilitado y de que el ámbito de decisión tenga el formato correcto. Compruebe que existe la política de combinación activa para extremos.
- **Ofertas incoherentes en todos los canales:** Si se usan directivas de decisión independientes por canal, el mismo perfil puede recibir ofertas diferentes. Utilice una única política de decisión en todos los canales para mantener la coherencia o acepte divergencias intencionadas basadas en ubicaciones específicas del canal.
- **El contenido de la oferta no se representa en el correo electrónico:** Compruebe que la oferta tenga una representación de contenido que coincida con el formato de ubicación del correo electrónico (HTML o URL de imagen). La falta de representaciones da como resultado zonas de colocación en blanco.

### Prácticas recomendadas

Siga estas recomendaciones para una implementación correcta de Offer Decisioning.

- **Comience con un pequeño catálogo de ofertas e itere**: Empiece con 5-10 ofertas y amplíe a medida que se valida el marco de toma de decisiones. Esto simplifica la resolución de problemas y garantiza que las reglas de idoneidad funcionen correctamente antes de escalarlas.
- **Use calificadores de colección de forma estratégica**: Etiquete ofertas por categoría (por ejemplo, &quot;Adquisición&quot;, &quot;Retención&quot;, &quot;Ampliación de venta&quot;) para habilitar ámbitos de decisión flexibles basados en colecciones que se puedan reutilizar en campañas y recorridos.
- **Cree siempre ofertas de reserva significativas**: las ofertas de reserva no son solo una red de seguridad; son la experiencia predeterminada para perfiles que no coinciden con ninguna regla de elegibilidad. Invierta en contenido de reserva que proporcione valor incluso sin personalización.
- **Diseñe reglas de elegibilidad para que sean mutuamente excluyentes siempre que sea posible** — Cuando varias ofertas tienen elegibilidad superpuesta, la estrategia de clasificación se vuelve crítica. Si los requisitos comerciales dictan una oferta específica para un segmento específico, las reglas de elegibilidad se excluyen mutuamente en lugar de depender únicamente de la clasificación.
- **Prueba con perfiles representativos de Edge para la opción B**: los perfiles de Edge contienen un subconjunto de atributos de perfil de hub. Haga pruebas con perfiles que tengan atributos disponibles del perímetro para garantizar que la idoneidad se evalúe correctamente en la producción.
- **Monitorizar tasas de reserva como métrica de estado**: una tasa de reserva alta (por encima del 20-30%) indica que el catálogo de ofertas no cubre suficientes segmentos de clientes. Expanda el catálogo de ofertas o amplíe las reglas de idoneidad.
- **Directivas de decisión de versión en lugar de editar las activas**: cree una nueva versión de directiva de decisión en lugar de modificar una activa. Esto evita interrupciones en las campañas en directo y permite la comparación A/B de las estrategias de decisión.

### Decisiones de compensación

Tenga en cuenta las siguientes compensaciones cuando tome decisiones sobre arquitectura y configuración.

#### Precisión de elegibilidad frente a cobertura de ofertas

Las reglas de elegibilidad estrictas garantizan que cada oferta alcance solo los perfiles más relevantes, pero puede dar como resultado altas tasas de reserva cuando los perfiles no coinciden con ninguna oferta. Las reglas de aceptación generales maximizan la cobertura de la oferta pero reducen la precisión de la personalización.

- **Favoritos de elegibilidad ajustados:** mayores tasas de aceptación, mejor personalización, menor fatiga de ofertas
- **Favoritos de elegibilidad generales:** Tasas de reserva más bajas, más perfiles reciben ofertas personalizadas y administración de reglas más sencilla
- **Recomendación:** Comience con reglas de elegibilidad más amplias y apriételas en función de los datos de rendimiento. Monitorice las tasas de reserva y las tasas de aceptación para encontrar el equilibrio adecuado. Utilice estrategias de clasificación para diferenciar entre ofertas ampliamente aptas.

#### Clasificación basada en prioridades y clasificación por IA

La clasificación basada en prioridades proporciona al negocio control total sobre las ofertas mostradas, mientras que la clasificación basada en IA optimiza la conversión, pero reduce el control humano sobre la selección de ofertas.

- **Favoritos basados en prioridades:** Control empresarial, predictibilidad, sin requisito de datos de capacitación, implementación inmediata
- **Favoritos de clasificación de IA:** Optimización de conversión, descubrimiento de patrones inesperados, adaptación automática a un comportamiento cambiante del cliente
- **Recomendación:** Use la clasificación basada en prioridades para los lanzamientos iniciales y las ofertas confidenciales según la normativa, donde el control empresarial es primordial. La transición a IA se clasifica para casos de uso de alto volumen y optimizado para el rendimiento una vez que haya disponibles suficientes datos de conversión (más de 1000 eventos).

#### Política de decisión única frente a políticas de decisión por canal

Una única política de decisión garantiza la coherencia de la oferta en todos los canales, pero restringe la optimización por canal. Las políticas por canal permiten la clasificación y la idoneidad específicas del canal, pero arriesgan experiencias de cliente incoherentes.

- **Favoritos de directiva única:** coherencia en canales múltiples, administración más sencilla, informes unificados
- **Las políticas por canal favorecen:** Clasificación optimizada para el canal, idoneidad específica para el canal (por ejemplo, ofertas solo para la web), iteración independiente
- **Recomendación:** Comience con una directiva de decisión única para la coherencia entre canales. Cree directivas por canal únicamente cuando los requisitos empresariales exijan estrategias de oferta específicas del canal (por ejemplo, ventas flash exclusivas de la web).

#### Toma de decisiones en Hub (Opción A/C) vs. toma de decisiones en Edge (Opción B)

Hub Decisioning tiene acceso al perfil completo, pero funciona en el momento de la entrega. Edge Decisioning funciona en tiempo real con latencia de subsegundos, pero se limita a atributos de perfil disponibles para Edge.

- **Favoritos de Hub Decisioning:** Acceso a datos de perfil completos, reglas de elegibilidad complejas, volúmenes de campañas por lotes
- **Favoritos en la toma de decisiones de Edge:** Contexto en tiempo real, personalización durante la sesión, respuesta en segundos
- **Recomendación:** Utilice la toma de decisiones de concentrador para canales salientes (correo electrónico, push) donde los datos de perfil completos mejoran la relevancia de la oferta. Utilice Edge Decisioning para canales entrantes (web, aplicación) donde la respuesta en tiempo real es crítica. Asegúrese de que las reglas de idoneidad para el uso de Edge solo utilicen atributos disponibles en Edge.

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre los componentes utilizados en este patrón de caso de uso.

### Gestión de decisiones

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear calificadores de colección](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Entrega de ofertas

- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Entrega de ofertas mediante la API de Edge Decisioning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Entrega de ofertas mediante la API de decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/decisioning-api)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configuración de superficie de correo electrónico](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegar subdominios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Configuración del canal de notificaciones push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Configuración del canal SMS](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### Creación y personalización de mensajes

- [Diseño del contenido del correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Previsualización y prueba del contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Campañas y recorridos

- [Introducción a las campañas](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introducción a recorrido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/journey)

### Experimentación de contenido

- [Introducción al experimento de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### Audiencias y segmentación

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)

### Perfil e identidad

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview)
- [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview)
- [Información general sobre Customer AI](https://experienceleague.adobe.com/es/docs/experience-platform/intelligent-services/customer-ai/overview)

### Modelado y recopilación de datos

- [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home)
- [Información general de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure)

### Informes y análisis

- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Informe global de recorrido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Información general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/home)

### Gobernanza de datos y ciclo vital

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Información general sobre Advanced Data Lifecycle Management](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/home)
- [Consentimiento en Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Guardas

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)

### Tutoriales

- [Introducción a la API de Gestión de decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/getting-started)
