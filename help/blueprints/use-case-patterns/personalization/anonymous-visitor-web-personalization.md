---
title: Personalization web de visitante anónimo
description: Aprenda a ofrecer contenido web personalizado a visitantes no identificados en función de las señales de comportamiento durante la sesión.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '8076'
ht-degree: 1%

---


# Personalización web de visitante anónimo

Este plan de referencia proporciona directrices de implementación para ofrecer contenido web personalizado a visitantes anónimos (no identificados) en función de las señales de comportamiento durante la sesión. Abarca el ciclo de vida completo de la implementación, desde la configuración de [!DNL Web SDK] y la definición de la audiencia perimetral hasta la entrega de contenido y los informes de rendimiento, y está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que trabajan con [!DNL Adobe Journey Optimizer] (AJO), [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP) y [!DNL Adobe Experience Platform] (AEP).

Utilice este plan para comprender la arquitectura, evaluar las opciones de implementación, tomar decisiones de configuración informadas y localizar la documentación de Experience League relevante para cada fase de implementación.

El patrón funciona con datos limitados, solo lo que se puede observar en la sesión actual y cualquier perfil de Edge anónimo acumulado de visitas anteriores con el mismo dispositivo o cookie. Esto lo convierte en una herramienta adecuada para la personalización de la parte superior de funnel, en la que el visitante no tiene cuenta o no se ha autenticado.

## Resumen del caso de uso

La Personalization web de visitantes anónimos aborda la necesidad empresarial de ofrecer contenido relevante y personalizado a los visitantes del sitio web que aún no se han identificado: no han iniciado sesión, no tienen identidad conocida y no se pueden resolver en un perfil unificado de cliente. A pesar de esta limitación, se puede lograr una personalización significativa mediante señales de comportamiento en la sesión: páginas vistas, tiempo en el sitio, profundidad de desplazamiento, fuente de referencia, ubicación geográfica, tipo de dispositivo y parámetros de campaña de UTM.

Este patrón utiliza las superficies de canal web de AJO y las experiencias basadas en código para modificar el contenido de la página en tiempo real. La segmentación de Edge es el método de evaluación principal, ya que las decisiones deben tomarse con latencia de subsegundos a medida que el visitante navega por el sitio. [!DNL Web SDK] recopila señales de comportamiento y las envía a [!DNL AEP Edge Network], donde las reglas de audiencia evaluadas por el perímetro determinan qué variante de contenido se va a enviar.

A diferencia de la personalización de aplicaciones/web de visitantes conocidos, que aprovecha el perfil unificado completo y la pertenencia a segmentos, este patrón se limita a los datos observables en la sesión actual y a cualquier perfil Edge anónimo asociado al ECID del visitante ([!DNL Experience Cloud ID]). Esta distinción es crítica para la planificación de la implementación: las señales de comportamiento disponibles para la personalización se limitan a lo que captura [!DNL Web SDK] y a lo que persiste en el almacén de perfiles de Edge entre sesiones a través del ECID basado en cookies.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

**[Aumentar la participación en el sitio web](../../business-objectives/acquisition-growth/increase-website-engagement.md)**

Mejore el tiempo en el sitio, las páginas por sesión y la interacción con el contenido web mediante experiencias relevantes adaptadas a las señales de visitantes anónimos.

| KPI |
| --- |
| Página de tiempo de activación (web) |
| Participación |
| Tasas de conversión |

**[Ofrecer experiencias personalizadas a los clientes](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

Adapte el contenido, las ofertas y los mensajes a las preferencias, los comportamientos y las fases del ciclo vital individuales, incluso para los visitantes que aún no se han identificado.

| KPI |
| --- |
| Participación |
| Tasas de conversión |
| Satisfacción del cliente (CSAT) |

**[Aumentar las tasas de conversión](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

Mejore el porcentaje de visitantes y clientes potenciales que completan las acciones deseadas, como compras, suscripciones o envíos de formularios, presentando el contenido más relevante en función del contexto de comportamiento.

| KPI |
| --- |
| Tasas de conversión |
| Conversión de cliente potencial |
| Coste por posible cliente |

## Casos de uso tácticos de ejemplo

Los siguientes ejemplos ilustran escenarios específicos en los que se puede aplicar este patrón.

- **Prueba A/B de titular de página de aterrizaje basada en la fuente de referencia**: pruebe diferentes titulares para visitantes que llegan desde Google, medios sociales o tráfico directo para optimizar la participación por canal de adquisición
- **Recomendaciones de afinidad de la categoría basadas en el comportamiento del explorador** — Muestra recomendaciones de productos o contenido basadas en páginas vistas en la sesión actual para aumentar el descubrimiento y la conversión
- **Oferta de intención de salida para visitantes que están a punto de irse**: presenta una oferta promocional o un formulario de captura de posibles clientes cuando las señales de comportamiento indican que el visitante está a punto de abandonar el sitio
- **Banner promocional con destino geográfico**: muestra promociones específicas de la ubicación, contenido de localizadores de tiendas u ofertas regionales basadas en la ubicación geográfica del visitante
- **Optimización del diseño de contenido específico del dispositivo**: adapte el diseño del contenido, los tamaños de las imágenes y la ubicación de CTA en función de si el visitante está en un equipo de escritorio, una tableta o un dispositivo móvil
- **Mensajes de bienvenida de visitantes nuevos y recurrentes**: diferencie la experiencia de los visitantes nuevos de la de los anónimos que regresan mediante la persistencia de ECID en todas las sesiones
- **Recomendaciones de contenido basadas en páginas vistas en la sesión actual**: muestra de forma dinámica artículos, productos o recursos relacionados basados en las páginas que el visitante ya ha visto
- **Banner a pantalla completa dinámico basado en parámetros de campaña de UTM** — Personalice el banner a pantalla completa para que coincida con los mensajes o el elemento creativo de la campaña de referencia

## Indicadores clave de rendimiento

Utilice los siguientes KPI para medir la eficacia de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de impresiones de Personalization | Porcentaje de vistas de página aptas en las que se entregó contenido personalizado | informe AJO campaign: impresiones / vistas totales de página |
| Tasa de clics (CTR) | Porcentaje de impresiones de contenido personalizadas que resultan en un clic | informe AJO campaign: clics/impresiones |
| Alza de participación | Aumento del tiempo en la página, las páginas por sesión o la profundidad de desplazamiento para el contenido personalizado frente al predeterminado | Comparación de CJA Workspace: cohorte personalizada frente a control |
| Tasa de conversión | Porcentaje de visitantes expuestos a contenido personalizado que completan una acción deseada | análisis de CJA funnel: impresión > interacción > conversión |
| Reducción de tasa de devolución | Disminución en las sesiones de una sola página para los visitantes que reciben contenido personalizado | análisis de sesión de CJA: delta de tasa de devolución para personalizado frente a predeterminado |
| Tasa de victorias del experimento | Porcentaje de pruebas A/B que producen un ganador estadísticamente significativo | Informe de experimento de AJO: experimentos que alcanzan el umbral de confianza |

## Patrón de caso de uso

A continuación se describe el patrón principal y la cadena de funciones para este caso de uso.

**Personalization web de visitante anónimo**

Ofrezca contenido personalizado basado en señales de comportamiento en la sesión para visitantes no identificados a través del canal web de AJO.

**Cadena de funciones:** Configuración de superficie web > Evaluación de regla de comportamiento > Entrega de contenido > Seguimiento de impresión > Informes

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Adobe Journey Optimizer] (AJO)**: configuración de superficie de canal web, creación de contenido (experiencias web y basadas en código), ejecución de campañas, experimentación de contenido (pruebas A/B), toma de decisiones (selección dinámica de contenido) y sistema de informes.
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Segmentación de Edge para la evaluación de audiencias en tiempo real basada en señales de comportamiento en la sesión; administración anónima de perfiles de Edge
- **[!DNL Adobe Experience Platform] (AEP)** — [!DNL Web SDK] para la recopilación de señales de comportamiento, [!DNL Edge Network] para el enrutamiento de datos en tiempo real y la entrega de personalización, configuración de secuencia de datos

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Se asume en contexto | Zona protegida de AJO con permisos de canal web configurados. [!DNL Web SDK] permisos de implementación y acceso al flujo de datos concedido al equipo de implementación. Los usuarios aprovisionados con funciones que permiten la configuración del canal web, la administración de audiencias y la ejecución de campañas. | [Resumen de control de acceso](https://experienceleague.adobe.com/es/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | Esquema de Experience Event que captura señales de comportamiento web (vistas de página, clics, profundidad de desplazamiento, datos de referencia, parámetros de UTM). El esquema debe incluir grupos de campos de interacción web estándar y estar habilitado para que el perfil de Edge admita la evaluación en tiempo real. Se debe crear un conjunto de datos correspondiente y habilitar para el perfil. | [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home) |
| Fuentes de datos y recopilación | Requerido | [!DNL Web SDK] debe implementarse en todas las propiedades web de destino con una secuencia de datos configurada para enrutar datos a [!DNL AEP Edge Network]. La secuencia de datos debe tener los servicios [!DNL Adobe Experience Platform] y [!DNL Adobe Journey Optimizer] habilitados. Esta es una dependencia esencial — sin [!DNL Web SDK], no es posible la recopilación de señales de comportamiento ni la entrega de experiencias. | [Información general del SDK web](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home) |
| Configuración de identidad y perfil | Requerido | ECID ([!DNL Experience Cloud ID]) configurado como el área de nombres de identidad principal para visitantes anónimos. La política de combinación de Edge debe configurarse con `isActiveOnEdge: true` para resolver los datos de perfil anónimos en el perímetro de. Solo puede haber una política de combinación activa en Edge por zona protegida. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home) |
| Definición de audiencia y segmentación | Requerido | Los segmentos de audiencia evaluados por Edge se definen en función de las señales de comportamiento durante la sesión. La segmentación de Edge es obligatoria para la latencia de evaluación de subsegundos. Las reglas de segmentos solo deben utilizar expresiones de reglas de segmentos aptas para Edge (comprobaciones de atributos simples y pertenencia a segmentos, sin consultas de series temporales ni agregaciones complejas). | [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | No aplicable | Valor limitado para visitantes anónimos, ya que la suma de los datos de perfil históricos es mínima. Puede ser aplicable si el perfil de Edge acumula datos de comportamiento significativos de visitas anónimas anteriores en varias sesiones. | [Resumen de atributos calculados](https://experienceleague.adobe.com/es/docs/experience-platform/profile/computed-attributes/overview) |
| Administración del ciclo de datos | Recomendado | La caducidad del perfil seudónimo debe configurarse para perfiles Edge anónimos a fin de administrar el almacenamiento y cumplir con los requisitos de privacidad. Los perfiles solo de ECID se pueden configurar para que caduquen entre 14 y 365 días. Las políticas de consentimiento de cookies deben aplicarse para la recopilación de datos de comportamiento. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/home) |
| Etiquetado y aplicación del uso de datos | Recomendado | Las etiquetas de gobernanza en los datos de comportamiento garantizan el cumplimiento, especialmente para la segmentación geográfica (etiqueta geográfica sensible a S2) y la personalización basada en dispositivos. Las etiquetas impiden que los datos de comportamiento restringidos se utilicen en contextos de personalización no autorizados. | [Resumen de control de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home) |
| Monitorización y observabilidad | Recomendado | La supervisión del flujo de datos de [!DNL Edge Network] y [!DNL Web SDK] ayuda a detectar problemas de entrega de personalización. Configure alertas para errores de flujo de datos, errores de ingesta y anomalías de entrega de Edge. Esencial para implementaciones de producción en las que los errores de personalización degradan la experiencia del visitante. | [Resumen de Observability Insights](https://experienceleague.adobe.com/es/docs/experience-platform/observability/home) |
| Informes y análisis | Incluido | La creación de informes de rendimiento de Personalization forma parte de la cadena de funciones (Fase 5). El análisis de CJA de la efectividad de la personalización de visitantes anónimos permite realizar análisis de funnel profundos, comparaciones de cohortes y mediciones de impacto de conversión más allá de lo que ofrecen los informes nativos de AJO. | [Información general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del Catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Journey Optimizer] (AJO)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Configuración de canal | Fase 1: Configuración de la superficie web | Configure las superficies de canal web que definen dónde se enviará el contenido personalizado en las propiedades web de destino |
| Creación de mensajes | Fase 3: Creación de contenido y creación de variantes | Cree variantes de contenido personalizadas para superficies web mediante el diseñador web, el editor de experiencias basado en código o las plantillas de contenido |
| Ejecución de campaña | Fase 4: Configuración de campaña y envío | Cree y active campañas web que enlacen audiencias, contenido y configuración de envío |
| Decisioning | Fase 3: Creación de contenido y creación de variantes (Opción C) | Configure políticas de decisión, reglas de elegibilidad y estrategias de clasificación para la selección de contenido dinámico en función de señales de comportamiento |
| Experimentación de contenido | Fase 3: Creación de contenido y creación de variantes (Opción B) | Configure experimentos de contenido A/B y multivariable con asignación de tráfico, métricas de éxito y umbrales de confianza |
| Informes y análisis de rendimiento | Fase 5: Informes y análisis de rendimiento | Monitorización de métricas de envío de personalización, eficacia de variante, resultados de experimentos e impacto de conversión |

### [!DNL Real-Time CDP] (RT-CDP)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Evaluación de audiencia | Fase 2: Definición de audiencia de comportamiento | Defina y evalúe segmentos de audiencia basados en Edge mediante señales de comportamiento en la sesión para una segmentación de personalización en tiempo real |

## Prerrequisitos

Complete lo siguiente antes de comenzar la implementación.

- [ ] [!DNL Web SDK] se ha implementado en todas las propiedades web de destino con `sendEvent` llamadas que capturan vistas de página, clics e interacciones de comportamiento relevantes
- [ La secuencia de datos ] está configurada en la interfaz de usuario de recopilación de datos con los servicios [!DNL Adobe Experience Platform] y [!DNL Adobe Journey Optimizer] habilitados
- [ El esquema de evento de experiencia ] existe con grupos de campos de interacción web (vistas de página, datos de referencia, parámetros de UTM y contexto de dispositivo) y está habilitado para el perfil
- [ El área de nombres de identidad ECID ] está configurado y designado como identidad principal en el esquema de evento de comportamiento web
- [ ] La política de combinación de Edge se ha configurado con `isActiveOnEdge: true` en la zona protegida de destino
- [ El canal web AJO ] está aprovisionado y se puede acceder a él desde la zona protegida de destino
- [ ] variantes de contenido (copia, imágenes, CTA) están diseñadas y aprobadas para cada caso de uso de personalización
- [ Se han definido ] métricas de éxito (lo que constituye un evento de conversión o participación para la medición)
- [ ] El mecanismo de consentimiento de cookies se ha implementado en el sitio web para cumplir con las normas de privacidad antes de recopilar datos de comportamiento

## Opciones de implementación

En esta sección se describen tres métodos de implementación. Seleccione la opción que mejor se ajuste a sus necesidades de personalización.

### Opción A: personalización web basada en reglas

**Ideal para:** Personalización simple y determinística: titulares con objetivo geográfico, titulares con fuentes de referencia específicas, diseños específicos del dispositivo, mensajes nuevos de visitantes que regresan. Elija esta opción cuando la variante de contenido se pueda determinar mediante una lógica condicional directa (si la condición X, mostrar contenido Y).

**Cómo funciona:**

La personalización basada en reglas utiliza segmentos de audiencia evaluados por Edge para determinar qué variante de contenido ve un visitante. Cada segmento de audiencia se asigna a una variante de contenido específica mediante reglas condicionales definidas en la campaña. Cuando un visitante carga una página, [!DNL Web SDK] envía señales de comportamiento a [!DNL Edge Network], que evalúa el perfil de Edge del visitante frente a las reglas de audiencia definidas en milisegundos. La variante de contenido coincidente se devuelve en la respuesta [!DNL Edge Network] y se representa en la página.

Este método requiere la definición de segmentos de audiencia distintos en RT-CDP (por ejemplo, &quot;visitantes de la búsqueda de Google&quot;, &quot;visitantes en California&quot;, &quot;visitantes de dispositivos móviles&quot;) y la creación de las variantes de contenido correspondientes en AJO. La campaña vincula cada audiencia a su variante de contenido mediante reglas de contenido condicional o campañas independientes por segmento. No hay que clasificar la IA ni dividir el tráfico: la relación entre audiencia y contenido es determinista.

**Consideraciones clave:**

- Requiere criterios de audiencia bien definidos que se puedan expresar como expresiones de reglas de segmentos aptas para Edge
- Las variantes de contenido deben ser creadas previamente para cada segmento de audiencia
- Para añadir nuevas reglas de personalización es necesario crear nuevos segmentos de audiencia y variantes de contenido
- No proporciona una medición estadística de la eficacia de las variantes de contenido

**Ventajas:**

- La implementación y la comprensión más sencillas: relación causa-efecto clara entre audiencia y contenido
- No se requiere sobrecarga de experimentación ni división de tráfico
- El comportamiento determinista hace que las pruebas y el control de calidad sean directos
- Baja latencia, ya que la evaluación de Edge solo se basa en reglas
- Funciona bien cuando la empresa ya sabe qué contenido funciona mejor para cada segmento

**Limitaciones:**

- No hay ningún mecanismo integrado para medir si la personalización mejora los resultados en comparación con el contenido predeterminado
- Requiere una toma de decisiones manual sobre qué contenido mostrar cada segmento
- No se adapta ni optimiza con el tiempo: reglas estáticas hasta que se cambian manualmente
- La ampliación a muchos segmentos y variantes aumenta la complejidad de la configuración

**Experience League:**

- [Introducción al canal web](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/web/get-started-web)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)

### Opción B: personalización web basada en experimentos

**Ideal para:** Pruebas A/B y multivariable: probar variantes de titulares, colores de botones de CTA, alternativas de diseño, ofertas promocionales, con medición de relevancia estadística. Elija esta opción cuando necesite validar qué variante de contenido funciona mejor antes de comprometerse con una regla de personalización permanente.

**Cómo funciona:**

La personalización basada en experimentos utiliza la experimentación de contenido de AJO para asignar de forma aleatoria visitantes a grupos de tratamiento de contenido y medir qué variante ofrece el mejor rendimiento con respecto a una métrica de éxito definida. El tráfico se divide entre variantes (por ejemplo, 50/50 para A/B, 33/33/34 para A/B/C) y el rendimiento se rastrea hasta que se alcanza la relevancia estadística.

El experimento está incrustado en una campaña web de AJO. Cuando un visitante carga una página, [!DNL Edge Network] la asigna a un grupo de tratamiento en función de la asignación de tráfico configurada. El visitante ve de forma consistente el mismo tratamiento durante el experimento (persistencia a nivel de sesión o de visitante según la configuración). Las métricas de éxito (clics, conversiones y eventos de participación) se rastrean a través de [!DNL Web SDK] y se incluyen en el informe de experimento de AJO.

Esta opción no requiere segmentos de audiencia predefinidos para la segmentación: todos los visitantes (o un subconjunto segmentado) participan en el experimento. El objetivo es descubrir qué contenido tiene el mejor rendimiento, no segmentar segmentos conocidos con contenido predeterminado.

**Consideraciones clave:**

- Requiere un volumen de tráfico suficiente para alcanzar la relevancia estadística en un plazo razonable
- Los experimentos utilizan un modelo estadístico bayesiano con intervalos de confianza válidos en cualquier momento
- Se recomienda un grupo de exclusión (no recibe contenido personalizado) para medir el alza incremental
- Solo puede haber un experimento activo por campaña a la vez
- Las modificaciones del experimento requieren detener y reiniciar la campaña

**Ventajas:**

- Proporciona una medición estadísticamente rigurosa de la efectividad de variantes de contenido
- Elimina las conjeturas de las decisiones de personalización: selección de contenido basada en datos
- Admite grupos de exclusión para la medición de alza incremental real
- Creación de informes de experimentos integrados con intervalos de confianza y declaración de ganador
- Los resultados pueden informar la futura personalización basada en reglas (Opción A) al identificar las variantes ganadoras

**Limitaciones:**

- Requiere un volumen de tráfico significativo: las páginas de poco tráfico pueden tardar semanas en alcanzar la relevancia
- La división del tráfico significa que algunos visitantes ven contenido subóptimo durante el período de prueba
- No se puede personalizar por segmento durante el experimento (todos los visitantes o un subconjunto participan por igual)
- Máximo de 10 variantes de tratamiento por experimento
- Sin optimización continua: los experimentos son discretos con un inicio y un final

**Experience League:**

- [Introducción al experimento de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### Opción C: personalización web basada en decisiones

**Mejor opción para:** Selección dinámica de contenido: recomendaciones de afinidad de categoría, ofertas de intención de salida, recomendaciones de comportamiento; una directiva de decisión evalúa las señales de sesión y selecciona el contenido óptimo de un catálogo de elementos aptos. Elija esta opción cuando la lógica de selección de contenido sea demasiado compleja para reglas simples, cuando desee una optimización de clasificación de IA o cuando el conjunto de elementos de contenido aptos sea grande y dinámico.

**Cómo funciona:**

La personalización basada en decisiones utiliza AJO Decisioning para evaluar las señales de comportamiento y seleccionar la mejor variante de contenido para cada visitante de un catálogo administrado de elementos de contenido (ofertas). Cada elemento de contenido tiene reglas de idoneidad (quién califica), representaciones (cómo se ve el contenido en cada ubicación) y restricciones de límite opcionales (con qué frecuencia se puede mostrar). Una directiva de decisión vincula las ubicaciones (donde el contenido aparece en la página) a colecciones de elementos de contenido y aplica una estrategia de clasificación para seleccionar la mejor opción.

Cuando un visitante carga una página, [!DNL Web SDK] envía una solicitud [!DNL Edge Network] que incluye el ámbito de decisión. El motor de decisión evalúa el perfil de Edge del visitante frente a las reglas de idoneidad para el elemento de contenido, aplica la estrategia de clasificación (basada en prioridad, en fórmulas o en clasificación de IA) y devuelve el elemento de contenido ganador. Esto sucede en el extremo con latencia de subsegundos.

La estrategia de clasificación determina cómo se ordenan los elementos de contenido aptos. La clasificación basada en prioridades utiliza los valores de prioridad asignados manualmente. La clasificación basada en fórmulas utiliza una expresión personalizada (por ejemplo, ponderar la actualización de las vistas de página). La clasificación clasificada por IA utiliza un modelo de aprendizaje automático que se optimiza para la métrica de éxito seleccionada a lo largo del tiempo, pero requiere un mínimo de 1000 eventos de conversión para la formación.

**Consideraciones clave:**

- Requiere la configuración de los componentes de Decisioning: ubicaciones, reglas de idoneidad, elementos de contenido, elementos de reserva, colecciones y políticas de decisión
- Las estrategias clasificadas por IA requieren un volumen de conversión suficiente (más de 1000 eventos) para entrenar el modelo
- Las decisiones de Edge se limitan a atributos de perfil disponibles en el almacén de perfiles Edge
- Los elementos de contenido deben administrarse y mantenerse en la biblioteca de decisiones
- Se debe definir contenido de reserva para los casos en que no se cumpla ningún elemento personalizado

**Ventajas:**

- Se adapta a catálogos de contenido grandes sin requerir una asignación individual de audiencia a contenido
- Las estrategias de clasificación de IA optimizan continuamente la selección de contenido en función del rendimiento observado
- Las reglas de elegibilidad y las restricciones de límite proporcionan un control preciso sobre la entrega de contenido
- Admite una lógica empresarial compleja que sería difícil expresar como segmentos de audiencia
- Reutilizable en todos los canales: la misma política de decisión puede potenciar la personalización web, del correo electrónico y móvil

**Limitaciones:**

- Mayor complejidad de la implementación: requiere la configuración de la pila completa de componentes de Decisioning.
- La clasificación de IA requiere un volumen de conversión y un tiempo significativos para que la formación sea eficaz
- Las limitaciones de datos de perfil de Edge limitan la complejidad de las reglas de elegibilidad para los visitantes anónimos
- Gastos generales de gestión de elementos de contenido: cada elemento necesita representaciones, reglas de aceptación y mantenimiento
- La depuración de la lógica de decisión es más compleja que los enfoques basados en reglas

**Experience League:**

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)

### Comparación de opciones

En la tabla siguiente se comparan las tres opciones de implementación en función de criterios clave.

| Criterios | Opción A: basado en reglas | Opción B: experimentación | Opción C: toma de decisiones |
| --- | --- | --- | --- |
| Mejor para | Asignaciones de segmento a contenido conocidas | Descubrimiento del contenido que mejor funciona | Selección de contenido dinámico de catálogos grandes |
| Complejidad | Baja | Medio | Alta |
| Latencia | Subsegundo (borde) | Subsegundo (borde) | Subsegundo (borde) |
| Precisión de Personalization | Nivel de segmento (reglas de audiencia) | Nivel de visitante (asignación aleatoria) | Nivel de visitante (idoneidad + clasificación) |
| Optimización de contenido | Manual (sin medición) | Pruebas estadísticas (A/B) | Continua (clasificación de IA) o manual (prioridad) |
| Requiere segmentos de audiencia | Sí (evaluado por el perímetro) | No (división del tráfico) | Opcional (para reglas de idoneidad) |
| Capacidad de medición | Ninguno integrado (requiere CJA) | Informes de experimentos integrados | Informes integrados de toma de decisiones |
| Tamaño del catálogo de contenido | Pequeño (1:1 segmento a contenido) | Pequeño (2-10 variantes) | Grande (artículos aptos ilimitados) |
| Requiere | Audiencias de Edge, variantes de contenido | Campaña con el experimento habilitado | Componentes de toma de decisiones (ubicaciones, ofertas, políticas) |

### Elija la opción correcta

Utilice la siguiente lógica de decisión para seleccionar la opción de implementación adecuada:

1. **¿Ya sabe qué contenido se debe mostrar a cada segmento de visitante?**
   - Sí: Comience con **Opción A (basada en reglas)**. Ha establecido estrategias de contenido por segmento y necesita una entrega determinista.
   - No: Pasemos a la pregunta 2.

2. **¿Necesita probar un número pequeño de variantes de contenido para encontrar el mejor ejecutante?**
   - Sí: Elija **Opción B (experimento)**. Desea una validación estadística antes de comprometerse con una estrategia de contenido.
   - No: Pasemos a la pregunta 3.

3. **¿Tiene un catálogo grande de elementos de contenido con requisitos de clasificación y elegibilidad complejos?**
   - Sí: Elija **Opción C (Toma De Decisiones)**. Necesita una selección de contenido dinámico que escale más allá de las reglas simples.
   - No: Comience con **Opción A (basada en reglas)** para simplificar y, a continuación, evolucione a Opción B o C a medida que aumenten los requisitos.

**Combinar opciones:** Estas opciones no se excluyen mutuamente. Una progresión común es comenzar con la opción B (Experimentación) para descubrir contenido ganador e implementar ganadores mediante la opción A (basada en reglas) para una entrega continua. La opción C (Decisioning) se puede colocar en la parte superior para los casos de uso que requieren una selección dinámica basada en el catálogo, mientras que la opción A gestiona reglas deterministas más sencillas.

## Fases de implementación

Las siguientes fases describen el flujo de trabajo de implementación de extremo a extremo.

### Fase 1: Configuración de superficies web

**Función de aplicación:** AJO: Configuración de canal

Defina las superficies de canal web que especifican en qué parte del sitio web se enviará el contenido personalizado. Una superficie web identifica una dirección URL o un patrón de URL de página específico y la ubicación de la página (selector CSS o superficie de experiencia basada en código) donde AJO puede insertar o reemplazar contenido.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: tipo de superficie** — ¿Cómo se debe entregar el contenido personalizado a la página?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Canal web (editor visual) | La personalización implica la modificación de elementos de página visibles (titulares, titulares, imágenes, CTA) mediante un editor visual de arrastrar y soltar | Requiere la extensión del explorador del diseñador web. Es ideal para cambios de contenido liderados por marketing. Se limita a las modificaciones visuales de elementos de página existentes. |
| Experiencia basada en código | La personalización requiere la inyección de datos estructurados (JSON) que el código de la aplicación web consume y procesa | Requiere implementación para desarrolladores para consumir la carga útil JSON. Máxima flexibilidad para una personalización compleja. Ideal para SPA, componentes dinámicos y procesamiento programático. |
| Ambos (híbridos) | Las diferentes personalizaciones en el mismo sitio necesitan diferentes mecanismos de envío | Utilice el canal web para realizar cambios visuales sencillos y experiencias basadas en código para el procesamiento programático. Aumenta la complejidad de la implementación pero maximiza la cobertura. |

>[!NOTE]
>**Decisión: ámbito de superficie** — ¿Qué ámbito de URL debe cubrir la superficie web?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Coincidencia de URL exacta | Personalization se dirige a una página específica (por ejemplo, página principal, página de aterrizaje) | La segmentación más precisa. Requiere superficies independientes para cada página. |
| Patrón de URL con caracteres comodín | Personalization se aplica a toda una categoría de páginas (por ejemplo, todas las páginas de productos, todos los artículos de blogs) | Reduce la sobrecarga de gestión de superficies. Las variantes de contenido deben diseñarse para que funcionen en todas las páginas coincidentes. |
| Superficie de aplicación de una sola página (SPA) | El sitio web es un SPA donde los cambios en la URL no almacenan en déclencheur las recargas de la página completa | Requiere la configuración de [!DNL Web SDK] según SPA con llamadas de `sendEvent` en los cambios de vista. Las definiciones de superficie utilizan el nombre de vista de SPA en lugar de la URL. |

**Navegación por la interfaz de usuario:** [!DNL Journey Optimizer] > Administración > Canales > Configuración web

**Detalles de configuración de clave:**

- Defina la URL de la página o el patrón de URL para la superficie
- Especifique el selector CSS o el URI de superficie para la ubicación del contenido
- Para las experiencias basadas en código, defina el nombre de superficie al que hará referencia el código de la aplicación
- Asocie la superficie con la zona protegida de AJO donde se crearán las campañas

**Documentación de Experience League:**

- [Introducción al canal web](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/web/get-started-web)
- [Creación de experiencias web](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/web/create-web)
- [Canal de experiencia basado en código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [Configuración de experiencias basadas en código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/code-based-configuration)

### Fase 2: Definir audiencias de comportamiento

**Función de aplicación:** RT-CDP: Evaluación de audiencia

Defina segmentos de audiencia evaluados por Edge basados en señales de comportamiento en la sesión que impulsen la segmentación de personalización. Estas audiencias determinan qué visitantes cumplen los requisitos para cada experiencia personalizada. La evaluación de Edge es obligatoria para este patrón, ya que las decisiones de personalización deben tomarse en periodos de tiempo de menos de segundo a medida que el visitante navega por el sitio.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: selección de señales de comportamiento** — ¿Qué señales en la sesión deben dirigir la segmentación de personalización?

| Señal | Cuándo usar | Idoneidad de Edge |
| --- | --- | --- |
| Parámetros de fuente de referencia/UTM | Personalización de la página de aterrizaje específica de la campaña | Elegible: simple comprobación de atributos en el evento actual. |
| Ubicación geográfica (país, región, ciudad) | Promociones regionales, contenido específico de cada idioma, localizador de tiendas | Elegible: comprobación de atributos de perfil |
| Tipo de dispositivo (escritorio, móvil, tableta) | Diseños de contenido y CTA optimizados para dispositivos | Elegible: comprobación de atributos de perfil |
| Páginas visitadas en la sesión | Afinidad de la categoría, recomendaciones de contenido | Apto con restricciones: sólo comprobaciones simples de recuento de eventos |
| Visitante nuevo frente a recurrente | Mensajería de bienvenida, participación progresiva | Elegible: la persistencia de ECID indica que el visitante regresa |
| Tiempo en el sitio/profundidad de desplazamiento | Ofertas de salida basadas en la participación | Puede requerir una implementación personalizada, no elegible de forma nativa para Edge |

>[!NOTE]
>**Decisión: método de evaluación de audiencia** — Todas las audiencias de este patrón deben usar la evaluación de Edge. Confirme la idoneidad antes de definir los segmentos.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Evaluación de Edge | Necesario para este patrón | Las expresiones de regla de segmento deben ser elegibles para Edge: comparaciones de atributos simples, comprobaciones de pertenencia a segmentos, sin consultas de series temporales ni funciones de agregación. Latencia de evaluación de subsegundo. |
| Evaluación de la transmisión (reserva) | Cuando la expresión de regla de segmento no es apta para Edge, pero se acepta en tiempo casi real | Latencia de segundos a minutos. Admite expresiones de reglas de segmentos más complejas. Puede introducir un retraso notable en la entrega de personalización. |

**Navegación de la interfaz de usuario:** Cliente > Audiencias > Crear audiencia > Generar regla

**Detalles de configuración de clave:**

- Utilice el Generador de segmentos para definir reglas de audiencia mediante atributos de comportamiento
- Compruebe la idoneidad del perímetro confirmando que la expresión de regla de segmento solo utiliza funciones admitidas (comparaciones de atributos simples, pertenencia a segmentos)
- Establezca la política de combinación en la política de combinación activa para extremos configurada en F4
- Previsualizar la población de audiencia para validar el segmento devuelve los resultados esperados
- Para audiencias basadas en vistas de página en la sesión, utilice atributos de nivel de evento de la sesión actual en lugar de consultas de series temporales

**Donde las opciones difieren:**

**Para La Opción A (Basada En Reglas):**
Cree segmentos de audiencia distintos para cada variante de contenido. Cada segmento representa una condición de comportamiento específica (por ejemplo, &quot;Referencia = Google AND Geo = US&quot; se asigna a la variante de contenido A). El número de audiencias es igual al número de reglas de personalización.

**Para Opción B (Experimentación):**
La definición de audiencia es opcional. Si el experimento se dirige a todos los visitantes, no se requiere ninguna audiencia: la división del tráfico gestiona la asignación de variantes. Si el experimento se dirige a un subconjunto específico (por ejemplo, solo visitantes móviles), defina una audiencia de segmentación única para la elegibilidad del experimento.

**Para Opción C (Toma De Decisiones):**
Defina audiencias para usarlas como reglas de aceptación en los elementos de contenido. Estas audiencias determinan qué visitantes cumplen los requisitos para qué elementos de contenido de la política de decisión. El motor de decisión gestiona la selección de contenido entre los elementos aptos.

**Documentación de Experience League:**

- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/pql/overview)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)

### Fase 3: Crear contenido y crear variantes

**Función de la aplicación:** AJO: Creación de mensajes, AJO: Experimentación de contenido (Opción B), AJO: Decisioning (Opción C)

Cree las variantes de contenido personalizadas que se enviarán a los visitantes en función del abono a audiencia (Opción A), la asignación de experimentos (Opción B) o la lógica de toma de decisiones (Opción C). Esta fase cubre la creación de contenido mediante el diseñador web de AJO o el editor de experiencias basado en código, así como la configuración de experimento o toma de decisiones que rige la forma en que se selecciona el contenido.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: enfoque de creación de contenido** — ¿Cómo se deben crear las variantes de contenido web?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Editor visual web | El equipo de marketing puede modificar los elementos de página visualmente sin código | Requiere extensión de explorador. Es ideal para modificaciones de texto, imagen y CTA. Limitado a modificar elementos de página existentes. |
| Editor de experiencias basado en código | El contenido requiere datos estructurados (JSON) que procesa el código de la aplicación | Máxima flexibilidad. Requiere implementación para desarrolladores para consumir la carga útil. Ideal para componentes dinámicos y SPA. |
| Editor de código HTML/CSS | Las modificaciones de contenido requieren HTML o CSS personalizados | Control directo de código. Requiere experiencia en HTML/CSS. Es ideal para cambios de diseño complejos. |

>[!NOTE]
>**Decisión: tokens de Personalization**. ¿El contenido debe incluir personalización dinámica mediante atributos contextuales o de perfil?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Variantes de contenido estático | Cada variante es un fragmento de contenido fijo sin tokens dinámicos | El enfoque más simple. El contenido es predecible y fácil de evaluar. No hay riesgo de que falten valores de atributo. |
| Contenido dinámico con expresiones de personalización | El contenido incluye tokens de estilo Handlebars que se resuelven en atributos de perfil o evento (por ejemplo, nombre de ciudad, fuente de referencia) | Contenido más relevante. Requiere valores de reserva para atributos que pueden ser nulos en perfiles anónimos. Use la sintaxis `{{profile.homeAddress.city}}` con los ayudantes. |
| Bloques de contenido condicionales | Distintos bloques de contenido se representan en función de las condiciones de atributo dentro de una sola variante | Reduce el número de variantes distintas necesarias. Aumenta la complejidad del contenido. Bueno para variaciones menores dentro de un diseño compartido. |

**Navegación por la interfaz de usuario:** [!DNL Journey Optimizer] > Campañas > Seleccionar campaña > Editar contenido

**Detalles de configuración de clave:**

- Crear contenido mediante el diseñador web (modificaciones visuales) o el editor de experiencias basado en código (carga útil JSON)
- Utilice el editor de expresiones de personalización para insertar tokens dinámicos desde atributos de perfil de Edge
- Configure el contenido de reserva para tokens de personalización que puedan estar vacíos en perfiles anónimos
- Vista previa del contenido con perfiles de prueba para verificar el procesamiento en todos los escenarios

**Donde las opciones difieren:**

**Para La Opción A (Basada En Reglas):**
Cree una variante de contenido distinta para cada segmento de audiencia definido en la fase 2. Enlace cada variante a su audiencia de destino mediante reglas de contenido condicional en la configuración de la campaña. Asegúrese de que exista una variante de contenido predeterminada para los visitantes que no coincidan con ninguna regla de audiencia.

**Para Opción B (Experimentación):**
Variantes de tratamiento del autor (A, B, C, etc.) para el experimento. Habilite la experimentación de contenido en la campaña, defina variantes de tratamiento con su contenido, establezca porcentajes de asignación de tráfico y configure la métrica de éxito.

- Definir de 2 a 10 variantes de tratamiento con contenido distinto
- Establezca la asignación de tráfico (por ejemplo, 50/50 para A/B o división ponderada para pruebas de menor riesgo)
- Incluya opcionalmente un grupo de exclusión (por ejemplo, el 10% recibe el contenido predeterminado) para medir el alza incremental
- Seleccione la métrica de éxito: aperturas únicas, clics únicos, conversiones o métricas personalizadas
- Defina el umbral de confianza: 95 % para pruebas estándar, 99 % para decisiones de alto riesgo, 90 % para aprendizaje direccional
- **Navegación de la interfaz de usuario:** Campaign > Experimento de contenido > Agregar tratamiento > Asignación de tráfico > Métrica de éxito

**Para Opción C (Toma De Decisiones):**
Configure la pila del componente Decisioning e integre el componente en la campaña.

1. **Crear ubicaciones**: defina en qué parte de la página aparecerán los elementos de contenido (web HTML, web JSON, imagen web)
   - **Navegación de la interfaz de usuario:** [!DNL Journey Optimizer] > Componentes > Administración de decisiones > Ubicaciones
2. **Definir reglas de elegibilidad**: cree reglas basadas en atributos de perfil de Edge que determinen qué visitantes cumplen los requisitos para cada elemento de contenido
   - **Navegación de la interfaz de usuario:** [!DNL Journey Optimizer] > Componentes > Administración de decisiones > Reglas
3. **Crear elementos de contenido (ofertas)**: cree elementos de contenido personalizados con representaciones para cada ubicación, reglas de elegibilidad, prioridad y límite opcional
   - **Navegación de la interfaz de usuario:** [!DNL Journey Optimizer] > Componentes > Administración de decisiones > Ofertas > Crear oferta
4. **Crear contenido de reserva**: defina un elemento de reserva devuelto cuando no se cumpla ningún elemento personalizado
   - **Navegación de la interfaz de usuario:** [!DNL Journey Optimizer] > Componentes > Administración de decisiones > Ofertas > Crear oferta de reserva
5. **Organizar en colecciones** — Agrupar elementos de contenido mediante calificadores de colección (etiquetas) y crear colecciones
   - **Navegación de la interfaz de usuario:** [!DNL Journey Optimizer] > Componentes > Administración de decisiones > Cualificadores de colección/Colecciones
6. **Crear directiva de decisión**: vincule las ubicaciones a las colecciones y seleccione la estrategia de clasificación (basada en prioridades, en fórmulas o en IA)
   - **Navegación de la interfaz de usuario:** [!DNL Journey Optimizer] > Componentes > Administración de decisiones > Decisiones > Crear decisión

**Documentación de Experience League:**

- [Creación de experiencias web](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/web/create-web)
- [Canal de experiencia basado en código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fase 4: Configuración de la campaña y la entrega

**Función de aplicación:** AJO: Campaign Execution

Cree y active la campaña web de AJO que enlaza la superficie web (Fase 1), la segmentación de audiencias o la configuración del experimento (Fases 2-3) y las variantes de contenido (Fase 3) en una unidad de entrega. La campaña controla cuándo y cómo se sirve el contenido personalizado a los visitantes.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: Tipo de campaña** — ¿Cómo se debe activar la campaña?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Campaña programada (siempre activada) | Personalization debe ejecutarse continuamente para todos los visitantes aptos | Establezca la fecha de inicio sin fecha de finalización para la personalización permanente. La evaluación de audiencias se produce al límite en tiempo real. Más común en la personalización web. |
| Campaña programada (con límite de tiempo) | Personalization está ligado a un periodo de promoción o a un evento de temporada específico | Establecer fechas de inicio y finalización explícitas. Campaign se desactiva automáticamente en la fecha de finalización. Ideal para campañas promocionales. |
| Campaña activada por API | La entrega de Personalization debe activarse mediante un evento externo del sistema | Requiere integración de API. Menos común para la personalización web anónima. Se utiliza cuando un sistema backend debe controlar cuándo está activa la personalización. |

**Navegación por la interfaz de usuario:** [!DNL Journey Optimizer] > Campañas > Crear campaña

**Detalles de configuración de clave:**

- Seleccione el canal Web y la superficie Web configurados en la fase 1
- Enlace la audiencia de destino (para la opción A), configure las opciones del experimento (para la opción B) o incruste la decisión (para la opción C)
- Establezca la programación de la campaña (fecha de inicio, fecha de finalización o siempre activada)
- Configure la restricción de frecuencia a nivel de campaña si corresponde
- Revise toda la configuración y active la campaña

**Donde las opciones difieren:**

**Para La Opción A (Basada En Reglas):**
Cree una campaña por regla de personalización, cada una dirigida a una audiencia perimetral diferente con su variante de contenido correspondiente. También puede utilizar una sola campaña con reglas de contenido condicional que asignen la pertenencia de la audiencia a variantes de contenido dentro de una campaña.

**Para Opción B (Experimentación):**
Cree una sola campaña con la experimentación de contenido habilitada. La configuración del experimento (variantes, asignación de tráfico, métrica de éxito) se definió en la fase 3. Active la campaña para iniciar el experimento.

**Para Opción C (Toma De Decisiones):**
Cree una campaña que incruste la política de decisión configurada en la fase 3. La acción de contenido de la campaña hace referencia al ámbito de decisión, que almacena en déclencheur el motor de decisión en el perímetro. Active la campaña para comenzar la entrega de contenido basado en decisiones.

**Documentación de Experience League:**

- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introducción a las campañas](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Fase 5: informar y analizar el rendimiento

**Función de aplicación:** AJO: Informes y análisis de rendimiento

Monitorice el rendimiento de la personalización mediante los informes integrados de AJO y, opcionalmente, amplíe el análisis con CJA para obtener perspectivas más profundas entre canales. Esta fase abarca el acceso a informes de campaña en directo e históricos, la revisión de los resultados de los experimentos y la creación de espacios de trabajo de análisis personalizados.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: profundidad del informe**. ¿Qué profundidad debe tener el análisis de rendimiento?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo informes nativos de AJO | Las métricas básicas de envío y participación son suficientes | Proporciona impresiones, clics, CTR y métricas de conversión listas para usar. Disponible inmediatamente en la interfaz de usuario de Campaign. Personalización limitada. |
| Informes AJO + análisis CJA | Se necesita un análisis funnel profundo, una comparación de cohortes o una medición de impacto en canales múltiples | Requiere conexión de CJA y vista de datos vinculada a conjuntos de datos de AJO. Permite el análisis de forma libre, las métricas calculadas personalizadas, el modelado de atribución y la publicación de audiencias. |

**Navegación por la interfaz de usuario:** [!DNL Journey Optimizer] > Campañas > Seleccionar campaña > Ver informe

**Detalles de configuración de clave:**

- Acceda al informe en directo durante las campañas activas para monitorizar la entrega en tiempo real (se actualiza cada 60 segundos, muestra las últimas 24 horas)
- Acceda al informe histórico (todo el tiempo) después de la finalización de la campaña para un análisis completo (puede tardar hasta dos horas en rellenarse completamente)
- Para la Opción B (Experimentación): revise el informe del experimento para la comparación del rendimiento del tratamiento, los intervalos de confianza y la declaración de ganador
- Para el análisis de CJA: asegúrese de que una conexión de CJA incluya conjuntos de datos de evento de experiencia de AJO y de que una vista de datos esté configurada con métricas de personalización web

**Donde las opciones difieren:**

**Para La Opción A (Basada En Reglas):**
Revise los informes de campaña de cada segmento de audiencia para comparar las métricas de entrega y participación en variantes de contenido personalizadas. Utilice CJA para crear un espacio de trabajo comparativo que mida el impacto de conversión del contenido personalizado frente al predeterminado.

**Para Opción B (Experimentación):**
Revise el informe del experimento para obtener confianza estadística, alza del tratamiento e identificación del ganador. Espere a que se alcance el umbral de confianza antes de declarar un ganador. Aplicar contenido ganador como variante permanente (transición a la opción A para envío continuo).

- **Navegación de la interfaz de usuario:** Campaign > Experimento de contenido > Ver informe
- **Experience League:** [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

**Para Opción C (Toma De Decisiones):**
Revise las métricas de rendimiento de la toma de decisiones, incluidas las tasas de impresión de ofertas, la frecuencia de selección y la atribución de conversión por elemento de contenido. Analice el rendimiento de las estrategias de clasificación y si el contenido de reserva se sirve con demasiada frecuencia (lo que indica que las reglas de elegibilidad son demasiado restrictivas).

**Documentación de Experience League:**

- [Informe en vivo de la campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/home)
- [Cálculos estadísticos en el Experimento de Contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

## Consideraciones sobre la implementación

Esta sección abarca protecciones, escollos comunes, prácticas recomendadas y decisiones de compensación para este patrón de caso de uso.

### Protecciones y límites

Revise las siguientes protecciones antes y durante la implementación.

- Los segmentos de Edge se limitan a comprobaciones de atributos sencillas y a la pertenencia a segmentos (sin consultas de series temporales ni agregaciones complejas): [idoneidad para la segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)
- Solo puede haber una política de combinación activa en Edge por zona protegida: [protecciones de perfil](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- Máximo de 4000 definiciones de segmento por zona protegida — [Protecciones de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- Máximo de 500 campañas activas por zona protegida: [protecciones de Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 10 variantes de tratamiento por experimento de contenido: [límites del experimento de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 10 000 ofertas personalizadas aprobadas por zona protegida (opción C) — [Protecciones de administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 30 ubicaciones por decisión (opción C) — [protecciones de Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- Los modelos de clasificación de IA requieren un mínimo de 1000 eventos de conversión para la formación (opción C)
- [!DNL Edge Network] tiempo de respuesta SLA: &lt; 200 ms para segmentos evaluados por el perímetro
- Caducidad de perfil seudónimo: configurable de 14 a 365 días para perfiles solo de ECID
- Los informes en vivo se actualizan cada 60 segundos y muestran las últimas 24 horas de datos
- Los informes históricos pueden tardar hasta dos horas en rellenarse completamente después de la finalización de la campaña

### Peligros comunes

Evite los siguientes errores comunes de implementación.

- **[!DNL Web SDK]no envía señales de comportamiento a AEP:** Compruebe que la secuencia de datos tiene habilitado el servicio [!DNL Adobe Experience Platform] y que el conjunto de datos de evento está asignado correctamente. Sin esto, los perfiles de Edge no se rellenan y la evaluación de audiencias falla de forma silenciosa: el visitante recibe contenido predeterminado sin indicación de error.
- La audiencia de **Edge devuelve cero calificaciones:** La segmentación de Edge tiene requisitos de elegibilidad estrictos. Las consultas de series temporales, las funciones de agregación y las consultas de varias entidades no son elegibles para Edge. Vuelva a escribir la expresión de regla de segmento mediante comparaciones de atributos simples o comprobaciones de pertenencia a segmentos.
- **La política de combinación no está activa en el perímetro:** Si la política de combinación utilizada por el segmento de audiencia no tiene `isActiveOnEdge: true`, las búsquedas del perfil de Edge fallarán y la personalización no se entregará. Solo puede haber una política de combinación por zona protegida activa en Edge. Compruebe que no existe ningún conflicto.
- **Parpadeo de Personalization al cargar la página:** La llamada de [!DNL Web SDK] `sendEvent` que recupera propuestas de personalización debe ejecutarse antes de que la página procese el área de contenido de destino. Implemente fragmentos preocultados o procesamiento asincrónico para evitar que el contenido predeterminado parpadee antes de que se cargue el contenido personalizado.
- **El contenido no se está representando en los cambios de ruta de la SPA:** Las aplicaciones de una sola página requieren llamadas `sendEvent` explícitas con información de vista actualizada cuando cambia la ruta. Sin esto, [!DNL Edge Network] no vuelve a evaluar la personalización para la nueva vista.
- **El experimento no alcanza relevancia estadística:** El volumen de tráfico insuficiente o el número excesivo de variantes de tratamiento diluyen el tamaño de la muestra por variante. Reduzca el número de variantes o aumente la duración del experimento. No detenga los experimentos prematuramente, los resultados pueden ser engañosos.
- **La toma de decisiones solo devuelve contenido de reserva:** Compruebe que se aprueban los elementos de contenido personalizados, dentro de su intervalo de fechas de validez, y que las reglas de elegibilidad coinciden con los atributos de perfil de Edge del visitante anónimo. Compruebe también que no se han alcanzado los límites de límite.

### Prácticas recomendadas

Siga estas recomendaciones para una implementación exitosa.

- **Empiece por el método simple y, a continuación, itere:** Empiece por la opción A (basada en reglas) para la personalización inicial y, a continuación, utilice la opción B (experimentación) para validar las suposiciones y la opción C (toma de decisiones) para los casos de uso avanzados. Cada opción se basa en la infraestructura básica.
- **Use la preocultación para evitar parpadeos:** Implemente el fragmento de preocultación de AEP en las páginas donde se enviará la personalización. Esto oculta el área de contenido de destino hasta que el contenido personalizado está listo para procesarse, lo que evita el parpadeo visual.
- **Diseñar contenido de reserva de forma deliberada:** El contenido predeterminado (no personalizado) debe ser una experiencia de alta calidad por sí solo. Los visitantes que no cumplan los requisitos para la personalización (o cuando la respuesta de [!DNL Edge Network] se retrase) no deberían recibir una experiencia degradada.
- **Valide la idoneidad del perímetro antes de crear audiencias:** Antes de invertir en el desarrollo de reglas de audiencia, confirme que la expresión de regla de segmento es apta para el perímetro revisando los criterios de idoneidad en Experience League. Las expresiones no aptas volverán silenciosamente a la evaluación por lotes o de flujo continuo con una latencia inaceptable para este patrón.
- **Supervisar el rendimiento del envío perimetral:** Configure alertas de supervisión para [!DNL Edge Network] tiempos de respuesta y errores de envío de personalización. Los problemas de entrega de Edge son invisibles para el visitante (ve contenido predeterminado) y pueden pasar desapercibidos sin supervisión proactiva.
- **Configurar la caducidad del perfil seudónimo:** Establezca períodos de caducidad adecuados para los perfiles Edge anónimos a fin de equilibrar la personalización entre sesiones (reconociendo a los visitantes que regresan) con el cumplimiento de la privacidad y la administración del almacenamiento.
- **Prueba con perfiles representativos:** Al obtener una vista previa del contenido personalizado, use perfiles de prueba que representen los escenarios reales de visitantes anónimos (sin datos de CRM, historial de comportamiento limitado, varias ubicaciones geográficas y dispositivos).

### Decisiones de compensación

Tenga en cuenta los siguientes aspectos clave al planificar la implementación.

>[!NOTE]
>**Compensación: Personalization en su amplitud frente a la complejidad de la implementación**
>
>Una personalización más granular (muchas audiencias, muchas variantes de contenido) produce experiencias más relevantes, pero aumenta la complejidad de la configuración y la sobrecarga de producción de contenido.
>
>- **Favoritos de personalización amplia:** Simplicidad, tiempo de comercialización más rápido, menor costo de producción de contenido. Un pequeño número de audiencias y variantes cubre la mayoría de los visitantes con una personalización significativa.
>- **Favoritos de personalización granular:** Máxima relevancia, mayor alza de participación y mejores tasas de conversión. Muchas audiencias y variantes abordan señales de comportamiento específicas con contenido personalizado.
>- **Recomendación:** Comience con 3-5 reglas de personalización de alto impacto dirigidas a los segmentos de visitantes más comunes (por ejemplo, origen de referencia, tipo de dispositivo, región geográfica). Mida el impacto y, a continuación, expanda a reglas más granulares basadas en el rendimiento observado y el valor empresarial.

>[!NOTE]
>**Compensación: determinismo basado en reglas vs. optimización impulsada por IA**
>
>Los enfoques basados en reglas (Opción A) proporcionan a la empresa un control total sobre el contenido que ve cada visitante. Los enfoques de clasificación de IA (Opción C) optimizan la selección de contenido con el paso del tiempo, pero reducen la visibilidad de por qué se seleccionó contenido específico.
>
>- **Favoritos basados en reglas:** Previsibilidad, auditabilidad y control empresarial. Los equipos de marketing saben exactamente qué contenido recibe cada segmento y pueden explicar la lógica a las partes interesadas.
>- **Favoritos impulsados por IA:** Optimización del rendimiento, escalabilidad y mejora continua. El modelo de IA descubre afinidades entre contenido y visitante que la escritura de reglas humanas podría pasar por alto.
>- **Recomendación:** Utilice basada en reglas para decisiones de contenido de alto riesgo en las que la coherencia de la marca y la transparencia de las partes interesadas sean fundamentales. Utilice la clasificación de IA para catálogos de contenido grandes en los que la administración manual de reglas resulta difícil de manejar y la optimización continua ofrece un alza mensurable.

>[!NOTE]
>**Compensación: persistencia de perfil anónima frente a cumplimiento de privacidad**
>
>La caducidad más larga del perfil seudónimo permite una mejor personalización entre sesiones (reconociendo a los visitantes que regresan, creando un contexto de comportamiento a lo largo del tiempo). Una caducidad más corta mejora el cumplimiento de la privacidad y reduce los costes de almacenamiento.
>
>- **Favoritos de caducidad más largos:** Perfiles anónimos más completos, mejor reconocimiento de visitantes que regresan y más datos para las decisiones de personalización. Establezca la caducidad en 90-365 días.
>- **Favoritos de caducidad más cortos:** cumplimiento de la privacidad (RGPD, CCPA), costos de almacenamiento reducidos y riesgo minimizado de datos de perfiles antiguos. Establezca la caducidad en 14-30 días.
>- **Recomendación:** Alinee la caducidad con la directiva de consentimiento de cookies y los requisitos de privacidad de su organización. Para la mayoría de las implementaciones, de 30 a 90 días proporciona un equilibrio razonable entre el valor de personalización y el cumplimiento de la privacidad.

## Documentación relacionada

Los siguientes recursos de Experience League proporcionan detalles adicionales sobre las funciones utilizadas en este patrón de caso de uso.

**Canal web y experiencias basadas en código**

- [Introducción al canal web](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/web/get-started-web)
- [Creación de experiencias web](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/web/create-web)
- [Canal de experiencia basado en código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [Configuración de experiencias basadas en código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/code-based-configuration)

**Audiencias y segmentación**

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentación de Edge](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Segmentación de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/pql/overview)

**Personalization y contenido**

- [Añadir personalización](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxis de Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Contenido dinámico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabajo con plantillas de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabajo con fragmentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

**Experimentación de contenido**

- [Introducción al experimento de contenido](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Creación de un experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Informe de experimento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Cálculos estadísticos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

**Administración de decisiones**

- [Información general de Administración de decisiones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Creación de ubicaciones](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Creación de reglas de decisión](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crear ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Crear ofertas de reserva](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Crear colecciones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Crear decisiones](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estrategias de clasificación](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entrega de ofertas en mensajes](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

**Campañas**

- [Introducción a las campañas](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Creación de una campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

**[!DNL Web SDK]y recopilación de datos**

- [Información general de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home)
- [Instalación de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/install/overview)
- [Configuración de flujos de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure)
- [Información general sobre etiquetas](https://experienceleague.adobe.com/es/docs/experience-platform/tags/home)

**Identidad y perfil**

- [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Información general sobre áreas de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview)
- [Resumen del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/home)

**Modelado de datos**

- [Información general del sistema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/home)
- [Conceptos básicos de composición](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/composition)

**Informes y análisis**

- [Informe en vivo de la campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Informe global de campaña](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Trabajo con Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Información general de Analysis Workspace](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-workspace/home)
- [Información general de CJA](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-overview/cja-overview)

**Gobernanza de datos y privacidad**

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Información general sobre Advanced Data Lifecycle Management](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/home)
- [Grupo de campos de consentimiento y preferencias](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/field-groups/profile/consents)

**Protecciones**

- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/get-started/guardrails)
- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/guardrails)
- [Protecciones del servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/guardrails)
