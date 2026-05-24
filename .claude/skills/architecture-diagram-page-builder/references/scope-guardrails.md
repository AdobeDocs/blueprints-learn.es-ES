---
source-git-commit: e79d9d6490e4f50c4611dd879b53f0e63a90cd65
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---
# Protecciones de ámbito: página de arquitectura vs. página de patrón de caso de uso

El sitio de modelos separa **páginas de diagrama de arquitectura** de **páginas de patrones de casos de uso** porque sirven para diferentes necesidades del lector. Este documento define qué pertenece a dónde y cómo gestionar el contenido que se desplaza por los límites.

## La distinción básica

- **Las páginas de diagrama de arquitectura** son referencias visuales de nivel superior. Responden: *&quot;¿Cómo encajan estos sistemas? ¿Dónde están los puntos de integración? ¿Cuál es la forma del flujo de datos?&quot;* Los lectores vienen aquí para orientarse.
- **Las páginas de patrones de casos de uso** son guías de implementación. Responden: *&quot;¿Cómo puedo crear esta capacidad? ¿Qué funciones están involucradas? ¿Qué KPI miden el éxito? ¿Cuáles son mis opciones de implementación?&quot;* Los lectores vienen aquí cuando tienen un caso de uso y necesitan enviarlo.

## pertenece a una página de arquitectura

| Categoría | Ejemplos |
| --- | --- |
| Arquitectura de nivel superior | Diagramas generales de AEP y aplicaciones, marketing de Experience Cloud, topología hub vs. edge |
| Flujo de datos del sistema | Rutas de ingesta en tiempo real frente a por lotes, sincronización de perfiles entre hub y edge, flujos de búsqueda frente a activación |
| Puntos de integración | Donde AEP se integra con AJO, CJA, Target, Campaign, Marketo, Workfront; límites de SDK; superficies de API |
| Topología de implementación | Implementación de Web SDK frente a Mobile SDK, reenvío del lado del servidor, ubicación de nodos perimetrales |
| Arquitectura de aplicación | Cómo se estructura internamente una sola aplicación (AJO, CJA, RTCDP) en el sistema |
| Punteros para patrones de casos de uso | &quot;Esta arquitectura admite los patrones X, Y y Z&quot; con vínculos; la página de arquitectura **no** duplica ese contenido |

## NO pertenece a una página de arquitectura

Si escribe algo de lo siguiente, redirija a una página de patrones de casos de uso (use la aptitud `use-case-pattern-builder`):

| Categoría | Por qué pertenece a otra parte |
| --- | --- |
| KPI y fórmulas de medición | Los patrones de casos de uso miden resultados; las páginas de arquitectura no |
| Objetivos empresariales, impacto empresarial | El contenido de KBO tiene menos de `/help/blueprints/business-objectives/`; los patrones hacen referencia a él |
| Ejemplos de casos de uso tácticos | &quot;Recordatorio de abandono del carro de compras&quot;, &quot;Héroe de página de inicio personalizado&quot;, etc.: estos son contenidos de patrones |
| Capacidades (`A > B > C > D`) | La construcción de capacidades forma parte de la plantilla de patrones de casos de uso |
| Narrativas personales | &quot;María, la comercializadora, quiere...&quot; los escenarios de estilo pertenecen a patrones, no a referencias de arquitectura |
| Opciones de implementación | La guía de implementación de varias opciones (Mejor para, Cómo funciona, Ventajas, Limitaciones) es una construcción de patrón |
| Tablas de funciones básicas/auxiliares | Son secciones de página de patrón |
| Listas de comprobación de requisitos previos por caso de uso | Los patrones los rastrean; las páginas de arquitectura se vinculan a patrones en su lugar |

## frases de déclencheur a tener en cuenta

Si el usuario proporciona cualquiera de estas frases al describir la nueva página, ponga en pausa y vuelva a comprobar el ámbito:

- &quot;KPI&quot;
- &quot;impacto comercial&quot; / &quot;resultados empresariales&quot;
- &quot;casos de uso tácticos&quot; / &quot;escenarios de ejemplo&quot;
- &quot;funcionalidades&quot;
- &quot;opciones de implementación&quot;
- &quot;mejor para&quot;
- &quot;ventajas y limitaciones&quot;
- &quot;requisitos previos&quot;
- &quot;personas&quot; / &quot;interesados&quot;
- &quot;medida&quot;

No descalifican automáticamente la página, pero indican que el usuario puede querer una página de patrón de caso de uso, no una página de arquitectura. Confirme la intención antes de generar.

## Qué hacer cuando el contenido se desvía

1. **Identificar la deriva.** Apunte a la sección o viñeta específica que haya cruzado el límite.
2. **Ofrecer dos opciones al usuario:**
   - Recortar la sección desde la página de arquitectura (lo más común: mantiene la página de arquitectura centrada).
   - Deténgase y cambie a `use-case-pattern-builder` para ese contenido (cuando el usuario realmente desee una página de patrón).
3. **Esperar confirmación.** No reescriba ni suelte contenido de forma silenciosa.
4. **Si mantiene contenido solo de arquitectura**, reemplace el contenido profundo con una sola viñeta bajo `## Use case patterns supported` que se vincule al patrón relevante (existente o por crear).

## Casos de Edge

- **La página es mitad arquitectura, mitad patrón.** Dividir en dos páginas: una página de arquitectura (esta aptitud), una página de patrón de caso de uso (la aptitud `use-case-pattern-builder`). Cruza los vínculos.
- **La página Arquitectura describe un único caso de uso de extremo a extremo.** Es un patrón de caso de uso, no una página de arquitectura. Redirigir a `use-case-pattern-builder`.
- **La página de arquitectura debe mostrar flujos de datos de ejemplo para un escenario específico.** Aceptable si el escenario es solo ilustrativo y la mayor parte de la página permanece en el nivel de arquitectura del sistema. Mantenga el ejemplo en un párrafo y vincúlelo al patrón relevante para obtener detalles completos.

## Prueba rápida

Antes de generar, pregunte: *&quot;Si un lector llega a esta página esperando una referencia de arquitectura de nivel superior, ¿obtendrá una o obtendrá un tutorial de caso de uso a medio terminar?&quot;* En este último caso, la página pertenece a `use-case-pattern-builder`.
