---
user-guide-title: Modelos de experiencia digital
breadcrumb-title: Modelos
user-guide-description: Los modelos son implementaciones repetibles, creadas para solucionar problemas empresariales existentes y que contienen diagramas de arquitectura, consideraciones técnicas y enlaces a documentación relevante.
product: adobe experience platform
mini-toc-levels: 3
role: Architect, Developer, User
source-git-commit: af390011dc068c4289f98d7fc0108ce48a5375c7
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 100%

---


# Modelos de experiencia digital {#architecture}

+ [Información general](/help/blueprints/overview.md)
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
      + [SDK web Experience Platform y red de Edge](/help/blueprints/experience-platform/deployment/websdk.md)
      + [SDK para aplicaciones](/help/blueprints/experience-platform/deployment/appsdk.md)
      + [Guardas](/help/blueprints/experience-platform/deployment/guardrails.md)
+ Activación de audiencias y perfiles {#audience-activation}
   + [Información general](/help/blueprints/audience-activation/overview.md)
   + [Activación de audiencia anónima   (AAM)](/help/blueprints/audience-activation/anonymous.md)
   + Activación de cliente conocida (RTCDP) {#known-customer-audience-activation}
      + [Información general](/help/blueprints/audience-activation/known.md)
      + Activación en canales publicitarios y sociales {#audience-activation}
         + [Activación en Facebook Custom Audiences](/help/blueprints/audience-activation/destinations/facebook.md)
         + [Activación en Google Customer Match](/help/blueprints/audience-activation/destinations/gcm.md)
      + [Activación en destinos de flujo empresarial y de archivos](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [Centro de actividad del cliente](/help/blueprints/audience-activation/customer-activity.md)
      + [Coincidencia de segmentos](/help/blueprints/audience-activation/segment-match.md)
   + [Activación con las aplicaciones de Experience Cloud](/help/blueprints/audience-activation/platform-and-applications.md)
+ Activación y marketing B2B {#b2b-activation}
   + [Información general](/help/blueprints/b2b/overview.md)
   + [Activación B2B](/help/blueprints/b2b/b2bactivation.md)
   + Cadena de suministro de campañas con Marketo y Workfront {#optimize-campaign-supply-chain-with-marketo-and-workfront}
      + [Información general](/help/blueprints/b2b/campaign-supply-chain/overview.md)
      + [Ingesta y creación](/help/blueprints/b2b/campaign-supply-chain/intake-and-create.md)
      + [Historias de éxito de clientes](/help/blueprints/b2b/campaign-supply-chain/customer-success-stories.md)
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
      + [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=es)
      + [Real-Time CDP con Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=es)
   + Campaign v8 {#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8.md)
      + [Real-Time CDP con Adobe Campaign v8](/help/blueprints/customer-journeys/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer con Adobe Campaign v8](/help/blueprints/customer-journeys/ajo-and-campaign-v8.md)
   + Campaign v7 {#campaign-v7}
      + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7.md)
      + [Real-Time CDP con Adobe Campaign  v7](/help/blueprints/customer-journeys/rtcdp-and-campaign.md)
      + [Journey Optimizer con Adobe Campaign v7](/help/blueprints/customer-journeys/ajo-and-campaign-v7.md)
+ Recopilación, acceso y exportación de datos {#data-ingestion}
   + [Información general](/help/blueprints/data-ingestion/overview.md)
   + [Preparación e ingesta de datos](/help/blueprints/data-ingestion/ingestion.md)
   + [Acceso y exportación de datos](/help/blueprints/data-ingestion/egress.md)
   + [Reenvío de eventos](/help/blueprints/data-ingestion/server-side-collection.md)
+ Análisis de datos, inteligencia e IA/ML (aprendizaje automático) {#data-exploration}
   + [Información general](/help/blueprints/data-insights/overview.md)
   + [Análisis de datos e inteligencia](/help/blueprints/data-insights/analysis.md)
   + [Ciencia de datos personalizada para el enriquecimiento de perfiles](/help/blueprints/data-insights/data-science.md)
+ Personalización web y móvil {#web-personalization}
   + [Información general](/help/blueprints/web-personalization/overview.md)
   + [Personalización basada en comportamiento  - Target](/help/blueprints/web-personalization/behavioral.md)
   + [Personalización de cliente conocida: Target y RTCDP](/help/blueprints/web-personalization/known-personalization.md)
   + [Gestión de decisiones](/help/blueprints/web-personalization/decision-management-edge.md)