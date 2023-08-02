---
title: 'Sector minorista: activación con aplicaciones de Experience Cloud'
description: Ofrezca experiencias del cliente en tiempo real en medios digitales, correo electrónico, mensajes push y canales web.
solution: Real-Time Customer Data Platform, Customer Journey Analytics, Journey Orchestration, Campaign, Analytics, Target
kt: 9474
exl-id: a675bc81-e76c-491a-8718-359867d63351
source-git-commit: ae7347be5095ca4a7f99f9371dd94d87097112b0
workflow-type: ht
source-wordcount: '630'
ht-degree: 100%

---

# Desafío empresarial del sector minorista

Esta empresa de experiencia integrada tenía como objetivo personalizar todo el recorrido del cliente para aumentar la lealtad, impulsar las ventas en relación con los clientes existentes y mejorar el gasto en marketing en todas sus campañas. La estrategia para lograr el objetivo era ampliar su capacidad digital para incluir datos de transacciones y datos de clientes sin conexión a fin de impulsar el crecimiento.

## Enfoque de Adobe

* Generar un perfil de cliente unificado que incluya todos los datos relevantes en línea y sin conexión que se puedan activar en tiempo real.
* Orquestar las interacciones de los clientes entre canales web, multimedia y mensajes push para impulsar el comportamiento de compra por primera vez o por segunda vez.

## Valor empresarial ofrecido

| Objetivos | Tácticas | Valor conseguido |
|---|---|---|
| **Orquestación de recorridos de clientes en tiempo real **<br></br>** Impulsar la repetición de compras de los clientes nuevos **<br></br>** Mejore la eficacia del marketing y reduzca los costes de los medios**</ul> | <ul><li>Sólida estrategia de datos e identidad para impulsar un perfil integral en tiempo real.</li><li>Flujo continuo de datos transaccionales y del cliente en tiempo real, incluida una carga histórica de 90 días.</li><li>Segmentación por flujo continuo a Advertising Networks y Adobe Target para potenciar el gasto en medios y los esfuerzos de personalización.</li><li>Recorridos de clientes en tiempo real a través de Adobe Campaign, que incluye una estrategia para medir el rendimiento.</li></ul> | <ul><li><strong>Real-time Customer Data Platform:</strong> entrega de experiencias del cliente en tiempo real en medios, correo electrónico, mensajes push y canales web.</li><li><strong>Fuentes de datos:</strong> datos de flujo que cubren las tiendas de perfiles, el sistema de pedidos, el catálogo de productos y los puntos de venta de este minorista.</li><li><strong>Activación de medios en tiempo real:</strong> transmisión de segmentos a Advertising Networks para la atribución y supresión de anuncios.</li><li><strong>Personalización web en tiempo real:</strong> transmisión de segmentos activados a Adobe Target para activarlos en la experiencia web del minorista.</li><li><strong>Journey Orchestration a escala:</strong> mensajería activada en tiempo real enriquecida con todos los datos de los clientes disponibles y activada en tiempo real en canales de correo electrónico y mensajes push.</li></ul> |


## Casos de uso

| Categoría | Objetivo | Caso de uso | Descripción |
|:----|:----|:----|:----|
| Recorridos del cliente | Adquisición | Serie de bienvenida | Dé la bienvenida a nuevos suscriptores con una presentación de la empresa y sus productos y servicios |
| | | Programa de primera compra | |
| | Mejore las ventas | Carro de compras abandonado/Examinar | Recupere posibles compradores y aumente las ventas |
| | | Revisión de productos/Venta cruzada | Realice más ventas cruzadas con reseñas de productos |
| | | Promociones de productos |  |
| | | Hora de repetir el pedido | Recordatorio recurrente para productos/servicios cíclicos |
| | Lealtad de marca | Recuperar el éxito | Recupere a los clientes que han estado inactivos. |
| | | Recordatorios de cumpleaños | Forme parte de la celebración de los cumpleaños de sus clientes y fomente una relación más personal con ellos. |
| Comercialización | Administrar inventario | De nuevo en stock | Mejore el inventario mostrando a los clientes que los productos que querían vuelven a estar en stock |
| | | Siguiente mejor categoría | Identifique las mejores categorías/ventas para los usuarios |
| | | Más vendidos | |
| | | Recordatorios de bajada de precios | Mostrar a los usuarios que los artículos que les han gustado tienen un precio reducido |
| | | Productos similares |  |
| Personalizar | Aumentar conversión | Cupones/Ofertas | Mostrar mejores ofertas/cupones a los clientes |
| | | Búsqueda personalizada de productos | Mejorar la experiencia de búsqueda |
| | | Recomendaciones de productos | Mejore la experiencia de navegación por los productos |
| | | Experiencia en todos los canales | Llegue a los clientes en todos los canales |
| Medida | Comprender los recorridos del cliente | Campaña en canales múltiples | Medición de campañas en canales múltiples |
| | | Rendimiento de los segmentos | Comprender el rendimiento y la contribución de los segmentos |
| | | Informes de visitas en el orden previsto | Visualice las conversiones en cada fase |
| | | Análisis de cohorte | Medición de la participación entre grupos de segmentos |
| | | Informes Click-to-Brick | Vea cómo las conversiones de los clientes conducen a la experiencia en la tienda |
| | | Atribución | Vea qué punto de contacto/experiencia tiene mayor influencia en conversiones de compras |
| | | Insights predictivos | Más información sobre las propensiones de los clientes |

## Arquitectura

<img src="../vertical-blueprints/assets/retail-architecture.png" alt="Arquitectura de referencia comercial" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />


## Modelos relacionados


| Caso de uso/Integración  | Vínculo |
|:----|:----|
| CJA + AEP | [Visión general sobre los modelos de Customer Journey Analytics](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journey-analytics/overview.html?lang=es) |
| | [Customer Journey Analytics: casos de uso](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cja-usecases.html?lang=es) |
| AJO + AEP | [Adobe Journey Optimizer: casos de uso](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/journey-optimizer.html?lang=es) |
| | [Gestión de decisiones ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview.html?lang=es) |
| RTCDP + AEP | [Activación de Audiencia en línea/sin conexión](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=es) |
| | [Experience Platform + Application Activation](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=es) |
| Marketo + AEP | [Activación y marketing B2B ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/overview.html?lang=es) | |
| Target + AEP | [Caso de uso de Adobe Target: personalización web y móvil basada en el comportamiento](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/web-personalization/behavioral.html?lang=es) | [Personalización web y móvil con datos de clientes conocidos](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/web-personalization/known-personalization.html?lang=es) | |
