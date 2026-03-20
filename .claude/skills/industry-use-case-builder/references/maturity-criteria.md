---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---
# Criterios de evaluación de madurez de casos de uso

## Niveles de madurez

### Fundacional

**Insignia:** `[!BADGE Foundational]{type=Neutral}`

Un caso de uso es **Foundation** cuando:

- Asigna a un patrón de un solo paso o activado por eventos (mensajería activada por eventos, activación de mensaje saliente por lotes)
- Tiene requisitos de datos sencillos (tipo de evento único, atributos de perfil estándar)
- Requiere capacidades mínimas o nulas de AI/ML.
- Utiliza la entrega de canal estándar (correo electrónico, SMS, push) sin una orquestación compleja
- Tiene patrones de implementación bien establecidos con prácticas recomendadas claras
- Requiere menos integraciones del sistema (normalmente entre 1 y 2 fuentes de datos)

**Patrones habituales:** mensajes activados por eventos, activación de mensajes salientes por lotes

**Ejemplos:** Recuperación del carro de compras abandonado, recordatorios de citas, notificaciones de servicio, alertas de caída de precios, recordatorios de pago de factura

### Emergente

**Insignia:** `[!BADGE Emerging]{type=Informative}`

Un caso de uso es **Emergente** cuando:

- Asigna a un patrón de personalización o de varios pasos (Recorrido orquestado de varios pasos, Personalization de visitante conocido, recomendación de comportamiento, Personalization de visitante anónimo).
- Requiere recopilación y análisis de datos de comportamiento
- Utiliza modelos de recomendación o resolución de perfiles de visitante conocida
- Implica secuencias de nutrición multitáctil con lógica de ramificación
- Tiene una complejidad de integración moderada (2 a 4 fuentes de datos)
- Puede requerir activación de audiencia o segmentación basada en segmentos

**Patrones habituales:** Recorrido orquestado en varios pasos, Personalization de aplicaciones/web de visitantes conocidos, recomendación de comportamiento, Personalization web de visitante anónimo, Audience Activation B2B

**Ejemplos:** Serie de bienvenida, campañas de cumplimiento de medicamentos, paneles de cuentas personalizados, puntuación de posibles clientes, recomendaciones de contenido

### Avanzadas

**Insignia:** `[!BADGE Advanced]{type=Caution}`

Un caso de uso es **Avanzado** cuando:

- Se asigna a un patrón de toma de decisiones o de orquestación entre canales (Recorrido entre canales con toma de decisiones, Offer Decisioning)
- Requiere predicción basada en IA o puntuación de tendencia
- Utiliza la lógica de decisión centralizada en varios canales simultáneamente
- Implica una orquestación compleja con toma de decisiones en tiempo real en varios puntos de recorrido
- Tiene una alta complejidad de integración (más de 4 fuentes de datos, fuentes de datos en tiempo real)
- Requiere reglas comerciales sofisticadas, administración de prioridades y administración de frecuencias

**Patrones habituales:** Recorrido en canales múltiples con Decisioning, Offer Decisioning

**Ejemplos:** Prevención de pérdida con puntuación de IA, recomendaciones de productos en fase de vida, optimización de ventas cruzadas, personalización de programas de fidelidad, ofertas exclusivas de VIP

## Flujo de trabajo de evaluación

1. Identificar a qué patrón de caso de uso se asigna el caso de uso
2. Consulte la lista &quot;Patrones típicos&quot; para obtener una coincidencia rápida
3. Si el patrón no indica claramente la madurez, evalúe la complejidad de los datos, los requisitos de IA/ML y el alcance de la integración
4. Presente la evaluación al usuario con un razonamiento: &quot;Basándome en la asignación de patrones ({pattern}) y {key factors}, clasificaría esto como {level} debido a {reasoning}&quot;.
5. Permitir al usuario confirmar o anular la suscripción antes de continuar
