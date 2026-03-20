---
name: use-case-icon-generator
description: Genere especificaciones de iconos y peticiones de datos para la generación de imágenes para los iconos de casos de uso en el repositorio de modelos de Adobe Experience Platform. Utilice esta aptitud cuando cree iconos para nuevos casos de uso del sector, cuando la aptitud de generador de casos de uso del sector necesite un icono o cuando el usuario pregunte sobre la creación o actualización de iconos de casos de uso. Genera una solicitud de generación de imágenes detallada que el usuario puede utilizar con Midjourney, DALL-E, Adobe Firefly o herramientas similares, junto con el nombre y la ubicación correctos del archivo.
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Generador de iconos de casos de uso

Genere especificaciones detalladas de los iconos y peticiones de datos de generación de imágenes de IA para iconos de casos de uso en el repositorio de modelos.

## Cuándo usar esta aptitud

- Creación de un nuevo caso de uso que necesite un icono
- La aptitud del generador de casos de uso del sector la llama para generar una especificación de icono.
- El usuario pregunta sobre la creación, actualización o sustitución de un icono de caso de uso
- El usuario desea generar un lote de iconos para un nuevo sector vertical

## Paso 1: Recopilar entradas

Recopile la siguiente información del usuario o de la aptitud para llamar:

**Requerido:**
- **Nombre del caso de uso**: el nombre legible en lenguaje natural del caso de uso (por ejemplo, &quot;Carro abandonado&quot;, &quot;Puntuación de posibles clientes&quot;).
- **Sector vertical**: Uno de los siguientes: automoción, b2b, servicios financieros, atención médica, seguros, entretenimiento multimedia, comercio minorista, telecomunicaciones, viajes y hospitalidad
- **Descripción breve** — de 1 a 2 oraciones que describen lo que hace el caso de uso

**Opcional:**
- **Metáfora visual o asunto preferido**: Si el usuario tiene una idea específica de lo que el icono debería representar

Si falta alguna entrada necesaria, pregunte al usuario antes de continuar.

## Paso 2: Leer la guía de estilo

Lea el archivo `references/icon-style-guide.md` (relativo al directorio de esta aptitud) para cargar la guía de estilo completa, incluido lo siguiente:

- Especificaciones técnicas
- Directrices de estilo visual
- Ejemplos de metáforas visuales por sector
- La plantilla de solicitud
- El inventario de iconos existente

Utilice la guía de estilo para garantizar la coherencia con los iconos existentes.

## Paso 3: Generación de la especificación del icono

Produzca las tres partes de la especificación del icono:

### A. Especificación del archivo

Derive el nombre de archivo y la ruta del nombre del caso de uso y la industria:

- **Nombre de archivo:** `icon-{kebab-case-name}.png`
   - Convierta el nombre del caso de uso a minúscula (kebab) (guiones en minúsculas para espacios)
   - Ejemplos: &quot;Carro abandonado&quot; se convierte en `icon-abandoned-cart.png`, &quot;Ampliación de venta cruzada&quot; se convierte en `icon-cross-sell-upsell.png`
- **Ruta de acceso:** `/help/blueprints/industry-use-cases/assets/use-case-icons/{industry}/`
- **Dimensiones:** 1024 x 1024 píxeles
- **Formato:** PNG, RGB de 8 bits o RGBA
- **Tamaño de archivo de destino:** 900 KB - 1,4 MB

### B. Mensaje de generación de imagen

Cree un mensaje detallado y listo para copiar para las herramientas de generación de imágenes de IA. El mensaje debe:

1. **Describir una metáfora visual clara**: elija una sola metáfora visual sólida que comunique inmediatamente el concepto de caso de uso. Si el usuario proporcionó una metáfora preferida, utilícela. De lo contrario, seleccione uno en función de los ejemplos de la guía de estilo y la descripción del caso de uso.

2. **Especificar el estilo artístico** — Incluir estas directivas de estilo:
   - Estilo de ilustración de icono limpio y moderno
   - Estética profesional del diseño corporativo
   - Formas en negrita y líneas limpias
   - Acabado pulido y procesado (no fotorrealista)
   - Compatible con un sistema de diseño unificado

3. **Incluir especificaciones técnicas:**
   - Formato cuadrado, 1024 x 1024 píxeles
   - Asunto centrado único
   - Fondo de degradado sólido o sutil
   - Alto contraste entre el asunto y el fondo

4. **Aplicar legibilidad de tamaño pequeño:**
   - Sin texto ni letras de ningún tipo
   - No hay detalles finos o patrones intrincados
   - Sin fondos complejos ni escenas de varios elementos
   - Silueta atrevida que se lee claramente a 40 px
   - Fuerte reconocimiento de formas incluso sin color

5. **Guía de la paleta de colores:**
   - Colores profesionales apropiados para la empresa
   - Vibrante pero refinado (no neón o saturado en exceso)
   - Alto contraste para accesibilidad
   - Cohesivo con otros iconos del mismo sector

Estructurar el mensaje como un solo párrafo, listo para pegar en cualquier herramienta de generación de imágenes.

### C. Fragmento de referencia de catálogo

Genere el fragmento de HTML para utilizarlo en la tabla de catálogo:

```
<img src="assets/use-case-icons/{industry}/icon-{name}.png" alt="{Alt Text}" width="40">
```

Donde `{Alt Text}` es el nombre de caso de uso legible en lenguaje natural.

## Paso 4: Enumerar los iconos existentes en el mismo sector

Consulte la sección de inventario de iconos existentes de la guía de estilo y enumere todos los iconos actuales del mismo sector. Esto ayuda al usuario a:
- Garantizar la coherencia visual al generar el nuevo icono
- Evite duplicar un icono que ya existe
- Hacer referencia a iconos existentes como ejemplos de estilo

## Paso 5: Presentar el resultado

Dé un formato claro a la salida con estas secciones:

&#x200B;---

### Especificación del icono: &lbrace;Use Case Name&rbrace;

**Sector:** {Industry}

**Detalles de archivo:**
- Nombre de archivo: `icon-{kebab-case-name}.png`
- Ruta: `/help/blueprints/industry-use-cases/assets/use-case-icons/{industry}/`
- Dimensiones: 1024 x 1024 píxeles
- Formato: PNG (RGB/RGBA de 8 bits)

**Mensaje de solicitud de generación de imagen:**

> {El mensaje completo y detallado, con formato de cotización de bloque para que sea fácil de copiar}

**HTML de catálogo:**

```html
<img src="assets/use-case-icons/{industry}/icon-{name}.png" alt="{Use Case Name}" width="40">
```

**Iconos existentes en {Industry}:**
- {list of existing icon names}

**Pasos siguientes:**
1. Copie el mensaje de generación de imágenes anterior.
2. Péguelo en la herramienta de generación de imágenes que prefiera (Adobe Firefly, Midjourney, DALL-E o similar).
3. Genere la imagen y seleccione el mejor resultado.
4. Cambie el tamaño o exporte exactamente a 1024 x 1024 píxeles si es necesario.
5. Guardar como `{filename}` en la ruta de acceso mostrada anteriormente.
6. Compruebe que el icono tenga un aspecto claro y reconocible con un tamaño de visualización de 40 píxeles.
7. Utilice el fragmento de HTML del catálogo al añadir este caso de uso a la tabla del catálogo.

&#x200B;---

## Pautas

- **No generar nunca la imagen real**: esta aptitud produce únicamente la especificación y el mensaje. El usuario debe utilizar una herramienta de generación de imágenes externa.
- **Un icono por caso de uso**: cada caso de uso obtiene exactamente un icono.
- **Buscar duplicados**: si ya existe un icono con el mismo nombre o muy similar en el inventario, avise al usuario.
- **Dar prioridad a la legibilidad**: cuando haya dudas entre una metáfora detallada y una simple, elija siempre la opción más simple que se lea bien a 40 píxeles.
- **Sea específico en las indicaciones**: las indicaciones vagas producen resultados incoherentes. Incluya detalles visuales concretos (por ejemplo, &quot;un carro de compras con dos cajas de colores dentro&quot; en lugar de &quot;un concepto de compra&quot;).
- **Evite clichés siempre que sea posible** — Intente encontrar metáforas visuales nuevas pero reconocibles de inmediato. Una bombilla para cada caso de uso &quot;inteligente&quot; se vuelve repetitiva.
