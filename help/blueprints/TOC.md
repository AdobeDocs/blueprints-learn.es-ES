---
user-guide-title: Objetivos empresariales, casos de uso, diagramas y modelos de arquitectura de Customer Experience Orchestration
breadcrumb-title: Casos de uso y modelos
user-guide-description: Explore los objetivos comerciales clave, los patrones de casos de uso y los casos de uso del sector para Adobe Experience Platform y aplicaciones. Los diagramas y modelos de arquitectura visual proporcionan referencias técnicas para la integración de sistemas, flujos de datos y el diseño de soluciones, lo que conecta el valor empresarial con la implementación.
product: Adobe Experience Platform
mini-toc-levels: 3
role: Developer, User
nudge: orange
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 15%
---

# Modelos de organización de experiencia del cliente {#architecture}

+ [Modelos de organización de experiencia del cliente](/help/blueprints/overview.md)
+ Objetivos comerciales clave para AEP y aplicaciones{#business-objectives}
  + [Información general](/help/blueprints/business-objectives/overview.md)
  + Adquisición y crecimiento{#acquisition-growth}
    + [Adquirir nuevos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)
    + [Aumentar generación de posibles clientes](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)
    + [Aumentar la participación del sitio web](/help/blueprints/business-objectives/acquisition-growth/increase-website-engagement.md)
  + Ingresos y monetización{#revenue-monetization}
    + [Aumentar tasas de conversión](/help/blueprints/business-objectives/revenue-monetization/increase-conversion-rates.md)
    + [Aumentar ingresos y ventas](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)
    + [Aumentar los ingresos de venta cruzada y aumento de ventas](/help/blueprints/business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)
    + [Aumentar la lealtad del cliente y el valor de duración](/help/blueprints/business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)
  + Coste y eficiencia{#cost-efficiency}
    + [Reducción del coste de adquisición de clientes](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)
    + [Optimizar el gasto y el retorno de la inversión en marketing](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)
    + [Mejorar la calidad y la gobernanza de los datos](/help/blueprints/business-objectives/cost-efficiency/improve-data-quality-governance.md)
    + [Consolidar y modernizar la tecnología de marketing](/help/blueprints/business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md)
  + Experiencia del cliente{#customer-experience-objectives}
    + [Ofrezca experiencias de cliente personalizadas](/help/blueprints/business-objectives/customer-experience/deliver-personalized-customer-experiences.md)
    + [Mejore la retención de clientes](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)
    + [Mejore la incorporación del cliente](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)
    + [Recuperar carritos y Recorridos abandonados](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)
  + Analytics y perspectivas{#analytics-insights}
    + [Mejorar análisis e informes](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)
    + [Habilitar la toma de decisiones basada en datos](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)
    + [Mejorar la atribución de marketing](/help/blueprints/business-objectives/analytics-insights/improve-marketing-attribution.md)
  + Calificación y ventas (B2B){#qualification-sales-b2b}
    + [Mejore la calificación y conversión de posibles clientes](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)
    + [Mejore la participación del cliente](/help/blueprints/business-objectives/qualification-sales-b2b/improve-customer-engagement.md)
+ Patrones de casos de uso{#use-case-patterns}
  + [Información general](/help/blueprints/use-case-patterns/overview.md)
  + Generación y activación de audiencias{#audience-building-activation}
    + [Audience Activation a destinos](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md)
    + [Audience Collaboration con coincidencia de segmentos](/help/blueprints/use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md)
    + [Reenvío de eventos](/help/blueprints/use-case-patterns/audience-building-activation/event-forwarding.md)
    + [Búsqueda de perfil en tiempo real para soporte y ventas](/help/blueprints/use-case-patterns/audience-building-activation/real-time-profile-lookup.md)
    + [Ciencia de datos personalizados para enriquecimiento de perfiles](/help/blueprints/use-case-patterns/audience-building-activation/data-science-profile-enrichment.md)
  + Personalización{#personalization-patterns}
    + [Personalization web de visitante anónimo](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md)
    + [Personalization de aplicación/web de visitante conocido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md)
    + [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md)
    + [Recomendación de comportamiento](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md)
    + [Acceso al perfil de Edge para Personalization web/móvil](/help/blueprints/use-case-patterns/personalization/edge-profile-access.md)
    + [Uso compartido de audiencias con Adobe Target](/help/blueprints/use-case-patterns/personalization/audience-sharing-with-target.md)
  + Administración y orquestación de campañas{#campaign-orchestration-patterns}
    + [Activación de mensaje saliente por lotes](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md)
    + [Mensajería activada por eventos](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md)
    + [Recorrido orquestado de varios pasos](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md)
    + [Recorrido en canales múltiples con toma de decisiones](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
    + [Orquestación por lotes y mensajería transaccional de Campaign v8](/help/blueprints/use-case-patterns/campaign-management-orchestration/campaign-v8-orchestration.md)
    + [Integración de mensajería de terceros con Journey Optimizer](/help/blueprints/use-case-patterns/campaign-management-orchestration/third-party-messaging.md)
  + Análisis{#analysis-patterns}
    + [Generación de Customer Analytics y Insight](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md)
  + Activación y marketing B2B{#b2b-patterns}
    + [Audience Activation B2B](/help/blueprints/use-case-patterns/b2b/account-audience-activation.md)
    + [Adquisición de gestión de Recorridos y marketing basada en grupos](/help/blueprints/use-case-patterns/b2b/buying-group-marketing.md)
    + [Análisis B2B](/help/blueprints/use-case-patterns/b2b/account-analytics.md)
    + [Recorridos B2B con datos de Marketo](/help/blueprints/use-case-patterns/b2b/marketo-data-journeys.md)
    + [Controladora de medios de pago AJO B2B](/help/blueprints/use-case-patterns/b2b/paid-media-orchestration.md)
    + [Admisión y creación de Marketo y Workfront](/help/blueprints/use-case-patterns/b2b/campaign-intake-and-creation.md)
    + [Revisión y aprobación de Marketo y Workfront](/help/blueprints/use-case-patterns/b2b/campaign-review-and-approval.md)
  + Experiencia de conversación{#conversational-experience-patterns}
    + [Experiencia de conversación en Brand Concierge](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md)
+ Ejemplos de casos de uso del sector{#industry-use-cases}
  + [Catálogo de casos de uso](/help/blueprints/industry-use-cases/use-case-catalog.md)
  + [Automoción](/help/blueprints/industry-use-cases/automotive/automotive-overview.md)
  + [B2B](/help/blueprints/industry-use-cases/b2b/b2b-overview.md)
  + [Servicios financieros](/help/blueprints/industry-use-cases/financial-services/financial-services-overview.md)
  + [Asistencia sanitaria](/help/blueprints/industry-use-cases/healthcare/healthcare-overview.md)
  + [Seguro](/help/blueprints/industry-use-cases/insurance/insurance-overview.md)
  + [Medios de comunicación y entretenimiento](/help/blueprints/industry-use-cases/media-entertainment/media-entertainment-overview.md)
  + [Sector minorista](/help/blueprints/industry-use-cases/retail/retail-overview.md)
  + [Telecomunicaciones](/help/blueprints/industry-use-cases/telecommunications/telecommunications-overview.md)
  + [Tecnología](/help/blueprints/industry-use-cases/technology/technology-overview.md)
  + [Viajes y hospitalidad](/help/blueprints/industry-use-cases/travel-hospitality/travel-hospitality-overview.md)
+ Diagramas y modelos de arquitectura{#architecture-diagrams}
  + Información general de arquitectura{#architecture-overview}
    + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
    + [Experience Platform y aplicaciones](/help/blueprints/experience-platform/platform-applications.md)
    + [Flujo de datos de Experience Platform](/help/blueprints/experience-platform/platform-data-flow.md)
    + [protecciones de Experience Platform](/help/blueprints/experience-platform/guardrails.md)
    + Implementación{#deployment}
      + [Experience Platform Web SDK &amp;  [!DNL Edge Network]](/help/blueprints/experience-platform/deployment/websdk.md)
      + [SDK para aplicaciones](/help/blueprints/experience-platform/deployment/appsdk.md)
  + Activación de audiencias y perfiles{#audience-activation}
    + [Basado en dispositivo: segmentación de audiencia anónima con Audience Manager](/help/blueprints/audience-activation/audience-manager.md)
    + Real-Time Customer Data Platform (RTCDP) {#known-customer-audience-activation}
      + [Activación de audiencias en destinos sociales y publicitarios](/help/blueprints/audience-activation/advertising-activation.md)
      + [Modelo de activación de audiencia y perfil a destinos empresariales](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [Acceso a perfiles en tiempo real para casos de soporte y ventas](/help/blueprints/audience-activation/customer-activity.md)
      + [Acceso a perfiles Edge en tiempo real para personalización web y móvil](/help/blueprints/audience-activation/real-time-lookup.md)
      + [Colaboración de audiencias con Coincidencia de segmentos](/help/blueprints/audience-activation/segment-match.md)
      + [Personalización de clientes conocida con Target](/help/blueprints/audience-activation/rtcdp-target.md)
      + [Ciencia de datos personalizada para enriquecimiento de perfiles](/help/blueprints/audience-activation/data-science.md)
  + Activación y marketing B2B{#b2b-activation}
    + [Información general](/help/blueprints/b2b/overview.md)
    + [Activación B2B](/help/blueprints/b2b/b2bactivation.md)
    + [Activación de cuenta B2B](/help/blueprints/b2b/b2b-account-activation.md)
    + [Adquisición de gestión de recorridos y marketing basada en grupos](/help/blueprints/b2b/b2b-buying-group-journeys.md)
    + [Recorridos B2B que utilizan datos de Marketo](/help/blueprints/b2b/b2b-journeys-with-marketo.md)
    + [Controladora de medios de pago B2B](/help/blueprints/b2b/ajo-b2b-paid-media-controller.md)
    + Modelo de integración de Marketo Engage y Workfront{#marketo-engage-and-workfront-integration-blueprint}
      + [Información general](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
      + [Admisión y creación](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
      + [Revisar y aprobar](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
      + [Historias de éxito de clientes](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md)
  + Customer Journey Analytics{#customer-journey-analytics}
    + [Información general](/help/blueprints/customer-journey-analytics/overview.md)
    + [Customer Journey Analytics B2B](/help/blueprints/customer-journey-analytics/b2b-cja.md)
    + [Uso compartido de audiencias de CJA con RTCDP](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
    + [CJA y Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
    + [Análisis de datos e inteligencia](/help/blueprints/customer-journey-analytics/analysis.md)
  + Recorridos del cliente{#customer-journeys}
    + [Información general](/help/blueprints/customer-journeys/overview.md)
    + Journey Optimizer{#journey-optimizer}
      + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md)
      + [AJO recorrido](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-journeys.md)
      + [Campañas de AJO](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-campaigns.md)
      + [Mensajería de terceros](/help/blueprints/customer-journeys/journey-optimizer/3rd-party-messaging.md)
    + Gestión de decisiones{#decision-management}
      + [Información general](/help/blueprints/customer-journeys/decision-management/decision-management-overview.md)
      + [Gestión de decisiones en Edge](/help/blueprints/customer-journeys/decision-management/decision-management-edge.md)
      + [Administración de decisiones en el concentrador](/help/blueprints/customer-journeys/decision-management/decision-management-hub.md)
    + Campaign v8{#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8/campaign-v8-overview.md)
      + [Real-Time CDP con Adobe [!DNL Campaign] v8](/help/blueprints/customer-journeys/campaign-v8/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer con Adobe Campaign v8](/help/blueprints/customer-journeys/campaign-v8/ajo-and-campaign-v8.md)
    + Modelos obsoletos{#deprecated-blueprints}
      + Campaign Standard{#campaign-standard}
        + [[!DNL Campaign Standard]](https://experienceleague.adobe.com/en/docs/campaign-standard){target="_blank"}
        + [Real-Time CDP con Adobe [!DNL Campaign Standard]](https://experienceleague.adobe.com/en/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/get-started-sources-destinations)
      + Campaign v7{#campaign-v7}
        + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md)

+ Laboratorios prácticos{#labs}
  + [Información general sobre los laboratorios prácticos](/help/blueprints/labs/overview.md)
  + Talleres prácticos{#workshops}
    + AEP Foundations{#aep-foundations}
      + [Información general](/help/blueprints/labs/aep-foundations/overview.md)
      + [Configuración](/help/blueprints/labs/aep-foundations/setup.md)
      + Configuración de zona protegida{#aep-sandbox}
        + [Configuración de Developer Console](/help/blueprints/labs/aep-foundations/sandbox-setup/developer-console-setup.md)
        + [Instrucciones de implementación](/help/blueprints/labs/aep-foundations/sandbox-setup/deployment-instructions.md)
      + Configuración de Postman{#aep-postman}
        + [Instalación de Postman](/help/blueprints/labs/aep-foundations/postman-setup/postman-installation.md)
        + [Archivo de entorno](/help/blueprints/labs/aep-foundations/postman-setup/environment-file.md)
        + [Colección de API](/help/blueprints/labs/aep-foundations/postman-setup/api-collection.md)
        + [Acceso a zona protegida](/help/blueprints/labs/aep-foundations/postman-setup/sandbox-access.md)
        + [Token de acceso](/help/blueprints/labs/aep-foundations/postman-setup/access-token.md)
      + Perfil del cliente en tiempo real{#aep-rtcp}
        + [Conferencias](/help/blueprints/labs/aep-foundations/real-time-customer-profile/lectures.md)
        + Inspección del perfil{#aep-rtcp-inspect}
          + [Información general](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/overview.md)
          + [Conceptos básicos de perfil](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/profile-basics.md)
          + [Políticas de combinación](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/merge-policies.md)
          + [API de perfil e identidad](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/profile-and-identity-apis.md)
      + Metodología LID{#aep-lid}
        + [Prerrequisitos](/help/blueprints/labs/aep-foundations/lid-methodology/prerequisites.md)
        + [Etiqueta](/help/blueprints/labs/aep-foundations/lid-methodology/label.md)
        + Identificar{#aep-lid-identify}
          + [Información general](/help/blueprints/labs/aep-foundations/lid-methodology/identify/overview.md)
          + [Parte 1: Tipos de tablas restantes](/help/blueprints/labs/aep-foundations/lid-methodology/identify/part-1-remaining-table-types.md)
          + [Parte 2: Campos clave](/help/blueprints/labs/aep-foundations/lid-methodology/identify/part-2-key-fields.md)
        + [Desnormalizar](/help/blueprints/labs/aep-foundations/lid-methodology/denormalize.md)
      + Modelado XDM{#aep-xdm}
        + [Conferencias](/help/blueprints/labs/aep-foundations/xdm-modeling/lectures.md)
        + Modelado de IU{#aep-xdm-ui}
          + [Información general](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/overview.md)
          + [Inicio de sesión y exploración](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/login-and-browse.md)
          + [Objetos estándar del modelo](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/model-standard-objects.md)
          + [Objetos personalizados de modelo](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/model-custom-objects.md)
          + [Configurar para el perfil](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/configure-for-profile.md)
        + Modelado de API{#aep-xdm-api}
          + [Información general](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/overview.md)
          + Crear esquema{#aep-xdm-api-build}
            + [Información general](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/overview.md)
            + [Obtener grupos de campos estándar](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/get-standard-field-groups.md)
            + [Crear grupos de campos personalizados](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/create-custom-field-groups.md)
            + [Obtener clase de perfil](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/get-profile-class.md)
            + [Crear esquema](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/create-schema.md)
            + [Ver esquema](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/view-schema.md)
            + [Modificar esquema: parche de JSON](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/modify-schema-json-patch.md)
          + Marcar campos de identidad{#aep-xdm-api-identity}
            + [Información general](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/overview.md)
            + [Crear identidad principal](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/create-primary-identity.md)
            + [Crear otras identidades](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/create-other-identities.md)
            + [Ver esquema](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/view-schema.md)
          + Definir relaciones{#aep-xdm-api-relationships}
            + [Información general](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/overview.md)
            + [Obtener ID de esquema de plan](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/get-plan-schema-id.md)
            + [Crear relación de esquema](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/create-schema-relationship.md)
            + [Crear identidad de referencia del plan](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/create-plan-reference-identity.md)
            + [Ver esquema](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/view-schema.md)
          + [Resumen](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/recap.md)
        + Laboratorios de bonificación{#aep-xdm-bonus}
          + [Automatización con API](/help/blueprints/labs/aep-foundations/xdm-modeling/bonus-labs/automate-with-apis.md)
      + Ingesta de datos{#aep-ingestion}
        + [Conferencias](/help/blueprints/labs/aep-foundations/data-ingestion/lectures.md)
        + [Resumen de laboratorio](/help/blueprints/labs/aep-foundations/data-ingestion/lab-overview.md)
        + [Archivos de muestra](/help/blueprints/labs/aep-foundations/data-ingestion/sample-files.md)
        + Ingesta por lotes{#aep-ingestion-batch}
          + [Información general](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/overview.md)
          + [Crear flujo de datos](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/create-dataflow.md)
          + Datos de asignación{#aep-ingestion-batch-mapping}
            + [Información general](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/overview.md)
            + [Corregir asignaciones de paso a través](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/fix-passthrough-mappings.md)
            + [Campos calculados](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/calculated-fields.md)
            + [Comprobar conjunto de asignaciones final](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/check-final-mapping-set.md)
          + [Ejecutar flujo de datos](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/run-dataflow.md)
          + [Depuración de errores](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/debugging-errors.md)
          + [Crear un nuevo flujo de datos](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/create-a-new-dataflow.md)
          + [Corrección de errores](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/fixing-errors.md)
          + [Verificación y validación](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/verification-and-validation.md)
        + Ingesta de flujo{#aep-ingestion-stream}
          + [Información general](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/overview.md)
          + [Configuración de Source](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/setup-source.md)
          + [Configurar asignación](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/configure-mapping.md)
          + [Comprobar conjunto de asignaciones final](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/check-final-mapping-set.md)
          + [Transmitir un perfil](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/stream-a-profile.md)
          + [Verificar perfil introducido](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/verify-ingested-profile.md)
          + [Supervisión y depuración de errores](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/monitoring-and-debugging-errors.md)
          + [Verificación y validación](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/verification-and-validation.md)
        + Laboratorios de bonificación{#aep-ingestion-bonus}
          + [Corregir errores de MAPPER para CreateDate](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/fix-mapper-errors-for-createdate.md)
          + [Transmitir un evento de pedido](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/stream-an-order-event.md)
          + Uso de la zona de aterrizaje de datos{#aep-ingestion-dlz}
            + [Información general](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/overview.md)
            + [Configuración de Source](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/setup-source.md)
            + [Crear asignaciones](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/create-mappings.md)
            + [Programar flujo de datos](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/schedule-dataflow.md)
            + [Reintento de un flujo de datos fallido](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/retry-a-failed-dataflow.md)
            + Cargar pedidos{#aep-ingestion-dlz-orders}
              + [Información general](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/overview.md)
              + [Configuración de Source](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/setup-source.md)
              + [Asignaciones iniciales](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/initial-mappings.md)
              + [Asignaciones de copia de objeto](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/object-copy-mappings.md)
              + [Verificar y programar flujo de datos](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/verify-and-schedule-dataflow.md)
      + Segmentación y activación{#aep-segmentation}
        + [Conferencia](/help/blueprints/labs/aep-foundations/segmentation-and-activation/lecture.md)
        + Edge Activation{#aep-segmentation-edge}
          + [Información general](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/overview.md)
          + [Crear audiencia de Edge](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/create-edge-audience.md)
          + [Enviar un evento de Edge](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/send-an-edge-event.md)
          + Configuración del reenvío de eventos{#aep-segmentation-edge-ef}
            + [Información general](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/overview.md)
            + [Crear propiedad](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/create-property.md)
            + [Crear flujo de datos](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/create-datastream.md)
      + Generación de audiencias{#aep-audiences}
        + Caso de uso 1: Adquisición{#aep-uc1}
          + [Información general](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/overview.md)
          + Configurar destinos{#aep-uc1-destinations}
            + [Configurar destino personalizado de Personalization](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/configure-destinations/setup-custom-personalization-destination.md)
            + [Configurar destino de flujo](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/configure-destinations/setup-streaming-destination.md)
          + [Generar audiencia 1](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-1.md)
          + [Generar audiencia 2](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-2.md)
          + [Generar audiencia 3](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-3.md)
          + [Enviar un evento de Edge](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/send-an-edge-event.md)
          + [Revisión del pensamiento crítico](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/critical-thinking-review.md)
        + Caso de uso 2: ampliación de venta{#aep-uc2}
          + [Información general](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/overview.md)
          + [Trabajo previo](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/pre-work.md)
          + [Opción 1: Uso de audiencias para agregar](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/option-1-using-audiences-to-aggregate.md)
          + [Opción 2: Uso de preacumulados](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/option-2-use-pre-aggregates.md)
          + [Revisión del pensamiento crítico](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/critical-thinking-review.md)
        + Caso de uso 3: Divulgación{#aep-uc3}
          + [Información general](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/overview.md)
          + [Caso de uso de compilación 3](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/build-use-case-3.md)
          + [Revisión del pensamiento crítico](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/critical-thinking-review.md)
        + Laboratorios de bonificación{#aep-audiences-bonus}
          + [Enviar evento de pedido al concentrador](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/send-order-event-to-hub.md)
          + [Enviar evento web a Hub](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/send-web-event-to-hub.md)
          + [Monitorización de eventos](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/monitor-your-event.md)
    + AJO Foundations{#ajo-foundations}
      + [Información general](/help/blueprints/labs/ajo-foundations/overview.md)
      + [Configuración](/help/blueprints/labs/ajo-foundations/setup.md)
      + Configuración de zona protegida{#ajo-sandbox}
        + [Configuración de Developer Console](/help/blueprints/labs/ajo-foundations/sandbox-setup/developer-console-setup.md)
        + [Instrucciones de implementación](/help/blueprints/labs/ajo-foundations/sandbox-setup/deployment-instructions.md)
      + Configuración de Postman{#ajo-postman}
        + [Instalación de Postman](/help/blueprints/labs/ajo-foundations/postman-setup/postman-installation.md)
        + [Importar archivo de entorno](/help/blueprints/labs/ajo-foundations/postman-setup/import-environment-file.md)
        + [Importar colección de API](/help/blueprints/labs/ajo-foundations/postman-setup/import-api-collection.md)
      + Bloques de creación de arquitectura{#ajo-architecture}
        + [Conferencia](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/lecture.md)
        + Asignación de casos de uso a la arquitectura{#ajo-architecture-mapping}
          + [Información general](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/overview.md)
          + [Introducción al laboratorio](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-introduction.md)
          + [Ejercicio de laboratorio](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-exercise.md)
          + [Revisión de laboratorio](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-review.md)
      + Almacenes de datos{#ajo-data-stores}
        + [Conferencia sobre el perfil del cliente en tiempo real](/help/blueprints/labs/ajo-foundations/data-stores/real-time-customer-profile-lecture.md)
        + Perfil en acción{#ajo-profile}
          + [Información general](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/overview.md)
          + [Inicio de sesión y exploración](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/login-and-browse.md)
          + [Crear flujo de datos](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/create-datastream.md)
          + [Enviar un evento web de Edge](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/send-an-edge-web-event.md)
          + [Validar perfil en Hub](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-on-hub.md)
          + [Validar perfil en Edge](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-on-edge.md)
          + [Validar evento en el lago de datos](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-event-on-data-lake.md)
          + [Validar instantánea de perfil](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-snapshot.md)
          + [Resumen](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/summary.md)
        + [Conferencia sobre almacenamiento relacional](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-lecture.md)
        + Almacenamiento relacional en acción{#ajo-relational}
          + [Información general](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/overview.md)
          + [Examinar esquemas](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/browse-schemas.md)
          + [Dimension de destino de perfil](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/profile-target-dimension.md)
          + [Leer una audiencia](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/read-an-audience.md)
          + [Resumen](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/summary.md)
        + Configurar canales de correo electrónico{#ajo-email}
          + [Información general](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/overview.md)
          + [Configurar para el perfil](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/configure-for-profile.md)
          + [Configurar para relacional](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/configure-for-relational.md)
          + [Esperando al estado activo](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/waiting-for-active-status.md)
      + Campañas orquestadas{#ajo-campaigns}
        + [Conferencia de entrega de mensajes](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-lecture.md)
        + Entrega de mensajes en acción{#ajo-campaigns-delivery}
          + [Información general](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/overview.md)
          + [Crear una campaña](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/create-a-campaign.md)
          + [Crear una audiencia](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/build-an-audience.md)
          + [Añadir actividad de bifurcación](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/add-fork-activity.md)
          + [Añadir actividades de correo electrónico](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/add-email-activities.md)
          + [Prueba de la campaña](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/test-the-campaign.md)
          + [Resumen](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/summary.md)
        + [Conferencia sobre bloques de creación de flujos de trabajo](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/workflow-building-blocks-lecture.md)
        + Lanzamiento del teléfono insignia{#ajo-campaigns-flagship}
          + [Información general](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/overview.md)
          + [Configuración del canal de SMS](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/configure-sms-channel.md)
          + [Creación de una campaña organizada](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/create-an-orchestrated-campaign.md)
          + [Crear una audiencia](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/build-an-audience.md)
          + [Ramificar el resultado](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/fork-the-result.md)
          + [Guardar la audiencia](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/save-the-audience.md)
          + [Filtrar las líneas](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/filter-the-lines.md)
          + [Componga el SMS](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/compose-the-sms.md)
          + [Ejecutar el flujo de trabajo](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/run-the-workflow.md)
          + [Resumen](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/summary.md)
      + Recorridos{#ajo-journeys}
        + [Conferencia](/help/blueprints/labs/ajo-foundations/journeys/lecture.md)
        + Emoción tras la compra{#ajo-journeys-post-purchase}
          + [Información general](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/overview.md)
          + [Configurar evento](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/configure-event.md)
          + [Configurar acción personalizada](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/configure-custom-action.md)
          + [Generar Recorrido](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/build-journey.md)
          + [Recorrido de prueba](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/test-journey.md)
          + [Enviar un evento](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/send-an-event.md)
          + [Validar evento introducido](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/validate-event-ingested.md)
          + [Validar Recorrido](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/validate-journey.md)
          + [Resumen](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/summary.md)
      + Decisioning{#ajo-decisioning}
        + [Experience Edge](/help/blueprints/labs/ajo-foundations/decisioning/experience-edge.md)
        + Decisión explicada{#ajo-decisioning-explained}
          + [Información general](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/overview.md)
          + [Introducción](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/introduction.md)
          + [XDM del elemento de decisión](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-item-xdm.md)
          + [Creación de elemento de decisión](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-item-creation.md)
          + [Colecciones](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/collections.md)
          + [Fórmulas de clasificación](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/ranking-formulas.md)
          + [Estrategias de selección](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/selection-strategies.md)
          + [Políticas de decisión](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-policies.md)
          + [Protecciones, modelos de IA y decisiones futuras](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/guardrails-ai-models-decisioning-future.md)
        + Exploración abandonada{#ajo-decisioning-abandoned}
          + [Información general](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/overview.md)
          + [Crear regla de decisión](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-decision-rule.md)
          + [Crear atributos de oferta](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-attributes.md)
          + [Crear elementos de oferta](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-items.md)
          + [Crear colección de ofertas](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-collection.md)
          + [Crear fórmula de clasificación](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-ranking-formula.md)
          + [Crear estrategia de selección](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-selection-strategy.md)
          + [Crear canal de experiencia basado en código](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-code-based-experience-channel.md)
          + [Creación del Recorrido](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-the-journey.md)
          + [Toma de decisiones y CBE en acción](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/decisioning-and-cbes-in-action.md)
          + [Resumen](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/summary.md)
      + Creación de contenido con IA{#ajo-content-ai}
        + [Conferencia](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/lecture.md)
        + [Información general](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/overview.md)
        + [Administración de marca](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/brand-management.md)
        + [Creación de fragmentos de contenido](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/building-content-fragments.md)
        + [Creación de plantilla de contenido](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/building-content-template.md)
        + [Creación del correo electrónico](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/creating-the-email.md)
        + [Asistente de IA y Personalization de contenido](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/ai-assistant-and-content-personalization.md)
        + [Personalization y experimentación de contenido](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/personalization-and-content-experimentation.md)
        + [Simulación de contenido](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/content-simulation.md)
        + [Alineación de marca](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/brand-alignment.md)
        + [Prueba del correo electrónico](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/test-the-email.md)
        + [Resumen](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/summary.md)
