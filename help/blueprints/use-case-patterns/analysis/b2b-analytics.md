---
title: Análisis B2B
description: Aprenda a incluir información de nivel de cuenta B2B en el análisis de recorrido de clientes en canales múltiples.
solution: Customer Journey Analytics, Real-Time Customer Data Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '7528'
ht-degree: 1%

---


# Análisis B2B

Esta guía proporciona una referencia de implementación completa para el análisis de nivel de cuenta B2B mediante [!DNL Customer Journey Analytics] ([!DNL CJA]) B2B edition y [!DNL Real-Time Customer Data Platform] ([!DNL RT-CDP]) B2B edition. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten incorporar información de nivel de cuenta B2B en el análisis de recorrido de clientes en canales múltiples.

Abarca todos los enfoques viables para el análisis centrado en las cuentas, desde estructuras de cuentas planas hasta jerarquías de cuentas globales complejas, con instrucciones sobre cuándo elegir cada opción. El plan aborda las conexiones de datos B2B, la configuración de vistas de datos de cuenta, el análisis del espacio de trabajo y la publicación del panel.

B2B Analytics amplía las capacidades estándar de [!DNL CJA] con conexiones basadas en cuentas, contenedores específicos de B2B (cuenta, cuenta global, oportunidad, grupo de compra) e informes de nivel de cuenta. Esta capacidad permite a las organizaciones analizar la participación de ventas y marketing a nivel de cuenta, rastrear la progresión de las oportunidades, medir la integridad del grupo de compra y atribuir ingresos a puntos de contacto de marketing en ciclos de ventas B2B ampliados.

## Resumen del caso de uso

Las organizaciones B2B se enfrentan a un desafío de análisis fundamental: sus clientes no son personas individuales, sino cuentas compuestas por múltiples partes interesadas, grupos de compra y oportunidades. Los análisis estándar basados en personas no pueden responder preguntas como &quot;¿Qué cuentas son las más comprometidas?&quot;, &quot;¿Cuán completos son nuestros grupos de compra?&quot; o &quot;¿Qué puntos de contacto de marketing impulsan la progresión de la oportunidad?&quot;.

B2B Analytics resuelve esto aprovechando [!DNL CJA] B2B edition para crear vistas analíticas centradas en las cuentas que combinan datos de comportamiento a nivel de persona con dimensiones de cuenta, oportunidad y grupo de compra. [!DNL RT-CDP] B2B edition proporciona la unificación del perfil de cuenta subyacente y la resolución de identidad B2B que alimenta la capa de análisis. En conjunto, estas soluciones permiten a las organizaciones crear análisis de recorrido en canales múltiples a nivel de cuenta, correlacionar la participación de marketing con la progresión de la canalización y ofrecer perspectivas procesables a los equipos de marketing y ventas.

La audiencia de destino incluye equipos de operaciones de marketing B2B, líderes de generación de demanda, analistas de operaciones de ingresos y líderes de ventas que necesitan visibilidad sobre la participación a nivel de cuenta y el estado de la canalización.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Mejore los análisis y los informes

Mejore las capacidades de creación de informes para obtener perspectivas de marketing más rápidas y procesables mediante paneles unificados y herramientas de autoservicio. B2B Analytics permite a las organizaciones consolidar datos de participación a nivel de cuenta de múltiples fuentes en un único entorno analítico, lo que proporciona visibilidad en canales múltiples sobre cómo los programas de marketing influyen en la canalización y los ingresos.

**KPI:** eficiencia, productividad

[Más información sobre la mejora de los análisis y los informes](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)

### Habilitar la toma de decisiones basada en datos

Habilite a los equipos con análisis de autoservicio, perspectivas de clientes en tiempo real y predicciones impulsadas por IA para guiar la estrategia. Los análisis a nivel de cuenta equipan a los equipos de marketing y ventas con los datos necesarios para priorizar las cuentas, optimizar las estrategias de participación y alinearse en las oportunidades de canalización.

**KPI:** eficiencia, productividad

[Obtenga más información sobre cómo habilitar la toma de decisiones basada en datos](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)

### Mejore la calificación y conversión de posibles clientes

Aumente la calidad del posible cliente y acelere la progresión de la canalización mediante la puntuación, la nutrición y el seguimiento personalizado. CJA B2B edition proporciona ventanas retrospectivas de cuenta de 13 meses ampliadas diseñadas específicamente para ciclos de ventas B2B, lo que permite una atribución exacta de múltiples contactos en todo el recorrido de la cuenta.

**KPI:** eficiencia, ingresos incrementales

[Obtenga más información sobre cómo mejorar la calificación y conversión de posibles clientes](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran cómo se puede aplicar este patrón en la práctica.

- **Análisis de puntuación de participación de cuenta**: mida y clasifique cuentas según su participación agregada en la web, el correo electrónico, los eventos y las interacciones de contenido para identificar cuentas de alta intención para el seguimiento de ventas
- **Seguimiento de la integridad del grupo de compra** — Analice la composición del grupo de compra en todas las cuentas para identificar lagunas en la cobertura de roles y priorizar la adquisición de posibles clientes para los grupos de compra incompletos
- **Correlación de canalización de oportunidad**: correlacione los datos de participación de marketing con la progresión de la fase de oportunidad para comprender qué campañas y puntos de contacto impulsan el avance de la canalización
- **Atribución B2B multitáctil**: aplique modelos de atribución con ventanas retrospectivas de 13 meses a puntos de contacto de marketing de crédito en todo el recorrido de compra B2B desde el primer contacto hasta el cerrado ganado
- **Asignación de recorridos de cuenta**: visualice el recorrido de cuentas en canales múltiples desde la percepción inicial hasta la creación y el cierre de oportunidades, identificando rutas comunes y puntos de fricción
- **Influencia de la campaña en la canalización**: mida cómo influyen las campañas específicas en la creación de la canalización de la cuenta, el avance de la oportunidad y la generación de ingresos
- **Progresión de la participación del grupo de compra**: efectúe el seguimiento de la evolución de las puntuaciones de participación del grupo de compra a lo largo del tiempo y correlacione los umbrales de participación con los resultados de la oportunidad
- **Rendimiento del contenido basado en cuentas**: Analice qué recursos y temas de contenido resuenan en segmentos de cuenta específicos, industrias o roles de grupo de compra
- **Paneles de alineación de ventas y marketing**: cree paneles compartidos que proporcionen a los equipos de ventas y marketing una vista unificada de la participación de la cuenta, el estado de la canalización y la atribución de ingresos
- **Segmentación de cuentas para activación**: cree segmentos B2B basados en análisis de nivel de cuenta (por ejemplo, &quot;cuentas con un alto nivel de participación sin oportunidades abiertas&quot;) y publíquelos para su activación descendente

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir el éxito de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Puntuación de participación de cuenta | Métrica de participación agregada en todos los contactos de una cuenta | Métrica calculada que combina visitas web, interacciones por correo electrónico, asistencia a eventos y descargas de contenido a nivel de cuenta |
| Integridad del grupo de compra | Porcentaje de funciones requeridas dentro de un grupo de compra | Proporción de puestos ocupados respecto al total de puestos necesarios por grupo de compra, con seguimiento en el tiempo |
| Canalización influenciada por el marketing | Ingresos en canalización que se han visto afectados por las actividades de marketing | Valor de oportunidad donde los contactos de cuenta asociados tienen puntos de contacto de marketing dentro de la ventana de atribución |
| Tasa de conversión de cuenta a oportunidad | Porcentaje de cuentas comprometidas que generan oportunidades cualificadas | Cuentas con oportunidades divididas por el total de cuentas comprometidas durante un periodo definido |
| Duración media del ciclo de oferta | Tiempo desde el primer contacto de marketing hasta el cerrado ganado | Duración media desde el primer punto de contacto atribuido hasta la fecha de cierre de la oportunidad |
| Ingresos de atribución de marketing | Ingresos atribuidos a puntos de contacto de marketing | Ingresos de oportunidades ganadas a puerta cerrada con toques de marketing, distribuidos por modelo de atribución |
| Alcance y penetración de la cuenta | Número de contactos contratados por cuenta de destinatario | Contactos únicos con interacciones de marketing por cuenta, en comparación con el total de contactos conocidos |
| Participación en el contenido por rol de compra | Métricas de participación segmentadas mediante la compra de un rol de grupo | Vistas de página, descargas y tiempo empleado desglosados por persona o función dentro de los grupos compradores |

## Patrón de caso de uso

**Análisis B2B**

Incluya información de nivel de cuenta B2B en el análisis de recorrido de clientes en canales múltiples.

**Cadena de funciones:** Conexión de datos B2B > Configuración de vista de datos de cuenta > Workspace Analysis > Publicación de paneles

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón de caso de uso.

- **[!DNL Customer Journey Analytics]B2B edition**: proporciona conexiones basadas en cuentas, contenedores de vista de datos específicos de B2B, análisis del espacio de trabajo a nivel de cuenta, análisis de grupos de compras, análisis de oportunidades, segmentación B2B y atribución B2B con ventanas retrospectivas extendidas
- **[!DNL Real-Time CDP]B2B edition**: proporciona la base de datos B2B, incluida la unificación del perfil de cuenta, la resolución de identidades B2B, las clases de esquema B2B (cuenta, oportunidad, grupo de compra) y la integración de [!DNL Marketo Engage] para la ingesta de datos de participación B2B

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Requerido | Zona protegida configurada con [!DNL CJA] derechos de B2B edition y [!DNL RT-CDP] B2B edition. Roles aprovisionados para ingenieros de datos, analistas y usuarios de operaciones de marketing con acceso a [!DNL CJA] y al modelo de datos B2B. | [Resumen de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home) |
| Modelado y preparación de datos | Requerido | Esquemas XDM B2B configurados con clases B2B: miembros de lista de marketing empresarial de XDM, relación de persona de cuenta empresarial de XDM, relación de persona de oportunidad empresarial de XDM y miembros de lista de marketing empresarial de XDM. Deben definirse grupos de campos para atributos de cuenta, fases de oportunidad y roles de grupo de compra. Conjuntos de datos creados y habilitados para el perfil. | [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [esquemas de B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b) |
| Fuentes de datos y recopilación | Requerido | Fuentes de datos B2B conectadas, normalmente a través del conector de origen [!DNL Marketo Engage] o del conector de origen CRM [!DNL Salesforce]. Los registros de cuenta, los registros de oportunidad, las relaciones persona-cuenta y los eventos de participación de comportamiento deben fluir a los conjuntos de datos de AEP. [!DNL Web SDK] o la integración [!DNL Marketo] debe estar capturando eventos de comportamiento con asociación de cuenta. | [Resumen de fuentes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home), [conector de Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| Configuración de identidad y perfil | Requerido | Resolución de identidad B2B configurada para resolver relaciones persona a cuenta. Se deben vincular el ID de cuenta, el ID de persona ([!DNL Marketo] ID de posible cliente o ID de contacto de CRM) y las identidades entre dispositivos (ECID, correo electrónico). El gráfico de identidad debe admitir la asignación de persona a cuenta de varios a varios inherente a los modelos de datos B2B. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [resolución de identidad B2B](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b) |
| Definición de audiencia y segmentación | Se asume en contexto | Las definiciones de audiencia de nivel de cuenta deben estar disponibles si los segmentos B2B se publicarán de [!DNL CJA] de nuevo en AEP para su activación. Para casos de uso solo de análisis, no se trata de un requisito previo estricto, pero se recomienda para el análisis basado en segmentos. | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Los atributos calculados en los perfiles de cuenta (por ejemplo, puntuación de participación total, días transcurridos desde la última actividad, recuento de oportunidades) enriquecen las dimensiones analíticas disponibles en [!DNL CJA] para el análisis a nivel de cuenta. | [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Administración del ciclo de datos | Recomendado | Los conjuntos de datos B2B, en particular los datos de eventos de comportamiento de [!DNL Marketo Engage], pueden crecer rápidamente. Las políticas de caducidad de conjuntos de datos ayudan a administrar el almacenamiento y garantizar el cumplimiento de los requisitos de retención de datos. | [Administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Etiquetado y aplicación del uso de datos | Recomendado | Los datos B2B suelen contener información empresarial confidencial (valores contractuales, inteligencia competitiva). Las etiquetas de uso de datos y las políticas de gobernanza garantizan que estos datos se utilicen correctamente en los flujos de trabajo de análisis y activación. | [Resumen de control de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Monitorización y observabilidad | Recomendado | Los conectores de origen B2B ([!DNL Marketo], [!DNL Salesforce]) requieren supervisión para el estado de la ingesta. La supervisión del estado de la conexión en [!DNL CJA] garantiza la actualización de los datos para Analytics. Las reglas de alerta para errores de ingesta evitan paneles obsoletos. | [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Informes y análisis | Incluido | Este patrón es en sí mismo un patrón de análisis. Esta función se incluye de forma inherente ya que la cadena de funciones principales ofrece funciones de creación de informes y análisis. | [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del Catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Customer Journey Analytics] B2B edition

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Conexión basada en cuentas | Fase 1: Conexión de datos B2B | Configure conexiones utilizando Cuenta o Cuenta global como identificador principal para el análisis en el nivel de organización |
| Configuración de vista de datos B2B | Fase 2: Configuración de vista de datos de cuenta | Defina vistas de datos con contenedores específicos de B2B (cuenta, cuenta global, oportunidad, grupo de compra) junto con contenedores estándar de persona, sesión y evento |
| Análisis de Workspace a nivel de cuenta | Fase 3: Análisis de Workspace | Cree análisis de forma libre utilizando dimensiones, métricas y contenedores B2B de nivel de cuenta para obtener perspectivas de recorrido de nivel de organización |
| Análisis del grupo de compra | Fase 3: Análisis de Workspace | Analizar la composición, la participación y la progresión del grupo de compra a través del proceso de decisión de compra |
| Análisis de oportunidad | Fase 3: Análisis de Workspace | Rastree la progresión de la oportunidad a través de las fases de funnel de ventas y correlóciela con los datos de participación de marketing |
| Segmentación B2B | Fase 3: Análisis de Workspace | Creación de segmentos utilizando contenedores B2B para el análisis filtrado a nivel de cuenta |
| Atribución B2B | Fase 3: Análisis de Workspace | Aplicar modelos de atribución con ventanas retrospectivas de cuenta ampliadas de 13 meses para el análisis del ciclo de ventas B2B |
| Creación de métricas calculadas | Fase 3: Análisis de Workspace | Defina métricas calculadas para KPI B2B como la tasa de participación en la cuenta, la integridad del grupo de compra y la influencia de la canalización |
| Publicación de paneles y cuadros de resultados | Fase 4: Publicación del panel | Cree y comparta paneles y cuadros de resultados móviles para el liderazgo de marketing y ventas |
| Publicación de audiencias | Fase 4: Publicación del panel | Volver a publicar audiencias basadas en cuentas definidas por [!DNL CJA] en AEP para la activación descendente |

### [!DNL Customer Journey Analytics]: funciones estándar

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Conexión de datos | Fase 1: Conexión de datos B2B | Enlazar conjuntos de datos B2B de AEP a [!DNL CJA] conexiones para análisis en canales múltiples |
| Configuración de vista de datos | Fase 2: Configuración de vista de datos de cuenta | Configure dimensiones, métricas, atribuciones y configuraciones de persistencia estándar en la vista de datos B2B |
| Análisis de Workspace | Fase 3: Análisis de Workspace | Cree análisis de forma libre con tablas, visitas en orden previsto, flujo, cohorte y visualizaciones de atribución |
| Análisis guiado | Fase 3: Análisis de Workspace | Uso de flujos de trabajo guiados para el análisis de funnel, tendencias y retención a nivel de cuenta |

### [!DNL Real-Time CDP] B2B edition

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Unificación del perfil de cuenta | Requisitos previos (F2/F4) | Consolidar datos B2B de fuentes cruzadas en perfiles de cuenta unificados mediante clases de esquema B2B XDM especializadas |
| Resolución de identidad B2B | Requisito previo (F4) | Resolver relaciones persona a cuenta compatibles con jerarquías de cuentas de varios niveles y asignaciones de varios a varios |
| Integración de [!DNL Marketo Engage] | Requisito previo (F3) | Ingesta de datos de participación de comportamiento y registros de cuenta/posible cliente de [!DNL Marketo Engage] mediante conectores de origen B2B nativos |

## Prerrequisitos

Los siguientes elementos deben estar implementados antes de que comience la implementación.

- La licencia de B2B edition [!DNL CJA] está activa y aprovisionada para la organización
- La licencia de B2B edition [!DNL RT-CDP] está activa con esquemas B2B y perfiles de cuenta configurados
- Se definen los esquemas XDM B2B (cuenta, oportunidad, relación de persona de cuenta, relación de persona de oportunidad, miembros de lista de marketing)
- [!DNL Marketo Engage] y/o los conectores de origen CRM están configurados e ingiriendo datos activamente
- Los datos de evento de comportamiento de nivel de cuenta (visitas web, interacciones por correo electrónico, envíos de formularios) fluyen a AEP con la asociación de cuentas
- Las relaciones persona a cuenta se establecen en el gráfico de identidades
- Hay disponibles al menos 30 días de datos históricos de participación B2B para un análisis significativo
- Las partes interesadas han acordado comprar definiciones de funciones de grupo y asignaciones de intereses de soluciones
- Las cuentas de usuario de [!DNL CJA] se han aprovisionado con perfiles de producto apropiados para las funciones de B2B edition
- Los KPI de objetivo y los requisitos de informes han sido definidos por el liderazgo de marketing y ventas

## Opciones de implementación

Las secciones siguientes describen diferentes enfoques para implementar este patrón de caso de uso.

### Opción A: análisis centrado en la cuenta

**Ideal para:** organizaciones que desean analizar toda la participación y canalizar los datos a través de la vista de la cuenta. Este método utiliza el contenedor Cuenta como unidad analítica principal, lo que proporciona una vista descendente del progreso de las cuentas a través del recorrido de compra.

**Cómo funciona:**

Configure una conexión B2B [!DNL CJA] con Account como identificador principal. Todos los eventos de comportamiento, las oportunidades y los datos de grupos de compra se acumulan en el nivel de cuenta. La vista de datos utiliza Cuenta como contenedor de nivel superior, con Persona, Sesión y Evento anidados en él. Esto permite realizar análisis como &quot;¿Cuántas cuentas visitaron la página de precios y luego crearon una oportunidad en un plazo de 30 días?&quot;

El análisis centrado en cuentas proporciona la vista más natural para las organizaciones B2B, donde la cuenta es la unidad de compra. Se pueden usar dimensiones como el sector, el tamaño de la empresa, el nivel de cuenta y el propietario de la cuenta para desglosar los patrones de participación y las métricas de canalización. La atribución se aplica en el nivel de cuenta con ventanas retrospectivas de 13 meses que admiten ciclos de ventas B2B largos.

**Consideraciones clave:**

- Requiere una asignación de cuenta a persona limpia en el gráfico de identidad
- Todos los eventos a nivel de persona deben ser atribuibles a una cuenta
- El tráfico web anónimo que no se pueda asociar con una cuenta no aparecerá en el análisis de nivel de cuenta

**Ventajas:**

- Proporciona una auténtica vista de nivel de cuenta de todo el recorrido de compra
- Habilita la atribución basada en cuentas que coincide con el modo en que se generan los ingresos B2B
- Admite el análisis de grupos de compras y oportunidades como contenedores anidados dentro de la cuenta
- Alinea los análisis con la estrategia de marketing basado en cuentas (ABM)

**Limitaciones:**

- Requiere una resolución sólida de la identidad de persona a cuenta
- Se excluyen del análisis los datos de participación anónimos o no coincidentes
- Es más complejo de configurar que el análisis centrado en la persona

**Experience League:**

- [Información general sobre CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [Esquemas de B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)

### Opción B: análisis global centrado en las cuentas

**Ideal para:** organizaciones empresariales con jerarquías de cuentas complejas en las que una compañía principal tiene varias cuentas de subsidiarias. Este método utiliza la cuenta global como identificador principal, acumulando toda la actividad de la cuenta subsidiaria en el nivel de la organización principal.

**Cómo funciona:**

Configure la conexión B2B [!DNL CJA] con la cuenta global como identificador principal en lugar de con la cuenta. Esto agrega datos de participación de todas las cuentas de filiales bajo su organización matriz. Por ejemplo, si &quot;Acme Corp&quot; tiene filiales regionales &quot;Acme EMEA&quot; y &quot;Acme APAC&quot;, una conexión de cuenta global consolida todas las participaciones de las tres entidades en una sola vista analítica.

La vista de datos incluye Cuenta global como contenedor de nivel superior, con Cuenta, Persona, Sesión y Evento como contenedores anidados. Esto permite realizar análisis en los niveles de cuenta global y subsidiaria dentro del mismo proyecto de Workspace. Las ventanas retrospectivas de atribución se aplican al nivel de cuenta global, capturando todos los puntos de contacto en toda la jerarquía corporativa.

**Consideraciones clave:**

- Requiere datos de jerarquía de cuentas con relaciones principal-secundario definidas en el modelo de datos B2B
- El ID de cuenta global debe rellenarse y ser preciso en todos los registros de cuenta
- Las cuentas de filiales deben asignarse correctamente a su matriz

**Ventajas:**

- Proporciona visibilidad consolidada en estructuras de cuentas empresariales complejas
- Evita el análisis fragmentado cuando un único cliente empresarial tiene varios registros de cuenta
- Permite la comparación entre filiales regionales en una sola cuenta global
- Admite canalización e informes de ingresos a nivel empresarial

**Limitaciones:**

- Requiere datos precisos de jerarquía de cuentas, que muchas organizaciones tienen dificultades para mantener
- Puede oscurecer los patrones a nivel subsidiario cuando se los ve solamente a nivel global
- Esfuerzo adicional de modelado de datos para establecer y mantener relaciones de jerarquía

**Experience League:**

- [Información general sobre CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### Opción C: análisis híbrido de persona y cuenta

**Ideal para:** organizaciones que realizan la transición del análisis basado en personas al análisis basado en cuentas o aquellas que necesitan vistas a nivel de persona y de cuenta. Este método crea dos vistas de datos a partir de la misma conexión: una centrada en la persona y otra centrada en la cuenta.

**Cómo funciona:**

Configure una sola conexión B2B [!DNL CJA] que incluya todos los conjuntos de datos B2B (evento, cuenta, oportunidad, grupo de compra, relaciones persona-cuenta). A continuación, cree dos vistas de datos: una que utilice la persona como contenedor principal (similar al estándar [!DNL CJA]) y otra que utilice la cuenta como contenedor principal. Los analistas pueden cambiar entre vistas de datos en función de la pregunta que se haga.

La vista de datos centrada en las personas proporciona un análisis de recorrido tradicional a nivel individual (por ejemplo, &quot;¿Cuál es la ruta de conversión para los posibles clientes que se convierten en oportunidades?&quot;), mientras que la vista de datos centrada en las cuentas proporciona análisis a nivel de organización (por ejemplo, &quot;¿Qué cuentas tienen la tasa de conversión de participación a canalización más alta?&quot;). Ambas vistas utilizan los mismos datos subyacentes, lo que garantiza la coherencia.

**Consideraciones clave:**

- Requiere dos vistas de datos con configuraciones de dimensión y métrica potencialmente diferentes
- Los analistas necesitan recibir formación sobre cuándo utilizar cada vista
- Es posible que las métricas calculadas deban crearse por separado para cada vista de datos

**Ventajas:**

- Proporciona flexibilidad para analizar datos en el nivel de persona y de cuenta
- Ruta de adopción más sencilla para equipos acostumbrados a análisis de nivel de persona
- Permite la comparación entre métricas de nivel de persona y de nivel de cuenta
- Admite estrategias de marketing basadas en clientes potenciales y en cuentas

**Limitaciones:**

- Dos vistas de datos para mantener y sincronizar
- Posible confusión para los analistas sobre la vista que deben utilizar
- Es posible que las métricas calculadas y los filtros necesiten la duplicación entre vistas

**Experience League:**

- [Creación o edición de una vista de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Resumen de vistas de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)

### Comparación de opciones

| Criterios | Opción A: centrada en la cuenta | Opción B: global centrado en la cuenta | Opción C: persona híbrida + cuenta |
| --- | --- | --- | --- |
| Mejor para | B2B estándar con estructura de cuenta plana | Empresa con jerarquías principal-secundario | Transición de organizaciones o necesidades duales |
| Complejidad | Medio | Alta | Medium-High |
| Requisitos de datos | Asignación de cuenta a persona | Jerarquía de cuentas + asignación | Asignación de cuenta a persona |
| Ámbito de atribución | Nivel de cuenta (retrospectiva de 13 meses) | Nivel de cuenta global (retrospectiva de 13 meses) | Nivel de persona y cuenta |
| Datos anónimos | Excluido de la vista de cuentas | Excluido de la vista global | Incluido en la vista de persona, excluido de la vista de cuenta |
| Requiere | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition, datos de jerarquía | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition |
| Mantenimiento | Vista de datos única | Vista de datos única | Dos vistas de datos |

### Elija la opción correcta

- **Elija la opción A** si su organización tiene una estructura contable plana (sin jerarquías principal-secundaria), su estrategia ABM funciona en el nivel de cuenta individual y desea la ruta más sencilla para el análisis en el nivel de cuenta.
- **Elija la opción B** si sus cuentas de destino son grandes empresas con cuentas subsidiarias en regiones o divisiones, y necesita informes consolidados en el nivel primario corporativo. Esta opción requiere datos de jerarquía de cuentas de alta calidad.
- **Elija la opción C** si su organización está realizando la transición del marketing basado en clientes potenciales al marketing basado en cuentas, los analistas necesitan análisis de funnel a nivel de persona y análisis de participación a nivel de cuenta, o si tiene una combinación de líneas de negocio B2B y B2C.

## Fases de implementación

Las siguientes fases describen la secuencia de implementación recomendada.

### Fase 1: Conexión de datos B2B

**Función de aplicación:** [!DNL CJA] B2B: Conexión basada en cuenta, [!DNL CJA]: Conexión de datos

Configure la conexión [!DNL CJA] que enlaza los conjuntos de datos B2B de AEP a [!DNL CJA] para su análisis. Esta conexión define qué conjuntos de datos fluyen a [!DNL CJA], el tipo de identificador principal (Cuenta o Cuenta global) y cómo se incorporan los datos históricos y de flujo continuo. La conexión es la base de todos los análisis subsiguientes.

#### Decisión: Tipo de identificador principal

Determine si la conexión debe utilizar el ID de cuenta o el ID de cuenta global como identificador principal.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| ID de cuenta | Estructura de cuenta plana, sin jerarquías principal-secundario | Configuración más sencilla; cada cuenta se analiza de forma independiente. La opción más común para B2B centradas en pymes. |
| ID de cuenta global | Cuentas empresariales con jerarquías de filiales | Requiere datos de jerarquía; agrega todas las filiales bajo la matriz. Lo mejor para los programas ABM empresariales. |

#### Decisión: Selección de conjuntos de datos y designación de tipos

Determine qué conjuntos de datos B2B deben incluirse y cómo debe escribirse cada uno.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Conjuntos de datos de evento (comportamiento) | Incluir siempre | Interacciones web, eventos de correo electrónico, envíos de formularios, descargas de contenido. Debe tener un campo de marca de hora. Estas son las señales de compromiso. |
| Conjuntos de datos de registro de cuenta (perfil) | Incluir siempre | Atributos de cuenta como sector, tamaño, nivel y propietario. Proporciona el contexto dimensional para el análisis de cuentas. |
| Conjuntos de datos de oportunidad (búsqueda/perfil) | Incluir para el análisis de canalización | Fase de oportunidad, valor, fecha de cierre. Necesario para el análisis de atribución de ingresos y canalización. |
| Comprar conjuntos de datos de grupo (búsqueda/perfil) | Incluir para comprar análisis de grupo | Compra de funciones de grupo, puntuaciones de participación, integridad. Necesario para comprar análisis de composición de grupos. |
| Conjuntos de datos de relación persona-cuenta (consulta) | Incluir siempre | Asigna personas a cuentas. Esencial para asociar eventos de nivel de persona con análisis de nivel de cuenta. |
| Conjuntos de datos de campañas/programas (búsqueda) | Incluir para atribución | Metadatos de campaña, tipos de programas, canales. Habilita el análisis de influencia de campaña. |

#### Decisión: Intervalo de relleno

Determine cuántos datos históricos deben importarse en la conexión.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Todos los datos existentes | Los ciclos de ventas B2B son largos (de 6 a 18 meses) y necesita un historial completo | Recomendado para B2B. El relleno puede tardar días para conjuntos de datos grandes, pero proporciona datos de atribución completos. |
| Intervalo de fechas personalizado (últimos 2 a 3 años) | La calidad de los datos se degrada más allá de un determinado punto | Equilibra integridad con calidad de datos. Frecuentes cuando los datos CRM tienen incoherencias históricas. |
| Sin relleno | Solo pruebas o desarrollo | Solo ingresan los datos nuevos. No apto para análisis B2B de producción. |

#### Configuración de la conexión de datos B2B

**Navegación de la interfaz de usuario:** [!DNL Customer Journey Analytics] > Conexiones > Crear nueva conexión

Detalles de configuración clave:

- Seleccione la zona protegida de AEP que contiene los conjuntos de datos B2B
- Establezca el número promedio de eventos diarios para la planificación de la capacidad
- Añada cada conjunto de datos y designe su tipo (evento, búsqueda o perfil)
- Configure el campo ID de persona para que utilice ID de cuenta o ID de cuenta global para las conexiones B2B
- Habilitar el streaming para conjuntos de datos que requieren actualizaciones casi en tiempo real
- Habilitar &quot;Importar todos los datos existentes&quot; para el relleno histórico

**Donde las opciones difieren:**

**Para La Opción A (Centrada En La Cuenta):**
Establezca el identificador principal en ID de cuenta. Agregar conjuntos de datos de registro de cuenta, oportunidad, grupo de compra y relación persona-cuenta. Configure conjuntos de datos de evento de nivel de persona con el campo ID de cuenta para la unión de conjuntos de datos cruzados.

**Para La Opción B (Global Account-Centric):**
Establezca el identificador principal en ID de cuenta global. Asegúrese de que los datos de jerarquía de cuentas incluyan el campo ID de cuenta global. Todos los conjuntos de datos deben incluir o estar unidos al ID de cuenta global para un resumen adecuado.

**Para Opción C (Híbrida):**
Cree una sola conexión con todos los conjuntos de datos B2B. Utilice ID de cuenta como identificador principal. La vista centrada en las personas se creará en la fase 2 mediante una configuración de vista de datos diferente en la misma conexión.

**Documentación de Experience League:**

- [Información general sobre Conexiones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Crear o editar una conexión](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Administrar conexiones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)
- [Información general sobre CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### Fase 2: Configuración de la vista de datos de cuenta

**Función de la aplicación:** [!DNL CJA] B2B: Configuración de vista de datos B2B, [!DNL CJA]: Configuración de vista de datos

Configure la vista de datos que define cómo aparecen los datos de conexión en el análisis. Para el análisis B2B, esto incluye la configuración de contenedores específicos B2B (cuenta, oportunidad, grupo de compra), la asignación de campos de esquema B2B a dimensiones y métricas, la configuración de modelos de atribución con ventanas retrospectivas apropiadas para B2B y la creación de campos derivados para la lógica empresarial B2B.

#### Decisión: configuración del contenedor

Determine qué contenedores B2B deben habilitarse y cómo deben asignarse.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Cuenta + Persona + Sesión + Evento | B2B estándar sin grupo de compra ni análisis de oportunidad | La jerarquía de contenedor B2B más sencilla. La cuenta es el contenedor de nivel superior. |
| Cuenta + Oportunidad + Persona + Sesión + Evento | Análisis de canalización e ingresos obligatorio | Agrega la oportunidad como nivel de contenedor, lo que permite un análisis con alcance de oportunidad. |
| Cuenta + Grupo de compra + Oportunidad + Persona + Sesión + Evento | Análisis B2B completo, incluida la composición del grupo comprador | El más completo. Permite el análisis en todos los niveles del modelo de datos B2B. |
| Cuenta Global + Cuenta + Persona + Sesión + Evento | Análisis de jerarquía de cuenta global | Agrega Cuenta global como el contenedor de nivel superior sobre Cuenta. |

#### Decisión: modelo de atribución para métricas B2B

Determine qué modelo de atribución debe ser el predeterminado para las métricas de conversión.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Atribución lineal (retrospectiva de 13 meses) | Igual crédito a todos los puntos de contacto del recorrido B2B | Lo mejor para comprender la combinación completa de actividades de marketing. Punto de partida recomendado para B2B. |
| Atribución en forma de U (retrospectiva de 13 meses) | Énfasis en el primer y último contacto con el crédito a los toques medios | Resalta los momentos de creación de posibles clientes y conversión de oportunidades. Frecuentes en el análisis de generación de demanda. |
| Deterioro de tiempo (retrospectiva de 13 meses) | Los puntos de contacto más recientes deben recibir más crédito | Lo mejor cuando la actualización de la participación es una señal importante para la preparación de las ventas. |
| Último contacto | Creación de informes sencillos del punto de contacto final antes de la conversión | Es fácil de entender, pero infravalora el marketing en las primeras etapas. Se utiliza únicamente para informes de funcionamiento rápidos. |

#### Decisión: Definición de la sesión para B2B

Determine cómo se deben definir las sesiones para la participación B2B.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Tiempo de espera de 30 minutos (predeterminado) | Comportamiento de sesión de análisis web estándar | Estándar para el análisis de participación web. Puede fragmentar sesiones de consumo de contenido largas. |
| Tiempo de espera ampliado (60 a 120 minutos) | Los usuarios de B2B participan en sesiones de investigación más largas | Los compradores de B2B suelen dedicar mucho tiempo a revisar el contenido técnico, los precios y la documentación. |
| Nueva sesión basada en eventos | Los eventos específicos siempre deben iniciar una nueva sesión | Se utiliza cuando las pulsaciones de campaña o las solicitudes de demostración siempre deben comenzar una nueva sesión analítica. |

#### Configuración de la vista de datos de cuenta

**Navegación de la interfaz de usuario:** [!DNL Customer Journey Analytics] > Vistas de datos > Crear nueva vista de datos

Detalles de configuración clave:

- Seleccione la conexión creada en Phase 1
- Configure la zona horaria y el tipo de calendario adecuados para la organización
- Cambie el nombre de los contenedores a la terminología relevante para B2B (por ejemplo, Cuenta/Participación/Punto de contacto)
- Asignar campos de esquema B2B a dimensiones: nombre de cuenta, ID de cuenta, sector, tamaño de empresa, nivel de cuenta, propietario de cuenta, fase de oportunidad, valor de oportunidad, función de grupo de compra, interés de solución
- Asignar métricas de participación: eventos (ocurrencias), personas, sesiones, vistas de página, envíos de formularios, aperturas de correo electrónico, clics en correos electrónicos
- Configure la persistencia para dimensiones clave (por ejemplo, el sector de cuentas persiste en el nivel de cuenta)
- Establezca la atribución en lineal con retrospectiva de 13 meses como predeterminada para las métricas de conversión
- Cree campos derivados para la clasificación del canal de marketing, los niveles de puntuación de participación y la agrupación de fases de oportunidad

**Donde las opciones difieren:**

**Para La Opción A (Centrada En La Cuenta):**
Configure una sola vista de datos con Account como contenedor de nivel superior. Incluya contenedores de oportunidad y de grupo de compra si es necesario realizar análisis de canalización y de grupo de compra.

**Para La Opción B (Global Account-Centric):**
Configure Cuenta global como el contenedor de nivel superior. Incluya la cuenta como subcontenedor para habilitar el análisis global y subsidiario.

**Para Opción C (Híbrida):**
Cree dos vistas de datos desde la misma conexión. La vista de datos 1 utiliza la persona como contenedor principal (comportamiento estándar de [!DNL CJA]). La vista de datos 2 utiliza Cuenta como contenedor principal con contenedores B2B. Asigne métricas idénticas a ambas vistas cuando corresponda.

**Documentación de Experience League:**

- [Resumen de vistas de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [Creación o edición de una vista de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Resumen de configuración de componentes](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configuración de persistencia](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configuración de atribución](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Campos derivados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [Configuración de sesión](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)

### Fase 3: Análisis de Workspace

**Función de aplicación:** [!DNL CJA] B2B: Análisis de Workspace a nivel de cuenta, Análisis de grupo de compra, Análisis de oportunidad, Segmentación B2B, Atribución B2B, [!DNL CJA]: Análisis de Workspace, Creación de métricas calculadas, Análisis guiado

Cree proyectos de Workspace que proporcionen perspectivas analíticas definidas en los KPI. Esta fase incluye la creación de tablas de forma libre con dimensiones y métricas B2B, la creación de métricas calculadas para KPI B2B, la configuración de visualizaciones específicas B2B (flujo de nivel de cuenta, funnel de oportunidades, compra de participación de grupo), la creación de filtros/segmentos mediante contenedores B2B y la aplicación de modelos de atribución B2B.

#### Decisión: estructura de Analysis Workspace

Determine cómo se debe organizar el proyecto de Workspace.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Un solo proyecto completo con varios paneles | Equipo pequeño, todas las partes interesadas ven los mismos informes | Es más fácil de mantener. Utilice los paneles para separar los temas (participación, canalización, atribución). Hasta 40 paneles por proyecto. |
| Varios proyectos centrados por audiencia | Las distintas partes interesadas necesitan puntos de vista diferentes | El marketing obtiene participación/atribución. Las ventas obtienen el estado de la canalización/cuenta. Las operaciones obtienen calidad de datos. Más mantenimiento, pero mejor segmentado. |
| Proyectos basados en plantillas con análisis guiado | Análisis de autoservicio para usuarios no expertos | Utilice análisis guiados para funnel y vistas de tendencias. Guardar como plantillas para análisis repetibles. Lo mejor para una amplia adopción. |

#### Decisión: métricas calculadas B2B

Determine qué métricas calculadas son necesarias para los KPI B2B.

| Métrica | Fórmula | Cuándo se crea |
| --- | --- | --- |
| Tasa de participación de cuenta | (Total de eventos de cuenta/Total de cuentas) | Siempre: métrica principal B2B |
| Porcentaje de integridad del grupo de compra | (Funciones completadas/Funciones requeridas) * 100 | Al comprar, el análisis de grupo está en el ámbito |
| Conversión de cuenta a oportunidad | Cuentas con oportunidades/cuentas comprometidas | Cuando se necesita el análisis de canalización |
| Porcentaje de influencia de canalización | Valor de canalización influenciado / Valor de canalización total | Cuando se requiere la atribución de marketing |
| Promedio de participación por contacto | Eventos / Personas únicas por cuenta | Cuando se necesita un análisis de penetración de cuenta |
| Participación de contenido por función | Eventos filtrados por la función de grupo de compra | Cuando se necesita la optimización de contenido para B2B |

#### Decisión: ámbito del segmento/filtro B2B

Determine en qué nivel de contenedor deben crearse los filtros.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Filtros de nivel de cuenta | Análisis con ámbito de cuentas que coinciden con criterios (por ejemplo, cuentas empresariales, sectores específicos) | Incluye todos los eventos de cuentas que cumplen los requisitos. El más común para B2B. |
| Filtros de nivel de oportunidad | Análisis con alcance para tipos o etapas de oportunidad específicos | Incluye todos los eventos asociados con las oportunidades de calificación. |
| Compra de filtros de nivel de grupo | Análisis con alcance de estados específicos de grupos de compra | Incluye eventos de personas de grupos compradores aptos. |
| Filtros de nivel de persona | Análisis con ámbito de individuos que coinciden con los criterios (por ejemplo, funciones específicas, títulos) | Comportamiento de filtro estándar. Se utiliza al analizar la participación individual en el contexto B2B. |

#### Creación del análisis de Workspace

**Navegación de la interfaz de usuario:** [!DNL Customer Journey Analytics] > Workspace > Proyectos > Crear proyecto

Detalles de configuración clave:

- Seleccione la vista de datos B2B creada en la fase 2
- Cree tablas improvisadas con dimensiones de nivel de cuenta (nombre de cuenta, sector, nivel) desglosadas por métricas de participación
- Crear visualizaciones de funnel de oportunidades que muestren la progresión de las oportunidades por fases
- Crear tablas de composición de grupos de compra que muestren las tasas de relleno de rol y la participación por rol.
- Configurar paneles de atribución B2B comparando modelos de atribución (lineal, en forma de U, decadencia temporal) con retrospectiva de 13 meses
- Crear visualizaciones de flujo de cuenta que muestren rutas comunes a través del recorrido de compra
- Creación de tablas de cohorte que analicen la retención y la reparticipación de la cuenta a lo largo del tiempo
- Aplique filtros B2B al análisis de segmentos por nivel de cuenta, sector o nivel de participación
- Cree anotaciones para eventos significativos (lanzamientos de campañas, versiones de productos, cambios de precios)

**Documentación de Experience League:**

- [Información general de Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Crear un proyecto](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabla de forma libre](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Panel de atribución](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Visualización de flujo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualización de abandonos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabla de cohortes](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Resumen de filtros](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Resumen de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Creación de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Resumen de anotaciones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [Resumen del análisis guiado](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Dimensiones de desglose](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

### Fase 4: Publicación del panel

**Función de la aplicación:** [!DNL CJA]: Publicación de tableros y cuadros de resultados, [!DNL CJA]: Publicación de audiencias

Cree paneles y cuadros de resultados móviles que se puedan compartir y que proporcionen perspectivas de análisis B2B a las partes interesadas. Esta fase también cubre la publicación de audiencias B2B definidas por [!DNL CJA] en AEP para su activación en casos de uso descendentes, como la activación de audiencias B2B.

#### Decisión: método de envío del panel

Determine cómo deben entregarse las perspectivas de análisis B2B a las partes interesadas.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Proyecto de Workspace (escritorio) | Analistas y operaciones de marketing que necesitan exploración interactiva | Interactividad completa, desglose, alternancia de filtros. Requiere acceso de [!DNL CJA]. |
| Cuadro de resultados móvil | Ejecutivos y líderes de ventas que necesitan KPI de un vistazo | Números de resumen con líneas de tendencia. Se puede acceder a través de la aplicación de paneles [!DNL Adobe Analytics]. Interactividad limitada. |
| Exportación programada de PDF/CSV | Partes interesadas sin acceso de [!DNL CJA] que necesitan actualizaciones regulares | Entrega automatizada según lo programado. No hay interactividad. Ideal para resúmenes ejecutivos semanales/mensuales. |
| Todo lo anterior | Grandes organizaciones con diversas necesidades para las partes interesadas | Alcance máximo. Mayor mantenimiento. Recomendado para programas de análisis B2B consolidados. |

#### Decisión: publicación de audiencia de [!DNL CJA]

Determine si los segmentos B2B deben volver a publicarse en AEP para su activación.

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Publicación de audiencias basadas en cuentas | Las perspectivas de Analytics deben informar sobre la segmentación y la supresión | Habilita la activación de [!DNL CJA] segmentos definidos por el usuario (por ejemplo, &quot;cuentas altamente comprometidas sin oportunidades abiertas&quot;) mediante [!DNL RT-CDP]. Actualizar cadencia: de 4 horas a semanalmente. |
| No publicar | Analytics es solo para informes, no para activación | Configuración más sencilla. La activación se administra por separado en [!DNL RT-CDP]. |

#### Publicación de paneles y audiencias

**Navegación de la interfaz de usuario:** [!DNL Customer Journey Analytics] > Proyectos > Compartir (para Workspace), Proyectos > Crear > Cuadro de resultados móvil (para cuadros de resultados), Componentes > Audiencias > Publicar (para publicación de audiencias)

Detalles de configuración clave:

- Cree paneles ejecutivos con números de resumen para los KPI clave B2B (cuentas comprometidas totales, valor de la canalización, integridad del grupo de compra)
- Configurar periodos de comparación (mes tras mes, trimestre tras trimestre) para indicadores de tendencia
- Cree cuadros de resultados móviles con mosaicos para las métricas de participación de la cuenta, estado de la canalización y atribución
- Agregue filtros para que los ejecutivos cambien de vista por región, sector o nivel de cuenta
- Configurar la entrega programada del proyecto para los informes ejecutivos semanales
- Para la publicación de audiencias: seleccione el filtro B2B, configure el área de nombres de identidad (ID de cuenta) y establezca la cadencia de actualización

**Documentación de Experience League:**

- [Creación de un cuadro de resultados móvil](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Uso compartido de proyectos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Programar proyectos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Configurar y depurar informes de valoración](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Paneles de Adobe Analytics: guía ejecutiva](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [Resumen de audiencias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Crear y publicar públicos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)

## Consideraciones sobre la implementación

Las secciones siguientes abarcan protecciones, escollos comunes, prácticas recomendadas y decisiones de compensación que se deben tener en cuenta durante la implementación.

### Protecciones y límites

- [!DNL CJA] conexiones pueden incluir conjuntos de datos de una sola zona protegida de AEP: [protecciones de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)
- Máximo de 5000 dimensiones y 5000 métricas por vista de datos
- Máximo de 100 campos derivados por vista de datos
- La atribución B2B admite ventanas retrospectivas de hasta 13 meses para análisis de nivel de cuenta
- Máximo de 75 audiencias publicadas por [!DNL CJA] cliente en todas las zonas protegidas
- La cadencia mínima de actualización de publicación de audiencia es cada 4 horas
- La latencia de streaming de AEP a [!DNL CJA] suele ser inferior a 90 minutos
- Las tablas de forma libre admiten hasta 10 desgloses de dimensión profundos
- Los cuadros de resultados móviles admiten hasta 16 mosaicos por cuadro de resultados
- Los proyectos de Workspace admiten hasta 40 paneles por proyecto
- El relleno para conjuntos de datos B2B grandes (miles de millones de registros) puede tardar días en completarse

### Peligros comunes

- **Asignación incompleta de persona a cuenta:** Si los eventos de nivel de persona no se pueden asociar con una cuenta, no aparecerán en el análisis de nivel de cuenta. Asegúrese de que todos los conjuntos de datos de evento incluyan un campo que se pueda unir al ID de cuenta, ya sea directamente o a través de un conjunto de datos de búsqueda de relación persona-cuenta. Audite el porcentaje de eventos con asociación de cuenta faltante antes de generar el análisis.
- **Designación de tipo de conjunto de datos incorrecta:** Los conjuntos de datos de búsqueda B2B (oportunidad, grupo de compra, relaciones persona-cuenta) deben designarse correctamente como tipo de búsqueda o perfil en la conexión [!DNL CJA]. Escribir incorrectamente un conjunto de datos de búsqueda como un conjunto de datos de evento producirá resultados incorrectos porque [!DNL CJA] intentará tratar cada registro como un evento con marca de tiempo.
- **Ventana de atribución demasiado corta para B2B:** Si utiliza ventanas de atribución de 30 días predeterminadas, se perderán puntos de contacto de la etapa inicial en recorridos B2B que normalmente abarcan de 6 a 18 meses. Configure siempre ventanas retrospectivas de 13 meses para métricas de atribución B2B.
- **Combinar incorrectamente las métricas de nivel de cuenta y de nivel de persona:** El recuento de &quot;personas&quot; en un análisis de nivel de cuenta puede ser engañoso. Asegúrese de que las métricas calculadas se definen en el nivel de contenedor adecuado. Una &quot;tasa de participación en la cuenta&quot; debe utilizar eventos de nivel de cuenta divididos por cuentas, no por personas.
- **Datos de grupo de compra obsoletos:** La composición del grupo de compra y las asignaciones de roles cambian con el tiempo. Si los conjuntos de datos del grupo de compra no se actualizan con regularidad, las métricas de integridad serán inexactas. Asegúrese de que el sistema de origen ([!DNL Marketo Engage] o [!DNL AJO] B2B edition) sincronice activamente los datos del grupo de compra.
- **Sobrecarga de un solo proyecto del espacio de trabajo:** el análisis B2B abarca la participación, la canalización, la atribución y la compra de grupos. Si se intenta colocar todo en un proyecto, la carga es lenta y la navegación, confusa. Utilice varios proyectos centrados o paneles claramente etiquetados.

### Prácticas recomendadas

- Comience con la Opción A (Centrada en la cuenta) incluso si planea utilizar la Opción B (Cuenta global) más adelante. El análisis centrado en cuentas es más sencillo y valida el modelo de datos antes de añadir complejidad a la jerarquía.
- Cree un proyecto de espacio de trabajo dedicado &quot;Calidad de datos B2B&quot; que realice un seguimiento del porcentaje de eventos con asociación de cuenta, el número de cuentas huérfanas y las métricas de integridad de grupos compradores. Ejecute esto semanalmente para detectar problemas de datos antes de tiempo.
- Utilice campos derivados para crear niveles de puntuación de participación (alta/Medium/baja) basados en recuentos de eventos de nivel de cuenta. Esto simplifica el análisis y hace que los paneles sean más procesables para las partes interesadas no técnicas.
- Al configurar la atribución B2B, comience con la atribución lineal como línea de base y, a continuación, compárela con los modelos en forma de U y en decadencia de tiempo. Las diferencias entre modelos a menudo revelan si la combinación de marketing se orienta hacia actividades de sensibilización o conversión.
- Publique un cuadro de resultados móvil de &quot;Resumen ejecutivo B2B&quot; con no más de 8 mosaicos que cubran los KPI que más importan al liderazgo. Manténgalo enfocado: los cuadros de resultados ejecutivos deben responder &quot;¿Cómo lo estamos haciendo?&quot; no &quot;¿Por qué?&quot;
- Anote eventos clave (lanzamientos de productos, lanzamientos de campañas principales, cambios de precios y cambios en los procesos de ventas) para proporcionar un contexto para las tendencias de datos. Los datos B2B suelen mostrar picos y caídas inexplicables sin contexto de evento.
- Al publicar audiencias B2B desde [!DNL CJA], utilice la actualización diaria para segmentos de activación estándar y la actualización de 4 horas solo para segmentos con distinción de tiempo. Las actualizaciones frecuentes consumen recursos de procesamiento.

### Decisiones de compensación

>[!NOTE]
>Las siguientes decisiones de compensación deben evaluarse en función de los requisitos y restricciones específicos de su organización.

**Complejidad de datos vs. precisión analítica**

La inclusión de todos los eventos de nivel de persona en el análisis de cuentas (incluso los que tienen una asociación de cuentas débil) mejora la integridad de los datos, pero puede reducir la precisión analítica si la asignación de cuentas no es fiable.

- **Incluyendo todos los favores de eventos:** Medición de participación integral, puntuaciones de participación de cuenta más altas, mayor visibilidad
- **Excluir eventos no coincidentes favorece:** Métricas precisas a nivel de cuenta, atribución confiable y correlación de canalización confiable
- **Recomendación:** Excluya los eventos no coincidentes del análisis de nivel de cuenta, pero inclúyalos en una vista de datos de nivel de persona independiente (Opción C) para entender el panorama completo. Priorice la mejora de la calidad de datos de asociación de cuentas como flujo de trabajo paralelo.

**Longitud de ventana retrospectiva de atribución B2B**

Las ventanas retrospectivas más largas (13 meses) capturan más puntos de contacto, pero pueden incluir actividades de marketing que ya no son relevantes para la decisión de compra actual.

- **Favoritos de retrospectiva más largos (13 meses):** Capturar el recorrido B2B completo, acreditar las actividades de la fase de sensibilización y dar cabida a ciclos de ventas largos.
- **Favoritos de retrospectiva más cortos (6 meses):** Se centra en la participación reciente, reduce el ruido de los puntos de contacto antiguos y refleja mejor la intención de compra actual.
- **Recomendación:** Use retrospectiva de 13 meses para cuentas empresariales con ciclos de ventas largos (más de 12 meses). Utilice una ventana retrospectiva de 6 meses para cuentas de mercado medio con ciclos más cortos. Cree métricas calculadas independientes para cada ventana con el fin de compararlas.

**Vista de datos integral única vs. múltiples vistas de datos enfocadas**

El mantenimiento de una vista de datos con todos los contenedores y dimensiones B2B es más sencillo, pero puede saturar a los analistas con complejidad. Las vistas de datos centradas múltiples (participación, canalización, atribución) son más fáciles de usar, pero más difíciles de mantener.

- **Una sola vista favorece:** Coherencia, mantenimiento más sencillo, análisis entre dominios dentro de un solo proyecto
- **Favoritos de varias vistas:** Simplicidad para los analistas, tiempos de carga más rápidos, listas de componentes personalizadas por caso de uso
- **Recomendación:** Comience con una sola vista de datos completa. Si los analistas informan de dificultades para encontrar las dimensiones y métricas adecuadas, cree grupos de componentes depurados dentro de la misma vista antes de dividirlos en varias vistas. Utilice plantillas de Workspace para guiar a los analistas hacia los componentes adecuados.

## Documentación relacionada

Los siguientes recursos proporcionan información adicional para implementar este patrón de caso de uso.

**[!DNL CJA]B2B edition**

- [Información general sobre CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [protecciones de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)

**Conexiones**

- [Información general sobre Conexiones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Crear o editar una conexión](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Administrar conexiones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)

**Vistas de datos**

- [Resumen de vistas de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [Creación o edición de una vista de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Resumen de configuración de componentes](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configuración de persistencia](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configuración de atribución](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Configuración de formato](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Campos derivados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [Configuración de sesión](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)

**Workspace y análisis**

- [Información general de Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Crear un proyecto](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabla de forma libre](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Visualización de flujo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualización de abandonos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabla de cohortes](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Panel de atribución](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Uso compartido de proyectos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Programar proyectos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Dimensiones de desglose](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

**Componentes**

- [Resumen de filtros](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Creación de filtros](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Resumen de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Creación de métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Resumen de anotaciones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [Intervalos de fechas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

**Audiencias**

- [Resumen de audiencias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Crear y publicar públicos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
- [Administrar audiencias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/manage)

**Paneles y cuadros de resultados**

- [Creación de un cuadro de resultados móvil](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Configurar y depurar informes de valoración](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Paneles de Adobe Analytics: guía ejecutiva](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)

**Análisis guiado**

- [Resumen del análisis guiado](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Vista de funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Vista de tendencias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Vista Retención](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

**[!DNL RT-CDP]B2B edition**

- [Información general sobre RT-CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#702702)
- [Esquemas de B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Resumen de fuentes B2B](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/sources/b2b)

**AEP data foundation**

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Resumen de orígenes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Conector de Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Información general de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home)

**Gobernanza de datos y ciclo vital**

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

**Tutoriales y guías**

- [Conceptos básicos de composición](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
