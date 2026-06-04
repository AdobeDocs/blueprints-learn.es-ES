---
name: architecture-diagram-page-builder
description: 'Creación de guías de creación de nuevas páginas de diagrama de arquitectura para el repositorio de modelos de Adobe Experience Platform. Utilice esta aptitud cuando añada un nuevo diagrama de arquitectura de nivel superior, una página de arquitectura de integración o información general sobre la arquitectura de aplicaciones. Las páginas de arquitectura cubren las arquitecturas de aplicaciones y AEP de nivel superior y los puntos de integración principales, no los casos de uso detallados (pertenecen al generador de patrones de casos de uso). Gestiona el flujo de trabajo completo: recopilar información de página, generar el archivo Markdown, colocarlo en la carpeta de temas correcta y actualizar TOC.md.'
source-git-commit: 4d236750286c28a8b8eb53a5bdec0645cc0e3e91
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 1%

---


# Diagrama de arquitectura Page Builder

Esta aptitud guía la creación de nuevas páginas de diagrama de arquitectura para el repositorio de modelos de Adobe Experience Platform. Las páginas de diagrama de arquitectura proporcionan referencias visuales de nivel superior sobre cómo encajan las aplicaciones de AEP y Adobe, los datos principales fluyen entre ellas y los puntos de integración que los autores deben tener en cuenta al diseñar soluciones.

## Ámbito

Las páginas del diagrama de arquitectura son **páginas centradas, de estilo de referencia**, normalmente de 40 a 100 líneas de marcado, que contienen:

- Uno o más diagramas de arquitectura con breves explicaciones del propósito de cada diagrama
- Vínculos a patrones de casos de uso que admite la arquitectura (la página de arquitectura no duplica ese contenido)
- Se ilustra una breve lista de los flujos de datos principales y los puntos de integración
- Vínculos de Experience League para obtener más información sobre el dominio de aplicación

Son **no** el lugar para el contenido de casos de uso detallados. Los KPI, los objetivos empresariales, los ejemplos de casos de uso tácticos, las capacidades y las narrativas de personas pertenecen a páginas de patrones de casos de uso en su lugar, generadas a través de la aptitud de `use-case-pattern-builder`. Consulte `references/scope-guardrails.md` para ver las protecciones completas.

## Lectura requerida antes de comenzar

Lea los siguientes archivos de referencia para plantillas y reglas:

- `references/diagram-template.md`: la plantilla de markdown completa con valores de marcador de posición
- `references/toc-placement.md`: formato de entrada y tabla de asignación de subsecciones para TOC.md
- `references/scope-guardrails.md`: reglas para lo que pertenece a una página de arquitectura frente a una página de patrón de caso de uso

## Fase 1: Recopilación de información

**Use formularios, no una entrevista lineal.** Recopile toda la información necesaria presentando `AskUserQuestion` formularios en rondas lógicas por lotes en lugar de hacer una pregunta a la vez. Esto mantiene la experiencia rápida y analizable para el usuario.

### Restricciones de AskUserQuestion

- Máximo de **4 preguntas** por llamada de `AskUserQuestion`.
- Máximo de **4 opciones** por pregunta.
- Si una pregunta tiene más de 4 opciones plausibles, divida la pregunta en dos llamadas (p. ej., pregunte las primeras 4 opciones y luego siga con un sí/no en la quinta).
- Utilice `multiSelect: true` para preguntas con varias respuestas (soluciones, patrones, flujos de datos).

### Ronda 1: información de la página principal (una llamada de AskUserQuestion, hasta 4 preguntas)

Solicite todo lo siguiente en un solo formulario:

1. **Título de la página** — presenta 2-3 variantes sugeridas derivadas de lo que el usuario ya le dijo, además de una trampilla de escape &quot;Otro&quot;.
2. **Carpeta de temas**: presente las 5 carpetas válidas como opciones; recomiende la más probable en función de la entrada del usuario.
3. **Soluciones de Adobe**: selección múltiple; sugiera los candidatos más probables según el tema de la página.
4. **Recuento de diagramas**: cuántos diagramas incluirá la página (1 / 2 / 3 / 4+).

### Ronda 2: detalles del diagrama (una llamada a AskUserQuestion, hasta 4 preguntas)

Pida el nombre de archivo de la imagen de cada diagrama y el propósito de la página de una forma:

- Para cada diagrama (hasta 2 en una sola ronda de formulario), pregunte por **nombre de archivo de imagen** como una pregunta con 2-3 nombres de archivo sugeridos (derivados del título de la página) más una opción &quot;Otro&quot;.
- Pregunte por el **propósito de la página** (descripción de la oración 1-2) como una pregunta con 2-3 frases sugeridas más &quot;Otro&quot;.
- Pregunte si se necesita una llamada **`>[!MORELIKETHIS]`** (Sí/No). En caso afirmativo, recopile la dirección URL y el texto del vínculo en un mensaje de seguimiento.

> **Títulos de sección y texto alternativo:** Cuando el nombre de archivo de la imagen es descriptivo (por ejemplo, `fac-architecture.svg`, `fac-dataflow.svg`), deduzca el título de sección H2 y el texto alternativo de él, no es necesario preguntar al usuario. Utilice el nombre de archivo, con mayúsculas y minúsculas y humanizado, como título de sección (por ejemplo, `Architecture diagram`, `Data flow diagram`). Pregunte únicamente si el nombre del archivo es ambiguo.

### Ronda 3: patrones de casos de uso (AskUserQuestion después del análisis)

Antes de presentar este formulario, **glob`/help/blueprints/use-case-patterns/`** e identifique de 3 a 5 patrones coincidentes probables en función del título de la página, el propósito y las soluciones. Confirme que cada archivo existe antes de sugerirlo.

Presentar los 4 candidatos principales como una pregunta de `multiSelect`. Si existe un quinto candidato fuerte, siga con una pregunta separada de sí/no para ese candidato. Invite también al usuario a nombrar cualquier patrón que se haya perdido.

Incluir solo patrones cuyos archivos se confirmen que existen. No alucinar nombres de patrones.

### Ronda 4: flujos de datos y vínculos de Experience League (una llamada a AskUserQuestion)

**Flujos de datos:** Proponer de 3 a 5 viñetas de flujo de datos preescritas como una pregunta `multiSelect` (derivada del tema de la página). El usuario selecciona cuál aplicar. Mantenga cada opción en una oración concisa. Si el usuario necesita flujos personalizados que no estén en la lista, puede proporcionarlos en un seguimiento.

**Vínculos de Experience League:** Después del formulario, presente una tabla de markdown de 4-6 vínculos sugeridos con título de artículo, dirección URL y una lógica de una línea. Marcar cada dirección URL como **sin comprobar**. Pida al usuario que (a) acepte, (b) sustituya por una URL verificada o (c) añada la suya propia. Use un `AskUserQuestion` de seguimiento con hasta 4 opciones si la lista es larga; de lo contrario, acepte la confirmación en texto sin formato.

Nunca invente direcciones URL que no haya recuperado. Si no está seguro, sugiera el título del artículo y deje que el usuario proporcione la URL.

### Cuando se hayan completado todas las rondas

Confirme la información completa establecida con el usuario antes de generar cualquier archivo. Si falta algún elemento requerido o está marcado como &quot;Otro&quot; sin valor, pídalo antes de continuar. No fabrique diagramas, patrones ni vínculos.

## Fase 2: Comprobación del ámbito

Antes de generar, vuelva a leer las descripciones de los diagramas del usuario, las viñetas de flujo de datos y cualquier borrador de prosa. Aplicar las protecciones de `references/scope-guardrails.md`.

Si aparece alguna de las siguientes opciones en el contenido planificado, avise al usuario y ofrezca redirigir esa sección a una página de patrones de caso de uso (o recortarla de la página arquitectura):

- KPI o fórmulas de medición
- Objetivos empresariales o narrativas de impacto empresarial
- Ejemplos de casos de uso tácticos (escenarios de personalización específicos, ejemplos de campañas, etc.)
- Capacidades (estilo `A > B > C > D`)
- Narración guiada por la personalidad

Si el contenido planificado permanece dentro del ámbito de la página de arquitectura (arquitectura de nivel superior, flujo de datos del sistema, puntos de integración, topología de implementación, Edge o hub), confirme con el usuario y continúe a la fase 3.

## Fase 3: Generación de contenido

Genere la página en:

```
/help/blueprints/{topic-folder}/{kebab-filename}.md
```

Usar `references/diagram-template.md` como plantilla de origen. Rellene todos los valores de marcador de posición con la información recopilada. El archivo generado debe incluir:

1. **YAML frontmatter** — `title`, `description`, `solution` solamente.
   - **NO incluya`exl-id`**: la canalización de publicación lo asigna automáticamente.
   - **No incluya** `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt` o `thumbnail`; también se rellenan automáticamente.

2. **Encabezado H1**: el título de la página.

3. **Párrafo de apertura**: 1-2 frases derivadas de la entrada con fines de página.

4. **Bloque `>[!MORELIKETHIS]` opcional** — solo si el usuario proporcionó un vínculo de contenido relacionado.

5. **Una sección H2 por diagrama**, en el orden en que los proporcionó el usuario. Cada sección contiene:
   - El título de la sección como encabezado H2
   - 1-2 oraciones que explican el propósito del diagrama
   - La imagen se incrusta utilizando la convención estándar de:

     ```html
     <img src="assets/{filename}" alt="{Alt Text}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />
     ```

6. **`## Use case patterns supported`** — lista con viñetas. Cada viñeta:

   ```
   - [{Pattern name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) -- {1-line note on why this architecture enables the pattern}
   ```

7. **`## Primary data flows and integration points`**: lista con viñetas de 3 a 7 elementos de flujo/integración.

8. **`## Further reading`** — lista con viñetas de vínculos de Experience League:

   ```
   - [{Article title}]({Experience League URL})
   ```

Utilice la sintaxis `[!DNL ...]` para los nombres de productos de Adobe en el texto del cuerpo y las viñetas, de forma que coincidan con la convención de páginas existentes.

## Fase 4: Actualizaciones de referencias cruzadas

Actualice **`/help/blueprints/TOC.md`** para agregar la nueva página a la navegación. Esta es la única página de referencia cruzada que se puede actualizar.

Lea `references/toc-placement.md` las reglas y la tabla de asignación de subsecciones completa. Resumen:

| Carpeta de temas | Subsección del índice |
| --- | --- |
| `experience-platform/` | `+ Architecture overviews{#architecture-overview}` |
| `experience-platform/deployment/` | `+ Deployment{#deployment}` (subsección de descripciones generales de arquitectura) |
| `audience-activation/` | `+ Audience & Profile Activation{#audience-activation}` |
| `b2b/` | `+ B2B activation & marketing{#b2b-activation}` |
| `customer-journey-analytics/` | `+ Customer Journey Analytics{#customer-journey-analytics}` |
| `customer-journeys/` | `+ Customer journeys{#customer-journeys}` |

Formato de entrada (sangría de 4 espacios + `+`):

```
    + [{Page title}](/help/blueprints/{topic-folder}/{filename}.md)
```

Anexe la nueva entrada como el último elemento de la subsección correspondiente, a menos que el usuario especifique una posición diferente. Conservar la sangría exacta de 4 espacios: el análisis del índice depende de él.

**Inspeccione los subgrupos anidados antes de colocarlos.** Algunas subsecciones (en particular `Audience & Profile Activation`) contienen agrupaciones anidadas (por ejemplo, `Real-Time Customer Data Platform (RTCDP) {#known-customer-audience-activation}`). Lea la subsección afectada de TOC.md antes de editar. Las nuevas páginas de arquitectura de nivel superior pertenecen al nivel de sangría de 4 espacios de la subsección: **no** dentro de un subgrupo anidado (que usa sangría de 6 espacios). Coloque la nueva entrada después de la última entrada de subgrupo anidada y antes del siguiente encabezado de subsección de nivel superior.

## Fase 5: Validación

Una vez creados y actualizados todos los archivos, compruebe lo siguiente e informe de cualquier error al usuario:

1. **Existencia del recurso de imagen**: para cada diagrama, compruebe que `/help/blueprints/{topic-folder}/assets/{filename}` existe. **Advertir** si falta; no bloquear (el usuario puede estar creando en paralelo con el diseño del diagrama). Aparecer una lista clara de los archivos que faltan para que el usuario sepa qué añadir.

2. **Vínculos de patrones de casos de uso**: cada vínculo de patrones del archivo señala a un archivo Markdown existente en `/help/blueprints/use-case-patterns/`. Use `Read` o glob para confirmar que existe cada destino.

3. **Vínculos de Experience League**: compruebe de forma puntual que todas las direcciones URL de la sección `## Further reading` empiecen por `https://experienceleague.adobe.com/`.

4. **Ubicación de la entrada de índice**: la nueva entrada se encuentra dentro de la subsección correcta, utiliza sangría de 4 espacios y la ruta de acceso coincide exactamente con la ubicación del archivo generado.

5. **Nomenclatura de archivo**: el nombre de archivo de la página es minúscula y coincide con la ruta a la que se hace referencia en TOC.md.

6. **Finalización de la materia frontal** — La página incluye `title`, `description` y `solution`. Debe **no** incluir `exl-id`, `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt` o `thumbnail`.

Corrija los problemas de validación antes de considerar que la tarea se ha completado.

## Notas

- Utilice siempre la sintaxis `[!DNL ...]` para los nombres de productos de Adobe en el texto del cuerpo y las viñetas, siguiendo la convención de las páginas existentes.
- Los diagramas de arquitectura suelen ser SVG (preferidos para nitidez y escalado), pero PNG es aceptable para ilustraciones de fuente rasterizada.
- La cadena de estilo en línea `<img>` incrustada (`border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;`) y `class="modal-image"` son necesarias; habilitan la interacción de zoom modal de Experience League.
- Si el usuario está creando una página para una carpeta de temas completamente nueva que aún no existe, adviértele de que TOC.md necesita una nueva subsección de nivel superior bajo `+ Architecture Diagrams and Blueprints{#architecture-diagrams}`. Gestionarlo como un paso independiente con la aprobación explícita del usuario.
- Si el diagrama de arquitectura documenta ampliamente un *caso de uso único de extremo a extremo* (con KPI, objetivos empresariales y capacidades), redirija al usuario a `use-case-pattern-builder`; no es una página de arquitectura.
