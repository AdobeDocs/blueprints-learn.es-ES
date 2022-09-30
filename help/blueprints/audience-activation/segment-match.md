---
title: Coincidencia de segmentos
description: Obtenga información sobre [!UICONTROL Coincidencia de segmentos] para Adobe Experience Platform (AEP). [!UICONTROL Coincidencia de segmentos] es un servicio de colaboración de datos que le permite intercambiar datos de segmentos basados en identificadores comunes del sector de forma segura, regulada y compatible con la privacidad.
solution: Experience Platform
source-git-commit: a5bf86b8606d40a0686c667f83516e3b495350b8
workflow-type: tm+mt
source-wordcount: '1764'
ht-degree: 0%

---

# Coincidencia de segmentos

La coincidencia de segmentos permite a las marcas de socios compartir audiencias en sus respectivos entornos de Experience Platform. La clave para las marcas es conectarse con los clientes en función de los datos recopilados de sus relaciones directas con los consumidores. Con un mejor gobierno, permisos y sistemas de administración de preferencias, los especialistas en marketing pueden mejorar aún más sus audiencias autenticadas de origen con socios clave.

[!UICONTROL Coincidencia de segmentos] es un servicio de colaboración de datos para permitir a los clientes Experience Platform (AEP) (denominado _partners_) para intercambiar datos de segmentos basados en identificadores comunes del sector de forma segura, regulada y compatible con la privacidad.

El servicio permite a los clientes identificar de forma segura los ID coincidentes de una manera segura y neutral sin tener que revelar toda su base de datos. Los socios solo reciben atributos designados (nombre del segmento) para ID superpuestos, lo que permite compartir de forma más rápida y sencilla, controlada por el consentimiento.

[!UICONTROL Coincidencia de segmentos] utiliza el marco de consentimiento y control de datos de AEP como su columna vertebral. Está disponible para todos los clientes de B2C y B2P Real-time Customer Data Platform. Características principales de [!UICONTROL [!UICONTROL Coincidencia de segmentos]] incluir:

* Uso compartido de segmentos para clientes con consentimiento superpuesto
* Informes de superposición antes del uso compartido para obtener información sobre el volumen de coincidencia estimado
* Política DULE totalmente integrada y aplicación de permisos
* Columna básica del marco de consentimiento para el uso compartido de datos
* Fuentes de datos para organizar segmentos y socios

## Aplicaciones

Marca para editor:

El &quot;caso de uso del editor&quot; es el más afectado por la desaprobación de cookies de terceros y datos de ID de publicidad móvil. Este caso de uso tiene un gran impacto en la industria de los medios y el entretenimiento, que se centra en la venta de publicidad como modelo de negocio. [!UICONTROL Coincidencia de segmentos] es una ruta para editores con grandes audiencias de origen que buscan colaborar directamente con sus anunciantes. Los anunciantes pueden trabajar directamente con los editores para hacer publicidad en las audiencias coincidentes en las propiedades del editor para campañas de prospección o segmentación granulares.

### Marca a marca

Los recorridos de los consumidores nunca son lineales. Por ejemplo, un cliente puede ser leal a una aerolínea y a su compañía de tarjetas de crédito. Usando [!UICONTROL Coincidencia de segmentos], la aerolínea y la empresa de tarjetas de crédito pueden crear una asociación de datos para comprender las audiencias superpuestas y luego adaptar las ofertas para personalizar las experiencias a los consumidores fieles de cada una de las compañías.

### BU a BU

Las multinacionales mundiales tienen dificultades con la colaboración de datos entre unidades de negocio que operan de manera independiente. Puede que no sea posible combinar datos en un solo simulador de pruebas debido a las diferentes políticas de privacidad, adquisiciones o permisos de administración en las distintas unidades de negocio.

[!UICONTROL Coincidencia de segmentos] ayuda a los equipos de marketing dispares de las organizaciones masivas a colaborar de forma más eficiente, mientras continúa funcionando de forma independiente

## Arquitectura

![Arquitectura de coincidencia de segmentos](assets/architecture-segment-match.png)

[!UICONTROL Coincidencia de segmentos] no es un mercado de datos en el que se puedan adquirir datos. En su lugar, es una función de AEP que funciona con datos de origen con socios seleccionados, utilizando controles de privacidad y consentimiento para ayudar a colaborar. [!UICONTROL Coincidencia de segmentos] ayuda a centrar los esfuerzos en mejorar las relaciones con los clientes y en ampliar la marca. Es beneficioso cuando existen marcas preexistentes o relaciones con socios. [!UICONTROL Coincidencia de segmentos] la experiencia es fácil de administrar, escalable y permite a los administradores compartir segmentos de forma opcional y controlable.

[!UICONTROL Coincidencia de segmentos] habilita:

* Los datos de pertenencia a segmentos se portarán de forma segura en todas las organizaciones mediante identificadores estándar de nivel de personas, como correo electrónico con hash o número de teléfono
* Una interfaz de usuario y flujos de trabajo de uso compartido de audiencias con notificaciones
* Estimaciones de superposición precompartidas
* Configuración del socio de autoservicio
* Superposiciones en áreas de nombres estandarizadas seleccionadas (correo electrónico con hash, teléfono con hash, ECID, IDFA, GAID)
* Aplicación del consentimiento para el uso compartido de datos
* Administración del ciclo de vida de la audiencia compartida
* Aplicación DULE en el flujo de trabajo de uso compartido
* Actualizaciones diarias por lotes

[!UICONTROL Coincidencia de segmentos] permite crear experiencias de cliente interconectadas. Los identificadores duraderos admitidos son correos electrónicos con hash, números de teléfono con hash e identificadores como ECID, IDFA y GAID. Los clientes pueden crear fuentes que coincidan con los datos de audiencia y los muevan entre entornos limitados de marca, con una sólida gobernanza, transparencia y capacidades de revocación para su uso en activaciones de publicidad y marketing

## Requisitos previos

Requisitos previos para [!UICONTROL Coincidencia de segmentos] son:

* Licencia activa de RT-CDP
* Los identificadores hash estándar admitidos son correo electrónico con hash SHA256, teléfono con hash, ECID, Apple IDFA y GAID
* Marco de privacidad y estrategia de consentimiento
* Acuerdos de uso compartido de datos entre clientes

## Seguridad

### RBAC

La variable [!UICONTROL Coincidencia de segmentos] RBAC garantiza el flujo para administrar socios. Solo las personas con el permiso adecuado pueden iniciar, aceptar o administrar socios. Esto se puede hacer en la sección Ingesta de datos del perfil de producto. Se requieren los siguientes permisos:

![Conexión compartida de audiencia](assets/data-ingestion.png)

| Permiso | Descripción |
|---|---|
| **Administrar conexiones de uso compartido de audiencias** | Este permiso le permite completar el proceso de protocolo de enlace con el socio, que conecta dos organizaciones IMS para habilitar [!UICONTROL Coincidencia de segmentos] flujos. |
| **Administrar audiencias compartidas** | Este permiso le permite crear, editar y publicar fuentes (el paquete de datos utilizado para [!UICONTROL Coincidencia de segmentos]) con socios activos (socios que el usuario administrador ha conectado con **Conexiones de uso compartido de audiencias** acceso). |

Consulte la [documentación oficial](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/segment-match/overview.html?lang=en#understanding-segment-match-permissions) para obtener más información sobre los permisos.

### ID de conexión

El proceso de conexión del socio se administra mediante la variable **[!UICONTROL ID de conexión],** que es un identificador generado aleatoriamente que se asigna a un entorno limitado de AEP específico. Este ID de conexión es necesario para iniciar y administrar entornos limitados de socios. También existe la posibilidad de volver a generar el ID de conexión para reconfigurar una conexión de socio, si es necesario.

### Gobierno

Cualquier conjunto de datos o atributos de datos con *C11* la etiqueta de contrato está restringida para el [!UICONTROL Coincidencia de segmentos] servicio. Los segmentos que utilizan esos atributos no se pueden usar para [!UICONTROL Coincidencia de segmentos]. Esto proporciona el control para el que los segmentos pueden utilizarse o no [!UICONTROL Coincidencia de segmentos]. Además, también se aplican las políticas personalizadas y las acciones de marketing creadas. De forma predeterminada, las directivas están deshabilitadas y deben habilitarse para la aplicación. Las restricciones como el marketing por correo electrónico y la publicidad en el sitio que se eligen al compartir segmentos también se propagan y comparten con los socios.

### Consentimiento

La configuración de consentimiento para [!UICONTROL Coincidencia de segmentos] se puede administrar de las siguientes maneras:

* En el nivel de organización, durante la incorporación, se utiliza la configuración de exclusión o inclusión para las comprobaciones de consentimiento.

   Esta configuración determina si los datos del usuario se pueden compartir o no. El valor predeterminado es la exclusión, lo que indica que los datos de usuario se pueden compartir con la suposición de que el cliente de AEP ya tiene el acuerdo de consentimiento necesario para el uso compartido de datos. Esta configuración se puede cambiar a Opt-in poniéndose en contacto con el administrador de cuentas de Adobe, lo que supone un registro adicional para obligar a los clientes de AEP a rastrear explícitamente el consentimiento.

* Configuración del atributo de uso compartido específico de identidades (idSpecific) mediante el uso de la variable [Grupo de campos Consentimientos y Preferencias](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/consents.html?lang=en).

   Este grupo de campos proporciona un único campo de tipo objeto, consentimientos, para capturar información de consentimiento y preferencias. [!UICONTROL Coincidencia de segmentos], de forma predeterminada, incluye todas las identidades que no se hayan excluido explícitamente, por ejemplo:

   ```
   "share": {
   `                `"val": "n"
   `     `}
   ```

   Esta configuración se puede cambiar poniéndose en contacto con el administrador de cuentas de Adobe para que solo incluya identidades con inclusión explícita, como por ejemplo:

   ```
   "share": {
   `                `"val": "y"
   `     `}
   ```

### Alertas

Las alertas se generan cuando se inicia una conexión de socio o cuando las fuentes de segmentos se comparten con socios.

## Flujo de trabajo de configuración

El flujo de trabajo para configurar la conexión de socio se administra con el RBAC como se ha mencionado anteriormente. Con los permisos adecuados en su lugar, la conexión a un simulador para pruebas de socio requiere que se comparta el ID de conexión de ese simulador para pruebas/instancia dentro de la organización del socio.

Una vez que se solicita una conexión al socio remitente, debe aprobarse en el lado receptor para garantizar una configuración segura del socio. El protocolo de enlace de la conexión con el socio garantiza que el acuerdo existe entre las dos organizaciones y permite al Adobe facilitar el [!UICONTROL Coincidencia de segmentos] en nombre de la organización. Con la conexión aprobada y en estado activo, el proceso de uso compartido de segmentos se puede iniciar desde cualquiera de las partes.

### Uso compartido de segmentos

El uso compartido de segmentos con un socio solo se produce cuando existe una coincidencia en el identificador seleccionado. Puede haber una relación de socio de uno a varios, lo que significa que los segmentos se pueden compartir con varios socios.

Para iniciar el uso compartido de segmentos después de configurar la conexión de socio, el socio remitente debe crear una fuente. A continuación, seleccione los casos de uso de marketing o las acciones de las que deben excluirse los datos del segmento junto con los identificadores duraderos. A continuación, se pueden agregar segmentos relevantes a la fuente para compartirlos.

Como parte de este flujo de trabajo de uso compartido de segmentos, el socio remitente puede descubrir posibles segmentos de alto valor mediante superposiciones estimadas antes de mover datos.

El flujo de proceso general es:

![Uso compartido de segmentos](assets/segment-sharing.png)

Estas estimaciones de superposición ofrecen perspectivas clave, descubrimiento de socios y datos para impulsar acuerdos de colaboración de datos. Ningún dato de cliente o segmento se mueve entre entornos limitados para obtener estas métricas de estimación de superposición. Las identidades aplicables preconfiguradas y seleccionadas por el cliente en cualquier entorno limitado dado se añaden a una estructura de datos probabilística que permite a Adobe realizar operaciones de unión e intersección entre ellas. Estas operaciones ayudan a [!UICONTROL Coincidencia de segmentos] obtenga la intersección estimada de dos estructuras de datos compuestas de identidades de dos entornos limitados diferentes sin tener que comparar los valores reales

El proceso de superposición de identidad depende de la variable **exportación diaria de perfil completo** conjunto de datos de entornos limitados tanto del remitente como del receptor para identificar perfiles comunes que pertenecen a los segmentos compartidos. A continuación se muestra el flujo de proceso detallado para el proceso de superposición:

![Proceso de superposición de identidad](assets/overlap-process.png)

Una vez que el socio remitente ha completado el uso compartido de segmentos, el receptor recibe una notificación sobre la fuente de segmentos compartida. Esta fuente de segmentos debe estar habilitada para que el perfil del receptor inicie el flujo de datos de pertenencia al segmento. Solo se incorpora la pertenencia a segmentos en los fragmentos de perfil superpuestos de la organización IMS del receptor y no se transfiere ninguna identidad adicional del remitente al receptor.

El segmento compartido está disponible en la sección `AEPSegmentMatch` de la sección **[!UICONTROL Audiencias]** en la ficha **[!UICONTROL Generador de segmentos]** y se pueden usar para la inclusión o supresión de audiencias mientras se generan segmentos en el simulador para pruebas del receptor.

El proceso de superposición diaria mantiene la pertenencia al segmento sincronizada entre el remitente y el receptor. El receptor puede desactivar el perfil de la fuente de segmentos recibida para pausar el proceso de uso compartido de segmentos.

#### Salida/entrada del segmento

Como parte de la exportación de perfil completo, el estado de los ID de segmento compartidos en la pertenencia de segmento para los perfiles tiene uno de los valores correspondientes: _realizado_, _exitado_ o _existente_ para reflejar el estado actual.

Durante el proceso diario de superposición de identidad, si existe la identidad correspondiente en el simulador para pruebas del receptor, estos estados de pertenencia a segmentos para segmentos compartidos se envían al receptor para su ingesta.

#### Revocación de segmentos

La revocación/eliminación de segmentos del remitente es un proceso bajo demanda en el que la lista de todos los perfiles con los ID de segmento revocados se obtiene del receptor. Los ID de segmento se eliminan de la pertenencia a segmentos de esas identidades y se vuelven a introducir en el receptor. Esta acción sobrescribe el fragmento de pertenencia a segmentos existente, que elimina la pertenencia a dicho segmento.

## Más información

* [Coincidencia de segmentos](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/segment-match/overview.html?lang=en#)
* [Permisos](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=en)
* [Solución de problemas](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/segment-match/troubleshooting.html?lang=en)
* [XID](https://experienceleague.adobe.com/docs/experience-platform/identity/api/list-native-id.html?lang=en)
