---
title: Audience Activation B2B
description: Obtenga información sobre cómo activar audiencias B2B basadas en cuentas en canales web, de correo electrónico y de publicidad.
solution: Real-Time Customer Data Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '7567'
ht-degree: 0%

---


# Activación de audiencia B2B

Esta guía proporciona una referencia de implementación completa para activar audiencias B2B basadas en cuentas mediante [!DNL Adobe Real-Time Customer Data Platform] ([!DNL RT-CDP]) B2B edition. Está diseñado para arquitectos de soluciones, tecnólogos de marketing e ingenieros de implementación que necesiten crear, evaluar y activar audiencias a nivel de cuenta en canales web, de correo electrónico, de publicidad y CRM.

Abarca el ciclo de vida completo, desde la unificación del perfil de la cuenta hasta la evaluación y activación de audiencias, pasando por destinos específicos de B2B como [!DNL Marketo Engage], [!DNL LinkedIn] y sistemas CRM. Todos los enfoques de implementación viables se presentan con compensaciones y directrices de decisión para ayudarle a seleccionar la ruta correcta para su organización.

## Resumen del caso de uso

Los equipos de marketing B2B necesitan segmentar y activar audiencias en el nivel de la cuenta en lugar de en el nivel de persona individual. A diferencia de la activación de audiencia B2C, en la que la unidad de segmentación es un perfil de consumidor único, la activación de audiencia B2B requiere comprender la relación entre las personas y las cuentas a las que pertenecen, evaluar la pertenencia a la audiencia en función de atributos de nivel de cuenta combinados con señales de participación de nivel de persona y enviar esas audiencias a destinos que admitan la segmentación basada en cuentas.

[!DNL RT-CDP] B2B edition amplía el estándar [!DNL Real-Time Customer Data Platform] con clases XDM especializadas para cuentas, oportunidades y campañas, junto con la resolución de identidad B2B que asigna relaciones persona a cuenta. Esto permite a los especialistas en marketing crear audiencias de cuenta que combinen datos firmográficos (industria, ingresos, recuento de empleados), datos tecnográficos (pila de tecnología, uso de productos) y datos de comportamiento (visitas web, participación por correo electrónico, asistencia a eventos) de las personas asociadas con esas cuentas.

Las audiencias de cuentas activadas alimentan los casos de uso en toda la funnel de generación de demanda: campañas de sensibilización de funnel en [!DNL LinkedIn] y publicidad de visualización, programas de nutrición de funnel en [!DNL Marketo Engage] y activación de ventas de funnel de nivel inferior mediante la integración de CRM. Las audiencias de supresión de cuentas evitan el gasto desperdiciado al excluir a los clientes existentes, las cuentas cerradas y perdidas o las cuentas que ya están en ciclos de ventas activos.

## Objetivos empresariales clave

Este patrón de caso de uso admite los siguientes objetivos empresariales.

### Aumentar la generación de posibles clientes

Genere posibles clientes más cualificados para el canal de ventas a través de formularios, eventos, contenido y participación multicanal.

**KPI:** clientes potenciales, coste por cliente potencial, conversión de cliente potencial

[Más información sobre cómo aumentar la generación de posibles clientes](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### Mejore la calificación y conversión de posibles clientes

Aumente la calidad del posible cliente y acelere la progresión de la canalización mediante la puntuación, la nutrición y el seguimiento personalizado.

**KPI:** conversión de posibles clientes, conversión de posibles clientes/posibles clientes, eficiencia

[Obtenga más información sobre cómo mejorar la calificación y conversión de posibles clientes](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### Adquisición de nuevos clientes

Amplíe la base de clientes con campañas de adquisición dirigidas, audiencias similares y optimización de medios de pago.

**KPI:** nuevos clientes, coste de adquisición del cliente, conversión de cliente potencial/posible cliente

[Más información sobre la adquisición de nuevos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Optimización del gasto y el ROI de marketing

Mejore el retorno de la inversión en marketing mediante una mejor segmentación, atribución, supresión de audiencias y asignación de presupuesto.

**KPI:** ahorros en costos, costo de adquisición de clientes, ingresos incrementales

## Casos de uso tácticos de ejemplo

Los siguientes escenarios ilustran cómo se puede aplicar este patrón en la práctica.

- **Publicidad basada en cuentas en[!DNL LinkedIn]**: cuentas de Target que coinciden con su perfil de cliente (ICP) ideal con contenido patrocinado y campañas de InMail en [!DNL LinkedIn], mediante listas de cuentas activadas desde [!DNL RT-CDP] B2B edition
- **[!DNL Marketo Engage]segmentación de programas de Nutrición** — Activar audiencias de cuenta para [!DNL Marketo Engage] para inscribir posibles clientes y contactos asociados en flujos de Nutrición segmentados según criterios de calificación de nivel de cuenta
- **Sincronización de lista de cuentas de CRM**: inserte listas de cuentas calificadas en [!DNL Salesforce] o [!DNL Microsoft Dynamics] para la visibilidad del equipo de ventas, la asignación de territorios y los flujos de trabajo de prospección de salida
- **Supresión de cuentas para medios pagados**: elimine clientes existentes, cuentas ganadas cerradas o cuentas en ciclos de ventas activos de campañas de adquisición pagada para reducir el gasto desperdiciado
- **Segmentación de cuentas basada en intención**: combine señales de intención de terceros con datos de participación de origen a nivel de cuenta para identificar y activar audiencias de cuentas en el mercado
- **Venta cruzada de productos a cuentas existentes**: cree audiencias de cuentas con una línea de productos pero no con otra y, a continuación, actívela en canales de correo electrónico y publicidad para campañas de venta cruzada
- **Segmentación de eventos y seminarios web**: active las audiencias de cuenta en los canales de publicidad y correo electrónico para impulsar el registro de eventos desde las cuentas de destino
- **Campañas de desplazamiento competitivo** — Cuentas de Target que utilizan productos de la competencia con mensajes personalizados activados a través de canales de publicidad y correo electrónico
- **Participación de cuenta por niveles**: Segmente las cuentas en niveles de participación (alta, media, baja) según la actividad agregada a nivel de persona y active campañas diferenciadas para cada nivel
- **Audiencias de marketing conjunto de socios**: comparta segmentos de audiencia de cuenta con socios de canal o programas de marketing conjunto a través de destinos de almacenamiento en la nube

## Indicadores clave de rendimiento

Los siguientes KPI ayudan a medir el éxito de este patrón de caso de uso.

| KPI | Descripción | Método de medición |
| --- | --- | --- |
| Alcance de cuenta | Número de cuentas de destinatario contactadas a través de canales de activación | Seguimiento de cuentas únicas activadas por destino |
| Tasa de participación de cuenta | Porcentaje de cuentas activadas que muestran señales de participación | Medir la participación a nivel de persona agregada a la cuenta |
| Influencia de canalización | Canalización de ingresos atribuida a campañas de activación basadas en cuentas | Rastrear oportunidades creadas a partir de audiencias de cuentas activadas |
| Costo por cuenta comprometida | Gasto en marketing dividido por el número de cuentas que muestran participación | Cálculo entre los costes de canal de correo electrónico y publicidad |
| Tasa de conversión de posibles clientes | Porcentaje de posibles clientes de cuentas activadas que se convierten en oportunidades | Rastrear conversión de posible cliente a oportunidad para audiencias activadas |
| Ahorro de supresión de audiencia | Coste evitado al suprimir cuentas no aptas de campañas pagadas | Mida la reducción de gasto de las audiencias de supresión |
| Cobertura de cuenta | Porcentaje del mercado total accesible (TAM) cubierto por audiencias activadas | Comparar cuentas activadas con el universo ICP total |

## Patrón de caso de uso

**Activación de audiencia B2B**

Active audiencias B2B basadas en cuentas en los canales web, de correo electrónico y de publicidad.

**Cadena de funciones:** Enriquecimiento de perfiles de cuenta > Evaluación de audiencias de cuenta > Configuración de destino > Audience Activation > Monitorización

## Aplicaciones

Las siguientes aplicaciones se utilizan para implementar este patrón de caso de uso.

- **[!DNL Real-Time CDP]B2B edition**: plataforma principal para la unificación de perfiles de cuenta, resolución de identidades B2B, evaluación de audiencias de cuenta, configuración de destino específica B2B y activación de audiencias de cuenta
- **[!DNL Adobe Experience Platform] (AEP)**: infraestructura básica para el modelado de datos XDM B2B, la ingesta de datos desde CRM y fuentes de automatización de marketing, servicio de identidad y administración
- **[!DNL Marketo Engage]**: destino principal de automatización de marketing B2B para programas de nutrición de posibles clientes, puntuación y ejecución de campañas alimentadas por audiencias de cuenta activadas

## Funciones básicas

Para este patrón de caso de uso, deben existir las siguientes capacidades básicas. Para cada función, el estado indica si suele ser necesaria, si se supone que está preconfigurada o si no es aplicable.

| Función base | Estado | Lo que debe estar en su lugar | Referencia de Experience League |
| --- | --- | --- | --- |
| Administración y gobernanza | Requerido | Zona protegida aprovisionada con [!DNL RT-CDP] B2B edition habilitado. Funciones configuradas para la administración de datos B2B, la creación de audiencias y la activación de destino. Se aplican políticas ABAC si los datos de la cuenta contienen campos restringidos. | [Resumen de zonas protegidas](https://experienceleague.adobe.com/es/docs/experience-platform/sandbox/home), [Resumen de control de acceso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Modelado y preparación de datos | Requerido | Esquemas XDM B2B configurados con clases de cuenta empresarial XDM, oportunidad empresarial XDM, campaña empresarial XDM y perfil individual XDM. Grupos de campos B2B aplicados a atributos de cuenta, relaciones persona-cuenta y datos de oportunidad. Conjuntos de datos creados y habilitados para perfil para cada entidad B2B. Relaciones de esquema definidas entre entidades de cuenta, persona, oportunidad y campaña. | [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [esquemas B2B en Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b) |
| Fuentes de datos y recopilación | Requerido | Conectores de Source configurados para CRM ([!DNL Salesforce], [!DNL Microsoft Dynamics]) y automatización de marketing ([!DNL Marketo Engage]) para ingerir datos de cuenta, persona, oportunidad y campaña. Canalizaciones de ingesta por lotes o de flujo continuo activas. Asignaciones de preparación de datos configuradas para transformar datos de origen en esquemas XDM B2B. | [Resumen de fuentes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home), [conector de Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| Configuración de identidad y perfil | Requerido | Áreas de nombres de identidad B2B configuradas para identificadores de cuenta (ID de cuenta, ID de cuenta CRM) e identificadores de persona (correo electrónico, ID de contacto CRM, ID de posible cliente de Marketo). Las relaciones persona a cuenta se resuelven mediante la resolución de identidades B2B. Políticas de combinación configuradas para la unificación de perfiles de cuenta. | [Descripción general del servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [B2B edition de Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b) |
| Definición de audiencia y segmentación | Requerido | Definiciones de audiencias de nivel de cuenta creadas con atributos de cuenta, atributos de persona y datos de actividad. Programaciones de evaluación configuradas para audiencias de cuenta. Audiencias de supresión definidas para la exclusión de cuentas no aptas. | [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [audiencias de la cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences) |

## Funciones de soporte

Las siguientes capacidades aumentan este patrón de caso de uso, pero no son necesarias para la ejecución principal.

| Función de apoyo | Estado | Por qué importa | Referencia de Experience League |
| --- | --- | --- | --- |
| Creación de atributos calculados/derivados | Recomendado | Las puntuaciones de participación agregadas, el valor de duración y las métricas de actividad a nivel de cuenta mejoran la precisión de la audiencia. Los atributos calculados pueden resumir eventos de nivel de persona (aperturas de correo electrónico, visitas web, descargas de contenido) en el nivel de cuenta para su uso en la segmentación. | [Resumen de atributos calculados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Administración del ciclo de datos | Recomendado | Las políticas de retención de datos B2B garantizan la limpieza de los datos de cuentas y oportunidades obsoletos. La administración de consentimientos para los contactos B2B garantiza el cumplimiento de las regulaciones de marketing por correo electrónico. Las políticas de caducidad del conjunto de datos impiden la acumulación de datos de sincronización de CRM obsoletos. | [Información general sobre la administración avanzada del ciclo de vida de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Etiquetado y aplicación del uso de datos | Incluido | Los datos de la cuenta B2B suelen contener restricciones contractuales (cifras de ingresos, recuentos de empleados de proveedores externos). Las etiquetas de uso de datos impiden que los atributos de cuenta restringidos se activen en destinos no autorizados. Las políticas de gobernanza garantizan que los campos PII de los registros de contacto se gestionen correctamente durante la activación. | [Resumen de control de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Monitorización y observabilidad | Incluido | La supervisión de los flujos de datos de CRM y [!DNL Marketo Engage] conector de origen garantiza que los datos de la cuenta permanezcan actuales. La supervisión de la activación del destino confirma que las audiencias se han entregado correctamente a [!DNL LinkedIn], [!DNL Marketo] y a los destinos de CRM. Las reglas de alerta detectan errores de ingesta que podrían causar datos de cuenta obsoletos. | [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [Supervisar flujos de datos de destino](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations) |
| Informes y análisis | Recomendado | [!DNL CJA] B2B edition proporciona análisis de nivel de cuenta, que incluye el alcance de la audiencia, la participación y la influencia de la canalización. La atribución basada en cuentas ayuda a medir el impacto de las campañas de activación en la progresión de la oportunidad y los ingresos. | [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funciones de aplicación

Este plan utiliza las siguientes funciones del Catálogo de funciones de la aplicación. Las funciones se asignan a fases de implementación en lugar de pasos numerados.

### [!DNL Real-Time CDP] B2B edition ([!DNL RT-CDP] B2B)

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Unificación del perfil de cuenta | Fase 1: enriquecimiento del perfil de cuenta | Consolide los datos de cuenta de CRM, automatización de marketing y fuentes de terceros en perfiles de cuenta unificados mediante clases de esquema XDM B2B |
| Resolución de identidad B2B | Fase 1: enriquecimiento del perfil de cuenta | Resolver relaciones persona a cuenta mediante identificadores principales, asignación de contactos y posibles clientes a sus cuentas asociadas |
| Evaluación de audiencia de cuenta | Fase 2: Evaluación de audiencias de cuenta | Evaluar la pertenencia a segmentos en el nivel de cuenta combinando atributos de cuenta, atributos de persona y datos de actividad de persona |
| Configuración de destino de cuenta | Fase 3: Configuración del destino | Configure conexiones a destinos específicos de B2B ([!DNL Marketo Engage], [!DNL LinkedIn], CRM, almacenamiento en la nube) con asignación de campos de nivel de cuenta |
| Audience Activation de cuenta | Fase 4: Audience Activation | Publicar audiencias basadas en cuentas en destinos configurados para segmentación, supresión o sincronización con CRM |
| Integración de [!DNL Marketo Engage] | Fase 3: Configuración del destino | Configurar el flujo de datos bidireccional con [!DNL Marketo Engage] mediante conectores de origen y destino B2B nativos |
| Gobernanza de datos B2B | Fase 5: Gobernanza y monitorización | Aplique políticas de uso de datos y consentimiento en la activación de datos de la cuenta B2B para evitar la exposición de datos no autorizados |

### [!DNL Real-Time CDP] ([!DNL RT-CDP]): funciones estándar

| Función | Fase de implementación | Descripción |
| --- | --- | --- |
| Evaluación de audiencia | Fase 2: Evaluación de audiencias de cuenta | Motor de evaluación subyacente para audiencias de cuenta que admite la evaluación por lotes de definiciones de segmentos de nivel de cuenta |
| Configuración de destino | Fase 3: Configuración del destino | Infraestructura de conexión de destino principal utilizada por la configuración de destino específica de B2B |
| Audience Activation | Fase 4: Audience Activation | Infraestructura de flujo de datos de activación principal utilizada por la activación de audiencia de cuenta |
| Cumplimiento del consentimiento y la gobernanza | Fase 5: Gobernanza y monitorización | Aplicar preferencias de consentimiento y políticas de uso de datos en el momento de la activación |

## Prerrequisitos

Complete lo siguiente antes de iniciar la implementación.

- [ ] [!DNL RT-CDP] licencia de B2B edition aprovisionada y activada en la organización
- [ Se puede acceder al sistema CRM ] ([!DNL Salesforce] o [!DNL Microsoft Dynamics]) con credenciales de API para la configuración del conector de origen
- [ ] [!DNL Marketo Engage] instancia aprovisionada con acceso a API (Munchkin ID, ID de cliente, Secreto de cliente) si se usa [!DNL Marketo] como destino
- [ ] [!DNL LinkedIn] cuenta del administrador de campañas con capacidad de audiencias coincidentes si se usa [!DNL LinkedIn] como destino
- [ ] esquemas XDM B2B creados con clases de cuenta, persona, oportunidad y campaña (F2)
- [ ] conectores de Source configurados e ingiriendo activamente datos de CRM y automatización de marketing (F3)
- [ ] relaciones de identidad de persona a cuenta resueltas y perfiles de cuenta unificados (F4)
- [ ] convenciones de nomenclatura de cuentas y taxonomía acordadas para definiciones de audiencia
- [ ] directivas de gobernanza de datos definidas para clasificaciones de confidencialidad de datos de nivel de cuenta

## Opciones de implementación

Las siguientes opciones describen diferentes enfoques para implementar este patrón de caso de uso. Revise cada opción y seleccione la que mejor se ajuste a sus necesidades.

### Opción A: transmitir la activación de audiencia a [!DNL Marketo Engage]

**Ideal para:** organizaciones que utilizan [!DNL Marketo Engage] como su plataforma principal de automatización de marketing B2B y que necesitan actualizaciones de miembros de audiencia casi en tiempo real para programas de nutrición de déclencheur, actualizar puntuaciones de posibles clientes o modificar la pertenencia a campañas cuando las cuentas califiquen o descalifiquen.

**Cómo funciona:**

Esta opción usa el conector de destino nativo [!DNL Marketo Engage] en [!DNL RT-CDP] para transmitir los cambios de pertenencia de la audiencia de la cuenta directamente a [!DNL Marketo Engage]. Cuando una cuenta califica para un segmento de audiencia o sale de él, los posibles clientes y contactos asociados en [!DNL Marketo] se actualizan con los atributos de pertenencia al segmento. [!DNL Marketo] las campañas inteligentes pueden generar déclencheur en función de estos cambios de pertenencia.

El destino [!DNL Marketo Engage] es un destino de flujo continuo, lo que significa que los cambios en la pertenencia a audiencias se envían de forma incremental a medida que se producen en lugar de en lotes programados. Esto proporciona un tiempo de acción más rápido para las campañas que necesitan responder a los cambios de calificación de cuentas. Las asignaciones de campos conectan atributos de perfil de [!DNL RT-CDP] a [!DNL Marketo] campos de posible cliente/contacto, lo que permite enriquecer los registros de [!DNL Marketo] con los datos de nivel de cuenta de [!DNL RT-CDP].

**Consideraciones clave:**

- Requiere una suscripción activa de [!DNL Marketo Engage] con acceso a API
- La activación de streaming envía actualizaciones incrementales, no instantáneas de audiencia completas
- Los registros de nivel de persona en [!DNL Marketo] se actualizan, no los registros de nivel de cuenta directamente
- [!DNL Marketo] campañas inteligentes deben configurarse para que actúen en las actualizaciones de los campos de abono a segmentos

**Ventajas:**

- Actualizaciones de miembros de audiencia casi en tiempo real en [!DNL Marketo]
- El conector bidireccional nativo simplifica la integración
- Las actualizaciones incrementales minimizan el volumen de transferencia de datos
- [!DNL Marketo] puede almacenar en déclencheur inmediatamente los programas según los cambios de audiencia

**Limitaciones:**

- Limitado a [!DNL Marketo Engage] como destino de activación
- Las restricciones de idoneidad para la evaluación de streaming se aplican a las definiciones de audiencia subyacentes
- Requiere la asignación entre [!DNL RT-CDP] audiencias de cuenta y [!DNL Marketo] registros de contacto o posible cliente
- Es posible que se necesite una lógica de programa [!DNL Marketo] compleja para traducir actualizaciones de nivel de persona en acciones de nivel de cuenta

**Experience League:**

- [Marketo Engage destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [Activar audiencias en el destino de Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage#activate)

### Opción B: activación de audiencia por lotes en plataformas publicitarias

**Ideal para:** Campañas de publicidad basadas en cuentas en [!DNL LinkedIn], redes de visualización u otras plataformas de publicidad donde las actualizaciones diarias de la audiencia son suficientes y el objetivo principal es el alcance y la concienciación a nivel de cuenta en lugar de la respuesta en tiempo real.

**Cómo funciona:**

Esta opción activa las audiencias de cuenta para los destinos de plataforma de publicidad ([!DNL LinkedIn] audiencias coincidentes, [!DNL Google] coincidencia de cliente, [!DNL Facebook] audiencias personalizadas o [!DNL The Trade Desk]) en una cadencia por lotes programada. El flujo de datos de activación exporta miembros de audiencia de cuenta con campos de identidad asignados (generalmente direcciones de correo electrónico con hash de contactos asociados) que la plataforma de publicidad utiliza para comparar con su base de usuarios.

Para [!DNL LinkedIn] específicamente, el destino de audiencias coincidentes [!DNL LinkedIn] acepta la coincidencia basada en el nombre de la empresa y el dominio, además de la coincidencia basada en el correo electrónico, lo que habilita la segmentación a nivel de cuenta real. Otras plataformas de publicidad suelen requerir identificadores de nivel de persona (correo electrónico, teléfono) de los contactos asociados con cuentas que cumplen los requisitos.

La activación por lotes se ejecuta en una programación configurable (diariamente, cada 6 horas, etc.) y exporta instantáneas de audiencia completas o cambios incrementales según el tipo de destino. Este enfoque es adecuado para campañas de sensibilización sostenidas en las que los requisitos de actualización de la audiencia se miden en horas en lugar de minutos.

**Consideraciones clave:**

- La actualización de la audiencia depende de la programación por lotes (normalmente diaria)
- Las plataformas Advertising tienen sus propias limitaciones de tasa de coincidencia
- [!DNL LinkedIn] admite la coincidencia en el nivel de cuenta; otras plataformas requieren identificadores en el nivel de persona
- Los formatos de archivo de exportación y los requisitos de identidad varían según el destino

**Ventajas:**

- Admite varias plataformas publicitarias simultáneamente
- El procesamiento por lotes gestiona eficazmente los grandes volúmenes de audiencia
- Las audiencias de supresión de cuentas reducen el gasto publicitario desperdiciado
- [!DNL LinkedIn] audiencias coincidentes habilita la segmentación a nivel de cuenta nativa

**Limitaciones:**

- Las actualizaciones de audiencia no son en tiempo real; la latencia depende de la programación por lotes
- Las tasas de coincidencia varían según la plataforma y los campos de identidad disponibles
- Algunas plataformas no admiten la coincidencia a nivel de cuenta real, solo a nivel de persona
- Requiere una configuración de destino independiente para cada plataforma publicitaria

**Experience League:**

- [Destino de audiencias coincidentes de LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
- [Destino de Customer Match de Google](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/google-customer-match)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)

### Opción C: activación basada en archivos en el almacenamiento en la nube

**Ideal para:** organizaciones que necesitan la máxima flexibilidad en la forma en que se consumen las audiencias de la cuenta en la fase posterior, incluidas las importaciones de CRM, el enriquecimiento del Data Warehouse, el uso compartido de datos de socios o las integraciones personalizadas en las que se prefiere un traspaso basado en archivos.

**Cómo funciona:**

Esta opción exporta audiencias de cuenta como archivos CSV, JSON o Parquet a destinos de almacenamiento en la nube ([!DNL Amazon S3], [!DNL Azure Blob Storage], [!DNL Google Cloud Storage], SFTP) en una cadencia programada. La exportación incluye atributos de cuenta, campos de nivel de persona de contactos asociados y metadatos de pertenencia a audiencias. Los sistemas descendentes consumen estos archivos a través de sus propios procesos de importación.

La activación basada en archivos ofrece el mayor control sobre el formato de exportación, la selección de campos y la programación. Admite exportación completa (instantánea de audiencia completa en cada ejecución) y exportación incremental (solo cambios desde la última ejecución). Este método se utiliza normalmente cuando el sistema de destino no tiene un conector de destino [!DNL RT-CDP] nativo o cuando la organización necesita procesar previamente o transformar los datos antes de cargarlos en el sistema de destino.

**Consideraciones clave:**

- Requiere la infraestructura de almacenamiento en la nube ([!DNL S3], [!DNL Azure Blob], [!DNL GCS] o SFTP)
- Deben crearse y mantenerse procesos de importación posteriores
- El formato de archivo (CSV, JSON, Parquet) debe coincidir con los requisitos del sistema descendente
- La programación de exportación debe alinearse con las ventanas de procesamiento descendente

**Ventajas:**

- Máxima flexibilidad en el consumo de datos de audiencia
- Admite cualquier sistema descendente que pueda leer archivos
- Control total sobre el formato, los campos y la programación de la exportación
- Puede servir a varios consumidores intermedios desde una sola exportación
- Admite modos de exportación completa e incremental

**Limitaciones:**

- Latencia máxima de todas las opciones (solo lote)
- Requiere crear y mantener flujos de trabajo de importación descendentes
- Sin integración nativa: se requiere un esfuerzo de desarrollo adicional
- La administración de archivos (limpieza, archivado) debe gestionarse por separado

**Experience League:**

- [Amazon S3 destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)
- [Destino de almacenamiento del blob de Azure](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/azure-blob)
- [Activar audiencias en destinos por lotes](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/api/connect-activate-batch-destinations)

### Opción D: Transmisión de la activación a los sistemas CRM

**Ideal para:** Casos de uso de alineación de ventas y marketing en los que los cambios de calificación de la cuenta deben reflejarse en CRM ([!DNL Salesforce] o [!DNL Dynamics]) en tiempo casi real para la visibilidad del equipo de ventas, las actualizaciones de asignación de territorios o los flujos de trabajo de ventas automatizados.

**Cómo funciona:**

Esta opción usa conectores de destino de streaming ([!DNL Salesforce] CRM, [!DNL Microsoft Dynamics]) para insertar los cambios de pertenencia de audiencia de cuenta directamente en los registros de cuenta o contacto de CRM. Cuando una cuenta cumple los requisitos de una audiencia o sale de ella, el registro CRM se actualiza con un campo personalizado que indica la pertenencia a un segmento. Los equipos de ventas pueden generar informes, vistas y alertas de CRM en función de estos campos.

El conector de flujo continuo envía actualizaciones incrementales a medida que se producen cambios en el abono a audiencia. Las asignaciones de campos conectan los atributos de cuenta y persona de [!DNL RT-CDP] a los campos CRM, lo que permite enriquecer los registros CRM con los datos unificados de [!DNL RT-CDP]. Este enfoque cierra el bucle entre inteligencia de marketing (calificación de cuentas) y ejecución de ventas (flujos de trabajo CRM).

**Consideraciones clave:**

- Requiere acceso a la API de CRM con permisos de escritura adecuados
- Los campos personalizados de CRM deben crearse para recibir los datos de pertenencia a audiencias
- El volumen de streaming debe estar dentro de los límites de velocidad de API de CRM
- La automatización del flujo de trabajo de CRM debe configurarse para actuar sobre las actualizaciones de campo

**Ventajas:**

- Actualizaciones de CRM casi en tiempo real para la visibilidad del equipo de ventas
- Activa flujos de trabajo automatizados CRM activados por cambios de audiencia
- Enriquece registros CRM con datos de cuenta unificada de [!DNL RT-CDP]
- Admite actualizaciones de campo a nivel de cuenta y de contacto

**Limitaciones:**

- Los límites de velocidad de API de CRM pueden acelerar las actualizaciones de gran volumen
- Requiere personalización CRM (campos personalizados, flujos de trabajo)
- Limitado a [!DNL Salesforce] y [!DNL Microsoft Dynamics] como conectores nativos
- Las restricciones de evaluación de streaming se aplican a las audiencias subyacentes

**Experience League:**

- [Destino de Salesforce CRM](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Microsoft Dynamics 365 destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/microsoft-dynamics-365)

### Comparación de opciones

En la tabla siguiente se comparan las características clave de cada opción de implementación.

| Criterios | Opción A: Flujo [!DNL Marketo] | Opción B: Lote Advertising | Opción C: Almacenamiento en la nube | Opción D: flujo CRM |
| --- | --- | --- | --- | --- |
| Mejor para | Activación del programa de nutrición | Publicidad basada en cuentas | Integración descendente flexible | Alineación de ventas y marketing |
| Complejidad | Baja | Medio | Medium-High | Medio |
| Latencia | Casi en tiempo real (minutos) | Lote (horas) | Lote (horas) | Casi en tiempo real (minutos) |
| Flexibilidad | Bajo ([!DNL Marketo] solamente) | Medium (plataformas publicitarias) | Alto (cualquier sistema descendente) | Baja (solo CRM) |
| Requiere | Licencia de [!DNL Marketo Engage] | Cuentas de plataforma de Advertising | Infraestructura de almacenamiento en nube | Acceso a API de CRM |
| Segmentación a nivel de cuenta | Mediante registros de persona | solo [!DNL LinkedIn] (nivel de persona de otros) | Configurable | Mediante registros de cuenta/contacto |
| Mantenimiento | Baja | Low-Medium | Alta | Medio |

### Elija la opción correcta

Utilice la siguiente guía de decisión para seleccionar el método de activación correcto:

1. **Si su objetivo principal es la nutrición de clientes potenciales B2B y usa[!DNL Marketo Engage]**, elija la Opción A. El conector de flujo nativo proporciona el tiempo de acción más rápido para los flujos de trabajo de automatización de marketing.

2. **Si su objetivo principal es el conocimiento basado en la cuenta y la generación de demanda a través de la publicidad**, elija la Opción B. [!DNL LinkedIn] Las audiencias coincidentes proporcionan la segmentación a nivel de cuenta más sólida. Utilice otras plataformas publicitarias para ampliar el alcance.

3. **Si necesita proporcionar audiencias de cuenta a sistemas sin conectores [!DNL RT-CDP] nativos**, o si necesita tener el máximo control sobre el formato de los datos y el procesamiento descendente, elija la opción C. También es la mejor opción para compartir datos con socios o ampliar el Data Warehouse.

4. **Si su objetivo principal es la habilitación de ventas y la visibilidad de CRM de las cuentas calificadas para marketing**, elija la Opción D. Esto cierra el bucle de transferencia de marketing a ventas actualizando los registros CRM en tiempo casi real.

La mayoría de las organizaciones B2B implementarán varias opciones simultáneamente, por ejemplo, la opción A para programas de nutrición, la opción B para publicidad de [!DNL LinkedIn] y la opción D para sincronización de CRM. Estas opciones no se excluyen mutuamente; la misma audiencia de cuenta se puede activar en varios destinos simultáneamente.

## Fases de implementación

Las siguientes fases describen el proceso paso a paso para implementar este patrón de caso de uso.

### Fase 1: Enriquecimiento del perfil de cuenta

Esta fase establece perfiles de cuenta unificados mediante la consolidación de datos de CRM, automatización de marketing y fuentes de terceros.

**Función de aplicación:** [!DNL RT-CDP] B2B: Unificación de perfiles de cuenta, [!DNL RT-CDP] B2B: Resolución de identidad B2B

**Lo que configurará:** Esta fase establece perfiles de cuenta unificados mediante la consolidación de datos de CRM, automatización de marketing y fuentes de terceros. La resolución de identidad B2B asigna relaciones persona a cuenta para que los datos de participación a nivel de persona (aperturas de correo electrónico, visitas web, descargas de contenido) se puedan acumular y utilizar en la evaluación de audiencias a nivel de cuenta. Esta fase se basa en las funciones básicas F2, F3 y F4, que ya deben estar establecidas.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: estrategia de identificador de cuenta**
>
>¿Qué identificador sirve como clave de cuenta principal en todos los sistemas?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| ID de cuenta de CRM (p. ej., [!DNL Salesforce] ID de cuenta) | CRM es el sistema de registro para cuentas | El enfoque más común. Garantiza la alineación entre [!DNL RT-CDP] y CRM. Requiere que todos los sistemas de origen hagan referencia al mismo ID de cuenta de CRM. |
>| ID de cuenta personalizada | Varias instancias de CRM o un maestro de cuentas propietario | Requiere una capa de asignación entre los ID de sistema de origen y el ID de cuenta canónico. Más flexible, pero añade complejidad. |
>| Número o dominio DUNS | El enriquecimiento de datos de terceros es la fuente de cuenta principal | Resulta útil cuando los proveedores de datos firmográficos son la fuente principal. Puede requerir una coincidencia aproximada para la resolución basada en el dominio. |

>[!NOTE]
>**Decisión: modelo de relación persona a cuenta**
>
>¿Cómo se asocian las personas (posibles clientes, contactos) con las cuentas?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Uno a uno (cada persona pertenece a una cuenta) | Modelo B2B simple con datos CRM limpios | Resolución directa. Más común para B2B de mercado medio. |
>| Varios a varios (las personas pueden pertenecer a varias cuentas) | Relaciones empresariales complejas, consultores o redes de socios | [!DNL RT-CDP] B2B edition admite esto de forma nativa. Aumenta la complejidad de la audiencia, pero refleja con precisión las relaciones del mundo real. |

**Navegación por la interfaz de usuario:** Plataforma > Perfiles > Examinar (para verificar perfiles de cuenta unificados)

**Detalles de configuración de clave:**

- Compruebe que los esquemas XDM B2B (cuenta empresarial de XDM, cuenta de persona empresarial de XDM) están en su lugar desde F2
- Confirme que los conectores de origen de CRM y [!DNL Marketo] están ingiriendo activamente datos de cuenta y persona de F3
- Validar que las relaciones persona a cuenta se resuelvan en el gráfico de identidades de F4
- Revisar la integridad del perfil de la cuenta explorando perfiles de cuenta de muestra

**Documentación de Experience League:**

- [Información general sobre Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b)
- [Esquemas B2B en Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Conector de Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Conector de Salesforce](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/crm/salesforce)

### Fase 2: Evaluación de la audiencia de cuenta

Esta fase define y evalúa las audiencias de nivel de cuenta mediante una combinación de atributos de cuenta, atributos de persona y datos de actividad de persona.

**Función de aplicación:** [!DNL RT-CDP] B2B: Evaluación de audiencia de cuenta, [!DNL RT-CDP]: Evaluación de audiencia

**Lo que configurará:** Esta fase define y evalúa las audiencias de nivel de cuenta mediante una combinación de atributos de cuenta, atributos de persona y datos de actividad de persona. Las audiencias de cuenta en [!DNL RT-CDP] B2B edition le permiten segmentar cuentas en función de características de firmografía (industria, ingresos, recuento de empleados) y del comportamiento de participación de las personas asociadas con esas cuentas.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: método de evaluación de audiencia**
>
>¿Con qué rapidez debe actualizar la pertenencia a audiencia de cuenta?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Evaluación por lotes (diaria) | Audiencias de Campaign actualizadas en una cadencia diaria, activaciones basadas en archivos o audiencias de plataformas de publicidad | La mayoría de las audiencias de cuenta utilizan la evaluación por lotes. Gestiona consultas complejas de varias entidades que combinan atributos de cuenta y persona. Suficiente para la mayoría de los casos de uso B2B en los que la actualización diaria es aceptable. |
>| Evaluación de streaming | Activación de [!DNL Marketo] o CRM donde se necesita una calificación en tiempo casi real | Las audiencias de la cuenta tienen una elegibilidad limitada para streaming. Solo las condiciones de atributo de cuenta simples cumplen los requisitos para la evaluación de streaming. Las condiciones de comportamiento a nivel de persona suelen requerir un lote. |

>[!NOTE]
>**Decisión: enfoque de definición de audiencia de cuenta**
>
>¿Cómo definirá los criterios de audiencia de la cuenta?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Solo atributos de cuenta | Segmentación firmográfica simple (industria, ingresos, región) | La implementación más rápida. Limitado a datos de nivel de cuenta. Se utiliza para la segmentación amplia. |
>| Atributos de cuenta + persona | Cuentas de segmentación en las que las personas asociadas coinciden con criterios específicos (cargo, departamento) | Direccionamiento más preciso. Combina datos fimográficos y demográficos. |
>| Cuenta + atributos de persona + actividad de persona | Segmentación de cuentas con contactos comprometidos (aperturas de correo electrónico, visitas web, descargas de contenido) | Más poderoso pero más complejo. Requiere datos de evento de comportamiento de F3. Normalmente requiere una evaluación por lotes. |
>| Composición de audiencia | Lógica de audiencia compleja que requiere operaciones de clasificación, división, exclusión o enriquecimiento | Utilice el lienzo de Composición de audiencia visual para audiencias de cuenta derivadas. Limitado a la evaluación por lotes. |

>[!NOTE]
>**Decisión: estrategia de audiencia de supresión**
>
>¿Qué cuentas deben excluirse de la activación?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Supresión de clientes existente | Campañas de adquisición dirigidas a cuentas netas nuevas | Excluir cuentas con suscripciones activas u oportunidades ganadas cerradas |
>| Supresión activa del ciclo de ventas | Evite interferir con las cuentas en el compromiso de ventas activo | Excluir cuentas con oportunidades abiertas por encima de una determinada etapa |
>| Supresión de participación reciente | Evitar mensajes excesivos de cuentas contactadas recientemente | Excluir cuentas comprometidas dentro de una ventana retrospectiva (por ejemplo, 30 días) |
>| Sin supresión | Campañas de sensibilización de la marca dirigidas a todas las cuentas aptas | Usar con precaución; puede provocar un gasto desperdiciado en cuentas no elegibles |

**Navegación de la interfaz de usuario:** Cliente > Audiencias > Crear audiencia > Generar regla (seleccione Cuenta como tipo de audiencia)

**Detalles de configuración de clave:**

- Seleccione &quot;Cuenta&quot; como tipo de audiencia al crear una nueva en el Generador de segmentos
- Los atributos de cuenta aparecen en la sección Cuenta del Generador de segmentos (sector, ingresos, estado de la cuenta)
- Los atributos de persona y las actividades se pueden agregar a través de la relación &quot;Personas&quot; en el generador de audiencias de cuenta
- Configure la programación de evaluación por lotes si aún no existe ninguna para la zona protegida
- Cree audiencias de segmentación (cuentas que incluir) y audiencias de supresión (cuentas que excluir)

**Documentación de Experience League:**

- [Audiencias de cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Composición de audiencia](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)

### Fase 3: Configuración del destino

Esta fase establece conexiones autenticadas con los destinos a los que se enviarán las audiencias de la cuenta.

**Función de aplicación:** [!DNL RT-CDP] B2B: Configuración de destino de cuenta, [!DNL RT-CDP] B2B: integración de [!DNL Marketo Engage], [!DNL RT-CDP]: configuración de destino

**Lo que configurará:** Esta fase establece conexiones autenticadas con los destinos de destino a los que se enviarán las audiencias de la cuenta. La configuración incluye la selección del destino en el catálogo, el suministro de credenciales de autenticación, la configuración de asignaciones de campos de nivel de cuenta y de nivel de persona, y la configuración de la programación de exportación. Cada tipo de destino tiene requisitos y capacidades únicos.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: selección de destino**
>
>¿Qué destino o destinos recibirán las audiencias de cuenta activadas?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| [!DNL Marketo Engage] | Nutrición de posibles clientes B2B, puntuación y ejecución de campañas | Conector de flujo nativo. Actualiza los registros de posibles clientes/contactos. Requiere credenciales de API [!DNL Marketo] (Munchkin ID, ID de cliente, Secreto de cliente). |
>| [!DNL LinkedIn] audiencias coincidentes | Publicidad basada en cuentas en [!DNL LinkedIn] | Admite la coincidencia de nombres de empresa y dominios para la segmentación a nivel de cuenta. Activación por lotes. Requiere acceso a [!DNL LinkedIn] Campaign Manager. |
>| [!DNL Salesforce] CRM | Activación de ventas y sincronización de lista de cuentas CRM | El conector de streaming actualiza los registros de cuenta o contacto. Requiere acceso a la API [!DNL Salesforce] con permisos de escritura. |
>| [!DNL Microsoft Dynamics 365] | Habilitación de ventas para organizaciones basadas en [!DNL Dynamics] | Conector de streaming. Requiere acceso a la API [!DNL Dynamics 365]. |
>| Almacenamiento en la nube ([!DNL S3], [!DNL Azure Blob], [!DNL GCS], SFTP) | Integraciones personalizadas, Data Warehouse, uso compartido entre socios | Exportación por lotes basada en archivos. Máxima flexibilidad, pero requiere un procesamiento posterior. |
>| Coincidencia de cliente de [!DNL Google] | Buscar y mostrar objetivos de publicidad | Coincidencia de nivel de persona por correo electrónico con hash. Activación por lotes. |
>| [!DNL The Trade Desk] | Publicidad en vídeo y visualización programática | Coincidencia a nivel de persona. Activación por lotes. |

>[!NOTE]
>**Decisión: estrategia de asignación de campos**
>
>¿Qué campos de cuenta y persona deben asignarse al destino?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Solo campos de identidad | Plataformas Advertising que solo necesitan identificadores coincidentes | Transferencia de datos mínima. El destino coincide en el correo electrónico o el dominio de la empresa. |
>| Identidad + atributos de la cuenta principal | CRM o [!DNL Marketo] donde el contexto de la cuenta mejora el direccionamiento | Incluya el sector, los ingresos, el recuento de empleados y el nivel de cuenta. Enriquezca los registros descendentes. |
>| Conjunto de atributos completo | Exportaciones de almacenamiento en la nube o Data Warehouse | Incluya todos los atributos relevantes de cuenta y persona. Carga útil de exportación más grande. |

**Navegación de la interfaz de usuario:** Conexiones > Destinos > Catálogo > Buscar destino > Configurar

**Detalles de configuración de clave:**

- Vaya al catálogo de destinos y seleccione el destino.
- Proporcione credenciales de autenticación específicas para el tipo de destino
- Configurar asignaciones de campos que conecten [!DNL RT-CDP] campos XDM a campos de destino
- Para [!DNL Marketo Engage]: proporcione el ID de Munchkin, el ID de cliente y el secreto de cliente
- Para [!DNL LinkedIn]: autorice mediante OAuth y seleccione la cuenta de publicidad [!DNL LinkedIn]
- Para el almacenamiento en la nube: proporcione un nombre de contenedor/contenedor, una ruta, un formato de archivo y credenciales.
- Para CRM: proporcione la URL de instancia, las credenciales de la API y el tipo de objeto de destino (cuenta o contacto)

**Donde las opciones difieren:**

**Para La Opción A ([!DNL Marketo Engage] Transmisión):**

Vaya a Destinos > Catálogo > Adobe > [!DNL Marketo Engage]. Configure las credenciales del ID de Munchkin y de la API. Asigne [!DNL RT-CDP] campos de identidad (correo electrónico) y atributos de perfil a [!DNL Marketo] campos de posible cliente. El destino gestiona automáticamente las actualizaciones de flujo incremental.

**Para Opción B (Lote De Advertising Platform):**

Vaya a Destinos > Catálogo > Advertising/Social > Seleccionar plataforma. Autorizar mediante OAuth. Configure la programación de exportación (recomendado: diario). Asigne identificadores de correo electrónico con hash y cualquier campo coincidente admitido. Para [!DNL LinkedIn], asigne además los campos Nombre de empresa y Dominio para la coincidencia a nivel de cuenta.

**Para La Opción C (Basada En Archivos De Almacenamiento En La Nube):**

Vaya a Destinos > Catálogo > Almacenamiento en la nube > seleccione un proveedor. Configure el bloque/contenedor, la plantilla de ruta de archivo y el formato de archivo (CSV, JSON o Parquet). Establezca la programación de exportación y elija exportación completa o incremental. Asigne todos los campos de cuenta y atributo de persona deseados.

**Para la opción D (transmisión CRM):**

Vaya a Destinos > Catálogo > CRM > seleccione [!DNL Salesforce] o [!DNL Dynamics]. Proporcione credenciales de API y URL de instancia. Asigne [!DNL RT-CDP] campos a los campos de cuenta o contacto de CRM. Asegúrese de que existan campos personalizados en CRM para recibir los datos de pertenencia a audiencias.

**Documentación de Experience League:**

- [Información general sobre los destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Marketo Engage destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [Destino de audiencias coincidentes de LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
- [Destino de Salesforce CRM](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Amazon S3 destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)

### Fase 4: Activación de audiencias

Esta fase publica las audiencias de cuenta evaluadas en los destinos configurados.

**Función de aplicación:** [!DNL RT-CDP] B2B: Audience Activation de cuenta, [!DNL RT-CDP]: Audience Activation

**Lo que configurará:** Esta fase publica las audiencias de cuenta evaluadas en los destinos configurados. Activation crea el flujo de datos que conecta la audiencia de la cuenta (origen) con el destino externo (destino), aplica las asignaciones de atributos e inicia la exportación según la programación configurada o el comportamiento de flujo. También configurará las audiencias de supresión para excluir de la activación las cuentas no aptas.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: Tipo de exportación**
>
>¿Debe la activación exportar instantáneas de audiencia completas o solo cambios incrementales?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Exportación incremental | Destinos de streaming ([!DNL Marketo], CRM) o destinos por lotes donde los sistemas descendentes administran deltas | Volumen de datos menor por exportación. Procesamiento más rápido. Requiere sistemas descendentes para administrar el estado. Predeterminado para destinos de flujo continuo. |
>| Exportación completa | Destinos por lotes en los que el sistema descendente reemplaza la audiencia completa cada ejecución | Mayor volumen de datos, pero lógica descendente más sencilla. Útil cuando los sistemas posteriores no mantienen el estado. Disponible para destinos basados en archivos. |

>[!NOTE]
>**Decisión: ámbito de activación**
>
>¿Cuántas audiencias deben activarse por destino?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Una audiencia por flujo de datos | Activación sencilla con asignación clara de audiencia a destino | Es más fácil de monitorizar y solucionar problemas. Un error de audiencia no afecta a otros. |
>| Varias audiencias por flujo de datos | Varias audiencias relacionadas que van al mismo destino | Uso más eficiente de las conexiones de destino. Todas las audiencias comparten la misma asignación de campos y programación. |

**Navegación de la interfaz de usuario:** Conexiones > Destinos > Examinar > Seleccionar destino > Activar audiencias

**Detalles de configuración de clave:**

- Seleccione la audiencia o audiencias de destino de la lista de audiencias
- Revise y confirme las asignaciones de campo configuradas en la fase 3
- Para destinos por lotes: configure la programación de exportación (hora, frecuencia)
- Para destinos de flujo continuo: la activación comienza inmediatamente después de la configuración
- Opcionalmente, se pueden añadir audiencias de supresión mediante la funcionalidad de exclusión
- Almacene en déclencheur una ejecución de activación de prueba inicial para validar el flujo de datos

**Donde las opciones difieren:**

**Para La Opción A ([!DNL Marketo Engage] Transmisión):**

Seleccione las audiencias de la cuenta que desea activar. La activación comienza a transmitirse inmediatamente. Compruebe en [!DNL Marketo] que los registros de clientes potenciales/contactos se están actualizando con los campos de pertenencia a segmentos. Configure [!DNL Marketo] campañas inteligentes en déclencheur en función de estos cambios de campo.

**Para Opción B (Lote De Advertising Platform):**

Seleccione las audiencias de la cuenta y configure la programación diaria de exportación. Una vez finalizada la primera exportación, compruebe en la plataforma publicitaria que la audiencia aparece y tiene un recuento de miembros rellenado. La plataforma tarda de 24 a 48 horas en procesar el archivo de audiencia inicial.

**Para La Opción C (Basada En Archivos De Almacenamiento En La Nube):**

Seleccione las audiencias de la cuenta y configure la programación de exportación y el formato de archivo. Después de la primera exportación, compruebe que los archivos aparecen en la ubicación de almacenamiento de destino con el formato y el contenido esperados. Confirme que los procesos de importación descendentes consumen correctamente los archivos exportados.

**Para la opción D (transmisión CRM):**

Seleccione las audiencias de la cuenta que desea activar. La activación comienza a transmitirse inmediatamente. Compruebe en CRM que los registros de cuenta o contacto se actualizan con los campos asignados. Configure los informes de CRM, las vistas de lista o la automatización del flujo de trabajo para actuar en los campos actualizados.

**Documentación de Experience League:**

- [Activar audiencias en destinos de flujo continuo](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Activar audiencias en destinos por lotes](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Protecciones de activación](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
- [Información general sobre los destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)

### Fase 5: Gobernanza y monitorización

Esta fase garantiza que la activación de la audiencia de cuenta cumpla con las políticas de gobernanza de datos y las preferencias de consentimiento, y que los flujos de datos de activación continua se monitoricen por motivos de estado.

**Función de la aplicación:** [!DNL RT-CDP] B2B: Gobernanza de datos B2B, [!DNL RT-CDP]: Aplicación del consentimiento y la gobernanza

**Lo que configurará:** Esta fase garantiza que la activación de la audiencia de la cuenta cumpla con las directivas de gobernanza de datos y las preferencias de consentimiento, y que los flujos de datos de activación en curso se supervisen por motivos de estado. La gobernanza de datos B2B impone restricciones en los atributos de cuentas confidenciales (ingresos, recuento de empleados de proveedores externos), mientras que la aplicación del consentimiento garantiza que las comunicaciones a nivel de persona respeten las preferencias de exclusión. La monitorización confirma que los flujos de datos de activación se completan correctamente.

**Puntos de decisión en esta fase:**

>[!NOTE]
>**Decisión: nivel de cumplimiento de gobernanza**
>
>¿Con qué rigor se debe aplicar la gobernanza de datos para las activaciones B2B?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Aplicación completa (bloque en infracción) | Activaciones de producción con datos confidenciales | Evita cualquier activación que infrinja las directivas de gobernanza. Puede requerir ajustes iterativos de asignación de campos para resolver infracciones. |
>| Avisar y continuar | Entornos de desarrollo o prueba | Permite continuar la activación, pero registra las advertencias. Útil durante la configuración inicial para identificar posibles problemas. |

>[!NOTE]
>**Decisión: enfoque de supervisión**
>
>¿Cómo se debe monitorizar la salud de activación?
>
>| Opción | Cuándo elegir | Consideraciones |
>| --- | --- | --- |
>| Monitorización basada en alertas | Entornos de producción en los que los errores deben detectarse rápidamente | Configure alertas para errores de activación de destino, errores de flujo de origen y retrasos de flujo de datos. Requiere configuración de suscripción de alerta. |
>| Monitorización manual | Desarrollo o activaciones de bajo volumen | Revise periódicamente las ejecuciones de flujo de datos en la IU Destinos. Menos sobrecarga, pero riesgo de detección de fallos retrasada. |
>| Ambos | Entornos de producción con activación compleja de varios destinos | Alertas de errores críticos más una revisión periódica del panel para detectar tendencias. Recomendado para la mayoría de las implementaciones B2B. |

**Navegación de la interfaz de usuario:** Privacidad > Políticas (para el control), Conexiones > Destinos > Examinar > Seleccionar destino > Ejecuciones del flujo de datos (para el control)

**Detalles de configuración de clave:**

- Aplicar etiquetas de uso de datos a conjuntos de datos B2B que contengan atributos restringidos
- Compruebe que las políticas de gobernanza se aplican evaluando la activación con la acción de marketing de destino
- Configurar alertas para errores de activación de destino y errores del conector de origen
- Revise las métricas de ejecución del flujo de datos (perfiles exportados, registros fallidos) después de cada ciclo de activación
- Configure la revisión del tablero de uso de licencias para rastrear el volumen de perfil de cuenta con los derechos

**Documentación de Experience League:**

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [Monitorización de flujos de datos de destino](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Protecciones de activación](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

## Consideraciones sobre la implementación

Las secciones siguientes proporcionan directrices adicionales para una implementación exitosa.

### Protecciones y límites

Revise las siguientes protecciones y límites de la plataforma que se aplican a este patrón de caso de uso.

- Máximo de 4000 definiciones de segmento por zona protegida, incluidas las audiencias de cuenta — [Protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Las audiencias de cuenta se evalúan principalmente mediante la evaluación por lotes; la idoneidad para la transmisión se limita a condiciones simples de atributos de cuenta
- Máximo de 100 flujos de datos por conexión de destino: [protecciones de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
- Los destinos por lotes exportan hasta 5 millones de perfiles por segmento de archivo
- Los destinos de streaming tienen límites de rendimiento por segundo establecidos por el socio de destino (por ejemplo, [!DNL Marketo] límites de tasa de API)
- Las audiencias compuestas (de Composición de audiencia) se limitan a la evaluación por lotes y no pueden utilizar el streaming
- Máximo de 10 bloques de composición por lienzo de composición de audiencia
- [!DNL LinkedIn] audiencias coincidentes requieren un tamaño mínimo de audiencia (normalmente 300 miembros) para su activación
- Los destinos de streaming de CRM están sujetos a los límites de tasa de API del proveedor de CRM (por ejemplo, [!DNL Salesforce] límites diarios de API masivos)
- [!DNL RT-CDP] La licencia de B2B edition rige el número total de perfiles de cuenta empresarial: [Descripción de producto de RT-CDP](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

### Peligros comunes

Tenga en cuenta los siguientes problemas comunes al implementar este patrón de caso de uso.

- **Asignación incompleta de persona a cuenta:** Si los registros de persona (posibles clientes, contactos) no están vinculados correctamente a los registros de cuenta mediante la resolución de identidades B2B, las audiencias de cuenta que dependen de atributos o actividades de persona no contarán las cuentas que cumplen los requisitos. Valide las relaciones persona a cuenta en F4 antes de crear audiencias de cuenta.

- **Datos de CRM obsoletos que provocan la desviación de la audiencia:** Si los conectores de origen de CRM no se ejecutan de forma regular o fallan de forma silenciosa, los atributos de cuenta (sector, ingresos, estado) quedan obsoletos. Esto hace que las audiencias incluyan cuentas que ya no cumplen los requisitos o excluyan cuentas que deberían cumplir los requisitos. Monitorice el estado del flujo de datos del conector de origen.

- **Expectativas de tasa de coincidencia de la plataforma Advertising:** Al activar audiencias de cuenta en plataformas de publicidad distintas de [!DNL LinkedIn], la tasa de coincidencia depende de tener identificadores válidos de nivel de persona (correo electrónico con hash) para los contactos asociados con cuentas que cumplen los requisitos. Las cuentas sin contactos asociados que tengan direcciones de correo electrónico no coincidirán. Monitorice las tasas de coincidencia y considere enriquecer los datos de contacto.

- Desalineación de asignación de campo de **[!DNL Marketo]:** Al transmitir a [!DNL Marketo Engage], la asignación de campo de [!DNL RT-CDP] debe estar dirigida a los campos de contacto o posible cliente de [!DNL Marketo] existentes. Si el campo [!DNL Marketo] asignado no existe, la actualización fallará de forma silenciosa. Cree previamente todos los campos de destino en [!DNL Marketo] antes de configurar el destino.

- **Activación del bloqueo de la directiva de gobernanza:** Las etiquetas de uso de datos en los campos de atributos de cuenta (especialmente los datos firmográficos de terceros) pueden infringir la directiva de déclencheur al activarse en los destinos de publicidad. Evalúe el cumplimiento de la gobernanza antes de activar y ajustar las asignaciones de campos para excluir los campos restringidos si es necesario.

- **Audiencia de cuenta que combina datos de cuenta y persona con evaluación por lotes:** Las audiencias de cuenta que hacen referencia a eventos de comportamiento a nivel de persona (por ejemplo, &quot;cuentas en las que al menos un contacto ha abierto un correo electrónico en los últimos 30 días&quot;) requieren evaluación por lotes. Si el caso de uso espera una calificación en tiempo real, esta restricción puede causar una latencia inesperada.

### Prácticas recomendadas

Siga estas recomendaciones para obtener resultados óptimos.

- Comience con un pequeño número de audiencias de cuenta bien definidas (nivel ICP, sector vertical, nivel de participación) antes de ampliarse a definiciones complejas de varios atributos
- Cree audiencias de supresión dedicadas para los clientes existentes, las oportunidades activas y las cuentas contratadas recientemente para evitar gastos desperdiciados y conflictos de canal
- Use la Composición de audiencias para crear audiencias de cuenta por niveles (participación alta/media/baja) mediante la clasificación de cuentas en puntuaciones de participación agregadas
- Active la misma audiencia de cuenta en varios destinos simultáneamente para campañas multicanal coordinadas (por ejemplo, [!DNL LinkedIn] para publicidad, [!DNL Marketo] para correo electrónico, CRM para visibilidad de ventas)
- Implemente una convención de nombres uniforme para las audiencias de cuenta que incluya los criterios de segmentación y el canal deseado (por ejemplo, &quot;B2B_ICP_Enterprise_Tech_LinkedIn&quot; o &quot;B2B_Suppression_ActiveOpps&quot;)
- Programe la activación por lotes durante las horas de menor actividad para minimizar el impacto en los sistemas descendentes y alinearse con las ventanas de procesamiento de la plataforma de publicidad
- Monitorice las tasas de coincidencia por destino después de la activación inicial e itere en las asignaciones de los campos de identidad para mejorar la coincidencia
- Mantener flujo de datos bidireccional con [!DNL Marketo Engage]: ingrese datos de participación de [!DNL Marketo] en [!DNL RT-CDP] (conector de origen) y vuelva a activar audiencias en [!DNL Marketo] (conector de destino) para un sistema de bucle cerrado

### Decisiones de compensación

Tenga en cuenta los siguientes aspectos clave al tomar decisiones de implementación.

>[!NOTE]
>**Compensación: Actualización de audiencia vs. complejidad de evaluación**
>
>Las audiencias de cuenta que combinan atributos de cuenta con datos de comportamiento de nivel de persona proporcionan los objetivos más precisos, pero se limitan a la evaluación por lotes (actualización diaria). Las audiencias más sencillas basadas únicamente en atributos de cuenta pueden cumplir los requisitos para la evaluación de streaming con actualizaciones casi en tiempo real.
>
>- **Lote (criterio complejo) favorece:** Precisión de segmentación, combinación de señales fimográficas y de comportamiento, puntuación de cuenta completa
>- **El streaming (con criterios simples) favorece:** la velocidad de las actualizaciones de audiencia, la respuesta en tiempo real a los cambios de cuenta, un tiempo de acción más rápido en [!DNL Marketo] y CRM
>- **Recomendación:** Utilice la evaluación por lotes para audiencias de segmentación principales en las que se acepte una actualización diaria (la mayoría de los casos de uso de B2B). Reserve la evaluación de streaming para déclencheur con distinción de tiempo, como cambios de estado de cuenta o alertas de cuenta de alto valor.

>[!NOTE]
>**Compensación: activación centralizada frente a audiencias específicas del destino**
>
>Puede activar una sola audiencia de cuenta unificada en varios destinos o crear audiencias específicas del destino adaptadas a las capacidades y los requisitos de cada canal.
>
>- **Favoritos de audiencia centralizados:** Coherencia entre canales, administración de audiencias más sencilla, informes unificados
>- **Favoritos de audiencias específicas del destino:** Segmentación optimizada por canal (por ejemplo, [!DNL LinkedIn] se beneficia de atributos a nivel de compañía mientras que [!DNL Marketo] necesita detalles a nivel de posible cliente), reglas de supresión específicas del canal
>- **Recomendación:** Comience con audiencias centralizadas para mantener la coherencia y, a continuación, cree variantes específicas del destino solo cuando los requisitos de canal difieran significativamente (por ejemplo, diferentes ventanas de supresión para publicidad o correo electrónico).

>[!NOTE]
>**Compensación: sincronización de CRM en tiempo real frente a actualizaciones de CRM por lotes**
>
>El streaming a CRM proporciona visibilidad de ventas inmediata, pero consume cuota de API de CRM. Las exportaciones de archivos por lotes son más eficientes, pero introducen latencia.
>
>- **Favoritos de sincronización de CRM de transmisión:** Capacidad de respuesta de ventas, alertas inmediatas de cuenta, visibilidad de canalización en tiempo real
>- **Actualizaciones de CRM por lotes favorece:** Conservación de cuotas de API, eficiencia de actualizaciones masivas, alineación con ventanas de carga de datos de CRM
>- **Recomendación:** Use la sincronización de CRM de flujo continuo para los cambios de calificación de cuentas de alta prioridad (por ejemplo, la cuenta se mueve al nivel &quot;Listo para ventas&quot;). Utilice exportaciones de archivos por lotes para actualizaciones masivas como actualizaciones mensuales de puntuación de cuenta o listas de reasignación de territorios.

## Documentación relacionada

Los siguientes recursos proporcionan contexto adicional e instrucciones detalladas para las capacidades utilizadas en este patrón de caso de uso.

**[!DNL RT-CDP]B2B edition**

- [Información general sobre Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b)
- [Esquemas B2B en Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Audiencias de cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [Descripción del producto de RT-CDP B2B edition](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

**Evaluación y segmentación de audiencias**

- [Resumen del servicio de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guía de IU del Generador de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Composición de audiencia](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Segmentación de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Protecciones de segmentación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

**Destinos y activación**

- [Información general sobre los destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Marketo Engage destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [Destino de audiencias coincidentes de LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
- [Destino de Salesforce CRM](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Microsoft Dynamics 365 destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/microsoft-dynamics-365)
- [Amazon S3 destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)
- [Activar audiencias en destinos de flujo continuo](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Activar audiencias en destinos por lotes](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Protecciones de activación](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

**Fuentes de datos y conectores**

- [Resumen de orígenes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Conector de Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Conector de Salesforce](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/crm/salesforce)

**Modelado e identidad de datos**

- [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Introducción al servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Resumen del perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Resumen de políticas de combinación](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

**Gobernanza de datos y privacidad**

- [Información general sobre la gobernanza de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Información general sobre las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview)
- [Consentimiento y preferencias](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**Monitoreo y observabilidad**

- [Resumen de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Monitorización de flujos de datos de destino](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Monitorización de flujos de datos de origen](https://experienceleague.adobe.com/en/docs/experience-platform/sources/api-tutorials/monitor)
- [Panel de control de uso de licencias](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**Informes y análisis**

- [Información general de CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Información general sobre Conexiones](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Resumen de vistas de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)

**Tutoriales y guías**

- [Introducción a Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro)
- [Creación de un esquema para fuentes B2B](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Herramientas de zona protegida](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/overview)
