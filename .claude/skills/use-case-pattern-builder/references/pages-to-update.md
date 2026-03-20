---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---
# Páginas que se actualizarán al agregar un patrón de caso de uso

Cuando se crea un nuevo patrón de caso de uso, se deben actualizar las siguientes páginas para garantizar que el patrón se pueda detectar y se vincule correctamente.

## Actualizaciones requeridas

### 1. TOC.md
- **Archivo:** `/help/blueprints/TOC.md`
- **Acción:** Agregue una nueva entrada en la sección de categoría correcta
- **Formato:** `    + [{{Pattern Title}}](/help/blueprints/use-case-patterns/{{category}}/{{filename}}.md)`
- **Ubicación por categoría:**
   - Generación de audiencias y activación: después de la línea ~47 (después de las entradas existentes en esa sección)
   - Personalization: después de la línea ~52
   - Orquestación y administración de campañas: después de la línea ~58
   - Análisis: después de la línea ~61
   - Experiencia de conversación: después de la línea ~63

#### Asignación de categoría a índice

| slug de categoría | Encabezado de sección del índice | Anclaje |
| --- | --- | --- |
| `audience-building-activation` | `+ Audience Building & Activation` | `{#audience-building-activation}` |
| `personalization` | `+ Personalization` | `{#personalization-patterns}` |
| `campaign-management-orchestration` | `+ Campaign Management & Orchestration` | `{#campaign-orchestration-patterns}` |
| `analysis` | `+ Analysis` | `{#analysis-patterns}` |
| `conversational-experience` | `+ Conversational Experience` | `{#conversational-experience-patterns}` |

#### Reglas de sangría

- Los encabezados de categoría utilizan dos espacios + `+` (por ejemplo, `  + Personalization{#personalization-patterns}`)
- Las entradas de patrón utilizan cuatro espacios + `+` (por ejemplo, `    + [Pattern Title](path)`)

### &#x200B;2. Información general sobre patrones de casos de uso
- **Archivo:** `/help/blueprints/use-case-patterns/overview.md`
- **Acción:** Agregue una nueva fila a la tabla de categorías correcta
- **Formato:** `| [{{Pattern Title}}]({{category}}/{{filename}}.md) | {{Primary capability description}} | [!DNL {{Solution1}}], [!DNL {{Solution2}}] |`
- **Categorías en la descripción general:**
   - Creación y activación de audiencias (línea ~18)
   - Personalization (línea ~29)
   - Administración y orquestación de campañas (línea ~40)
   - Análisis (línea ~52)
   - Experiencia de conversación (línea ~61)

#### Ejemplo de formato de fila

```
| [Event-Triggered Messaging](campaign-management-orchestration/event-triggered-messaging.md) | Listen for a real-time behavioral or system event, then deliver a contextual message to the triggering profile | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
```

## Lista de comprobación de validación

- [ ] archivo Markdown de patrón creado en el directorio de categoría correcto
- [ ]: Frontmatter incluye el título, la descripción, la solución y el exl-id
- [ ] entrada de TOC.md agregada en la categoría correcta
- [ Se agregó la fila de tabla ] Overview.md en la categoría correcta
- [ ] Todos los vínculos de objetivos empresariales apuntan a archivos existentes
- [ ] El archivo usa la convención de nomenclatura de mayúsculas y minúsculas
- [ ]: todos los vínculos de Experience League son direcciones URL válidas
- [ ] nombres de productos de Adobe utilizan sintaxis `[!DNL ...]`
- [ ] La cadena de funciones utiliza el formato de separador ` > `
- [ ] El archivo de patrón incluye todas las secciones requeridas (consulte pattern-template.md)
