---
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---
# Adobe Experience League: referencia de campos de metadatos aprobados

*Procedente de la Guía de creación de Adobe ExL (rastreada en febrero de 2026) + análisis de repositorios de blueprints-learn.es*

&#x200B;---

## Jerarquía de metadatos

Los metadatos se acumulan en cascada en este orden (el artículo anula la TDC, la TDC anula la cesión temporal):
1. Antecedentes del artículo (máxima prioridad)
2. TOC.md en la guía del usuario
3. metadata.md en la raíz del repositorio (prioridad más baja)

&#x200B;---

## Campos de nivel de artículo

### OBLIGATORIO

| Campo | Descripción | Formato / Restricciones |
|-------|-------------|----------------------|
| `title` | Título de la página SEO. Aparece en los resultados de búsqueda. | Máximo de ~60 caracteres; caso de título; use `[!DNL Product]` para nombres de productos; NO duplique H1 exactamente a menos que se pretenda |
| `description` | Descripción de Meta para motores de búsqueda y recomendaciones ExL. | 150-160 caracteres; idealmente comienza &quot;Aprenda a...&quot; o &quot;Más información...&quot;; la validación falla si falta/es nula |
| `exl-id` | Identificador único asignado al sistema. Se utiliza para el seguimiento de contenido. | Formato UUID (p. ej. `70573eb9-cd69-4fe6-b2ae-dae81665a308`); **eliminar al copiar un archivo**; se asignará automáticamente; nunca se duplicará entre archivos |

### MUY RECOMENDADO

| Campo | Descripción | Valores válidos |
|-------|-------------|--------------|
| `solution` | Los productos de Adobe que cubre el artículo. Se utiliza para la búsqueda/filtrado de ExL y recomendaciones de contenido. | Separado por comas; distingue entre mayúsculas y minúsculas; debe coincidir con la enumeración aprobada (consulte Valores válidos de solución a continuación) |

### OPCIONAL: COMÚN

| Campo | Descripción | Valores válidos/Notas |
|-------|-------------|----------------------|
| `kt` | Número JIRA del artículo de conocimientos heredado. Se utiliza para el seguimiento de análisis. | Entero (p. ej. `7207`); en blanco aceptable; `null` aceptable |
| `thumbnail` | Referencia de imagen en miniatura para Recommendations/Analytics. | Cadena de nombre de archivo o `null` o en blanco |
| `version` | Filtro de versión del producto. Se utiliza principalmente para modelos de AEM y Campaign. | E.g. `Campaign v8`, `Campaign v8 Client Console`; debe coincidir con version.yml |
| `doc-type` | Clasificación de contenido utilizada en el repositorio/análisis. | `blueprint`, `overview-page`, `Video`, `Tutorial`, `Troubleshooting` (se prefieren las minúsculas) |
| `feature` | Etiquetas de temas mostradas como &quot;Temas&quot; en páginas ExL. | 1-2 por artículo; caso de título; debe coincidir con feature.yml; separado por comas |
| `feature-set` | Aplicación principal para la validación de funciones. | Debe coincidir con los valores feature.yml |
| `role` | Función de audiencia de Target. Se muestra como &quot;Creado para&quot; en ExL. | `Admin`, `Architect`, `Data Architect`, `Data Engineer`, `Developer`, `Leader`, `User` |
| `level` | Nivel de experiencia del usuario. Se muestra como &quot;Creado para&quot; en ExL. | `Beginner`, `Intermediate`, `Experienced` (caso de título) |
| `topic` | Temas entre productos para búsqueda/filtrado. | Título, mayúsculas y minúsculas; debe coincidir con topic.yml; separado por comas |
| `type` | Clasificación de la guía. | `Documentation` (predeterminado), `Tutorial`, `Troubleshooting` |
| `last-substantial-update` | Muestra el contenido en widgets &quot;Novedades&quot;. | Formato: `YYYY-MM-DD` |
| `hide` | Excluye la página de todas las búsquedas y recomendaciones; también establece el índice en no. | `yes` o `no` |
| `hidefromtoc` | Elimina de la navegación del índice, pero aún se puede acceder a la página mediante un vínculo directo. | `yes` o `no` |
| `index` | Controla si la página aparece en la búsqueda externa o en el mapa del sitio. | `yes`/`no` o `y`/`n`; predeterminado: `no` (indizado) |
| `recommendations` | Controla el comportamiento del widget &quot;Más ayuda sobre esta función&quot;. | `noDisplay` (evita que se muestre el widget), `noCatalog` (excluye del grupo de recomendaciones) |
| `internal` | Marca la página como solo interna de Adobe. Evita el indicador de vínculos internos. | `yes` |
| `short-description` | Descripción condensada de las páginas de aterrizaje de ExL. Usa `description` si se omite. | Una frase; máximo ~20 palabras |
| `activity` | Clasificación de uso de página. | `understand`, `implement`, `troubleshoot` (minúsculas) |
| `sub-product` | Subcomponente de producto. Trabaje con equipos de solución para obtener enumeraciones válidas. | Minúsculas; p. ej. `search`, `assets`, `sites` |
| `team` | Asignación de equipo para Analytics. | E.g. `TM` |
| `landing-page-name` | Vínculos a la página de aterrizaje para la ruta. | E.g. `experience-manager` |
| `landing-page-breadcrumb-title` | Texto de ruta para el vínculo de la página de aterrizaje. | E.g. `AEM` |
| `auto-video-transcripts` | Activa las transcripciones de vídeo de forma predeterminada. | `true` |
| `badgeType` | Insignia para el estado del contenido. | Varía; p. ej. `informative`, `positive` |
| `badgePremium` | Indicador de insignia Premium. | Especificación de distintivo según Adobe |
| `badgeLabel` | Texto de etiqueta de distintivo. | Cadena corta |
| `source-git-url` | URL del repositorio de Source. | URL completa de GitHub |
| `cloud` | Anulación de la categoría de nube en el nivel de artículo. | Título; debe coincidir con cloud.yml |

&#x200B;---

## Campos de TOC.md

| Campo | Descripción | Notas |
|-------|-------------|-------|
| `user-guide-title` | Nombre de la guía mostrado en las rutas de exploración y páginas de aterrizaje de ExL. | Necesario para archivos de índice |
| `breadcrumb-title` | Nombre de guía más corto para las rutas de exploración cuando user-guide-title es demasiado largo. | Opcional |
| `user-guide-description` | Resumen de la guía de la página de aterrizaje de ExL. | Una frase; máximo: 20 palabras recomendadas |
| `product` | Seguimiento de Analytics para la guía. Solo valor único. | Debe coincidir con product.yml (consulte Valores de producto válidos) |
| `mini-toc-levels` | Número de niveles de encabezado que se muestran en el mini-TOC de navegación derecha. | Entero 1-6; predeterminado 2 |
| `role` | Función de audiencia predeterminada para la guía. | Mismos valores que el artículo `role`; separados por comas |
| `index` | Si la guía está indexada. | `yes`/`no` |

&#x200B;---

## Campos metadata.md del nivel de repositorio

| Campo | Notas |
|-------|-------|
| `cloud` | Categoría de nube predeterminada para todos los artículos del repositorio |
| `solution` | Solución predeterminada para todos los artículos |
| `product` | Producto predeterminado para el seguimiento de análisis |
| `type` | Tipo de guía predeterminado |
| `doc-type` | Tipo de documento predeterminado |
| `mini-toc-levels` | Niveles de mini-TOC predeterminados |
| `git-repo` | URL del repositorio de GitHub; habilita los botones &quot;Editar esta página&quot; y &quot;Registrar problema&quot; |
| `index` | Configuración de índice predeterminada |

&#x200B;---

## Valores De Solución Válidos (Distinguen Entre Mayúsculas Y Minúsculas)

Valores comunes utilizados en este repositorio:
- `Experience Platform`
- `Real-Time Customer Data Platform`
- `Journey Optimizer`
- `Journey Optimizer B2B Edition`
- `Customer Journey Analytics`
- `Campaign`
- `Campaign v8`
- `Campaign Classic v7`
- `Campaign Standard`
- `Audience Manager`
- `Target`
- `Analytics`
- `Data Collection`
- `Commerce`
- `Marketo Engage`
- `Experience Cloud`
- `Journey Orchestration`

Varios valores: separados por comas, p. ej. `Real-Time Customer Data Platform, Campaign`

&#x200B;---

## Valores de producto válidos (para el campo `product` — seguimiento de análisis)

Consulte la solicitud del sistema para obtener una lista completa. Valores clave:
- `adobe experience platform` / `experience platform` / `aem`
- `adobe analytics` / `analytics` / `aa`
- `adobe journey optimizer` / `journey optimizer` / `jo`
- `adobe customer journey analytics` / `customer journey analytics` / `cja`
- `adobe real time customer data platform` / `real time cdp` / `rtcdp`
- `adobe marketo` / `marketo` / `amk`
- `adobe campaign` / `campaign` / `ac`
- `adobe target` / `target` / `at`

&#x200B;---

## Valores de rol válidos

- `Admin`
- `Architect`
- `Data Architect`
- `Data Engineer`
- `Developer`
- `Leader`
- `User`

&#x200B;---

## Reglas de validación de claves

1. Nunca deje `exl-id` con el mismo UUID en un archivo copiado: elimínelo y permita que el sistema asigne uno nuevo.
2. Se aceptan `thumbnail` y `kt` vacíos o nulos; estos son campos heredados.
3. Los valores de `solution` deben coincidir exactamente con la enumeración aprobada (distingue entre mayúsculas y minúsculas).
4. La validación de `description` falla si falta o es nula; proporcione siempre un valor significativo.
5. Ajuste `title` valores entre comillas si contienen dos puntos, corchetes o caracteres especiales iniciales.
6. Los valores `solution` múltiples se separan con comas dentro de un solo valor de cadena.
7. `product` es solo de un valor (para el seguimiento de analytics); no utilice valores separados por comas.
8. Para solicitar nuevos valores de enumeración, presente un ticket JIRA de UGP con el componente &quot;Etiquetado de contenido&quot;.
