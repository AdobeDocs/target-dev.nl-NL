---
user-guide-title: Adobe Target Developer Guide
breadcrumb-title: Doelontwikkelaarsgids
user-guide-description: Leer hoe u de ervaring van uw klanten kunt aanpassen en personaliseren om uw omzet te maximaliseren op uw websites en mobiele sites, apps, sociale media en andere digitale kanalen.
source-git-commit: 697822cd7c5afcaac988d61035af56491301dc74
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 3%

---


# Adobe Target Developer Guide {#developer}

+ [Adobe Target Developer Guide](overview.md)
+ Aan de slag {#implementation}
   + Voordat u implementeert {#before-implement}
      + [Voordat u implementeert](before-implement/considerations-before-you-implement-target.md)
      + [Voorbereiden op implementatie van doel](before-implement/prepare-to-implement-target.md)
   + Privacy en beveiliging {#privacy}
      + [Privacyoverzicht](before-implement/privacy/privacy.md)
      + [Regels inzake privacy en gegevensbescherming](before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)
      + [Doelcookies](before-implement/privacy/cookie-behavior.md)
      + [Het doelcookie verwijderen](before-implement/privacy/cookie-deleting.md)
      + [Het effect van de afleiding van cookies van derden op Target (at.js)](/help/dev/before-implement/privacy/third-party-cookie-deprecation.md)
      + [Google Chrome SameSite cookie beleidsregels](before-implement/privacy/google-chrome-samesite-cookie-policies.md)
      + [Apple Intelligent Tracking Prevention (ITP) 2.x](before-implement/privacy/apple-itp-2x.md)
      + [Inhoudsbeveiligingsbeleid (CSP)-instructies](before-implement/privacy/content-security-policy.md)
      + [Lijst van gewenste personen randknooppunten doel](before-implement/privacy/allowlist-edges.md)
   + Methoden om gegevens op te halen in Doel {#methods}
      + [Overzicht van methoden](before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md)
      + [Paginaparameters](before-implement/methods-to-get-data-into-target/page-parameters.md)
      + [Profielkenmerken in pagina](before-implement/methods-to-get-data-into-target/in-page-profile-attributes.md)
      + [Scriptprofielkenmerken](before-implement/methods-to-get-data-into-target/script-profile-attributes.md)
      + [Gegevensleveranciers](before-implement/methods-to-get-data-into-target/data-providers.md)
      + [Bulkprofielupdate-API](before-implement/methods-to-get-data-into-target/bulk-profile-update-api.md)
      + [Single Profile Update API](before-implement/methods-to-get-data-into-target/single-profile-update-api.md)
      + [Klantkenmerken](before-implement/methods-to-get-data-into-target/customer-attributes.md)
      + [Profiel-API-instellingen](before-implement/methods-to-get-data-into-target/profile-api-settings.md)
   + [Overzicht van doelbeveiliging](before-implement/target-security-overview.md)
   + [Ondersteunde browsers](before-implement/supported-browsers.md)
   + [TLS (Transport Layer Security)-coderingswijzigingen](before-implement/tls-transport-layer-security-encryption.md)
   + [CNAME en Adobe Target](before-implement/implement-cname-support-in-target.md)
+ Implementatie op de client {#client-side}
   + [Overzicht: Doel implementeren voor web op client](implement/client-side/overview.md)
   + Adobe Experience Platform Web SDK-implementatie {#aep}
      + [Implementatieoverzicht van Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)
      + [Adobe Target en Platform Web SDK gebruiken voor personalisatie](/help/dev/implement/client-side/aep-web-sdk/target-overview.md)
      + [Implementatie van één pagina](/help/dev/implement/client-side/aep-web-sdk/spa-implementation.md)
      + [Toegang krijgen tot reactietokens](/help/dev/implement/client-side/aep-web-sdk/accessing-response-tokens.md)
      + [Id van derde partij gebruiken](/help/dev/implement/client-side/aep-web-sdk/using-mbox-3rdpartyid.md)
      + [De bibliotheek at.js vergelijken met de Web SDK](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md)
   + Hoe werkt at.js {#at-js}
      + [at.js JavaScript-bibliotheekoverzicht](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)
      + [at.js-werkoverzicht](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
      + [Hoe at.js flikkering beheert](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
      + [at.js-integratie](/help/dev/implement/client-side/atjs/how-atjs-works/target-atjs-integrations.md)
   + Hoe te opstellen bij.js {#deploy-at-js}
      + [Hoe te opstellen bij.js](implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md)
      + [Doel implementeren met Adobe Experience Platform](implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)
      + [Doel implementeren zonder tagbeheer](implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)
      + [Doel implementeren met Dynamic Tag Manager (DTM)](implement/client-side/atjs/how-to-deployatjs/implement-target-using-dtm.md)
      + [Doel implementeren voor toepassingen van één pagina (SPAs)](implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)
   + Apparaatbeslissingen {#on-device-decisioning}
      + [Overzicht van apparaatbeslissingen](implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md)
      + [Ondersteunde functies](implement/client-side/atjs/on-device-decisioning/supported-features.md)
      + [Artefact](implement/client-side/atjs/on-device-decisioning/rule-artifact.md)
      + [Problemen oplossen](implement/client-side/atjs/on-device-decisioning/troubleshooting-on-device-decisioning.md)
   + at.js-functies {#functions-overview}
      + [at.js, functieoverzicht](implement/client-side/atjs/atjs-functions/atjs-functions.md)
      + [adobe.target.getOffer()](implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md)
      + [adobe.target.getOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
      + [adobe.target.applyOffer()](implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md)
      + [adobe.target.applyOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)
      + [adobe.target.triggerView() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)
      + [adobe.target.trackEvent()](implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
      + [mboxCreate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)
      + [targetGlobalSettings()](implement/client-side/atjs/atjs-functions/targetglobalsettings.md)
      + [mboxDefine() en mboxUpdate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)
      + [targetPageParams()](implement/client-side/atjs/atjs-functions/targetpageparams.md)
      + [targetPageParamsAll()](implement/client-side/atjs/atjs-functions/targetpageparamsall.md)
      + [registerExtension() - at.js 1.x](implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)
      + [sendNotifications() - at.js 2.1](implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)
      + [at.js, aangepaste gebeurtenissen](implement/client-side/atjs/atjs-functions/atjs-custom-events.md)
      + [Foutopsporing in.js met Adobe Experience Cloud Debugger](implement/client-side/target-debugging-atjs/target-debugging-atjs.md)
      + [Gebruik cloudgebaseerde instanties met Doel](implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md)
   + [at.js Veelgestelde vragen](implement/client-side/atjs/target-atjs-faq.md)
   + [details at.js-versie](implement/client-side/atjs/target-atjs-versions.md)
   + [Bijwerken van at.js 1.x naar at.js 2.x](implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md)
   + [at.js, cookies](implement/client-side/atjs/atjs-cookies.md)
   + [Gebruiker-agent en cliëntwenken](implement/client-side/atjs/user-agent-and-client-hints.md)
   + De globale box begrijpen {#global-mbox}
      + [Globaal mbox-overzicht](implement/client-side/atjs/global-mbox/global-mbox-overview.md)
      + [Een globale box aanpassen](implement/client-side/atjs/global-mbox/customize-global-mbox.md)
      + [Globale mbox uit een oudere implementatie gebruiken](implement/client-side/atjs/global-mbox/mbox-global-target-standard.md)
      + [Parameters doorgeven aan een globale box](implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md)
      + [Algemene mbox vaak gestelde vragen](implement/client-side/atjs/global-mbox/global-mbox-faq.md)
+ Server-side implementatie {#server-side}
   + [Serverzijde: Overzicht van doel implementeren](implement/server-side/server-side-overview.md)
   + [Aan de slag met doel-SDK&#39;s](implement/server-side/sdk-guides/getting-started/getting-started.md)
   + [Voorbeeldtoepassingen](implement/server-side/sdk-guides/sample-apps/sample-apps.md)
   + [Overgang van verouderde API&#39;s van Target naar Adobe I/O](implement/server-side/transition-from-target-classic-apis.md)
   + Basisbeginselen {#core-principles}
      + [Overzicht van kernbeginselen](implement/server-side/sdk-guides/core-principles/overview.md)
      + [Gebruikersnaam en wachtwoord](implement/server-side/sdk-guides/core-principles/user-identification-and-bucketing.md)
      + [Doelgerichtheid publiek](implement/server-side/sdk-guides/core-principles/audience-targeting.md)
      + [Gebeurtenissen bijhouden](implement/server-side/sdk-guides/core-principles/event-tracking.md)
      + [Gebruikersmachtigingen en -eigenschappen](implement/server-side/sdk-guides/core-principles/user-permissions-and-properties.md)
   + Integratie {#integration}
      + [Overzicht van integratie](implement/server-side/sdk-guides/integration-with-experience-cloud/overview.md)
      + [Experience Cloud ID Service (ECID)](implement/server-side/sdk-guides/integration-with-experience-cloud/ecid.md)
      + [Analyses voor doelrapportage (A4T)](implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md)
      + [AAM-segmenten](implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md)
   + Apparaatbeslissingen {#on-device-decisioning}
      + [Overzicht van apparaatbeslissingen](implement/server-side/sdk-guides/on-device-decisioning/overview.md)
      + Artefact {#rule-artifact}
         + [Overzicht van artikelen](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)
         + [Downloaden via Adobe Target SDK](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-sdk.md)
         + [Downloaden via JSON-payload](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-json.md)
         + [Artefact van voorbeeldregel](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-example.md)
      + [A/B-tests uitvoeren met functiemarkeringen](implement/server-side/sdk-guides/on-device-decisioning/execute-ab-tests-with-feature-flags.md)
      + [Functietests uitvoeren met kenmerken](implement/server-side/sdk-guides/on-device-decisioning/execute-feature-tests-with-attributes.md)
      + [Rolouts voor functietests beheren](implement/server-side/sdk-guides/on-device-decisioning/manage-rollouts-for-feature-tests.md)
      + [Leveren personalisatie](implement/server-side/sdk-guides/on-device-decisioning/deliver-personalization.md)
      + [Overzicht van ondersteunde functies](implement/server-side/sdk-guides/on-device-decisioning/supported-features.md)
      + [Problemen met apparaatbeslissingen oplossen](implement/server-side/sdk-guides/on-device-decisioning/troubleshooting.md)
      + [Aanbevolen procedures](implement/server-side/sdk-guides/best-practices/best-practices.md)
   + Node.js SDK Reference {#node-js}
      + [Overzicht van Node.js SDK](implement/server-side/node-js/overview.md)
      + [De SDK Node.js installeren](implement/server-side/node-js/install-sdk.md)
      + [De SDK Node.js initialiseren](implement/server-side/node-js/initialize-sdk.md)
      + [Offertes ophalen (Node.js)](implement/server-side/node-js/get-offers.md)
      + [Kenmerken ophalen (Node.js)](implement/server-side/node-js/get-attributes.md)
      + [Meldingen verzenden (Node.js)](implement/server-side/node-js/send-notifications.md)
      + [SDK Events (Node.js)](implement/server-side/node-js/sdk-events.md)
      + [Logger (Node.js)](implement/server-side/node-js/logger.md)
      + [Proxyconfiguratie (Node.js)](implement/server-side/node-js/proxy-configuration.md)
   + Java SDK Reference {#java}
      + [Java SDK - overzicht](implement/server-side/java/overview.md)
      + [Java SDK installeren](implement/server-side/java/install-sdk.md)
      + [De Java SDK initialiseren](implement/server-side/java/initialize-sdk.md)
      + [Voorstel ophalen (Java)](implement/server-side/java/get-offers.md)
      + [Kenmerken ophalen (Java)](implement/server-side/java/get-attributes.md)
      + [Meldingen verzenden (Java)](implement/server-side/java/send-notifications.md)
      + [SDK Events (Java)](implement/server-side/java/sdk-events.md)
      + [Aanmelder (Java)](implement/server-side/java/logger.md)
      + [Asynchrone verzoeken (Java)](implement/server-side/java/asynchronous-requests.md)
      + [Proxyconfiguratie (Java)](implement/server-side/java/proxy-configuration.md)
      + [Aangepaste HTTP Client Configuration (Java)](implement/server-side/java/custom-http-client.md)
      + [Hulpprogrammamethoden (Java)](implement/server-side/java/utility-methods.md)
   + .NET SDK Reference {#net}
      + [.NET SDK-overzicht](implement/server-side/net/overview.md)
      + [.Net SDK installeren](implement/server-side/net/install-sdk.md)
      + [De .NET SDK initialiseren](implement/server-side/net/initialize-sdk.md)
      + [Aanbiedingen ophalen (.NET)](implement/server-side/net/get-offers.md)
      + [Kenmerken ophalen (.NET)](implement/server-side/net/get-attributes.md)
      + [Meldingen verzenden (.NET)](implement/server-side/net/send-notifications.md)
      + [SDK Events (.NET)](implement/server-side/net/sdk-events.md)
      + [Asynchrone verzoeken (.NET)](implement/server-side/net/asynchronous-requests.md)
   + Referentie Python SDK {#python}
      + [Overzicht van Python SDK](implement/server-side/python/overview.md)
      + [Python SDK installeren](implement/server-side/python/install-sdk.md)
      + [De Python SDK initialiseren](implement/server-side/python/initialize-sdk.md)
      + [Voorstel ophalen (Python)](implement/server-side/python/get-offers.md)
      + [Kenmerken ophalen (Python)](implement/server-side/python/get-attributes.md)
      + [Meldingen verzenden (Python)](implement/server-side/python/send-notifications.md)
      + [SDK Events (Python)](implement/server-side/python/sdk-events.md)
      + [Asynchrone verzoeken (Python)](implement/server-side/python/asynchronous-requests.md)
      + [Logger (Python)](implement/server-side/python/logger.md)
+ [Hybride implementatie](implement/hybrid/hybrid-overview.md)
+ [Implementatie van aanbevelingen](implement/recommendations/recommendations.md)
+ [bèta implementatie van aanbevelingen](/help/dev/implement/recommendations/recommendations-beta.md)
+ Implementatie van mobiele apps {#mobile-apps}
   + [Overzicht van het doel voor mobiele apps](implement/mobile/overview.md)
   + [Voorvertoning voor mobiele doelversie](implement/mobile/target-mobile-preview.md)
   + [Locatieservice gebruiken](implement/mobile/use-location-service.md)
   + [Veelgestelde vragen over het doel voor mobiele apps](implement/mobile/mobile-faq.md)
   + [Doel implementeren met de AEP Mobile SDK in een systeemeigen app met webweergaven](/help/dev/implement/mobile/native-app.md)
+ E-mailimplementatie {#implement-email}
   + [E-mail: Implementeer overzicht van doel](implement/email/overview.md)
   + [Een dialoogvenster maken voor een afbeelding](implement/email/testing-content-with-the-adbox.md)
   + [Een e-mailafbeeldingsvenster testen](implement/email/testing-email-image-adbox.md)
   + [Werken met directeuren](implement/email/working-with-redirectors.md)
+ API-hulplijnen {#api}
   + [Overzicht doelAPI](/help/dev/before-administer/target-api-overview.md)
   + [Verificatie voor doel-API&#39;s configureren](/help/dev/before-administer/configure-authentication.md)
   + Handleiding voor API voor levering {#delivery-api}
      + [Overzicht van de bezorgings-API](/help/dev/implement/delivery-api/overview.md)
      + [SDK&#39;s voor interactie met de API voor levering](/help/dev/before-implement/delivery-api-overview/sdks.md)
      + [Aan de slag](/help/dev/before-implement/delivery-api-overview/getting-started.md)
      + [Gebruikersmachtigingen (Premium)](/help/dev/before-implement/delivery-api-overview/user-permissions.md)
      + [Bezoekers identificeren](/help/dev/before-implement/delivery-api-overview/identifying-visitors.md)
      + [Single of Batch-levering](/help/dev/before-implement/delivery-api-overview/single-or-batch.md)
      + [Prefetch](/help/dev/before-implement/delivery-api-overview/prefetch.md)
      + [Meldingen](/help/dev/before-implement/delivery-api-overview/notifications.md)
      + [Integratie met Experience Cloud](before-implement/delivery-api-overview/integration.md)
      + [Overwegingen en bekende beperkingen](/help/dev/before-implement/delivery-api-overview/known-limitations.md)
      + [Clienttips](/help/dev/before-implement/delivery-api-overview/client-hints.md)
      + [Leverings-API](/help/dev/implement/delivery-api/delivery-api.md)
   + Admin-API {#admin-api}
      + [Overzicht van Admin API](before-administer/admin-api-overview/admin-api-overview.md)
      + [Adobe Target Admin API](/help/dev/administer/admin-api/admin-api-overview-new.md)
   + Profile API {#profile-apis}
      + [Overzicht van API-profielen](/help/dev/administer/profile-api/profiles-api.md)
      + [Ophaalprofielen](/help/dev/administer/profile-api/profile-fetch.md)
      + [Profielen bijwerken](/help/dev/administer/profile-api/profile-api-overview.md)
      + [Single Profile Update API](/help/dev/administer/profile-api/profile-single-api.md)
      + [Bulkprofielupdate-API](/help/dev/administer/profile-api/profile-bulk-api.md)
   + [API voor rapportage](/help/dev/administer/reporting-api/reporting-api.md)
   + Aanbevelingen-API {#recommendations-api}
      + [Overzicht van de aanbevelingen-API](before-administer/recs-api/overview.md)
      + [Uw catalogus beheren met API&#39;s](before-administer/recs-api/manage-catalog.md)
      + [Aangepaste criteria beheren](before-administer/recs-api/manage-custom-criteria.md)
      + [De leverings-API gebruiken met aanbevelingen](before-administer/recs-api/fetch-recs-server-side-delivery-api.md)
      + [Aanbevelingen-API](/help/dev/administer/recommendations-api/recommendations-api.md)
   + Modellen-API {#models-api}
      + [Overzicht van de model-API (Voegend op lijst van gewenste personen)](before-administer/models-api.md)
      + [Modellen-API](/help/dev/administer/models-api/models-api-overview.md)
   + [Adobe Admin Console API&#39;s](/help/dev/before-implement/delivery-api-overview/adobe-console-api.md)
   + [Adobe Experience Platform Edge Network Server-API](/help/dev/before-implement/delivery-api-overview/aep-edge-network-server-api.md)
+ Implementatiepatronen {#implementation-patterns}
   + [Overzicht van implementatiepatronen](/help/dev/patterns/pattern-overview.md)
   + Implementatiepatroon voor aanbevelingen met behulp van at.js {#atjs}
      + [Implementatiepatroon voor aanbevelingen met behulp van het overzicht at.js](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md)
      + [SDK&#39;s initialiseren](/help/dev/patterns/recs-atjs/initialize-sdk.md)
      + [Gegevensverzameling configureren](/help/dev/patterns/recs-atjs/data-collection.md)
      + [Renderervaringen](/help/dev/patterns/recs-atjs/render-experiences.md)
      + [Doel op hoogte stellen](/help/dev/patterns/recs-atjs/notify-target.md)


