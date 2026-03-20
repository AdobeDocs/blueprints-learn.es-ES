---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 3%

---
# Caso de uso Icono Guía de estilo

## Información general

Los iconos de casos de uso sirven como identificadores visuales en la tabla del catálogo de casos de uso. Deben ser reconocibles inmediatamente a una anchura de pantalla de 40 píxeles, manteniendo la calidad a su resolución nativa de 1024 x 1024.

## Especificaciones técnicas

| Propiedad | Valor |
| --- | --- |
| Dimensiones | 1024 x 1024 píxeles |
| Formato | PNG (RGB de 8 bits o RGBA) |
| Tamaño de archivo | 900 KB - 1,4 MB típica |
| Tamaño de visualización | 40 px de anchura en las tablas del catálogo |
| Nombre | `icon-{kebab-case-name}.png` |
| Ruta de almacenamiento | `/help/blueprints/industry-use-cases/assets/use-case-icons/{industry}/` |

## Directrices de estilo visual

### Composición
- **Asunto central único**: cada icono debe incluir una metáfora visual clara que represente el concepto de caso de uso
- **Composición centrada**: el asunto principal debe estar centrado con un espacio en blanco equilibrado
- **Sin texto**: el texto no se puede leer a 40 píxeles; confíe totalmente en la metáfora visual
- **Sin escenas complejas**: evite las composiciones de elementos múltiples, los fondos con muchos objetos o las escenas narrativas
- **Siluetas en negrita**: la forma del icono debe ser reconocible incluso como una silueta pequeña

### Color y tono
- **Paleta moderna y limpia**: use colores profesionales apropiados para la empresa
- **Cohesión del sector**: los iconos dentro del mismo sector deberían parecer como si pertenecieran juntos
- **Alto contraste**: asegúrese de que el asunto principal se destaca claramente del fondo
- **Evite los colores de neón o saturados en exceso** — Mantenga la paleta refinada y profesional

### Estilo
- **Moderno y profesional** — Líneas limpias, acabado pulido
- **Procesamiento coherente**: todos los iconos deben parecer provenir del mismo sistema de diseño
- **3D o plano es aceptable**, pero sea coherente dentro de un sector vertical
- **Evitar el fotorrealismo**: se prefiere el estilo ilustrado o procesado por coherencia
- **No hay logotipos de marca ni imágenes de marca comercial**: utilice metáforas visuales genéricas

### Prueba de legibilidad de tamaño pequeño
Antes de finalizar, escale mentalmente la imagen a 40 px:
- ¿Puede identificar el asunto principal?
- ¿Hay suficiente contraste entre el primer plano y el fondo?
- ¿Hay algún detalle fino que se convertiría en ruido visual?
- ¿La forma se lee claramente sin color (en caso de accesibilidad)?

## Ejemplos de metáforas visuales por sector

### Sector minorista
| Ejemplo de uso | Metáfora visual |
| --- | --- |
| Carro abandonado | Carro de compras con artículos |
| Recomendaciones de productos | Caja de regalo o productos seleccionados |
| Ampliación de venta cruzada | Artículos de compra conectados |
| Serie de bienvenida | Tarjeta de bienvenida o regalo |
| Bajada de precios | Etiqueta de precio con flecha hacia abajo |

### Automoción
| Ejemplo de uso | Metáfora visual |
| --- | --- |
| Recordatorios de servicio | Llave inglesa o calendario de servicio |
| Compra de vehículo | Coche con llaves |
| Intercambio | Flechas de cambio de coche |
| Coche conectado | Coche con conexión digital |

### Asistencia sanitaria
| Ejemplo de uso | Metáfora visual |
| --- | --- |
| Recordatorio de cita | Calendario con estetoscopio |
| Adherencia al medicamento | Frasco de píldoras o receta |
| Atención Preventiva | Blindaje con símbolo de salud |

### Servicios financieros
| Ejemplo de uso | Metáfora visual |
| --- | --- |
| Cultivo de plomo | Gráfico de crecimiento para plántulas |
| Prevención de pérdida | Escudo o símbolo de retención |
| Fase de vida | Cronología de hitos de vida |

### B2B
| Ejemplo de uso | Metáfora visual |
| --- | --- |
| ABM | Destinatario con creación |
| Puntuación de posibles clientes | Calibrador o termómetro |
| Renovación del contrato | Documento con símbolo de actualización |

### Viajes y hospitalidad
| Ejemplo de uso | Metáfora visual |
| --- | --- |
| Abandono del carro | Maleta o reserva |
| Programa de fidelización | Tarjeta de fidelización o distintivo de estrella |
| Recordatorios de reserva | Calendario con avión/hotel |

### Seguro
| Ejemplo de uso | Metáfora visual |
| --- | --- |
| Renovación de directivas | Documento con flechas de renovación |
| Proceso de reclamaciones | Portapapeles con marca de verificación |
| Venta cruzada | Documentos de directivas conectados |

### Medios de comunicación y entretenimiento
| Ejemplo de uso | Metáfora visual |
| --- | --- |
| Nuevo contenido | Botón Reproducir o proyector |
| Recomendaciones de contenido | Lista de reproducción seleccionada o contenido con estrellas |
| Pérdida de suscripción | Tarjeta de suscripción rota |

### Telecomunicaciones
| Ejemplo de uso | Metáfora visual |
| --- | --- |
| Optimización del plan | Barras de señal con engranaje |
| Actualización de dispositivo | Teléfono con flecha hacia arriba |
| Prevención de pérdida | Blindaje con señal |

## Plantilla del mensaje de generación de imágenes

Utilice esta plantilla como punto de partida, personalizando el asunto y los detalles para cada caso de uso:

```
A clean, modern icon illustration of {visual metaphor} representing {use case concept}. Professional corporate design style with bold shapes and clean lines. Single centered subject on a {solid/gradient} background. High contrast, vibrant but refined color palette. No text, no fine details, no complex backgrounds. The icon must be clearly recognizable when scaled down to 40 pixels. Square format, 1024x1024 pixels.
```

### Sugerencias de personalización

- **Sea específico sobre el tema**: &quot;Un carro de compras rojo brillante con dos cajas de regalo coloridas dentro&quot; es mejor que &quot;un carro de compras&quot;
- **Especificar el tratamiento de fondo**: &quot;sobre un fondo degradado azul suave&quot; o &quot;sobre un fondo blanco limpio con una sombra sutil&quot;
- **Mención de iluminación**: &quot;iluminación suave de estudio&quot; o &quot;brillo suave en el ambiente&quot; ayuda a lograr la consistencia
- **Agregar modificadores de estilo**: &quot;minimalista&quot;, &quot;geométrico&quot;, &quot;isométrico&quot; o &quot;diseño plano&quot; para dirigir la estética
- **Incluir mensajes negativos si se admite**: &quot;sin texto, sin marcas de agua, sin bordes, sin elementos fotorrealistas&quot;

## Inventario de iconos existentes

### Por sector

**Venta minorista (9 iconos):**
icono-abandonado-carro, icono-inventario-urgencia, icono-precio-caída, icono-producto-recomendaciones, icono-categoría-páginas, icono-bienvenida-serie, icono-reabastecimiento, icono-post-compra, icono-venta cruzada-upsell

**Automoción (12 iconos):**
icon-service-reminder, icon-reminder-notifications, icon-test-drive, icon-model-launch, icon-trade-in, icon-parts-accessorios, icon-garantía, icon-connected-car, icon-dealer-network, icon-vehículo-purchase, icon-finance, icon-owner-loyalty

**Servicios financieros (6 iconos):**
icon-lead-nurturing, icon-account-dashboard, icon-product-recommendation, icon-churn-prevention, icon-life-stage

**Atención médica (4 iconos):**
icon-cita-recordatorio, icon-post-visita, icon-preventivo-cuidado, icon-medicación-adherencia

**Seguro (3 iconos):**
icon-policy-refresh, icon-claim-process, icon-cross-sell

**Medios y entretenimiento (3 iconos):**
icon-new-content, icon-content-recommendations, icon-subscription-churn

**Telecomunicaciones (3 iconos):**
icon-plan-optimization, icon-device-upgrade, icon-churn-prevention

**Viajes y hospitalidad (12 iconos):**
icon-cart-abandment, icon-booking-reminder, icon-season-campaigns, icon-personalized-homepage, icon-high-intent, icon-post-booking-upsell, icon-win-back, icon-dynamic-itinerary, icon-newly-browsed, icon-group-booking, icon-exit-intent, icon-loyalty-program

**B2B (11 iconos):**
icon-webinar-demo, icon-abm, icon-lead-scoring, icon-content-personalization, icon-event-registration, icon-trial-conversion, icon-customer-onboarding, icon-competition-replace, icon-case-study, icon-Contract-validation, icon-upsell-expand
