---
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---
# Memoria del agente de Experience League

## Archivos de referencia clave en este repositorio
- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/metadata.md`: valores predeterminados de metadatos de nivel de repositorio
- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/help/blueprints/TOC.md` — metadatos de nivel de guía
- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/.cursor/skills/blueprint-document-reference/reference.md` — patrones de creación de modelo

## Reglas de metadatos (consulte metadata-fields.md para obtener una referencia completa)
- Se requiere la presentación del artículo: `title`, `description`, `exl-id`
- Se RECOMIENDA ENCARECIDAMENTE la presentación del artículo: `solution`
- `exl-id` debe ser un UUID válido; eliminar/dejar en blanco al copiar archivos (asignado automáticamente por el sistema)
- `description` debe comenzar &quot;Aprenda a...&quot; o &quot;Más información...&quot; Directrices de Adobe
- `title` máximo ~60 caracteres para SEO; use `[!DNL ProductName]` para los nombres de productos en el título
- `solution` valores distinguen entre mayúsculas y minúsculas y deben coincidir con la enumeración aprobada (consulte metadata-fields.md)
- Se utilizan `thumbnail: null` o `thumbnail:` (en blanco); se acepta vacío
- `kt:` es un campo heredado (número JIRA del artículo de conocimiento); aún se ve en este repositorio; se puede aceptar en blanco
- Los archivos de índice utilizan: `user-guide-title`, `breadcrumb-title`, `user-guide-description`, `product`, `mini-toc-levels`, `role`
- El nivel de repositorio `metadata.md` usa: `cloud`, `solution`, `product`, `type`, `doc-type`, `mini-toc-levels`, `git-repo`, `index`

## Patrones comunes en este repositorio (blueprints-learn.es)
- La mayoría de los archivos de modelo tienen: `title`, `description`, `solution`, `exl-id`
- Algunos archivos más antiguos también incluyen: `kt`, `thumbnail`
- Algunos archivos utilizan `version` (modelos de Campaign v8)
- Las páginas de información general utilizan `doc-type: overview-page`
- `solution` a menudo contiene varios valores separados por comas: p. ej. `Real-Time Customer Data Platform, Campaign`
- Los archivos SIN `solution` siguen pasando la validación si `exl-id` está presente

## Extensiones de Adobe Markdown utilizadas en este repositorio
- `>[!NOTE]`, `>[!TIP]`, `>[!IMPORTANT]`, `>[!WARNING]`, `>[!CAUTION]`
- `>[!BEGINTABS]` / `>[!TAB Name]` / `>[!ENDTABS]` para contenido con pestañas
- `[!DNL ProductName]` — No localizar etiquetas para nombres de productos
- `[!UICONTROL Label]`: referencias de control de IU
- `{zoomable="yes"}` — atributo de zoom de imagen
- `{width="1000"}` — atributo de anchura de imagen
- `{target="_blank"}` — destino de vínculo externo

## Referencias detalladas
- Referencia de campo de metadatos completo: `metadata-fields.md`
- Guía de creación rastreada: https://experienceleague.adobe.com/en/docs/authoring-guide-exl/using/home (febrero de 2026)
