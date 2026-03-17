---
title: Catálogo de casos de uso
description: Examine los casos de uso del sector por vertical, nivel de madurez o patrón de implementación para encontrar el punto de partida adecuado para su recorrido de Adobe Experience Platform.
doc-type: overview-page
exl-id: 7a3c2f1e-9b4d-4e6a-8f5c-2d1b3a4e7c9f
source-git-commit: 8ad59ff130dae13553f10049eb685cf557a73ead
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 6%

---

# Catálogo de casos de uso

Explore casos de uso del sector para [!DNL Adobe Experience Platform] y aplicaciones. Examine por sector para ver casos de uso para su vertical, por nivel de madurez para encontrar el punto de partida adecuado para su organización o por patrón de implementación para comprender qué enfoque técnico se adapta a sus necesidades.

Cada caso de uso se vincula a una guía de implementación detallada a través de un patrón de caso de uso, que describe la cadena de funciones, los puntos de decisión y los pasos de configuración necesarios para dar vida al caso de uso.

## Examinar por sector

>[!BEGINTABS]

>[!TAB Comercial]

Las organizaciones comerciales usan [!DNL Adobe Experience Platform] para unificar los datos de clientes de tiendas en línea, ubicaciones físicas y programas de fidelidad en una sola vista de cada comprador.

| | Ejemplo de uso | Descripción | Vencimiento | Patrón |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="Recomendaciones de productos personalizadas" width="40"> | [Recomendaciones de productos personalizadas](retail/retail-overview.md#personalized-product-recommendations) | Mostrar productos personalizados basados en el historial de navegación y compras | [!BADGE Emergente]{type=Informative} | [Recomendación de comportamiento](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="Carro abandonado" width="40"> | [Recuperación de correo electrónico del carro de compras abandonado](retail/retail-overview.md#abandoned-cart-email-recovery) | Envío de recordatorios personalizados para carros de compras abandonados | [!BADGE Fundacional]{type=Neutral} | [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="Urgencia de inventario" width="40"> | [Campañas de urgencia basadas en inventario](retail/retail-overview.md#inventory-based-urgency-campaigns) | Déclencheur alertas en tiempo real cuando el inventario de productos es bajo | [!BADGE Fundacional]{type=Neutral} | [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="Ampliación de venta cruzada" width="40"> | [Recomendaciones de venta cruzada y aumento de ventas](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | Mostrar los productos relevantes de venta cruzada y de ampliación de ventas al finalizar la compra y en el correo electrónico | [!BADGE Avanzado]{type=Caution} | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="Serie de bienvenida" width="40"> | [Nueva serie de bienvenida al cliente](retail/retail-overview.md#new-customer-welcome-series) | Automatice una serie de bienvenida de varios correos electrónicos con recomendaciones personalizadas | [!BADGE Emergente]{type=Informative} | [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="Bajada de precios" width="40"> | [Alertas de bajada de precios](retail/retail-overview.md#price-drop-alerts) | Notificar a los clientes cuando la lista de deseos o los artículos vistos bajen de precio | [!BADGE Fundacional]{type=Neutral} | [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="Reposición" width="40"> | [Recordatorios de reabastecimiento](retail/retail-overview.md#replenishment-reminders) | Envíe recordatorios automatizados para los productos consumibles comprados con regularidad | [!BADGE Emergente]{type=Informative} | [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="Páginas de categoría" width="40"> | [Páginas de categoría personalizadas](retail/retail-overview.md#personalized-category-pages) | Reordenar dinámicamente las páginas de categorías en función de las preferencias de cada cliente | [!BADGE Emergente]{type=Informative} | [Recomendación de comportamiento](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="Posterior a la compra" width="40"> | [Campañas de seguimiento posteriores a la compra](retail/retail-overview.md#post-purchase-follow-up-campaigns) | Envíe consejos de atención, solicitudes de revisión y sugerencias de productos relacionados | [!BADGE Emergente]{type=Informative} | [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| | [Ofertas exclusivas para clientes de VIP](retail/retail-overview.md#vip-customer-exclusive-offers) | Proporcionar ofertas exclusivas y acceso anticipado a clientes de alto valor | [!BADGE Avanzado]{type=Caution} | [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |
| | [Notificaciones sin existencias](retail/retail-overview.md#out-of-stock-notifications) | Notificar a los clientes cuando haya productos sin existencias disponibles | [!BADGE Fundacional]{type=Neutral} | [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| | [Personalization de Social Proof](retail/retail-overview.md#social-proof-personalization) | Mostrar valoraciones y comentarios personalizados según el perfil del cliente | [!BADGE Emergente]{type=Informative} | [Personalization de aplicación/web de visitante conocido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

>[!TAB Servicios financieros]

Los casos de uso de los servicios financieros llegarán pronto. [Ver casos de uso actuales de Financial Services &#x200B;](financial-services/financial-services-overview.md).

>[!TAB Atención médica]

Los casos de uso de atención médica llegarán pronto. [Ver casos de uso actuales de atención médica](healthcare/healthcare-overview.md).

>[!TAB Automoción]

Los casos de uso de automoción llegarán pronto. [Ver casos de uso actuales de Automoción](automotive/automotive-overview.md).

>[!TAB Viajes y hospitalidad]

Los casos de uso de Viajes y hospitalidad llegarán pronto. [Ver los casos de uso actuales de Viajes y hospitalidad](travel-hospitality/travel-hospitality-overview.md).

>[!TAB Telecomunicaciones]

Los casos de uso de telecomunicaciones llegarán pronto. [Ver casos de uso de telecomunicaciones actuales &#x200B;](telecommunications/telecommunications-overview.md).

>[!TAB Medios de comunicación y entretenimiento]

Los casos de uso de medios y entretenimiento llegarán pronto. [Ver casos de uso actuales de medios y entretenimiento](media-entertainment/media-entertainment-overview.md).

>[!TAB Seguro]

Los casos de uso del seguro llegarán pronto. [Ver casos de uso actuales del seguro](insurance/insurance-overview.md).

>[!TAB B2B]

Los casos de uso de B2B llegarán pronto. [Ver casos de uso B2B actuales &#x200B;](b2b/b2b-overview.md).

>[!ENDTABS]

## Examinar por nivel de madurez

>[!BEGINTABS]

>[!TAB Fundacional]

Patrones básicos y comprobados que utilizan entrega de un solo canal. Puntos de partida ideales para organizaciones que comienzan su recorrido de [!DNL Experience Platform].

| | Ejemplo de uso | Industria | Impacto empresarial | Patrón |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="Carro abandonado" width="40"> | [Recuperación de correo electrónico del carro de compras abandonado](retail/retail-overview.md#abandoned-cart-email-recovery) | Sector minorista | 25-35% tasa de recuperación del carro de compras | [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="Urgencia de inventario" width="40"> | [Campañas de urgencia basadas en inventario](retail/retail-overview.md#inventory-based-urgency-campaigns) | Sector minorista | Aumento de la conversión de entre 30 y 40 % | [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="Bajada de precios" width="40"> | [Alertas de bajada de precios](retail/retail-overview.md#price-drop-alerts) | Sector minorista | Tasa de conversión de 20-30 % | [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| | [Notificaciones sin existencias](retail/retail-overview.md#out-of-stock-notifications) | Sector minorista | Tasa de conversión del 40 al 50 % | [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |

>[!TAB Emergente]

Patrones de varios canales y pasos que se basan en las capacidades básicas con personalización impulsada por IA y recorridos organizados.

| | Ejemplo de uso | Industria | Impacto empresarial | Patrón |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="Recomendaciones de productos" width="40"> | [Recomendaciones de productos personalizadas](retail/retail-overview.md#personalized-product-recommendations) | Sector minorista | Aumento de 20-30 % en CTR, aumento de conversión de 15-25 % | [Recomendación de comportamiento](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="Páginas de categoría" width="40"> | [Páginas de categoría personalizadas](retail/retail-overview.md#personalized-category-pages) | Sector minorista | Aumento del 25 al 35 % en la participación | [Recomendación de comportamiento](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="Serie de bienvenida" width="40"> | [Nueva serie de bienvenida al cliente](retail/retail-overview.md#new-customer-welcome-series) | Sector minorista | Tasa de participación del 40 al 50 % | [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="Reposición" width="40"> | [Recordatorios de reabastecimiento](retail/retail-overview.md#replenishment-reminders) | Sector minorista | Tasa de repetición de compras del 30-40% | [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="Posterior a la compra" width="40"> | [Campañas de seguimiento posteriores a la compra](retail/retail-overview.md#post-purchase-follow-up-campaigns) | Sector minorista | Del 15 al 20% de tasa de revisión, del 10 al 15% de compras repetidas | [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| | [Personalization de Social Proof](retail/retail-overview.md#social-proof-personalization) | Sector minorista | Aumento de tasa de conversión del 10 al 15 % | [Personalization de aplicación/web de visitante conocido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

>[!TAB Avanzado]

Orquestación en canales múltiples con toma de decisiones en tiempo real y selección de ofertas impulsadas por IA para las experiencias de cliente más sofisticadas.

| | Ejemplo de uso | Industria | Impacto empresarial | Patrón |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="Ampliación de venta cruzada" width="40"> | [Recomendaciones de venta cruzada y aumento de ventas](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | Sector minorista | Aumento de 25 a 75 dólares en AOV, aumento de ingresos de entre el 10 y el 15 % | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| | [Ofertas exclusivas para clientes de VIP](retail/retail-overview.md#vip-customer-exclusive-offers) | Sector minorista | 50-70% tasa de participación de VIPs | [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |

>[!ENDTABS]

## Examinar por patrón de implementación

>[!BEGINTABS]

>[!TAB Administración y orquestación de campañas]

### Mensajería activada por eventos

Responda a eventos de comportamiento en tiempo real con mensajes oportunos de un solo canal.

| | Ejemplo de uso | Industria | Vencimiento | Impacto empresarial |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="Carro abandonado" width="40"> | [Recuperación de correo electrónico del carro de compras abandonado](retail/retail-overview.md#abandoned-cart-email-recovery) | Sector minorista | [!BADGE Fundacional]{type=Neutral} | 25-35% tasa de recuperación del carro de compras |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="Urgencia de inventario" width="40"> | [Campañas de urgencia basadas en inventario](retail/retail-overview.md#inventory-based-urgency-campaigns) | Sector minorista | [!BADGE Fundacional]{type=Neutral} | Aumento de la conversión de entre 30 y 40 % |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="Bajada de precios" width="40"> | [Alertas de bajada de precios](retail/retail-overview.md#price-drop-alerts) | Sector minorista | [!BADGE Fundacional]{type=Neutral} | Tasa de conversión de 20-30 % |
| | [Notificaciones sin existencias](retail/retail-overview.md#out-of-stock-notifications) | Sector minorista | [!BADGE Fundacional]{type=Neutral} | Tasa de conversión del 40 al 50 % |

### Recorrido orquestado de varios pasos

Guíe a los clientes a través de secuencias multitáctiles que se adapten en función de la participación y el comportamiento.

| | Ejemplo de uso | Industria | Vencimiento | Impacto empresarial |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="Serie de bienvenida" width="40"> | [Nueva serie de bienvenida al cliente](retail/retail-overview.md#new-customer-welcome-series) | Sector minorista | [!BADGE Emergente]{type=Informative} | Tasa de participación del 40 al 50 % |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="Reposición" width="40"> | [Recordatorios de reabastecimiento](retail/retail-overview.md#replenishment-reminders) | Sector minorista | [!BADGE Emergente]{type=Informative} | Tasa de repetición de compras del 30-40% |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="Posterior a la compra" width="40"> | [Campañas de seguimiento posteriores a la compra](retail/retail-overview.md#post-purchase-follow-up-campaigns) | Sector minorista | [!BADGE Emergente]{type=Informative} | Del 15 al 20% de tasa de revisión, del 10 al 15% de compras repetidas |

### Recorrido en canales múltiples con toma de decisiones

Orqueste experiencias en canales múltiples con Offer Decisioning en tiempo real en cada punto de contacto.

| | Ejemplo de uso | Industria | Vencimiento | Impacto empresarial |
| --- | --- | --- | --- | --- |
| | [Ofertas exclusivas para clientes de VIP](retail/retail-overview.md#vip-customer-exclusive-offers) | Sector minorista | [!BADGE Avanzado]{type=Caution} | 50-70% tasa de participación de VIPs |

>[!TAB Personalization]

### Recomendación de comportamiento

Utilice modelos impulsados por IA para mostrar contenido y productos personalizados basados en señales de comportamiento.

| | Ejemplo de uso | Industria | Vencimiento | Impacto empresarial |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="Recomendaciones de productos" width="40"> | [Recomendaciones de productos personalizadas](retail/retail-overview.md#personalized-product-recommendations) | Sector minorista | [!BADGE Emergente]{type=Informative} | Aumento de 20-30 % en CTR, aumento de conversión de 15-25 % |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="Páginas de categoría" width="40"> | [Páginas de categoría personalizadas](retail/retail-overview.md#personalized-category-pages) | Sector minorista | [!BADGE Emergente]{type=Informative} | Aumento del 25 al 35 % en la participación |

### Offer Decisioning

Utilice una lógica de decisión centralizada para evaluar y seleccionar la mejor oferta para cada cliente y contexto.

| | Ejemplo de uso | Industria | Vencimiento | Impacto empresarial |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="Ampliación de venta cruzada" width="40"> | [Recomendaciones de venta cruzada y aumento de ventas](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | Sector minorista | [!BADGE Avanzado]{type=Caution} | Aumento de 25 a 75 dólares en AOV, aumento de ingresos de entre el 10 y el 15 % |

### Personalization de aplicación/web de visitante conocido

Personalice el contenido web y de la aplicación para los visitantes identificados en función del perfil, las preferencias y el contexto de navegación.

| | Ejemplo de uso | Industria | Vencimiento | Impacto empresarial |
| --- | --- | --- | --- | --- |
| | [Personalization de Social Proof](retail/retail-overview.md#social-proof-personalization) | Sector minorista | [!BADGE Emergente]{type=Informative} | Aumento de tasa de conversión del 10 al 15 % |

>[!ENDTABS]
