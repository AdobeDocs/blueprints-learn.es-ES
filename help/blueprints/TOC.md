---
user-guide-title: Modelos de experiencia digital
breadcrumb-title: Modelos
user-guide-description: Los modelos son implementaciones repetibles, creadas para solucionar problemas empresariales existentes y que contienen diagramas de arquitectura, consideraciones técnicas y enlaces a documentación relevante.
product: adobe experience platform
mini-toc-levels: 3
role: Architect, Developer, User
source-git-commit: 3cb8d1566e0ce1356c864e360f660a739d0a472a
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 90%

---


# Modelos de experiencia digital {#architecture}

+ [Modelos de experiencias digitales](/help/blueprints/overview.md)
+ Modelos sectoriales verticales {#vertical-blueprints}
   + [Información general](/help/blueprints/vertical-blueprints/overview.md)
   + [Moda](/help/blueprints/vertical-blueprints/apparel.md)
   + [Sector minorista](/help/blueprints/vertical-blueprints/retail.md)
   + [Telecomunicaciones](/help/blueprints/vertical-blueprints/telecommunications.md)
   + [Turismo y hostelería](/help/blueprints/vertical-blueprints/travel-hospitality.md)
+ Información general sobre la arquitectura {#architecture-overview}
   + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
   + [Experience Platform y otras aplicaciones](/help/blueprints/experience-platform/platform-applications.md)
   + [Flujo de datos de Experience Platform](/help/blueprints/experience-platform/platform-data-flow.md)
   + Implementación {#deployment}
      + [SDK web Experience Platform y Edge Network](/help/blueprints/experience-platform/deployment/websdk.md)
      + [SDK para aplicaciones](/help/blueprints/experience-platform/deployment/appsdk.md)
      + [Guardas](/help/blueprints/experience-platform/deployment/guardrails.md)
+ Activación de audiencias y perfiles {#audience-activation}
   + [Información general](/help/blueprints/audience-activation/overview.md)
   + [Audience Activation AAM anónimo ()](/help/blueprints/audience-activation/anonymous.md)
   + Activación de cliente conocida (RTCDP) {#known-customer-audience-activation}
      + [Información general](/help/blueprints/audience-activation/known.md)
      + [Activación en canales publicitarios y sociales](/help/blueprints/audience-activation/advertising-activation.md)
      + [Activación en destinos de flujo empresarial y de archivos](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [Centro de actividad del cliente](/help/blueprints/audience-activation/customer-activity.md)
      + [Coincidencia de segmentos](/help/blueprints/audience-activation/segment-match.md)
   + [Activación con las aplicaciones de Experience Cloud](/help/blueprints/audience-activation/platform-and-applications.md)
   + Personalización web y móvil {#web-personalization}
      + [Información general](/help/blueprints/audience-activation/web-personalization/overview.md)
      + [Personalización del comportamiento: Target](/help/blueprints//audience-activation/web-personalization/behavioral.md)
      + [Personalización de cliente conocida: Target y RTCDP](/help/blueprints/audience-activation/web-personalization/known-personalization.md)
      + [Gestión de decisiones](/help/blueprints/audience-activation/web-personalization/decision-management-edge.md)
+ Activación y marketing B2B {#b2b-activation}
   + [Información general](/help/blueprints/b2b/overview.md)
   + [Activación B2B](/help/blueprints/b2b/b2bactivation.md)
   + Marketo Engage y modelo de integración de Workfront{#marketo-engage-and-workfront-integration-blueprint}
      + [Información general](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
      + [Ingesta y creación](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
      + [Revisión y aprobación](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
      + [Historias de éxito de clientes ](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md)
+ Content &amp; Commerce de{#content-commerce}
   + [ADOBE COMMERCE Y RTCDP](/help/blueprints/content-commerce/commerce/commerce-rtcdp.md)
+ Customer Journey Analytics {#customer-journey-analytics}
   + [Información general](/help/blueprints/customer-journey-analytics/overview.md)
   + [Uso compartido de audiencias de CJA con RTCDP](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
   + [CJA y Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
+ Recorridos del cliente {#customer-journeys}
   + [Información general](/help/blueprints/customer-journeys/overview.md)
   + Journey Optimizer {#journey-optimizer}
      + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer.md)
      + Gestión de decisiones {#decision-management}
         + [Información general](/help/blueprints/customer-journeys/decision_management/decision-management-overview.md)
         + [Gestión de decisiones en Edge](/help/blueprints/customer-journeys/decision_management/decision-management-edge.md)
         + [Gestión de decisiones en el centro](/help/blueprints/customer-journeys/decision_management/decision-management-hub.md)
      + [Journey Optimizer con Adobe Campaign](/help/blueprints/customer-journeys/ajo-and-campaign.md)
      + [Mensajería de terceros](/help/blueprints/customer-journeys/3rd-party-messaging.md)
   + Campaign Standard {#campaign-standard}
      + [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=es){target="_blank"}
      + [Real-Time CDP con Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=es){target="_blank"}
   + Campaign v8 {#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8.md)
      + [Real-Time CDP con Adobe Campaign v8](/help/blueprints/customer-journeys/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer con Adobe Campaign v8](/help/blueprints/customer-journeys/ajo-and-campaign-v8.md)
   + Campaign v7 {#campaign-v7}
      + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7.md)
      + [Real-Time CDP con Adobe Campaign v7](/help/blueprints/customer-journeys/rtcdp-and-campaign.md)
      + [Journey Optimizer con Adobe Campaign v7](/help/blueprints/customer-journeys/ajo-and-campaign-v7.md)
+ Recopilación, acceso y exportación de datos {#data-ingestion}
   + [Información general](/help/blueprints/data-ingestion/overview.md)
   + [Recopilación de datos de reenvío de eventos de múltiples zonas protegidas](/help/blueprints/data-ingestion/multi-sandbox-event-forwarding.md)
   + [Preparación e ingesta de datos](/help/blueprints/data-ingestion/ingestion.md)
   + [Acceso y exportación de datos](/help/blueprints/data-ingestion/egress.md)
   + [Reenvío de eventos](/help/blueprints/data-ingestion/server-side-collection.md)
+ Análisis de datos, inteligencia e IA/ML (aprendizaje automático) {#data-exploration}
   + [Información general](/help/blueprints/data-insights/overview.md)
   + [Análisis de datos e inteligencia](/help/blueprints/data-insights/analysis.md)
   + [Ciencia de datos personalizada para el enriquecimiento de perfiles](/help/blueprints/data-insights/data-science.md)
