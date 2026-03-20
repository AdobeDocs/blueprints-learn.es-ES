---
name: use-case-pattern-builder
description: 'Creación de guía del nuevo contenido de patrón de caso de uso para el repositorio de modelos de Adobe Experience Platform. Utilice esta habilidad cuando añada un nuevo patrón de caso de uso, cree contenido de guía de implementación o cuando el usuario mencione la adición de patrones al sitio de modelos. Gestiona el flujo de trabajo completo: recopilación de información de patrones, generación del archivo Markdown con la estructura de plantilla correcta y actualización de todas las páginas de referencia cruzada (TOC.md, overview.md).'
source-git-commit: ed8928687806b619e95d8d320478d27c13722a80
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---


# Generador de patrones de casos de uso

Esta aptitud guía la creación de un nuevo patrón de caso de uso para el repositorio de modelos de Adobe Experience Platform. Gestiona el flujo de trabajo completo: recopila información sobre el patrón del usuario, genera el archivo de contenido Markdown con la estructura de plantilla correcta y actualiza todas las páginas de referencias cruzadas para que el nuevo patrón sea detectable.

Antes de empezar, lea los siguientes archivos de referencia para ver la estructura completa de la plantilla y la lista de comprobación de páginas que desea actualizar:

- `references/pattern-template.md`: la plantilla de markdown completa con valores de marcador de posición
- `references/pages-to-update.md`: la lista de comprobación de páginas que deben actualizarse al agregar un patrón

## Fase 1: Recopilación de información

Entrevista al usuario para recopilar toda la información necesaria antes de generar los archivos. Pida lo siguiente y no continúe con la generación de contenido hasta que se proporcione cada elemento o se difiera explícitamente.

### Información requerida

1. **Nombre de patrón**: el título legible en lenguaje natural (por ejemplo, &quot;Mensajería activada por eventos&quot;).

2. **Categoría** — Exactamente una de las siguientes:
   - `audience-building-activation`
   - `personalization`
   - `campaign-management-orchestration`
   - `analysis`
   - `conversational-experience`

3. **Descripción de la capacidad principal**: una sola frase que describe lo que hace este patrón (se utiliza en la tabla de información general y en la descripción de la materia principal).

4. **Soluciones principales de Adobe**: los productos de Adobe fundamentales para este patrón. Elija entre: Journey Optimizer, Real-Time Customer Data Platform, Experience Platform, Customer Journey Analytics, Brand Concierge, Journey Optimizer B2B edition, Real-Time CDP B2B edition u otros según corresponda.

5. **Pasos de la cadena de funciones**: de 3 a 6 fases secuenciales que describen el flujo de ejecución del patrón, separadas por `>`. Ejemplo: &quot;Ingesta de eventos > Entrada de Recorrido > Evaluación de condiciones > Entrega de mensajes > Informes&quot;.

6. **Se admiten objetivos empresariales** — Uno o más objetivos empresariales del conjunto existente en `/help/blueprints/business-objectives/`. Cada uno debe incluir el nombre del objetivo, la subcarpeta de categoría y el nombre de archivo. Compruebe que los archivos a los que se hace referencia existen antes de generar contenido.

7. **Casos de uso tácticos de ejemplo** — 6-10 escenarios con viñetas que describen cómo se puede aplicar este patrón en diferentes contextos comerciales. Cada uno debe tener un nombre de escenario en negrita seguido de una descripción.

8. **KPI**: una tabla con tres columnas: KPI (nombre), Descripción (qué mide), Medición (fórmula o enfoque).

9. **Opciones de implementación** — 2-4 opciones de implementación. Para cada opción, recopile:
   - Nombre de opción
   - Lo mejor para (cuándo usar esta opción)
   - Cómo funciona (2 a 4 párrafos)
   - Consideraciones clave (lista con viñetas)
   - Ventajas (lista con viñetas)
   - Limitaciones (lista con viñetas)
   - Vínculos de Experience League (direcciones URL a documentación relevante)

### Opcional pero recomendada

- Ejemplos de casos de uso (párrafos 3 a 5; si no se facilitan, extráigalos de la otra información)
- Lista de aplicaciones con descripciones de la función de cada aplicación de Adobe
- Tabla de funciones básicas (función, estado, qué debe estar en su lugar, referencia de Experience League)
- Tabla de funciones de soporte (función, estado, por qué importa, referencia de Experience League)
- Tablas de funciones de la aplicación (una por aplicación, con función, fase de implementación, descripción)
- Lista de comprobación de requisitos previos

Si el usuario no proporciona los elementos opcionales, genere valores predeterminados razonables basados en la categoría del patrón, las soluciones y la cadena de funciones.

## Fase 2: Generación de contenido

Genere el archivo de marcador de patrón en la siguiente ruta:

```
/help/blueprints/use-case-patterns/{category}/{kebab-case-pattern-name}.md
```

El nombre de archivo debe utilizar un kebab-case derivado del nombre del patrón. Por ejemplo, &quot;Mensajería activada por eventos&quot; se convierte en `event-triggered-messaging.md`.

Utilice la plantilla de `references/pattern-template.md` y rellene todos los valores de marcador de posición con la información recopilada. El archivo generado debe incluir todas las secciones de la plantilla:

1. **YAML frontmatter** — título, descripción, solución (separada por comas), exl-id (genera un marcador de posición UUID como `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` — el equipo de publicación asignará el real).

2. **Sección de apertura** — `# {Pattern name}` encabezado seguido de un párrafo introductorio y el texto &quot;Use esta guía para entender...&quot; sentencia.

3. **Resumen del caso de uso**: de 3 a 5 párrafos que describen el ámbito del patrón, cuándo se aplica, qué hace y no hace, y quiénes son las partes interesadas habituales.

4. **Objetivos empresariales clave**: cada objetivo tiene un encabezado vinculado con una breve descripción y una fila de resumen de KPI.

5. **Casos de uso tácticos de ejemplo**: lista con viñetas de 6 a 10 escenarios.

6. **Indicadores clave de rendimiento** — Tabla con KPI, Descripción, Columnas de medición.

7. **Patrón de caso de uso**: párrafo de descripción y cadena de funciones.

8. **Aplicaciones**: lista de aplicaciones de Adobe con formato y descripciones de `[!DNL ...]`.

9. **Funciones básicas** — Tabla con columnas: Función básica, Estado, Lo que debe estar en su lugar, Referencia de Experience League. Valores de estado: Necesario, Supuesto en su lugar, No aplicable.

10. **Funciones de soporte** — Tabla con columnas: Función de soporte, Estado, Por qué importa, Referencia de Experience League. Valores de estado: Recomendado, Incluido, No aplicable.

11. **Funciones de la aplicación** — Una tabla por aplicación con columnas: Función, Fase de implementación, Descripción.

12. **Requisitos previos**: lista de comprobación con sintaxis `- [ ]`.

13. **Opciones de implementación** — 2-4 opciones detalladas, cada una con los vínculos Mejor para, Cómo funciona, Consideraciones clave, Ventajas, Limitaciones y Experience League.

14. **Comparación de opciones**: tabla de comparación de resumen al final.

## Fase 3: Actualizaciones de referencias cruzadas

Después de generar el archivo de patrón, actualice los siguientes archivos. Lea `references/pages-to-update.md` la lista de comprobación detallada.

### TOC.md

**Archivo:** `/help/blueprints/TOC.md`

Añada una nueva entrada en la sección de categoría correcta. Las categorías se asignan a estas secciones del índice:

| slug de categoría | Encabezado de sección del índice |
| --- | --- |
| `audience-building-activation` | `+ Audience Building & Activation{#audience-building-activation}` |
| `personalization` | `+ Personalization{#personalization-patterns}` |
| `campaign-management-orchestration` | `+ Campaign Management & Orchestration{#campaign-orchestration-patterns}` |
| `analysis` | `+ Analysis{#analysis-patterns}` |
| `conversational-experience` | `+ Conversational Experience{#conversational-experience-patterns}` |

El formato de entrada es:

```
    + [{{Pattern Title}}](/help/blueprints/use-case-patterns/{{category}}/{{filename}}.md)
```

Agregue la nueva entrada después de la última entrada existente en la sección correspondiente. Conservar la sangría exacta (cuatro espacios antes de `+`).

### Página de información general

**Archivo:** `/help/blueprints/use-case-patterns/overview.md`

Agregue una nueva fila a la tabla de categorías correcta. El formato es:

```
| [{{Pattern Title}}]({{category}}/{{filename}}.md) | {{Primary capability description}} | [!DNL {{Solution1}}], [!DNL {{Solution2}}] |
```

Agregue la nueva fila después de la última fila existente en la tabla de categorías coincidente.

## Fase 4: Validación

Una vez creados y actualizados todos los archivos, compruebe lo siguiente:

1. **Vínculos de objetivos empresariales**: todos los vínculos de objetivos empresariales del archivo de patrones apuntan a un archivo existente en `/help/blueprints/business-objectives/`. Utilice glob o read para confirmar que cada archivo de destino existe.

2. **Ubicación de la entrada del índice**: la nueva entrada del índice se encuentra dentro de la sección de categoría correcta y usa la sangría y el formato de ruta correctos.

3. **Fila de tabla de información general**: la nueva fila de información general se encuentra en la tabla de categorías correcta y sigue el mismo formato de columna que las filas existentes.

4. **Nomenclatura de archivo**: el nombre de archivo del patrón usa kebab-case y coincide con la ruta a la que se hace referencia en TOC.md y overview.md.

5. **Complejidad de Frontmatter**: el archivo de patrón incluye título, descripción, solución y exl-id en su frontmatter de YAML.

6. **Vínculos de Experience League**: compruebe de forma puntual que las direcciones URL de Experience League son plausibles (comience por `https://experienceleague.adobe.com/es`).

Informe al usuario de cualquier error de validación y corríjalo antes de considerar que la tarea se ha completado.

## Notas

- Utilice siempre la sintaxis `[!DNL ...]` para los nombres de productos de Adobe en tablas y texto independiente, siguiendo la convención de archivos de patrones existentes.
- `exl-id` en frontmatter debe ser un UUID de marcador de posición. La canalización de publicación asigna el valor real.
- Si el usuario desea crear varios patrones a la vez, repita las Fases 2-4 para cada patrón, pero recopile toda la información en la Fase 1.
- Si se necesita una nueva categoría que no existe en la lista anterior, avise al usuario de que TOC.md y overview.md necesitarán que se creen nuevas secciones y gestiónelas como un paso independiente.
