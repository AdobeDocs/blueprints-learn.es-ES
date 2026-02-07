---
source-git-commit: dfa21942ecf2a1db06df6f6cc945f5572811ca93
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 2%

---
# Referencia de documento de modelo: guía detallada

## Tipos de documento

| Tipo | Finalidad | Ubicación/ejemplo |
|------|---------|--------------------|
| **Información general / hub** | Presenta un producto o área; vínculos a modelos de escenario | p. ej. `overview.md`, `journey-optimizer-overview.md` |
| **Modelo de escenario** | Caso de uso único: arquitectura, pasos, barreras | p. ej. `real-time-lookup.md`, `journey-optimizer-journeys.md` |
| **TDC** | Navegación; no utilizar como plantilla de contenido | `help/blueprints/TOC.md` |

&#x200B;---

## Referencia de sección completa

### Título y descripción (contenido preliminar)

- **título**: corto, específico. Use `[!DNL Product Name]` para los nombres de productos (por ejemplo: `[!DNL Journey Optimizer]`).
- **description**: Una oración. Describa lo que muestra el modelo y el resultado (por ejemplo, &quot;Acceso al perfil del cliente en tiempo real en el perímetro para la personalización web y móvil&quot;).

### Secciones del cuerpo

| Sección | Cuándo incluir | Guía de contenido |
|---------|-----------------|-------------------|
| **Aplicaciones** | Siempre para modelos de escenario | Lista con viñetas de los productos y las soluciones de Adobe implicados (por ejemplo, Real-time Customer Data Platform, Recopilación de datos). |
| **Casos de uso** | Siempre | Lista con viñetas de casos de uso empresariales/técnicos compatibles con este modelo. |
| **Requisitos previos** | Cuando se requiere la configuración | Productos, subdominios, SDK y configuración que deben estar configurados. Vínculo a Experience League para ver los pasos de configuración. |
| **Diagrama de arquitectura** | Siempre | Diagrama principal único (preferido por SVG). Usar estilo coherente: `style="width:90%; border:1px solid #4a4a4a" class="modal-image"`. Proporcionar texto `alt` significativo. |
| **Protecciones** | Siempre cuando el producto tiene protecciones | Vínculo a páginas oficiales de la protección de Experience League. Añada límites específicos del modelo (por ejemplo, TTL, límites de velocidad) como viñetas. |
| **Patrones de implementación** | Cuando existen varios enfoques | Asigne un nombre a cada patrón (por ejemplo, &quot;Patrón 1: basado en la pertenencia a audiencias con Web SDK&quot;). Utilice viñetas para indicar cuándo usar y las compensaciones. |
| **Pasos de implementación** | Para modelos de escenario con una ruta definida | Lista numerada. Cada paso: acción + vínculo a Experience League donde se encuentra el procedimiento. No copie los procedimientos completos. |
| **Consideraciones sobre la implementación** | Cuando hay advertencias importantes | Subsecciones (por ejemplo, Consideraciones de identidad o Personalización basada en atributos). Viñetas o párrafos cortos; vincular para obtener una mayor profundidad. |
| **Documentación relacionada** | Siempre | Vínculos agrupados a Experience League (y opcionalmente developer.adobe.com). Consulte Grupos de vínculos de Experience League a continuación. |

### Páginas de información general/hub

- Comience con 1-2 párrafos sobre el producto/área y lo que cubren los modelos.
- **Casos de uso**: Puede usar `>[!BEGINTABS]` / `>[!TAB ...]` / `>[!ENDTABS]` para varias categorías.
- **Arquitectura**: Un diagrama principal.
- **Escenarios de modelo** o **Patrones de integración**: Tabla con nombre de escenario, descripción breve y vínculo al modelo de escenario.
- **Requisitos previos**, **Protecciones**, **Documentación relacionada**: Igual que arriba; sea conciso.

&#x200B;---

## Adobe Experience League — Instrucciones del agente

### Cuándo hacer referencia a Experience League

- **Documentación del producto**: Cómo funciona un producto, flujos de interfaz de usuario y conceptos.
- **API**: puntos de conexión, parámetros, ejemplos (Experience Platform, Edge, etc.).
- **Protecciones**: páginas de protecciones oficiales del producto o servicio.
- **Tutoriales**: guías paso a paso (por ejemplo: crear esquemas, activar destinos).
- **Configuración**: flujos de datos, destinos, políticas de combinación, identidades, etc.

No pegue procedimientos largos de Experience League en el modelo. Resumir y vincular.

### Patrones de URL

| Tipo de contenido | URL básica | Ruta de ejemplo |
|--------------|----------|--------------|
| Documentos de Experience Platform | `https://experienceleague.adobe.com/docs/experience-platform/` | `.../profile/home.html`, `.../destinations/catalog/...` |
| Experience League (en) | `https://experienceleague.adobe.com/en/docs/` | La misma estructura que la anterior con `/en/`. |
| Journey Optimizer | `https://experienceleague.adobe.com/docs/journey-optimizer/` | `.../using/get-started/guardrails.html` |
| SDK web | `https://experienceleague.adobe.com/docs/experience-platform/web-sdk/` | `.../home.html`, `.../commands/command-responses.html` |
| API de servidor de Edge Network | `https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/` | `.../overview.html`, `.../guardrails.html` |
| SDK móvil | `https://developer.adobe.com/client-sdks/` | `.../home/`, `.../edge/adobe-journey-optimizer-decisioning/` |
| Etiquetas | `https://experienceleague.adobe.com/docs/experience-platform/tags/` | `.../home.html` |
| Tutoriales de Platform | `https://experienceleague.adobe.com/docs/platform-learn/tutorials/` | `.../profiles/create-merge-policies.html` |

Utilice la ruta canónica que coincida con el sitio actual de Experience League (prefiera `/en/docs/` cuando se conozca la ruta al inglés).

### Formato de vínculo en Markdown

- **Texto de vínculo descriptivo**: `[Create schemas](https://experienceleague.adobe.com/...)` no &quot;haga clic aquí&quot;.
- **Nombres de productos en texto**: use `[!DNL Product Name]` por cada estilo de Adobe (p. ej. `[!DNL Real-time Customer Profile]`).
- **Vínculos externos**: Agregue `{target="_blank"}` solo cuando la plantilla o canalización lo requiera (compruebe los modelos existentes en el repositorio).

### Documentación relacionada: grupos sugeridos

Utilice estos grupos cuando se apliquen:

1. **Configuraciones de destino** (para modelos de activación/personalización de Edge)
2. **Documentación de SDK** (Web SDK, SDK móvil, API de servidor de Edge Network, etiquetas)
3. **Perfil y segmentación** (perfil del cliente en tiempo real, políticas de combinación, segmentación)
4. **Tutoriales** (guías paso a paso de aprendizaje de la plataforma o específicas del producto)
5. **Documentación del producto** (subsecciones principal o clave del documento del producto)
6. **Protecciones** (si no está ya en la sección Protecciones)

Ejemplo:

```markdown
## Related documentation

### Destination configurations
* [Custom Personalization Connection](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization)
* [Activate audiences to edge personalization destinations](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)

### SDK documentation
* [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html)
* [Edge Network Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html)

### Profile and segmentation
* [Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html)
* [Profile Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
```

&#x200B;---

## Repositorio y índice

- **Ruta de acceso al contenido del modelo**: `help/blueprints/` (con subcarpetas por área, p. ej. `audience-activation/`, `customer-journeys/journey-optimizer/`).
- **Assets**: ubique junto con el modelo (por ejemplo, `assets/`, `images/`) o en una carpeta compartida (por ejemplo, `experience-platform/assets/`).
- **TDC**: edite `help/blueprints/TOC.md` al agregar, cambiar el nombre o mover páginas de modelo. Conservar el elemento frontCount (`user-guide-title`, `breadcrumb-title`, `user-guide-description`, `product`, `mini-toc-levels`, `role`) y la jerarquía `+`.

&#x200B;---

## Referencias de ejemplo en este repositorio

- **Modelo de escenario (formato largo)**: `help/blueprints/audience-activation/real-time-lookup.md`
- **Información general/concentrador con fichas y tablas**: `help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md`
- **Centrado en las protecciones**: `help/blueprints/experience-platform/guardrails.md`
- **Navegación**: `help/blueprints/TOC.md`, `help/blueprints/overview.md`

Utilícelos como patrones para el orden de secciones, la frontmatter, la ubicación del diagrama y el uso de vínculos de Experience League.
