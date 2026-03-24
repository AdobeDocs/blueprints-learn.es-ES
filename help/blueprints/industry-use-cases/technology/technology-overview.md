---
title: Casos de uso de tecnología
description: Descubra cómo las organizaciones tecnológicas utilizan Adobe Experience Platform para unificar la recopilación de datos, reenviar eventos en tiempo real y activar el análisis y la activación en todos los productos digitales.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: a1b2c3d4-e5f6-7890-abcd-ef1234567890
source-git-commit: 77908fd8a9f4309cbe66063cd33f065424697e55
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Casos de uso de tecnología

Las organizaciones tecnológicas utilizan Adobe Experience Platform para centralizar la recopilación de datos de superficies web, móviles y de productos, y distribuir eventos en tiempo real a los destinos de análisis, Data Warehouse y activación que alimentan sus productos y programas de marketing. Al consolidar la recopilación de eventos en el perímetro de, los equipos tecnológicos reducen la complejidad del lado del cliente, mejoran la calidad de los datos y garantizan que todos los sistemas descendentes reciban datos de comportamiento coherentes de una sola fuente autorizada.

## Reenvío de eventos en tiempo real

Reenvíe eventos de comportamiento en tiempo real recopilados mediante Edge Network a análisis de terceros, almacenes de datos y plataformas de socios para su enriquecimiento y activación. La centralización de la recopilación de eventos en el perímetro y el reenvío a varios destinos reduce la sobrecarga de etiquetas del lado del cliente, mejora la calidad de los datos y garantiza que todos los sistemas descendentes reciban datos de evento coherentes desde una única fuente autorizada.

### Impacto empresarial

Las organizaciones tecnológicas que implementan el reenvío de eventos en tiempo real reducen la carga de etiquetas del lado del cliente y la sobrecarga de rendimiento asociada, a la vez que mejoran la coherencia de los datos de evento en los destinos de Analytics, Data Warehouse y activación. El reenvío del lado del servidor también reduce el peso de página y mejora el rendimiento de carga, lo que beneficia directamente a las métricas de experiencia del usuario.

### Cómo implementar

Utilice el patrón [Reenvío de eventos](/help/blueprints/use-case-patterns/audience-building-activation/event-forwarding.md) para enrutar los eventos recopilados por Adobe Experience Platform Web SDK a través de Edge Network a destinos configurados del lado del servidor. Este es el patrón correcto cuando el objetivo es la distribución de eventos de servidor a servidor desde un único punto de recopilación, en lugar de administrar etiquetas independientes para cada destino en el lado del cliente, lo que añade peso de página y crea incoherencia de datos en todos los sistemas.

### Consideraciones técnicas

- El reenvío de eventos de Edge Network requiere la migración de la colección de eventos a Adobe Experience Platform Web SDK o Mobile SDK; la compatibilidad de las implementaciones existentes basadas en etiquetas debe evaluarse antes de configurar los destinos de reenvío.
- Las reglas de reenvío deben configurarse para enviar solo los campos requeridos por cada destino; evite reenviar cargas XDM completas a destinos que solo necesiten un pequeño subconjunto de campos, ya que esto aumenta los costes de transferencia de datos y crea una exposición de conformidad.
- Los conectores de destino deben gestionar los errores correctamente; las canalizaciones de reenvío de eventos deben implementar la lógica de reintentos y las alertas para los destinos que no están disponibles para evitar la pérdida de datos durante las interrupciones.
- Las políticas de gobernanza de datos deben revisarse para cada destino de reenvío para garantizar que las preferencias de consentimiento del usuario capturadas en el perímetro se cumplan en la configuración de reenvío.
