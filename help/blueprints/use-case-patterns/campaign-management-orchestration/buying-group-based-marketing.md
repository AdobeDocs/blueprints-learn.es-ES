---
title: Adquisición de gestión de Recorridos y marketing basada en grupos
description: Aprenda a desarrollar recorridos de nivel de cuenta que califiquen clientes potenciales en grupos de compra para mejorar la eficacia del marketing B2B.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 2bf57f67-80c8-4368-98d2-05706427772d
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7932'
ht-degree: 0%

---

# Compra de gestión de recorridos y marketing basada en grupos

Esta guía proporciona una referencia de implementación completa para adquirir administración de recorridos y marketing basada en grupos. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten implementar la orquestación de recorridos a nivel de cuenta con administración de grupos de compras mediante [!DNL Adobe Journey Optimizer B2B Edition] y [!DNL Real-Time CDP B2B Edition].

Utilice este documento para comprender qué configurar, dónde existen las opciones de implementación y qué compensaciones impulsan cada decisión.

A diferencia de los patrones de recorrido a nivel de persona, este patrón funciona a nivel de cuenta, calificando a los posibles clientes individuales en grupos de compra asociados con intereses de soluciones, puntuando la participación a nivel de grupo de compra y orquestando recorridos de cuenta de varios pasos que llevan las cuentas a través de las fases de canalización hasta la preparación de las ventas.

## Resumen del caso de uso

Las organizaciones B2B se enfrentan a un desafío fundamental: las decisiones de compra rara vez las toma una sola persona. Las compras complejas de B2B implican múltiples partes interesadas (responsables de la toma de decisiones, influyentes, defensores, tenedores de presupuesto y evaluadores técnicos) que, colectivamente, forman un &quot;grupo de compra&quot;. El marketing tradicional basado en el posible cliente trata a cada persona de forma independiente, sin tener en cuenta la señal crítica de si la combinación correcta de funciones dentro de una cuenta está comprometida y lista para comprar.

La compra de gestión de recorridos y marketing basada en grupos soluciona este problema cambiando la unidad de orquestación de posibles clientes individuales a cuentas y grupos de compra. El patrón permite a los especialistas en marketing B2B definir los intereses de la solución (los productos o servicios que se venden), crear plantillas de grupo de compra que especifican qué funciones se necesitan para una decisión de compra, calificar los posibles clientes entrantes respecto a esas funciones, puntuar la participación en el nivel de grupo de compra y orquestar recorridos de cuenta que responden a las señales de integridad y preparación del grupo de compra.

El resultado deseado es mejorar la calidad y la velocidad de la canalización: el marketing envía cuentas a las ventas solo cuando se involucra a las personas adecuadas dentro de la cuenta y el grupo de compra es lo suficientemente completo, lo que reduce el esfuerzo de ventas desperdiciado y acelera la progresión del acuerdo.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Mejore la calificación y conversión de posibles clientes

Aumente la calidad del posible cliente y acelere la progresión de la canalización mediante la puntuación, la nutrición y el seguimiento personalizado.

**KPI:** conversión de posibles clientes, conversión de posibles clientes/posibles clientes, eficiencia

[Obtenga más información sobre cómo mejorar la calificación y conversión de posibles clientes](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### Aumentar la generación de posibles clientes

Genere posibles clientes más cualificados para el canal de ventas a través de formularios, eventos, contenido y participación multicanal.

**KPI:** clientes potenciales, coste por cliente potencial, conversión de cliente potencial

[Más información sobre cómo aumentar la generación de posibles clientes](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### Aumentar ingresos y ventas

Impulse el crecimiento de los ingresos de primera línea a través de canales digitales optimizados, campañas y recorridos con los clientes.

**KPI:** crecimiento de ingresos, velocidad de canalización, tasa de cierre de acuerdo

[Más información sobre el aumento de ingresos y ventas](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

## Casos de uso tácticos de ejemplo

Los siguientes son escenarios específicos en los que se puede aplicar este patrón.

- **Calificación del grupo de compra específica de la solución**: defina grupos de compra para cada línea de producto (por ejemplo, &quot;Enterprise CRM&quot;, &quot;Data Platform&quot;, &quot;Security Suite&quot;) con plantillas de roles que especifiquen las personas requeridas (Comprador económico, Evaluador técnico, Campeón, Usuario final) y califique a los posibles clientes del sistema de automatización de marketing y CRM con esas funciones.
- **recorrido de cuenta para la aceleración de canalizaciones**: organice un recorrido de cuenta de varios pasos que envíe correos electrónicos de nutrición dirigidos a roles que no participan suficientemente dentro de un grupo de compras, genere déclencheur de ventas cuando se alcancen los umbrales de participación y pase la cuenta a una fase lista para las ventas.
- **Campañas de integridad de grupos de compra**: identifique las cuentas en las que faltan roles en los grupos de compra (por ejemplo, no se ha identificado ningún comprador económico) e inicie campañas de adquisición dirigidas para atraer a las personas adecuadas dentro de esas cuentas.
- **recorridos de cuentas de venta cruzada**: después de que se cierre un acuerdo inicial, cree nuevos grupos de compras para intereses de soluciones complementarias y organice recorridos de cuentas que nutren al comité de compras ampliado.
- **Reparticipación para ofertas estancadas**: detecta cuentas en las que las puntuaciones de participación del grupo comprador han declinado y déclencheur recorridos de renovación de participación con contenido nuevo, alcance ejecutivo o invitaciones a eventos.
- **Alineación de ventas y marketing mediante perspectivas de CRM**: el estado del grupo de compras superficiales, los datos de participación y el progreso del recorrido de la cuenta directamente dentro de [!DNL Salesforce] o [!DNL Dynamics 365], de modo que los representantes de ventas tengan visibilidad en tiempo real de las cuentas calificadas para marketing.
- **Actualizaciones de grupos de compra impulsadas por eventos**: actualice automáticamente las puntuaciones de participación y pertenencia a grupos de compra cuando los posibles clientes asistan a seminarios web, descarguen documentos técnicos, visiten páginas de precios o soliciten demostraciones.
- **Coordinación de cuentas de varias regiones**: administre grupos de compras en cuentas globales donde los distintos contactos regionales tienen diferentes roles, unificando la puntuación de participación en todas las regiones.

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir la eficacia de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Índice de integridad del grupo de compra | Porcentaje de grupos compradores con todos los roles obligatorios ocupados | [!DNL AJO B2B] paneles de Analytics: rastrear la cobertura de funciones por grupo de compra |
| Puntuación de participación del grupo de compra | Puntuación de participación agregada en todos los miembros de un grupo comprador | Puntuación de participación de [!DNL AJO B2B]: puntuaciones a nivel de persona acumuladas en el grupo de compra |
| Tasa de cuenta calificada de marketing (MQA) | Porcentaje de cuentas que alcanzan el umbral de cualificación de marketing | Criterios de salida del recorrido de cuentas: cuentas en transición a la fase de ventas preparadas |
| Velocidad de canalización | Tiempo promedio desde la creación del grupo de compra hasta la oportunidad calificada para ventas | Integración de CRM: rastrear transiciones de fase de [!DNL AJO B2B] a la canalización de CRM |
| Tasa de calificación del grupo de clientes potenciales a compradores | Porcentaje de posibles clientes cualificados correctamente para comprar roles de grupo | [!DNL AJO B2B] Administración de grupos de compra: relación de clientes potenciales cualificados frente a no cualificados |
| Tasa de respuesta de alertas de ventas | Porcentaje de alertas de ventas que resultan en una actividad de seguimiento de ventas | Perspectivas de ventas de CRM: rastrear la conversión de alerta a actividad |
| Tasa de finalización de Recorridos de cuenta | Porcentaje de cuentas que completan la ruta de recorrido deseada | [!DNL AJO B2B] paneles de Analytics: métricas de finalización de recorridos |
| Tasa de participación en el correo electrónico (B2B) | Tasas de apertura y clics para correos electrónicos de B2B nutre | Informes de [!DNL AJO B2B]: envío de correo electrónico y métricas de participación |

## Patrón de caso de uso

**Comprar administración de recorridos y marketing basada en grupos**

Desarrolle recorridos de nivel de cuenta que califiquen clientes potenciales en grupos de compra para mejorar la eficacia del marketing B2B.

**Cadena de funciones:** Identificación de cuenta > Definición de grupo de compra > Calificación de posibles clientes > Ejecución de Recorridos de cuenta > Puntuación de participación > Informes

## Aplicaciones

En este patrón de caso de uso se utilizan las siguientes aplicaciones de Adobe.

- **[!DNL Journey Optimizer B2B Edition]([!DNL AJO B2B])**: Orquesta recorridos de nivel de cuenta, administra grupos de compras con plantillas de roles e intereses de soluciones, puntúa la participación a nivel de persona y grupo de compras, crea contenido de correo electrónico B2B, envía mensajes SMS, configura alertas de ventas y proporciona paneles de análisis B2B.
- **[!DNL Real-Time CDP B2B Edition]([!DNL RT-CDP B2B])**: unifica perfiles de cuenta a partir de datos B2B de origen cruzado, resuelve relaciones persona a cuenta, evalúa audiencias a nivel de cuenta, configura destinos específicos B2B ([!DNL Marketo Engage], [!DNL LinkedIn], CRM) y aplica el control de datos en los datos B2B.

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Requerido | Zona protegida aprovisionada con [!DNL AJO B2B Edition] y [!DNL RT-CDP B2B Edition] derechos habilitados. Roles configurados para especialistas en marketing B2B, operaciones de ventas y administradores con los permisos adecuados para comprar la administración de grupos, los recorridos de cuenta y la configuración de integración de CRM. | [Resumen de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home), [Resumen de control de acceso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | Esquemas XDM B2B configurados con clases específicas B2B: Cuenta empresarial XDM, Oportunidad empresarial XDM, Persona empresarial XDM (posible cliente/contacto), Campaña empresarial XDM y Lista de marketing empresarial XDM. Deben existir grupos de campos para los atributos de cuenta, atributos de persona y datos de actividad/participación. Conjuntos de datos creados y habilitados para perfil para cada esquema. | [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [clases de esquema B2B](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Fuentes de datos y recopilación | Requerido | Canalizaciones de ingesta de datos B2B establecidas, normalmente a través del conector de origen [!DNL Marketo Engage] o los conectores de origen CRM [!DNL Salesforce]/[!DNL Dynamics]. Los datos de la cuenta, la persona, la oportunidad, la campaña y el miembro de la campaña deben fluir a los conjuntos de datos de AEP. Los datos de participación de comportamiento (visitas web, interacciones por correo electrónico, descargas de contenido) también deben ingerirse para la puntuación de participación. | [Resumen de fuentes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home), [conector de Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| Configuración de identidad y perfil | Requerido | Resolución de identidad B2B configurada para resolver relaciones persona a cuenta. Deben existir áreas de nombres de identidad para identificadores B2B ([!DNL Marketo] ID de persona, [!DNL Salesforce] ID de cliente potencial/contacto, ID de cuenta). Políticas de combinación configuradas para la unificación de perfiles B2B. Los perfiles de cuenta deben unificarse a partir de los datos de fuentes cruzadas. | [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Resolución de identidad B2B](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview) |
| Definición de audiencia y segmentación | Requerido | Definiciones de audiencias de nivel de cuenta creadas con atributos de cuenta, atributos de persona y datos de actividad. Las audiencias de cuenta identifican qué cuentas ingresan en los recorridos de grupo de compra. La evaluación por lotes suele ser suficiente para las recorridos de cuenta B2B, aunque la evaluación de streaming se puede utilizar para déclencheur de calificación de cuentas en tiempo real. | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [audiencias de la cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Los atributos calculados pueden acumular eventos de participación a nivel de persona (aperturas de correo electrónico, descargas de contenido, asistencia a seminarios web) en métricas de participación a nivel de cuenta que alimentan la puntuación de grupo de compra y la lógica de calificación de cuentas. | [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Administración del ciclo de datos | Recomendado | La administración de consentimientos es crítica para las comunicaciones por correo electrónico y SMS B2B. Las políticas de caducidad del conjunto de datos ayudan a administrar el ciclo vital de los datos de participación transitorios y garantizan el cumplimiento de los requisitos de retención de datos. | [Administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Etiquetado y aplicación del uso de datos | Recomendado | Los datos B2B suelen contener información confidencial de la compañía y datos personales de contactos comerciales. Las políticas de gobernanza de datos garantizan el uso compatible de los datos B2B entre destinos, especialmente al activarlos en plataformas publicitarias o sistemas de terceros. | [Resumen de control de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Monitorización y observabilidad | Recomendado | La supervisión garantiza que las canalizaciones de datos B2B (sincronizaciones CRM/[!DNL Marketo]) estén en buen estado, que los perfiles de cuenta se estén actualizando y que las ejecuciones del recorrido de cuentas se lleven a cabo sin errores. Las alertas sobre errores del flujo de datos de origen son críticas para mantener la moneda de los datos. | [Resumen de Observability Insights](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Informes y análisis | Incluido | Los paneles de análisis B2B de [!DNL AJO B2B Edition] proporcionan la participación del grupo comprador, el rendimiento del recorrido de la cuenta y las métricas de canalización. [!DNL CJA B2B Edition] amplía el análisis con análisis de espacio de trabajo a nivel de cuenta, análisis de grupos de compra y correlación de oportunidades. | [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Journey Optimizer B2B Edition] ([!DNL AJO B2B])

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Configuración de interés de solución | Fase 1: Configuración del grupo de interés y compra de la solución | Defina intereses de soluciones que asignen productos o servicios a criterios de cualificación de grupos de compra |
| Administración del grupo de compra | Fase 1: Configuración del grupo de interés y compra de la solución | Cree y administre grupos de compras con plantillas de funciones, asignación de personas y definiciones de intereses de soluciones |
| Journey Orchestration de cuenta | Fase 3: Diseño y ejecución del Recorrido de cuentas | Diseñe y administre recorridos de cuenta de varios pasos con condiciones, acciones y ramificación basada en la participación |
| Puntuación de participación | Fase 2: Calificación de posibles clientes y puntuación de la participación | Puntuar la participación a nivel de persona dentro de los grupos compradores para medir la integridad y preparación del grupo comprador. |
| Calificación de cuenta | Fase 2: Calificación de posibles clientes y puntuación de la participación | Utilice agentes de calificación de cuentas con tecnología de IA para evaluar la preparación de la cuenta y la calidad de la canalización |
| Creación de correo electrónico B2B | Fase 3: Diseño y ejecución del Recorrido de cuentas | Cree contenido de correo electrónico B2B con plantillas, fragmentos visuales, temas de marca y generación de contenido asistido por IA |
| Administración de canales SMS | Fase 3: Diseño y ejecución del Recorrido de cuentas | Configuración y administración de comunicaciones SMS dentro de recorridos de cuenta B2B |
| Configuración de alerta de ventas | Fase 4: alineación de ventas e integración CRM | Configure correos electrónicos de alerta de ventas para notificar a los equipos de ventas los hitos de participación de la cuenta y las señales de compra |
| Perspectivas de ventas de CRM | Fase 4: alineación de ventas e integración CRM | Proporcionar visibilidad en CRM ([!DNL Salesforce], [!DNL Dynamics]) para el estado del grupo de compra, los datos de participación y el progreso del recorrido de la cuenta |
| Paneles de B2B Analytics | Fase 5: Creación de informes y optimización | Monitorice el rendimiento del recorrido de la cuenta, la participación del grupo de compra y las métricas de canalización a través de paneles inteligentes y de participación |

### [!DNL Real-Time CDP B2B Edition] ([!DNL RT-CDP B2B])

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Unificación del perfil de cuenta | Fase 0: Base de datos B2B | Consolidar datos B2B de origen cruzado en perfiles de cuenta unificados mediante clases de esquema B2B XDM especializadas y grupos de campos |
| Resolución de identidad B2B | Fase 0: Base de datos B2B | Resuelva las relaciones persona a cuenta mediante identificadores principales que admitan jerarquías de cuentas de varios niveles y asignaciones de persona a cuenta de varios a varios |
| Evaluación de audiencia de cuenta | Fase 0: Base de datos B2B | Evaluar la pertenencia a segmentos en el nivel de cuenta combinando atributos de cuenta, atributos de persona y datos de actividad |
| Configuración de destino de cuenta | Fase 4: alineación de ventas e integración CRM | Configurar conexiones a destinos específicos B2B ([!DNL Marketo Engage], [!DNL LinkedIn], sistemas CRM) con asignación de campos a nivel de cuenta |
| Audience Activation de cuenta | Fase 4: alineación de ventas e integración CRM | Publicar audiencias basadas en cuentas en destinos para la segmentación y supresión basadas en cuentas |
| Integración de [!DNL Marketo Engage] | Fase 0: Base de datos B2B | Ingresar y activar datos bidireccionalmente con [!DNL Marketo Engage] mediante conectores de origen y destino B2B nativos |
| Gobernanza de datos B2B | Fase 0: Base de datos B2B | Aplicar políticas de uso de datos y el consentimiento en los procesos de activación y centralización de datos de la cuenta B2B |

## Prerrequisitos

Complete lo siguiente antes de comenzar la implementación.

- [ ] [!DNL AJO B2B Edition] licencia aprovisionada y habilitada en la zona protegida de destino
- [ ] [!DNL RT-CDP B2B Edition] licencia aprovisionada y habilitada en la zona protegida de destino
- [ Se puede acceder al sistema CRM ] ([!DNL Salesforce] o [!DNL Microsoft Dynamics 365]) con las credenciales de API adecuadas para la sincronización de datos bidireccional
- [ ] [!DNL Marketo Engage] instancia conectada (si usa [!DNL Marketo] como plataforma de automatización de marketing) con el conector de origen configurado
- [ ] esquemas XDM B2B implementados: clases de cuenta, persona, oportunidad, campaña y miembro de campaña con grupos de campos requeridos
- [ ] datos de cuenta y persona introducidos en AEP con relaciones persona a cuenta resueltas
- [ ] Canal de correo electrónico configurado: subdominio delegado, grupo de IP calentado y superficie de canal creada para el envío de correo electrónico B2B
- [ Proveedor de SMS ] configurado (si el canal SMS se usa en las recorridos de la cuenta): credenciales de [!DNL Sinch], [!DNL Twilio] o [!DNL Infobip] aprovisionadas
- [ ] Equipo de ventas incorporado al componente de perspectivas de ventas de CRM ([!DNL Salesforce] paquete de AppExchange o [!DNL Dynamics] solución instalada)
- [ ] Recursos de contenido preparados: plantillas de correo electrónico B2B, temas de marca y fragmentos visuales para correos electrónicos de alerta de nutrición y ventas
- [ ] taxonomía de interés de soluciones definida: lista de productos/servicios que tendrán grupos de compra asociados
- [ ] plantillas de rol de grupo de compra diseñadas: personas y roles necesarios para cada interés de solución (por ejemplo, Comprador económico, Evaluador técnico, Campeón)

## Opciones de implementación

En esta sección se describen los enfoques de implementación disponibles, cada uno de ellos adaptado a diferentes necesidades organizativas y niveles de madurez.

### Opción A: interés de solución única con recorrido de cuenta lineal

**Ideal para:** organizaciones nuevas en la administración de grupos de compras que desean comenzar con una sola línea de productos u oferta de soluciones, validar el enfoque e iterar antes de escalar a varios intereses de soluciones.

**Cómo funciona:**

Este enfoque se centra en un único interés de solución (un producto o servicio) con una plantilla de grupo de compra. Un recorrido de cuentas lineal está diseñado con etapas secuenciales: identificación de cuentas, formación de grupos de compras, participación de nutrientes, umbral de puntuación de participación y transferencia de ventas. El recorrido sigue una trayectoria directa sin ramificaciones complejas ni pistas paralelas.

Los posibles clientes se clasifican para comprar roles de grupo a medida que se ingieren desde CRM o [!DNL Marketo Engage]. El recorrido de cuenta envía correos electrónicos de promoción a funciones con participación insuficiente, supervisa las puntuaciones de participación y genera un déclencheur de venta cuando el grupo de compra alcanza un umbral definido de integridad y participación. Este enfoque proporciona una prueba de concepto clara y mensurable antes de introducir la complejidad.

**Consideraciones clave:**

- Implementación y validación más sencillas, por lo que son adecuadas para una primera implementación
- Limitado a un movimiento de compra de producto/servicio a la vez
- Es posible que la estructura de recorrido lineal no se adapte a ciclos de compra complejos en varias fases

**Ventajas:**

- Obtención de valor en menos tiempo con una complejidad mínima de la configuración
- Borrar métricas de éxito vinculadas a un único interés de solución
- Más fácil de explicar y de obtener la aprobación de la organización
- Informes directos y medición de KPI

**Limitaciones:**

- No aborda casos de venta cruzada o de varios productos
- Las cuentas interesadas en varias soluciones requieren recorridos separados y no coordinados
- Es posible que no aproveche completamente las capacidades de administración de grupos de compra

**Experience League:**

- [Información general sobre AJO B2B edition](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [Creación de grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)

### Opción B: intereses de varias soluciones con recorridos de cuenta de ramificación

**Ideal para:** organizaciones con varias líneas de productos u ofertas de servicios que necesitan administrar distintos grupos de compras según el interés de la solución, con recorridos de cuenta que determinan la rama en función de los intereses de la solución que están activos y la distancia a lo largo de cada grupo de compras en el proceso de calificación.

**Cómo funciona:**

Se definen varios intereses de solución, cada uno con su propia plantilla de función de grupo de compra. El recorrido de cuentas comienza con la identificación de cuentas y evalúa qué intereses de solución se aplican a cada cuenta en función de señales de comportamiento, datos firmográficos o intención explícita. Las ramas de recorrido para abordar cada interés activo de la solución, ejecutando pistas de nutrición paralelas para diferentes grupos de compra dentro de la misma cuenta.

La puntuación de participación funciona de forma independiente por grupo de compra, lo que permite que un grupo de compra alcance la preparación para las ventas mientras otro se nutre. Las alertas de ventas se configuran según el interés de la solución, por lo que se notifica al equipo de ventas o especialista correspondiente cuando un grupo de compra específico reúne los requisitos. Las perspectivas de CRM aparecen en todos los grupos de compras activos de una cuenta, lo que proporciona a las ventas una vista integral.

**Consideraciones clave:**

- Requiere una taxonomía de intereses de soluciones bien definida y distintas plantillas de grupos de compra
- La complejidad del recorrido aumenta con cada interés de solución adicional
- Se debe planificar la coordinación entre grupos de compra (por ejemplo, contactos compartidos que tengan funciones en varios grupos de compra)

**Ventajas:**

- Admite estrategias de cuentas de venta cruzada y de varios productos
- La puntuación independiente por grupo de compra proporciona visibilidad granular de la canalización
- Los equipos de ventas reciben alertas segmentadas por interés de solución
- Maximiza las capacidades de administración de grupos de compras de [!DNL AJO B2B Edition]

**Limitaciones:**

- Mayor complejidad de la implementación y mayor tiempo de implementación
- Se requieren más recursos de contenido (seguimientos de correo electrónico independientes por interés de solución)
- Los informes son más complejos con varios grupos de compras por cuenta
- Riesgo de enviar mensajes en exceso a los contactos que están en varios grupos de compra (requiere administración de frecuencia)

**Experience League:**

- [Intereses de solución](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [Recorridos de cuenta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)

### Opción C: Calificación de cuentas asistidas por IA con progresión de recorridos automatizada

**Ideal para:** organizaciones B2B maduras con datos históricos significativos que desean aprovechar agentes de calificación de cuentas con tecnología de IA para automatizar la evaluación de la preparación de la cuenta, reducir el esfuerzo de calificación manual y ajustar dinámicamente las rutas de recorrido en función de las puntuaciones de preparación generadas por IA.

**Cómo funciona:**

Este enfoque se basa en la base de interés de varias soluciones de la opción B, pero añade una calificación de cuentas con tecnología de IA para automatizar la transición entre etapas de recorrido. En lugar de depender únicamente de los umbrales de puntuación de participación basados en reglas, el agente de calificación de IA evalúa la preparación de la cuenta mediante un conjunto más amplio de señales: integridad del grupo de compra, velocidad de participación, ajuste firmográfico, patrones de conversión históricos y datos de intención.

Los recorridos de cuentas utilizan el resultado de calificación de IA para determinar los siguientes pasos: las cuentas con una puntuación alta en preparación se dirigen rápidamente a alertas de ventas, las cuentas del nivel medio reciben una nutrición intensificada y las cuentas de baja preparación se colocan en pistas de sensibilización a largo plazo. El agente de IA vuelve a evaluar continuamente a medida que llegan nuevos datos de participación, lo que permite la progresión dinámica del recorrido sin intervención manual.

**Consideraciones clave:**

- Requiere datos históricos suficientes para formar modelos de cualificación eficaces
- Las salidas de IA deben validarse con los resultados reales de la canalización antes de la implementación completa
- Se combina bien con [!DNL CJA B2B Edition] para analizar la precisión de calificación y la correlación de canalización

**Ventajas:**

- Reduce el esfuerzo de calificación manual y elimina las entregas arbitrarias basadas en umbrales
- Se adapta dinámicamente a los cambiantes patrones de comportamiento y participación de la cuenta
- Mayor calidad de la canalización mediante la incorporación de múltiples señales más allá de las puntuaciones de participación simples
- La reevaluación continua evita que las cuentas se atasquen en etapas de recorrido incorrectas

**Limitaciones:**

- Requiere datos de conversión históricos para una formación significativa sobre IA
- Las decisiones de calificación de &quot;caja negra&quot; pueden ser más difíciles de entender y confiar inicialmente en los equipos de ventas
- Es más complejo solucionar problemas cuando las cuentas se clasifican inesperadamente o no se clasifican
- Depende de la calidad y exhaustividad de los datos en todas las señales de entrada

**Experience League:**

- [Calificación de cuenta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Asistente de IA en AJO B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)

### Comparación de opciones

| Criterios | Opción A: interés de solución única | Opción B: intereses de varias soluciones | Opción C: calificación asistida por IA |
| --- | --- | --- | --- |
| Mejor para | Primera implementación, una sola línea de productos | Organizaciones de varios productos | Organizaciones maduras con datos históricos |
| Complejidad | Baja | Medium-High | Alta |
| Tiempo hasta el valor | 2 a 4 semanas | 4 a 8 semanas | 6 a 12 semanas |
| Intereses de solución | 1 | Múltiple | Múltiple |
| estructura del recorrido | Lineal | Ramificación, pistas paralelas | Progresión dinámica impulsada por IA |
| Método de puntuación | Umbrales basados en reglas | Basado en reglas por grupo de compra | Calificación y reglas con tecnología de IA |
| Requisitos de contenido | Mínimo (una pista de crianza) | Alto (por interés de solución) | Selección de contenido alto + dinámico |
| Alineación de ventas | Flujo de trabajo de alerta única | Alertas de interés por solución | Alertas priorizadas y con puntuación de IA |
| Requiere | Base de datos básica B2B | taxonomía de soluciones bien definida | Datos de conversión histórica + taxonomía |

### Elija la opción correcta

Comience con estas preguntas para determinar el mejor enfoque de implementación:

1. **¿Cuántos productos o servicios distintos tienen comités de compra independientes?** Si la respuesta es una (o la organización desea probar el concepto primero), comience con la Opción A. Si es múltiple, vaya a la pregunta 2.

2. **¿Hay suficientes datos históricos sobre ofertas ganadas/perdidas, composición del comité de compras y patrones de participación?** Si es así y la organización desea minimizar la calificación manual, la opción C proporciona el enfoque más automatizado. Si no es así, la opción B proporciona compatibilidad con varias soluciones en función de sus intereses con puntuación basada en reglas.

3. **¿Cuál es la capacidad de administración de cambios de la organización?** Las opciones B y C requieren una mayor alineación organizativa (producción de contenido, capacitación de ventas, coordinación interfuncional). Si la capacidad es limitada, comience con la opción A y amplíe.

Una ruta de progresión común es: comenzar con la opción A para probar el concepto con un interés de solución, ampliar a la opción B añadiendo intereses de solución a medida que aumenta la confianza y, a continuación, colocar en la calificación de IA de la opción C una vez que se disponga de suficientes datos históricos para entrenar los modelos de forma eficaz.

## Fases de implementación

Las siguientes fases describen el proceso de implementación paso a paso para este patrón de caso de uso.

### Fase 0: Base de datos B2B

**Funciones de la aplicación:** [!DNL RT-CDP B2B]: unificación de perfiles de cuenta, resolución de identidad B2B, integración de [!DNL Marketo Engage], administración de datos B2B, evaluación de audiencia de cuenta

Esta fase establece la infraestructura de datos B2B en [!DNL RT-CDP B2B Edition]. Unificará los datos de cuenta de CRM, automatización de marketing y otras fuentes en un único perfil de cuenta, resolverá las relaciones persona a cuenta, configurará el control de datos B2B y creará audiencias de nivel de cuenta que se alimentarán de la administración de grupos de compra de [!DNL AJO B2B Edition].

#### Decisión: estrategia de fuente de datos B2B

¿Qué sistemas sirven como fuentes principales de datos de cuenta, persona y participación?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| [!DNL Marketo Engage] como origen principal | [!DNL Marketo] es la plataforma de automatización de marketing de la organización con un historial de participación enriquecido | El conector bidireccional nativo simplifica la configuración; los datos de participación fluyen automáticamente; relaciones persona a cuenta heredadas de [!DNL Marketo] |
| CRM ([!DNL Salesforce]/[!DNL Dynamics]) como origen principal | CRM es el sistema de registro para cuentas y contactos; no se utiliza [!DNL Marketo] | Requiere la configuración del conector de origen de CRM; los datos de participación pueden necesitar fuentes suplementarias; relaciones persona a cuenta de asociaciones de contacto de cuenta de CRM |
| Híbrido: CRM para cuentas + [!DNL Marketo] para participación | CRM posee datos maestros de cuenta/contacto mientras [!DNL Marketo] captura la participación de comportamiento | Patrón más común para las organizaciones que utilizan ambos; requiere una resolución de identidad cuidadosa para vincular a [!DNL Marketo] personas a contactos de CRM |

#### Decisión: estrategia de audiencia de cuenta

¿Cómo se deben definir las audiencias de cuenta para la entrada de recorrido?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Audiencias de cuenta basadas en Firmographic | Cuentas de Target basadas en el sector, el tamaño de la empresa, el nivel de ingresos o la geografía | Positivo para las listas de objetivos ABM; no requiere datos de participación; puede ser amplio |
| Audiencias de cuenta basadas en la participación | Cuentas de Target donde las personas han mostrado señales de intención de comportamiento | Requiere que fluyan los datos de participación; una segmentación más precisa; puede omitir cuentas con interés latente |
| Firmográfico y participación combinados | Cuentas de Target que coinciden con el perfil de cliente ideal Y muestran participación | El más preciso; requiere ambos tipos de datos; recomendado para la generación de canalizaciones aptas |

**Navegación por la interfaz de usuario:** Plataforma > Fuentes > Catálogo > Seleccionar origen ([!DNL Marketo Engage], [!DNL Salesforce], etc.) > Configuración del flujo de datos

**Detalles de configuración de clave:**

- Configure esquemas XDM B2B para cada entidad B2B (cuenta, persona, oportunidad, campaña, miembro de campaña) con los grupos de campos requeridos
- Configure los conectores de origen para CRM o [!DNL Marketo Engage] con la programación adecuada (normalmente intervalos de 1 a 4 horas para los datos B2B)
- Configurar áreas de nombres de identidad para identificadores B2B ([!DNL Marketo] ID de persona, ID de posible cliente de SFDC, ID de contacto de SFDC, ID de cuenta)
- Habilitar la resolución de identidades B2B para vincular personas a cuentas
- Crear audiencias de nivel de cuenta usando la capacidad Audiencias de cuenta en [!DNL RT-CDP]

**Documentación de Experience League:**

- [Información general sobre RT-CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)
- [Esquemas B2B en Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Conector de origen de Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Audiencias de cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [Resolución de identidad B2B](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)

### Fase 1: Interés de la solución y configuración del grupo de compra

**Funciones de la aplicación:** [!DNL AJO B2B]: Configuración de interés de solución, Administración de grupos de compra

Esta fase define los intereses de la solución (productos/servicios) y las plantillas de grupo de compra que forman el núcleo del modelo de gestión de grupos de compra. Creará intereses de soluciones, definirá plantillas de funciones con requisitos personales y configurará cómo los posibles clientes se clasifican para adquirir funciones de grupo.

#### Decisión: granularidad de interés de solución

¿A qué nivel deben definirse los intereses de la solución?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Intereses de la solución de nivel de producto | Cada producto tiene su propio grupo de compra | Más granular; activa plantillas de grupos de compra específicas del producto; puede resultar en muchos grupos de compra por cuenta |
| Intereses a nivel de categoría de solución | Agrupe los productos relacionados en categorías de solución (por ejemplo, &quot;Marketing Cloud&quot; en lugar de productos individuales) | Más fácil de administrar; menos grupos compradores; las funciones pueden ser más genéricas; recomendado para implementaciones iniciales |
| Intereses a nivel de caso de uso | Defina intereses en torno a los resultados empresariales en lugar de los productos (por ejemplo, &quot;Transformación digital&quot;) | Se alinea con la venta consultiva; las funciones de grupo de compra pueden abarcar varios productos; más difícil de asignar a las fases de canalización de CRM |

#### Decisión: comprar diseño de plantilla de rol de grupo

¿Cómo se deben definir las funciones dentro de cada grupo comprador?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Plantilla de rol estándar | Utilice un conjunto común de funciones en todos los intereses de la solución (por ejemplo, Comprador económico, Evaluador técnico, Campeón, Usuario final) | Puntuación y calificación coherentes; más fáciles de administrar; es posible que no capturen funciones específicas de la solución |
| Plantillas de funciones específicas de la solución | Defina funciones únicas por interés de solución en función del comité de compras real de ese producto | Calificación más precisa; requiere un conocimiento más profundo de cada proceso de compra; mayor mantenimiento |
| Plantillas de roles en niveles | Defina las funciones necesarias (debe tener para la calificación) y las funciones opcionales (mejore la integridad, pero no es necesario) | Equilibra la precisión con la flexibilidad; evita que los criterios de cualificación excesivamente estrictos bloqueen la canalización |

**Navegación de la interfaz de usuario:** [!DNL AJO B2B Edition] > Grupos de compra > Intereses de la solución > Crear interés de la solución

**Navegación de la interfaz de usuario:** [!DNL AJO B2B Edition] > Comprar grupos > Plantillas de roles > Crear plantilla de roles

**Detalles de configuración de clave:**

- Defina cada interés de la solución con un nombre, una descripción y el resultado comercial que aborda
- Cree plantillas de funciones que especifiquen las personas necesarias para cada grupo comprador (por ejemplo, &quot;Responsable de la toma de decisiones&quot;, &quot;Influyente&quot;, &quot;Profesional&quot;, &quot;Patrocinador ejecutivo&quot;).
- Configurar criterios de cualificación de posible cliente a función: cómo determina el sistema a qué persona se asigna un posible cliente (en función del puesto, el departamento, la antigüedad o los atributos personalizados)
- Definir umbrales de integridad: defina qué porcentaje de roles debe rellenarse para que un grupo comprador se considere &quot;completo&quot;
- Vincule los intereses de la solución a audiencias de cuenta o atributos de cuenta que indiquen un interés potencial

**Donde las opciones difieren:**

**Para La Opción A (Interés De Solución Única):**
Cree un interés de solución y una plantilla de funciones. Céntrese en un movimiento de compra claro y bien entendido para el producto o servicio principal de la organización.

**Para La Opción B (Intereses De Varias Soluciones):**
Cree varios intereses de soluciones, cada uno con su propia plantilla de funciones. Asigne cada interés de solución al tipo de producto/oportunidad de CRM adecuado para el seguimiento de la canalización descendente.

**Para la opción C (calificación asistida por IA):**
Configure los intereses de la solución y las plantillas de funciones como en la Opción B, pero además configure el agente de calificación de IA con datos históricos sobre composiciones de grupos de compra exitosas y resultados de acuerdos para entrenar el modelo de calificación.

**Documentación de Experience League:**

- [Resumen de grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [Intereses de solución](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [Plantillas de roles](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [Creación de grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)

### Fase 2: Calificación de posibles clientes y puntuación de la participación

**Funciones de la aplicación:** [!DNL AJO B2B]: Puntuación de participación, Calificación de la cuenta

Esta fase configura el modelo de puntuación de participación que mide la participación a nivel de persona dentro de los grupos de compra y la acumula en puntuaciones de preparación a nivel de grupo de compra y de cuenta. Configurará reglas de puntuación, definirá umbrales de participación para la calificación y, opcionalmente, habilitará la calificación de cuentas con tecnología de IA.

#### Decisión: modelo de puntuación de participación

¿Cómo se debe puntuar el compromiso a nivel de persona y grupo de compra?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Puntuación basada en actividades | Asignar valores de punto a acciones específicas (correo electrónico abierto = 5 pts, descarga de contenido = 15 pts, solicitud de demostración = 50 pts) | Transparente y fácil de ajustar; requiere mantenimiento continuo a medida que cambia el contenido y los canales; más familiar para [!DNL Marketo] usuarios |
| Puntuación ponderada por la actualización | Peso de las actividades recientes mayor que las más antiguas (modelo de puntuación en declive) | Refleja mejor la intención actual; evita que puntuaciones altas antiguas inflen la calificación; es más complejo de configurar |
| Puntuación con tecnología de IA | Usar el agente de calificación de IA [!DNL AJO B2B] para generar puntuaciones de preparación basadas en el reconocimiento de patrones | Más sofisticado; se adapta automáticamente; requiere datos históricos; puede ser opaco para los equipos de ventas inicialmente |

#### Decisión: enfoque del umbral de calificación

¿Cuándo se debe considerar que un grupo comprador está listo para el traspaso de ventas?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo umbral de puntuación | El grupo comprador cumple los requisitos cuando la puntuación de participación agregada supera un valor definido | Fácil de implementar; es posible que el umbral de puntuación deba ajustarse con el tiempo; no tiene en cuenta la composición de funciones |
| Complejidad + umbral de puntuación | El grupo de compra es válido cuando se cumple la cobertura mínima de funciones Y el umbral de puntuación | Calificación más sólida; evita la transferencia de grupos de compra con puntuaciones altas pero sin funciones clave |
| Preparación determinada por IA | El agente de calificación de IA determina la preparación utilizando múltiples señales más allá de la puntuación y la integridad | Más sofisticado; explica la velocidad de compra, las señales competitivas y los patrones históricos; sólo la opción C |

**Navegación de la interfaz de usuario:** [!DNL AJO B2B Edition] > Comprar grupos > Puntuación de participación > Configurar reglas de puntuación

**Detalles de configuración de clave:**

- Defina reglas de puntuación de participación: asigne valores de punto a eventos de comportamiento (aperturas de correo electrónico, clics, visitas a páginas web, descargas de contenido, envíos de formularios, asistencia a seminarios web, solicitudes de demostración).
- Configurar la disminución de puntuación o la ponderación de actualización si se utiliza la puntuación con distinción de tiempo
- Establecer agregación de puntuación a nivel de grupo de compra: cómo se combinan las puntuaciones de persona en una puntuación de grupo de compra (suma, promedio ponderado o umbral mínimo por rol)
- Definir umbrales de cualificación: los niveles de puntuación y de integridad que déclencheur la transición a la siguiente fase de compra
- Configuración del agente de calificación de IA (opción C): entrenar con datos de acuerdos históricos, definir las señales que el agente debe considerar y establecer umbrales de confianza

**Documentación de Experience League:**

- [Puntuación de participación](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Fases del grupo de compras](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Calificación de cuenta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)

### Fase 3: Diseño y ejecución del recorrido de cuentas

**Funciones de la aplicación:** [!DNL AJO B2B]: Journey Orchestration de cuenta, creación de correo electrónico B2B, administración de canales SMS

Esta fase diseña e implementa el recorrido de cuentas que organiza la participación con los miembros del grupo comprador. Creará recorridos de cuenta con condiciones de entrada, nodos de acción (correo electrónico, SMS), ramas de condición (según la fase de grupo de compra, puntuación de participación, cobertura de funciones), pasos de espera y criterios de salida.

#### Decisión: déclencheur de entrada de Recorrido

¿Qué evento o condición hace que una cuenta entre en la recorrido?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Calificación de audiencia de cuenta | La cuenta introduce cuando se une a una audiencia de cuenta de destinatario | Orientado a lotes; bueno para la entrada basada en listas ABM; la audiencia debe estar predefinida |
| Evento de creación de grupo de compra | La cuenta introduce el momento en el que se crea un grupo de compra para la cuenta | Impulsado por eventos; activado por la calificación de posibles clientes en un rol de grupo de compra; más tiempo real |
| Cambio de atributo de cuenta | La cuenta introduce cuándo cambia un atributo específico (por ejemplo, puntuación por intención, nivel de cuenta) | Requiere que el atributo de activación se actualice en tiempo real o casi en tiempo real |

#### Decisión: mezcla de canales para la nutrición B2B

¿Qué canales debe utilizar el recorrido de la cuenta para atraer a los miembros del grupo comprador?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo correo electrónico | La mayoría de las interacciones B2B se producen por correo electrónico; no existe ninguna infraestructura de inclusión de SMS | El más fácil de configurar; el patrón B2B más común; puede perder contactos que dan prioridad a los móviles |
| Correo electrónico + SMS | La organización tiene la opción de recibir SMS de los contactos comerciales; se garantizan notificaciones de alta urgencia | SMS efectivo para alertas con distinción de tiempo (recordatorios de eventos, confirmaciones de reuniones); requiere la configuración del proveedor de SMS |
| Correo electrónico + SMS + Alertas de ventas | Espectro completo: nutrición de marketing por correo electrónico/SMS más notificaciones al equipo de ventas | El más completo; requiere la adopción por parte del equipo de ventas de un flujo de trabajo de alertas; coordina los puntos de contacto de marketing y ventas |

#### Decisión: estrategia de ramificación de Recorridos

¿Cómo debería basarse la rama de recorrido en la cuenta y el estado del grupo de compra?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Ramificación basada en etapas | Sucursal basada en la fase de grupo de compra (por ejemplo, Sensibilización, Consideración, Decisión) | Se alinea con las fases tradicionales de funnel; contenido asignado a fases; borrar ruta de progresión |
| Ramificación basada en roles | Rama para enviar contenido diferente a diferentes funciones de grupo de compra (contenido técnico para evaluadores, contenido de ROI para compradores económicos). | Más personalizado; requiere recursos de contenido específicos de funciones; mayor esfuerzo de producción de contenido |
| Ramificación basada en la participación | Rama basada en los umbrales de puntuación de participación (participación baja = reparticipación, alta = aceleración) | Dinámico y adaptable; se adapta al comportamiento real; puede crear ramas complejas de árboles |

**Navegación de la interfaz de usuario:** [!DNL AJO B2B Edition] > Recorridos de la cuenta > Crear Recorrido

**Detalles de configuración de clave:**

- Crear el lienzo del recorrido de cuentas con la condición de entrada seleccionada
- Agregar nodos de recorrido de cuenta: acciones de correo electrónico, acciones de SMS, pasos de espera, divisiones de condición y ramificación de rutas
- Crear contenido de correo electrónico B2B mediante el Designer de correo electrónico B2B con temáticas de marca, fragmentos visuales y generación de contenido asistido por IA
- Configure tokens de personalización que hagan referencia a atributos de cuenta, atributos de persona y datos de grupos de compras
- Establezca duraciones de espera entre puntos de contacto (los recorridos B2B suelen utilizar esperas más largas: de 3 a 7 días entre correos electrónicos)
- Definir criterios de salida: condiciones en las que las cuentas abandonan el recorrido (el grupo comprador alcanza el umbral de calificación, la oportunidad creada en CRM, la cuenta se excluye)
- Configure las acciones de SMS si utiliza el canal SMS (requiere la configuración del proveedor de SMS y la inclusión de contacto)
- Pruebe el recorrido con cuentas de prueba antes de publicar

**Donde las opciones difieren:**

**Para La Opción A (Interés De Solución Única):**
Diseñe un recorrido lineal con etapas secuenciales. La entrada se basa en una audiencia de una sola cuenta o en un evento de creación de grupo de compra. Un seguimiento de nutrición de correo electrónico con una urgencia y profundidad de contenido cada vez mayores.

**Para La Opción B (Intereses De Varias Soluciones):**
Diseñe un recorrido con ramas paralelas por interés de solución. Utilice nodos de condición para dirigir las cuentas a la pista de nutrición adecuada en función de los grupos de compra. Cada rama tiene su propio contenido y umbrales de puntuación.

**Para la opción C (calificación asistida por IA):**
Diseñe un recorrido en el que los nodos de condición evalúen la puntuación de calificación de IA en lugar de los umbrales basados en reglas (o además de ellos). Incluya la selección de rutas dinámicas donde la API determine si se debe acelerar, mantener o quitar la prioridad de una cuenta.

**Documentación de Experience League:**

- [Resumen de recorridos de cuenta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [Nodos del recorrido de cuentas](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [Creación de correo electrónico B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/email-authoring)
- [Canal de SMS en AJO B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sms-authoring)
- [Asistente de IA para la creación de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/ai-assistant-emails)

### Fase 4: Alineación de ventas e integración CRM

**Funciones de la aplicación:** [!DNL AJO B2B]: Configuración de alertas de ventas, Perspectivas de ventas de CRM; [!DNL RT-CDP B2B]: Configuración de destino de cuenta, Audience Activation de cuenta

Esta fase establece el puente entre marketing y ventas mediante la configuración de correos electrónicos de alerta de ventas, la implementación de perspectivas de ventas de CRM para la visibilidad dentro de CRM y, opcionalmente, la activación de audiencias de cuenta en destinos B2B ([!DNL LinkedIn], [!DNL Marketo], sistemas CRM).

#### Decisión: estrategia de déclencheur de alertas de ventas

¿Cuándo se debe notificar a las ventas el estado del grupo de compra de una cuenta?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Alertas basadas en hitos | Notificar a las ventas cuando el grupo de compra alcance hitos específicos (cualificado, completo, alta participación) | Notificaciones claras y discretas; evita la fatiga de las alertas; puede pasar por alto tendencias de participación graduales |
| Alertas basadas en umbrales | Notificar a las ventas cuando la puntuación de participación supere un umbral definido | Monitorización continua; puede almacenar varias alertas en déclencheur a medida que las puntuaciones fluctúan cerca del umbral |
| Alertas de transición entre etapas | Notificar a las ventas cuando el grupo de compras pase a una nueva etapa (por ejemplo, de Consideración a Decisión) | Se alinea con las fases de la canalización; la señal más clara para la acción de ventas; requiere definiciones de fases bien definidas |

#### Decisión: profundidad de integración de CRM

¿Con qué profundidad deberían aparecer los datos de grupo compradores en CRM?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo alertas de ventas (sin componente en CRM) | La organización no utiliza [!DNL Salesforce] o [!DNL Dynamics], o la integración con CRM no es factible | Menor esfuerzo de integración; ventas recibe notificaciones por correo electrónico pero no tiene panel CRM; visibilidad limitada |
| Panel de perspectivas de ventas CRM | La organización utiliza [!DNL Salesforce] o [!DNL Dynamics] y desea que el estado del grupo de compra sea visible en CRM | Requiere la instalación del paquete de perspectivas de ventas de CRM; proporciona inteligencia de nivel de cuenta enriquecida; recomendado para la mayoría de las implementaciones |
| Sincronización completa bidireccional de CRM | Las etapas y puntuaciones del grupo de compra vuelven a escribirse en objetos CRM, lo que influye en el flujo de trabajo y los informes de CRM | Complejidad de integración máxima; habilita la creación de informes de canalización nativa de CRM; requiere una configuración de CRM personalizada |

**Navegación de la interfaz de usuario:** [!DNL AJO B2B Edition] > Administración > Configuración de alertas de ventas

**Navegación de la interfaz de usuario:** [!DNL AJO B2B Edition] > Administración > Perspectivas de ventas de CRM > Configurar

**Detalles de configuración de clave:**

- Configurar plantillas de correo electrónico de alertas de ventas: incluye estado de grupo de compra, personalidades comprometidas, puntuación de participación y acciones siguientes recomendadas
- Definir reglas de enrutamiento de alertas: qué representantes de ventas o equipos reciben alertas en función de la propiedad de la cuenta, el territorio o el interés de la solución
- Instalar y configurar las perspectivas de ventas de CRM para [!DNL Salesforce] o [!DNL Dynamics 365]
- Asigne datos de grupo de compra a objetos CRM para que las ventas puedan ver la composición del grupo de compra, la participación y el progreso del recorrido dentro de su flujo de trabajo CRM
- Si lo desea, puede configurar conexiones de destino de cuenta para activar audiencias de cuenta en [!DNL LinkedIn] (para publicidad de ABM), [!DNL Marketo Engage] (para seguimiento de nivel de cliente potencial) u otros destinos B2B

**Documentación de Experience League:**

- [Correos electrónicos de alerta de ventas](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sales-alert-email)
- [Perspectivas de ventas de CRM](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/crm-sales-insights)
- [Información general sobre los destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Destino de audiencias coincidentes de LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)

### Fase 5: Creación de informes y optimización

**Funciones de la aplicación:** [!DNL AJO B2B]: Paneles de B2B Analytics

En esta fase se establece el marco de informes y análisis para medir el rendimiento del grupo de compra, la efectividad del recorrido de cuentas y el impacto en la canalización. [!DNL AJO B2B Edition] proporciona paneles de analytics integrados; [!DNL CJA B2B Edition] (si tiene licencia) amplía el análisis con perspectivas más profundas a nivel de cuenta en canales múltiples.

#### Decisión: enfoque de informes

¿Qué herramientas de análisis se deben configurar para la monitorización continua del rendimiento?

| Opción | Cuándo elegir | Consideraciones |
| --- | --- | --- |
| Solo paneles de [!DNL AJO B2B] | Los paneles integrados de [!DNL AJO B2B Edition] son suficientes para comprar métricas de recorridos y grupos | El más rápido de configurar; cubre las métricas principales B2B; capacidad limitada de análisis personalizado |
| [!DNL AJO B2B] paneles + [!DNL CJA B2B Edition] | La organización necesita un análisis en canales múltiples más profundo, un análisis de grupo de compra, una correlación de oportunidades y una atribución personalizada | Requiere licencia de [!DNL CJA B2B Edition]; la más completa; admite el análisis de forma libre a nivel de cuenta |
| Paneles de [!DNL AJO B2B] + informes de CRM | La organización prefiere centralizar los informes de canalización en CRM junto con las métricas de grupo de compra | Requiere desarrollo de tableros CRM; combina métricas de marketing y ventas en un solo lugar; se limita a las capacidades de informes CRM |

**Navegación de la interfaz de usuario:** [!DNL AJO B2B Edition] > Paneles > Información general de participación / Tablero inteligente

**Detalles de configuración de clave:**

- Acceda al tablero de participación de [!DNL AJO B2B] para monitorizar las puntuaciones de participación del grupo de compra, las tasas de integridad y la distribución de etapas
- Acceda al tablero inteligente para obtener perspectivas impulsadas por IA sobre la preparación de la cuenta y la calidad de la canalización
- Si usa [!DNL CJA B2B Edition]: configure una conexión CJA basada en cuentas que incluya [!DNL AJO B2B] conjuntos de datos, configure una vista de datos B2B con contenedores de grupo de compra y cuenta y genere un análisis del espacio de trabajo para la progresión del grupo de compra, la correlación de oportunidades y la atribución
- Definir la cadencia de los informes: revisiones semanales del rendimiento del grupo de compra, análisis mensual del impacto de la canalización, optimización trimestral del programa
- Cree anotaciones para eventos significativos (lanzamientos de campañas, actualizaciones de contenido, cambios en el modelo de puntuación) para correlacionarlos con las tendencias de rendimiento

**Documentación de Experience League:**

- [Paneles de análisis B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/buying-groups-dashboard)
- [Tablero de participación](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/engagement-dashboard)
- [Panel inteligente](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/intelligent-dashboard)
- [Información general sobre CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

## Consideraciones sobre la implementación

Las secciones siguientes abarcan protecciones, escollos comunes, prácticas recomendadas y decisiones de compensación que se deben tener en cuenta durante la implementación.

### Protecciones y límites

- [!DNL AJO B2B Edition] límites de recorrido de cuenta, incluidos el máximo de recorridos simultáneos y el máximo de cuentas por recorrido, siga las [!DNL AJO B2B Edition] protecciones de producto: [protecciones B2B de AJO](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [!DNL RT-CDP B2B Edition] admite hasta 50 clases de esquema B2B y sigue las protecciones estándar de perfil y segmentación: [protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- La evaluación de audiencias de cuenta funciona según programaciones por lotes; no se admiten actualizaciones de audiencias de cuenta en tiempo real para todos los tipos de segmentos: [Protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- La ingesta del conector de origen B2B tiene intervalos de programación mínimos (normalmente 15 minutos para [!DNL Marketo], que varían para las fuentes CRM) — [Protecciones de ingesta](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- Las superficies de canal de correo electrónico están limitadas a 10 por tipo de canal por zona protegida — [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)

### Peligros comunes

- **Definir demasiados roles por grupo de compra:** La sobreespecificación de roles (por ejemplo, requerir de 8 a 10 personalidades distintas) hace que sea casi imposible que los grupos de compra alcancen los umbrales de integridad. Comience con 3-5 funciones esenciales y expanda a medida que el modelo madure.
- **Estableciendo umbrales de puntuación de participación demasiado altos o demasiado bajos:** Si los umbrales son demasiado altos, no se califican grupos de compra, lo que hace que la canalización se vea privada de acceso. Si es demasiado bajo, las cuentas no calificadas inundan las ventas. Comience con el análisis de datos históricos (si está disponible) e itere en función de los comentarios sobre las ventas.
- **Se ignora la calidad de la resolución de persona a cuenta:** Si las personas no están vinculadas correctamente a las cuentas, los grupos compradores tendrán miembros que faltan incluso cuando participen las personas adecuadas. Invierta en calidad de resolución de identidades antes de lanzar recorridos de grupo de compra.
- **Contactos con mensajes excesivos en varios grupos de compras:** Un solo contacto puede tener roles en varios grupos de compras (por ejemplo, un CTO que sea evaluador técnico para compras tanto de CRM como de Data Platform). Sin administración de frecuencias, esta persona recibe correos electrónicos de todos los recorridos activos. Implementar reglas de recorrido cruzado.
- **Descuidando la habilitación de ventas:** Los equipos de ventas deben entender cómo interpretar los datos de los grupos de compras, las puntuaciones de participación y las alertas de ventas. Sin formación ni adopción, el traspaso de marketing a ventas falla independientemente de la calidad de los datos.
- **Tratar recorridos de cuenta como recorridos de persona:** Los recorridos de cuenta funcionan a nivel de cuenta y envían correos electrónicos a personas dentro de los grupos de compra de la cuenta. El diseño del recorrido debe tener en cuenta que varias personas reciben mensajes por cada ejecución de nodo de cuenta, lo que es fundamentalmente diferente de los recorridos de nivel de persona [!DNL AJO].

### Prácticas recomendadas

- **Empiece con un interés de solución y amplíe**: pruebe que el modelo funciona para un movimiento de compra antes de escalarlo a varios intereses de solución. Esto permite al equipo refinar las plantillas de funciones, los modelos de puntuación y el contenido antes de añadir complejidad.
- **Alinear los roles del grupo de compra con el proceso de ventas de CRM** — Asignar los roles del grupo de compra a los perfiles que el equipo de ventas ya reconoce. Utilice el mismo idioma (comprador económico, campeón, etc.) así que el traspaso es intuitivo.
- **Implementar un bucle de comentarios con ventas**: recopile regularmente comentarios de ventas sobre la calidad de las cuentas aptas para marketing. Utilice estos comentarios para ajustar los umbrales de puntuación de participación y los criterios de calificación de funciones.
- **Diseñe contenido para funciones, no solo para etapas**: las diferentes funciones de los grupos de compra necesitan contenido diferente: los ejecutivos quieren ROI e impacto estratégico, los evaluadores técnicos quieren detalles de arquitectura e integración, los usuarios finales quieren demostraciones de facilidad de uso. Asigne activos de contenido a funciones para lograr una nutrición más eficaz.
- **Configurar perspectivas de ventas de CRM temprano** — No espere hasta que el recorrido completo esté activo para implementar la visibilidad de CRM. Los equipos de ventas deben comprobar la formación anticipada de los datos del grupo de compra para proporcionar comentarios sobre la precisión de las funciones y la segmentación de cuentas.
- **Use los pasos de espera de forma estratégica**: los ciclos de compra B2B son largos. Los pasos de espera del recorrido de la cuenta deben reflejar esta realidad (intervalos de 5 a 14 días entre toques), en lugar de la urgencia del estilo del consumidor (de 1 a 3 días).
- **Supervisar la velocidad de interacción, no solo la puntuación de participación**: Un grupo comprador que pasa de la puntuación 20 a 80 en dos semanas indica una intención más fuerte que una que llega a 80 en seis meses. Configure la puntuación y la calificación para tener en cuenta la velocidad.

### Decisiones de compensación

Las siguientes compensaciones deben evaluarse en función de las necesidades específicas de su organización.

#### Compra de la integridad del grupo frente al volumen de canalización

Exigir que se llenen todas las funciones antes de calificar a un grupo comprador maximiza la calidad de la canalización, pero puede limitar seriamente el volumen de cuentas calificadas, especialmente para nuevos productos o mercados donde la base de datos de la organización tiene una cobertura limitada.

- **El umbral de integridad más alto favorece:** Calidad de la canalización; las ventas reciben grupos de compra completamente formados; tasas de ganancia más altas por cuenta
- **El umbral de integridad más bajo favorece:** Volumen de canalización; más cuentas alcanzan ventas; mayor cobertura; mayor volumen pero potencialmente menor calidad
- **Recomendación:** Comience con un umbral moderado (cobertura de rol del 60 al 70%) y ajuste según los datos de tasa de ganancia real. Para mercados establecidos con buena cobertura de datos, aumente hasta un 80% o más. Para nuevos mercados, acepte inicialmente el 50-60% y utilice campañas de integridad de grupos de compra para llenar vacíos.

#### Granularidad de puntuación frente a simplicidad operativa

Los modelos de puntuación muy granulares (con decenas de tipos de actividades, ponderación de la actualización y puntuación específica de funciones) proporcionan señales de calificación más precisas, pero son más difíciles de mantener, explicar y solucionar problemas.

- **Mayor granularidad favorece:** Precisión de la calificación; diferenciación matizada entre cuentas; mejor alineación con procesos de compra complejos
- **Menor granularidad favorece:** Simplicidad operativa; más fácil de mantener y explicar a las ventas; implementación más rápida; menos casos puntuales
- **Recomendación:** Comience con un modelo de puntuación simple (de 10 a 15 tipos de actividades, valores de punto uniformes) y agregue complejidad únicamente cuando el modelo simple no pueda diferenciar la calidad de la cuenta. Documente el modelo de puntuación para la alineación de ventas.

#### Un solo recorrido frente a varios recorridos especializados

Un recorrido de cuentas único y completo que gestiona todas las etapas e intereses de la solución en un solo lienzo proporciona un control unificado, pero puede resultar difícil de manejar. Múltiples recorridos especializados (uno por etapa o interés en la solución) son más sencillos individualmente, pero más difíciles de coordinar.

- **Un solo recorrido favorece:** vista holística; más fácil asegurar la sincronización y la mensajería coherentes; más fácil de supervisar; un solo lugar para toda la lógica
- **Varios recorridos favorecen:** Modularidad; es más fácil actualizar una etapa sin afectar a otras; distintos equipos pueden tener diferentes recorridos; diseño de lienzo más limpio
- **Recomendación:** Para la opción A, es apropiado un solo recorrido. Para las opciones B y C, utilice un recorrido de &quot;orquestación&quot; principal que dirija las cuentas a recorridos secundarios especializados por interés de solución o fase de compra.

## Documentación relacionada

Los siguientes recursos proporcionan detalles adicionales sobre las aplicaciones y capacidades a las que se hace referencia en esta guía.

### [!DNL AJO B2B Edition]

- [Inicio de la documentación de AJO B2B edition](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [Resumen de grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [Intereses de solución](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [Plantillas de roles](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [Creación de grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)
- [Fases del grupo de compras](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Resumen de recorridos de cuenta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [Nodos del recorrido de cuentas](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [Correos electrónicos de alerta de ventas](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sales-alert-email)
- [Perspectivas de ventas de CRM](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/crm-sales-insights)

### Correo electrónico y contenido B2B

- [Creación de correo electrónico B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/email-authoring)
- [Creación de SMS en AJO B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sms-authoring)
- [Asistente de IA para la creación de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/ai-assistant-emails)

### Análisis y paneles B2B

- [Panel de grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/buying-groups-dashboard)
- [Tablero de participación](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/engagement-dashboard)
- [Panel inteligente](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/intelligent-dashboard)
- [Información general sobre CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### [!DNL RT-CDP B2B Edition]

- [Información general sobre RT-CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)
- [Esquemas B2B en Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Audiencias de cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [Conector de origen de Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)

### Base de datos

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Resumen de orígenes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)

### Configuración de canal

- [Introducción a la configuración de correo electrónico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configuración del canal SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### Gobernanza de datos y privacidad

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

### Destinos

- [Información general sobre los destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Destino de audiencias coincidentes de LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)

### Guardas

- [Protecciones del perfil del cliente en tiempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [Protecciones de ingesta](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [protecciones de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)

### Tutoriales y introducción

- [Introducción a AJO B2B edition](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [Tutorial de B2B edition de RT-CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-tutorial)
