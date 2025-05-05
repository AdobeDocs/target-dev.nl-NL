---
keywords: Adobe Experience Platform Web SDK, aep web sdk, web sdk, sdk, adobe Experience cloud, platform edge network, adobe Experience platform edge network, edge network, aep edge network, Adobe Experience Platform Web SDK0
description: Leer hoe u de [!UICONTROL Adobe Experience Platform Web SDK] de interactie met de verschillende diensten van de [!UICONTROL Adobe Experience Cloud] via de [!UICONTROL AEP Edge Network].
title: Hoe kan ik implementeren met de [!UICONTROL Experience Platform Web SDK]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK) is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van [!UICONTROL Adobe Experience Cloud] de interactie met de verschillende diensten van de [!DNL Adobe Experience Cloud] (inclusief [!DNL Target]) via de [!UICONTROL Adobe Experience Platform Edge Network]. Naast de JavaScript-bibliotheek is er een [!UICONTROL Adobe Experience Platform] extensie voor hulp bij uw Web SDK-configuraties.

Raadpleeg de volgende koppelingen in het dialoogvenster *[!UICONTROL Adobe Experience Platform Web SDK]* Help:

* Voor uitgebreide informatie: [Wat is [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=nl-NL)
* Voor specifieke informatie [!DNL Target]: [[!DNL Target] Overzicht](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=nl-NL)

## Tutorials

De volgende zelfstudies helpen u bij uw implementatie:

### Implementeren [!DNL Adobe Experience Cloud] with [!DNL Platform Web SDK]

Leer hoe u implementeert [!DNL Experience Cloud] toepassingen gebruiken [!DNL Adobe Experience Platform Web SDK] with [deze zelfstudie](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=nl-NL). Voor specifieke informatie [!DNL Target], zie de sectie van de zelfstudie getiteld [Instellen [!DNL Target] met Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=nl-NL).

### Migreren [!DNL Target] vanuit om.js 2.*x* tot [!DNL Platform Web SDK]

Leer hoe u uw [!DNL Target] uitvoering vanuit at.js 2.*x* aan de [!DNL Adobe Experience Platform Web SDK] with [deze zelfstudie](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=nl-NL).

## Aanbevolen documentatie

Naast de [!UICONTROL Platform Web SDK] de hierboven vermelde documentatie, onderwerpen in deze gids bevatten ook specifieke informatie over de [!UICONTROL Platform Web SDK] aangezien het betrekking heeft op [!DNL Target] functies en functionaliteit.

| Functie | Beschrijving/koppeling |
| --- | --- |
| [Activiteit QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html?lang=nl-NL) | QA-URL&#39;s gebruiken in [!DNL Target] om gemakkelijke activiteit QA van begin tot eind met voorproefverbindingen uit te voeren die nooit veranderen, facultatieve publiek het richten, en QA rapportering die van levende activiteitengegevens gesegmenteerd blijft. Activiteit QA laat u volledig testen [!DNL Target] activiteiten voordat ze worden gelanceerd.<p>Zie [Compatibiliteit met de QA-modus van de JavaScript-bibliotheek als doel](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html?lang=nl-NL#compatibility) en [Voorvertoning van URL&#39;s](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html?lang=nl-NL#preview). |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=nl-NL) | [!UICONTROL Adobe Analytics for Target] (A4T) is een integratie met meerdere oplossingen waarmee u activiteiten kunt maken op basis van [!DNL Analytics] conversiemetriek en publiekssegmenten. Met de integratie A4T kunt u analyserapporten gebruiken om uw resultaten te bekijken.<p>Zie [Ondersteunde activiteitstypen](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=nl-NL#section_F487896214BF4803AF78C552EF1669AA) en [Implementatiestappen voor een Adobe Experience Platform Web SDK-implementatie](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=nl-NL#platform). |
| [Soorten publiek](https://experienceleague.adobe.com/docs/target/using/audiences/target.html?lang=nl-NL) | Soorten publiek in [!DNL Target] bepalen wie inhoud en ervaringen in een gerichte activiteit ziet.<p>Zie [De lijst Soorten publiek gebruiken](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=nl-NL#use-list) en [Meerdere doelgroepen combineren](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html?lang=nl-NL). |
| [Soorten publiek maken](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=nl-NL) | Het publiek gebruiken dat is gemaakt in [!DNL Adobe Experience Platform] Verstrek rijkere klantengegevens die tot uitvoerigere verpersoonlijking leiden.<p>Zie [Soorten publiek uit Adobe Experience Platform gebruiken](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=nl-NL#aep). |
| [Beslissingen voorstellen](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html?lang=nl-NL) | Aanbiedingsbesluiten toevoegen die zijn gemaakt in [!DNL Adobe Journey Optimizer] tot [!DNL Target] activiteiten (handmatige A/B Test of Experience Targeting) om de volgende beste aanbieding voor uw bezoekers op het web en mobiel te bepalen en te leveren. |
| [Aanbiedingen omleiden - Veelgestelde vragen A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html?lang=nl-NL) | Met omleidingsvoorstellen leiden bezoekersbrowsers om naar een nieuwe pagina.<p>Zie [doet het [!UICONTROL Adobe Experience Platform Web SDK] steun omleidingsaanbiedingen voor A4T?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html?lang=nl-NL#platform) |
| [Reactietokens](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL) | Met responstokens kunt u [!DNL Target] gegevens aan Google Analytics en andere integratie van derden.<p>Zie [Gegevens verzenden naar Google Analytics via Web SDK van Platform](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL#sending-data-to-google-analytics-via-platform-web-sdk) om een codevoorbeeld van te zien hoe te om deze taak te verwezenlijken. |
| [Implementatie van één pagina](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html?lang=nl-NL) in de *[!UICONTROL Platform Web SDK]overzicht* hulplijn. | [!UICONTROL Adobe Experience Platform Web SDK] biedt rijke functies die uw bedrijf uitrusten om personalisatie uit te voeren op de volgende generatie, clienttechnologieën zoals single-page toepassingen (SPA). |
| [TLS (Transport Layer Security)-coderingswijzigingen](../../before-implement/tls-transport-layer-security-encryption.md) | TLS (de Veiligheid van de Laag van het Vervoer) helpt u de hoogste veiligheidsnormen handhaven en de veiligheid van klantengegevens bevorderen. |
