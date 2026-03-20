---
name: industry-use-case-builder
description: 'Guía de creación de nuevos casos de uso del sector para el repositorio de modelos de Adobe Experience Platform. Utilice esta aptitud cuando añada un nuevo caso de uso a un sector (minorista, automoción, sanidad, servicios financieros, seguros, medios de comunicación y entretenimiento, telecomunicaciones, viajes y hospitalidad, B2B), cuando el usuario desee añadir escenarios comerciales a páginas del sector o al actualizar el catálogo de casos de uso. Gestiona el flujo de trabajo completo: recopilación de detalles de casos de uso, evaluación del nivel de madurez, generación de contenido, actualización de la página de información general del sector y el catálogo de casos de uso, e invocación de la aptitud de generador de iconos de casos de uso para la creación de iconos.'
source-git-commit: ed8928687806b619e95d8d320478d27c13722a80
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---


# Generador de casos de uso del sector

Esta aptitud guía la creación de nuevos casos de uso del sector para el repositorio de modelos de Adobe Experience Platform. Seguir cada fase secuencialmente. Lea los archivos de referencia antes de comenzar:

- `references/use-case-template.md`: plantilla exacta para secciones de casos de uso
- `references/catalog-row-template.md`: formato exacto de las filas de la tabla del catálogo
- `references/maturity-criteria.md`: encabezamiento detallado para la evaluación de madurez

## Fase 1: Recopilación de información

Entrevista al usuario para recopilar todos los detalles necesarios antes de generar cualquier contenido.

### Campos obligatorios

1. **Sector vertical** — Debe ser uno de:
   - automotriz
   - b2b
   - financial-services
   - asistencia sanitaria
   - seguro
   - media-entretenimiento
   - minorista
   - telecomunicaciones
   - viaje-hospitalidad

2. **Nombre del caso de uso**: Un título claro y descriptivo (por ejemplo, &quot;Recuperación de correo electrónico del carro de compras abandonado&quot;, &quot;Campañas de adherencia a medicamentos&quot;).

3. **Descripción** — 1-2 oraciones que describen el escenario comercial y por qué importa.

4. **Impacto en la empresa**: resultados cuantificados con métricas específicas (por ejemplo, &quot;aumento de 20 a 30 % en las tasas de clics&quot;, &quot;mejora de 15 a 25 % en las tasas de recarga&quot;).

5. **Patrón de caso de uso**: debe asignarse exactamente a uno de estos patrones existentes:
   - Audience Activation a destinos
   - Audience Collaboration con coincidencia de segmentos
   - Reenvío de eventos
   - Audience Activation B2B
   - Personalization web de visitante anónimo
   - Personalization de aplicación/web de visitante conocido
   - Offer Decisioning
   - Recomendación de comportamiento
   - Activación de mensaje saliente por lotes
   - Mensajería activada por eventos
   - Recorrido orquestado de varios pasos
   - Recorrido en canales múltiples con toma de decisiones
   - Adquisición de gestión de Recorridos y marketing basada en grupos
   - Generación de Customer Analytics y Insight
   - Análisis B2B
   - Experiencia de conversación en Brand Concierge

6. **Consideraciones técnicas**: de 4 a 8 puntos de viñeta que cubren requisitos de datos, integraciones, necesidades regulatorias/de cumplimiento, consideraciones de rendimiento y notas de arquitectura.

Solicite los campos que faltan antes de continuar. No asuma ni fabrique detalles.

## Fase 2: Evaluación de la madurez

Lea `references/maturity-criteria.md` para ver el encabezamiento completo. Asigne uno de los tres niveles de vencimiento:

- **Fundacional** `[!BADGE Foundational]{type=Neutral}`: patrones de un solo paso o activados por eventos (mensajería activada por eventos, salida por lotes), requisitos de datos directos, IA/ML mínima, integraciones estándar.
- **Emergente** `[!BADGE Emerging]{type=Informative}`: recorridos de varios pasos, datos de comportamiento, modelos de recomendaciones, personalización de visitantes conocidos, complejidad de integración moderada.
- **Avanzado** `[!BADGE Advanced]{type=Caution}`: Toma de decisiones en canales múltiples, predicción basada en IA, Offer Decisioning, orquestación compleja, integraciones múltiples de sistemas.

### Flujo de evaluación

1. Identifique a qué patrón de caso de uso se asigna el caso de uso.
2. Marque la lista &quot;Patrones típicos&quot; en los criterios de madurez para una coincidencia rápida.
3. Si el patrón no indica claramente la madurez, evalúe la complejidad de los datos, los requisitos de IA/ML y el alcance de la integración.
4. Presente la evaluación al usuario con un razonamiento: &quot;Basándome en la asignación de patrones ({pattern}) y {key factors}, clasificaría esto como {level} debido a {reasoning}&quot;.
5. Espere a que el usuario confirme o anule antes de continuar con la generación de contenido.

## Fase 3: Generación de contenido

Generar o actualizar contenido en dos archivos.

### A. Archivo de información general del sector

**Ruta de archivo:** `/help/blueprints/industry-use-cases/{industry}/{industry}-overview.md`

Lea primero el archivo existente para comprender la estructura y el contenido actuales. A continuación, agregue una nueva sección siguiendo la plantilla exacta de `references/use-case-template.md`:

```markdown
## {Use Case Title}

{1-2 sentence description of the business scenario and why it matters}

### Business impact

{Quantified business outcomes, e.g., "Retailers typically see a 20-30% increase in click-through rates..."}

### How to implement

Use the [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) pattern. {1-2 sentence explanation of why this pattern applies}

### Technical considerations

- {4-8 bullet points covering data integration, regulatory, performance, or architectural considerations}
```

Coloque la nueva sección después de las secciones de casos de uso existentes, manteniendo un formato coherente.

### B. Catálogo de casos de uso

**Ruta de archivo:** `/help/blueprints/industry-use-cases/use-case-catalog.md`

Lea primero el archivo de catálogo existente. Añada una nueva fila a la pestaña del sector correcta. El catálogo usa una estructura con fichas con `>[!TAB {Industry}]` marcadores. Cada pestaña contiene una tabla con estas columnas:

| Columna | Contenido |
| --- | --- |
| Icono | `<img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40">` (dejar vacío si todavía no hay ningún icono) |
| Ejemplo de uso | `[{Use Case Title}]({industry}/{industry}-overview.md#{anchor})`, donde el anclaje es el encabezado en kebab-case |
| Descripción | Resumen de una frase |
| Vencimiento | Sintaxis de distintivo para el nivel asignado |
| Patrón | `[{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md)` |

**Regla de colocación:** Dentro de cada ficha de sector, las filas se agrupan por vencimiento en este orden: Básico primero, Emergente después Avanzado. Coloque la nueva fila al final del grupo de vencimiento correcto.

Las rutas del archivo de patrón son:
- `audience-building-activation/audience-activation-to-destinations.md`
- `audience-building-activation/audience-collaboration-segment-match.md`
- `audience-building-activation/event-forwarding.md`
- `audience-building-activation/b2b-audience-activation.md`
- `personalization/anonymous-visitor-web-personalization.md`
- `personalization/known-visitor-web-app-personalization.md`
- `personalization/offer-decisioning.md`
- `personalization/behavioral-recommendation.md`
- `campaign-management-orchestration/batch-outbound-message-activation.md`
- `campaign-management-orchestration/event-triggered-messaging.md`
- `campaign-management-orchestration/multi-step-orchestrated-journey.md`
- `campaign-management-orchestration/cross-channel-journey-with-decisioning.md`
- `campaign-management-orchestration/buying-group-based-marketing.md`
- `analysis/customer-analytics-insight-generation.md`
- `analysis/b2b-analytics.md`
- `conversational-experience/brand-concierge-conversational-experience.md`

## Fase 4: Generación de iconos

Una vez creado el contenido, invoque la aptitud `use-case-icon-generator` para generar una especificación de icono para el nuevo caso de uso. Proporcione a la aptitud lo siguiente:
- El nombre del caso de uso
- La industria vertical
- Una breve descripción del caso de uso

Una vez que el usuario tenga el archivo de icono generado, actualice la fila del catálogo para incluir la referencia de icono:

```
<img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40">
```

## Fase 5: Validación

Antes de finalizar, compruebe lo siguiente:

1. **Cumplimiento de la plantilla**: la sección de información general del sector sigue exactamente a la plantilla (encabezado ##, descripción, ### impacto empresarial, ### implementación, ### consideraciones técnicas).
2. **Colocación del catálogo**: la fila del catálogo se encuentra en la ficha de sector correcta y en el grupo de vencimiento correcto (Básico, Emergente y Avanzado).
3. **Validez del vínculo de patrón**: el vínculo de patrón de la descripción general y del catálogo utiliza una ruta de archivo de patrón válida de la lista anterior.
4. **Coherencia de anclaje**: el anclaje del vínculo del catálogo (por ejemplo, `#abandoned-cart-email-recovery`) coincide con el encabezado `##` del archivo de información general convertido a minúscula.
5. **Convenciones de rutas de iconos**: La ruta de iconos sigue a `assets/use-case-icons/{industry}/icon-{kebab-name}.png`.

Informe de los problemas encontrados durante la validación y corríjalos antes de completarlos.
