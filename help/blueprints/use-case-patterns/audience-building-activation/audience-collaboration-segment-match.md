---
title: Audience Collaboration
description: Aprenda a compartir y hacer coincidir segmentos de audiencia en entornos limitados u organizaciones mediante Coincidencia de segmentos.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: 7014849c-5e32-4ec3-a531-c0e8ce896f44
source-git-commit: 27f7e230982807ec70ca96af7f737944a6588f27
workflow-type: tm+mt
source-wordcount: '6232'
ht-degree: 1%

---

# Audience Collaboration

Esta guía proporciona una referencia de implementación completa para la colaboración entre audiencias usando [!DNL Segment Match] en [!DNL Real-Time CDP] y [!DNL Adobe Experience Platform]. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten compartir y hacer coincidir segmentos de audiencia en entornos limitados u organizaciones de forma segura para la privacidad.

Utilice este plan para comprender los enfoques disponibles, evaluar las compensaciones y navegar por [!DNL Adobe Experience League] para obtener instrucciones de configuración detalladas.

[!DNL Segment Match] permite que dos o más organizaciones de [!DNL Experience Platform] (o zonas protegidas dentro de una organización) colaboren en los datos de audiencia compartiendo información de pertenencia a segmentos sin exponer la PII subyacente. Los participantes pueden estimar la superposición, compartir audiencias y activar perfiles coincidentes en destinos descendentes.

## Resumen del caso de uso

Las organizaciones necesitan cada vez más colaborar en los datos de audiencia con socios, filiales o entre unidades de negocio, al tiempo que mantienen estrictos controles de privacidad. La colaboración entre audiencias resuelve esta necesidad habilitando el uso compartido seguro de segmentos a través de [!DNL Segment Match], una característica de [!DNL Real-Time CDP] que permite a dos o más organizaciones de [!DNL Experience Platform] (o zonas protegidas) intercambiar información de pertenencia a audiencias mediante identificadores hash seguros para la privacidad.

El escenario empresarial suele incluir una organización (el remitente) que ha creado un segmento de audiencia valioso y desea compartirlo con una organización asociada (el receptor) para la segmentación, supresión o enriquecimiento conjuntos. Antes de compartir, ambas partes pueden estimar la superposición de audiencias para evaluar el valor. Una vez compartida, la organización receptora puede activar la audiencia coincidente a través de sus propios destinos.

Este patrón es distinto de la activación de audiencia estándar porque funciona entre organizaciones o zonas protegidas en lugar de con destinos de marketing o publicidad externos. También es distinto de las salas limpias de datos o las plataformas de colaboración de terceros, ya que funciona de forma nativa dentro del ecosistema de Adobe mediante la infraestructura de identidad [!DNL Experience Platform].

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Adquisición de nuevos clientes

Amplíe la base de clientes con campañas de adquisición dirigidas, audiencias similares y optimización de medios de pago. La colaboración de audiencias permite a las organizaciones descubrir nuevos grupos de clientes potenciales comparando sus segmentos con las audiencias de los socios, identificando superposiciones de alto valor y llegando a clientes nuevos mediante la activación conjunta.

- **KPI:** nuevos clientes, coste de adquisición del cliente, conversión de cliente potencial/posible cliente
- [Adquisición de nuevos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Reducción del coste de adquisición del cliente

Mejore la eficacia de la segmentación, elimine a los clientes existentes de las campañas de adquisición y optimice el gasto en medios. Al compartir segmentos de supresión entre organizaciones o unidades de negocio, los equipos pueden evitar el gasto desperdiciado en clientes ya convertidos y centrar los presupuestos en perspectivas realmente nuevas.

- **KPI:** coste de adquisición del cliente, coste por posible cliente, eficiencia
- [Reducción del coste de adquisición del cliente](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### Optimización del gasto y el ROI de marketing

Mejore el retorno de la inversión en marketing mediante una mejor segmentación, atribución, supresión de audiencias y asignación de presupuesto. [!DNL Segment Match] permite la supresión de audiencias entre organizaciones y la segmentación conjunta, lo que reduce la duplicación y mejora la precisión.

- **KPI:** ahorros en costos, costo de adquisición de clientes, ingresos incrementales
- [Optimización del gasto y el ROI de marketing](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## Casos de uso tácticos de ejemplo

- **Coincidencia de audiencia de publicador-anunciante**: una marca comparte su segmento de cliente de alto valor con un publicador de medios para estimar la superposición y dirigirse a los usuarios coincidentes con anuncios personalizados, lo que mejora la relevancia de la campaña sin exponer la PII.
- **Supresión entre marcas dentro de una compañía matriz**: varias marcas bajo una organización principal comparten segmentos de clientes para suprimir a los clientes existentes de marcas hermanas de las campañas de adquisición, lo que reduce el gasto desperdiciado en publicidad.
- **Enriquecimiento de la audiencia de la red de medios comerciales**: Un retailer comparte segmentos basados en compras con socios de marcas CPG, lo que permite que las marcas se dirijan a compradores probados en la red de medios de retailer con tasas de conversión más altas.
- **Descubrimiento de audiencias de socios de marketing conjunto**: dos marcas que no compiten evalúan la superposición de audiencias para evaluar el potencial de asociación antes de lanzar una campaña conjunta, utilizando una estimación de superposición para validar la alineación de audiencia.
- **Uso compartido de segmentos de la cooperativa de datos**: las organizaciones en una cooperativa de datos comparten segmentos de audiencia con hash para expandir el alcance de segmentación mientras mantienen el cumplimiento de la privacidad y los controles de gobernanza de datos.
- **Federación de audiencias de zonas protegidas múltiples**: una empresa global comparte segmentos de audiencia en zonas protegidas regionales para permitir una segmentación de clientes coherente en todos los mercados, respetando al mismo tiempo los requisitos de residencia de datos regionales.
- **Activación de socios cruzados del programa de fidelización**: una coalición de fidelidad comparte segmentos de nivel de fidelidad con comerciantes participantes para que cada socio pueda ofrecer promociones apropiadas para el nivel a la base de clientes compartidos.
- **Colaboración de medición y atribución**: Un anunciante comparte un segmento de conversión con un socio de medios para que pueda medir la eficacia de la campaña comparando usuarios expuestos con convertidores.

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir el éxito de las implementaciones de colaboración de audiencia.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Tasa de superposición de audiencia | Porcentaje de perfiles en el segmento compartido que coinciden entre remitente y destinatario | [!DNL Segment Match] informe de estimación de superposición |
| Tamaño de audiencia coincidente | Número de perfiles coincidentes correctamente y disponibles para la activación | [!DNL Segment Match] estado de uso compartido y recuento de población de audiencia |
| Nueva adquisición de cliente de audiencias coincidentes | Nuevos clientes netos adquiridos mediante campañas dirigidas a segmentos coincidentes | Seguimiento de conversión en campañas que utilizan audiencias coincidentes |
| Reducción de costes de adquisición de clientes | Disminución del coste por adquisición al usar audiencias coincidentes frente a una segmentación amplia | Análisis de costes de Campaign comparando el rendimiento de audiencia coincidente con el incomparable |
| Ahorros por supresión | Gasto en medios ahorrado al eliminar clientes conocidos de las campañas de adquisición | Comparación del gasto en medios antes y después de la supresión |
| Alza de rendimiento de Campaign | Mejora en la tasa de conversión, la tasa de pulsaciones o la participación para campañas que utilizan audiencias coincidentes | Prueba A/B que compara campañas de audiencia coincidentes con control |
| Tiempo para Collaboration | Tiempo transcurrido desde el inicio del uso compartido de segmentos hasta la preparación para la activación | [!DNL Segment Match] marcas de tiempo de flujo |

## Patrón de caso de uso

Este caso de uso sigue el patrón de Audience Collaboration.

Comparta y combine segmentos de audiencia en zonas protegidas u organizaciones mediante [!DNL Segment Match].

**Cadena de funciones:** Selección de segmentos > Configuración de coincidencias > Estimación de superposición > Uso compartido de audiencias > Activación

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones.

- **[!DNL Real-Time CDP]**: proporciona la capacidad [!DNL Segment Match] para el uso compartido de audiencias con seguridad de privacidad, la evaluación de audiencias para la creación de segmentos y la activación de destino para el uso posterior de audiencias coincidentes.
- **[!DNL Adobe Experience Platform]**: proporciona la infraestructura de datos básica, incluida la resolución de identidades, la unificación de perfiles, el control de datos y la aplicación del consentimiento de la que depende [!DNL Segment Match].

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Requerido | Las organizaciones de remitente y destinatario deben tener zonas protegidas aprovisionadas con las funciones y los permisos adecuados. Los usuarios que administran [!DNL Segment Match] deben tener permisos para ver y compartir segmentos, configurar conexiones y administrar fuentes de socios. Las políticas ABAC deben configurarse para controlar qué usuarios pueden iniciar y aceptar acciones de segmentos. | [Resumen de control de acceso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Se asume en contexto | Los esquemas XDM para perfiles y eventos deben existir con los grupos de campos requeridos. Los conjuntos de datos de perfil y evento deben crearse y habilitarse para [!DNL Real-Time Customer Profile]. El modelo de datos debe admitir las áreas de nombres de identidad utilizadas para la coincidencia de segmentos (normalmente correo electrónico con hash o teléfono con hash). | [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home) |
| Fuentes de datos y recopilación | Se asume en contexto | Los datos del cliente deben fluir activamente a [!DNL Experience Platform] a través de las fuentes de datos configuradas (SDK, conectores de origen, ingesta por lotes). Los perfiles deben rellenarse con los tipos de identidad utilizados para [!DNL Segment Match] (por ejemplo, correo electrónico con hash). | [Resumen de orígenes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| Configuración de identidad y perfil | Requerido | Las áreas de nombres de identidad deben configurarse para los identificadores utilizados en la coincidencia de segmentos. Tanto el remitente como el receptor deben utilizar áreas de nombres de identidad compatibles. Las políticas de combinación deben configurarse para unificar los perfiles correctamente. Deben establecerse reglas de vinculación de identidad para garantizar una resolución precisa del perfil. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home) |
| Definición de audiencia y segmentación | Requerido | Las audiencias de Source deben definirse y evaluarse antes de poder compartirse mediante [!DNL Segment Match]. Las audiencias deben generarse usando [!DNL Segment Builder] o [!DNL Audience Composition] con la evaluación por lotes completada. Solo las audiencias evaluadas por lotes pueden compartir [!DNL Segment Match]. | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Los atributos calculados, como el valor de compra de por vida, la puntuación de participación o la afinidad del producto, pueden crear segmentos más precisos para compartir. Los segmentos de entrada de mayor calidad generan una colaboración de audiencia más valiosa. | [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Administración del ciclo de datos | Recomendado | Las políticas de consentimiento y retención de datos garantizan que los segmentos compartidos cumplan con las normas de privacidad. Las políticas de caducidad del conjunto de datos ayudan a administrar el ciclo vital de los datos de audiencia recibidos. La aplicación del consentimiento impide compartir los perfiles que han optado por la exclusión. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-lifecycle/home) |
| Etiquetado y aplicación del uso de datos | Incluido | Las políticas de gobernanza de datos deben evaluarse antes de compartir segmentos para garantizar el cumplimiento. Las etiquetas en los campos de identidad y los atributos de perfil determinan lo que se puede compartir. La aplicación de la gobernanza evita que se incluyan datos no autorizados en los recursos compartidos de segmentos. | [Resumen de control de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home) |
| Monitorización y observabilidad | Recomendado | La supervisión del proceso de uso compartido de [!DNL Segment Match], los trabajos de estimación de superposición y los flujos de datos de activación ayuda a detectar errores de forma temprana. Las alertas se pueden configurar para errores de uso compartido o tasas de coincidencia inesperadamente bajas. | [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Informes y análisis | Recomendado | La medición del rendimiento de las campañas que utilizan audiencias coincidentes valida el valor de la colaboración. [!DNL Customer Journey Analytics] analysis puede comparar el rendimiento de audience campaign con los grupos de control. | [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Real-Time CDP]

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Evaluación de audiencia | Fase 1: Selección y preparación de segmentos | Evaluar el abono a segmentos mediante la evaluación por lotes para producir las audiencias que se compartirán a través de [!DNL Segment Match] |
| Composición de audiencia | Fase 1: Selección y preparación de segmentos | Opcionalmente, puede componer audiencias derivadas (clasificar, dividir, excluir, enriquecer) para crear segmentos más segmentados para compartir |
| Cumplimiento del consentimiento y la gobernanza | Fase 2: Configuración y control de coincidencias | Haga cumplir las políticas de uso de datos y las preferencias de consentimiento antes de compartir segmentos para garantizar el cumplimiento |
| Audience Activation | Fase 5: Audience Activation coincidente | Publicar audiencias coincidentes recibidas a través de [!DNL Segment Match] en destinos externos para segmentación o supresión |
| Configuración de destino | Fase 5: Audience Activation coincidente | Configure conexiones a destinos externos donde se activarán las audiencias coincidentes |

## Prerrequisitos

- Tanto las organizaciones de remitente como las de destinatario tienen [!DNL Real-Time CDP] aprovisionado con el derecho [!DNL Segment Match]
- [!DNL Segment Match] está habilitado para las organizaciones o zonas protegidas que participan en la colaboración
- Se ha establecido una conexión de socio entre las organizaciones remitente y receptor en la interfaz de usuario de [!DNL Segment Match]
- Ambas organizaciones utilizan áreas de nombres de identidad compatibles (por ejemplo, ambas tienen configurado correo electrónico con hash)
- Las audiencias de Source se han definido y evaluado con poblaciones diferentes a cero
- Se configuran las políticas de gobernanza de datos y se aplican etiquetas de uso de datos a los conjuntos de datos y campos relevantes
- Los usuarios de ambos lados tienen los permisos necesarios para administrar [!DNL Segment Match] conexiones, recursos compartidos y fuentes
- Los campos de consentimiento se rellenan en perfiles para habilitar el filtrado basado en el consentimiento antes de compartir

## Opciones de implementación

Las siguientes opciones describen diferentes enfoques para implementar la colaboración de audiencias con [!DNL Segment Match]. Seleccione la opción que mejor se ajuste a la estructura organizativa y a los requisitos de colaboración.

### Opción A: uso compartido directo de segmentos (uno a uno)

Esta opción es mejor para asociaciones bilaterales entre dos organizaciones específicas, como un anunciante y un editor, o dos marcas en un acuerdo de marketing conjunto.

**Cómo funciona:**

En un recurso compartido de segmentos uno a uno directo, la organización remitente selecciona una o más audiencias evaluadas, inicia un recurso compartido con una organización asociada específica y el receptor acepta el recurso compartido. La estimación de superposición se ejecuta automáticamente para mostrar a ambas partes el porcentaje y el volumen de los perfiles coincidentes antes de que se finalice la acción.

El remitente define qué áreas de nombres de identidad se utilizarán para la coincidencia y selecciona los segmentos que se van a compartir. El receptor revisa el recurso compartido entrante, lo acepta y la audiencia coincidente está disponible en su lista de audiencias para la activación descendente. Solo se intercambia la superposición de identidades con hash: no hay PII subyacente ni datos de atributos de perfil que crucen los límites de la organización.

Este enfoque es sencillo y proporciona control total a ambas partes. El remitente elige exactamente qué compartir y con quién, y el receptor tiene la opción de aceptar o rechazar cada acción.

**Consideraciones clave:**

- Requiere la configuración de una conexión de socio explícita entre las dos organizaciones
- Ambas organizaciones deben acordar áreas de nombres de identidad para la coincidencia
- La estimación de superposición proporciona transparencia antes del compromiso
- Cada acción debe ser administrada y supervisada individualmente

**Ventajas:**

- Flujo de trabajo bilateral sencillo y bien entendido
- Transparencia total mediante estimación de superposición antes de compartir
- Control granular: el remitente elige exactamente qué segmentos compartir
- Seguridad para la privacidad: solo se utilizan identificadores hash para la coincidencia
- El receptor puede aceptar o rechazar acciones de forma selectiva

**Limitaciones:**

- No se escala de forma eficaz cuando se colabora con muchos socios simultáneamente
- Cada asociación requiere una configuración y administración de conexiones independientes
- La configuración de uso compartido debe repetirse para cada nuevo segmento

**Experience League:**

- [Resumen de coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Solución de problemas de Coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### Opción B: Distribución de segmentos de varios socios (uno a varios)

Esta opción es perfecta para las organizaciones que necesitan compartir segmentos con varios socios simultáneamente, como una red de medios minoristas que comparta segmentos basados en compras con varios anunciantes de marcas o una compañía que distribuya segmentos a marcas subsidiarias.

**Cómo funciona:**

En un modelo de distribución de uno a varios, la organización remitente establece [!DNL Segment Match] conexiones con varias organizaciones asociadas y comparte el mismo segmento o segmentos diferentes con cada una. El remitente administra un portafolio de conexiones de socios y puede compartir selectivamente diferentes segmentos de audiencia con diferentes socios en función de la relación y el caso de uso.

Cada conexión de socio funciona de forma independiente: la estimación de superposición, la aceptación de acciones y la activación se administran por socio. El remitente puede controlar qué segmentos recibe cada socio, lo que permite estrategias de colaboración diferenciadas (por ejemplo, los socios Premium reciben segmentos más granulares, los socios estándar reciben otros más amplios).

Este método utiliza el mismo mecanismo [!DNL Segment Match] subyacente que la opción A, pero lo aplica a escala con un marco operativo para administrar varias asociaciones simultáneas.

**Consideraciones clave:**

- Requiere procesos operativos sólidos para administrar varias asociaciones
- Las políticas de gobernanza deben tener en cuenta el hecho de compartir los mismos segmentos con varias partes externas
- Cada socio puede utilizar diferentes áreas de nombres de identidad, lo que requiere una configuración flexible
- Las tasas de superposición variarán según el socio, lo que requiere una evaluación por socio

**Ventajas:**

- Escala la colaboración de audiencias en un ecosistema de socios
- Estrategias de uso compartido diferenciadas por socio
- Administración centralizada de todos los segmentos salientes compartidos desde una organización
- Cada sociedad mantiene controles independientes de gobernanza y consentimiento

**Limitaciones:**

- La complejidad operativa aumenta con cada socio adicional
- La supervisión y la solución de problemas deben realizarse por socio
- Se requiere una revisión de administración para cada nueva conexión de socio
- Los socios no ven los datos de los demás ni comparten el estado

**Experience League:**

- [Resumen de coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)

### Opción C: federación de audiencias en zonas protegidas cruzadas

Esta opción es perfecta para las grandes empresas con varios entornos limitados de [!DNL Experience Platform] (por ejemplo, entornos limitados regionales, específicos de la marca o específicos del entorno) que necesitan compartir segmentos de audiencia entre límites internos sin mover datos sin procesar.

**Cómo funciona:**

En lugar de compartir entre organizaciones independientes, la federación de audiencias entre zonas protegidas utiliza [!DNL Segment Match] para compartir segmentos de audiencia entre zonas protegidas dentro de la misma organización. Esto permite a un equipo de marketing global crear un segmento en una zona protegida central y compartirlo con zonas protegidas regionales, o permite que las zonas protegidas específicas de la marca compartan listas de supresión entre sí.

El flujo de trabajo refleja el uso compartido directo de segmentos (Opción A), pero funciona dentro de los límites de la organización. Las conexiones de zona protegida a zona protegida se establecen a través de [!DNL Segment Match] y los segmentos se comparten utilizando el mismo proceso de coincidencia seguro para la privacidad. La zona protegida de recepción obtiene la audiencia coincidente como una nueva audiencia que se puede activar a través de sus propios destinos configurados localmente.

Este enfoque es especialmente valioso cuando los requisitos de residencia de datos impiden mover datos de clientes sin procesar entre regiones, pero se permite la colaboración a nivel de audiencia.

**Consideraciones clave:**

- Requiere el derecho de [!DNL Segment Match] que admite el uso compartido entre zonas protegidas
- Las áreas de nombres de identidad deben ser coherentes en todos los entornos limitados
- Las políticas de combinación en cada zona protegida pueden resolver los perfiles de forma diferente, lo que podría afectar a las tasas de coincidencia
- Las políticas de gobernanza se aplican de forma independiente por zona protegida

**Ventajas:**

- Habilita la colaboración entre audiencias sin mover datos sin procesar a través de los límites de la zona protegida
- Admite requisitos de residencia de datos y cumplimiento regional
- Aprovecha la infraestructura de identidad organizativa existente
- Revisión de la gobernanza más sencilla, ya que el uso compartido se produce dentro de la misma organización

**Limitaciones:**

- Requiere una configuración de área de nombres de identidad coherente en entornos limitados
- Las tasas de coincidencia dependen de la coherencia de las políticas de combinación entre zonas protegidas
- No aborda las necesidades de colaboración entre organizaciones
- Puede que se necesite Sandbox Tool para sincronizar el esquema y la configuración

**Experience League:**

- [Resumen de coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Información general de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home)

### Comparación de opciones

En la tabla siguiente se comparan las tres opciones de implementación en función de criterios clave.

| Criterios | Opción A: Uso Compartido Directo De Segmentos | Opción B: Distribución de varios socios | Opción C: Federación Entre Zonas Protegidas |
| --- | --- | --- | --- |
| Mejor para | Asociaciones bilaterales | Colaboración a escala ecosistémica | Uso compartido interno entre zonas protegidas |
| Complejidad | Baja | Alta | Medio |
| Número de socios | 1 | Muchos | Zonas protegidas internas |
| Gastos generales de gobernanza | Baja | Alto (revisión por socio) | Medium (dentro de la organización) |
| Gestión operativa | Sencilla | Requiere un marco de administración de socios | Moderar |
| Soporte de residencia de datos | N/A | Depende de la ubicación del socio | Fuerte |
| Requiere | Configuración de conexión de socio | Varias conexiones de socios | Zona protegida cruzada [!DNL Segment Match] |

### Elija la opción correcta

Utilice las siguientes directrices de decisión para seleccionar el método de implementación adecuado:

1. **¿Está colaborando con una organización externa o con su propia organización?**
   - Organización externa: pase a la pregunta 2.
   - Dentro de su propia organización (en entornos limitados): elija **Opción C** (Federación de entornos limitados).

2. **¿Con cuántos socios externos colaborará?**
   - Un socio: elija **Opción A** (uso compartido directo de segmentos).
   - Varios socios: elija **Opción B** (Distribución de varios socios).

3. **¿Tiene restricciones de residencia de datos que impiden mover datos sin procesar entre regiones?**
   - Sí: elija **Opción C** independientemente de si los socios son internos o externos: use el uso compartido entre zonas protegidas para mantener la ubicación de los datos.

## Fases de implementación

Las siguientes fases describen el proceso de implementación de extremo a extremo para la colaboración de audiencias con [!DNL Segment Match].

### Fase 1: Selección y preparación de segmentos

**Función de aplicación:** [!DNL Real-Time CDP]: Evaluación de audiencia, [!DNL Real-Time CDP]: Composición de audiencia

Esta fase implica definir y evaluar los segmentos de audiencia que se compartirán a través de [!DNL Segment Match]. Los segmentos de origen deben evaluarse completamente con poblaciones distintas de cero para poder seleccionarlos para compartir. Esta fase también cubre la composición opcional de audiencias para refinar los segmentos antes de compartirlos.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: enfoque de definición de audiencia**
>
>¿Cómo se deben crear las audiencias de origen para el uso compartido?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Generador de segmentos (reglas de segmentos) | Definiciones de audiencia estándar basadas en atributos de perfil, eventos o abono a segmentos. | Admite evaluación por lotes, flujo y perímetros; más flexible para definir criterios |
>| Composición de audiencia | Audiencias derivadas que requieren operaciones de clasificación, división, exclusión o enriquecimiento en segmentos existentes | Solo admite la evaluación por lotes; limitado a 10 lienzos de composición por zona protegida |
>| Composición de audiencia federada | Audiencias creadas a partir de consultas de Data Warehouse externas sin ingerir datos en [!DNL Experience Platform] | Requiere el derecho de [!DNL Federated Audience Composition]; los datos permanecen en el almacén |

>[!NOTE]
>
>**Decisión: método de evaluación de audiencia**
>
>[!DNL Segment Match] requiere audiencias evaluadas por lotes. ¿Cómo se debe programar la evaluación?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Lote programado (diario) | Casos de uso estándar en los que la actualización diaria de la audiencia es suficiente | Programación de evaluación predeterminada; más fácil de administrar |
>| Lote bajo demanda | El uso compartido ad hoc necesita un lugar en el que desee compartir la audiencia más actual inmediatamente | Requiere déclencheur manual; útil para colaboraciones en las que el tiempo es un factor importante |
>| Programación personalizada | Requisitos de temporización específicos alineados con las ventanas de activación de socios | Configurar una programación cron personalizada; más compleja pero precisa |

**Navegación de la interfaz de usuario:** Cliente > Audiencias > Crear audiencia > Generar regla (para [!DNL Segment Builder]) o Escribir audiencia (para [!DNL Audience Composition])

**Detalles de configuración de clave:**

- Defina criterios de audiencia mediante atributos de perfil, eventos de comportamiento o abono a segmentos
- Asegúrese de que la audiencia utiliza una política de combinación compatible con las áreas de nombres de identidad utilizadas para [!DNL Segment Match]
- Verificar que la población de audiencia no sea cero después de la evaluación
- Aplique reglas de supresión para excluir perfiles que no deban compartirse (por ejemplo, perfiles que hayan optado por no compartir datos)

**Donde las opciones difieren:**

**Para La Opción A (Uso Compartido Directo De Segmentos):**
Prepare los segmentos específicos que desea compartir con su socio único. Céntrese en la calidad sobre la cantidad: revise los segmentos que proporcionan un valor claro a la asociación.

**Para La Opción B (Distribución De Socios Múltiples):**
Prepare un portafolio de segmentos que puedan compartirse con diferentes socios. Considere la posibilidad de crear segmentos específicos de socio si distintos socios necesitan definiciones de audiencia diferentes. Utilice convenciones de nomenclatura coherentes para administrar segmentos entre asociaciones.

**Para La Opción C (Federación Entre Zonas Protegidas):**
Asegúrese de que las audiencias de origen de la zona protegida de envío utilicen áreas de nombres de identidad que existan en la zona protegida de recepción. Compruebe que las políticas de combinación están alineadas en los entornos limitados.

**Documentación de Experience League:**

- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Resumen de composición de audiencia](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Métodos de evaluación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home#evaluation-methods)
- [Referencia de Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Fase 2: Configuración de la coincidencia y el control

**Función de la aplicación:** [!DNL Real-Time CDP]: Aplicación del consentimiento y control

Esta fase establece la conexión [!DNL Segment Match] entre organizaciones o zonas protegidas, configura las áreas de nombres de identidad utilizadas para la coincidencia y garantiza que las directivas de gobernanza de datos permitan el uso compartido. La aplicación de la gobernanza actúa como una puerta de directiva que debe borrarse antes de compartir cualquier dato de segmento.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: área de nombres de identidad para la coincidencia**
>
>¿Qué área de nombres de identidad se utilizará para hacer coincidir perfiles entre remitente y destinatario?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Correo electrónico con hash (SHA-256) | Ambas organizaciones recopilan direcciones de correo electrónico y pueden hash de manera consistente | Clave de coincidencia más común; tasas de coincidencia elevadas para los casos de uso del consumidor; ambas partes deben utilizar el mismo algoritmo hash |
>| Número de teléfono con hash | El correo electrónico no siempre está disponible, pero los números de teléfono sí lo están | Menor cobertura que el correo electrónico en muchos mercados; útil para audiencias con prioridad móvil |
>| Área de nombres personalizada (por ejemplo, ID de lealtad con hash) | Las organizaciones comparten un ID de programa de fidelidad o pertenencia común | Tasas de coincidencia más altas para bases de clientes compartidos conocidas; requiere una infraestructura de ID compartido preexistente |
>| Varias áreas de nombres | La maximización de la tasa de coincidencia es crítica y ambas organizaciones tienen varios identificadores coherentes | Aumenta las tasas de coincidencia, pero añade complejidad; cada área de nombres debe configurarse de forma independiente |

>[!NOTE]
>
>**Decisión: revisión del control de datos**
>
>¿Qué comprobaciones de gobernanza deben completarse antes de compartir?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Evaluación de gobernanza estándar | Caso de uso típico con etiquetas y políticas de uso de datos estándar | Evaluar la acción de marketing &quot;Exportar a terceros&quot; con etiquetas de conjuntos de datos; resolver cualquier infracción antes de compartir |
>| Gobernanza mejorada con filtrado de consentimiento | Uso compartido con socios externos donde el consentimiento debe verificarse explícitamente | Añada el filtrado basado en el consentimiento para excluir perfiles sin compartir el consentimiento (por ejemplo, conents.share.val = &#39;n&#39;); más estricto pero seguro |
>| Revisión de la gobernanza interna | Uso compartido entre zonas protegidas dentro de la misma organización | Requisitos de gobernanza más ligeros, ya que los datos se mantienen dentro de los límites de la organización; compruebe las etiquetas de uso de datos |

**Navegación de la interfaz de usuario:** Cliente > Audiencias > Coincidencia de segmentos > Conexiones de socios

**Detalles de configuración de clave:**

- Establezca una conexión de socio intercambiando identificadores de conexión entre organizaciones de remitente y destinatario
- Configure las áreas de nombres de identidad que se utilizarán para la coincidencia en ambos lados
- Ejecute la evaluación de la política de gobernanza de datos con la acción de marketing asociada al uso compartido de segmentos
- Compruebe que los campos de consentimiento se rellenan en perfiles y que se excluyen los perfiles sin consentimiento compartido
- Revise las etiquetas de uso de datos en los conjuntos de datos y campos de esquema incluidos en el recurso compartido

**Donde las opciones difieren:**

**Para La Opción A (Uso Compartido Directo De Segmentos):**
Establezca una conexión de socio única. Configure áreas de nombres de identidad con su socio específico. La revisión de la gobernanza se centra en la relación bilateral.

**Para La Opción B (Distribución De Socios Múltiples):**
Establezca y administre varias conexiones de socios. Cada socio puede requerir una revisión de la gobernanza por separado. Documente la aprobación de gobernanza para cada asociación. Considere la posibilidad de crear una lista de comprobación de gobernanza para racionalizar la incorporación de los socios.

**Para La Opción C (Federación Entre Zonas Protegidas):**
Establezca conexiones de zona protegida a zona protegida dentro de la organización. La administración suele ser más sencilla, ya que el uso compartido se produce internamente. Asegúrese de que las áreas de nombres de identidad sean coherentes en todas las zonas protegidas.

**Documentación de Experience League:**

- [Resumen de coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Aplicación de políticas](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/enforcement/overview)
- [Consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

### Fase 3: Superposición estimada

**Función de aplicación:** [!DNL Real-Time CDP]: Evaluación de audiencia (para estimar la superposición)

Esta fase ejecuta la estimación de superposición entre los segmentos del remitente y la base de perfiles del receptor. La estimación de superposición proporciona a ambas partes el volumen de coincidencia y el porcentaje esperados antes de comprometerse con la cuota de segmento completa, lo que permite tomar decisiones informadas sobre el valor de la colaboración.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: umbral de superposición para continuar**
>
>¿Qué tasa mínima de superposición justifica continuar con la cuota de segmento completa?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Sin umbral mínimo | Asociaciones exploratorias o cuando cualquier superposición proporcione valor | Adecuado para colaboraciones iniciales en las que se prueba la relación |
>| Umbral bajo (1-5 %) | Colaboración de audiencia a gran escala en la que incluso una pequeña superposición representa un volumen significativo | Común para las relaciones de editor y anunciante con bases de audiencia grandes |
>| Umbral de Medium (5-20 %) | Asociaciones estándar en las que se espera una superposición significativa | Típico para colaboraciones de marketing conjunto o del mismo sector |
>| Umbral alto (20 %+) | Asociaciones en las que una fuerte alineación de audiencias es un requisito previo | Común para coaliciones de fidelidad o asociaciones de marca estrechamente integradas |

**Navegación de la interfaz de usuario:** Cliente > Audiencias > Coincidencia de segmentos > Recursos compartidos > Superposición de estimaciones

**Detalles de configuración de clave:**

- Seleccione los segmentos que desea incluir en la estimación de superposición
- Revise el informe de superposición que muestra el recuento y el porcentaje de perfiles coincidentes
- Comparta los resultados de la estimación de superposición con las partes interesadas de ambas partes para su aprobación
- Documente las métricas de superposición como línea de base para medir la eficacia de la colaboración
- Si la superposición está por debajo del umbral aceptable, considere la posibilidad de ajustar las definiciones de segmentos o la configuración de coincidencia de identidades antes de continuar

**Documentación de Experience League:**

- [Resumen de coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)

### Fase 4: Compartir audiencias

**Función de aplicación:** [!DNL Real-Time CDP]: Evaluación de audiencia (para ejecución de recurso compartido)

Esta fase ejecuta el uso compartido de segmentos real de remitente a receptor. El remitente inicia el recurso compartido para los segmentos seleccionados y el receptor acepta el recurso compartido entrante. Una vez aceptada, la audiencia coincidente aparece en la lista de audiencias del receptor como una nueva audiencia disponible para la activación descendente.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: Compartir dirección**
>
>¿Cuál es el modelo de uso compartido para esta colaboración?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Recurso compartido unidireccional (de remitente a receptor) | Asociación asimétrica en la que una sola parte proporciona datos de audiencia | Modelo más sencillo; el remitente comparte, el receptor activa; común en las relaciones anunciante-editor |
>| Uso compartido bidireccional | Ambas partes se benefician de compartir audiencias entre sí | Ambas organizaciones actúan como remitente y receptor simultáneamente; requiere dos configuraciones de uso compartido; comunes en las asociaciones de marketing conjunto |

>[!NOTE]
>
>**Decisión: compartir cadencia de actualización**
>
>¿Con qué frecuencia se debe actualizar la audiencia compartida con la inscripción a segmento actualizada?
>
>| Opción | When to choose | Considerations |
>| --- | --- | --- |
>| One-time share | Testing the collaboration or for a specific campaign with a fixed audience | Simplest; no ongoing maintenance; audience becomes stale over time |
>| Recurring share (aligned with batch evaluation) | Ongoing partnerships where audience membership changes and needs to be kept current | Requires monitoring of refresh status; most common for production collaborations |

**UI navigation:** Customer > Audiences > Segment Match > Shares > Create share (sender) or Accept share (receiver)

**Key configuration details:**

- Sender selects the segments to share and initiates the share with the configured partner
- Receiver reviews the incoming share details (segment names, estimated size, identity namespaces used)
- Receiver accepts the share to create the matched audience in their sandbox
- Verify the matched audience appears in the receiver&#39;s audience list with the expected population
- Confirm that the matched audience is labeled appropriately for governance tracking

**Where options diverge:**

**For Option A (Direct Segment Share):**
Execute a single share with your partner. Monitor the share status and verify the matched audience on the receiver side.

**For Option B (Multi-Partner Distribution):**
Execute shares for each partner independently. Track share status across all partnerships. Consider staggering share initiation to manage processing load.

**For Option C (Cross-Sandbox Federation):**
Execute the cross-sandbox share. The matched audience appears in the receiving sandbox&#39;s audience list. Verify that the receiving sandbox has the necessary destination configurations for downstream activation.

**Experience League documentation:**

- [Resumen de coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Solución de problemas de Coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### Fase 5: Activar audiencias coincidentes

**Función de aplicación:** [!DNL Real-Time CDP]: Configuración de destino, [!DNL Real-Time CDP]: Audience Activation

Esta fase activa la audiencia coincidente (en el lado del receptor) a destinos externos para el direccionamiento, la supresión o el uso descendente. La audiencia coincidente se trata como cualquier otra audiencia en la zona protegida del receptor y se puede activar a través del flujo de trabajo de activación de destino estándar.

**Puntos de decisión en esta fase:**

>[!NOTE]
>
>**Decisión: tipo de destino para la audiencia coincidente**
>
>¿Dónde se debe activar la audiencia coincidente?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Destinos de Advertising (Google, Meta, Trade Desk) | Uso de audiencias coincidentes para la segmentación o supresión de anuncios | Requiere conexión y autenticación de destino; sujeto a los límites de velocidad y requisitos de formato específicos del destino |
>| Destinos de almacenamiento en la nube (S3, Azure, GCS) | Exportación de audiencias coincidentes como archivos para su uso en sistemas externos | Admite la personalización del formato de archivo; se requiere programación de exportación por lotes; flexible para el procesamiento descendente |
>| Destinos de automatización de marketing/CRM | Enriquecimiento de registros CRM o activación de flujos de trabajo de marketing automatizados con datos de audiencia coincidentes | Requiere asignación de campos al esquema CRM; útil para la alineación de ventas y marketing |
>| Destinos de Personalization (web, aplicación) | Uso de pertenencia a audiencia coincidente para la personalización en el sitio | Requires edge evaluation of the matched audience or streaming activation; latency varies by destination |

>[!NOTE]
>
>**Decision: Activation schedule**
>
>How frequently should the matched audience be exported to the destination?
>
>| Option | When to choose | Considerations |
>| --- | --- | --- |
>| Daily incremental export | Standard activation with regular audience updates | Only exports changed profiles; lower data volume; most common for ongoing campaigns |
>| Daily full export | Destinations that require a complete audience file each time | Higher data volume; ensures destination has complete audience state; some destinations require full exports |
>| On-demand activation | Ad-hoc campaign launches or time-sensitive activations | Manual trigger; bypasses scheduled cadence; available for batch destinations only |

**UI navigation:** Connections > Destinations > Catalog (for destination setup) or Browse > Select destination > Activate audiences (for activation)

**Key configuration details:**

- Configure the destination connection with appropriate authentication credentials
- Map profile attributes from the matched audience to destination fields (identity fields, profile attributes, segment membership)
- Configure the export schedule (incremental vs. full, daily vs. custom)
- Monitor the activation dataflow to confirm matched audience profiles are exported successfully
- Verify activation metrics (profiles exported, records failed) in the destination monitoring view

**Where options diverge:**

**For Option A (Direct Segment Share):**
The receiver activates the matched audience through their standard destination workflow. No special configuration is needed beyond normal destination activation.

**Para La Opción B (Distribución De Socios Múltiples):**
Cada organización receptora activa audiencias coincidentes de forma independiente a través de sus propios destinos. El remitente no tiene visibilidad de la activación del lado del receptor.

**Para La Opción C (Federación Entre Zonas Protegidas):**
La zona protegida de recepción debe tener sus propias configuraciones de destino. Los destinos no se pueden compartir en entornos limitados. Asegúrese de que la zona protegida de recepción tenga establecidas las conexiones de destino necesarias.

**Documentación de Experience League:**

- [Información general sobre los destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Monitorización de flujos de datos para destinos](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Protecciones de activación](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

## Consideraciones sobre la implementación

Revise las siguientes consideraciones antes y durante la implementación para evitar problemas comunes y optimizar la colaboración entre audiencias.

### Protecciones y límites

- [!DNL Segment Match] utiliza identificadores hash para la coincidencia: ninguna PII cruza los límites de la organización. Consulte [Resumen de coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview).
- Solo se pueden compartir audiencias evaluadas por lotes a través de [!DNL Segment Match]. Los segmentos de streaming y evaluados por Edge deben convertirse a una evaluación por lotes antes de compartirse.
- Se aplica un máximo de 4000 definiciones de segmentos por zona protegida tanto a los segmentos de origen como a los recibidos. Consulte [protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails).
- La precisión de la estimación de superposición depende del volumen de identificadores coincidentes. Las audiencias pequeñas pueden mostrar estimaciones menos precisas.
- Las protecciones de activación se aplican a audiencias coincidentes igual que cualquier otra audiencia: un máximo de 100 flujos de datos por destino. Consulte [Protecciones de activación](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails).
- Las audiencias compuestas se evalúan según una programación por lotes y están limitadas a 10 lienzos de composición por zona protegida. Consulte [Protecciones de composición de audiencia](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails).

### Peligros comunes

- **Hash de identidad inconsistente entre el remitente y el destinatario:** Si ambas organizaciones usan direcciones de correo electrónico hash pero usan algoritmos de hash, reglas de normalización o valores Sal diferentes, las tasas de coincidencia se acercarán a cero. Ambas partes deben acordar la especificación exacta de hash (por ejemplo, SHA-256 en minúsculas, correo electrónico recortado) antes de establecer la conexión.
- **Compartir audiencias sin revisión de control:** Si se inicia un uso compartido de segmentos sin evaluar las directivas de uso de datos, se pueden producir infracciones de cumplimiento. Ejecute siempre la evaluación de la política de gobernanza con la acción de marketing &quot;Exportar a terceros&quot; antes de compartir segmentos con organizaciones externas.
- **Tasas de coincidencia bajas debido a brechas de cobertura de identidad:** Si la audiencia del remitente está identificada principalmente por ECID (cookie anónima) pero el área de nombres coincidente es correo electrónico con hash, la tasa de coincidencia será muy baja porque los perfiles anónimos no tienen direcciones de correo electrónico. Compruebe que las audiencias de origen tengan cobertura suficiente del área de nombres de identidad coincidente configurada.
- **Olvidando aceptar el recurso compartido del lado del receptor:** La audiencia compartida no aparece en la lista de audiencias del receptor hasta que se acepte explícitamente el recurso compartido. Coordine con el receptor para garantizar la aceptación oportuna, especialmente para campañas en las que el tiempo sea un factor importante.
- **Audiencias coincidentes obsoletas debido a la desalineación de la programación de evaluación:** Si la audiencia de origen del remitente se evalúa diariamente pero la actualización de [!DNL Segment Match] se ejecuta semanalmente, es posible que la audiencia coincidente del lado del receptor no refleje la pertenencia más reciente. Alinee la evaluación y comparta las cadencias de actualización.

### Prácticas recomendadas

- Establezca un acuerdo formal de uso compartido de datos entre organizaciones antes de configurar [!DNL Segment Match]. Esto debe cubrir casos de uso permitidos, requisitos de gobernanza de datos, obligaciones de consentimiento y procedimientos de finalización.
- Utilice la estimación de superposición como herramienta de validación antes de cada campaña principal: ejecute la estimación antes de comprometerse a garantizar que la audiencia coincidente cumpla los umbrales de tamaño y calidad mínimos.
- Aplique convenciones de nomenclatura descriptiva a los segmentos compartidos que incluyen el nombre del socio, el caso de uso y la fecha (por ejemplo, &quot;PartnerX_HighValue_Suppression_2026Q1&quot;) para mantener la claridad entre las organizaciones.
- Monitorice las tasas de coincidencia con el tiempo. La disminución de las tasas de coincidencia puede indicar una degradación de la cobertura de identidad, problemas de calidad de datos o cambios en la base de clientes del socio.
- Las audiencias de origen de segmentos para excluir perfiles sin el área de nombres de identidad coincidente rellenada. Esto mejora los porcentajes de tasa de coincidencia y proporciona estimaciones de superposición más precisas.
- Para las asociaciones de uso compartido bidireccional, indique una propiedad clara del mantenimiento del segmento y los programas de actualización para evitar confusiones sobre qué organización es responsable de las actualizaciones.

### Decisiones de compensación

>[!NOTE]
>
>**Compensación: Tasa de coincidencia frente a control de privacidad**
>
>El uso de más áreas de nombres de identidad (correo electrónico con hash, teléfono con hash, ID de dispositivo) para la coincidencia aumenta las tasas de coincidencia, pero amplía el área de superficie para una posible reidentificación. El uso de menos áreas de nombres (solo correo electrónico con hash) proporciona una protección de privacidad más sólida, pero puede reducir el tamaño de audiencia coincidente.
>
>- **Varias áreas de nombres favorecen:** Tasas de coincidencia más altas, audiencias coincidentes más grandes y más valiosas para la segmentación de campañas
>- **Un solo espacio de nombres favorece:** Una postura de privacidad más sólida, una revisión de gobernanza más sencilla y un menor riesgo de cumplimiento
>- **Recomendación:** Comience con un solo área de nombres (el correo electrónico con hash es el más común) y agregue áreas de nombres adicionales solo si las tasas de coincidencia no son suficientes para el caso de uso. Documente la evaluación de impacto en la privacidad de cada área de nombres agregada.

>[!NOTE]
>
>**Compensación: granularidad de segmentos vs. simplicidad operativa**
>
>Al compartir muchos segmentos granulares y con un objetivo alto con un socio, se proporciona más flexibilidad para la segmentación de campañas, pero aumenta la complejidad operativa tanto para el remitente como para el receptor. Compartir menos segmentos y más amplios simplifica la administración, pero reduce la precisión de segmentación.
>
>- **Los segmentos granulares favorecen:** Direccionamiento preciso, campañas diferenciadas, mayor relevancia
>- **Los segmentos amplios favorecen:** Administración más sencilla, menos recursos compartidos que supervisar, menor sobrecarga operativa
>- **Recomendación:** Comience con un pequeño número de segmentos de alto valor (2-5) para una nueva asociación. Aumente la granularidad a medida que la asociación madure y se establezcan los procesos operativos. Utilice las convenciones de nomenclatura y la documentación para administrar la complejidad a medida que aumenta el recuento de segmentos.

>[!NOTE]
>
>**Compensación: frecuencia de actualización frente a costo de procesamiento**
>
>Al actualizar las audiencias compartidas con mayor frecuencia, la audiencia coincidente se mantiene actualizada, pero aumenta la carga de procesamiento y puede consumir más capacidad de licencia. Las actualizaciones menos frecuentes reducen el coste, pero permiten que la audiencia coincidente quede obsoleta.
>
>- **Favoritos de actualización frecuentes:** Abono a audiencia actual, mayor relevancia de campaña, mejor precisión de supresión
>- **Favoritos de actualización poco frecuentes:** Menor costo de procesamiento, supervisión más sencilla y menor consumo de licencias
>- **Recomendación:** La actualización diaria es adecuada para la mayoría de las colaboraciones de producción. En el caso de casos de uso sensibles al tiempo (por ejemplo, ventas flash, campañas basadas en eventos), considere la posibilidad de volver a evaluar y compartir bajo demanda inmediatamente antes del inicio de la campaña.

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las capacidades utilizadas en este patrón de caso de uso.

### [!DNL Segment Match]

- [Resumen de coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Solución de problemas de Coincidencia de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### Segmentation and audiences

- [Segmentation Service overview](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Segment Builder UI guide](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder)
- [Audience Composition overview](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language reference](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [Streaming segmentation](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentación de Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Identity and profile

- [Identity Service overview](https://experienceleague.adobe.com/es/docs/experience-platform/identity/home)
- [Identity namespaces overview](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces)
- [Merge policies overview](https://experienceleague.adobe.com/es/docs/experience-platform/profile/merge-policies/overview)
- [Real-Time Customer Profile overview](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### Data governance and consent

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Policy enforcement](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/enforcement/overview)
- [Consent and preferences](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [Consent and preferences field group](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)

### Destinations and activation

- [Información general sobre los destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Destinations catalog](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Monitor dataflows for destinations](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)

### Data modeling and schema

- [XDM System overview](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Schema composition basics](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### Administration and access control

- [Access control overview](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home)
- [Información general de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home)

### Monitoring and observability

- [Alerts overview](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Observability Insights overview](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)

### Guardas

- [Real-Time Customer Profile guardrails](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [Protecciones de activación](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

### Tutoriales

- [Creación de un esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [Habilitar un conjunto de datos para el perfil](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/enable-for-profile)
