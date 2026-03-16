---
name: Adobe Experience League Authoring Guidelines
description: Referencia completa para las reglas de creación de Markdown de Adobe Experience League, rastreadas a partir de la guía oficial de creación en marzo de 2026.
type: reference
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 0%

---


# Directrices de creación de Adobe Experience League

Source: https://experienceleague.adobe.com/en/docs/authoring-guide/using/home
Rastreado: 15-03-2026

---

## &#x200B;1. METADATOS / MATERIA PRINCIPAL

### Campos obligatorios
| Campo | Requisito | Reglas |
|---|---|---|
| `title` | Requerido | Máx. 60 caracteres (inglés). Caso de título. No hay nombres de producto a menos que sean necesarios para una mayor claridad. El sistema anexa &quot; | ProductName&quot; automáticamente. Ajuste entre comillas si contiene dos puntos o corchetes. |
| `description` | Requerido | 150-160 caracteres máx. No puede estar en blanco/ser nulo. Los conceptos comienzan por &quot;Aprenda acerca de...&quot; Las tareas comienzan por &quot;Aprenda a...&quot; o verbo imperativo. |

### Campos opcionales pero utilizados con frecuencia
| Campo | Valores válidos | Notas |
|---|---|---|
| `feature` | Debe coincidir con los valores de YAML de la función; el caso del título con los espacios (por ejemplo, &quot;Fragmento de contenido&quot;) | 1-2 por artículo; se muestra en Temas |
| `feature-set` | Debe validarse con la función YAML | Aplicación principal de la función |
| `role` | Usuario, Desarrollador, Responsable, Administrador, Arquitecto, Arquitecto de datos, Ingeniero de datos | Distingue entre mayúsculas y minúsculas; se muestra como &quot;Creado para&quot; |
| `level` | Principiante, Intermedio, Con experiencia | Si no se especifica, el valor predeterminado es Principiante |
| `solution` | Debe coincidir con la solución YAML (por ejemplo, &quot;Campaign, Campaign Standard v7&quot;) | Se permiten varios valores; se utiliza para el filtrado de búsquedas |
| `topic` | Debe coincidir con el tema YAML; caso de título con espacios | Para el filtrado entre productos (por ejemplo, &quot;Integraciones&quot;) |
| `type` | Documentación, tutorial, resolución de problemas | Nivel de repositorio; el valor predeterminado es Documentación |
| `short-description` | Una frase, máximo 20 palabras | Para páginas de aterrizaje de ExL cuando la descripción es demasiado larga |
| `badgePremium` | `label="Premium" type="Positive" url="..."` | Distintivo de nivel de página |
| `mini-toc-levels` | 1-6 (predeterminado 2) | Controla la profundidad de visualización del encabezado de navegación derecho |
| `hidefromtoc` | true/false | Excluye de la navegación izquierda pero mantiene la URL accesible |

### Ubicación de metadatos
- Nivel de artículo: parte superior del archivo Markdown como materia principal YAML
- Nivel de TDC: en el archivo TOC.md
- Nivel de repositorio: en el archivo metadata.md

### Reglas de formato clave
- Agrupe los valores que contengan comas o corchetes entre comillas
- Varios valores separados por comas
- Coincidencia que distingue entre mayúsculas y minúsculas con definiciones de YAML
- Los valores de etiqueta vacíos o en blanco producen un error de validación

### Campos obsoletos
seo-title, seo-description, audience, difference, uuid (from migration era)

---

## &#x200B;2. SINTAXIS DE MARKDOWN (CON SABOR A ADOBE)

### Formato de texto
- Negrita: `**text**`
- Cursiva: `*text*`
- Negrita + Cursiva: `***text***`
- Caracteres especiales de escape: use la barra invertida `\` antes de `# { } [ ] * + - . !`
- Entidades HTML: `&lt;` `&gt;` `&amp;` `&mdash;` `&ndash;`

### Encabezados
- Usar estilo ATX (solo sintaxis `#`, nunca subrayado/estilo de texto)
- Un H1 por documento (normalmente el título de página que coincide con los metadatos `title`)
- Todos los encabezados H2 (`##`) o inferiores posteriores
- Líneas en blanco necesarias antes y después de los encabezados (excepto el primer encabezado)
- Máx. 69 caracteres (inglés) / 120 caracteres (localizado)
- Se prefieren ~5 palabras como máximo
- Mayúsculas y minúsculas en todas las frases (ponga mayúsculas solo en la primera palabra y los sustantivos propios)
- Solo mayúsculas y minúsculas en el título del campo de metadatos `title`
- Sin puntuación final (se permiten signos de interrogación en los encabezados de las preguntas frecuentes)
- Identificadores de anclaje personalizados: `## Title {#custom-id}`: utilice guiones, no puntos
- No hay ID de anclaje de encabezado duplicados en un documento
- Evite los nombres de anclaje reservados: buscar, resultados, facetas, paginación, ordenación, consulta, cuadro de búsqueda, contenido, encabezado, pie de página, principal, navegación, barra lateral, página, contenedor, contenedor
- Siga cada encabezado con al menos un párrafo de texto independiente (no coloque listas o tablas directamente después de un encabezado)
- Encabezados del concepto: frases sustantivadas
- Encabezados de tareas: verbos imperativos (NO gerundios — &quot;Crear un segmento&quot; no &quot;Crear un segmento&quot;)
- Estructura paralela en los niveles de encabezado

### Listas
- Viñeta (sin ordenar): `*`, `-` o `+`: utilice de forma coherente dentro de un documento
- Ordenado: `1.` por cada elemento (números automáticos)
- Líneas en blanco antes y después de listas
- Aplicar sangría a elementos numerados anidados 3 espacios; viñetas anidadas 2 espacios
- Puntuación de viñeta: omita punto y coma/comas/conjunciones al final; agregue puntos solo para oraciones completas.
- No agregue puntos si todos los elementos tienen ≤3 palabras o son etiquetas o encabezados de la interfaz de usuario

### Vínculos
- Externo: `[text](https://url.com)`
- Relativo (mismo nivel): `[text](file.md)`
- Relativo raíz: `[text](/help/path/file.md)` — debe comenzar con `/`
- Vínculos profundos (misma página): `[text](#heading-anchor)`
- Vínculos profundos de documentos cruzados: `[text](file.md#heading-id)`
- Forzar nueva ficha: `[text](url){target="_blank"}`
- Direcciones URL sin formato: ajuste entre corchetes angulares `<https://example.com>` para que se pueda hacer clic en ellas
- Vínculos de referencia: solo funcionan los vínculos absolutos para los vínculos de estilo de referencia
- No incluya el mismo archivo en varias ubicaciones del índice a través de vínculos relativos
- Usuarios de Windows: convertir barras invertidas en barras diagonales en rutas

### Imágenes
- Básico: `![alt text](image.png "hover tooltip")`
- Cambiar tamaño: `{width="300"}`
- Alinear: `{align="center"}` o `{align="right"}`
- Ampliable: `{zoomable="yes"}` o `{modal="regular"}`
- Tamaño máximo de archivo: 100 MB (se recomienda menos de 5 MB)
- Se REQUIERE texto alternativo para todas las imágenes (para SEO y accesibilidad)
- Nombres de archivo de imagen: minúsculas con guiones
- Almacenar imágenes en una carpeta de recursos designada

### Bloques de código
- En línea: acentos graves `` `code` ``
- Se utiliza para: nombres de archivo, direcciones URL, términos definidos por el usuario, comandos
- Bloques de código delimitado: triples comillas invertidas con identificador de idioma

  ```
  ```javascript
  code here
  ```

  ```
  
  
- Opciones: `{line-numbers="true"}`, `{start-line="7"}`, `{highlight="11-13, 16"}`
- Incluya siempre un identificador de idioma en los bloques de código delimitado

### Tablas
- La fila del separador requiere al menos 3 guiones por columna: `|---|---|---|`
- Alineación: izquierda `|---|`, centro `|:---:|`, derecha `|---:|`
- Omitir canalizaciones literales: `\|` o usar `&vert;`
- Se permiten tablas HTML; use `<table style="table-layout:auto">` o `table-layout:fixed`
- Alineación de tabla de HTML: `<td align="left|center|right">`
- Evite la sintaxis Markdown dentro de las tablas de HTML (por ejemplo, `[!NOTE]` no funciona en tablas de HTML)
- Quitar bordes: `<tr style="border: 0;">`
- Opción de diseño de tabla de Markdown: agregar `{style="table-layout:auto"}` después de la tabla con líneas en blanco
- Evite tablas muy anchas/altas debido a problemas de visibilidad de la barra de desplazamiento horizontal

---

## &#x200B;3. EXTENSIONES ESPECIALES DE SINTAXIS DE ADOBE

### Llamadas/amonestaciones

```
>[!NOTE]
>
>Text here.

>[!TIP]
>
>Text here.

>[!IMPORTANT]
>
>Text here.

>[!WARNING]
>
>Text here.

>[!CAUTION]
>
>Text here.

>[!ADMIN]
>[!AVAILABILITY]
>[!PREREQUISITES]
>[!INFO]
>[!ERROR]
>[!SUCCESS]
```
- CRÍTICO: No hay espacio entre `>` y `[!` — usar `>[!NOTE]` NO `> [!NOTE]`
- Agregar línea en blanco entre `>[!NOTE]` y la línea de texto del cuerpo

### Fichas

```
>[!BEGINTABS]

>[!TAB iOS]
Content here

>[!TAB Android]
Content here

>[!ENDTABS]
```

### Secciones contraíbles (acordeones)

```
+++Click to expand
Content inside
+++
```
Nota: NO se admiten secciones contraíbles anidadas.

### Cuadros de sombra

```
>[!BEGINSHADEBOX "Optional Title"]
Content here
>[!ENDSHADEBOX]
```

### Videos

```
>[!VIDEO](https://video.tv.adobe.com/v/ID/?quality=12&learn=on)
```
Agregar `{transcript=true}` para transcripciones.

### Más como esto

```
>[!MORELIKETHIS]
>* [Article 1](url)
>* [Article 2](url)
```

### Ayuda contextual

```
>[!CONTEXTUALHELP]
>id="..."
>title="..."
>abstract="..."
>additional-url="..."
```

### Insignias (en línea)

```
[!BADGE Label]{type=Informative url="https://example.com" tooltip="text"}
```
Tipos: `Informative` (azul), `Positive` (verde), `Negative` (rojo), `Neutral` (gris), `Caution` (amarillo)

### Resaltado de texto (vista previa)

```html
<span class="preview">highlighted text</span>
```

### Incluye y fragmentos de código
- Incluir todo el archivo: `{{$include /help/_includes/legal-blurb.md}}`
- Fragmento (sin encabezados): `{{snippet-id}}`
- Almacenar archivos reutilizables en la carpeta `help > _includes/`
- Fragmentos almacenados en `help > _includes/snippets.md`
- Las inclusiones pueden tener encabezados; los fragmentos de código NO PUEDEN
- Solo funciona dentro del mismo repositorio (no entre repositorios)
- Omitir `{{` o `}}` caracteres en archivos que no hacen referencia

### Etiqueta DNL (no localizar)
- `[!DNL ProductName]`: envuelve nombres de productos o marcas que no deben traducirse
- Uso en la primera o prominente mención dentro de una página

### Etiqueta UICONTROL
- `[!UICONTROL Button Label]`: ajusta el texto del elemento de la interfaz de usuario (botones, menús, nombres de campo).
- Garantiza que las cadenas de IU se extraigan de bases de datos de productos en lugar de traducción automática
- Sin apóstrofos, comillas ni puntuación dentro de las etiquetas UICONTROL
- Utilice el formato de negrita para los elementos de IU a los que se hace referencia en los pasos

### Funciones no admitidas
- Listas de tareas (casillas de verificación)
- Emoji
- Reglas horizontales
- Secciones contraíbles anidadas

---

## &#x200B;4. NOMENCLATURA DE ARCHIVOS Y ESTRUCTURA DE CARPETAS

### Reglas de nomenclatura de archivos
- Nombres de archivo en minúsculas solo con guiones
- Sin mayúsculas, guiones bajos, puntos ni espacios
- Nombres descriptivos y descriptivos (por ejemplo, `calculated-metric-overview.md` no `cmo.md`)
- Evitar números en nombres de archivo; usar palabras descriptivas
- Evitar nombres reservados o en conflicto: `metadata.md`, `search.md`
- El cambio de nombre de archivos activos requiere administración de redireccionamiento (cambios de URL)

### Estructura de carpetas
- Los nombres de directorio/carpeta NO afectan a las URL (solo los nombres de repositorio y los nombres de archivo afectan a las URL)
- TOC.md controla la jerarquía de navegación, no la ubicación de la carpeta Git
- Almacenar imágenes/recursos en una carpeta de recursos designada
- Incluye reutilizables almacenados en `help/_includes/`
- Fragmentos almacenados en `help/_includes/snippets.md`

### Reglas de TOC.md
- Todos los artículos deben aparecer en TOC.md para poder procesarse en Experience League
- Formato H1: `# Guide Title {#anchor-id}` — el anclaje genera la ruta de acceso de la dirección URL base
- Los encabezados de sección deben tener identificadores de anclaje: `+ Section Name {#section-id}`
- Los encabezados de sección (elementos principales) no pueden ser vínculos en sí
- Vínculos de artículo: `+ [Title](path/file.md)`
- Al cambiar los ID de anclaje de sección, se cambian todas las URL de artículo anidadas (requiere redirecciones)
- Usar un estilo de viñeta coherente en (`+`, `*` o `-`)
- Metadatos de TDC: `user-guide-description`, opcionalmente `breadcrumb-title`
- `mini-toc-levels`: controla la visualización de encabezados de navegación derecha (1-6, predeterminado 2)

---

## &#x200B;5. CALIDAD DE CONTENIDO Y ESTÁNDARES EDITORIALES

### Voz y tono
- Voz activa preferida sobre pasiva
- Tiempo presente sobre tiempo futuro
- Segunda persona (&quot;usted&quot;) para contenido informativo
- Frases de menos de 35 palabras
- Verbos fuertes y precisos: evite los adverbios débiles (&quot;muy&quot;, &quot;extremadamente&quot;)

### Pasos y procedimientos
- Cada paso es UN solo comando conciso (una oración)
- La información adicional se incluye en la línea siguiente (con sangría debajo del paso)
- Iniciar cada paso con un verbo imperativo
- Limite los procedimientos a aproximadamente 7 pasos (máximo: ~10 antes de dividir en subtareas)
- Colocar información conceptual ANTES de los pasos
- Realizar capturas de pantalla DESPUÉS del paso correspondiente
- Repetir nombres de páginas/pestañas para la orientación del lector
- Formato UICONTROL en negrita para elementos de la interfaz de usuario por pasos

### Terminología de interfaz
- **Abrir/Cerrar**: aplicaciones y programas
- **Ir a**: menús, pestañas o ubicaciones de IU
- **Seleccionar**: texto, celdas u opciones de listas
- **Hacer clic**: acciones del mouse (ratón) (evitar especificar el tipo de control a menos que sea esencial)
- **Menú desplegable** (no &quot;lista desplegable&quot;)

### Nombres de productos
- No agregue el nombre del producto a títulos o encabezados a menos que la claridad lo requiera
- Omita &quot;the&quot; antes de los nombres de producto
- Incluir &quot;Adobe&quot; en la primera mención a nivel de guía (requisito de marca comercial)
- Coloque &quot;Adobe&quot; en menciones secundarias a menos que sea legalmente requerido
- Utilice etiquetas DNL para los nombres de productos a fin de evitar traducciones incorrectas

### Énfasis y formato
- Negrita: elementos de la IU y acciones del teclado
- Cursiva: mensajes de error, palabras extranjeras, énfasis
- Código (acento grave): nombres de archivo, direcciones URL, términos definidos por el usuario
- No hay comillas alrededor de los elementos de la interfaz de usuario (utilice la etiqueta UICONTROL en su lugar)

### Capitalización
- Caso de oración para encabezados, navegación, subencabezados
- Solo mayúsculas y minúsculas en el título del campo de metadatos `title`
- Los sustantivos propios siempre aparecen en mayúsculas

---

## &#x200B;6. PRÁCTICAS RECOMENDADAS DE SEO

- Un H1 por página: debe ser conciso, descriptivo y debe indicar a los usuarios de qué trata la página
- Jerarquía de encabezados secuencial (h1 → h2 → h3, no omitir nunca niveles)
- Incluir palabras clave en H1, texto independiente y metadatos (no la metaetiqueta `keywords`; Google la ignora)
- Evite el relleno de palabras clave (intención > frecuencia)
- Título: 50-60 caracteres como máximo; el sistema anexa &quot;|&quot; Adobe &quot;ProductName&quot; automáticamente
- Descripción: de 150 a 160 caracteres; debe ser una call to action, no una repetición de contenido
- Agregar texto alternativo descriptivo a todas las imágenes
- Incluir transcripciones de vídeo (los motores de búsqueda solo pueden leer texto)
- Vincular estratégicamente a páginas relacionadas (evitar páginas huérfanas)
- Incluir elementos estructurados: listas numeradas, subencabezados, bloques de código
- Utilice herramientas como AnswerThePublic o Google Trends para buscar palabras clave
- El contenido debe demostrar E-E-A-T (experiencia, experiencia, autoridad, fiabilidad)

---

## &#x200B;7. LOCALIZACIÓN

### Traducción automática primero
- El contenido de origen en inglés genera automáticamente versiones localizadas
- Idiomas admitidos: alemán, francés, japonés, italiano, español, portugués de Brasil, chino simplificado, chino tradicional, coreano, holandés, sueco

### Escribir para localización
- Terminología coherente en todo
- Frases cortas y voz activa
- Orden de palabras estándar en inglés (objeto de → de verbo de → de asunto)
- Usar pronombres relativos (&quot;eso&quot;, &quot;cuál&quot;)
- Evite: humor, expresiones idiomáticas, jerga, frases regionales, metáforas, palabras innecesarias

### Etiquetas de localización
- `[!UICONTROL Label]`: garantiza que las cadenas de interfaz de usuario se extraigan de la base de datos del producto, no traducidas por el equipo
- `[!DNL ProductName]`: evita que se traduzcan los nombres de productos o marcas
- Las imágenes de una carpeta &quot;no localizar&quot; se excluyen de la localización

---

## &#x200B;8. TIPOS DE CONTENIDO

- **Guía**: colección en línea de páginas a las que se hace referencia en un índice; abarca las prácticas recomendadas oficiales
- **Tutorial**: contenido instructivo (vídeo o texto) para casos de uso específicos; publicado en repositorios de aprendizaje
- **Guía de referencia**: API/SDK de desarrollador; normalmente en formato de tabla; publicado en developer.adobe.com
- **Curso**: conjunto de lecciones revisadas por expertos y dirigidas a roles de usuario específicos
- **Artículos de la base de conocimiento**: contenido de solución de problemas breve y relevante temporalmente
- **Página de aterrizaje/página principal**: administrado por separado (SCCM)

---

## &#x200B;9. ERRORES DE VALIDACIÓN COMUNES QUE SE DEBEN EVITAR

- Faltan los metadatos `title` o `description`, o están en blanco
- `description` no comienza con &quot;Más información...&quot; o &quot;Aprenda a...&quot;
- Espacio entre `>` y `[!` en la sintaxis de llamada (`> [!NOTE]` en lugar de `>[!NOTE]`)
- Espacios en marcadores en negrita: `**text **` (espacios finales en negrita)
- Sintaxis de Markdown dentro de tablas de HTML (por ejemplo, las llamadas no funcionan allí)
- Duplicar ID de anclaje de encabezado en un documento
- ID de anclaje que contienen puntos (utilice guiones en su lugar)
- Usar nombres de anclaje reservados (búsqueda, resultados, encabezado, pie de página, etc.)
- `role`, `level`, `feature`, `topic` valores que no coinciden con las definiciones de YAML
- Encabezados apilados sin texto independiente entre ellos
- H1 ha utilizado más de una vez por documento
- Niveles de encabezado omitidos (por ejemplo, H1 → H3)
- Nombrar archivos con mayúsculas, guiones bajos o espacios
- Falta texto alternativo en las imágenes
- Encabezados de tareas gerundinales (&quot;Creando...&quot; en lugar de &quot;Crear...&quot;)
