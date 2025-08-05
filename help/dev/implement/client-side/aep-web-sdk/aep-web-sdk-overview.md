---
keywords: Adobe Experience Platform Web SDK, aep web sdk, web sdk, sdk, adobe Experience cloud, platform edge network, adobe Experience platform edge network, edge network, aep edge network, Adobe Experience Platform Web SDK0
description: Leer hoe u de [!UICONTROL Adobe Experience Platform Web SDK] kunt gebruiken om te communiceren met de verschillende services in de [!UICONTROL Adobe Experience Cloud] tot en met de [!UICONTROL AEP Edge Network] .
title: Hoe kan ik implementeren met de [!UICONTROL Experience Platform Web SDK] ?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: ac03d5d15875ab4945b07b3e95037ce9ecde1044
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK) is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van [!UICONTROL Adobe Experience Cloud] kunnen communiceren met de verschillende services in de [!DNL Adobe Experience Cloud] (inclusief [!DNL Target] ) via de [!UICONTROL Adobe Experience Platform Edge Network] . Naast de JavaScript-bibliotheek is er een [!UICONTROL Adobe Experience Platform] -extensie voor hulp bij uw Web SDK-configuraties.

Raadpleeg de volgende koppelingen in de Help van *[!UICONTROL Adobe Experience Platform Web SDK]* voor meer informatie:

* Voor uitvoerige informatie: [ wat is [!UICONTROL Adobe Experience Platform Web SDK] ](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* Voor informatie specifiek voor [!DNL Target]: [[!DNL Target]  Overzicht ](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html)

## Tutorials

De volgende zelfstudies helpen u bij uw implementatie:

### [!DNL Adobe Experience Cloud] implementeren met [!DNL Platform Web SDK]

Leer hoe te om [!DNL Experience Cloud] toepassingen uit te voeren gebruikend [!DNL Adobe Experience Platform Web SDK] met [ dit leerprogramma ](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html). Voor informatie specifiek voor [!DNL Target], zie de tutorial sectie getiteld [ Opstelling  [!DNL Target]  met het Web SDK van het Platform ](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### Migreer [!DNL Target] vanuit at.js 2.*x* aan [!DNL Platform Web SDK]

Leer hoe u uw [!DNL Target] -implementatie kunt migreren vanaf at.js 2.*x* aan [!DNL Adobe Experience Platform Web SDK] met [ dit leerprogramma ](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html).

## Aanbevolen documentatie

Naast de [!UICONTROL Platform Web SDK] -documentatie die hierboven is vermeld, bevatten onderwerpen in deze handleiding ook specifieke informatie over [!UICONTROL Platform Web SDK] voor wat betreft de functies en functionaliteit van [!DNL Target] .

| Functie | Beschrijving/koppeling |
| --- | --- |
| [ Activiteit QA ](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | Gebruik URL&#39;s met kwaliteitsgarantie in [!DNL Target] om eenvoudige end-to-end activiteit-QA met voorvertoningskoppelingen uit te voeren die nooit veranderen, optionele publieksgerichtheid en QA-rapportage die gesegmenteerd blijft van live-activiteitgegevens. Met Activity QA kunt u uw [!DNL Target] -activiteiten volledig testen voordat u deze live start.<p>Zie {de verenigbaarheid van de de bibliotheekQA van JavaScript van het 0} Doel {[ en ](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) Voorproef URLs [.](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview) |
| [[!UICONTROL Analytics for Target] (A4T) ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics for Target] (A4T) is een integratie met meerdere oplossingen waarmee u activiteiten kunt maken op basis van [!DNL Analytics] -omzettingsmaatstaven en publiekssegmenten. Met de integratie A4T kunt u analyserapporten gebruiken om uw resultaten te bekijken.<p>Zie [ Gesteunde activiteitentypes ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) en [ stappen van de Implementatie voor een implementatie van SDK van het Web van Adobe Experience Platform ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [ Soorten publiek ](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | Soorten publiek in [!DNL Target] bepalen wie inhoud en ervaringen in een doelactiviteit ziet.<p>Zie [ Gebruik de lijst van Soorten van publiek ](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) en [ combineer veelvoudige soorten publiek ](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [ creeer publiek ](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html) | Het gebruik van publiek dat in [!DNL Adobe Experience Platform] is gemaakt, levert rijkere klantgegevens die tot een onuitvoerbaardere personalisatie leiden.<p>Zie [ publiek van het Gebruik van Adobe Experience Platform ](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#aep). |
| [ de besluiten van de Aanbieding ](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Voeg in [!DNL Adobe Journey Optimizer] gemaakte aanbiedingsbeslissingen toe aan [!DNL Target] -activiteiten (handmatige A/B-test of Experience Targeting) om de volgende beste aanbieding voor uw bezoekers op het web en mobiel te bepalen en te leveren. |
| [ Redirect aanbiedingen - Veelgestelde vragen A4T ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | Met omleidingsvoorstellen leiden bezoekersbrowsers om naar een nieuwe pagina.<p>Zie [ aanbiedingen voor A4T opnieuw richten de [!UICONTROL Adobe Experience Platform Web SDK] steun?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [ Tokens van de Reactie ](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | Met responstokens kunt u [!DNL Target] -gegevens naar Google Analytics en andere integratie van derden verzenden.<p>Zie [ Verzendende gegevens naar Google Analytics via het Web SDK van het Platform ](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) om een codesteekproef van te zien hoe te om deze taak te verwezenlijken. |
| [ enig-paginatoepassing implementatie ](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) in de *[!UICONTROL Platform Web SDK]overzicht* gids. | [!UICONTROL Adobe Experience Platform Web SDK] verstrekt rijke eigenschappen die uw zaken uitrusten om verpersoonlijking op volgende generatie, cliënt-zijtechnologieën zoals single-page toepassingen (SPAs) uit te voeren. |
| [ TLS (de Veiligheid van de Laag van het Vervoer) encryptieveranderingen ](/help/dev/before-implement/tls-transport-layer-security-encryption.md) | TLS (de Veiligheid van de Laag van het Vervoer) helpt u de hoogste veiligheidsnormen handhaven en de veiligheid van klantengegevens bevorderen. |
