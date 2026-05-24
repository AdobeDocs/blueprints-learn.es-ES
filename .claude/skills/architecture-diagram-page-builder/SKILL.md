---
name: architecture-diagram-page-builder
description: 'Creación de guías de creación de nuevas páginas de diagrama de arquitectura para el repositorio de modelos de Adobe Experience Platform. Utilice esta aptitud cuando añada un nuevo diagrama de arquitectura de nivel superior, una página de arquitectura de integración o información general sobre la arquitectura de aplicaciones. Las páginas de arquitectura cubren las arquitecturas de aplicaciones y AEP de nivel superior y los puntos de integración principales, no los casos de uso detallados (pertenecen al generador de patrones de casos de uso). Gestiona el flujo de trabajo completo: recopilar información de página, generar el archivo Markdown, colocarlo en la carpeta de temas correcta y actualizar TOC.md.'
source-git-commit: e79d9d6490e4f50c4611dd879b53f0e63a90cd65
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 2%

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

Entrevista al usuario para recopilar toda la información necesaria antes de generar los archivos. No continúe con la generación de contenido hasta que se proporcione o se difiera explícitamente cada elemento requerido.

### Información requerida

1. **Título de página** — El título legible en lenguaje natural (por ejemplo, `Adobe Journey Optimizer architecture diagrams`).

2. **Carpeta de temas** — Donde se encuentra la página. Elija exactamente uno en función del dominio principal del diagrama:
   - `experience-platform/`: diagramas de nivel superior de AEP, de varias aplicaciones o de nivel de plataforma
   - `customer-journeys/`: AJO, Campaign, orquestación de recorrido
   - `customer-journey-analytics/` — Arquitecturas de CJA
   - `audience-activation/` — RTCDP, activación de audiencia y perfil
   - `b2b/`: arquitecturas específicas de B2B

3. **Nombre de archivo** — Teclado, derivado del título de la página (por ejemplo, `Journey Optimizer architecture` -> `journey-optimizer-architecture.md`). Confirme con el usuario.

4. **Propósito de la página** — frases de 1 a 2 que describen lo que ilustran colectivamente los diagramas. Se usa para el campo de frontMatter `description` y el párrafo de apertura.

5. **Soluciones de Adobe**: lista de productos de Adobe central en la página separados por comas. Se usa para el campo de frontmatter `solution`. Ejemplos: `Experience Platform, Journey Optimizer, Customer Journey Analytics`.

6. **Diagramas**: uno o más diagramas. Para cada diagrama, recopile:
   - **Nombre de archivo de imagen** (por ejemplo: `aep_data_flow.svg`). Se prefiere SVG; PNG es aceptable.
   - **Título de sección**: se convierte en el encabezado H2 del diagrama (por ejemplo, `Data flow diagram`, `Detailed architecture diagram`).
   - **Explicación de propósito** — 1-2 oraciones que describen lo que muestra el diagrama.
   - **Texto alternativo**: descripción accesible breve.

7. **Se admiten patrones de casos de uso** — se habilitan de 2 a 5 patrones existentes en esta arquitectura.

   **Recomendar candidatos primero.** Antes de pedirle al usuario que proporcione patrones, analice `/help/blueprints/use-case-patterns/` y proponga de 3 a 6 coincidencias probables en función del título de página, el propósito de página y las soluciones de Adobe recopiladas anteriormente. Para cada sugerencia, presente:
   - Nombre del patrón (con la ruta vinculada)
   - Razones de una sola frase para explicar por qué encaja en esta arquitectura

   Presente las sugerencias como una preselección numerada y pídale al usuario (a) que acepte cualquier, (b) rechace cualquier y (c) añada los patrones que omitió. Solo genere sugerencias que apunten a archivos reales: glob/read para confirmar antes de sugerir. No alucinar nombres de patrones.

   Para cada patrón aceptado, capture la categoría y el nombre de archivo. Valide que cada archivo exista en `/help/blueprints/use-case-patterns/{category}/{pattern-file}.md` antes de generar.

8. **Flujos de datos principales/puntos de integración**: de 3 a 7 viñetas que describen los flujos clave y los límites de integración mostrados en los diagramas (por ejemplo, `Real-time event ingestion from Web SDK to Edge Network`, `Profile synchronization between Experience Platform Hub and Edge`).

9. **Vínculos de Experience League**: de 3 a 6 vínculos a documentación relevante de Experience League para su posterior lectura. Cada uno debe comenzar con `https://experienceleague.adobe.com/`.

   **Recomendar candidatos primero.** En función de las soluciones de Adobe y el propósito de la página, proponga 4-8 artículos de Experience League plausibles (por ejemplo, las páginas de aterrizaje canónicas o de información general para cada solución con nombre, guías de integración clave, referencias de implementación). Para cada sugerencia, presente:
   - Título del artículo
   - URL
   - Argumento de una línea para saber por qué se ajusta a la página

   Marque las sugerencias como **no verificadas** a menos que haya recuperado la dirección URL; el usuario debe confirmar o reemplazar cada una antes de que aterrice en el archivo generado. Pida al usuario que (a) acepte, (b) sustituya cualquier URL por una verificada que ya tenga y (c) añada la suya propia. Nunca invente direcciones URL que no haya visto; si no está seguro, sugiera el título del artículo y permita que el usuario proporcione la dirección URL.

### Opcional

- **Llamada de contenido relacionado**: un solo vínculo se representa como bloque `>[!MORELIKETHIS]` cerca de la parte superior de la página. Resulta útil cuando hay una guía de integración o configuración del mismo nivel en Experience League que el lector debe tener en cuenta.

Si el usuario no proporciona todos los elementos necesarios, pida los que faltan antes de continuar. No fabrique diagramas, patrones ni vínculos.

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
